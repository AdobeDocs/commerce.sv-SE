---
title: Skapa anpassade händelser
description: Lär dig hur du skapar anpassade händelser för att koppla dina Adobe Commerce-data till andra Adobe DX-produkter.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 4e8cf0ad3f8f94d4f59bc8d78a44f4b3e86cbc3e
workflow-type: tm+mt
source-wordcount: '348'
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

För alla händelser som anges med `customContext` åsidosätter eller utökar insamlaren fält i händelsens nyttolast från fälten i `custom context`. Användbart för åsidosättningar är när en utvecklare vill återanvända och utöka kontexter som angetts av andra delar av sidan i händelser som redan stöds.

Händelseåsidosättningar gäller endast vid vidarebefordran till Experience Platform. De tillämpas inte på Adobe Commerce- och Sensei-analyshändelser. Adobe Commerce Events Collector [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md) innehåller ytterligare information.

>[!NOTE]
>
>När du utökar `productListItems` med anpassade attribut i Experience Platform händelsenyttolaster ska du matcha produkter med SKU. Detta krav gäller inte för `product-page-view`-händelser.

### Användning

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### Exempel 1

Det här exemplet lägger till anpassad kontext när händelsen publiceras.

```javascript
magentoStorefrontEvents.publish.productPageView({
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

### Exempel 2

I det här exemplet läggs en anpassad kontext till innan händelsen publiceras.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
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

mse.publish.productPageView();
```

### Exempel 3

I det här exemplet anges den anpassade kontexten i utgivaren och den anpassade kontext som tidigare angetts i Adobe Client Data Layer skrivs över.

I det här exemplet kommer händelsen `pageView` att ha **Eget sidnamn** i fältet `web.webPageDetails.name`.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### Exempel 4

I det här exemplet läggs anpassad kontext till i `productListItems`-händelser med flera produkter.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

Lumabaserade butiker:

Lumabaserade butiker implementerar publiceringshändelser internt, så du kan ange anpassade data genom att utöka `customContext`.

Exempel:

```javascript
mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name'
    },
  },
});
```

>[!NOTE]
>
> Om du åsidosätter händelser med anpassade attribut kan det påverka Adobe Analytics standardrapporter.
