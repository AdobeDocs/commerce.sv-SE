---
title: Framgångsmått
description: Framgångsmått ger insikt i nyckelresultatmåtten för din [!DNL Adobe Commerce Optimizer] butik.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 7202a531-fec3-4698-89b9-6bdbcc37015e
source-git-commit: 497f5e887d987435d57a340ef16fcfa561edc545
workflow-type: tm+mt
source-wordcount: '1125'
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

## Generera en rapport

1. Välj **Success Metrics** i den vänstra listen.
1. Under **Rapportkonfiguration** anger du **datumintervall**, **katalogkälla** utifrån språkinställningen och **Valuta**.
1. Klicka på **[!UICONTROL Apply]**.

   De **högsta markeringarna**, **Intäkter**, **Konvertering**, **engagemang**, **Förvärv** och **Studsfrekvens** uppdateras alla baserat på din rapportkonfiguration.

1. Klicka på **[!UICONTROL Export]** om du vill spara rapporten som en PDF.

## Nästa steg och optimeringsstrategier

Använd mätdata för att identifiera möjligheter till förbättringar och implementera riktade optimeringsstrategier. I följande avsnitt ges specifik, användbar vägledning för varje mätområde.

### Intäktsoptimering

Som intäkt är målet att öka den totala försäljningen och det genomsnittliga ordervärdet.

![Resultat för framgångsmått](../assets/revenue.png)

#### Strategier

- **Implementera AI-baserade rekommendationer**: Använd optimerarens rekommendationsmotor för att identifiera relevanta produkter som ökar konverteringsgraden. Distribuera *Kunder som tittade på det här visades även* och *köpte det här, köpte* rekommendationstyper för att öka korsförsäljningsmöjligheterna.

- **Skapa försäljningsregler**: Förbättra produkter med hög marginal i sökresultat med [försäljningsregler](../merchandising/rules/overview.md). Fäst de mest säljande objekten överst i sökresultaten för frågor med hög trafik.

- **Optimera produktupptäckt**: Använd [intelligenta aspekter](../merchandising/facets/overview.md) för att hjälpa kunderna att hitta produkter effektivare, vilket leder till högre konverteringsgrad och ökade intäkter.

- **Utnyttja säsongsrelaterade möjligheter**: Skapa tidsbaserade försäljningsregler för att marknadsföra säsongsrelaterade eller kampanjrelaterade artiklar under perioder med hög köpnivå.

### Förbättrad konverteringsgrad

För att förbättra konverteringsgraden är målet att konvertera fler besökare till kunder.

![Konverteringsgrad för framgångsmått](../assets/conversion-rate.png)

#### Strategier

- **Optimera sökrelevans**: Implementera [synonymer](../merchandising/synonyms/overview.md) för att se till att kunderna hittar det de söker, även med olika söktermer. Använd dynamisk fasettering för att tillhandahålla relevanta filtreringsalternativ.

- **Strategisk rekommendationsplacering**: Distribuera rekommendationsenheter på sidor med hög trafik, som produktinformationssidor och kategorisidor. Använd *De mest visade* och *de flesta köpta* rekommendationerna för att skapa förtroende och snabbhet.

- **Förbättra produktsynligheten**: Använd försäljningsregler för att försäkra dig om att de mest säljande och konverterande produkterna visas tydligt i sökresultaten.

- **Testrekommendationstyper för A/B**: Experimentera med olika rekommendationstyper och placeringar för att hitta det som fungerar bäst för er målgrupp.

### Förbättrat engagemang

För att öka engagemanget är målet att öka kundinteraktionen och tiden på plats.

![Interaktion med framgångsmått](../assets/engagement.png)

#### Strategier

- **Diversifiera rekommendationstyper**: Undvik att visa samma rekommendationer upprepade gånger. Använd en blandning av *Rekommenderas för dig*, *Trending* och *Recrecently displayed* för att hålla innehållet aktuellt och engagerande.

- **Implementera intelligent sökning**: Använd AI-driven dynamisk faceting och omrankning av resultat för att anpassa sökresultat i realtid baserat på kundbeteende.

- **Skapa personaliserade upplevelser**: Distribuera enheter som rekommenderas för dig på hemsidan och under hela kundresan för att få personaliserade produktförslag.

- **Optimera sökupplevelsen**: Använd synonymer för att förbättra sökrelevansen och se till att kunderna snabbt hittar det de söker.

### Förvärvsökning

Målet är att locka fler nya kunder och öka effektiviteten.

![Mätning av lyckade resultat](../assets/acquisition.png)

#### Strategier

