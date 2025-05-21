---
title: Vad är  [!DNL Live Search]?
description: '[!DNL Live Search] från Adobe Commerce ger en snabb, relevant och användarvänlig sökupplevelse.'
recommendations: noCatalog
exl-id: 15399216-6a96-4d0b-bbc1-293190cb9e14
source-git-commit: 29374c45f57e923666e255bfefadd9a1e736cfef
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---

# Vad är [!DNL Live Search]?

[!DNL Live Search] är en funktion som ersätter standardsökfunktionerna i Adobe Commerce. Funktionen [!DNL Live Search] installeras med Composer och din [!DNL Commerce]-butik ansluts till [Commerce Services Connector](../landing/saas.md). När det är konfigurerat ersätts standardtextfältet för sökning med textfältet [!DNL Live Search]. [!DNL Live Search] installerar också PLP-widgeten (Product Listing Page), som tillhandahåller robusta filtreringsfunktioner när du bläddrar bland sökresultaten.

Med [!DNL Live Search] kan du:

- Skapa meningsfulla sökupplevelser som hjälper kunder och köpare att hitta det de vill ha med så lite ansträngning som möjligt.
- Utnyttja den AI-baserade dynamiska Faceeting-funktionen och omrankningen av sökresultaten som svar på beteenden hos besökare.
- Använd en lättviktig SaaS-baserad tjänst som enkelt uppdaterar och ingår i licensen, vilket minskar den totala ägandekostnaden.
- Få teknisk hjälp genom att aktivera GraphQL API, headless flexibility, API sandbox-miljöer och extremt snabba SaaS.

>[!IMPORTANT]
>
>När det gäller webbplatssökningar har Adobe Commerce fler alternativ. Granska informationen [Gränser och gränser](boundaries-limits.md) innan du implementerar den för att se till att [!DNL Live Search] passar ditt företags behov.

## Arkitektur

På Adobe Commerce-sidan av arkitekturen finns värdtjänster för sökningen *Admin*, synkronisering av katalogdata och körning av frågetjänsten. När [!DNL Live Search] har installerats och konfigurerats börjar Adobe Commerce dela söknings- och katalogdata med SaaS-tjänster. Nu kan administratörsanvändare konfigurera, anpassa och hantera sökregler för [facets](facets.md), [synonymer](synonyms.md) och [försäljningsregler](category-merch.md).

![Dataflöde för Live-sökning](assets/ls-cs-data-flow.png)

## Snabbdemo

Med fokus på hastighet, relevans och användarvänlighet är [!DNL Live Search] en spelförändrare för både kunder och handlare. Titta på följande video och ta sedan en snabb genomgång av [!DNL Live Search] från butiken.

