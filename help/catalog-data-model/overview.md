---
title: '[!DNL Composable Catalog Data Model]'
description: Lär dig hur du med  [!DNL Composable Catalog Data Model] for Adobe Commerce kan konfigurera din katalog så att den matchar din affärsmodell och din marknadsstrategi
hidefromtoc: true
hide: true
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 0%

---

# [!DNL Composable Catalog Data Model]

En produktkatalog är väsentlig för shoppingupplevelser online, så att kunderna kan bläddra, söka och göra inköp. För en effektiv drift bör en produktkatalog nära återspegla företagets affärsstruktur. Företag behöver ofta sälja produkter till olika priser baserat på geografisk marknad, distributionskanal, kundsegment och andra variabler. För att tillgodose detta måste en e-handelsplattform erbjuda en flexibel katalogdatamodell som gör det möjligt för företag att producera variationer av sin katalog som är anpassade till dessa scenarier. Adobe Commerce Composable Catalog Data Model (CCDM) tillgodoser dessa behov. CCDM innehåller byggstenar som handlare kan använda för att skapa och hantera kataloger i stor skala. På så sätt kan företag konfigurera kataloger som är anpassade till deras affärsstruktur och go-to-market-strategier.

På en hög nivå kan du med CCDM:

- Använd en enda baskatalog för alla era affärsbehov. Skala upp katalogen snabbt på nya varumärken, marknader, affärsenheter, marknadskanaler och kundsegment utan behov av en fullständig omarkitektur. På så sätt slipper du datadubbletter och konfigurerar e-handelsplattformen för hög driftseffektivitet.
- Lås upp katalogsyndikering och leverera rätt innehåll genom att designa din produktkatalog så att den återspeglar din verksamhet, inklusive produkter, kunder, priser och distribution.
- Importera och uppdatera katalogdata snabbt och leverera snabbt uppdateringar till butiken för era kampanjer och kampanjbehov.
- Få perfekta fyrar med färdiga, blixtsnabba användargränssnittskomponenter som bygger på Edge Delivery Services för smidig bläddring och rekommendationer.
- Använd en modern sammansättningsbar arkitektur med hjälp av Adobe utbyggbarhetsarkitektur ([App Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development)) för att importera produktdata och driva headless-butiker med Adobe [API Mesh](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh).

