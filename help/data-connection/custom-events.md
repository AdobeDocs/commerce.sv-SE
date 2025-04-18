---
title: Skapa anpassade händelser
description: Lär dig hur du skapar anpassade händelser för att koppla dina Adobe Commerce-data till andra Adobe DX-produkter.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Skapa anpassade händelser

Du kan utöka [händelseplattformen](events.md) genom att skapa egna butikshändelser för att samla in data som är unika för din bransch. När du skapar och konfigurerar en anpassad händelse skickas den till [Adobe Commerce Events Collector](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector).

## Hantera anpassade händelser

Anpassade händelser stöds endast för Adobe Experience Platform. Anpassade data vidarebefordras inte till Adobe Commerce dashboards och metrics trackers.

För alla `custom`-händelser, insamlaren:

- Lägger till `identityMap` med `ECID` som primär identitet
- Inkluderar `email` i `identityMap` som en sekundär identitet _om_ `personalEmail.address` har angetts i händelsen
- Omsluter den fullständiga händelsen i ett `xdm`-objekt innan den vidarebefordras till Edge

Exempel:

Anpassade event som publiceras via Adobe Commerce Events SDK:

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

I Experience Platform Edge:

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> Användning av anpassade händelser kan påverka Adobe Analytics standardrapporter.

## Hantera händelseåsidosättningar (anpassade attribut)

Attributåsidosättningar för standardhändelser stöds endast för Experience Platform. Anpassade data vidarebefordras inte till Commerce dashboards och metrics trackers.

För alla händelser med `customContext` åsidosätter insamlaren sammanfogningsfält som angetts i relevanta kontexter med fält i `customContext`. Användbart för åsidosättningar är när en utvecklare vill återanvända och utöka kontexter som angetts av andra delar av sidan i händelser som redan stöds.

>[!NOTE]
>
>När du åsidosätter anpassade händelser bör händelsevidarebefordran till Experience Platform inaktiveras för den händelsetypen för att undvika dubbelräkning.

Exempel:

Produktvy med åsidosättningar som publicerats via Adobe Commerce Events SDK:

```javascript
mse.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

I Experience Platform Edge:

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

>[!NOTE]
>
> Om du åsidosätter händelser med anpassade attribut kan det påverka Adobe Analytics standardrapporter.
