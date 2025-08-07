---
title: Lägg till anpassade attribut i order
description: Lär dig hur du lägger till anpassade orderattribut i dina back office-data och skickar dessa attribut till Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
exl-id: dcd0b9e7-8d36-4bde-b226-ac19e83f00e4
source-git-commit: 5b1387e18e059c938aca600cc31951a3f5289e7e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 2%

---

# Lägg till anpassade attribut i order

I den här artikeln får du lära dig hur du lägger till anpassade attribut till back office-händelser. Med anpassade attribut kan ni samla in omfattande datainsikter för att förbättra analysen och ytterligare skapa personaliserade upplevelser för era kunder.

>[!NOTE]
>
>Lär dig hur du kan [lägga till anpassade identiteter](custom-identities.md) i profiler.

Anpassade attribut stöds på två nivåer:

- Ordernivå
- Orderartikelnivå

>[!NOTE]
>
>Adobe [!DNL Commerce] stöder anpassade attribut som har datatypen sträng, Boolean eller date.

Om du lägger till anpassade attribut till Office-händelser måste du:

1. Skapa ett projekt i din [!DNL Commerce]-installation.
1. Uppdatera ditt schema så att de nya anpassade attributen kan importeras korrekt till Experience Platform.
1. I Admin bekräftar du att de anpassade attributen hämtas och skickas till Experience Platform.

>[!IMPORTANT]
>
>Katalogstrukturen och kodexemplen nedan visar hur du kan implementera anpassade attribut. Den katalogstruktur och kod som krävs beror på din butikskonfiguration och -miljö.

## Steg 1: Skapa katalogstrukturen

1. Navigera till katalogen `app/code` i installationen av [!DNL Commerce] och skapa en modulkatalog. Till exempel: `Magento/AepCustomAttributes`. Den här katalogen innehåller de filer som behövs för dina anpassade attribut.
1. Skapa en underkatalog med namnet `etc` i modulkatalogen. Katalogen `etc` innehåller filerna `module.xml`, `query.xml`, `di.xml` och `et_schema.xml`.

## Steg 2: Definiera beroenden och installationsversionen

Skapa en `module.xml`-fil som definierar beroenden och installationsversionen. Exempel:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_AepCustomAttributes">
        <sequence>
            <module name="Magento_SalesOrderDataExporter"/>
        </sequence>
    </module>
</config>
```

## Steg 3: Hämta försäljningsorderdata

Skapa en `query.xml`-fil som hämtar försäljningsorderdata. Exempel:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:Module:Magento_QueryXml:etc/query.xsd">
  <query name="salesOrdersV2">
    <source name="sales_order">
      <link-source name="sales_order_inventory_source" link-type="inner">
        <attribute name="inventory_source_code" alias="inventory_source" />
        <using glue="and">
          <condition attribute="order_id" operator="eq" type="identifier">entity_id</condition>
         </using> 
        </link-source>
    </source>
  </query>
  </config>
```

## Steg 4: Ställa in beroendeinjektionen

Skapa en `di.xml`-fil som ställer in beroendeinjektionen. Exempel:

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
      <type name="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">commerceOrderId</argument>
          </arguments>
      </type>
      <type name="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">entityId</argument>
          </arguments>
      </type>
      <type name="Magento\DataServices\Model\ProductContext">
          <plugin name="product-context-plugin" type="Magento\AepCustomAttributes\Plugin\Model\ProductContext"/>
      </type>
  </config>
```

## Steg 5: Definiera de tjänster som används för beroendeinjektionen

Skapa en `et_schema.xml`-fil som definierar de tjänster som används för beroendeinjektionen. Exempel:

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_DataExporter:etc/et_schema.xsd">
      <record name="OrderV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
              <using field="commerceOrderId"/>
          </field>
      </record>
      <record name="OrderItemV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
              <using field="entityId"/>
          </field>
      </record>
  </config>
```

## Steg 6: Skapa en katalog för PHP-filerna

Skapa en katalog med namnet `etc` på samma nivå som katalogen `Module/Provider`. Den här katalogen innehåller `OrderCustomAttributes`- och `OrderItemCustomAttributes` PHP-filerna.

## Steg 7: Definiera OrderCustomAttributes

