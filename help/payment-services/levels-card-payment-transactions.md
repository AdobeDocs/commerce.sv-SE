---
title: Bearbetning på nivå 2 och nivå 3
description: Bearbetningsnivåer för kortbetalningar inom  [!DNL Payment Services] transaktioner.
role: Admin
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Bearbetning på nivå 2 och nivå 3

Det finns tre nivåer av kortbearbetning tillgängliga via [!DNL Payment Services]:

* Nivå 1 är den vanligaste, kräver mindre information och medför därför i allmänhet högre förmedlingsavgifter jämfört med transaktioner som behandlas med data på Nivå 2 eller Nivå 3, som vanligtvis är kopplade till kreditkort för företag och inköp.

* Med nivå 2 och nivå 3 kan [!DNL Payment Services] kunder med utbytesavtal plus (IC++)-priser som accepterar många köp- eller visitkortstransaktioner eventuellt få en lägre bearbetningshastighet genom att tillåta [!DNL Payment Services] att skicka mer information om en transaktion. Om transaktionen uppfyller kraven kan handlaren få en lägre handläggningsfrekvens för en viss transaktion enligt kraven för kortnätverk.

>[!NOTE]
>
>Prisnivå 2 och nivå 3 gäller endast för Visa- och MasterCard-transaktioner. American Express erbjuder endast nivå 2-pris. Upptäck priser på nivå 2 och 3. Mer information finns i [betalningshantering](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} i dokumentationen för PayPal-utvecklare.

Se [Vad är IC++?](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} i dokumentationen för PayPal-utvecklare om du vill ha mer information.

Bearbetningsdata på nivå 2 och nivå 3 gör det möjligt för handlare att sänka sina IC++-priser om de ger ytterligare information om köpet som minskar processorriskerna och ger fördelar:

* Stora kunder betalar mindre genom att tillhandahålla dessa bearbetningsdata.

* Kunderna är mindre benägna att hamna i bedrägliga situationer eftersom beställningarna har mer information.

Kortnäten, som Visa och Mastercard, avgör dock i slutändan om en transaktion uppfyller kraven för nivå 2 eller nivå 3:

* Data på nivå 2 innehåller ytterligare information, t.ex. orderns momsbelopp eller kundkoden eller inköpsordernumret.

* Data på nivå 3 är mer detaljerad information om försäljningen, vilket gör det lättare att kvalificera sig för ännu lägre utbytesfrekvenser jämfört med nivå 2. Data på nivå 3 innehåller information som en beskrivning av den köpta artikeln, antalet köpta enheter, måttenhet för beställda artiklar och annan specifik information.

[!DNL Payment Services] samlar in dessa data och tillhandahåller detaljerad rapportering av dina betalningstransaktioner.

## Betalningstransaktioner för nivå 2 och nivå 3 i [!DNL Payment Services]

För att vara berättigad till behandling på nivå 2 eller nivå 3 måste handlarna skicka den tidigare informationen, även om det är kortnätverken som bestämmer vilken nivå en transaktion kvalificerar sig för när den behandlas.

Mer information finns i [Vanliga frågor om betalningsbearbetning](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} i dokumentationen för PayPal-utvecklare.

Bearbetning på nivå 2 och nivå 3 är inaktiverad som standard för [!DNL Payment Services] handlare på butiksnivå.

Nivå 2- och nivå 3-bearbetning är tillgänglig om du redan använder IC++-priser. Om du vill aktivera den här funktionen kan du göra det via [kommandoradsgränssnittet (CLI](configure-cli.md)).

>[!IMPORTANT]
>
>Om du har några frågor kan du kontakta din kontoansvarige på [!DNL Payment Services].
