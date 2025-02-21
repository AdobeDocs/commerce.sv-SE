---
title: Produktrekommendationer Administratörsutveckling
description: Översikt över arkitekturen och utvecklingsfunktionerna i produktrekommendationer.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Produktrekommendationer Administratörsutveckling

Produktrekommendationer är ett kraftfullt marknadsföringsverktyg som ni kan använda för att öka konverteringarna, öka intäkterna och stimulera kundernas engagemang. Produktrekommendationer visas i butiken i form av enheter som&quot;kunder som tittade på den här produkten också såg&quot;,&quot;kunder som köpt den här produkten även köpte&quot;,&quot;Rekommenderas för dig&quot; och så vidare. Adobe Commerce produktrekommendationer drivs av [Adobe Sensei](https://www.adobe.com/sensei.html) som använder artificiell intelligens och maskininlärningsalgoritmer för att göra en djupgående analys av samlade kunddata. Dessa data kombineras med er Commerce-katalog och ger en engagerande, relevant och personaliserad upplevelse för kunderna.

>[!NOTE]
>
>Om din storefront implementeras med PWA Studio finns mer information i [PWA-dokumentationen](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Om du använder en anpassad klientteknik som React eller Vue JS läser du i användarhandboken för att lära dig hur du integrerar produktrekommendationer i en [headless](headless.md) -miljö. Headless-instanser måste implementera händelser för att fungera bättre i produktrekommendationsarbetsytan.

## Arkitektur - översikt

På en hög nivå distribueras Commerce produktrekommendationer som SaaS. På Commerce-sidan finns storefront, som innehåller händelseinsamlaren och rekommendationslayoutmallen, samt serverdelen, som innehåller datatjänster, SaaS-exportmodulen och administratörsgränssnittet. Adobe Sensei underrättelsetjänster utnyttjas av SaaS.

![Arkitektur för produktrekommendationer](assets/arch-diag-sensei.svg)

När rekommendationsmodulerna har installerats och konfigurerats börjar butiken samla in beteendedata. Adobe Sensei behandlar dessa beteendedata tillsammans med katalogdata och beräknar produktassociationer som används av rekommendationstjänsten. Nu kan handlaren skapa, hantera och driftsätta produktrekommendationsenheter i butiken direkt från administratörsgränssnittet.

## Nästa steg

Läs följande avsnitt för att komma igång med produktrekommendationer:

- [Implementera produktrekommendationer](implementation-workflow.md)

- [Installera och konfigurera produktrekommendationer](install-configure.md)

- [Skapa produktrekommendationer](create.md)
