---
title: Anpassad automatisk matchning
description: Läs om hur anpassad automatisk matchning är särskilt användbar för handlare med komplex matchningslogik eller de som förlitar sig på ett tredjepartssystem som inte kan fylla i metadata i AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: 6e8d266aeaec4d47b82b0779dfc3786ccaa7d83a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---

# Anpassad automatisk matchning

Om standardstrategin för automatisk matchning (**OTB automatisk matchning**) inte är anpassad efter dina specifika affärskrav väljer du det anpassade matchningsalternativet. Det här alternativet stöder användningen av [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) för att utveckla ett anpassat matchningsprogram som hanterar komplex matchningslogik, eller resurser från ett tredjepartssystem som inte kan fylla i metadata i AEM Assets.

## Konfigurera anpassad automatisk matchning

1. Gå till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]** i Commerce Admin.

1. Välj **[!UICONTROL Custom Matcher]** som matchningsregel.

1. När du väljer den här matchande regeln visar Admin ytterligare fält för att konfigurera **slutpunkterna** och de nödvändiga **autentiseringsparametrarna** för den anpassade matchningslogiken.

### workspace.json

I fältet **[!UICONTROL Adobe I/O Workspace Configuration]** finns ett smidigt sätt att konfigurera din anpassade matchare genom att importera konfigurationsfilen för App Builder `workspace.json`.

Du kan hämta filen `workspace.json` från [Adobe Developer Console](https://developer.adobe.com/console). Filen innehåller alla autentiseringsuppgifter och konfigurationsinformation för din App Builder-arbetsyta.

+++Exempel `workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. Dra och släpp din `workspace.json`-fil från ditt App Builder-projekt till fältet **[!UICONTROL Adobe I/O Workspace Configuration]**. Du kan också klicka för att bläddra och markera filen.

![Workspace-konfiguration](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. Systemet automatiskt:

   * Validerar JSON-strukturen
   * Extraherar och fyller i OAuth-autentiseringsuppgifter
   * Hämtar tillgängliga körningsåtgärder för arbetsytan
   * Fyller i listrutealternativ för fälten **[!UICONTROL Product to Asset URL]** och **[!UICONTROL Asset to Product URL]**

1. Välj lämpliga körningsåtgärder i listrutorna för varje flöde.

1. Klicka på **[!UICONTROL Save Config]**.

## API-slutpunkter för anpassad matchning

När du skapar ett anpassat matchningsprogram med [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank} måste följande slutpunkter visas:

* **App Builder-resurs till produkt-URL**-slutpunkt
* **App Builder-produkt till resurs-URL** slutpunkt

### App Builder-resurs till produkt-URL-slutpunkt

Den här slutpunkten hämtar listan med SKU:er som är associerade med en given resurs:

#### Exempel på användning

```javascript
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

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Begäran**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `assetId` | Sträng | Representerar det uppdaterade resurs-ID:t. |
| `eventData` | Sträng | Returnerar datanyttolasten som är associerad med resurs-ID:t. |

**Svar**

```json
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail", "image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ],
  "skip": false
}
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `asset_id` | Sträng | Det resurs-ID som matchas. |
| `product_matches` | Array | Lista över produkter som är associerade med tillgången. |
| `skip` | Boolean | (Valfritt) När `true` inträffar, hoppar regelmotorn över synkronisering för den här resursen (ingen produktmappningsuppdatering). När `false` eller utelämnas körs normal bearbetning. Se [Hoppa över synkroniseringsbearbetning](#skip-sync-processing). |

### App Builder product to asset URL endpoint

Den här slutpunkten hämtar listan över resurser som är associerade med en given SKU:

#### Exempel på användning

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Begäran**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `productSKU` | Sträng | Representerar den uppdaterade produktens SKU. |
| `eventData` | Sträng | Returnerar den datanyttolast som är associerad med produkt-SKU:n. |

**Svar**

```json
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail", "image"],
      "asset_position": 1,
      "asset_format": "image"
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"],
      "asset_position": 2,
      "asset_format": "image"
    }
  ],
  "skip": false
}
```

| Parameter | Datatyp | Beskrivning |
| --- | --- | --- |
| `product_sku` | Sträng | Produkt-SKU som matchas. |
| `asset_matches` | Array | Lista över resurser som är associerade med produkten. |
| `skip` | Boolean | (Valfritt) När `true` inträffar, hoppar regelmotorn över synkronisering för den här produkten (ingen resursmappningsuppdatering). När `false` eller utelämnas körs normal bearbetning. Se [Hoppa över synkroniseringsbearbetning](#skip-sync-processing). |

Parametern `asset_matches` innehåller följande attribut:

| Attribut | Datatyp | Beskrivning |
| --- | --- | --- |
| `asset_id` | Sträng | Resurs-ID. |
| `asset_roles` | Array | Resursroller. Använder [Commerce-resursroller som stöds](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) som `thumbnail`, `image`, `small_image` och `swatch_image`. |
| `asset_format` | Sträng | Resursformatet. Möjliga värden är `image` och `video`. |
| `asset_position` | Nummer | Positionen för resursen i produktgalleriet. |

## Hoppa över synkroniseringsbearbetning

Parametern `skip` gör att din anpassade matchare kan kringgå synkroniseringsbearbetning för specifika resurser eller produkter.

När ditt App Builder-program returnerar `"skip": true` i svaret skickar regelmotorn inte uppdateringar eller tar bort API-begäranden till Commerce för den resursen eller produkten. Optimeringen minskar onödiga API-anrop och förbättrar prestandan.
