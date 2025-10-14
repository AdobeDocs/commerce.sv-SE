---
title: Indexering
description: Lär dig hur  [!DNL Live Search] indexerar egenskaper för produktattribut.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# Indexering

Indexeringsprocessen [!DNL Live Search] läser igenom katalogen efter produktattribut och skapar ett index så att produkterna kan sökas igenom, filtreras och presenteras snabbt.

Egenskaper för produktattribut (metadata) bestämmer:

* Hur ett attribut kan användas i katalogen
* Dess utseende och beteende i butiken
* De data som ingår i dataöverföringsoperationer

Omfånget för attributmetadata är `website/store/store view`.

Med API:t [!DNL Live Search] kan en klient sortera efter vilket produktattribut som helst som har egenskapen [&#x200B; storefront](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/product-attributes) `Use in Search` inställd på `Yes` i Adobe Commerce Admin. När det är aktiverat kan `Search Weight` anges för attributet.

[!DNL Live Search] indexerar inte borttagna produkter eller produkter som är inställda på `Not Visible Individually`.

>[!NOTE]
>
> Commerce-kunder med [!DNL Live Search] kan dra nytta av snabbare prisändringar och synkroniseringstid på sina webbplatser med prisindexeraren [SaaS](../price-index/price-indexing.md).

## Indexerar pipeline

Klienten anropar söktjänsten från butiken för att hämta (filterbara, sorterbara) indexmetadata. Det går endast att anropa sökbara produktattribut med egenskapen *Använd i lagernavigering* inställd på `Filterable (with results)` och *Använd för sortering i produktlista* inställd på `Yes`.

Om du vill skapa en dynamisk fråga måste söktjänsten känna till vilka attribut som är sökbara och deras [vikt](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search-results). [!DNL Live Search] respekterar Adobe Commerce sökvikter (1-10, där 10 är den högsta prioriteten). Listan med data som synkroniseras och delas med katalogtjänsten finns i schemat, som definieras i:

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] indexerar klientens sökdiagram &#x200B;](assets/indexing-pipeline.svg)

1. Kontrollera om säljaren har rätt till [!DNL Live Search].
1. Hämta butiksvyer med ändringar i attributmetadata.
1. Lagra indexeringsattribut.
1. Indexera om sökindexet.

### Fullständigt index

När [!DNL Live Search] har konfigurerats och synkroniserats under introduktionen kan det ta upp till 60 minuter att skapa det inledande indexet. Stora kataloger kan ta längre tid att indexera. Processen börjar efter att `cron` har skickat feeden och slutar köras.

Följande händelser utlöser en fullständig synkronisering och indexgenerering:

* [Katalogdatasynkronisering av introduktion](install.md#synchronize-catalog-data)
* Ändringar av attributmetadata

Om du till exempel ändrar egenskapen `Use in Search` för attributet `color` från `No` till `Yes` ändras attributets metadata till `searchable=true` och en fullständig synkronisering och omindexering aktiveras. Följande attributmetadata utlöser en fullständig synkronisering och omindexering när de ändras:

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### Direktuppspelande produktuppdateringar

När det inledande indexet har skapats under [onboarding](install.md#synchronize-catalog-data) synkroniseras och indexeras följande stegvisa produktuppdateringar kontinuerligt:

* Nya produkter som lagts till i katalogen
* Ändringar av produktattributvärden

Om du till exempel lägger till ett nytt färgrutevärde i attributet `color` hanteras det som en direktuppspelad produktuppdatering.

Arbetsflöde för direktuppspelning av uppdatering:

1. Uppdaterade produkter synkroniseras från Adobe Commerce-instansen till katalogtjänsten.
1. Indexeringstjänsten söker kontinuerligt efter produktuppdateringar från katalogtjänsten. Uppdaterade produkter indexeras allt eftersom de kommer in i katalogtjänsten.
1. Det kan ta upp till 15 minuter innan en produktuppdatering blir tillgänglig om [!DNL Live Search].

#### Uppdateringar som påverkar synligheten

När du uppdaterar [!DNL Live Search] Admin-konfigurationsinställningar, konfigurationsinställningar för Adobe Commerce Admin eller uppdateringar av katalogdata kan du förvänta dig en fördröjning innan dessa ändringar visas i butiken.

I följande tabell beskrivs olika ändringar och den ungefärliga väntetiden innan de visas i butiken.

| Uppdateringar | Fördröj tills den syns i butiken |
|---|---|
| [!DNL Live Search] Administratören ändrar till facets, prisinställningar, regler för sökning eller kategoriförsäljning. | 15-20 minuter. |
| [!DNL Live Search] Administratörsändringar som kräver omindexering: språkinställningar eller synonymer. | Upp till 15 minuter efter att omindexeringen är klar. |
| Ändringar i Adobe Commerce Admin som kräver en fullständig indexering: sökbara, sorterbara eller filterbara attributmetadata | Upp till 15 minuter efter att omindexeringen är klar. |
| Inkrementella förändringar i katalogdata som inte behöver omindexeras: produktlager, pris, namn och så vidare. | Upp till 15 minuter efter att indexet för den elastiska sökningen har uppdaterats med de senaste data. |

## Klientsökning

Med API:t [!DNL Live Search] kan en klient sortera efter ett sorterbart produktattribut genom att ställa in egenskapen [storefront](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/product-attributes), *Används för sortering i produktlistor* på `Yes`. Beroende på temat gör den här inställningen att attributet inkluderas som ett alternativ i sidnumreringskontrollen [Sortera efter](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/navigation/navigation) på katalogsidor. Upp till 200 produktattribut kan indexeras av [!DNL Live Search], med [storefront-egenskaper](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/product-attributes) som är sökbara och filterbara.

Indexmetadata lagras i indexeringsflödet och är tillgängliga för söktjänsten.

![[!DNL Live Search] API-diagram för indexmetadata &#x200B;](assets/index-metadata-api.svg)

### Sorterbart attributarbetsflöde

1. Klienten anropar söktjänsten.
1. Söktjänsten anropar söktjänsten.
1. Söktjänsten anropar indexeringsflödet.

## Indexerad för alla produkter

Fältens ordning i den här listan återspeglar den typiska ordningen för kolumner i exporterade produktdata.

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

Följande fält är indexerat för alla konfigurerbara produkter:

* `childrenSkus`
