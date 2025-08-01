---
title: Översikt över ansikten
description: Lär dig mer om aspekter i [!DNL Adobe Commerce Optimizer] och hur de förbättrar sökresultaten.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: ad8fb7d1d7e1ad124647ba84377079dcfbd46a3c
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Fasetter

Ansikten är en metod för högpresterande filtrering som använder flera dimensioner av attributvärden som sökvillkor.

![Filtrerade sökresultat](../../assets/storefront-search-results-run.png)

Inom en aspekt kan kunderna välja flera alternativ, till exempel&quot;Grundläggande&quot; och&quot;Snug&quot; under&quot;Format&quot; och sökresultaten uppdateras så att endast dessa format visas. På samma sätt gäller att om en kund väljer alternativ i olika aspekter, till exempel&quot;Grundläggande&quot; under&quot;Format&quot; och&quot;Inomhus&quot; under&quot;Klimatteknik&quot;, uppdateras sökresultaten så att den valda stilen och det valda klimatet visas.

Alla definierade aspekter kan användas som URL-parametrar och resultaten filtreras baserat på parametervärdena: `http://yourstore.com?brand=acme&color=red`.

## Fasettaggregering

Akettaggregering utförs enligt följande: Om butiken har tre aspekter (kategorier, färg och pris) och shopparfiltren på alla tre (färg = blå, priset är från 10,00-50,00, kategorier = `promotions`).

- `categories`-aggregering - Aggregerar `categories` och tillämpar sedan filtren `color` och `price`, men inte filtret `categories`.
- `color`-aggregering - Aggregerar `color` och tillämpar sedan filtren `price` och `categories`, men inte filtret `color`.
- `price`-aggregering - Aggregerar `price` och tillämpar sedan filtren `color` och `categories`, men inte filtret `price`.

## Standardattributvärden

Följande produktattribut används av [!DNL Adobe Commerce Optimizer] och aktiveras som standard.

| Egenskap | Beskrivning | Attribut |
|---|---|---|
| Sorterbar | Används för sortering i produktlista | `price` |
| Sökbart | Använd i sökning | `price` <br />`sku`<br />`name` |

Se [API:t för datainmatningsmetadata](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) om du vill veta mer om produktattribut och deras egenskaper.

## Standardegenskaper för icke-systemattribut

I följande tabell visas standardegenskaperna för sökning och filtrering av attribut som inte är systemattribut. Om du anger attributegenskapen *Använd i sökning* till `Yes` blir attributet sökbart i [!DNL Adobe Commerce Optimizer].

| Attributkod | Sökbart |
|--- |--- |
| aktivitet | Ja |
| attributes_brand | Ja |
| varumärke | Ja |
| klimat | Ja |
| räntekrage | Ja |
| färg | Ja |
| kostnad | Ja |
| eco_collection |
| kön | Ja |
| tillverkare | Ja |
| material | Ja |
| syfte | Ja |
| strap_bag | Ja |
| style_general | Ja |

## Standardegenskaper för systemattribut

I följande tabell visas standardegenskaperna för sökning och filterbarhet för systemattribut.

| Attributkod | Sökbart |
|--- |--- |
| allow_open_amount | Ja |
| description | Ja |
| name | Ja |
| pris | Ja |
| short_description | Ja |
| sku | Ja |
| status | Ja |
| tax_class_id | Ja |
| url_key | Ja |
| vikt | Ja |
