---
title: Rapport om framgångsmått
description: Rapportsidan Success metrics ger insikt i nyckelresultatmåtten för din [!DNL Adobe Commerce Optimizer] butik.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: b462980c12342ae2fe6d24272c56c6a9d9b21989
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Rapport om framgångsmått

Den här sidan innehåller en översikt över nyckeltal för prestandamått för din [!DNL Adobe Commerce Optimizer]-butik. Målet är att du snabbt ska förstå resultatet av implementeringen av [!DNL Adobe Commerce Optimizer], och sedan hjälpa dig och ditt team att identifiera tillväxtmöjligheter och lyfta fram områden som ska optimeras.

![Rapport om lyckade mätvärden](../assets/success-metrics.png)

Måtten i rapporten hämtas från butikshändelsedata. [Läs mer](../setup/events/overview.md) om händelsedata som samlats in.

## Generera en rapport

1. Välj _Hantera resultat_ > **Lyckade mått** i den vänstra listen.
1. Högst upp på sidan väljer du den katalogvy som rapporten ska genereras från. I exempelbilden ovan är den valda katalogvyn ett fiktivt bilkonglomerat med namnet **Carvelo**.
1. Under **Rapportkonfiguration** anger du **datumintervall**, **land**, baserat på språkinställningen och **Valuta**.
1. Klicka på **[!UICONTROL Apply]**.

   De **vanligaste markeringarna**, **Intäkter**, **Konvertering**, **engagemang**, **Förvärv** och **Studsfrekvens** uppdateras alla baserat på din rapportkonfiguration.

1. Klicka på **[!UICONTROL Export]** om du vill spara rapporten som en PDF.

## Fältbeskrivningar

| Fält | Beskrivning |
|---|---|
| Datumintervall | Du kan välja mellan **Senaste 3 månaderna**, **Senaste 7 dagarna**, **Senaste 30 dagarna**, **Senaste 6 månaderna**, **Senaste 12 månaderna** och **År till och med**. |
| Land | Baserat på den katalogkälla som har angetts för [katalogvyn](../setup/catalog-view.md). |
| Valuta | Den valuta som har angetts för katalogvyn. |
| Exportera | Sparar rapporten som en PDF. |
| Överkantsmarkeringar | Sammanfattar mätvärden från de andra flikarna. |
| Intäkter | Det totala penningbeloppet som genereras från försäljningstransaktioner. Det här är det primära ekonomiska måttet som visar hur mycket pengar företaget tjänar på kundinköp. |
| Konvertering | Andelen besökare på webbplatsen som genomför ett köp. Detta visar hur effektivt webbplatsen konverterar webbläsare till köpare. |
| Engagemang | Mäter hur aktivt användarna interagerar med webbplatsen, inklusive mått som tid på webbplatsen, sidor per session, klickfrekvens och sociala interaktioner. Ett högre engagemang innebär vanligtvis att användarna tycker att ert innehåll är värdefullt och att det är mer sannolikt att det konverteras. |
| Förvärv | Avser processen och kostnaden för att köpa nya kunder. Detta inkluderar mätvärden som kundanskaffningskostnad (CAC), trafikkällor och marknadsföringskanalernas effektivitet när det gäller att ta in nya besökare på er webbplats. |
| Studsfrekvens | Andelen besökare som lämnar webbplatsen efter att endast ha visat en sida. En hög avhoppsfrekvens (vanligtvis över 50-60 %) tyder på att användarna inte hittar det de letar efter eller att sidan inte uppfyller deras förväntningar, vilket kan påverka konverteringar och intäkter negativt. |
