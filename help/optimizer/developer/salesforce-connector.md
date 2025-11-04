---
title: Salesforce Commerce Connector
description: Lär dig mer om  [!DNL Commerce Optimizer SFCC Connector] som är en startpunkt för integrering av Salesforce Commerce B2C med [!DNL Adobe Commerce Optimizer] för synkronisering av katalogdata och för implementering och anpassning av kopplingen för att stödja affärsåtgärder.
role: Admin, Developer
source-git-commit: fc6f8566a1932e830a37bcfa32cd1c4168c67c68
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Salesforce Commerce Connector for Adobe Commerce Optimizer

[!DNL Commerce Optimizer Salesforce Commerce Connector] bygger på Adobe App Builder-teknik och möjliggör smidig överföring och hantering av katalogdata från Salesforce Commerce Cloud B2C till [!DNL Adobe Commerce Optimizer]. Programmet överbryggar de båda plattformarna och håller produktinformation, priser och uppdateringar synkade utan att man behöver göra om plattformen.

Med den nya kopplingen får du tillförlitliga funktioner för datasynkronisering och den flexibilitet som krävs för att anpassa arbetsflöden efter företagets behov.

En komplett videosjälvstudiekurs finns i [Lär dig mer om startsatsen för Salesforce Commerce ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/sfcc-starter-kit/overview).

## Nyckelfunktioner

* **Katalogdatasynkronisering:** Skicka produktdata - inklusive varianter, prisböcker och strukturer - från Salesforce Commerce B2C till Adobe Commerce Optimizer för att hålla butiker och upplevelsedrivna program uppdaterade.
* **Prissynkronisering:** Importera och hantera prisdata direkt från Salesforce Commerce B2C.
* **Stöder flera datatyper:** Synkronisera produkter, priser och katalogstrukturer för att återspegla komplexa marknadsföringskonfigurationer.

* **Flexibla arbetsflöden för synkronisering**
   * **Schemalagd synkronisering:** Automatisera uppdateringar med schemaläggning av cron-jobb, ingen manuell åtgärd krävs.
   * **On-Demand Updates:** Utlösa omedelbart uppdateringar på SKU-nivå för brådskande ändringar, korrigeringar eller produktstarter.

* **Byggd för utökningsbarhet**
   * Använder anpassade [Salesforce Commerce B2C API](https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html) (SCAPI)-slutpunkter för kompatibilitet och enkel anpassning till unika eller avancerade användningsfall.
   * Skalas ut i takt med att ni börjar med kataloger och prissynkronisering, och utöka sedan arbetsflödena för att stödja ytterligare integreringar eller affärslogik.
   * Konfigurera och utveckla arbetsflöden utan att bygga om kärnintegreringar.

>[!NOTE]
>
>Kopplingen är särskilt utformad för Salesforce Commerce Cloud B2C. Det stöder inte Salesforce B2B- eller D2C-produkter som är byggda på olika teknikstackar.

## Vem har nytta av Salesforce Connector?

[!DNL Salesforce Commerce Connector] är idealisk för:

* **Befintliga Salesforce Commerce Cloud B2C-kunder** som förbättrar butiksfunktionerna
* **Organisationer med flera varumärken** som behöver avancerade funktioner för marknadsföring och personalisering i flera butiker
* **Företag som söker prestandaförbättringar** genom Adobe Edge Delivery Services för snabbare butiksupplevelser
* **Företag med komplexa prisstrukturer** synkroniserar sofistikerade prisböcker och språkspecifika priser
* **AEM-kunder** som hanterar produktkataloger från Salesforce Commerce B2C när de använder Adobe Commerce storefront med Edge Delivery Services
* **Återförsäljare med krav på flera språk** synkroniserar lokaliserad produktinformation mellan marknader och språk

## Användningsexempel

Kopplingen har stöd för flera viktiga användningsområden:

### Inmatning av katalogdata och visning av butiker

