---
title: Tillgängliga data
description: Använd ekonomiska rapporteringsdata för att stämma av mot rapporter i andra system än Commerce.
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Tillgängliga data

Vissa beställnings- och utbetalningsdata är tillgängliga för er så att ni kan samordna Adobe Commerce ekonomiska rapporter över externa system.

## Stäm av med ERP-system

Du kan stämma av Adobe Commerce ekonomiska rapporter med det ERP-system (Enterprise Resource Planning) som inte är Adobe med hjälp av det inkrement-ID som är kopplat till en viss order.

När betalningstjänster skickar Commerce-beställningen till PayPal inkluderas inkrement-ID som `custom_id` _och_ i `invoice_id` (som även innehåller en slumpmässig sträng efter `increment_id`).

ID:n är lätt tillgängliga både i detaljerna om handlaraktivitet för en utbetalning och på PayPals webbkrok.

`invoice_id` och `custom_id` visas längst ned i handelsaktivitetsinformationen för en utbetalning:

![`custom_id` i handelsaktivitetsinformation &#x200B;](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

`custom_id` och `invoice_id` i informationen i PayPals webkrok:

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

Mer information finns i dokumentationen för PayPals REST API:er:

* [`purchase_unit` där `custom_id` och `invoice_id` finns &#x200B;](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [Visa orderinformation](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
