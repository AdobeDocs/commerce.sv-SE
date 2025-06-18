---
title: Anpassad automatisk matchning
description: Läs om hur den anpassade automatiska matchningen är särskilt användbar för handlare med komplex matchningslogik eller de som förlitar sig på ett tredjepartssystem som inte kan fylla i visuella produktmetadata i AEM Assets.
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Anpassad automatisk matchning

Om standardstrategin för automatisk matchning (**OTB automatisk matchning**) inte är anpassad efter dina specifika affärskrav väljer du det anpassade matchningsalternativet. Det här alternativet stöder användningen av [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) för att utveckla ett anpassat matchningsprogram som hanterar komplex matchningslogik, eller resurser från ett tredjepartssystem som inte kan fylla i visuella produktmetadata i AEM Assets.

## Konfigurera anpassad automatisk matchning

1. Gå till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]** i Commerce Admin.

1. Välj **[!UICONTROL Custom Matcher]** som matchningsregel.

1. När du väljer den här matchande regeln visar Admin ytterligare fält för att konfigurera **slutpunkterna** och de nödvändiga **autentiseringsparametrarna** för den anpassade matchningslogiken.

## API-slutpunkter för anpassad matchning

När du skapar ett anpassat matchningsprogram med [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank} måste följande slutpunkter visas:

* **App Builder-resurs till produkt-URL**-slutpunkt
* **App Builder-produkt till resurs-URL** slutpunkt

### App Builder-resurs till produkt-URL-slutpunkt

Den här slutpunkten hämtar listan med SKU:er som är associerade med en given resurs:

#### Exempel på användning

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**Begäran**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `assetId` | Sträng | Representerar det uppdaterade resurs-ID:t |

**Svar**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### App Builder product to asset URL endpoint

Den här slutpunkten hämtar listan över resurser som är associerade med en given SKU:

#### Exempel på användning

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**Begäran**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `productSKU` | Sträng | Representerar den uppdaterade produktens SKU |

**Svar**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

>[!TIP]
>
> Använd de [Commerce-resursroller](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) som stöds, som `thumbnail`, `image`, `small_image` och `swatch_image`, i nyckeln `asset_roles`.
