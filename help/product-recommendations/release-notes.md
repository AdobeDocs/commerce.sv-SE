---
title: Versionsinformation för [!DNL Product Recommendations]
description: Den senaste versionsinformationen för  [!DNL Product Recommendations] från Adobe Commerce.
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: 30cbe1ed54dd8a1149afe9f5f77b1b6f543b277e
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---

# Versionsinformation för [!DNL Product Recommendations]

Versionsinformationen innehåller uppdateringar för följande [!DNL Product Recommendations] moduler:

* [!DNL Product Recommendations]-metapaket: `magento/product-recommendations`
* Stöd för Page Builder i modulen [!DNL Product Recommendations] (valfritt): `magento/module-page-builder-product-recommendations`
* Typstöd för visuell likhetsrekommendation för [!DNL Product Recommendations] (valfritt) modul: `magento/module-visual-product-recommendations`

Support ges för den senaste versionen. Versionsinformation för äldre versioner finns som referens.
Versionsinformationen innehåller:

![Nya](../assets/new.svg) nya funktioner
![Korrigera &#x200B;](../assets/fix.svg) Korrigeringar och förbättringar
![Fel](../assets/bug.svg) Kända fel

Läs utvecklardokumentationen för att [lära dig mer om produktsupport](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Uppdateringar av värdtjänster

Dessa anteckningar beskriver uppdateringar eller kända fel som har publicerats eller upptäckts utanför en versionshanteringsversion eller förbättringar av värdtjänsten.

_19 november 2025_

![Nytt](../assets/new.svg) Du kan nu skapa upp till 50 aktiva rekommendationsenheter för varje sidtyp. Tidigare var gränsen fem.

_1 oktober 2025_

![Nytt](../assets/new.svg) har lagt till ny datalagringsnyckel med namnet `ds-logged-in` för kundinloggade data.

_31 januari 2025_

![Nytt](../assets/new.svg) Det finns en ny datalagringsprincip för oefterfrågade katalogdata i testmiljön. [Läs mer](overview.md#catalog-data-retention-policy).

_28 juni 2024_

![Fel](../assets/bug.svg) Produkter som lagts till i kundvagnen från en [!DNL Product Recommendations]-enhet på kundvagnssidan tas inte bort från listan över rekommenderade produkter när kundvagnssidan läses in igen.
![Fel](../assets/bug.svg) Produkter som tagits bort från vagnen finns kvar i arrayen `cartSkus` tills kundvagnssidan läses in igen.

_18 juli 2023_

![Nytt](../assets/new.svg) [!DNL Product Recommendations] har nu en GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)-fråga.

_25 april 2023_

![Nya](../assets/new.svg) [!DNL Product Recommendations]-kunder kan nu dra nytta av prisindexering för [SaaS](../price-index/price-indexing.md).

## Aktuell huvudversion

### 6.5.0 magento/product-recommendations

_3 november 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Förbättrat hur enheter för produktrekommendationer interagerar i olika miljöer.

### Tidigare versioner

### 6.4.0 magento/product-recommendations

_17 september 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Ett tillfälligt problem där enheter för produktrekommendationer skulle försvinna på grund av ett JavaScript-fel när lokala lagringsdata inte var tillgängliga har åtgärdats. Den här korrigeringen ser till att PREX inte längre orsakar fel om `ds-view-history-time-decay` saknas i det lokala lagringsutrymmet.
![Nytt](../assets/new.svg) Uppdaterade CDN-URL:er för `recommendations-sdk` till domänen `adobe.io`.

### 6.3.0 of magento/product-recommendations

_5 september 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd har lagts till för att visa mått för [enheter för PageBuilder-rekommendationer](page-builder.md) som har skapats i butiksvyer som inte är standard på arbetsytan [Produktrekommendationer](workspace.md).
![Nytt](../assets/new.svg) Produktrekommendationer respekterar nu till fullo [läget för begränsning av cookies](setting-cookie.md) genom att datainsamling och lagring i cookies/lokal lagring förhindras när begränsningar har aktiverats.

### 6.2.1 of magento/product-recommendations

_14 juli 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Förbättrade [förhandsgranskningsrekommendationer](./create.md#preview-recommendations)-panelen.

### 6.2.0 of magento/product-recommendations

_4 april 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Uppdaterade CDN-URL:er för `recommendations-admin-ui` till domänen `adobe.io`.

### 6.1.0 of magento/product-recommendations

_11 mars 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd för PHP 8.4 har lagts till.

### 6.0.3 of magento/product-recommendations

_6 november 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Ett problem har korrigerats där [kategorifiltret](filters.md#category) innehöll kategorier som inte tillhör den aktuella granskningen.
![Åtgärda](../assets/fix.svg) Ett beroendeproblem i metapaketet `magento/product-recommendations` har korrigerats.

### 6.0.2 of magento/product-recommendations

_9 maj 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Ett fel har korrigerats där användaren omdirigerades till hemsidan i stället för att stanna kvar på den aktuella sidan genom att klicka på knappen **[!DNL Add to Cart]** på en enkel produkt i en produktrekommendationsenhet.
![Fel](../assets/bug.svg) Det finns ett valideringsfel som orsakas av elementet `referenceBlock` i XML-filen `ProductRecommendations Layout`.

### 6.0.1 of magento/product-recommendations

_19 mars 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd för PHP 8.3 har lagts till.

### 6.0.0 av magento/product-recommendations

_22 februari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) [!DNL Catalog Sync Dashboard] är nu [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Den här förbättrade instrumentpanelen ger insikter i dataströmmar för [!DNL Product Recommendations], [!DNL Live Search] och [!DNL Catalog Service].
![Åtgärda](../assets/fix.svg) Ett problem som orsakade utcheckningsfel för [!DNL Product Recommendations] har korrigerats.

+++5.0.0 och tidigare versioner

### 5.0.1 of magento/product-recommendations

_15 september 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) har lagt till nya moduler som stöder prisindexeraren [Saas](../price-index/price-indexing.md).
![Nytt](../assets/new.svg) har lagt till nya dataexportmoduler som stöd för export av fler produkttyper, inklusive paketerade produkter och presentkort.
![Korrigera](../assets/fix.svg) Tabellstorleken för produkt- och prisfeeds har reducerats avsevärt. Tabellerna `catalog_data_exporter_products` och `catalog_data_exporter_product_prices` bör se en betydande storleksminskning.

#### Kända begränsningar

* Värdet `websiteCode` returneras felaktigt om det innehåller ett understreck (_).

### 5.0.0 av magento/product-recommendations

_20 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Uppdaterat [!DNL Product Recommendations] med stöd för Adobe Commerce 2.4.6.
![Nytt](../assets/new.svg) Det här är en större version. [Redigera](install-configure.md#update) rotfilen `composer.json` för ditt projekt.
![Nytt](../assets/new.svg) [!DNL Product Recommendations] har nu stöd för fullständiga [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)-funktioner i Commerce (tidigare Multi-Source Inventory, eller MSI).   Om du vill aktivera fullständigt stöd måste du [uppdatera](install-configure.md#update) beroendemodulen `commerce-data-export` till version 102.2.0+.

### 4.0.1 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Tidigare visades ett fel i [!DNL Product Recommendations] när visningsvalutan växlades till en annan valuta än standardvalutan. Växling av valutor fungerar nu korrekt.

### 4.0.0 av magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) [beredskapsindikatorer](create.md) har lagts till för att hjälpa dig visualisera utbildningsförloppet för varje rekommendationstyp.
![Nytt](../assets/new.svg) Det här är en större version. [Redigera](install-configure.md#update) rotfilen `composer.json` för ditt projekt. Den här versionen kräver också att du tillhandahåller två API-nycklar när du installerar och konfigurerar [!DNL Product Recommendations]: [en produktionsnyckel och en sandlådenyckel](../landing/saas.md).

#### Kända begränsningar

* Värdet `websiteCode` returneras felaktigt om det innehåller ett understreck (_).

### 3.3.7 i magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Stöd för PHP 8.1 har lagts till
![Nytt](../assets/new.svg) Förbättrad storleksändring av bilder så att bildstorleksändring hanteras mer konsekvent i referensvisningsmallen

### 3.3.6 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Optimerat [!DNL Product Recommendations]-metapaket genom att explicit visa beroenden

### 3.3.5 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) [Stöd för B2B](onboarding.md#b2bsupport) har lagts till i [!DNL Product Recommendations]
![Nytt](../assets/new.svg) Nya feeds har lagts till i [synkronisera katalogdata](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) till Commerce Services via kommandoraden

### 3.3.3 i magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Ny](../assets/new.svg) har lagt till nya [rekommendationstyper](type.md): Konvertering (visa till kundvagn), Konvertering (visa till köp) och Senast visade. Dessa nya rekommendationstyper är tillgängliga i `magento/product-recommendations` modul 3.2.2 och senare.
![Korrigera](../assets/fix.svg) Ett problem där Fastly&#39;s Web Application Firewall (WAF) blockerade en cookie på ett felaktigt sätt har åtgärdats
![Åtgärda](../assets/fix.svg) Ett problem har korrigerats där produkter som tilldelats den icke-förvalda butiksvyn inte visades på panelen _Rekommendationer_ när en rekommendation skapades för den speciella butiksvyn
![Åtgärda](../assets/fix.svg) Ett problem har korrigerats där vissa rekommendationsenhetsnamn i Page Builder hindrade rekommendationsenheten att visas i butiken

### 3.3.2 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Korrigera](../assets/fix.svg) Ett saknat beroende för B2B-stöd har korrigerats

### 3.3.1 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Stöd för B2B-kundgruppspriser har lagts till. När du anger ett [prisfilter](filters.md) på en rekommendationsenhet kan B2B-kunder som är inloggade se kundgruppens priser för produkterna som visas.

### 3.3.0 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Stöd för Adobe Client Data Layer har lagts till för att standardisera beteendedatainsamling för alla funktioner och tjänster i Adobe Commerce. Mer information finns i [Viktigt](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md).

### 3.2.6 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Korrigera](../assets/fix.svg) Ett modalt JavaScript-fel har korrigerats
![Korrigera &#x200B;](../assets/fix.svg) Ett problem där Fastly&#39;s Web Application Firewall (WAF) blockerade en cookie på ett felaktigt sätt har åtgärdats

### 3.2.5 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) har ändrat namn på Magento Services till [Commerce Services](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) och förbättrat användbarheten i Admin

### 3.2.4 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Åtgärda](../assets/fix.svg) Felet&quot;Det gick inte att hämta data för konfigurerbara produktalternativ&quot; vid indexering av produktattribut har åtgärdats

### 3.2.3 i magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Åtgärda](../assets/fix.svg) Felet&quot;Det gick inte att hämta data för konfigurerbara produktalternativ&quot; under katalogsynkronisering har åtgärdats
![Åtgärda](../assets/fix.svg) Ett problem där butikskoden inte ställdes in korrekt när du aktiverade konfigurationen Lägg till butikskod i URL har åtgärdats
![Åtgärda](../assets/fix.svg) Förbättrad identifiering av ändringar i administratörspanelens konfiguration för att se till att ändringarna återspeglas i data för katalogsynkronisering

### 3.2.2 av magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) har lagt till möjligheten att [förhandsgranska rekommendationsresultat](create.md) när den skapades. Du kan behöva uppdatera modulen till den senaste versionen.
![Nytt](../assets/new.svg) har lagt till möjligheten att [övervaka och hantera](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) katalogsynkroniseringsprocessen från administratören.
![Nytt](../assets/new.svg) [filter](filters.md) har lagts till för att kontrollera vilka produkter som visas i rekommendationerna.
![Ny](../assets/new.svg) har lagt till rekommendationstypen [Visuell likhet](type.md#visualsim).

### 1.2.1 of magento/module-page-builder-product-recommendations for Page Builder

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Stöd har lagts till för version 3.2.0+ av modulen `magento/product-recommendations`

### 3.1.0 av magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) har lagt till möjligheten att [synkronisera om](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) din katalog till SaaS-tjänster via kommandoraden.
![Nytt](../assets/new.svg) Stöd har lagts till för databastabellprefix
![Korrigera &#x200B;](../assets/fix.svg) PHP 7.1-stödet har tagits bort

### 3.0.8 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Åtgärda](../assets/fix.svg) Ett problem där händelser skickades för datainsamling innan modulen konfigurerades har korrigerats, vilket orsakade ogiltig trafik

### 3.0.6 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) **(Beta)** Innehåller stöd för den nya rekommendationstypen [Visuell likhet](type.md#visualsim).

### 1.0.0 av magento/module-visual-product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) **(Beta)** [Visuell likhet](type.md#visualsim). Med rekommendationstypen _Visuell likhet_ kan du distribuera en rekommendationsenhet till produktinformationssidan som visar produkter som visuellt liknar den produkt som visas.

### 3.0.5 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Korrigera](../assets/fix.svg) Felet&quot;Det gick inte att hämta produktalternativdata&quot; som kunde inträffa vid katalogexport har åtgärdats.
![Korrigera](../assets/fix.svg) Valutasymbolen i kolumnen _Intäkter_ på kontrollpanelen _[!DNL Product Recommendations]_&#x200B;återspeglar nu korrekt den konfigurerade basvalutan.

### 3.0.4 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Korrigera](../assets/fix.svg) Stöd för Adobe Commerce 2.4.0 har lagts till

### 3.0.3 i magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Korrigera](../assets/fix.svg) Förbättrad symbolimplementering i butiksmallen

### 1.0.4 of magento/module-page-builder-product-recommendations for Page Builder

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Produktrekommendationsnamn lades till när Page Builder-innehållstypen redigerades

### 3.0.2 magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) lade till en statuskolumn i rutnätet när rekommendationsenheter väljs i Page Builder
![Åtgärda](../assets/fix.svg) Ett problem med felaktiga http-/https-protokoll i produkt- och bild-URL:er har korrigerats

### 3.0.1 of magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

Det här är en större version. [Redigera](install-configure.md#update) projektets rotfil Composer.json.

![Nytt](../assets/new.svg) Hämta [!DNL Product Recommendations] från alternativa SaaS-datautrymmen. Detta gör att du kan använda [!DNL Product Recommendations] som beräknas i din produktmiljö i andra icke-produktionsmiljöer. [Växling av SaaS-datautrymmen](settings.md) beskriver den här funktionen ytterligare.

![Korrigera](../assets/fix.svg) Ett problem där utcheckning hämtades för kunder som använde Block Origin har korrigerats
![Korrigera &#x200B;](../assets/fix.svg) Ett problem med att skicka ovidkommande tilläggshändelser i kundvagnen har korrigerats

### 1.0.3 av magento/module-page-builder-product-recommendations for Page Builder

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) stöd för Page Builder. Med integreringen i Page Builder kan du exakt och exakt placera rekommendationsenheter på valfri plats i innehåll som skapats i Page Builder. Du kan också formatera rubrikerna och rekommendationsenheterna själva. Mer information finns i [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations).

### 2.0.0 av magento/product-recommendations

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Ny](../assets/new.svg) allmän tillgänglighetsversion!

+++

## Dokumentation

Mer information om utveckling av [!DNL Product Recommendations] och [!DNL Product Recommendations]:

* [Användarhandbok](overview.md)
* [Utvecklardokumentation](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
