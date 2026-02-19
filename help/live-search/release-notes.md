---
title: Versionsinformation för [!DNL Live Search]
description: Den senaste versionsinformationen för  [!DNL Live Search] från Adobe Commerce.
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: 85753091e3f7708c65cc8465050d03f44add04ae
workflow-type: tm+mt
source-wordcount: '2688'
ht-degree: 0%

---

# Versionsinformation för [!DNL Live Search]

De här versionsinformationen beskriver de senaste versionerna av [!DNL Live Search].

Support ges för den senaste versionen. Versionsinformation för äldre versioner finns som referens.
Bland uppdateringarna finns:

![Nya](../assets/new.svg) nya funktioner
![Korrigera &#x200B;](../assets/fix.svg) Korrigeringar och förbättringar
![Fel](../assets/bug.svg) Kända fel

## Uppdateringar av värdtjänster

Dessa anteckningar beskriver uppdateringar som publicerats utanför en versionshanteringsversion eller förbättringar av värdtjänsten.

_1 oktober 2025_

![Nytt](../assets/new.svg) har lagt till ny datalagringsnyckel med namnet `ds-logged-in` för kundinloggade data.

_29 april 2025_

![Korrigera](../assets/fix.svg) Ett fel har korrigerats där rapporten **Exportera till CSV** på fliken [**Prestanda**](./performance.md) inte innehöll alla data som angavs i datumintervallet.
![Korrigera](../assets/fix.svg) Ett fel har korrigerats där du inte kunde spara en [försäljningsregel](./rules.md) om sökfrågefiltret användes.
![Åtgärda](../assets/fix.svg) Ett problem har korrigerats där [fästa produkter](./facets-manage.md#pinunpin-facet) inte fanns med överst på resultatsidan.

_21 april 2025_

![Korrigera](../assets/fix.svg) Ett problem med intervallfiltret för priser har korrigerats så att produkter som är lika med det övre intervallet inte tas med i resultatet. Den här ändringen anpassas till hur prisintervall definieras för facets.

_3 april 2025_

![Korrigera](../assets/fix.svg) Tillägget SaaS-dataexport har uppdaterats för att ta bort&quot;Produkterna måste tilldelas till rotkategorin&quot; [begränsning](boundaries-limits.md#b2b-and-category-permissions) för B2B-handlare. Se [Hantera tillägget för dataexport](../data-export/manage-extension.md) om du vill veta mer om hur du uppdaterar tillägget SaaS-dataexport till version 103.4.0+.

_20 februari 2025_

![Nytt](../assets/new.svg) Commerce har stöd för synonymer med flera ord. [Läs mer](synonyms-type.md#multi-word-synonym-behavior). Stöd för synonymer med flera ord är endast tillgängligt efter den 20 februari-utgåvan. Alla befintliga synonymer med flera ord kräver ett fullständigt indexvärde för att fungera, vilket du kan begära genom att [skapa en supportbiljett](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

_31 januari 2025_

![Nytt](../assets/new.svg) Det finns en ny datalagringsprincip för oefterfrågade katalogdata i testmiljön. [Läs mer](overview.md#catalog-data-retention-policy).

_19 september 2024_

![Ny](../assets/new.svg) Beta-version för följande avancerade sökfunktioner: sökning i lager med `startsWith` och `contains`. [Läs mer](workspace.md#layered-search-and-expansion-of-search-types).

_4 september 2024_

![Korrigera](../assets/fix.svg) Ökade det maximala antalet bucklar som kan returneras [&#x200B; inom en facet](boundaries-limits.md#facets) till 100.

_7 augusti 2024_

![Korrigera](../assets/fix.svg) Ökade det maximala intervallvärdet eller prisintervallet för [prisutjämning](settings.md#price-faceting) från 10 000 till 40 000 000.

_13 februari 2024_

![Nytt](../assets/new.svg) [!DNL Live Search] har nu stöd för att ange en standardregel för [Söka efter marknadsföring](rules.md).

_12 oktober 2023_

![Nya](../assets/new.svg) Commerce-administratörer kan nu ange indexspråket för [!DNL Live Search]. Se [Inställningar](settings.md).
![Korrigera](../assets/fix.svg) Fliken Sökregler har bytt namn till Sökmarknadsföring.

_13 juni 2023_

![Korrigera](../assets/fix.svg) Ett fel har korrigerats där vissa tecken som citattecken eller apostrofer orsakade rankningsproblem. Omindexering löser dessa problem.

_25 april 2023_

![Nya](../assets/new.svg) [!DNL Live Search]-kunder kan nu dra nytta av den nya prisindexeraren [SaaS](../price-index/price-indexing.md).

### PLP-widget

_2 februari 2026_

![Åtgärda](../assets/fix.svg) Ett fel i PLP-version 2.3.0 där webbläsarens bakåtknapp inte uppdaterade sidnumreringsstatusen i PLP-widgeten har korrigerats.

_22 maj 2025_

![Korrigera](../assets/fix.svg) Ett problem där knappen Lägg till i kundvagnen var på engelska när språkinställningen ändrades till franska, tyska, italienska eller spanska har korrigerats.
![Korrigera](../assets/fix.svg) Ett fel har korrigerats där knappen Lägg till i kundvagnen visades för produkter som inte finns i lager.

_31 maj 2024_

![Nytt](../assets/new.svg) Version 2.0.0 av PLP-widgeten har släppts. Den har stöd för följande funktioner:

- Knapparna Lägg till i kundvagnen - endast för enkla produkter.
- Flera bilder per produkt - Bilden kan ändras när en annan färg väljs för en konfigurerbar produkt.

_27 oktober 2023_

![Nytt](../assets/new.svg) PLP-widgeten [!DNL Live Search] har nu stöd för färgrutor.

## [!DNL Live Search] 4.6.1

_19 februari 2026_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Ett fel som kan inträffa under vissa förhållanden som rör funktionen för Visual Merchandiser-tillägget.

## [!DNL Live Search] 4.6.0

_9 oktober 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) GA-version för följande avancerade sökfunktioner: sökning i lager med `startsWith` och `contains`. [Läs mer](workspace.md#layered-search-and-expansion-of-search-types).
![Korrigera](../assets/fix.svg) Objektet `ProductInterface` i tjänsten [Live Search](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) har tagits bort. Använd objektet `ProductView` i katalogtjänsten i stället.

## [!DNL Live Search] 4.5.0

_5 september 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Live Search respekterar nu till fullo [läget för begränsning av cookies](install.md#cookies) genom att datainsamling och lagring i cookies/lokal lagring förhindras när begränsningar aktiveras.

## [!DNL Live Search] 4.4.1

_11 augusti 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Åtgärdade katalogtjänstslutpunkter för sandlådemiljöer.

## [!DNL Live Search] 4.4.0

_14 juli 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Ökade gränsen för [prisgruppering](./settings.md#price-faceting) från 50 till 100.

## [!DNL Live Search] 4.3.0

_11 mars 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) [!DNL Live Search] har nu stöd för PHP 8.4 för installationer som kör Adobe Commerce 2.4.8-beta2.
![Korrigera](../assets/fix.svg) Ett fel har korrigerats där sökadaptern inte var kompatibel med `psr/http-message:2.0`.

## [!DNL Live Search] 4.2.3

_13 februari 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Ett problem där orderdetaljsidan saknade ordernummer, datum och knappen **[!UICONTROL Reorder]** har åtgärdats.

## [!DNL Live Search] 4.2.2

_6 januari 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Åtgärda](../assets/fix.svg) Ett fel som orsakade ett fel med `categoryList` GraphqL-frågan i Adobe Commerce version 2.4.5 och tidigare har korrigerats.

## [!DNL Live Search] 4.2.1

_31 juli 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Ett fel har korrigerats där vissa skript inte lästes in på utcheckningssidan.
![Korrigera](../assets/fix.svg) Korrigerade en beroendeversion i filen `composer.json`.

## [!DNL Live Search] 4.2.0

_31 maj 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Uppdaterat Live Search-tillägg för att använda PLP-widgetar version 2.0.0.

## [!DNL Live Search] 4.1.2

_16 maj 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

### Uppdateringar

![Korrigera](../assets/fix.svg) Korrigerade GraphQL-frågan [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) så att den filtreras korrekt baserat på kategorierna `categoryPath` och `categoryList`.

## [!DNL Live Search] 4.1.1

_19 mars 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

### Nya funktioner

![Nytt](../assets/new.svg) språkstöd för polska har lagts till.
![Nytt](../assets/new.svg) [!DNL Live Search] stöder nu PHP 8.3 för installationer som kör Adobe Commerce 2.4.4.

## [!DNL Live Search] 4.1.0

_22 februari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

### Nya funktioner

![Nytt](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) är nu tillgängligt. Den här förbättrade instrumentpanelen ger insikter i dataströmmar för [!DNL Product Recommendations], [!DNL Live Search] och [!DNL Catalog Service].

### Uppdateringar

![Åtgärdade](../assets/fix.svg) ett fel som orsakade ett fel när gästanvändare lade till produkter i en varukorg i icke-standardbutiksvyer.
![Korrigera](../assets/fix.svg) Ett problem som gjorde att sökleverantören alltid visade valutasymbolen framför prisvärdet oavsett språkinställningar har korrigerats.
![Korrigera](../assets/fix.svg) Onödiga typdefinitioner för inaktiverade insticksprogram har tagits bort för att korrigera kompatibilitetsproblem vid installationen.

## [!DNL Live Search] 4.0.0

_13 november 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

### Nya funktioner

![Nytt](../assets/new.svg) [!DNL Live Search] stöder nu färgrutor i PLP-widgeten.
![Nytt](../assets/new.svg) [!DNL Live Search] visar nu kategorinamnet i stället för kategori-ID:t.
![Nytt](../assets/new.svg) [!DNL Live Search] har nu stöd för genomstrykningspris i PLP-widgeten.
![Nytt](../assets/new.svg) Knappen&quot;Dölj filter&quot; introducerades för att dölja filterpanelen.


### Uppdateringar

![Korrigera](../assets/fix.svg) PLP-widgeten [!DNL Live Search] är nu aktiverad som standard för nya installationer.
![Korrigera](../assets/fix.svg) Sökkortet är inaktuellt. Framöver kommer sökadaptern endast att uppdateras för att åtgärda säkerhetsproblem.
![Korrigera](../assets/fix.svg) Omkonfigurerade CSS-format för att isolera widgetklasser bättre.
![Åtgärda](../assets/fix.svg) Mindre felkorrigeringar

Efter installation av version 3.1.1 eller senare aktiverar du de nya indexerarna:

- Produktprisfeed
- Omfattningar av webbplatsens dataflöde
- Omfattningar av kundgruppsdatafeed

När du har uppgraderat testar du den uppdaterade konfigurationen i QA eller Staging innan du överför ändringarna till produktionen.

+++3.1.1 och tidigare versioner

### [!DNL Live Search] 3.1.1

_15 september 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) Ny flik för kategorimarknadsföring har lagts till. Nu kan man lägga in intelligenta rankningar och manuella rankningar (stift, boost, bury, hide) per kategori
![Nya](../assets/new.svg) användare kan lägga till en enskild kategoriregel med intelligent eller manuell rankning
![Nyhet](../assets/new.svg) Användare kan nu lägga till regler för intelligent rankning i underkategorier
![Nytt](../assets/new.svg) Detaljerad information ges när underkategorier tas bort med intelligent rankning
![Nytt](../assets/new.svg) Möjligheten att ta bort regler för ärvda rankningsstrategier har lagts till
![Nytt](../assets/new.svg) Lägg till möjligheten att ta bort regler för en enskild kategori
![Nya](../assets/new.svg) -användare kan nu söka efter kategorinamn när de lägger till en regel
![Nytt](../assets/new.svg) I kategoriträdvyn kan användare nu visa vilken kategori som har regler.
![Ny](../assets/new.svg) kategoriförhandsvisning visar bara den valda kategorin.
![Med komponenterna &#x200B;](../assets/new.svg) AEM CIF [Positionwidget](https://github.com/adobe/aem-cif-guides-venia/pull/319) och [PLP-widget](https://github.com/adobe/aem-cif-guides-venia/pull/320) kan AEM webbplatser dra nytta av [!DNL Live Search].

#### Uppdateringar

![Korrigera](../assets/fix.svg) Tabellstorleken för produkt- och prisfeeds har reducerats avsevärt. Tabellerna `catalog_data_exporter_products` och `catalog_data_exporter_product_prices` bör se en betydande storleksminskning.
![Korrigera](../assets/fix.svg) Fliken Regler har bytt namn till Sökregler
![Korrigera](../assets/fix.svg) När du rangordnar efter &#39;trending&#39; kan du nu välja mellan:
- 3 dagar (standard)
- 14 dagar
- 30 dagar
![Åtgärda](../assets/fix.svg) händelser (Öka/Fäst/Bränn/Dölj) har bytt namn till Manuell rankning
![Korrigera &#x200B;](../assets/fix.svg) rankningstyp har bytt namn till Intelligent ranking
![Korrigera &#x200B;](../assets/fix.svg) Mindre felkorrigeringar

### [!DNL Live Search] 3.1.0

_1 september 2023_

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

#### Uppdateringar

![Korrigera](../assets/fix.svg) Produktlistwidgeten har uppdaterats för att använda [katalogtjänstens API &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).

### [!DNL Live Search] 3.0.2

_7 augusti 2023_

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

#### Nya funktioner

![Nytt](../assets/new.svg) Följande värden har lagts till i objektet `storeDetails`:

- &quot;Tillåt alla produkter per sida&quot;
- Valutakurs
- &quot;Produkter per sida på tillåtna värden för stödraster&quot;
- &quot;Produkter per sida på standardvärde för stödraster&quot;
- Butiksspråk

#### Uppdateringar

![Korrigera](../assets/fix.svg) katalogtjänstmoduler har lagts till i metapaketet för att ge stöd för avancerad datahämtning.
![Åtgärda](../assets/fix.svg) Sidnavigeringen **Mitt konto** försvinner inte längre när du använder widgeten Produktlistsida.

Merchants måste uppgradera tilläggsversionen [!DNL Live Search] >= 3.0.2 för att få tillgång till dessa funktioner.

Vi rekommenderar att du uppgraderar och testar innan du går till produktion. Överväg att uppgradera produktionsmiljön under tider med låg belastning efter att ha verifierat testmiljöresultaten.

#### Begränsningar

När du använder widgeten Listsida för produkter i Live Search misslyckas Google Tag Manager. Använd standardsökkortet om Google Tag Manager behövs.

### [!DNL Live Search] 3.0.1

_14 mars 2023_

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

#### Nya funktioner

![Nytt](../assets/new.svg) produktartikelkort i regelförhandsgranskning
![Nytt](../assets/new.svg) [Widgeten Produktlistsida](https://experienceleague.adobe.com/sv/docs/commerce/live-search/live-search-storefront/plp-styling)
![Nytt](../assets/new.svg) [Kategorifiltreringsalternativ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![Nytt](../assets/new.svg) har lagt till möjligheten att dra och släppa för att skapa Fäst-händelser
![Nya &#x200B;](../assets/new.svg) Fäst-åtgärder:
- Fäst på plats - Fäst knappen för att skapa Fäst-händelse med ett klick
- Fäst överst - Placerar produkten på första plats
- Fäst längst ned - Placerar produkten längst ned i resultaten
- Plocka upp en händelse med ett klick
![Nytt](../assets/new.svg) [Intelligent rankning av regler](https://experienceleague.adobe.com/sv/docs/commerce/live-search/live-search-admin/rules/rules-add)
![Nytt](../assets/new.svg) [!DNL Live Search] har nu stöd för alla [Inventory management](https://experienceleague.adobe.com/sv/docs/commerce-admin/inventory/introduction) -funktioner i Commerce (tidigare Multi-Source Inventory, eller MSI). Om du vill aktivera fullständigt stöd måste du [uppdatera](install.md#update) beroendemodulen `commerce-data-export` till version 102.2.0+.

#### Uppdateringar

![Korrigera](../assets/fix.svg) Konfigurera regler sorterar nu positioner automatiskt
![Korrigera &#x200B;](../assets/fix.svg) Om du tar bort en befintlig händelse uppdateras nu förhandsvisningen
![Åtgärda](../assets/fix.svg) Regler utan händelser kan sparas
![Korrigera](../assets/fix.svg) Ta bort funktionsväljaren Välj typ
![Korrigera](../assets/fix.svg) Ny redigeringsstatus för osparade regler har lagts till

#### Korrigeringar

![Korrigera](../assets/fix.svg) Serverfel har korrigerats när en oavslutad händelse inträffar när filen sparades
![Korrigera &#x200B;](../assets/fix.svg) En korrekt borttagning av en specifik händelse när det finns flera händelser har åtgärdats
![Åtgärda](../assets/fix.svg) Den befintliga regelhändelsen som inte uppdateras när en ny händelse har lagts till har åtgärdats
![Korrigera &#x200B;](../assets/fix.svg) Korrigerad vid andra&quot;Redigera&quot;-klickning från detaljer, [!DNL Live Search] sidan måste läsas in igen
![Korrigera](../assets/fix.svg) synonymer: Ett problem har korrigerats när en användare klickade bort från indata, men det gick inte att returnera fokus till fältet
![&#x200B; Åtgärda &#x200B;](../assets/fix.svg) Andra mindre felkorrigeringar och prestandauppdateringar
![Fel &#x200B;](../assets/bug.svg) - Rankning med &quot;Rekommenderas för dig&quot; stöds bara i Live Search-widgetarna. Det stöds inte med standardsökfunktionerna för Luma och PWA.
![Fel](../assets/bug.svg) - Egna prisattributsaspekter återges inte korrekt i Luma, men API:t filtrerar dem korrekt.

Merchants måste uppgradera tilläggsversionen [!DNL Live Search] >= 3.0.1 för att få tillgång till dessa funktioner.

Vi rekommenderar att du uppgraderar och testar innan du går till produktion. Överväg att uppgradera produktionsmiljön under tider med låg belastning efter att ha verifierat testmiljöresultaten.

### [!DNL Live Search] 2.0.5

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) - Direktsökning genererar ett fel när SDK-resurser inte är tillgängliga på grund av nätverksproblem. Det här felet har åtgärdats.

Handläggarna måste uppgradera Live Search-tilläggsversionen >= 2.0.5 för att få tillgång till dessa funktioner.

Vi rekommenderar att du uppgraderar och testar innan du går till produktion. Överväg att uppgradera produktionsmiljön under tider med låg belastning efter att ha verifierat testmiljöresultaten.

### [!DNL Live Search] 2.0.4

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Live Search har nu stöd för filtrering med inställningen Visa utanför Stock-produkter i administratören. Om Visa utanför Stock-produkter är inställt på false läggs `inStock = true` till i filtret.
![Åtgärda](../assets/fix.svg) För att förbättra prestanda har blocket Förslag tagits bort från popup-fönstret Live Search. Data skickas fortfarande via GraphQL om du vill ersätta funktionen.
![Korrigera](../assets/fix.svg) `categories` och `categoryPath` har ersatt `categoryIds` för kategorifiltrering. Läs mer i avsnittet [productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).
![Åtgärda](../assets/fix.svg) Tidigare fick en användare som är knuten till ett B2B-företag en felaktig kundgruppskod när de gjorde sökningar. Live Search returnerar nu korrekt värde.
![Korrigera](../assets/fix.svg) Tidigare returnerades ett fel när du sökte efter en term som inte finns. Felet är nu åtgärdat.

Handlare måste uppgradera [!DNL Live Search]-tilläggsversionen >= 2.0.4 för att få tillgång till dessa funktioner.

Man rekommenderar att man uppgraderar och testar innan man går till produktion. Överväg att uppgradera produktionsmiljön under tider med låg belastning efter att ha verifierat testmiljöresultaten.

### [!DNL Live Search] 2.0.3

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Live Search har nu stöd för B2B-funktioner genom att hantera kategoribehörigheter, delade kataloger och kundgruppsspecifika priser.

Handlare måste uppgradera [!DNL Live Search]-tilläggsversionen >= 2.0.3 för att få tillgång till dessa funktioner.

Man rekommenderar att man uppgraderar och testar innan man går till produktion. Överväg att uppgradera produktionsmiljön under tider med låg belastning efter att ha verifierat testmiljöresultaten.

### [!DNL Live Search] 2.0

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

Befintliga [!DNL Live Search]-installationer måste uppgraderas till [!DNL Live Search] 2.0.0 för att kunna utnyttja följande nya funktioner, korrigeringar och förbättringar:

![Nytt](../assets/new.svg) [!DNL Live Search] stöder nu PHP 8.1 för installationer som kör Adobe Commerce 2.4.4.
![Nytt](../assets/new.svg) Modulen `Magento_ElasticsearchCatalogPermissionsGraphQl` läggs till i listan med moduler som inaktiveras under installationen.
![Nytt](../assets/new.svg) Antalet tillgängliga rader i [[!DNL storefront popover]](overview.md) kan konfigureras från *Admin*.
![Nytt](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/) stöds för [!DNL Live Search].
![Nytt](../assets/new.svg) Installationsprocessen [!DNL Live Search] uppdateras med avancerade processändringar.
![Åtgärda](../assets/fix.svg) [länken Avancerad sökning](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search) har tagits bort från sidfoten i förgrunden.
![Fel](../assets/bug.svg) Följande produktattribut stöds inte av [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) när de används i relation till betaversionen av PWA: `description`, `name`, `short_description`
![Fel](../assets/bug.svg) Betaversionen av PWA för [!DNL Live Search] stöder inte [händelsehantering](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/).

### [!DNL Live Search] 1.3.1

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Korrigera](../assets/fix.svg) [Eget prisattribut](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/attributes-input-types) returnerar inte längre ett fel när det konfigureras som en [facet](facets-add.md).
![Åtgärda](../assets/fix.svg) Ett fel som orsakade att ett fel uppstod när ingen [valutasymbol](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`) är tillgänglig har åtgärdats.
![Korrigera](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) visar nu [specialpriset](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/products/pricing/product-price-special) (minimipris) när det är tillgängligt.

### [!DNL Live Search] 1.3.0

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Ny](../assets/new.svg) [Performance](performance.md)-rapportinstrumentpanel ger insikt i söktermer som kunderna använder.
![Nytt](../assets/new.svg) [!DNL Live Search] [Store Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) ger åtkomst till ett gemensamt datalager med händelsepublicerings- och prenumerationstjänster samt mätvärden.
![Korrigera](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) har en ny `active`-klass för behållaren `.search-autocomplete` som styr synligheten.
![Korrigera](../assets/fix.svg) I butiken tas sidfotslänken [Sökvillkor](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search-terms) bort och dess cache inaktiveras för [!DNL Live Search]-installationer.
![Bug](../assets/bug.svg) Patch for Search Adapter hanterar dubblettprodukter.
![Fel](../assets/bug.svg) [!DNL Live Search] stöder [enskilda lagerplatser (fysiska)](https://experienceleague.adobe.com/sv/docs/commerce-admin/inventory/sources/sources-manage) med flera (virtuella) [stockar](https://experienceleague.adobe.com/sv/docs/commerce-admin/inventory/stocks/stocks-manage). Flera lagerkällor stöds inte nu.

### [!DNL Live Search] 1.2.0

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) visar föreslagna produkter och miniatyrbilder av de bästa sökresultaten som typfrågor för shoppare i sökrutan.
![Ny](../assets/new.svg) Commerce *Admin*-session förblir öppen under utökad inaktivitet på tangentbordet
![Nytt](../assets/new.svg) [!DNL Live Search] aktiveras automatiskt efter introduktionen
![&#x200B; Korrigera &#x200B;](../assets/fix.svg) Inledande indexeringstid är mindre än en timme
![Korrigera](../assets/fix.svg) stegvisa produktuppdateringar nära realtid (efter installation och installation)
![&#x200B; Korrigera &#x200B;](../assets/fix.svg) Sorterbara kolumner i synonymredigeraren
![&#x200B; Korrigera &#x200B;](../assets/fix.svg) [!DNL Live Search] genererar inte längre ett fel om sökvillkoren innehåller ett tomt sorteringsordningsvärde
![Korrigera &#x200B;](../assets/fix.svg) Intervallfiltrering fungerar inte längre om attributkoder innehåller strängarna &quot;to&quot; eller &quot;from&quot;

### [!DNL Live Search] 1.1.0

[!BADGE Stöds]{type="Informative" tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Fel](../assets/bug.svg) Tjänsten [!DNL Live Search] stöder endast [basvalutan](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) i Adobe Commerce-installationen.
![Fel](../assets/bug.svg) När du lägger till en fasett uppdateras inte produktattributsmatningen korrekt när värdet är `Update on Save`. Du undviker det här problemet genom att gå till [Indexhantering](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/tools/index-management) och ange produktattributsfeed till `Update by Schedule`.
Synonymer för ![Fel](../assets/bug.svg) [!DNL Live Search] definieras per butiksvy, men lagras för närvarande per webbplats och identifieras med en kombination av `environmentId` och `storeViewCode`. Därför delar alla webbplatser och vyer i Adobe Commerce-installationen synonymer. Den senast skapade uppsättningen synonymer för butiksvyn har företräde.
![Fel](../assets/bug.svg) Om en synonymterm innehåller flera ord behandlas varje ord som en separat synonym. Om du till exempel definierar&quot;tidsbit&quot; som en synonym till&quot;watch&quot;, behandlas både&quot;time&quot; och&quot;piece&quot; som synonymer för watch.

+++

## Dokumentation

Mer information:

- [Adobe Commerce Developer Documentation](https://developer.adobe.com/commerce/docs)
- [Adobe Commerce Användarhandbok](https://experienceleague.adobe.com/sv/docs/commerce)
- [[!DNL Live Search] på Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)