Skapa en `OrderCustomAttributes.php`-fil som definierar anpassade attribut för ordningen. Exempel:

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class CustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param string $usingField
   * @param Json $jsonSerializer
   */
  public function __construct(
      string $usingField,
      Json $jsonSerializer
  ) {
      $this->usingField = $usingField;
      $this->jsonSerializer = $jsonSerializer;
  }

  /**
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];

      /**
       * Entity IDs
       */
      $ids = array_column($values, $this->usingField);

      foreach ($this->flatten($values) as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];

          if (isset($row)) {
              $unserializedData['order_channel'] = 'order_channel';
              $unserializedData['order_status'] = 'order_status';

              $additionalInformation = [];
              foreach ($unserializedData as $name => $value) {
                  $additionalInformation[] = [
                      'name' => $name,
                      'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
                  ];
              }
              foreach ($additionalInformation as $information) {
                  $output[] = [
                      'additionalInformation' => $information,
                      $this->usingField => $row[$this->usingField],
                  ];
              }
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Steg 8: Definiera OrderItemCustomAttributes

Skapa en `OrderItemCustomAttributes.php`-fil som definierar anpassade attribut för orderobjektet. Exempel:

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class OrderItemCustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param Json $jsonSerializer
   * @param string $usingField
   */
  public function __construct(
      Json $jsonSerializer,
      string $usingField
  ) {
      $this->jsonSerializer = $jsonSerializer;
      $this->usingField = $usingField;
  }

  /**
   * Getting additional attributes data.
   *
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];
      $values = $this->flatten($values);

      foreach ($values as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];
          $unserializedData['product_brand'] = implode(',', ['label 1', 'label 2']);

          $additionalInformation = [];
          foreach ($unserializedData as $name => $value) {
              $additionalInformation[] = [
                  'name' => $name,
                  'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
              ];
          }
          foreach ($additionalInformation as $information) {
              $output[] = [
                  'additionalInformation' => $information,
                  $this->usingField => $row[$this->usingField],
              ];
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Steg 9: Skapa en katalog för productContext-filen

Skapa en katalog med namnet `etc` på samma nivå som katalogen `Plugin/Module`. Den här katalogen innehåller filen `ProductContext.php`.

## Steg 10: Definiera klassen ProductContext

Skapa en fil med namnet `ProductContext.php` som definierar klassen `ProductContext`. Exempel:

```php
<?php>
namespace Magento\AepCustomAttributes\Plugin\Model;
use Magento\Catalog\Model\Product;
use Magento\DataServices\Model\ProductContext as Subject;
use Magento\Framework\App\ResourceConnection;

class ProductContext
{
    private ?array $brandCache = [];
    public function __construct(
        private ResourceConnection $resourceConnection ) {
    }  

    public function afterGetContextData(Subject $subject, array $result Product $product)
    {
        $brand = $product->getCustomAttribute('cust_attr1');
        if (!empty($brand) && $brand->getValue()) {
            $result['brands'] = ['brand_label_1', 'brand_label_2'];
            }
            return $result;
      }
  }
```

## Steg 1: Registrera modulen

Skapa en `etc`-fil som registrerar modulen på samma nivå som katalogen `registration.php`. Exempel:

```php
<?php>
declare(strict_types=1);

use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Magento_AepCustomAttributes',
    __DIR__
);
```

## Steg 12: Utöka ditt befintliga XDM-schema

Om du vill vara säker på att de nya attributen för anpassad ordning kan importeras av ditt [!DNL Commerce]-schema i Experience Platform, måste du utöka schemat så att det omfattar dessa anpassade fält.

Om du vill lära dig hur du utökar ett befintligt XDM-schema så att det inkluderar dessa anpassade fält kan du läsa artikeln [Skapa och redigera scheman i användargränssnittet](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas#custom-fields-for-standard-groups) i Experience Platform-dokumentationen. Fältet Klient-ID genereras dynamiskt, men fältstrukturen ska likna exemplet i Experience Platform-dokumentationen.

>[!IMPORTANT]
>
>Anpassade XDM-attribut måste matcha de attribut som skickas från [!DNL Commerce].

Lägg till ett fält för ordernivå i `commerce.order`:

![Beställningsnivå](assets/order-level.png)

Lägg till fält för orderobjektnivå i `productListItems`:

![Beställningsobjektnivå](assets/order-item-level.png)

## Steg 12: Bekräfta att data hämtas

Visa fliken [Dataanpassning](connect-data.md#data-customization) i Admin för att bekräfta att anpassade attributdata hämtas och skickas till Experience Platform.

### Felsökning

Om meddelandet `No custom order attributes found.` visas på fliken **[!UICONTROL Data Customization]** bekräftar du följande:

1. Du har slutfört kraven för att aktivera [Data Connector-tillägget](overview.md#prerequisites).
1. Du har konfigurerat [anpassade orderattribut](#add-custom-order-attributes).
1. Minst en orderhändelse har genererats.
