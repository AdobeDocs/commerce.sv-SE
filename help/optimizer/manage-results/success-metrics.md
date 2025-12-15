---
title: Framgångsmått
description: Framgångsmått ger insikt i nyckelresultatmåtten för din [!DNL Adobe Commerce Optimizer] butik.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 7202a531-fec3-4698-89b9-6bdbcc37015e
source-git-commit: 4e85d70dc1b099a5b40a807a76ca589aa9a28f07
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# Framgångsmått

Den här sidan innehåller en översikt över nyckeltal för prestandamått för din [!DNL Adobe Commerce Optimizer]-butik. Målet är att du snabbt ska förstå resultatet av implementeringen av [!DNL Adobe Commerce Optimizer], och sedan hjälpa dig och ditt team att identifiera tillväxtmöjligheter och lyfta fram områden som ska optimeras.

![Rapport om lyckade mätvärden](../assets/success-metrics.png)

Måtten i rapporten hämtas från butikshändelsedata. [Läs mer](../setup/events/overview.md) om händelsedata som samlats in.

## Förstå mätvärden

Rapporten om framgångsmätningar ger användbara insikter om fem viktiga prestandaområden som direkt påverkar affärsresultatet. Varje mätvärde visar mönster i kundbeteenden och butiksprestanda som hjälper er att identifiera möjligheter och hantera utmaningar. Utnyttja dessa insikter för att fatta smartare beslut och optimera er handelsupplevelse.

**De översta högdagrarna** sammanfattar nyckelvärden från varje prestandaområde. Använd det här avsnittet för att snabbt identifiera de största möjligheterna till förbättring.

De viktigaste resultatindikatorerna är:

- **Intäkter** - Ditt primära ekonomiska mått visar det totala försäljningsresultatet.
- **Konvertering** - Andelen besökare som slutfört sina inköp.
- **Engagemang** - Så här interagerar aktivt användare med din webbplats.
- **Förvärv** - Effektiviteten i kundvärvningen.
- **Studsfrekvens** - Andelen besökare som lämnar efter att endast en sida har visats.

### Dataaktualitet och -precision

**Uppdateringsfrekvens:** Data för lyckade mått bearbetas och uppdateras regelbundet allt eftersom butikshändelser samlas in och bearbetas.

**När mätvärden ska kontrolleras:** Om du vill ha den mest korrekta trendanalysen kan du granska mätvärden efter att tillräcklig tid har gått för att samla in meningsfulla data. Dagliga fluktuationer är normala. Fokusera på trender varje vecka eller månad för strategiska beslut.

**Datakvalitet:** Mätvärden beräknas utifrån faktiska kundinteraktioner som hämtats via butikshändelser. Kontrollera att din butik har rätt [händelsespårning konfigurerad](../setup/events/overview.md) för korrekt rapportering.

## Generera en rapport

1. Välj **Success Metrics** i den vänstra listen.
1. Under **Rapportkonfiguration** anger du **datumintervall**, **katalogkälla** utifrån språkinställningen och **Valuta**.
1. Klicka på **[!UICONTROL Apply]**.

   De **högsta markeringarna**, **Intäkter**, **Konvertering**, **engagemang**, **Förvärv** och **Studsfrekvens** uppdateras alla baserat på din rapportkonfiguration.

1. Klicka på **[!UICONTROL Export]** om du vill spara rapporten som en PDF.

## Använda Success Metrics och Sites Optimizer tillsammans

Success Metrics och Sites Optimizer ([Opportunity](opportunities.md)) är komplementära verktyg som fungerar tillsammans och hjälper dig att förbättra din e-handelsplats prestanda. Genom att förstå skillnaden mellan dessa funktioner kan du fatta bättre beslut och uppnå mätbara resultat.

### Viktiga skillnader