>[!INFO]
>
>Mer information om API:erna i CCDM finns i [utvecklardokumentationen](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Arkitektur

CCDM är en mycket skalbar, flexibel katalogdatamodell som enkelt kan låsa upp flerspråkiga användningsfall för enheter med flera varumärken. Modellen ersätter användningen av de klassiska Adobe Commerce-produktomfången (webbplats, butik, butiksundersökning) med nya CCDM-produktomfång (kanal, policy och språkområde).

I följande diagram visas CCDM-ramverket på hög nivå.

![[!DNL Composable Catalog Data Model]-arkitektur](assets/ccdm-architecture.png)

Högst upp i det här diagrammet hämtas katalogdata (PIM, ERP o.s.v.) in i CCDM-ramverket. Katalogdata innehåller SKU:er. Varje SKU innehåller information om omfång (språkområde) och produktattribut, som mappas till de nya CCDM-produktomfånget (kanaler, principer och språkområde).

När alla dessa data är insamlade i CCDM-ramverket blir resultatet en ny enhetlig baskatalog som är tillgänglig i dataledningen för katalogtjänsten. I nästa del av diagrammet visas flera kanaler. Varje kanal representerar en affärsenhet. Exempel: *Texas Retail*, *Texas retail säsononal* osv. Som du kan se i diagrammet kan alla språkområden, policyer och prisböcker delas över alla kanaler. &#x200B;

Slutligen visar diagrammet hur distinkta katalogdata kan visas på olika platser, t.ex. en Edge Delivery Services-butik, en marknadsplats, en reklamkanal, en anpassad mikrobutik osv.

Mer information om hur du kan importera katalogdata till CCDM med hjälp av API:t för att hämta katalogdata och hur du konfigurerar dina språkområden, principer och prisböcker med hjälp av API:t för kataloghantering och regler finns i [utvecklardokumentationen](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Om du vill veta mer om de koncept som CCDM består av kan du läsa följande avsnitt.

## Hantering av produktkataloger

Produktkataloghantering omfattar två skilda aspekter: produktdata och produktsammanhang. CCDM respekterar separationen av dessa skyldigheter och erbjuder oberoende förvaltning för varje.

- **Produktdata** - Vilken produkt säljs och till vilket pris?
- **Produktkontext** - Vem säljer till vem och var?

![[!DNL Composable Catalog Data Model] aspekter ](assets/ccdm-parts.png)

### Produktdata

Produktdata innehåller följande typer:

- **Produkter** - Individuella SKU:er eller samlingar av SKU:er som representerar fysiska varor eller immateriella tjänster med attribut som representerar produkten, inklusive beskrivning, vikt, storlek, dimensioner med mera. Attribut anger också kanal- och principomfattningar för en SKU. Produkterna kan grupperas i olika produkttyper, t.ex. enkla, konfigurerbara produkter, paket, paket med paket, prenumerationer med mera.
- **Metadata** - Produktattributmetadata definierar och hanterar hur produktattribut visas på butiken i produktlistor, detaljsidor, sökresultat och så vidare. Metadata definierar också hur produktattribut används i sökningar - sortering, filtrering, sökvikter och så vidare.
- **Prisböcker och priser** - Bestämmer försäljningspriserna för produkter. I CCDM är en produkt-SKU och ett pris fristående, vilket innebär att du kan definiera flera prislistor för en enda SKU. Genom att koppla loss priserna från SKU:n kan ni låsa upp omfattningsspecifika priser för olika kundnivåer, affärsenheter och geografiska platser. Du kan definiera vanliga och rabatterade priser och hantera allt detta i stor skala.
- **Assets** - Artefakter som är kopplade till produkter, till exempel bilder, videoklipp, PDF-filer eller andra filtyper (framtida färdplan).

### Kontexthantering

Hantering av produktsammanhang omfattar följande aspekter:

- **Kanal** - Distributionskanalen definierar sökvägen som ett företag vill sälja produkter via. En kanal är en abstraktion på högsta nivå som kapslar in språkområden och principer.
   - Exempel: Återförsäljare för bilindustrin. Dotterföretag till konglomerat med flera varumärken. Tillverkningsplats för leverantörer.
- **Princip** - Dataåtkomstfilter som gör att du kan leverera rätt innehåll till rätt mål. Detta koncept möjliggör katalogsyndikering.
   - Exempel: fysiska butiker, marknadsplatser, reklamrörledningar (Google, Facebook, Instagram)
- **Scope** - Representerar språket (nationella inställningar) för kataloger, till exempel `en-US`. Omfånget anges på en SKU-nivå under inmatning av katalogdata.

Vid inmatning och uppdatering av produktdata innehåller en SKU detaljer om omfång och attribut (attributen mappar till kanaler och principer). Dessa definierar de produktkontextidentifierare som en SKU tillhör:

![[!DNL Composable Catalog Data Model] produktkontextidentifierare](assets/ccdm-product-id.png)

I bilden ovan ger varje SKU:

- &#x200B; för scopeidentifierare
   - Språk: Obligatorisk &#x200B;
- Produktattribut
   - Produktattribut används för att mappa till relevanta kanaler och policyer &#x200B;
   - Exempel: Som biltillverkare kan du välja att skapa en kombination av kanaler och policy för produktattribut: (1) Återförsäljare (2) Bilvarumärken. &#x200B;
- Priser och tilldelade prislistor
   - Varje SKU kan ha flera priser definierade med hjälp av flera prisböcker.
   - Exempel: Du erbjuder medarbetarna ett reducerat normalpris på bildelar med en extra rabatt på 25 %. Du erbjuder VIP-kunder ett högre ordinarie pris med en rabatt på 10 %. Produktens SKU-prisinformation säkerställer att rätt pris visas för varje kundsegment.

Kanal- och principdefinitionerna skapas med dedikerade API:er:

![[!DNL Composable Catalog Data Model] Kanal-, princip- och omfattningsmappning](assets/ccdm-scope-map.png)

- **Scope** (locale) - Ange på en SKU-nivå under inmatning av produktdata. &#x200B;
- **Kanal** - Definitionen har skapats med dedikerade API:er. &#x200B;
- **Princip** - Definitionen har skapats med dedikerade API:er.

## Viktiga funktioner

| Viktiga funktioner | Fördelar |
|---|---|
| **Direktinmatning av katalogdata i butikstjänstens pipeline**: Infoga dina katalogdata direkt i katalogtjänstens pipeline för butikens bläddring och söklivscykel (produktvisningssida, produktlistsida, sökresultatsida osv.) | <ul><li>Direktinmatning av katalogdata i butikstjänstens pipeline som driver: Katalogtjänst, Produktsökning (Live Search) och Produktrekommendationer. Med detta kan du leverera kataloguppdateringar i stor skala för miljontals SKU:er. Detta frigör tidskänslig hantering av kampanjer i stor skala. </li></ul> |
| **Nya katalogproduktomfång**: Kanal, princip och omfång är nya produktomfång som introducerats av CCDM. Dessa produktomfång ersätter webbplatsens, butikens och butikernas omfång i butikstjänstskiktet. [Läs mer](#product-context-management). | <ul><li>Med de nya omfången kan CCDM enkelt skala upp till flera platser, flera affärsenheter, flera varumärken och flerspråkiga användningsområden med hjälp av en enda baskatalog.</li><li>Eliminera dataredundans i kataloghanteringen.</li></ul> |
| **Skala till tiotals miljoner SKU:er** | Lås upp kataloghantering i stor skala. Här kan du enkelt importera och hantera över 200 MM SKU:er. |
| **Stöd för produkttyper** | <ul><li>Enkel, konfigurerbar</li><li>Paket och paket med paket (framtida färdplan)</li><li>Prenumerationer och planer (framtida färdplan)</li></ul> |
| **Headless commerce** | <ul><li>Fullt stöd för headless commerce-implementeringar via API:er för katalogtjänster, produktsökning (Live Search) och produktrekommendationer.</li></ul> |
| **Moderna blixtsnabba gränssnittskomponenter** | <ul><li>Komponentstöd för användargränssnitt som ingår i produktsökningar och produktrekommendationer finns inte i paketet.</li><li>UI-komponenterna är utökningsbara och flexibla så att de kan användas både av Adobe Edge Delivery Service och andra butiksimplementationer.</li></ul> |

## Vilken typ av handlare drar störst nytta av CCDM?

I följande tabell beskrivs de vanligaste utmaningarna som handlare möter och hur CCDM löser dem.

| Marknadsföringstyp | Använd skiftläge | Lösta problem |
|---|---|---|
| Konglomerat med flera varumärken | <ul><li>De säljer flera varumärken</li><li>De säljer i flera länder</li><li>De säljer på olika språk</li></ul> | Använd en enda enhetlig katalog och uppnå operativ effektivitet samtidigt som ni expanderar till flera varumärken, geografiska platser och språk. |
| Konglomerat mellan bil- och tillverkningsdelar | <ul><li>Säljer auto- eller maskindelar. Produkterna är desamma för alla kunder.</li><li>Olika återförsäljare säljer delar till kunder</li><li>Varje återförsäljare har sina egna priser, lager och leveransmetoder</li></ul> | För att få olika leveransintegreringar bör varje återförsäljare ha en separat webbplats. Men separata webbplatser tvingar den typiska katalogdatamodellen att duplicera data. Om det finns 3000 handlare i USA skapar en handlare 3000 katalogkopior trots att samma katalog används av alla återförsäljare. Den här datadupliceringen stör prestandagränserna. CCDM eliminerar dataduplicering. |
| Paketerings-/logistikföretag | <ul><li>De har flera leveransställen</li><li>De har olika pris för varje kund</li><li>Samma produkt som finns på två platser för två kunder har fyra möjliga priser</li></ul> | Trots att kundgrupper används för att täcka priser per kund har den typiska katalogdatamodellen inte möjlighet att hantera pris per plats. Dessutom vill handlarna ha unika synlighetsregler per plats/webbplats. Hanteringen av sådana komplexa pris- och synlighetsregler kan låsas upp i stor skala med CCDM. |

### Vart ska du gå härifrån?

- Infoga data i CCDM med [API:t för datainhämtning](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Hantera din katalog och definiera kanaler, principer och omfattningar med [API:t för kataloghantering](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Slutför en självstudie](https://developer-stage.adobe.com/commerce/services/composable-catalog/ccdm-use-case/) som visar hur ett företag med en enda baskatalog kan använda CCDM-API:er för att lägga till produktdata, definiera kataloger med projektioner och hämta katalogdata för visning i en headless store.
