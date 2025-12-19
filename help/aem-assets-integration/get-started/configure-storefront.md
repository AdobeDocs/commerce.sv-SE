---
title: Konfigurera din Storefront
description: Lär dig koppla din Edge Delivery Services-butik till din AEM Assets-integrering.
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Konfigurera din Storefront

I AEM Assets-integreringen visas produktbilder som hanteras i AEM Assets i stället för bilder som lagras i Adobe Commerce. Integreringen ger bättre bildhanteringsfunktioner, inklusive avancerad optimering, beskärning och leverans via Adobe Content Delivery Network (CDN).

Om du vill aktivera integreringen i Commerce StoreFront som drivs av Edge Delivery Services uppdaterar du konfigurationsfilen för storefront (`config.json`) så att parametern `"commerce-assets-enabled": true` läggs till.

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Commerce-insticksprogram identifierar automatiskt konfigurationen av `commerce-assets-enabled` och justerar bildhanteringen därefter.

Om du vill ha mer information om hur du använder AEM Assets med Commerce Storefront från Edge Delivery Services kan du slutföra konfigurationen av Store som beskrivs i avsnittet [AEM Assets-integrering](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=sv-SE) i dokumentationen för *Adobe Commerce Storefront* .