| Proportioner | Success Metrics | Sites Optimizer (möjligheter) |
|---|---|---|
| **Syfte** | Mät prestanda och resultat | Identifierar problem och ger rekommendationer |
| **Typ** | Analytisk kontrollpanel | Proaktiv problemidentifiering |
| **Vad det visar** | Viktiga resultatindikatorer (Intäkter, Konvertering, Inköp, Anskaffning, Studsfrekvens) | AI-baserade rekommendationer för problem som påverkar webbplatsens prestanda |
| **Datakälla** | Händelsedata för butiken | Produktkataloger, sökloggar, rekommendationsdata |
| **Använd när** | Du vill spåra resultat över tid | Du vill identifiera och åtgärda specifika problem |

### Så här använder du de här funktionerna tillsammans

Den mest effektiva metoden kombinerar båda verktygen i en kontinuerlig förbättringscykel:

1. **Mät med Success Metrics**: Börja med att granska kontrollpanelen Success Metrics för att få en förståelse för dina aktuella prestanda. Identifiera vilka KPI:er som behöver förbättras (till exempel låg konverteringsgrad eller hög studsfrekvens).

1. **Diagnostisera med affärsmöjligheter**: Navigera till sidan Affärsmöjligheter för att upptäcka specifika problem som kan orsaka dålig prestanda. Sites Optimizer skannar produktkatalogen, sökloggar och rekommendationsdata för att identifiera problem som saknade produktdata, dålig sökrelevans eller navigeringsproblem.

1. **Implementera rekommendationer**: Följ de AI-drivna rekommendationerna i säljprojekt för att åtgärda identifierade problem. Det kan vara till exempel att åtgärda problem med produktdatakvalitet, förbättra SEO eller optimera sökning och identifiering.

1. **Spåra förbättringar**: Gå tillbaka till Success Metrics för att övervaka hur ändringarna påverkar nyckeltal över tid. Använd datumintervallväljaren för att jämföra prestanda före och efter implementering av rekommendationer.

1. **Upprepa och optimera**: Fortsätt den här cykeln genom att använda säljprojekt för att identifiera nya problem och framgångsmått för att mäta effekten av optimeringarna.

### Exempel på arbetsflöde

En handlare ser att deras konverteringsgrad sjunker i Success Metrics. Så här kan de använda båda funktionerna:

1. **Identifiera problemet**: På kontrollpanelen Success Metrics visas att konverteringsgraden sjönk med 15 % under den senaste månaden.

1. **Hitta orsaken**: På sidan Affärsmöjligheter visas flera problem:
   - Flera produkter saknar viktiga attribut som påverkar sökrelevansen.
   - Vanliga sökfrågor returnerar dåliga resultat.
   - Långsam sidinläsningstid på kategorisidor.

1. **Vidta åtgärd**: Handlaren prioriterar att åtgärda problem med produktdatakvaliteten först, eftersom Sites Optimizer kategoriserar dessa som möjligheter med stor effekt som påverkar sökning och rekommendationer.

1. **Mät resultat**: När produktattribut har uppdaterats och rekommenderade ändringar har implementerats övervakas Success Metrics varje vecka. Under nästa månad ökar konverteringsgraden med 12 % och antalet sökinteraktioner förbättras avsevärt.

1. **Fortsätt optimera**: Med en förbättrad konverteringsgrad flyttar handlaren fokus till nästa prioritet som visas i säljprojekt, vilket optimerar sidinläsningshastigheten för att minska avhoppsfrekvensen.

### När ska varje funktion användas

**Använd framgångsmått när du vill:**

- Spåra övergripande affärsresultat.
- Mät effekten av förändringar över tid.
- Identifiera vilka områden i er verksamhet som behöver uppmärksammas.
- Dela resultatrapporter med intressenter.
- Förstå kundbeteendetrender.

**Använd Sites Optimizer (säljprojekt) när du vill:**

- Upptäck specifika problem som påverkar prestandan.
- Få användbara rekommendationer för att åtgärda problem.
- Förstå varför vissa mätvärden sjunker.
- Prioritera vilka optimeringar som ska tas i bruk först.
- Utnyttja AI för att identifiera problem som du kan missa manuellt.

Tillsammans ger de här funktionerna en komplett lösning: Success Metrics ger dig *vad* händer, medan Sites Optimizer berättar *varför* och *hur du åtgärdar det*.