Detta exempel visar det fullständiga dataflödet från Salesforce Commerce B2C till Adobe Commerce store:

1. **Inledande kataloginmatning:** Läs in hela e-handelskatalogen för Salesforce, inklusive enkla produkter med varianter, prisböcker och prisinformation.
1. **Automatiserade delta-uppdateringar:** Synkronisera automatiskt produktuppdateringar från användargränssnittet för kataloghantering i Salesforce Commerce till [!DNL Commerce Optimizer].
1. **Storefront-integrering:** Visa synkroniserade katalogdata i Adobe Commerce Edge Delivery Service Store med [!DNL Commerce Optimizer] storefront-API:er.
1. **Realtidsuppdateringar:** Visa uppdaterad produktinformation (namn, priser, beskrivningar) direkt i butiken när du har gjort ändringar i Salesforce.

### Produkthantering på flera språk

Utnyttja lokaliseringsmöjligheterna i Salesforce Commerce B2C:

* Synkronisera lokaliserade versioner av produkttextfält (namn, beskrivningar) från Salesforce Commerce B2C för olika språkområden.
* Mappa Salesforce språkbegrepp :1 med [!DNL Commerce Optimizer] språkområden.
* Stöd för flera produktanvändningscykler för olika lokaliseringar.
* Bibehåll enhetligheten i globala produktkataloger.

## Arkitektur och komponenter

[!DNL SFCC Connector] innehåller ett robust integreringslager mellan en Salesforce Commerce B2C-instans och [!DNL Commerce Optimizer]. Kopplingen fungerar genom en serie synkroniseringsåtgärder som överför katalogdata, prisböcker och produktinformation.

1. **Dataextrahering** - Autentisera med din Salesforce Commerce B2C-instans och extrahera katalogdata med anpassade SCAPI API:er.
1. **Dataomvandling** - Omforma produktdata så att de matchar datamodellen och schemakraven för [!DNL Commerce Optimizer].
1. **Datainmatning** - Överför transformerade data säkert till [!DNL Commerce Optimizer] med ACO TypeScript SDK.
1. **Storefront-integrering** - Synkroniserade data blir tillgängliga via [!DNL Commerce Optimizer] API:er för butiksupplevelser.

I följande diagram visas dataflödet på hög nivå för integreringen:

![Salesforce Commerce Connector Architecture](../assets/sfcc_starter_kit.png){zoomable="yes"}

### Nyckelkomponenter

[!DNL Commerce Optimizer SFCC Connector] består av flera nyckelkomponenter:

* **ACO SFCC Starter Kit App Builder-program** - Tillhandahåller serverlösa funktioner som hanterar datasynkronisering mellan SFCC och Adobe Commerce Optimizer.
* **Anpassad SFCC-kassett** - Krävd kassett som utökar din Salesforce Commerce Cloud-instans med API:er som behövs för dataextrahering.
* **Hanteringsgränssnitt** - Webbgränssnitt för övervakning av synkroniseringsstatus och hantering av anslutningsåtgärder.

### Synkroniseringsprocess

Kopplingen stöder flera synkroniseringslägen.

| Synkroniseringsläge | Beskrivning |
|-----------|-------------|
| **Fullständig platssynkronisering** | Utför en omfattande synkronisering av alla produkter, prislistor och priser för din konfigurerade Salesforce Commerce Cloud-webbplats och språkområden. Detta inkluderar <ul><li>metadata och attribut</li><li>katalogstruktur och kategorier</li><li>prisböcker</li><li>prisinformation</li><li>flerspråkiga produktdata</li></ul> |
| **Deltasynkronisering** | Hämtar och synkroniserar endast ändringar som gjorts i Salesforce-produkter och prisdata sedan den senaste synkroniseringen, vilket ger effektiva och aktuella uppdateringar.<br>Deltasynkronisering körs automatiskt på schemalagd basis (standard: timme) för att upprätthålla datans aktualitet. |
| **Alternativ för målsynkronisering** | Innehåller detaljerade synkroniseringsfunktioner: <ul><li>**Prisbokssynkronisering** synkroniserar endast prisboksinformation</li><li>**Synkronisering av metadata** uppdaterar produktmetadata och attributdefinitioner</li><li>**Specifik produktsynkronisering** synkroniserar enskilda produkter efter SKU</li></ul> |

