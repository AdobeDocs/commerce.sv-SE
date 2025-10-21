---
title: '[!DNL Live Search] metodtips'
description: Lär dig de bästa sätten att implementera [!DNL Live Search] i din butik.
role: Admin, Developer
exl-id: f7700339-fb13-42fe-a249-17cd4ba36e1b
source-git-commit: 4ba9734946f551784cd429ffa7cb23358f0f9710
workflow-type: tm+mt
source-wordcount: '2429'
ht-degree: 0%

---

# Bästa praxis

Den här artikeln hjälper handlare att förbättra sökfunktionen på webbplatser och skapa en smidig och effektiv shoppingupplevelse som maximerar konverteringsgraden. Genom att följa de beskrivna strategierna får du lära dig att implementera avancerade sökfunktioner och kontinuerligt förfina sökverktyget för optimala prestanda med Adobe Commerce [!DNL Live Search].

Det finns flera viktiga faktorer som avgör sökresultatens relevans och effektivitet:

- Välstrukturerade produktdata säkerställer att sökalgoritmer effektivt kan matcha produkter mot frågor. Produktdata av låg kvalitet leder till låga relevanta sökresultat. Så här påverkar du er marknadsföringsstrategi direkt:
   - Ställ in rätt attribut som sökbara med motsvarande vikt.
   - Se till att data i dessa attribut är relevanta.
- En väldesignad sökupplevelse skapar förtroende hos kunderna och ser till att de hittar det de behöver.
- Sökreglerna är avgörande eftersom de kan öka synligheten för vissa produkter baserat på popularitet, nya kunder, kampanjkriterier eller andra marknadsföringsstrategier för att uppfylla era affärskrav.
- Med enkel navigering kan kunderna förfina sina sökningar och få relevanta resultat snabbt.

Om du vill hantera [!DNL Live Search] går du till **Marknadsföring** > *SEO &amp; Search* > **[!DNL Live Search]** i Adobe [!DNL Commerce] Admin. 

## Optimera sökfunktionerna

I det här avsnittet får du lära dig att optimera sökfunktionen genom att använda funktioner som Autocomplete för att ge realtidsförslag som kundtyp, synonymer och stavningar för att se till att kunderna hittar produkter även om de använder olika ord, facets för att begränsa sökresultaten och sökomdirigeringar för att automatiskt dirigera om kunderna från en sökfråga till en viss sida.

### Komplettera automatiskt

Komplettera automatiskt, som också kallas typförslag eller autoförslag, är en interaktiv sökfunktion som dynamiskt visar förslag till kunder när de skriver sina söktermer. Detta hjälper kunderna att snabbt och enkelt hitta produkter genom att erbjuda realtidsförslag baserat på deras indata.

Widgeten [!DNL Live Search] [[!DNL popover]](storefront-popover.md) aktiverar alternativ för automatisk komplettering av sökningar för att föreslå populära produkter. För varje tecken som skrivs av kunden uppdateras poveringen med förslag på produkter och miniatyrbilder av de bästa sökresultaten.

[!DNL Live Search] börjar returnera resultat när användaren har skrivit in två tecken. För en partiell matchning är det maximala antalet tecken per ord 20. Det går inte att konfigurera antalet tecken i en sökfråga.

Läs mer om widgeten [pover](storefront-popover.md).

### Synonymer och felstavningar