## Nästa steg och optimeringsstrategier

Använd mätdata för att identifiera möjligheter till förbättringar och implementera riktade optimeringsstrategier. I följande avsnitt ges specifik, användbar vägledning för varje mätområde.

>[!BEGINTABS]

>[!TAB Intäktsoptimering]

Som intäkt är målet att öka den totala försäljningen och det genomsnittliga ordervärdet.

![Resultat för framgångsmått](../assets/revenue.png)

### Inkomstmåttet

**Vad det mäter:** Total inkomst som har genererats av din butik under den valda tidsperioden.

**Så här beräknas det:** Intäkter är summan av alla slutförda order (baspris × kvantitet) för alla produkter som sålts under rapporteringsperioden. Beräkningen använder data från `place-order` händelser som hämtats på din butik.

>[!IMPORTANT]
>
>Intäktsberäkningar exkluderar annullerade order, returer och order där händelsen `place-order` inte hämtades. Händelser kan saknas på grund av medgivandeinställningar, webbläsarproblem (annonsblockerare, skriptfel) eller tekniska bearbetningsfel.

**Formel:**

```
Total Revenue = Sum of (Product Base Price × Quantity) for all completed orders
```

**Datakälla:** StoreFront-händelser (speciellt `place-order` händelser)

**Innehåll:**

- Alla slutförda order under det valda datumintervallet.
- Basproduktpriser multiplicerat med inköpta kvantiteter.
- Intäkter från alla försäljningskanaler som spåras av Commerce Optimizer.

**Viktiga anteckningar:**

- Intäkterna beräknas baserat på baspriser som samlats in vid butiksevenemang.
- Rapporteringsperioden bestäms av det datumintervall du väljer i rapportkonfigurationen.
- Intäktsmått uppdateras när nya orderhändelser bearbetas.

### Strategier

- **Implementera AI-baserade rekommendationer**: Använd optimerarens rekommendationsmotor för att identifiera relevanta produkter som ökar konverteringsgraden. Distribuera *Kunder som tittade på det här visades även* och *köpte det här, köpte* rekommendationstyper för att öka korsförsäljningsmöjligheterna.

- **Skapa försäljningsregler**: Förbättra produkter med hög marginal i sökresultat med [försäljningsregler](../merchandising/rules/overview.md). Fäst de mest säljande objekten överst i sökresultaten för frågor med hög trafik.

- **Optimera produktupptäckt**: Använd [intelligenta aspekter](../merchandising/facets/overview.md) för att hjälpa kunderna att hitta produkter effektivare, vilket leder till högre konverteringsgrad och ökade intäkter.

- **Utnyttja säsongsrelaterade möjligheter**: Skapa tidsbaserade försäljningsregler för att marknadsföra säsongsrelaterade eller kampanjrelaterade artiklar under perioder med hög köpnivå.

>[!TAB Förbättrad konverteringsgrad]

För att förbättra konverteringsgraden är målet att konvertera fler besökare till kunder.

![Konverteringsgrad för framgångsmått](../assets/conversion-rate.png)

### Förstå mätvärdena för konverteringsgrad

**Vad det betyder:** Andelen besökare som visar produkter och sedan slutför ett köp, vilket visar hur effektivt din butik konverterar webbläsare till köpare.

**Så här beräknas det:** Konverteringsgraden jämför antalet unika besökare som köpte produkter mot antalet unika besökare som visade produkter.

**Formel:**

```
Conversion Rate = (Total Number of Orders ÷ Total Unique Visitors) × 100
```

**Datakälla:** StoreFront-händelser.

**Så här fungerar det:**

- **Produktvyer** spåras när besökare visar produktsidor (med `product-view` händelser).
- **Inköp** spåras när beställningarna har slutförts (med `place-order` händelser).
- Beräkningen matchar användare som visade specifika produkter med dem som köpte dem.

**Viktiga anteckningar:**

