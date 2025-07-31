---
title: Prisböcker
description: Lär dig hur du hanterar prisböcker i  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 513ed97442bfffe74d64f4eb0484cfa8f25b5ecc
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Prisböcker

Med prisböcker kan du definiera produktpriser för en katalogkälla i olika kundnivåer och på olika marknader. Prisböcker har stöd för en hierarkisk modell, vilket tillåter upp till tre nivåer av kapslade underordnade prisböcker under varje basprisbok. Varje prisbok kan referera till en överordnad prisbok, som utgör en trädstruktur för källorna till prislistor.

Basprisboken definierar valutan för sig själv och alla dess underordnade prisböcker. Underordnade prisböcker ärver den här valutan och kan inte åsidosätta den.

Läs [utvecklardokumentationen](https://developer.adobe.com/commerce/services/reference/rest/) om du vill veta mer om hur du skapar, uppdaterar och tar bort prisböcker [!DNL Adobe Commerce Optimizer] med hjälp av prisbokens API.

## Viktiga begrepp

| Villkor | Beskrivning |
|------|-------------|
| **Prisbok** | Logisk gruppering som definierar priser för en katalogkälla, till exempel en viss region eller kundnivå, och används för att hantera produktpriser. |
| **Reservprisbok** | Den översta prisboken i en hierarki. Det har ingen överordnad och är prisboken *only* som definierar valutan för sig själv och alla dess underordnade prisböcker.<br/><br/>Om ingen överordnad är definierad när prisboken skapas (via API:t) skapas en ny grundprisbok. |
| **Överordnad prisbok** | En prisbok på en högre nivå från vilken en underordnad prisbok kan ärva priser om de inte uttryckligen anges i den underordnade. |
| **Hierarkidjup** | Maximalt tre nivåer (Reservfall -> Underordnad -> Överordnad)<br/><br/> framtvingades inte vid intag. |
| **Valuta** | Definieras endast för reservprisboken. Ärvs av alla barnprisböcker.<br/><br/>Om ingen valuta anges när grundprisboken skapas (via API:t) blir standardvalutan USD. |
| **Produktpris** | Det specifika pris som tilldelats en produkt (SKU) inom en viss prisbok. |
| **Rabatter** | Rabatterna definieras i produktpriset. Ärvs inte. |