Live Search hanterar felstavningar som standard. Du kan konfigurera synonymer så att de innehåller ord som kunderna kan använda som skiljer sig från de ord som anges i din katalog. Du vill inte förlora någon affär eftersom någon letar efter en &quot;soffa&quot;, medan din produkt listas som en &quot;soffa&quot;. Du kan fånga ett stort antal söktermer genom att ange alla möjliga ord som kunderna kan använda för att hitta dina produkter. Du kan [ange synonymer som ett eller två sätt](synonyms-add.md#step-2-define-the-synonym-by-type) för att förbättra resultatet.

#### Tips för att optimera synonymer

- Mappa märkesnamn och förkortningar till deras fullständiga namn, till exempel&quot;HP&quot; till&quot;Hewlett-Packard&quot; och vanliga smeknamn för produkter, till exempel&quot;iPhone&quot; till&quot;Apple iPhone&quot;.
- Inkludera branschspecifik jargon och termer som kunderna kan använda som synonymer, till exempel&quot;smygskor&quot; och&quot;skor för löpning&quot;.
- Uppdatera synonymlistan regelbundet baserat på nya söktrender, produkttillägg och kundbeteende.
- Testa effekten av synonymmappningar genom att analysera sökresultat och feedback från kunderna. Förfina mappningarna för att förbättra noggrannheten och relevansen.

Läs mer om synonymer:

- [Typer av synonymer](synonyms-type.md)
- [Skapa synonymer](synonyms-add.md)
- [Hantera synonymer](synonyms-manage.md)
- [Språkstöd](settings.md#language)

### Fasetter

Filter- och ansiktsfunktioner är en viktig komponent på din [!DNL Commerce]-webbplats, som är utformad för att förbättra shoppingupplevelsen genom att låta kunderna begränsa sökresultaten och hitta produkterna effektivare. Den här funktionen hjälper kunderna att sortera genom enorma kataloger med artiklar genom att tillämpa specifika kriterier, vilket gör köpprocessen snabbare, enklare och mer tillfredsställande. Genom att implementera effektiva, kundvänliga filter och ansikten kan ni hjälpa kunderna att snabbt och effektivt hitta exakt det de behöver, vilket i slutänden ökar kundnöjdheten och konverteringsgraden.

Om du vill ställa in ett produktattribut som en aspekt måste den ha följande [egenskaper angivna](facets-add.md#step-1-add-a-facet):

- **[!UICONTROL Use in Search]** -  `No`
- **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
- **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

#### Tips för att optimera ansikten

- Identifiera de mest relevanta och användbara attributen för dina produkter, till exempel titel, kategori, varumärke, prisintervall, färg och storlek, och ange dem som [dynamiska aspekter](facets-type.md). 
- Ange och sortera produktattribut som är enhetliga i hela katalogen och mycket relevanta för produkterna för att förbättra relevansen och filtreringsmöjligheterna för era kunder.
- Se till att det är enkelt att förstå och namnge fasettetiketter på hela webbplatsen. Använd till exempel&quot;Prisintervall&quot; i stället för&quot;Kostnad&quot;.
- Undvik överväldigande kunder genom att begränsa antalet aspekter till de viktigaste. Alltför många alternativ kan orsaka besluttrötthet. Som standard är [!DNL Live Search] begränsad till högst 100 attribut konfigurerade som facets och 30 bucket returnerade inom varje facet. Läs mer om [ansiktsbegränsningar](boundaries-limits.md#facets). 
- Låt kunderna välja flera filtervillkor samtidigt för att förfina resultatet. Om du till exempel låter kunderna välja både&quot;röd&quot; och&quot;blå&quot; färg.
- Visa antalet tillgängliga produkter bredvid varje facettalternativ för att ge kunderna en uppfattning om de sökresultat de kan förvänta sig.
- Implementera komprimerbara ansiktssektioner för att hålla gränssnittet rent och hanterbart, särskilt på mobila enheter.
- Låt kunderna enkelt återställa enskilda aspekter eller alla valda filter för att starta en ny sökning.

Läs mer om ansikten:

- [Typer av ansikten](facets-type.md)
- [Lägg till ansikten](facets-add.md)
- [Hantera ansikten](facets-manage.md) (redigera, fästa en fasett, ta bort, publicera)
- [Prisfakturor](settings.md#price-faceting)

### Sökomdirigeringar

Med omdirigering av sökningar kan du automatiskt dirigera om kunder från en sökfråga till en viss sida. Sökomdirigeringar kan förbättra kundupplevelsen och vägleda kunderna till det mest relevanta innehållet, till exempel en produktsida, kategori, landningssida eller en skräddarsydd uppsättning sökresultat. Sökomdirigeringar effektiviserar shoppingupplevelsen och ser till att kunderna hittar det de söker snabbt och effektivt.

Rekommenderade användningsexempel för att konfigurera sökomdirigeringar:

- **Populära produkter eller kategorier** - Omdirigera kunder till en specifik produktsida eller produktkategori när de söker efter vanliga eller populära termer. Om du till exempel söker efter&quot;iPhone&quot; kan du omdirigera till iPhone kategorisida eller en viss modellsida.

- **Kampanjkampanjer** - Omdirigera relevanta söktermer till landningssidor där specialerbjudanden eller aktuella produkter markeras under kampanjevent eller försäljning.

- **Varumärkessökningar** - När kunderna söker efter ett varumärke kan du dirigera om dem till varumärkets dedikerade sida där alla produkter från det varumärket listas.

- **Produktavbrott** - Om en produkt avbryts kan du omdirigera sökningar efter den produkten till liknande produkter eller den nya versionen av produkten.

Testa alltid sökomdirigeringar för att kontrollera att de fungerar som de ska och leder till de mest relevanta sidorna. Övervaka kontinuerligt deras prestanda och gör justeringar efter behov.

Lär dig hur du [hanterar sökomdirigeringar](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms).

## Förbättra relevansen i sökresultatet

I det här avsnittet beskrivs hur du förbättrar sökresultatens relevans genom att implementera effektiva sökregler och använda produktmetadata för att säkerställa att korrekta och detaljerade attribut är sökbara.

### Bilder

Se till att de underordnade produkterna för konfigurerbara produkter har bilder med rätt roller. Om du har överordnade eller underordnade produkter kan det leda till att sökresultatet inte innehåller bilder.

>[!NOTE]
>
>Bilderna i sökresultaten kan vara olika beroende på söktermen. Om söktermen anger att en underordnad produkt är mer relevant kommer bilder från den underordnade produkten att användas i stället för bilder från den överordnade produkten.

### Sökregler

För att optimera konverteringsgraden och intäkterna måste ni implementera effektiva sökregler. Justera produktrankningar baserat på försäljningsdata, aktienivåer och kampanjer med [Search Merchandising](rules.md).

Det är viktigt att fastställa en genomtänkt standardregel för sökning. Din [standardregel](rules.md#default-rule) avgör hur sökresultaten sorteras och visas för kunderna, vilket förbättrar deras övergripande upplevelse och ökar sannolikheten för inköp. Regelbunden övervakning och anpassning av denna regel säkerställer att den även i fortsättningen uppfyller kundernas behov och verksamhetsmål på ett effektivt sätt.

#### Tips för att optimera sökregler

- Fäst eller förbättra produkter med höga försäljningsvolymer eller nyligen genomförd försäljningsaktivitet.
- Prioritera produkter med höga betyg och positiva recensioner.
- Se till att artiklar i lager rangordnas högre.
- Prioritera lite produkter med högre vinstmarginaler utan att kompromissa med relevansen.
- Markera produkter som säljs eller ingår i specialerbjudanden.
- Ange sökregler under kampanjen eller försäljningsperioderna automatiskt genom att använda datumintervallet under kampanjperioden.
- Skräddarsy sökresultat baserat på den enskilda kundens beteende med hjälp av [intelligent rankning](rules-add.md#intelligent-ranking), t.ex.&quot;Rekommenderas för dig&quot;,&quot;Visas bäst&quot; osv. För att skräddarsy kundernas beteende måste ni se till att eventeringen implementeras på rätt sätt. För Luma-handlare finns det alltid möjlighet att eventera. För headless-implementeringar eller anpassade implementeringar måste du [implementera &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) utifrån dina specifika behov.

Läs mer om sökregler:

- [Arbetsyta för marknadsföring](rules-workspace.md#set-the-scope)
- [Krav](rules.md#requirements)
- [Standardsökregel](rules.md#default-rule)
- Hantera sökregler
   - [Skapa](rules-add.md)
   - [Redigera, visa, ta bort](rules-manage.md)
- Datainsamling
   - [[!DNL Live Search] händelser](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)
   - [Adobe Commerce Event Collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)
   - [GitHub Commerce-händelser](https://github.com/adobe/commerce-events/tree/main/examples) 

### Använd produktmetadata

Se till att korrekta och detaljerade produktattribut är [konfigurerade som sökbara](workspace.md#set-attributes-as-searchable). Observera att SKU-, namn- och kategoriattribut som standard är sökbara och inte kan uteslutas från sökningen. För bästa resultat ska du inte använda blanksteg i dina SKU:er.

Om du vill öka sökrelevansen tilldelar du en vikt till varje sökbart attribut. Attribut med högre vikt bör visas högre i sökresultatet. Sorteringen efter relevans påverkas av flera kriterier, t.ex. sökvikt. Det innebär att attribut med lägre sökvikt ibland kan ha större relevans än attribut med högre sökvikt. Andra villkor kan vara antalet matchningar i ett givet attribut, positionen för det sökord som hittats och den övergripande textstrukturen före och efter ett sökord.

Se till att varje produkt har relevant innehåll inom varje sökbart attribut. Du bör inte ange ett attribut som sökbart om det har en stor mängd innehåll, eftersom det kan minska sökresultatets relevans.

Läs mer om produktattribut för sökning:

- [Ange attribut som sökbara](workspace.md#set-attributes-as-searchable)
- [Tilldela bredd till attribut](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results#weighted-search)

## Övervaka sökresultat

Om du vill optimera sökresultaten med [!DNL Live Search] ska du övervaka relevanta KPI:er (Key Performance Indicators), som unika frågor, genomsnittlig klickposition, klickfrekvens, konverteringsgrad och nollresultatfrekvens, för att förstå hur kunderna interagerar med sökfunktionen. Denna information hjälper dig att regelbundet uppdatera och förfina sökreglerna.

Du kan övervaka dessa KPI:er på [!DNL Live Search] [prestandaarbetsytan](performance.md) där du hittar följande mått: 

- **Unika sökningar** - Antalet distinkta sökfrågor som har utförts på din [!DNL Commerce]-plats. Varje unik sökning räknas bara en gång, även om den upprepas flera gånger av samma kund eller olika köpare. Denna mätmetod hjälper er att förstå de olika söktermer som används av kunder och ger insikter om vilka produkter eller vilken information som kunderna vill ha. Genom att spåra unika sökningar kan du:

   - Identifiera populära söktrender och ofta sökta objekt.
   - Identifiera potentiella luckor i produktkatalogen eller innehållet.
   - Optimera sökfunktionen genom att lägga till [synonymer](synonyms.md), skapa eller uppdatera sökregler.

- **Genomsnitt klickningsposition** - Anger att den genomsnittliga positionen för sökresultat som kunderna klickat på efter att ha utfört en sökfråga på webbplatsen är densamma. Det här måttet ger insikter om sökresultatens relevans och effektivitet.

  En lägre genomsnittlig klickposition (närmare 1) tyder på att kunderna snabbt hittar relevanta resultat, vilket indikerar att din sökstrategi är effektiv. Det hjälper er att förstå kundernas beteende och hur långt de är villiga att rulla för att hitta den önskade produkten. Om den genomsnittliga klickpositionen är hög kan det tyda på att de mest relevanta resultaten inte visas överst, vilket kräver en granskning och optimering av sökstrategin.

- **Genomklickningsfrekvens (CTR)** - Mäter den procentandel av kunderna som klickar på ett sökresultat efter att ha utfört en sökfråga. En hög CTR indikerar att sökresultaten är relevanta och tilltalande för kunderna när de klickar på de resultat de hittar. Övervakning av CTR kan hjälpa till att identifiera områden som kan förbättras. Låg CTR kan tyda på att sökresultaten inte matchar kundens avsikt, vilket innebär att man måste förfina sökreglerna, förbättra produktinformationen eller förbättra resultatpresentationen.

- **Konverteringsgrad** - Anger sökfunktionens effektivitet när det gäller att öka försäljningen och uppnå affärsmålen. Det återspeglar den övergripande effektiviteten i sökfunktionen när det gäller att tillgodose kundernas behov och underlätta en smidig shoppingupplevelse. En hög konverteringsgrad visar att sökresultaten är mycket relevanta och övertygande, vilket leder kunderna till att slutföra köpet. Om konverteringsgraden är låg kan det tyda på problem med sökrelevans, produkttillgänglighet eller den totala kundresan från sökning till köp.

- **Nollresultat** - Mäter den procentandel av sökfrågorna på din [!DNL Commerce] -plats som inte ger några resultat. Denna mätmetod är avgörande för att förstå hur ofta kundernas sökningar misslyckas och kan ge insikter i potentiella luckor i produktkatalogen eller sökinställningarna. Ett högt resultatvärde på noll kan frustrera kunderna, vilket leder till en dålig shoppingupplevelse och potentiell förlust av kunder. Det kan visa att det finns saknade produkter eller kategorier i din katalog som kunderna söker efter, och ge dem vägledning när det gäller lager och produktlistor.

  Om du vill minska nollresultatfrekvensen kan du:

   - Erbjud alternativa eller relaterade söktermer, till exempel [synonymer](synonyms.md), när inga exakta träffar hittas.
   - Ge kunderna relaterade eller alternativa förslag när sökningen inte ger några resultat genom att ange sökomdirigeringar.
   - Granska regelbundet nollresultatfrågor för att identifiera mönster och göra nödvändiga justeringar i produktkatalogen och sökinställningarna.

- **Populära resultat** - Kan förbättra dina sökresultat avsevärt genom att anpassa dem till kundernas preferenser och beteenden.

Du kan använda dessa mätdata för att optimera sökfunktionen på följande sätt:

- Implementera regler som automatiskt rangordnar populära produkter högre i sökresultaten. Produkter som du ofta klickar på eller köper kan prioriteras så att de visas högst upp. Manuellt strukturera listor med populära produkter för specifika sökfrågor och se till att dessa objekt visas tydligt.
- Markera produkter som för närvarande trendar eller nyligen har sett en ökning av popularitet. Detta kan vara särskilt effektivt under säsongsevenemang, helger eller kampanjperioder. För att uppnå detta använder du den intelligenta rankning som bättre passar ditt användningssätt och ditt företags behov när du skapar en sökregel.
- Markera populära filter eller ansikten, om kunderna ofta filtrerar efter vissa varumärken eller prisintervall, så gör dessa alternativ mer framträdande genom att fästa dem och sortera dem därefter.
- När en sökning ger noll resultat kan du använda populära resultatdata för att föreslå alternativa produkter eller relaterade kategorier som har ett högt kundengagemang.
- Analysera populära söktermer och produktdata för att identifiera viktiga nyckelord. Optimera dina produktsökbara attribut med dessa nyckelord för att förbättra sökrelevansen.
- Analysera regelbundet era resultatdata för att förstå förändrade trender, kundernas preferenser och beteende, identifiera de viktigaste söktermerna och identifiera problem. Använd den här feedbackslingan för att kontinuerligt förfina och förbättra dina sökregler och produkterbjudanden

Om du vill hämta korrekta data i din [!DNL Live Search]-rapport måste du se till att händelser implementeras korrekt. För Luma-handlare finns det alltid möjlighet att eventera. För headless-implementeringar eller anpassade implementeringar måste du [implementera &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) utifrån dina specifika behov.
