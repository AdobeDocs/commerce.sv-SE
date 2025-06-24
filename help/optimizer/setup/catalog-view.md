---
title: Katalogvy
description: Lär dig hur du skapar och hanterar katalogvyer i  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 0%

---

# Skapa katalogvy

[Katalogvyer](#catalog-views) hjälper dig att definiera din detaljhandelsstruktur i meningsfulla affärsgrupper. En katalogvy påverkar produktsynligheten genom att tillämpa specifika profiler och filter som avgör vilka produkter som visas i en butik. Dessa policyer kan innehålla attribut som märke, modell eller delkategori, vilket säkerställer att endast relevanta produkter är synliga för kunderna baserat på katalogvykonfigurationen. Dessutom kan man i katalogvyer använda prisböcker för att visa kundspecifika priser och ytterligare anpassa shoppingupplevelsen. [Läs mer](#catalog-views) om katalogvyer.

I det här avsnittet skapar du en katalogvy, väljer en [policy](policies.md) och en [prisbok](pricebooks.md).

1. Gå till _Store setup_ på den vänstra menyn och klicka på **[!UICONTROL Catalog views]**.

1. Klicka på **[!UICONTROL Create catalog view]**. &#x200B;

1. Lägg till information om katalogvyn:

   - **Namn** - Ange namnet på katalogvyn. Exempel: &quot;Celport&quot;. &#x200B;
   - **Katalogkällor** - Lägg till katalogkällan (nationella inställningar). Exempel: &quot;en-US&quot;. Tryck på tangenten **enter**.
   - **Profiler** - Använd listrutan för att välja relevanta profiler. Exempel: &quot;Varumärke&quot;, &quot;Modell&quot;. &#x200B;Kontrollera att du redan [har skapat en princip](policies.md).

1. Välj den prisbok som du vill länka till katalogvyn. Läs mer om [prisböcker](pricebooks.md).

1. Klicka på **[!UICONTROL Add]** om du vill skapa katalogvyn med den länkade prisboken och de länkade profilerna.

   Om knappen **[!UICONTROL Add]** inte är aktiv kontrollerar du att katalogkällan har lagts till korrekt genom att placera markören i fältet Katalogkällor och trycka på **enter**. &#x200B;

Sidan Katalog visar uppdateringar för att visa den nya katalogvyn. &#x200B;

När du har utfört de här stegen konfigureras den nya katalogvyn så att den visar produkter och priser baserat på de katalogkällor och principer du har valt.

## Katalogvyer

En produktkatalog är väsentlig för shoppingupplevelser online, så att kunderna kan bläddra, söka och göra inköp. För en effektiv drift bör en produktkatalog nära återspegla företagets affärsstruktur. Företag behöver ofta sälja produkter till olika priser baserat på geografisk marknad, distributionskatalogvy, kundsegment och andra variabler. För att tillgodose detta måste en e-handelsplattform erbjuda en flexibel katalogdatamodell som gör det möjligt för företag att producera variationer av sin katalog som är anpassade till dessa scenarier. Adobe tillgodoser dessa behov genom att erbjuda Merchandising Services som bygger på katalogvyer och katalogpolicyer. Merchandising Services tillhandahåller byggstenar som handlare kan använda för att skapa och hantera kataloger i stor skala. På så sätt kan företag konfigurera kataloger som är anpassade till deras affärsstruktur och go-to-market-strategier.

På en hög nivå kan ni med Merchandising Services:

- Använd en enda baskatalog för alla era affärsbehov. Skala upp katalogen snabbt mellan nya varumärken, marknader, affärsenheter, kataloger och kundsegment utan behov av en fullständig omarkitektur. På så sätt slipper man datadubbletter och skapar en e-handelsplattform som ger hög effektivitet.
- Lås upp katalogsyndikering och leverera rätt innehåll genom att designa din produktkatalog så att den återspeglar din verksamhet, inklusive produkter, kunder, priser och distribution.
- Importera och uppdatera katalogdata snabbt och leverera snabbt uppdateringar till butiken för era kampanjer och kampanjbehov.
- Få perfekta fyrar med färdiga, blixtsnabba användargränssnittskomponenter som bygger på Edge Delivery Services för smidig bläddring och rekommendationer.
- Använd en modern sammansättningsbar arkitektur med hjälp av Adobe utbyggbarhetsarkitektur ([App Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development)) för att importera produktdata och driva headless-butiker med Adobe [API Mesh](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh).

>[!INFO]
>
>Om du vill veta mer om API:erna som är tillgängliga i Merchandising Services som drivs av katalogvyer och -profiler kan du läsa [utvecklardokumentationen](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Arkitektur

Marknadsföringstjänster som bygger på katalogvyer och -profiler är en mycket skalbar, flexibel katalogdatamodell som enkelt kan låsa upp flervarumärkes-, affärsenhets- och flerspråkiga användningsfall. Den här modellen ersätter användningen av de klassiska Adobe Commerce-katalogkällorna (webbplats, butik, butiksgranskning) med nya källor i produktkatalogen Merchandising Services (katalogvy, policy och språkinställning).

Bilden nedan visar en helhetsbild av ramverket för marknadsföring.

![[!DNL Merchandising Services]-arkitektur](../assets/merchandising-svcs-architecture.png)

Högst upp i det här diagrammet hämtas katalogdata (PIM, ERP o.s.v.) in i ramverket för marknadsföringstjänster. Katalogdata innehåller SKU:er. Varje SKU innehåller information om katalogkällan (språkområde) och produktattribut, som mappas till de nya källorna i produktkatalogen Merchandising Services (katalogvyer, principer och språkområde).

När alla dessa data är insamlade i marknadsföringsramverket blir resultatet en ny enhetlig baskatalog som är tillgänglig i dataredjan för katalogtjänsten. I nästa del av diagrammet visas flera katalogvyer. Varje katalogvy representerar en affärsenhet. Exempel: *Texas Retail*, *Texas retail säsononal* osv. Som du ser i diagrammet kan alla språkområden, principer och prisböcker delas mellan olika katalogvyer. &#x200B;

Slutligen visar diagrammet hur distinkta katalogdata kan visas på olika platser, t.ex. en Edge Delivery Services-butik, en marknadsplats, en annonskatalogvy, en anpassad mikrobutik o.s.v.

Mer information om hur du kan importera katalogdata till Merchandising med hjälp av API:t för att hämta katalogdata och hur du konfigurerar dina språkområden, principer och prisböcker med hjälp av API:t för kataloghantering och regler finns i [utvecklardokumentationen](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Mer information om de begrepp som utgör Merchandising Services finns i följande avsnitt.

## Hantering av produktkataloger

Produktkataloghantering omfattar två skilda aspekter: produktdata och produktsammanhang. Merchandising Services respekterar separationen av dessa skyldigheter och erbjuder oberoende ledning för var och en.

- **Produktdata** - Vilken produkt säljs och till vilket pris?
- **Produktkontext** - Vem säljer till vem och var?

![[!DNL Merchandising Services] aspekter ](../assets/merchandising-svcs-parts.png)

### Produktdata

Produktdata innehåller följande typer:

- **Produkter** - Individuella SKU:er eller samlingar av SKU:er som representerar fysiska varor eller immateriella tjänster med attribut som representerar produkten, inklusive beskrivning, vikt, storlek, dimensioner med mera. Attribut anger även katalogvyn och principkatalogkällor för en SKU. Produkterna kan grupperas i olika produkttyper, t.ex. enkla, konfigurerbara produkter, paket, paket med paket, prenumerationer med mera.
- **Metadata** - Produktattributmetadata definierar och hanterar hur produktattribut visas på butiken i produktlistor, detaljsidor, sökresultat och så vidare. Metadata definierar också hur produktattribut används i sökningar - sortering, filtrering, sökvikter och så vidare.
- **Prisböcker och priser** - Bestämmer försäljningspriserna för produkter. I Merchandising Services är en produkt-SKU och ett pris fristående, vilket innebär att du kan definiera flera prislistor för en enda SKU. Genom att koppla loss priserna från SKU:n kan ni låsa upp specifika priser för olika kundnivåer, affärsenheter och geografiska platser. Du kan definiera vanliga och rabatterade priser och hantera allt detta i stor skala.
- **Assets** - Artefakter som är kopplade till produkter, till exempel bilder, videoklipp, PDF-filer eller andra filtyper (framtida färdplan).

### Kontexthantering

Hantering av produktsammanhang omfattar följande aspekter:

- **katalogvy** - Distributionskatalogvyn definierar sökvägen som ett företag vill sälja produkter via. En katalogvy är den abstraktion på den högsta nivån som kapslar in språkområden och principer.
   - Exempel: Återförsäljare för bilindustrin. Dotterföretag till konglomerat med flera varumärken. Tillverkningsplats för leverantörer.
- **Princip** - Dataåtkomstfilter som gör att du kan leverera rätt innehåll till rätt mål. Detta koncept möjliggör katalogsyndikering.
   - Exempel: fysiska butiker, marknadsplatser, reklamrörledningar (Google, Facebook, Instagram)
- **katalogkälla** - Representerar språket (nationella inställningar) för kataloger, till exempel `en-US`. Katalogkällan anges på SKU-nivå när katalogdata hämtas.

Vid inmatning och uppdatering av produktdata innehåller en SKU information om katalogkällor och -attribut (attributen mappar till katalogvyer och -profiler). Dessa definierar de produktkontextidentifierare som en SKU tillhör:

![[!DNL Merchandising Services] produktkontextidentifierare](../assets/merchandising-svcs-product-id.png)

I bilden ovan ger varje SKU:

- &#x200B; för katalogkällidentifierare
   - Språk: Obligatorisk &#x200B;
- Produktattribut
   - Produktattribut används för att mappa till relevanta katalogvyer och policyer &#x200B;
   - Exempel: Som biltillverkare kan du välja att skapa en katalogvy och en policykombination för produktattribut: (1) Återförsäljare (2) Bilvarumärken. &#x200B;
- Priser och tilldelade prislistor
   - Varje SKU kan ha flera priser definierade med hjälp av flera prisböcker.
   - Exempel: Du erbjuder medarbetarna ett reducerat normalpris på bildelar med en extra rabatt på 25 %. Du erbjuder VIP-kunder ett högre ordinarie pris med en rabatt på 10 %. Produktens SKU-prisinformation säkerställer att rätt pris visas för varje kundsegment.

Katalogvyn och principdefinitionerna skapas med dedikerade API:er:

Mappning av katalogvy, princip och katalogkälla för ![[!DNL Merchandising Services]](../assets/merchandising-svcs-scope-map.png)

- **katalogkälla** (språkinställning) - Ange på en SKU-nivå under inmatning av produktdata. &#x200B;
- **katalogvy** - Definitionen har skapats med dedikerade API:er. &#x200B;
- **Princip** - Definitionen har skapats med dedikerade API:er.

## Viktiga funktioner

| Viktiga funktioner | Fördelar |
|---|---|
| **Direktinmatning av katalogdata i butikstjänstens pipeline**: Infoga dina katalogdata direkt i katalogtjänstens pipeline för butikens bläddring och söklivscykel (produktvisningssida, produktlistsida, sökresultatsida osv.) | <ul><li>Direktinmatning av katalogdata i butikstjänstens pipeline som driver: Katalogtjänst, Produktidentifiering och rekommendationer. Med detta kan du leverera kataloguppdateringar i stor skala för miljontals SKU:er. Detta frigör tidskänslig hantering av kampanjer i stor skala. </li></ul> |
| **Nya katalogproduktkatalogkällor**: katalogvy, princip och katalogkälla är nya produktkatalogkällor som introducerades av Merchandising Services. De här produktkatalogskällorna ersätter katalogkällorna för webbplatser, butiker och butiker i butikstjänstskiktet. [Läs mer](#product-context-management). | <ul><li>Med de nya katalogkällorna ger Merchandising Services möjlighet att enkelt skala upp till flergeografi, enheter för flera företag samt flerspråkiga och flerspråkiga användningsområden med en enda baskatalog.</li><li>Eliminera dataredundans i kataloghanteringen.</li></ul> |
| **Skala till tiotals miljoner SKU:er** | Lås upp kataloghantering i stor skala. Här kan du enkelt importera och hantera över 200 MM SKU:er. |
| **Stöd för produkttyper** | <ul><li>Enkel, konfigurerbar</li><li>Paket och paket med paket (framtida färdplan)</li><li>Prenumerationer och planer (framtida färdplan)</li></ul> |
| **Headless commerce** | <ul><li>Fullt stöd för headless commerce-implementeringar via Catalog Service, Product Discovery och Recommendations API:er.</li></ul> |
| **Moderna blixtsnabba gränssnittskomponenter** | <ul><li>Komponentstöd för användargränssnitt för produktsökning och rekommendationer ingår inte i paketet.</li><li>UI-komponenterna är utökningsbara och flexibla så att de kan användas både av Adobe Edge Delivery Service och andra butiksimplementationer.</li></ul> |

## Vilken typ av handlare drar störst nytta av Merchandising Services?

I följande tabell beskrivs de vanligaste utmaningarna som handlare möter och hur marknadsföringstjänster som drivs av katalogvyer och -profiler hanterar dem.

| Marknadsföringstyp | Använd skiftläge | Lösta problem |
|---|---|---|
| Konglomerat med flera varumärken | <ul><li>De säljer flera varumärken</li><li>De säljer i flera länder</li><li>De säljer på olika språk</li></ul> | Använd en enda enhetlig katalog och uppnå operativ effektivitet samtidigt som ni expanderar till flera varumärken, geografiska platser och språk. |
| Konglomerat mellan bil- och tillverkningsdelar | <ul><li>Säljer auto- eller maskindelar. Produkterna är desamma för alla kunder.</li><li>Olika återförsäljare säljer delar till kunder</li><li>Varje återförsäljare har sina egna priser, lager och leveransmetoder</li></ul> | För att få olika leveransintegreringar bör varje återförsäljare ha en separat webbplats. Men separata webbplatser tvingar den typiska katalogdatamodellen att duplicera data. Om det finns 3000 handlare i USA skapar en handlare 3000 katalogkopior trots att samma katalog används av alla återförsäljare. Den här datadupliceringen stör prestandagränserna. Merchandising Services eliminerar datatypsbyte. |
| Paketerings-/logistikföretag | <ul><li>De har flera leveransställen</li><li>De har olika pris för varje kund</li><li>Samma produkt som finns på två platser för två kunder har fyra möjliga priser</li></ul> | Trots att kundgrupper används för att täcka priser per kund har den typiska katalogdatamodellen inte möjlighet att hantera pris per plats. Dessutom vill handlarna ha unika synlighetsregler per plats/webbplats. Hanteringen av sådana komplexa pris- och synlighetsregler kan låsas upp i stor skala med Merchandising Services. |
