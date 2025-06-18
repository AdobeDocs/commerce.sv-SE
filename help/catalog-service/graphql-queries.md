---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Använd GraphQL-frågor för att hämta katalogdata för att underlätta Commerce upplevelser.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Hämta katalogdata med GraphQL {#graphql-queries}

Använd GraphQL-frågor för att hämta produkter, priser och andra data från Adobe Commerce Catalog SaaS-datarymden och använd den för att återge Commerce-upplevelser snabbare än med Adobe Commerce GraphQL-frågor.

Katalogtjänsten innehåller följande frågor:

| Fråga | Beskrivning | Användning |
|-------|-------------|-------|
| `categories` | Returnerar kategoridata. Om indataobjektet för underträdet anges returnerar frågan information om underkategorier. | Användbar för att återge navigering och kategorisidor för butiker. [Se exempel.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | Returnerar information om de SKU:er som angetts som indata. | Används främst för att återge innehåll på sidor med produktinformation och produktjämförelser. [Se exempel.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | Returnerar en lista med produkter som matchar sökvillkoren. | Användbart för återgivning av sökresultat och produktlistsidor baserat på sökindata. [Se exempel.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | Begränsa resultatet av en produktfråga som körs mot en komplex produkt för att returnera en specifik information om en produktvariant. | Användbar för återgivning av uppdaterade produktinformationssidor när kunderna väljer ett produktalternativ. [Se exempel.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | Returnerar information om alla produktvariationer. | Användbar för att visa variantbilder på produktdetaljer eller listsidor utan att skicka flera API-begäranden. [Se exempel.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

Mer information om hur du använder dessa frågor finns i [API-handboken för katalogtjänsten](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
