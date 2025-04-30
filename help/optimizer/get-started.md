---
title: Kom igång med  [!DNL Adobe Commerce Optimizer]
description: Lär dig hur du kommer igång med  [!DNL Adobe Commerce Optimizer].
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Kom igång

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

Den här guiden hjälper dig att skapa och arbeta med en [!DNL Adobe Commerce Optimizer]-instans.

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/services/cloud/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## Provisionering

När [!DNL Adobe Commerce Optimizer]-instanserna är klara får du följande slutpunkter från [!DNL Adobe Commerce Optimizer]-provisioneringsteamet:

| Objekt | Exempel-URL | Syfte |
|---|---|---|
| [!DNL Adobe Commerce Optimizer]-gränssnitt | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Använd Commerce Optimizer-gränssnittet för att hantera din katalog över:<br>1. Marknadsföringsregler (produktupptäckt, produktrekommendationer).<br>2. Kataloghantering (skapa kanaler och principer).<br>3. Data Insights (Visa din status för att hämta katalogdata). |
| Storefront-API:er | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Få tillgång till de API:er som behövs för att konfigurera din Commerce Store som drivs av Edge Delivery Services. |
| API:er för inhämtning av katalogdata | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | Få tillgång till de API:er som behövs för att importera katalogdata. |

Som deltagare för tidig åtkomst får du ett e-postmeddelande med en säker länk som tillsammans med din IMS-token låter dig logga in på [!DNL Adobe Commerce Optimizer] eller göra API-anrop.

## Konfigurera butiken

Nu när du har en [!DNL Adobe Commerce Optimizer]-instans är du redo att fortsätta [konfigurera](./storefront.md) din Commerce Storefront som drivs av Edge Delivery Services.

## Tillgängliga katalogdata för deltagare med tidig åtkomst

Som en tidig deltagare för åtkomst innehåller instansen [!DNL Adobe Commerce Optimizer] data för modellkatalogen baserat på [Carvelos användningsfall](./use-case/admin-use-case.md). Mock-data, tillsammans med vissa förkonfigurerade kanaler och principer, hjälper dig att bekanta dig med användargränssnittet för [!DNL Adobe Commerce Optimizer].

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