- **Utnyttja sökresultatdata**: Använd rapporten [sökprestanda](../manage-results/search-performance.md) för att identifiera trendprodukter och vanliga söktermer. Skapa försäljningsregler för att lyfta fram dessa objekt.

- **Optimera rekommendationsprestanda**: Övervaka [rekommendationsprestanda](../manage-results/recommendation-performance.md) för att identifiera vilka rekommendationstyper som genererar flest trafik och konverteringar.

- **Markera nya och kampanjrelaterade objekt**: Använd försäljningsregler för att lyfta nya produkter eller kampanjartiklar i sökresultaten för att locka till dig uppmärksamhet från nya besökare.

- **Spåra trafikkällor**: Använd händelsedata för att förstå vilka kanaler som ger mest värdefull trafik och optimera marknadsföringssatsningarna utifrån detta.

### Sänk studsfrekvens

För att minska avhoppsfrekvensen är målet att hålla besökarna engagerade och minska antalet besök på en sida.

![Resultatmått för studsfrekvens](../assets/bounce-rate.png)

#### Strategier

- **Förbättra sökrelevansen**: Använd synonymer och intelligenta funktioner för att säkerställa att kunderna snabbt hittar relevanta produkter. Dåliga sökresultat är en viktig orsak till höga studsfrekvenser.

- **Implementera rekommendationsenheter**: Distribuera rekommendationsenheter på kategori- och sökresultatsidor för att tillhandahålla ytterligare produktalternativ och hålla besökarna engagerade.

- **Optimera produktupptäckt**: Använd försäljningsregler för att se till att de mest relevanta och populära produkterna visas först i sökresultaten.

- **Skapa engagerande webbplatsupplevelser**: Använd rekommendationstyperna &quot;Rekommenderas för dig&quot; och &quot;Trending&quot; på din hemsida för att omedelbart engagera besökare med relevant innehåll.

## Felsökning och optimering

### När mätvärden avtar

**Inkomstbortfall**:

- Kontrollera om rekommendationsenheterna fortfarande är aktiva och fungerar bra
- Granska försäljningsreglerna för att säkerställa att produkter med hög marginal marknadsförs
- Analysera sökresultatet för att identifiera om populära produkter fortfarande rankas bra

**Konverteringsfrekvens:**

- Kontrollera att sökrelevansen bevaras (kontrollera synonymer och ansikten)
- Kontrollera att rekommendationsenheterna visas korrekt
- Granska försäljningsregler för eventuella konflikter eller problem

**Höga studsfrekvenser**:

- Kontrollera sökresultatets relevans och implementera synonymer vid behov
- Kontrollera att rekommendationsenheterna läses in korrekt
- Granska produktdatakvalitet och tillgänglighet

**Lågt engagemang**:

- Diversifiera rekommendationstyper för att förhindra att kunderna tröttnar
- Implementera mer personaliserade rekommendationsstrategier
- Optimera sökupplevelsen med bättre ansikten och synonymer

## Fältbeskrivningar

### Rapportkonfiguration

| Fält | Beskrivning |
|---|---|
| Datumintervall | Du kan välja mellan **Senaste 3 månaderna**, **Senaste 7 dagarna**, **Senaste 30 dagarna**, **Senaste 6 månaderna**, **Senaste 12 månaderna** och **År till och med**. Använd kortare intervall för omedelbar optimeringsinsikter och längre intervall för trendanalys. |
| Land | Baserat på den katalogkälla som har angetts för [katalogvyn](../setup/catalog-view.md). Välj lämplig marknad för korrekt prestandaanalys. |
| Valuta | Den valuta som har angetts för katalogvyn. Se till att detta matchar er målmarknad för korrekt intäktsrapportering. |
| Exportera | Sparar rapporten som en PDF för delning med intressenter eller offlineanalys. |

## Mer som detta

- [Sökprestanda](../manage-results/search-performance.md) - Analysera söktermer och optimera sökrelevansen
- [Rekommendationsprestanda](../manage-results/recommendation-performance.md) - Övervaka och optimera rekommendationseffektivitet
- [Rekommendationer - översikt](../merchandising/recommendations/overview.md) - Läs mer om AI-baserade produktrekommendationer
- [Marknadsföringsregler](../merchandising/rules/overview.md) - Öka, begrava, fästa eller dölja produkter i sökresultat
- [Ansikten](../merchandising/facets/overview.md) - Förbättra sökningen med intelligent filtrering
- [Synonymer](../merchandising/synonyms/overview.md) - Förbättra sökrelevansen och kundupplevelsen
- [Händelseöversikt](../setup/events/overview.md) - Förstå data som ligger till grund för dina mätvärden
