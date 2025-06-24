---
title: Prisböcker
description: Lär dig hur du hanterar prisböcker i  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Prisböcker

I den här artikeln beskrivs hur du definierar och tilldelar prisböcker till katalogvyer med korrekta datastyrningskontroller.

Läs [utvecklardokumentationen](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books) om du vill veta hur du importerar prisboksinformation från ett tredjepartssystem till [!DNL Adobe Commerce Optimizer] med hjälp av prisbokens API.

Med prisböcker kan ni definiera priskataloger för att hantera produktpriser i olika kundnivåer och på olika marknader. Prisböcker har stöd för en hierarkisk modell, vilket tillåter upp till tre nivåer av kapslade underordnade prisböcker under varje basprisbok. Varje prisbok kan referera till en överordnad prisbok, som utgör en trädstruktur för källorna till prislistor.

Basprisboken definierar valutan för sig själv och alla dess underordnade prisböcker. Underordnade prisböcker ärver den här valutan och kan inte åsidosätta den.

## Viktiga begrepp

| Villkor | Beskrivning |
|------|-------------|
| **Prisbok** | Logisk gruppering som definierar priskatalogkälla, till exempel en viss region eller kundnivå, och som används för att hantera produktpriser. |
| **Reservprisbok** | Den översta prisboken i en hierarki. Det har ingen överordnad och är prisboken *only* som definierar valutan för sig själv och alla dess underordnade prisböcker.<br/><br/>Om ingen överordnad är definierad när prisboken skapas (via API:t) skapas en ny grundprisbok. |
| **Överordnad prisbok** | En prisbok på en högre nivå från vilken en underordnad prisbok kan ärva priser om de inte uttryckligen anges i den underordnade. |
| **Hierarkidjup** | Maximalt 3 nivåer (Fallback → Child → Morchild)<br/><br/> framtvingades inte vid intag. |
| **Valuta** | Definieras endast i fallback-prisbok. Ärvs av alla barn, prisböcker.<br/><br/>Om ingen valuta anges när grundprisboken skapas (via API:t) blir standardvalutan USD. |
| **Produktpris** | Det specifika pris som tilldelats en produkt (SKU) inom en viss prisbok. |
| **Rabatter** | Rabatterna definieras i produktpriset. Ärvs inte. |
