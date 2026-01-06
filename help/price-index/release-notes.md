---
title: Versionsinformation för [!DNL Catalog Adapter]
description: Den senaste versionsinformationen för  [!DNL Catalog Adapter]  för Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Versionsinformation om [!DNL Catalog Adapter] tillägg

De här versionsinformationen beskriver de senaste versionerna av tillägget [!DNL Catalog Adapter]. Support ges för den aktuella större versionen. Versionsinformation för äldre versioner finns som referens.

Bland uppdateringarna finns:

![Nya](../assets/new.svg) nya funktioner
![Korrigera ](../assets/fix.svg) Korrigeringar och förbättringar
![Fel](../assets/bug.svg) Kända fel


>[!NOTE]
>
>[Katalogkortstillägget](catalog-adapter.md) inaktiverar prisindexering för Adobe Commerce. Om du har installerat den kan du kontrollera vilken version som är installerad på datorn med hjälp av Composer. I vissa fall kanske du vill uppgradera katalogkortstillägget på datorn för att kunna hämta korrigeringar eller nya funktioner utan att uppdatera Commerce tjänstversion.

## Aktuell huvudversion

## 1.0.10 Utgåva

![Åtgärdade](../assets/fix.svg) ett problem där prisfrågor för importerade eller nyligen skapade paketprodukter kunde resultera i interna serverfel eftersom systemet försökte använda en sammanfogad SKU för sökning i stället för rätt, giltig SKU. Prisfrågor för paketprodukter använder nu rätt SKU och löser dem korrekt.<!--MDEE-1040-->

## 1.0.9 Utgåva

![Korrigera](../assets/fix.svg) Kompatibilitet för PHP 8.4 har lagts till. <!--MDEE-941-->

## 1.0.8 Utgåva

![Åtgärdade](../assets/fix.svg) ett fel som orsakade ett fel i undantagsloggen när konfigurerbara produktvarianter med numeriska SKU:er lades till i önskelistan. <!--MDEE-876-->
