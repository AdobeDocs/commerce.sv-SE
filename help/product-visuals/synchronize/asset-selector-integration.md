---
title: Manuellt urval av tillgångar
description: Upptäck hur AEM Asset Selector som är integrerad i Commerce Admin hjälper marknadsförare och handlare att enkelt lägga till bilder från AEM Assets i Adobe Commerce och effektivisera resurshanteringen.
feature: CMS, Media, Integration
source-git-commit: d362e6e821e81f6da99c420881e1e1b1058bbd45
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Manuellt urval av tillgångar

Med **AEM Resursväljare** kan marknadsförare och handlare enkelt lägga till bilder från AEM Assets i Adobe Commerce och effektivisera resurshanteringsprocessen. Den här metoden säkerställer varumärkets enhetlighet och efterlevnad genom att begränsa urvalet av resurser till dem som granskats och godkänts i [!DNL DAM (Digital Asset Management system)].

**AEM Resursväljare** är tillgänglig när IMS-klient-ID:t för AEM Assets-projektet har konfigurerats i Commerce Admin. Se [Konfigurera AEM Resursväljare]&#x200B;(#configure-the-aem-asset-selector-in-adobe-commerce.

När integreringen av **AEM Resursväljare** har konfigurerats kan marknadsförare och handlare:

* Hantera kategoribilder utan problem och säkerställ att de är anpassade efter riktlinjer för varumärken och kampanjer.
* [!BADGE PaaS endast]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."} Tilldela resurser direkt i Page Builder för visuellt avancerat innehåll.

>[!NOTE]
>
> AEM Resursväljare är en komponent i AEM som utgör en integrerad komponent för redigering av AEM Assets. Mer information om den här komponenten finns i [Micro-Front Asset Selector](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector){target=_blank} i *AEM as a Cloud Service användarhandbok*.

## Viktiga fördelar

Att bädda in AEM Resursväljare i Adobe Commerce Admin Panel ger flera fördelar:

* **Varumärkeskonsekvens**-Visar endast godkända resurser, vilket minimerar risken för inaktuella eller inkompatibla bilder i butiken.

* **Effektivitet** - Marknadsförare och handlare kan tilldela resurser snabbt utan att behöva växla mellan olika plattformar.

* **Effektivare Collaboration**-Smidigare teamwork genom att tillåta direktval av bilder från DAM, vilket eliminerar manuella hämtningar och överföringar.

* **Förbättrad innehållskvalitet** - Ser till att högupplösta, optimerade bilder används för produktsidor, kategorier och Page Builder.

![Resursväljare](../assets/asset-selector.png){width="600" zoomable="yes"}

## Konfigurera AEM Resursväljare i Adobe Commerce

1. Gå till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]** i Commerce Admin.

1. Fyll i fältet **[!UICONTROL IMS Client ID]**.

1. **Spara** konfigurationen.

## Nästa steg

* [Hantera kategoribilder med resursväljare](../manage-assets.md#category-images)
* [Hantera bilder i Page Builder-innehåll](../manage-assets.md#using-aem-asset-selector-in-page-builder)