>[!VIDEO](https://video.tv.adobe.com/v/3418797?learn=on)

En mer ingående video om hur du använder och konfigurerar Live Search finns i avsnittet [Fullständig demonstration om  [!DNL Live Search]](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/getting-started/capabilities/live-search-full-demonstration).

### Sök medan du skriver

[!DNL Live Search] svarar med föreslagna produkter och en miniatyrbild av de bästa sökresultaten i en [pover](storefront-popover.md) som typfrågor för kunder i rutan [Sök](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search). Sidan [produktinformation](https://experienceleague.adobe.com/sv/docs/commerce-admin/start/storefront/storefront) visas när kunderna klickar på en föreslagen eller aktuell produkt. Sökresultatsidan visas om du har en _Visa alla_-länk i popoverns sidfot.

[!DNL Live Search] returnerar sökresultatet när du skriver för en fråga med två eller flera tecken. För en partiell matchning är det maximala antalet tecken per ord 20. Det går inte att konfigurera antalet tecken i frågan. Leveransen innehåller fälten `name`, `sku` och `category_ids`.

![Exempelarkiv - sök medan du skriver](assets/storefront-search-as-you-type.png)

### Visa alla sökresultat

Om du vill visa alla produkter som returneras av frågan&quot;Sök när du skriver&quot; klickar du på _Visa alla_ i avsändarens sidfot.

![Exempelbutiker - prisfakturor](assets/storefront-view-all-search-results.png)

### Så här hanterar [!DNL Live Search] typografi

När en sökning görs kör [!DNL Live Search] en icke-otydlig sökning som inte tar hänsyn till några stavfel. Om inga resultat hittas utför [!DNL Live Search] en andra otydlig sökning, som tar hänsyn till mindre typografi. Den oskarpa sökningen utförs med ett maximalt redigeringsavstånd på 1. Det här redigeringsavståndet använder konceptet [Levenshöjdavstånd](https://en.wikipedia.org/wiki/Levenshtein_distance) och det tillåter tre typer av åtgärder:

| Åtgärd | Beskrivning | Exempel |
|---|---|---|
| Infoga | Lägga till ett tecken. | &quot;cat&quot; -> &quot;cart&quot; |
| Borttagning | Tar bort ett tecken. | &quot;cart&quot; -> &quot;cat&quot; |
| Ersättning | Ersätta ett tecken med ett annat. | &quot;cart&quot; -> &quot;cast&quot; |

Förutom den suddiga söklogiken räknas också transpositioner, det vill säga där två intilliggande tecken i ett ord byts ut, till exempel&quot;the&quot; i stället för&quot;the&quot;. Observera att dessa redigeringsgränser är per ord och inte frasen som helhet.

### Filtrerad sökning med fack

Filtrerad sökning använder flera dimensioner av attributvärden, eller [facets](facets.md), som sökvillkor. Urvalet av filter definieras av handlaren och ändras beroende på vilka produkter som returneras, med de mest använda ansiktena fästa överst i listan.

Använd ansikten som URL-parametrar:`http://yourwebsite.com?color=red`, och resultat från direktsökningsfilter baserade på dessa attributvärden.

### Synonymer

[Synonymer](synonyms.md) vidgar räckvidden och skärper fokus på frågor genom att inkludera ord som kunderna kan använda som skiljer sig från dem i katalogen. Du kan finjustera synonymordboken för att hålla kunderna engagerade och på köpvägen.

### Marknadsföringsregler

Marknadsföring av [regler](rules.md) formar shoppingupplevelsen med if-then-satser som lägger till logik och händelser som ska sökas. Du kan enkelt beskära eller begrava produkter för en kampanj, säsong eller annan tidsperiod.

### Stöd för söktermer

[!DNL Live Search] stöder Commerce [omdirigering av söktermer](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search-terms). Användarna kan t.ex. söka efter en term som &quot;Fraktsatser&quot; och direkt till sidan Leveransavgifter.

## Live Search-komponenter

- [!DNL Live Search] [popoverwidget](storefront-popover.md) är den ruta som öppnas under sökfältet som innehåller sökresultaten.
- [Widgeten Produktlistsida](plp-styling.md) (PLP) innehåller en sökbar produktlistsida med funktioner för ansikten och synonymer. Widgeten installeras och aktiveras i Live Search 4.0.0+ och ersätter sökadaptern.
- (**Borttagen**) Sökadaptern är föregångaren till PLP-widgeten och har installerats med Live Search &lt; 4.0.0. Om du använder en tidigare version av Live Search än 4.0.0 rekommenderar Commerce att du uppgraderar för att få fördelarna med PLP-widgetfunktionerna och framtida förbättringar. Framöver kommer sökadaptern endast att uppdateras för att åtgärda säkerhetsproblem.

## Arbetsytan [!DNL Live Search]

[!DNL Live Search] [arbetsytan](workspace.md) är det område i Admin där du konfigurerar [!DNL Live Search]-funktioner som synonymer, facets och Category Merchandising.

## Händelser

[!DNL Live Search] använder [events](events.md) för att beräkna kontrollpanelerna [Intelligent Merchandising](category-merch.md) och [performance](performance.md). Händelser tillhandahålls med standardimplementeringar. Händelser för headless-butiker ska aktiveras manuellt.

## Lagringspolicy för katalogdata

Om du inte skickar en sökfråga för katalogdata i testmiljön under 90 dagar i följd, ställs katalogdata in på viloläge och inga data returneras för sökfrågor. Katalogdata i produktionsmiljön påverkas inte av den här principen.

Om du vill återaktivera katalogdata i din testmiljö skickar [du en supportförfrågan](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) med titeln:&quot;Återaktivera [!DNL Live Search]&quot; och inkluderar miljö-ID:n. Katalogdata i testmiljön bör återställas inom några timmar.