- En besökare som tittar på flera produkter men gör ett inköp räknas som en konvertering.
- Mätvärdena spårar unika besökare med hjälp av webbläsarbaserade identifierare.
- Produktvyhändelser innehåller alltid ett klick, så vyer representerar ett verkligt användarintresse.

### Strategier

- **Optimera sökrelevans**: Implementera [synonymer](../merchandising/synonyms/overview.md) för att se till att kunderna hittar det de söker, även med olika söktermer. Använd dynamisk fasettering för att tillhandahålla relevanta filtreringsalternativ.

- **Strategisk rekommendationsplacering**: Distribuera rekommendationsenheter på sidor med hög trafik, som produktinformationssidor och kategorisidor. Använd *De mest visade* och *de flesta köpta* rekommendationerna för att skapa förtroende och snabbhet.

- **Förbättra produktsynligheten**: Använd försäljningsregler för att försäkra dig om att de mest säljande och konverterande produkterna visas tydligt i sökresultaten.

- **Testrekommendationstyper för A/B**: Experimentera med olika rekommendationstyper och placeringar för att hitta det som fungerar bäst för er målgrupp.

>[!TAB Förstärkning av engagemanget]

För att öka engagemanget är målet att öka kundinteraktionen och tiden på plats.

![Interaktion med framgångsmått](../assets/engagement.png)

### Förstå engagemangsmåtten

**Vad det betyder:** Så här interagerar användare aktivt med din butik och håller reda på meningsfulla åtgärder, från inledande surfning till utcheckningsprocessen.

**Så här beräknas det:** Engagemang spårar alla interaktioner som indikerar aktivt deltagande i din butik, inklusive bläddring, kundvagnsaktiviteter och utcheckningsåtgärder.

**Datakälla:** StoreFront-händelser

**Vad räknas som engagemang:**

Engagemang omfattar följande händelsekategorier och åtgärder:

- **Produktinteraktioner:** Produktvyer, produktklick och produktjämförelser.
- **Kundvagnsaktiviteter:** Lägger till artiklar i kundvagnen, uppdaterar kvantiteter och tar bort artiklar.
- **Utcheckningsåtgärder:** Initierar utcheckning, slutför utcheckningssteg.
- **Kategoribläddring:** Visa kategorisidor, filtrera efter fasets.
- **Önsklisteaktiviteter:** Lägger till i önskelistan, visar önskelisteobjekt.

**Information om händelsespårning:**

Systemet spårar engagemang när händelser har:

- Kategori: `product`, `shopper`, `shopping-cart` eller `checkout`.
- Egenskap: `Product`, `Checkout`, `Cart`, `Category` eller `Wishlist`.

**Viktiga anteckningar:**

- Högre engagemang korrelerar vanligtvis med högre konverteringsgrader.
- Interaktionsstatistik hjälper till att identifiera var användarna är mest aktiva på sin resa.
- Använd engagemangsdata för att optimera sidor med hög trafik och förbättra användarupplevelsen.

### Strategier

- **Diversifiera rekommendationstyper**: Undvik att visa samma rekommendationer upprepade gånger. Använd en blandning av *Rekommenderas för dig*, *Trending* och *Recrecently displayed* för att hålla innehållet aktuellt och engagerande.

- **Implementera intelligent sökning**: Använd AI-driven dynamisk faceting och omrankning av resultat för att anpassa sökresultat i realtid baserat på kundbeteende.

- **Skapa personaliserade upplevelser**: Distribuera enheter som rekommenderas för dig på hemsidan och under hela kundresan för att få personaliserade produktförslag.

- **Optimera sökupplevelsen**: Använd synonymer för att förbättra sökrelevansen och se till att kunderna snabbt hittar det de söker.

>[!TAB Förvärvsökning]

Målet är att locka fler nya kunder och öka effektiviteten.

![Mätning av lyckade resultat](../assets/acquisition.png)

### Förstå anskaffningsvärdet

**Vad det betyder:** Antalet nya unika besökare som kommer till din butik, vilket hjälper dig att förstå hur effektiv er marknadsföring och kundvärvning är.

**Så här beräknas det:** Anskaffningen räknar unika besökare baserat på webbläsaridentifierare som tilldelats vid deras första besök i din butik.