## Viktiga överväganden

Tänk på följande när du planerar implementeringen:

### Datamappning och attribut

* **Sökbara attribut:** Salesforce Commerce B2C anger sökbara attribut via användargränssnittet, som inte visas av API:t. Använd [[!DNL Catalog Data Ingestion metadata APIs]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) om du vill konfigurera dessa sökbara attribut manuellt i Adobe Commerce Optimizer.
* **Attributmappning:** Planera mappningen av Salesforce Commerce B2C-produktattribut till [!DNL Commerce Optimizer]-metadata baserat på dina affärsbehov.
* **Standardsökbara fält:** Kopplingen gör automatiskt huvudattribut (`name`, `description`, `ID`) sökbara som standard.

### Synkroniseringsomfång

* **Platsval:** Salesforce Commerce B2C har ett koncept för webbplatser som kataloger är kopplade till. Under synkroniseringen väljer du vilken Salesforce-webbplats som ska synkroniseras.
* **Språkinställningshantering:** Varje Salesforce Commerce-språkinställning resulterar i en separat produktinmatningscykel i [!DNL Commerce Optimizer].
* **Datavolym:** Överväg katalogstorlek och synkroniseringsfrekvens när du planerar implementering.

## Övervakning och hantering

[!DNL Commerce Optimizer SFCC Connector] har installerats och konfigurerats och innehåller omfattande övervaknings- och hanteringsfunktioner från [!DNL SFCC to ACO Sync Panel]:

![Salesforce Commerce Connector Management UI](../assets/sfcc_management_ui.png){width="700" zoomable="yes"}

URL:en för det här gränssnittet anges när du har distribuerat [!DNL Commerce Optimizer SFCC Connector Starter Kit] till App Builder-projektet.

Viktiga funktioner:

* **Synkroniseringsstatusspårning:** Övervaka status och tidsstämplar för alla synkroniseringsåtgärder.
* **Anslutningsverifiering:** Testa anslutningar till både Salesforce Commerce Cloud och Adobe Commerce Optimizer.
* **Produktdataverifiering:** Kontrollera att synkroniserade produktdata visas korrekt i butiken.
* **Felloggning och felsökning:** Felloggar för felsökning kan nås via App Builder CLI.
* **Tillståndshantering:** Spåra synkroniseringsförloppet och förhindra konflikter med inbyggd tillståndshantering.

## Source programkod och utvecklingsresurser

[!DNL Commerce Optimizer SFCC Connector] är en öppen källkod och tillgänglig för anpassning. Bland nyckeldatabaser finns:

* **[ACO SFCC Starter Kit](https://github.com/adobe-commerce/aco-sfcc-starter-kit)** - Huvudanslutningsprogram och -dokumentation.
* **[ACO SFCC-kassetter](https://github.com/adobe-commerce/aco-sfcc-cartridges)** - SFCC-kassett krävs för API-integrering.
* **[ACO TypeScript SDK](https://github.com/adobe-commerce/aco-ts-sdk)** - SDK för Adobe Commerce Optimizer-integrering.

Dessa databaser innehåller fullständig källkod, detaljerad dokumentation och exempel för implementering och anpassning av kopplingen.

## Nästa steg

Vill du integrera dina Salesforce Commerce Cloud-data med Adobe Commerce Optimizer? Börja med att läsa den detaljerade implementeringsguiden i [ACO SFCC Starter Kit-databasen](https://github.com/adobe-commerce/aco-sfcc-starter-kit) och kontrollera att du har de nödvändiga förutsättningarna på plats.
