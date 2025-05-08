---
title: Bearbetning på nivå 2 och nivå 3
description: Bearbetningsnivåer för kortbetalningar inom  [!DNL Payment Services] transaktioner.
role: Admin
feature: Payments, Paas, Saas
exl-id: db8993fe-dd6f-48b5-9e7b-69a0f2e08552
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Bearbetning på nivå 2 och nivå 3

[!DNL Payment Services] har avancerade kortbearbetningsfunktioner som hjälper handlarna att optimera sina betalningstransaktioner och sänka utbytesavgifterna. Det finns tre nivåer av kortbearbetning tillgängliga, var och en med olika krav på transaktionsdata.

## Uppgiftskrav per bearbetningsnivå

![Transaktionsrapport](assets/level-processing-details.png){width="500" zoomable="yes"}

[!DNL Payment Services] samlar in dessa data och tillhandahåller detaljerad rapportering av dina betalningstransaktioner.

## Tillgängliga bearbetningsnivåer per kortnätverk

![Kortinformation](assets/cards-details-level-processing.png){width="500" zoomable="yes"}

Mer information finns i [betalningshantering](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} i dokumentationen för PayPal-utvecklare.

### Nivå 1

Nivå 1 är den vanligaste, kräver mindre information och medför därför i allmänhet högre förmedlingsavgifter jämfört med transaktioner som behandlas med data på Nivå 2 eller Nivå 3, som vanligtvis är kopplade till kreditkort för företag och inköp.

### Nivå 2 och nivå 3

[!DNL Payment Services] handlare på Interchange Plus (IC++) kan kvalificera sig för nivå 2/nivå 3-bearbetning om de tillhandahåller ytterligare transaktionsinformation till kortnätverk och uppfyller särskilda kvalificeringskriterier. Dessa nivåer är särskilt fördelaktiga för handlare som hanterar stora inköp eller större företagskortvolymer, eftersom de kan ge betydande kostnadsbesparingar. Detaljerade data för nivå 2 eller nivå 3 kan:

* Sänk handläggningsavgifterna och optimera de totala kostnaderna
* Förebygga bedrägerier och minska processorriskerna
* Förbättra transaktionssäkerheten

Se [Vad är IC++?](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} i dokumentationen för PayPal-utvecklare om du vill ha mer information.

## Betalningstransaktioner för nivå 2 och nivå 3 i [!DNL Payment Services]

För att vara berättigad till behandling på nivå 2 eller nivå 3 måste handlarna skicka den tidigare informationen, även om det är kortnätverken som bestämmer vilken nivå en transaktion kvalificerar sig för när den behandlas.

Mer information finns i [Vanliga frågor om betalningsbearbetning](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} i dokumentationen för PayPal-utvecklare.

Bearbetning på nivå 2 och nivå 3 är inaktiverad som standard för [!DNL Payment Services] handlare på butiksnivå.

Nivå 2- och nivå 3-bearbetning är tillgänglig om du redan använder IC++-priser. Om du vill aktivera den här funktionen kan du göra det via [kommandoradsgränssnittet (CLI](configure-cli.md)).

>[!IMPORTANT]
>
>Om du har några frågor kan du kontakta din kontoansvarige på [!DNL Payment Services].
