---
title: Anpassad automatisk matchning
description: Läs om hur anpassad automatisk matchning är särskilt användbar för handlare med komplex matchningslogik eller de som förlitar sig på ett tredjepartssystem som inte kan fylla i metadata i AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Anpassad automatisk matchning

Om standardstrategin för automatisk matchning (**OTB automatisk matchning**) inte är anpassad efter dina specifika affärskrav väljer du det anpassade matchningsalternativet. Det här alternativet stöder användningen av [Adobe Developer App Builder](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) för att utveckla ett anpassat matchningsprogram som hanterar komplex matchningslogik, eller resurser från ett tredjepartssystem som inte kan fylla i metadata i AEM Assets.

## Konfigurera anpassad automatisk matchning

1. Gå till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]** i Commerce Admin.

1. Välj **[!UICONTROL Custom Matcher]** som matchningsregel.

1. När du väljer den här matchande regeln visar Admin ytterligare fält för att konfigurera **slutpunkterna** och de nödvändiga **autentiseringsparametrarna** för den anpassade matchningslogiken.

## API-slutpunkter för anpassad matchning

När du skapar ett anpassat matchningsprogram med [App Builder](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank} måste följande slutpunkter visas:

* **App Builder-resurs till produkt-URL**-slutpunkt
* **App Builder-produkt till resurs-URL** slutpunkt

### App Builder-resurs till produkt-URL-slutpunkt

Den här slutpunkten hämtar listan med SKU:er som är associerade med en given resurs:

#### Exempel på användning

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Begäran**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `assetId` | Sträng | Representerar det uppdaterade resurs-ID:t |
| `eventData` | Sträng | Returnerar datanyttolasten som är associerad med `assetId` |

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

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Begäran**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `productSKU` | Sträng | Representerar den uppdaterade produktens SKU. |
| `asset_matches` | Sträng | Returnerar alla resurser som är associerade med en specifik `productSku`. |

Parametern `asset_matches` innehåller följande attribut:

| Attribut | Datatyp | Beskrivning |
| --- | --- | --- |
| `asset_id` | Sträng | Representerar det uppdaterade resurs-ID:t. |
| `asset_roles` | Sträng | Returnerar alla tillgängliga resursroller. Använder [Commerce-resursroller som stöds](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) som `thumbnail`, `image`, `small_image` och `swatch_image`. |
| `asset_format` | Sträng | Tillhandahåller de tillgängliga formaten för resursen. Möjliga värden är `image` och `video`. |
| `asset_position` | Sträng | Visar tillgångens position. |

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
