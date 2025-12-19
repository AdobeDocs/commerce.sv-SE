---
title: Automatisk standardmatchning
description: Lär dig hur standardregeln för automatisk matchning möjliggör smidig synkronisering mellan Adobe Commerce och AEM Assets-integreringen, vilket säkerställer att resurser automatiskt länkas till rätt försäljningsenheter.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Automatisk standardmatchning

AEM Assets-integreringen för Commerce har en automatisk matchningsmekanism (**[!UICONTROL Match by product SKU]**) som är standard baserat på metadatakonfigurationen för **AEM Assets**. Den här regeln möjliggör smidig synkronisering mellan **Adobe Commerce** och **AEM Assets**, vilket säkerställer att resurser automatiskt länkas till rätt försäljningsenheter.

## Konfigurera den automatiska matchningsmekanismen

1. Gå till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]** i Commerce Admin.

1. Ange **[!UICONTROL Match by SKU]** som matchande regel.

   ![standardregel för automatisk matchning](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. Ange det metadatafältnamn som används för att identifiera objekt i AEM Assets.

   >[!NOTE]
   >
   > Om standardstartprocessen följdes bör det här värdet anges till `commerce:skus`.

## Så här fungerar den automatiska matchningsmekanismen

När matchningsregeln **[!UICONTROL Match by product SKU]** har konfigurerats i Commerce Admin synkroniseras Commerce resursfiler automatiskt från AEM Assets till ditt Commerce-projekt baserat på de metadata för resursen som har konfigurerats för varje fil. Du konfigurerar metadata från fliken AEM **Commerce** i **AEM Assets-redigeringsmiljön** :

1. I AEM Assets uppdaterar du bildmetadata för att lägga till Adobe Commerce-associationen genom att ställa in fältet `Eligible for Commerce` på `Yes`.

   ![Exempelmetadata](../assets/metadata-commerce-yes.png){width="600" zoomable="yes"}

1. Konfigurera de metadata ([!UICONTROL SKU], [!UICONTROL position] och [!UICONTROL role]) som länkar resursen till associerad produkt-SKU.

   >[!NOTE]
   >
   > Om en resurs används för flera produkter konfigurerar du metadata för varje associerad SKU.

1. På fliken `Basic` ställer du in standardvärdet för fältet _[!UICONTROL Review Status]_till `approved`.

   ![Exempelmetadata](../assets/metadata-review-status.png){width="600" zoomable="yes"}

Detta säkerställer att digitala resurser länkas och visas på rätt sätt i Adobe Commerce. Det ger också handlare och marknadsförare möjlighet att hantera roller och tillgångspositionering direkt i AEM Assets, vilket ger en enhetlig och centraliserad mekanism för att välja och beställa bilder i alla engagemangskanaler.
