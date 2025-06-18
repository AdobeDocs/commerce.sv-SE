---
title: Fasetter
description: '[!DNL Live Search] facets använder flera dimensioner av attributvärden som sökvillkor.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Fasetter

Faceting är en metod för högpresterande filtrering som använder flera dimensioner av attributvärden som sökvillkor. Fallerad sökning liknar, men är betydligt&quot;smartare&quot; än [lagerstyrd navigering](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=sv-SE). Listan med tillgängliga filter avgörs av de [filterbara attributen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=sv-SE#filterable-attributes) för produkter som returneras i sökresultaten.

[!DNL Live Search] använder `productSearch`-frågan, som returnerar faceting och andra data som är specifika för [!DNL Live Search]. Se [`productSearch` fråga ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) i utvecklardokumentationen för kodexempel.

![Filtrerade sökresultat](assets/storefront-search-results-run.png)

Inom en aspekt kan kunderna välja flera alternativ, till exempel&quot;Grundläggande&quot; och&quot;Snug&quot; under&quot;Format&quot; och sökresultaten uppdateras så att endast dessa format visas. På samma sätt gäller att om en kund väljer alternativ i olika aspekter, till exempel&quot;Grundläggande&quot; under&quot;Format&quot; och&quot;Inomhus&quot; under&quot;Klimatteknik&quot;, uppdateras sökresultaten så att den valda stilen och det valda klimatet visas.

Alla definierade aspekter kan användas som URL-parametrar och resultaten filtreras baserat på parametervärdena: `http://yourstore.com?brand=acme&color=red`.

## Motsvarande krav

Kategori- och produktattributkraven för faceting liknar de filterbara attribut som används för lagerstyrd navigering. Varje storefront-egenskap för ett attribut måste ha värdet &quot;Use in Search Results Layered Navigation&quot; inställt på &quot;Yes&quot;.

[!DNL Live Search] stöder upp till:

* 100 attribut konfigurerade som facets
* 50 sorterbara attribut
* 200 filterbara attribut
* 200 sökbara attribut

>[!NOTE]
>
> Om fler än 200 filterbara attribut har definierats är det inte deterministiskt vilka 200 som faktiskt kommer att indexeras.

Om du har ett stort antal attribut att innesluta bör du överväga att kombinera attribut i ett enda meta-attribut. Exempel: skor har i allmänhet numeriska storlekar, medan skjortor vanligtvis har formatet&quot;S/M/L/XL&quot;. Dessa två typer av storlekar kan kombineras till ett enda sökbart attribut.

| Inställning | Beskrivning |
|--- |--- |
| [Inställningar för kategorivisning](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html?lang=sv-SE) | Ankarpunkt - `Yes` |
| [Attributegenskaper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=sv-SE) | [Katalogindatatyp](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html?lang=sv-SE) - `Yes/No`, `Dropdown`, `Multiple Select`, `Price`, `Visual swatch` (endast widget), `Text swatch` (endast widget) |
| Egenskaper för attributarkiv | Använd i sökresultatnavigering i lager - `Yes` |

## Fasettaggregering

Akettaggregering utförs enligt följande: Om butiken har tre aspekter (kategorier, färg och pris) och shopparfiltren på alla tre (färg = blå, priset är från 10,00-50,00, kategorier = `promotions`).

* `categories`-aggregering - Aggregerar `categories` och tillämpar sedan filtren `color` och `price`, men inte filtret `categories`.
* `color`-aggregering - Aggregerar `color` och tillämpar sedan filtren `price` och `categories`, men inte filtret `color`.
* `price`-aggregering - Aggregerar `price` och tillämpar sedan filtren `color` och `categories`, men inte filtret `price`.

## Standardattributvärden

Följande produktattribut har [storefront-egenskaper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=sv-SE) som används av [!DNL Live Search] och är aktiverade som standard.

| Egenskap | Storefront-egenskap | Attribut |
|---|---|---|
| Sorterbar | Används för sortering i produktlista | `price` |
| Sökbart | Använd i sökning | `price` <br />`sku`<br />`name` |
| FilterableInSearch | Använd i navigering i lager - filtrerbar (med resultat) | `price`<br />`visibility`<br />`category_name` |

## Standardegenskaper för icke-systemattribut

I följande tabell visas standardegenskaperna för sökning och filtrering av attribut som inte finns i systemet, inklusive de som är specifika för Luma-exempeldata. Om attributegenskapen *Använd i sökning* anges till `Yes` blir attributet sökbart i både [!DNL Live Search] och Adobe Commerce.

| Attributkod | Sökbart | Använd i navigering i lager |
|--- |--- |--- |
| aktivitet | Ja | Filterbar (med resultat) |
| attributes_brand | Ja | Nej |
| varumärke | Ja | Nej |
| klimat | Ja | Filterbar (med resultat) |
| räntekrage | Ja | Filterbar (med resultat) |
| färg | Ja | Filterbar (med resultat) |
| kostnad | Ja | Nej |
| eco_collection | Ja | Filterbar (med resultat) |
| kön | Ja | Filterbar (med resultat) |
| tillverkare | Ja | Filterbar (med resultat) |
| material | Ja | Filterbar (med resultat) |
| syfte | Ja | Filterbar (med resultat) |
| strap_bag | Ja | Filterbar (med resultat) |
| style_general | Ja | Filterbar (med resultat) |

## Standardegenskaper för systemattribut

I följande tabell visas standardegenskaperna för sökning och filterbarhet för systemattribut.

| Attributkod | Sökbart | Använd i navigering i lager |
|--- |--- |--- |
| allow_open_amount | Ja | Filterbar (med resultat) |
| description | Ja | Nej |
| name | Ja | Nej |
| pris | Ja | Filterbar (med resultat) |
| short_description | Ja | Nej |
| sku | Ja | Nej |
| status | Ja | Nej |
| tax_class_id | Ja | Nej |
| url_key | Ja | Nej |
| vikt | Ja | Nej |