**Datakälla:** StoreFront-händelser.

**Så här fungerar det:**

- Varje besökares webbläsare får en unik identifierare (`domain_userid`) via en cookie från en annan leverantör.
- Nya besökare identifieras när deras sessionsindex är lika med 1 (första besök).
- Dessa identifierare spåras för att skilja nya besökare från återkommande.

**Viktiga anteckningar:**

Den här spårningsmetoden har några kända begränsningar:

- **Användare på olika enheter:** Samma person som besöker olika enheter (datorer, mobiler, surfplattor) eller webbläsare räknas som flera unika besökare eftersom varje enhet och webbläsare får en annan identifierare.
- **Cookie-rensning:** Användare som rensar sina webbläsarcookies tilldelas en ny identifierare och räknas som nya besökare igen.
- **Sekretessinställningar:** Användare med strikta sekretessinställningar eller cookie-blockerare kan inte spåras.

**Bäst för:**

- Spåra nya besökartrender över tid.
- Analysera effektiviteten i marknadsföringskampanjer.
- Förstå mönster för trafiktillväxt.

**Tolkningstips:** Även om det inte är helt korrekt på grund av begränsningarna ovan, är värvningsstatistik tillförlitliga för att identifiera trender och jämföra perioder när de flesta användare surfar på samma enhet och inte ofta tar bort cookies.

### Strategier

- **Utnyttja sökresultatdata**: Använd rapporten [sökprestanda](../manage-results/search-performance.md) för att identifiera trendprodukter och vanliga söktermer. Skapa försäljningsregler för att lyfta fram dessa objekt.

- **Optimera rekommendationsprestanda**: Övervaka [rekommendationsprestanda](../manage-results/recommendation-performance.md) för att identifiera vilka rekommendationstyper som genererar flest trafik och konverteringar.

- **Markera nya och kampanjrelaterade objekt**: Använd försäljningsregler för att lyfta nya produkter eller kampanjartiklar i sökresultaten för att locka till dig uppmärksamhet från nya besökare.

- **Spåra trafikkällor**: Använd händelsedata för att förstå vilka kanaler som ger mest värdefull trafik och optimera marknadsföringssatsningarna utifrån detta.

>[!TAB Sänkning av studs]

För att minska avhoppsfrekvensen är målet att hålla besökarna engagerade och minska antalet besök på en sida.

![Resultatmått för studsfrekvens](../assets/bounce-rate.png)

### Förstå studsfrekvensmåttet

**Vad det betyder:** Andelen besökare som lämnar din webbplats efter att endast ha visat en sida, vilket indikerar potentiella problem med användarupplevelsen, sidrelevansen eller webbplatsengagemanget.

**Så här beräknas det:** Studsfrekvensen jämför enkelsidiga sessioner med det totala antalet sessioner för att avgöra hur många besökare som lämnar utan ytterligare interaktion.

**Formel:**

```
Bounce Rate = (Number of Bounced Sessions ÷ Total Sessions) × 100
```

**Datakälla:** StoreFront-händelser.

**Så här fungerar det:**

- En **avbruten session** räknas när en besökare endast visar en sida under hela besöket.
- Systemet spårar sidvisningar i varje session för att identifiera enkelsidiga besök.
- Sessionerna avgörs av användaraktivitet och tid mellan interaktioner.

**Vad orsakar studsar:**

- Besökare som landar på irrelevanta sidor (dålig söknings-/annonsanpassning).
- Långsam sidinläsningstid.
- Dålig användarupplevelse eller förvirrande navigering.
- Hitta information snabbt utan att behöva utforska mer.
- Tekniska fel.

**Viktiga anteckningar:**

- Höga studsfrekvenser är inte alltid negativa - vissa sidor (som kontaktinformation eller specifika produktspecifikationer) kan naturligtvis ha höga studsfrekvenser.
- Jämför studsfrekvenser mellan olika sidtyper och trafikkällor för att identifiera problemområden.
- Plötsliga ökningar av avhoppsfrekvensen visar ofta på tekniska problem eller dålig målgruppsanpassning för kampanjer.

