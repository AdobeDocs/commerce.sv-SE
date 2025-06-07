---
title: Utöka och anpassa dataexportdata för SaaS
description: Lär dig hur du utökar och anpassar  [!DNL SaaS Data Export] feed-data.
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
source-git-commit: ac6c690f87e3df2ac4997d80453028829be8e657
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Utöka och anpassa dataexportdata för SaaS

Tillägget [!DNL Commerce Data Export] erbjuder ett sätt att exportera data från programmet [!DNL Commerce] till Commerce Services som Live Search, Catalog Service och Produktrekommendationer. Vid behov kan du utöka och anpassa flödesuppgifterna för att inkludera ytterligare attributdata eller ändra de insamlade uppgifterna.

När du har lagt till attributdata är den tillgänglig från [attributfältet](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type) i GraphQL-schemat för storefront-tjänsten.

>[!NOTE]
>
>Om du lägger till eller ändrar feed-data kan det påverka prestanda och bearbetningslogik på Commerce serverdel. Testa anpassad kod innan du sammanfogar till produktion. Använd API Mesh för att utöka Catalog Service GraphQL-schemat i stället för att lägga till data i serverdelen. Mer konfigurationsinformation finns i [Katalogtjänst och API-nät](../catalog-service/mesh.md).

## Utöka systemattributsdata i produktflödet

Produktflödet innehåller standardsystemattribut som krävs för produktbearbetning eller som ofta används av konsumenterna. Du kan inkludera ytterligare systemattribut i produktflödet genom att lägga till dem i flödet.

Slutför den här åtgärden genom att uppdatera modulen `magento/catalog-data-exporter` och lägga till ytterligare systemattribut i konfigurationsfilen [för beroendeinjicering](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`).

Lägg till attributen i produktattributfrågan (`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`).

**Exempel**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Lägg till produktattribut i Adobe Commerce

Utvecklare kan lägga till produktattribut som är tillgängliga från fältet [produktattribut](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#output-fields) på något av följande sätt:

- Lägg till attributet i Adobe Commerce för inkludering i `products`-feed-data som exporteras till Commerce storefront-tjänster.
- Lägg till attributet dynamiskt under feed-synkroniseringsprocessen med ett plugin-program.

### Lägg till attributet i Adobe Commerce

Du kan lägga till ett produktattribut från Commerce Admin eller programmässigt använda en anpassad PHP-modul för att definiera attributet och uppdatera Adobe Commerce. Att lägga till attributet från Commerce Admin är den enklaste metoden eftersom du kan lägga till attributet och alla metadata som krävs samtidigt. Det nya attributet och dess metadataegenskaper exporteras automatiskt till SaaS-tjänsterna under nästa schemalagda synkronisering.

#### Skapa produktattributet från administratören

1. Skapa attributet från konfigurationssidan för produktattribut i Commerce Admin ([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. Lägg till attributet i en attributuppsättning efter behov.

Se [Skapa produktattribut](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) i *Adobe Commerce Admin Guide*.

#### Skapa produktattributet programmatiskt

Lägg till ett produktattribut programmatiskt genom att skapa en datakorrigering som implementerar `DataPatchInterface` och initiera en kopia av klassen `EavSetup Factory` i konstruktorn för att konfigurera attributalternativen.

När du definierar attributalternativen är alla attributparametrar utom `type`, `label` och `input` valfria. Definiera följande ytterligare parametrar och eventuella andra som skiljer sig från standardinställningarna.

- **`user_defined`=`1`** - Exportera attributet till butikstjänster under datasynkronisering
- **`used_in_product_listing`=`1`** - Gör attributet tillgängligt i produktlistans databasfråga

Mer information om hur du skapar datakatchar finns i [Utveckla data och schemapatchar](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) i *Utvecklarhandbok för PHP*.

### Lägg till produktattributet dynamiskt

Mer information om hur du skapar produktattribut dynamiskt utan att införa nya EAV-attribut finns i [Lägg till attribut dynamiskt](add-attribute-dynamically.md).
