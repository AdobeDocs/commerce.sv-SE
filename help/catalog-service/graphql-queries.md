---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Använd GraphQL-frågor för att hämta katalogdata för att underlätta Commerce upplevelser.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
source-git-commit: 935f34a8b4317686e67e33b50df3301d746fbd25
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Hämta katalogdata med GraphQL {#graphql-queries}

Använd GraphQL-frågor för att hämta produkter, priser och andra data från Adobe Commerce Catalog SaaS-datarymden och använd den för att återge Commerce-upplevelser snabbare än med Adobe Commerce GraphQL-frågor.

Katalogtjänsten innehåller följande frågor:

| Fråga | Beskrivning | Användning |
|-------|-------------|-------|
| `categories` | Returnerar kategoridata. Om indataobjektet för underträdet anges returnerar frågan information om underkategorier. | Användbar för att återge navigering och kategorisidor för butiker. [Se exempel.](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) |
| `products` | Returnerar information om de SKU:er som angetts som indata. | Används främst för att återge innehåll på sidor med produktinformation och produktjämförelser. [Se exempel.](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) |
| `productSearch` | Returnerar en lista med produkter som matchar sökvillkoren. | Användbart för återgivning av sökresultat och produktlistsidor baserat på sökindata. [Se exempel.](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/) |
| `refineProduct` | Begränsa resultatet av en produktfråga som körs mot en komplex produkt för att returnera en specifik information om en produktvariant. | Användbar för återgivning av uppdaterade produktinformationssidor när kunderna väljer ett produktalternativ. [Se exempel.](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) |
| `variants` | Returnerar information om alla produktvariationer. | Användbar för att visa variantbilder på produktdetaljer eller listsidor utan att skicka flera API-begäranden. [Se exempel.](https://developer.adobe.com/commerce/services/graphql/catalog-service/product-variants/) |


Mer information om hur du använder dessa frågor finns i [API-handboken för katalogtjänsten](https://developer.adobe.com/commerce/services/graphql/catalog-service/)

