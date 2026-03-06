---
title: Produktbilder med AEM Assets
description: Lär dig hur du använder AEM Assets för produktbilder i  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och [!DNL Adobe Commerce Optimizer] projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Produktbilder med AEM Assets

Med produktvisuella effekter kan [!DNL Adobe Commerce Optimizer] handlare hantera produktbilder via Adobe Experience Manager (AEM) Assets. Den här integreringen ger ett smidigt arbetsflöde för synkronisering av högkvalitativa produktbilder från AEM Assets till din [!DNL Commerce Optimizer]-katalog med kataloglager.

## Viktiga fördelar

* **Centraliserad resurshantering**: Hantera alla produktbilder i AEM Assets, resurshanteringslösningen för företag.
* **Automatisk synkronisering**: Produktbilder synkroniseras automatiskt när resurser godkänns eller uppdateras i AEM Assets.
* **Dynamisk medieleverans**: Utnyttja Dynamic Media med OpenAPI-funktioner för optimerad bildleverans.
* **Kataloglager**: Produktbilder används som ett kataloglager så att du kan täcka över AEM Assets-bilder i din baskatalog.

## Så här fungerar det

Integreringen har två huvudflöden:

* **Från AEM Assets**: När en resurs har godkänts, avvisats eller tagits bort flödar händelsen genom Adobe Pipeline till Assets integreringstjänst. Tjänsten matchar resurser mot produkter med en `match-by-SKU` eller en anpassad matchningsstrategi och skickar sedan `product-asset`-mappningarna till [!DNL Commerce Optimizer], där de lagras som produktlager.

* **Från ACO**: När en produkt uppdateras i [!DNL Commerce Optimizer] flödar händelsen genom Adobe Pipeline till Assets Integration Service. Tjänsten synkroniserar alla matchande resursmappningar tillbaka till ACO.

De uppdaterade bilderna finns tillgängliga via storefront API:er (Catalog Service, Live Search, Product Recommendations).

### Source och lagerkonfiguration

Bilder från AEM Assets importeras som ett kataloglager med följande källkonfiguration:

> Exempel på en källkonfiguration

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

Den här konfigurationen ser till att AEM Assets-bilder används som en övertäckning i din basproduktkatalog.

## Förutsättningar

Innan du aktiverar produktvisningar måste du kontrollera att du uppfyller [kraven för Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md#prerequisites).

## Inställningar

Om du vill aktivera integreringen [skapar du en supportanmälan](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) med dina [!DNL Commerce Optimizer]- och AEM Assets-uppgifter. Adobe Support konfigurerar integreringen och registrerar din klient hos Assets Integration Service.

Se [Konfigurera AEM Assets för Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) för information om introduktion.

### Konfigurera AEM Assets-metadata

Om du vill aktivera automatisk produktmatchning konfigurerar du dina resurser i AEM Assets med Commerce-metadata.

Se [Konfigurera AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets) för de metadatafält och steg som krävs.

## Använda produktbilder

Hantera dina produktbilder via AEM Assets när integreringen har konfigurerats.

### Lägg till bilder i produkter

1. Ladda upp bilder till AEM Assets.

1. Lägg till Commerce-metadata i resursen. Se [Använda metadata på resurser](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets).

1. Godkänn tillgången för leverans. Resursen måste ha statusen **Approved** för att utlösa synkronisering.

1. Bilden synkroniseras automatiskt till [!DNL Commerce Optimizer].

### Använda lagret AEM-Assets

Om du vill visa AEM Assets-bilder i din butik [tilldelar du lagret `AEM-Assets` till katalogvyn](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Mer som detta

* [Kataloglager](catalog-layer.md)
* [Katalogvyer](catalog-view.md)
* [AEM Assets Integreringshandbok](../../aem-assets-integration/overview.md)