**Vad är en bra studsfrekvens?** Detta varierar beroende på bransch- och sidtyp, men vanligtvis:

- 40-60 %: Genomsnitt för e-handelsplatser.
- Under 40 %: Utmärkt engagemang.
- Över 70 %: Kan tyda på problem som kräver utredning.

### Strategier

- **Förbättra sökrelevansen**: Använd synonymer och intelligenta funktioner för att säkerställa att kunderna snabbt hittar relevanta produkter. Dåliga sökresultat är en viktig orsak till höga studsfrekvenser.

- **Implementera rekommendationsenheter**: Distribuera rekommendationsenheter på kategori- och sökresultatsidor för att tillhandahålla ytterligare produktalternativ och hålla besökarna engagerade.

- **Optimera produktupptäckt**: Använd försäljningsregler för att se till att de mest relevanta och populära produkterna visas först i sökresultaten.

- **Skapa engagerande webbplatsupplevelser**: Använd rekommendationstyperna &quot;Rekommenderas för dig&quot; och &quot;Trending&quot; på din hemsida för att omedelbart engagera besökare med relevant innehåll.

>[!ENDTABS]

## Felsökning och optimering

### När mätvärden avtar

**Inkomstbortfall**:

- Kontrollera om rekommendationsenheterna fortfarande är aktiva och fungerar bra.
- Se över försäljningsreglerna för att säkerställa att produkter med hög marginal marknadsförs.
- Analysera sökresultatet för att se om populära produkter fortfarande rankas bra.

**Konverteringsfrekvens:**

- Kontrollera att sökrelevansen upprätthålls (kontrollera synonymer och ansikten).
- Kontrollera att rekommendationsenheterna visas korrekt.
- Granska försäljningsreglerna för eventuella konflikter och problem.

**Höga studsfrekvenser**:

- Kontrollera sökresultatets relevans och implementera synonymer om det behövs.
- Kontrollera att rekommendationsenheterna läses in korrekt.
- Granska produktdatakvalitet och tillgänglighet.

**Lågt engagemang**:

- Diversifiera rekommendationstyper för att förhindra att kunderna tröttnar.
- Implementera mer personaliserade rekommendationer.
- Optimera sökupplevelsen med bättre ansikten och synonymer.

## Fältbeskrivningar

### Rapportkonfiguration

| Fält | Beskrivning |
|---|---|
| Datumintervall | Du kan välja mellan **Senaste 3 månaderna**, **Senaste 7 dagarna**, **Senaste 30 dagarna**, **Senaste 6 månaderna**, **Senaste 12 månaderna** och **År till och med**. Använd kortare intervall för omedelbar optimeringsinsikter och längre intervall för trendanalys. |
| Land | Baserat på den katalogkälla som har angetts för [katalogvyn](../setup/catalog-view.md). Välj lämplig marknad för korrekt prestandaanalys. |
| Valuta | Den valuta som har angetts för katalogvyn. Se till att detta matchar er målmarknad för korrekt intäktsrapportering. |
| Exportera | Sparar rapporten som en PDF för delning med intressenter eller offlineanalys. |

## Mer som detta

- [Sökprestanda](../manage-results/search-performance.md) - Analysera söktermer och optimera sökrelevansen.
- [Rekommendationsprestanda](../manage-results/recommendation-performance.md) - Övervaka och optimera rekommendationseffekten.
- [Rekommendationer - översikt](../merchandising/recommendations/overview.md) - Lär dig mer om AI-baserade produktrekommendationer.
- [Marknadsföringsregler](../merchandising/rules/overview.md) - Öka, begrava, fästa eller dölja produkter i sökresultat.
- [Ansikten](../merchandising/facets/overview.md) - Förbättra sökningen med intelligent filtrering.
- [Synonymer](../merchandising/synonyms/overview.md) - Förbättra sökrelevansen och kundupplevelsen.
- [Händelseöversikt](../setup/events/overview.md) - Förstå de data som ligger till grund för dina mätvärden.
