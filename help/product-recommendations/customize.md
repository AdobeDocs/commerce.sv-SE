---
title: Anpassa
description: Lär dig hur du anpassar dina produktrekommendationer.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Anpassa

När du installerar modulen Produktrekommendationer skapar Adobe Commerce katalogen `ProductRecommendationsLayout`. Den här katalogen innehåller mallfiler som du kan anpassa för att ändra hur rekommendationerna visas i din butik. Du kan ändra eller åsidosätta följande mall:

`<your theme>/Magento_ProductRecommendationsLayout/web/template/recommendations.html`

Mer information om hur du ändrar mallfiler finns i [Mallanpassning](https://developer.adobe.com/commerce/frontend-core/guide/templates/walkthrough/) i Utvecklarhandbok för Edge.

Om du ändrar filen `recommendations.html` måste du bevara följande taggar i filen för att vara säker på att Adobe Commerce kan samla in rekommendationsmått från din butik:

| Tagg | Använd |
|---|---|
| `<div data-bind="attr : {'data-unit-id' : unitId }"...</div>` | Samlar in visningshändelser. |
| `<a data-bind="attr : {'data-sku' : sku, 'data-unit-id'}"...</a>` | Samlar in klickningshändelser. <br/>**Obs!** Om du lägger till ankartaggar måste du ta med dessa attribut. |

Förutom filen `recommendations.html` innehåller katalogen `ProductRecommendationsLayout` följande underkataloger:

| Katalog | Syfte |
|---|---|
| `layout` | Innehåller `*.xml` filer för varje sidtyp |
| `templates` | Innehåller filer som anropar hämtningen och återger skript |
| `web/js` | Innehåller JavaScript-filer som hämtar och återger rekommendationer för din butik |
| `web/template` | Innehåller mallen för modulen `magento/product-recommendations` |

## Placering av rekommendationsenhet

När du [skapar](create.md) en rekommendation anger du [platsen](placement.md) där den ska visas på sidan. En rekommendationsenhet kan placeras antingen högst upp eller längst ned i behållaren med huvudinnehåll. Du kan dock anpassa placeringen. Om du skapar en innehållstyp för en rekommendation i Page Builder använder du verktygen i Page Builder för att placera rekommendationsenheten på sidan. För alla andra sidtyper redigerar du de `*.xml`-filer som genereras när rekommendationen skapas.

1. Ändra till katalogen `layout`:

   ```bash
   cd `<your theme>/Magento_ProductRecommendationsLayout/layout`
   ```

   I följande tabell visas de XML-filer som finns i den här katalogen:

   | Filnamn | Sida |
   |---|---|
   | `catalog_category_view.xml` | Kategori |
   | `catalog_product_view.xml` | Produktinformation |
   | `checkout_cart_index.xml` | Kundvagn |
   | `checkout_onepage_success.xml` | Utcheckning |
   | `cms_index_index.xml` | Startsida |

   >[!NOTE]
   >
   >Filnamnen i katalogen `layout` kan vara annorlunda om ditt arkiv använder tillägg från tredje part.

1. Ändra filen `catalog_product_view.xml` så att rekommendationsenheten visas efter produktbilden på produktinformationssidan. Innan du anpassar XML-filen bör du ta en titt på filen och förstå vilka avsnitt du behöver ändra:

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="main.content">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   I ovanstående kodutdrag anger referensblocket `main.content` att rekommendationsenheten kommer att placeras någonstans i förhållande till det elementet. Dess `block`-element innehåller attributet `after="-"` som anger att rekommendationsenheten ska visas på sidan efter huvudinnehållsblocket.

1. Låt oss ändra den här filen genom att ange ett annat innehållsblock.

   Ändra referensblocket `name` från `main.content` till `product.info.media`.

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="product.info.media">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   Ändringen resulterar i att din rekommendationsenhet visas efter produktbilden på produktinformationssidan. Om du vill att rekommendationsenheten ska visas före `product.info.media` ändrar du attributet `after="-"` till `before="-"`. Argumentet `pagePlacement` är ett internt argument som inte ska ändras.

Mer information om de olika blocktyperna på sidan finns i [layoutöversikt](https://developer.adobe.com/commerce/frontend-core/guide/layouts/).

## Anpassade produktattribut

Utvecklare behöver ofta tillgång till anpassade produktattributvärden i rekommendationsenheter på butiker så att de kan lägga till visuella behandlingar till produkter som baseras på dessa attribut.

Om din butik till exempel säljer vissa ekologiska produkter kan du ha ett anpassat attribut för de produkter som anger dem som `Organic = Yes`. Du kan behöva ha tillgång till det här attributvärdet i butiken så att du kan ge dessa produkter visuell specialbehandling när de visas i Rekommendationer. På samma sätt kan du använda dessa anpassade produktattributvärden för att märka produkter eller skapa egna logiska effekter i presentationsskiktet på webbplatsen.

![Lägg till märke](assets/unit-custom.png)

Om du vill vara säker på att ett anpassat produktattribut är tillgängligt när du återger rekommendationsenheten på sidan anger du egenskapen `Used in Product Listing` till `Yes` på sidan [Produktattribut](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html) i Admin.

När den här egenskapen anges innehåller JSON-nyttolasten ett `attributes`-objekt som innehåller en array med attributkoder och värden. Du kan sedan använda en anpassad storefront-formatering som baseras på dessa attributvärden, som att lägga till speciella visuella behandlingar eller emblem som nämns ovan.

>[!NOTE]
>
>Det kan ta upp till en timme innan produktattributändringar visas i JSON-nyttolasten.
