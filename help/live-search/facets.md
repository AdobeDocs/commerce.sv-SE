---
title: Fasetter
description: '[!DNL Live Search] facets använder flera dimensioner av attributvärden som sökvillkor.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: 86484d49aa4b79bfe64455dba18b84bcd9073736
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Fasetter

Faceting är en metod för högpresterande filtrering som använder flera dimensioner av attributvärden som sökvillkor. Fallerad sökning liknar, men är betydligt&quot;smartare&quot; än [lagerstyrd navigering](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=sv-SE). Listan med tillgängliga filter avgörs av de [filterbara attributen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=sv-SE#filterable-attributes) för produkter som returneras i sökresultaten.

[!DNL Live Search] använder `productSearch`-frågan, som returnerar faceting och andra data som är specifika för [!DNL Live Search]. Se [`productSearch` fråga &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) i utvecklardokumentationen för kodexempel.

![Filtrerade sökresultat](assets/storefront-search-results-run.png)

Inom en aspekt kan kunderna välja flera alternativ, till exempel&quot;Grundläggande&quot; och&quot;Snug&quot; under&quot;Format&quot; och sökresultaten uppdateras så att endast dessa format visas. På samma sätt gäller att om en kund väljer alternativ i olika aspekter, till exempel&quot;Grundläggande&quot; under&quot;Format&quot; och&quot;Inomhus&quot; under&quot;Klimatteknik&quot;, uppdateras sökresultaten så att den valda stilen och det valda klimatet visas.

Alla definierade aspekter kan användas som URL-parametrar och resultaten filtreras baserat på parametervärdena: `http://yourstore.com?brand=acme&color=red`.

## Motsvarande krav

Kategori- och produktattributkraven för faceting liknar de filterbara attribut som används för lagerstyrd navigering. Varje storefront-egenskap för ett attribut måste ha värdet &quot;Use in Search Results Layered Navigation&quot; inställt på &quot;Yes&quot;. Du kan granska och uppdatera attributkonfigurationen på menyn [!DNL Stores] > [!DNL Attribute] i Admin.

>[!NOTE]
>
>Om du definierar en produktkategori som en fasett visas `url_path` för kategorin och underkategorin.
>
>![Kategorifaktor](assets/facet-category.png)

Se [gränser och gränser](./boundaries-limits.md#facets) om du vill veta mer om aspektkraven i [!DNL Live Search].

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
