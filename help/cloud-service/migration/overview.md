---
title: Migrera till [!DNL Adobe Commerce as a Cloud Service]
description: Lär dig hur du migrerar till [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
role: Developer
level: Intermediate
source-git-commit: af56d52f98a83310b858f82f16693f5323c1b962
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 0%

---

# Migrera till [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] innehåller en omfattande guide för utvecklare som övergår från en befintlig Adobe Commerce PaaS-implementering till det nya SaaS-erbjudandet (Adobe Commerce as a Cloud Service). Adobe Commerce som molntjänst representerar en betydande förändring mot en fullt hanterad, versionslös SaaS-modell, som erbjuder förbättrad prestanda, skalbarhet, förenklade operationer och tätare integration med den bredare [!DNL Adobe Experience Cloud].

>[!NOTE]
>
>För mer information om migreringsverktyg, se [Bulk Data Migration Tool](./bulk-data.md).

## Att förstå förändringen – jämföra PaaS och SaaS

**Viktiga skillnader**

* [!BADGE PaaS endast]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."} **PaaS (nuvarande):** Merchant hanterar applikationskod, uppgraderingar, patchar och infrastrukturkonfiguration inom Adobes hostade miljö. [Modellen för delat ansvar](https://experienceleague.adobe.com/sv/docs/commerce-operations/security-and-compliance/shared-responsibility) för tjänster (MySQL, Elasticsearch och andra).
* [!BADGE Endast]{type=Positive url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."} **SaaS SaaS (Nytt - [!DNL Adobe Commerce as a Cloud Service])**: Adobe hanterar helt kärnapplikationen, infrastrukturen och uppdateringarna. Handlare fokuserar på anpassning via utbyggbarhetspunkter (API:er, App Builder, UI-SDK:er). Kärnapplikationskoden är låst.

**Arkitektoniska implikationer**

* **Versionslös plattform**: Kontinuerliga uppdateringar innebär inga större versionsuppgraderingar för kärnan.
* **Mikrotjänster och API-först**: Djupare beroende av API:er för utbyggbarhet och integration.
* **Headless som standard (valfritt):** Starkt stöd för frikopplade butiker (till exempel Commerce Storefront som drivs av Edge Delivery Services).
* **Edge-leveranstjänster**: Påverkan på frontend-prestanda och distribution.

**Nya verktyg och koncept**

* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) och [API Mesh för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Handelsoptimerare](../../optimizer/overview.md)
* [Kantleveranstjänster](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE)
* Självbetjäningsprovisionering med [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Migrationsvägar

[!DNL Adobe Commerce as a Cloud Service] Stöder flera migreringsvägar, beroende på din tidslinje, butik och anpassningar.

Som ett alternativ till en fullständig migrering [!DNL Adobe Commerce as a Cloud Service] stödjer den en fasad migrering, med Commerce Optimizer eller en inkrementell metod.

* **Inkrementell migrering**—Detta tillvägagångssätt innebär att du migrerar dina data, anpassningar och integrationer i steg. Detta tillvägagångssätt är idealiskt för stora handlare med många anpassningar som vill gradvis överföra sina komplexa anpassningar och data till [!DNL Adobe Commerce as a Cloud Service] dem i sin egen takt.

![Inkrementell migration](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—Denna metod gör det möjligt att migrera iterativt, genom att använda Commerce Optimizer som en övergångsfas för att flytta komplexa anpassningar och data i [!DNL Adobe Commerce as a Cloud Service] din egen takt. Commerce Optimizer ger tillgång till Merchandising-tjänster drivna av katalogvyer och policyer, Commerce Storefront drivna av Edge Delivery, och [!DNL Product Visuals powered by AEM Assets].

![iterativ migrering](../assets/optimizer.png){width="600" zoomable="yes"}

* **Fullständig migrering** - Detta innebär att migrera alla data, anpassningar och integreringar samtidigt. Den här metoden är perfekt för mindre handlare med få anpassningar som snabbt vill övergå till [!DNL Adobe Commerce as a Cloud Service].

I följande tabell visas en översikt över migreringsprocessen för olika butiker och konfigurationer:

|                    | LUMA Storefront | PWA Storefront | Commerce Storefront med Edge Delivery i botten | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Datamigrering | Obligatoriskt | Obligatoriskt | Obligatoriskt | Obligatoriskt |
| Storefront | Migrera till Commerce Storefront från Edge Delivery | Migrera till Commerce Storefront från Edge Delivery eller underhåll | Ingen effekt | Ingen påverkan |
| API Mesh | Skapa nytt nät | Skapa nytt nät eller konfigurera om befintligt nät | Skapa nytt nät eller konfigurera om befintligt nät | Skapa nytt nät eller konfigurera om befintligt nät |
| Integrationer | Startkit för integration med utnyttjande | Startkit för integration med utnyttjande | Startkit för integration med utnyttjande | Startkit för integration med utnyttjande |
| Anpassningar | Övergång till App Builder &amp; API Mesh | Övergång till App Builder &amp; API Mesh | Övergång till App Builder &amp; API Mesh | Övergång till App Builder &amp; API Mesh |
| Assets Management | Migrering krävs vid användning av OOTB | Migrering krävs vid användning av OOTB | Migrering krävs vid användning av OOTB | Migrering krävs om man använder OOTB |
| Utbyggnader | Migrera till App Builder | Migrera till App Builder | Migrera till App Builder | Migrera till App Builder |

Som visas i tabellen kommer åtgärderna för varje migration att bestå av:

* **Datamigrering**—Med hjälp av[&#x200B; tillhandahållna &#x200B;](./bulk-data.md)migreringsverktyg för att migrera data från din befintliga instans till [!DNL Adobe Commerce as a Cloud Service].
* **Storefront**—Befintliga Commerce Storefronts drivna av Edge Delivery och headless butiker kräver ingen åtgärd, men Luma-butiker kräver migrering till Commerce Storefront driven av Edge Delivery. PWA Studio-butiker kan migreras till Commerce Storefront som drivs av Edge Delivery eller underhålls i sitt nuvarande skick. Adobe kommer att tillhandahålla acceleratorer för att hjälpa till med flytt av butiker.
* **[API Mesh](https://developer.adobe.com/graphql-mesh-gateway)**—Skapa ett nytt mesh eller modifiera det befintliga. Adobe kommer att tillhandahålla förkonfigurerade mesh för att hjälpa till med denna process.
* **Integrationer**—Alla integrationer måste använda antingen integrationsstartpaketet[&#x200B; &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)eller REST API:[[!DNL Adobe Commerce as a Cloud Service] et](https://developer.adobe.com/commerce/webapi/reference/rest/saas/).
* **Anpassningar—** Alla anpassningar måste flyttas till App Builder och API Mesh.
* **Tillgångsförvaltning**—All tillgångsförvaltning kräver migrering. Om du redan använder [!DNL AEM Assets], finns det inget behov av att migrera.
* **Tillägg—** Alla tillägg under processen måste återskapas som utgående tillägg. I slutet av 2025 kommer Adobe att ge tillgång till våra mest populära tillägg för att minimera byggtider.

## Migrationsfaser

Följande faser beskriver de nödvändiga stegen och övervägandena för att migrera till [!DNL Adobe Commerce as a Cloud Service].

### Bedömning och planering före migration

Denna fas är viktig för att minimera riskerna och fastställa en tydlig migreringsväg och identifiera problem innan de uppstår.

**Identifiering och granskning av den aktuella miljön**

**Kodbasanalys:**

* Identifiera alla anpassade moduler, teman och åsidosättningar.
* Analysera ändringar av kärnkoden och se vilka som behöver omfaktoriseras som en del av migreringen.
* Utvärdera tillägg från tredje part och fastställa kompatibilitet med [!DNL Adobe Commerce as a Cloud Service]. Finns det SaaS-kompatibla alternativ, eller behöver du skapa anpassade API-integreringar för App Builder-program?
* Identifiera kod eller funktioner som inte kommer att migreras.

**Datakontroll:**

* Utvärdera databasens storlek och komplexitet.
* Identifiera oanvända data eller tabeller för rensning.
* Granska befintliga import-/exportprocesser.

**Integrationsgranskning:**

* Lista alla externa system som är integrerade med Adobe Commerce (ERP, CRM, PIM, betalningsgateways, rederier, OMS och alla andra system).
* Utvärdera integreringsmetoder (API, egna skript och andra metoder).
* Utvärdera kompatibiliteten med [!DNL Adobe Commerce as a Cloud Service]s API:er först och App Builder.

**Prestandatester:**

* Dokumentera de aktuella poängen för Lighthuse, sidinläsningstider och nyckeltal (KPI), som är en baslinje för att mäta förbättringar efter migrering.

**Granskning av säkerhetskonfiguration:**

* Utvärdera eventuella anpassade WAF-regler, IP-tillåtelselista och andra säkerhetskonfigurationer.

**Definiera migreringsomfång och -strategi:**

* **Avfasad och migrering från en gång till en:** Utvärdera för- och nackdelar för varje tillvägagångssätt.
* **Identifiera kärnaffärsprocesser:** Prioritera funktioner som måste migreras först, såsom:
   * Komplexa prissättningsregler
   * Anpassade affärsregler som tillämpas innan en order officiellt läggs eller bearbetas
   * Komplexa skatteberäkningar
   * Adressvalideringar
   * Anpassad logik triggas efter att en beställning lagts
* **Huvudlös vs. monolitisk butik:** Beslutspunkt för ny butiksutveckling eller anpassning av befintliga butikslokaler.
* **Integrationsstrategi:** Bestäm hur befintliga integrationer ska omplattformas (API Mesh, App Builder, direkt API).
* **Datamigreringsstrategi:** Bestäm om du avser att migrera med fullständig historisk data, partiell data eller ingen migrerad data.

**Lagberedskap och träning:**

* Bekanta dig med [!DNL Adobe Commerce as a Cloud Service] koncept, utvecklingsarbetsflöden och nya verktyg.
* Gå praktisk utbildning med Adobe App Builder, Edge Delivery Services och [!DNL Adobe Commerce as a Cloud Service] distributionspipelines.

**Miljöuppsättning och provisionering:**

* Provisionera dina [!DNL Adobe Commerce as a Cloud Service] sandlåde- och utvecklingsmiljöer med Commerce Cloud Manager.

### Inkrementella migreringsfaser

**Strategisk omfaktorisering och externalisering**

Den här fasen består av kärnan i migreringen, med fokus på att anpassa kodbasen till det [!DNL Adobe Commerce as a Cloud Service]-molnbaserade paradigmet. Detta innebär att strategiskt implementera nya Adobe-tjänster och flytta bort anpassad logik från Commerce kärnplattform.

#### &#x200B;1. Migrera&quot;pågående&quot; anpassningar och tillägg till App Builder

Detta är en avgörande fas för att uppnå en &quot;låst kärna&quot; och framtidssäkra din lösning, vilket är centralt för arkitekturfilosofin [!DNL Adobe Commerce as a Cloud Service] .

* **Externalisera komplex logik till App Builder**: Analysera befintliga anpassade moduler och tredjepartstillägg i din PaaS-kodbas. För komplex affärslogik, skräddarsydda integrationer eller mikrotjänster som inte kräver direkt, pågående manipulation av Commerce-kärndatamodellen, refaktorera och omplattform dem som serverlösa applikationer inom Adobe Developer App Builder.
* **Utnyttja API Mesh**: För scenarier som kräver data från flera backend-system (till exempel din PaaS Commerce-backend, ERP, CRM och anpassade App Builder-mikrotjänster), implementera ett API Mesh-lager inom App Builder. Detta konsoliderar olika API:er till en enda, fungerande GraphQL-endpoint som förbrukas av din nya butik eller andra tjänster, vilket förenklar komplex datahämtning.
* **Händelsedriven arkitektur**: Använd Adobe I/O-händelser för att trigga App Builder-åtgärder baserat på händelser som inträffar i din PaaS-instans (till exempel produktuppdateringar, kundregistreringar, ändringar i orderstatus) eller andra anslutna system. Detta främjar asynkron kommunikation, minskar tät koppling och förbättrar systemets motståndskraft.

**Fördel:** Detta steg minskar avsevärt den tekniska skulden kopplad till djupt inbäddade anpassningar, påskyndar dramatiskt övergången till [!DNL Adobe Commerce as a Cloud Service]din Commerce-instans, förbättrar skalbarheten och den oberoende implementeringen av anpassad logik samt främjar snabbare utvecklingscykler för tillägg.

#### &#x200B;2. Införa SaaS-baserade Adobe Commerce-merchandisingtjänster och integrera katalogdata

Detta är en kritisk initial integrationspunkt med två alternativ gällande katalogdatahantering:

>[!BEGINTABS]

>[!TAB Alternativ 1 - Befintlig katalog SaaS-tjänst]

**Utnyttja befintlig Catalog SaaS-tjänst integrerad med PaaS-backend**

Detta alternativ fungerar som ett övergångssteg, byggt på en befintlig integration där din PaaS-backend fyller en befintlig instans av Adobe Commerce SaaS-tjänsten med data från [katalogtjänsten](../../catalog-service/guide-overview.md), [live-sökning](../../live-search/overview.md) och [produktrekommendationer](../../product-recommendations/overview.md).

* **Synkronisering** av katalogdata: Se till att din Adobe Commerce PaaS-instans fortsätter att synkronisera produkt- och katalogdata till din befintliga Adobe Commerce Catalog SaaS-tjänst. Detta bygger vanligtvis på etablerade kontakter eller moduler inom din PaaS-instans. Catalog SaaS-tjänsten är fortfarande den auktoritativa källan för sök- och merchandisingfunktioner, och hämtar sin data från din PaaS-backend.
* **API Mesh för optimering**: Medan den headless storefront (på Edge Delivery Services) och andra tjänster kan konsumera data direkt från Catalog SaaS-tjänsten, rekommenderar Adobe starkt att använda API Mesh (inom App Builder). API Mesh kan förena API:er från Catalog SaaS-tjänsten med andra nödvändiga API:er från din PaaS-backend (till exempel realtidskontroller av inventarier från transaktionsdatabasen eller anpassade produktattribut som inte är fullt replikerade till Catalog SaaS-tjänsten) till en enda, fungerande GraphQL-endpoint. Detta möjliggör också centraliserad cache, autentisering och responstransformation.
* **Integrera Live Search och produktrekommendationer**: Konfigurera SaaS-tjänster för Live-sökning och produktrekommendationer till [att importera katalogdata](https://experienceleague.adobe.com/sv/docs/commerce/live-search/install#configure-the-data) direkt från din befintliga SaaS-tjänst för Adobe Commerce Catalog, som i sin tur fylls i av din AppaS-backend.

**Fördel**: Detta ger en snabbare väg till en headless Store och avancerade SaaS-försäljningsfunktioner genom att utnyttja en befintlig och fungerande Catalog SaaS-tjänst och dess integrering med din PaaS-backend. Den behåller dock beroendet av PaaS-backend för den primära katalogdatakällan och tillhandahåller inte de multikällsaggregationsmöjligheter som är inneboende i den nya Composable Catalog Data Model. Det här alternativet är en giltig språngbräda mot en mer heltäckande sammansättningsbar arkitektur.

>[!TAB Alternativ 2 – Komponerbar katalogdatamodell]

**Anta den nya Composable Catalog Data Model (CCDM)**

Detta är den strategiska, framtidssäkra lösningen för att utnyttja Adobe Commerce Optimizer. CCDM erbjuder en flexibel, skalbar och enhetlig katalogtjänst som är utformad för datagenerering från flera källor och dynamisk marknadsföring.

* **Intag och enhetlighet av data**
   * Börja med att importera produkt- och katalogdata från din befintliga Adobe Commerce PaaS-instans (och/eller andra PIM/ERP-system) till den nya Composable Catalog Data Model (CCDM).
   * Koppla befintliga produktattribut till CCDM:s flexibla schema. Prioritera viktiga produktdata för första intaget.
   * Skapa robusta dataledningar för kontinuerlig synkronisering. Detta kan omfatta:
      * **Händelsestyrd** (via App Builder): Använd Adobe I/O Events från din PaaS-instans för att utlösa offentligt tillgängliga eller anpassade Adobe App Builder-program. Dessa program omvandlar och skickar dataändringar (skapa, uppdatera och ta bort) till CCDM via dess API:er.
      * **Gruppinläsning**: För stora initiala inläsningar eller periodiska massuppdateringar använder du säkra filöverföringar (till exempel CSV eller JSON) till ett mellanlagringsområde som bearbetas av Adobe Experience Platform (AEP)-inmatningstjänster till CCDM.
      * **Direkt API-integrering** (med App Builder-koordinering): För mer komplexa scenarier kan App Builder fungera som ett orkestreringslager, göra direkta API-anrop till din PaaS-backend, omforma data och överföra dem till CCDM.
* **Katalogvy och principdefinition**: Konfigurera katalogvyer (logiska grupperingar för unik katalogpresentation, till exempel butiksvyer, regioner och B2B/B2C-segment) och definiera principer (regeluppsättningar för produktpresentation, filtrering och varuexponering) i CCDM. Detta ger dynamisk kontroll över produktsortiment och visningslogik per katalogvy.
* **Integrera Live Search och produktrekommendationer**: När katalogdata finns i CCDM integrerar du Adobe SaaS-baserade Live Search- och produktrekommendationer-tjänster. Dessa utnyttjar Adobe AI AI och maskininlärningsmodeller för överlägsen sökrelevans och personaliserade rekommendationer, och använder data direkt från CCDM.

**Fördel**: Genom att abstrahera kataloghantering och identifiering i CCDM och tillhörande SaaS-tjänster får du bättre prestanda, AI-drivna försäljningsfunktioner, avlastning av läsåtgärder från din gamla backend-server och en stabil avskalning av den översta funnel-upplevelsen.

>[!ENDTABS]

#### &#x200B;3. Bygg upp din butik på Edge Delivery Services

När man har etablerat och anpassat data och anpassat dem externt blir fokus på att bygga upp en högpresterande frontlinje.

* **Inledande konfiguration**: Konfigurera ditt projekt med Adobe Commerce Storefront-standardmallen för Edge Delivery Services. Detta utgör en grundläggande, headless front som bygger på modern webbteknik.
* **Anslut till katalogtjänster och API-nät**: Commerce Storefront använder data främst via GraphQL API:er:
   * **Alternativ 1**: Från den befintliga katalogtjänsten SaaS (via API Mesh) för produktinformation och försäljningsregler.
   * **Alternativ 2**: Från CCDM för produktinformation och försäljningsregler.
   * Från API Mesh för alla orkestrerade data från din gamla backend-server (PaaS-instans) eller anpassade App Builder-tjänster (t.ex. realtidslager, anpassade produktattribut och lojalitetspunkter).
* **Innehållsmigrering (AEM Services):** Migrera ditt befintliga statiska innehåll (till exempel &quot;Om oss&quot;-sidor, blogginlägg och marknadsföringsbanners) till AEM Services, som driver Commerce Storefront. Utnyttja AEM:s förmåga att skapa innehåll och se till att tillgångarna är optimerade för Edge Delivery Services.
* **Utveckla viktiga gränssnittskomponenter**: Bygg upp viktiga användargränssnittskomponenter för produktinformationssidor (PDP), produktlistningssidor (PLP) och sidor med allmänt innehåll med Edge Delivery Services instickskomponenter och anpassade React/Vue-komponenter. Prioritera centrala handelsflöden.
* **Integrering med befintlig kundvagn/utcheckning**: Till att börja med kommer Edge Delivery Services Store att skapa en leverans till din befintliga Adobe Commerce PaaS (eller någon annan tredjepartsplattform) för kundvagn och utcheckning. Detta innebär vanligtvis följande:
   * **Omdirigering**: Användaren omdirigeras till den gamla plattformens egna kundvagn- och utchecknings-URL:er och nödvändiga sessions- och kundvagnsidentifierare skickas.
   * **Direkt API-interaktion** (med App Builder-orkestrering): Bygga anpassade komponenter för kundvagn och utlåning inom Edge Delivery Services som interagerar direkt med din PaaS-backends kundvagn och utchecknings-API:er. Detta innebär ofta App Builder som en Backend-for-Frontend (BFF) för att orkestrera samtal till flera backend-tjänster (till exempel PaaS-vagn, betalningsgateways och fraktkalkylatorer).

**Fördel**: Levererar en blixtsnabb, SEO-optimerad och mycket flexibel butiksupplevelse. Denna fas bidrar direkt till en överlägsen kundupplevelse och lägger grunden för framtida frontend-innovation.

#### &#x200B;4. Datamigrering (fasad process)

Datamigrering är en kritisk och mångfacetterad process som körs parallellt med refaktorering och utveckling av butiker, vilket säkerställer datakonsistens och integritet.

* **Rensa och optimera befintlig data**: Innan någon storskalig migrering, utför omfattande datarensning, deduplicering och validering på din befintliga PaaS-databas. Detta proaktiva steg är avgörande för att minimera överföringen av äldre data och säkerställa datakvaliteten i den nya miljön.

**Massdatamigreringar**

Massdatamigrering innebär att du tar en fullständig datadump från din Adobe Commerce PaaS-instans, transformerar hela datamängden och importerar den till Adobe Commerce som en molntjänst på en gång. Denna metod används vanligtvis för den initiala populationen av data.

* **Verktygstillgänglighet**: Dedikerat [verktyg för migrering av massdata](./bulk-data.md) för kundanvändning för Commerce massdatamigrering från första part kommer att vara tillgängligt på begäran under första kvartalet 2026. Om kunderna behöver hjälp med att migrera data satsvis på förhand kan Adobe på deras vägnar underlätta dataöverföringen.

* **Process**:
   * **Fullständig dataexport**: Extrahera en fullständig datauppsättning från din Adobe Commerce PaaS-instans (till exempel produkter, kategorier, kundkonton, historiska orderdata, statiska block och sidinnehåll).
   * **Datatransformering**: Använd nödvändiga omformningar för att justera extraherade data efter schemakraven för de nya komponenterna i Adobe Commerce as a Cloud Service, inklusive CCDM (Composable Catalog Data Model) om en sådan används, samt andra relevanta Adobe-tjänster eller -databaser. Detta kan omfatta anpassade skript eller specialiserade datamappningsverktyg.
   * **Inledande import**: Importera den omformade fullständiga datauppsättningen till respektive komponenter i Adobe Commerce as a Cloud Service. För produkt- och kategoridata fylls den valda katalogtjänsten (CCDM eller befintliga katalog-SaaS) i. För kund- och orderdata fylls transaktionsbackend-tjänster eller tillhörande tjänster i.
   * **Validering**: Verifiera importerade data noggrant för att säkerställa fullständighet, exakthet och konsekvens i alla nya system.

**Interaktiv datamigrering**

Interaktiv datamigrering fokuserar på synkronisering av inkrementella ändringar och borttagningar från källinstansen av PaaS till de nya Cloud Service-komponenterna, vilket säkerställer att data uppdateras fram till och efter avslutningen.

* **Verktygstillgänglighet**: Verktyg som är särskilt utformade för iterativ datamigrering kommer att vara tillgängliga under 2026.

* **Process**:
   * **Deltaidentifiering**: Upprätta mekanismer för att identifiera ändringar (skapande, uppdateringar och borttagningar) i viktiga datauppsättningar i din PaaS-miljö sedan den senaste synkroniseringen. Detta kan omfatta registrering av ändringsdata (CDC), tidsstämpeljämförelser eller händelsebaserade utlösare.
   * **Kontinuerlig synkronisering**: Implementera robusta mekanismer för kontinuerlig, inkrementell datasynkronisering från din PaaS-miljö till de nya molntjänstkomponenterna (till exempel CCDM och transaktionell backend). Detta är avgörande för att bibehålla datafärskhet och minimera nedetid under cutover.
   * **Utnyttja händelser**: Använd Adobe I/O-händelser där det är möjligt för att trigga App Builder-åtgärder för realtids- eller nästan realtidsuppdateringar från din PaaS-instans till de nya tjänsterna. Till exempel kan en produktuppdatering i PaaS utlösa en händelse som uppdaterar motsvarande post i CCDM.
   * **API-drivna uppdateringar**: För data som inte är händelsedrivna, använd schemalagda API-anrop (via App Builder eller andra integrationsplattformar) för att hämta ändringar från PaaS och skicka dem till de nya systemen.
   * **Felhantering och övervakning**: Implementera robust felhantering, loggning och övervakning för alla iterativa datapipelines för att säkerställa att dataintegriteten bibehålls under hela processen.

### Eftermigrering och pågående verksamhet

**DNS-reducering och live:**

* Planera noggrant DNS-brytningen med minimala driftavbrott.
* Övervaka webbplatsens hälsa och prestanda direkt efter lanseringen.

**Operationer efter uppskjutning:**

**Demonstrerar PaaS-miljön:**

* Arkivera eller ta bort gamla PaaS-instanser och data säkert efter valideringsperioden.

**Pågående utvecklingsarbetsflöde:**

* Använd den versionslösa typen av [!DNL Adobe Commerce as a Cloud Service], som har kontinuerliga små distributioner i stället för stora uppgraderingar.
* Använd Cloud Manager för att hantera miljöer och driftsättningar.
* Utnyttja App Builder för utökad funktionalitet utan att påverka kärnan.

**Övervakning, prestanda och säkerhet:**

* Övervaka webbplatsens prestanda, fel och säkerhetsloggar kontinuerligt.
* Utnyttja Adobe inbyggda säkerhetsfunktioner och följ vedertagna standarder.

**Utbildning och dokumentation:**

* Utbilda nya utvecklare och affärsanvändare på [!DNL Adobe Commerce as a Cloud Service]-plattformen och i arbetsflödena.
* Underhåll uppdaterad intern dokumentation för anpassade integreringar och processer.
