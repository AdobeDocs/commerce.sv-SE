---
title: Radobjekt för  [!DNL Payment Services]
description: Lär dig mer om radobjekt för  [!DNL Payment Services]  och hur du visar radobjekt på kontrollpanelen för handlare.
feature: Payments
role: User
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Radobjekt för [!DNL Payment Services]

Radobjekt för [!DNL Payment Services] är de objekt som ingår i en order. De här radobjekten innehåller information som:

* Produktinformation
* Kvantitet
* Pris (inklusive skatter, rabatter och annan relevant information)

Den här informationen är användbar för kundservice, orderhantering och korrekt fakturering.

Den här funktionen är aktiverad som standard för [!DNL Payment Services]. Så här visar du radobjekt:

1. Navigera till din [PayPal-kontrollpanel](https://www.paypal.com/merchant/){target=_blank}.

1. Klicka på **Aktivitet** > **Alla transaktioner**.

1. Markera önskad ordning och visa radobjekten:

   > Exempel på radartiklar i butikens kontrollpanel

   ![Vyn Radobjekt](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## Attribut för radobjekt

Radobjekt genereras när beställningen placeras via Adobe Commerce och information skickas till PayPal, med följande attribut:

| Attribut | Datatyp | Beskrivning |
| --- | --- | --- |
| `name` | Sträng! | Objektnamnet. Om en artikel har mer än en rad på grund av flera kvantiteter eller en momsavrundningsutleverans, förblir artikelnamnet detsamma för alla rader, men det visade priset kan variera något på grund av avrundning. |
| `unit_amount` | Objekt! | Artikelpris eller pris per enhet. Innehåller följande attribut: `currency_code` och `value`. |
| `tax` | Objekt | Artikelmoms för varje enhet. Innehåller följande attribut: `currency_code` och `value`. |
| `quantity` | Sträng! | Artikelkvantiteten. Det blir ett heltal. |
| `description` | Sträng | Den detaljerade artikelbeskrivningen. |
| `sku` | Sträng | Lagerhållningsenheten (eller SKU) för artikeln. |
| `url` | Sträng | `URL` till det objekt som ska köpas. Synligt för köpare och används i köpupplevelser. |
| `upc` | Objekt | The Universal Product Code (eller UPC) of the item. |
| `category` | Sträng | Artikelkategoritypen. |

### `unit_amount` attribut

Objektet `unit_amount` innehåller följande attribut:

| Attribut | Datatyp | Beskrivning |
| --- | --- | --- |
| `currency_code` | Sträng! | Den [ISO-4217-valutakod ](https://developer.paypal.com/api/rest/reference/currency-codes/) med tre tecken som identifierar valutan. |
| `value` | Sträng! | Anger artikelns värde. `currency_code` avgör antalet decimaler som krävs, om sådana finns. |

### `tax` attribut

Objektet `tax` innehåller följande attribut:

| Attribut | Datatyp | Beskrivning |
| --- | --- | --- |
| `currency_code` | Sträng! | Den [ISO-4217-valutakod ](https://developer.paypal.com/api/rest/reference/currency-codes/) med tre tecken som identifierar valutan. |
| `value` | Sträng! | Anger artikelns värde. Beroende på varje `currency_code` för det antal decimaler som krävs. |

### `upc` attribut

Objektet `upc` innehåller följande attribut:

| Attribut | Datatyp | Beskrivning |
| --- | --- | --- |
| `type` | sträng! | UPC-typen. |
| `code` | sträng! | The UPC product code of the item. |

+++Exempel på radartiklar

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

Mer information om de här fälten och deras begränsningar finns i [dokumentationen för PayPal-utvecklare om radobjekt](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank}.

## Hantera radartiklar

Adobe Commerce [beräknar moms baserat på det totala beloppet för varje rad ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}, vilket kan orsaka avrundningsproblem om flera kvantiteter av samma objekt beställs eller om taxinkluderade priser visas i katalogen. I sådana fall kan den totala kvantiteten delas upp i två rader, men kvantiteten motsvarar den totala beställda artikeln.

> Exempel på radobjekt med avrundningsproblem i kontrollpanelen för handlare

![Vyn Radobjekt](assets/line-items-example.png){width="600" zoomable="yes"}

+++Hur Adobe Commerce beräknar ett avrundningsproblem i radobjekt

Radartiklar för [!DNL Payment Services] balanserar den här avrundningsutleveransen så att värdet `unit_amount` eller `unit_tax` motsvarar orderns totala belopp. Ett objekt kan delas upp i två rader för att lösa problemet med avrundning:

* När avrundningsproblemet visas på `unit_amount`, ska säljaren se en skillnad på priset på den här extra raden.
* När avrundningsproblemet visas på `unit_tax` visas ingen skillnad för de enskilda radobjekten eftersom `tax` inte visas i rutnätet, utan bara som en summa längst ned.

+++
