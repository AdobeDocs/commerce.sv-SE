---
title: GraphQL
description: Med arbetsytan i  [!DNL Live Search] GraphQL kan du skapa frågor med dina livedata.
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

Med arbetsytan *GraphQL* kan administratörer skapa och testa GraphQL-frågor med egna data.

Den här arbetsytan stöder frågorna [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) och [`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/attribute-metadata/).

![GraphQL-arbetsyta](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
        name
      }
    }
    facets {
      title
    }
  }
}
```

Variabler:

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```
