---
title: Lägg till produktattribut dynamiskt
description: Lär dig hur du lägger till anpassade produktattribut i dataexportflödet dynamiskt under datasynkroniseringsprocessen.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Lägg till produktattribut dynamiskt under datasynkronisering

Du kan utöka produktattribut utan att registrera dem i Adobe Commerce genom att skapa ett plugin-program som lägger till attributen under datasynkroniseringsprocessen.

>[!NOTE]
>
>Det bästa sättet att utöka produktattribut är att [lägga till dem i Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) där du kan konfigurera och hantera dem från Commerce Admin. Lägg bara till dem dynamiskt om du bara behöver dem för Commerce butikstjänster och inte vill registrera dem i Adobe Commerce. Du kan också hantera anpassade attribut med [API Mesh med katalogtjänsten](../catalog-service/mesh.md) för att utöka GraphQL-schemat för katalogtjänsten.

## Lägg till produktattribut

Skapa ett plugin-program som lägger till `customer_attribute` i klassen `Magento\CatalogDataExporter\Model\Provider\Product\Attributes`.

1. Uppdatera konfigurationsfilen [för beroendeinmatning](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) för att definiera plugin-programmet.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. Skapa plugin-programmet.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(Attributes $subject, array $result, $arguments): array
         {
              $productIds = \array_column($arguments, 'productId');
   
              foreach ($productIds as $productId) {
                    $result[] = [
                         'productId' => $productId,
                         // "storeViewCode" must be specified for products where the customer attribute value should be set
                         'storeViewCode' => 'default',
                         'attributes' => [
                              // specify the customer attribute code
                              'attributeCode' => 'customer_attribute',
                              // provide single or multiple values for the attribute
                              'value' => [
                                    rand(41,43)
                              ]
                         ]
                    ];
              }
   
              return $result;
         }
    }
   ```

   När du har lagt till plugin-programmet synkroniseras ändringarna med anslutna butikstjänster under nästa schemalagda synkronisering. Om du vill skicka uppdateringarna direkt använder du följande CLI-kommando för att starta synkroniseringsprocessen manuellt.

   ```
   bin/magento saas:resync --feed=products
   ```

## Deklarera metadata för anpassade produktattribut

Om du dynamiskt skapar ett anpassat produktattribut och vill använda det för visning, sökning eller filtrering i butikstjänster lägger du till metadata för produktattributet för att konfigurera storefront-beteendet.

1. Uppdatera konfigurationsfilen [för beroendeinjicering](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) för att definiera plugin-programmet för produktattributets metadata.

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Skapa plugin-programmet till följande provider `\Magento\CatalogDataExporter\Model\Provider\ProductMetadata`.

   Kontrollera `ProductAttributeMetadata` i `vendor/magento/module-catalog-data-exporter/etc/et_schema.xml` om det finns obligatoriska fält.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   När du har lagt till plugin-programmet synkroniseras ändringarna med anslutna butikstjänster under nästa schemalagda synkronisering. Om du vill skicka uppdateringarna direkt använder du följande CLI-kommando för att starta synkroniseringsprocessen manuellt.

   ```
   bin/magento saas:resync --feed=productattributes
   ```
