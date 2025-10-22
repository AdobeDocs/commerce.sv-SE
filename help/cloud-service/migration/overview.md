---
title: Migrera till  [!DNL Adobe Commerce as a Cloud Service]
description: Lär dig hur du migrerar till  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
role: Developer
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 0%

---

# Migrera till [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] innehåller en omfattande guide för utvecklare som övergår från en befintlig Adobe Commerce PaaS-implementering till det nya SaaS-erbjudandet (Adobe Commerce as a Cloud Service). Adobe Commerce as a Cloud Service innebär en betydande övergång till en helt hanterad, versionslös SaaS-modell med förbättrade prestanda, skalbarhet, förenklad drift och bättre integrering med hela Adobe Experience Cloud.

>[!NOTE]
>
>Mer information om migreringsverktyg finns i [Migreringsverktyget för massdata](./bulk-data.md).

## Förstå skiftet - jämför PaaS och SaaS

**Viktiga skillnader**

* [!BADGE PaaS endast]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."} **PaaS (aktuell)**: Merchant hanterar programkod, uppgraderingar, patchering och infrastrukturkonfiguration i Adobe värdmiljö. [Delad ansvarsmodell](https://experienceleague.adobe.com/sv/docs/commerce-operations/security-and-compliance/shared-responsibility) för tjänster (MySQL, Elasticsearch med flera).
* [!BADGE SaaS endast]{type=Positive url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."} **SaaS (ny - [!DNL Adobe Commerce as a Cloud Service])**: Adobe hanterar kärnprogrammet, infrastrukturen och uppdateringarna fullt ut. Handläggarna fokuserar på anpassning via utökningspunkter (API:er, App Builder, UI SDK:er). Programkoden är låst.

**Arkitekturkonsekvenser**

* **Versionslös plattform**: Kontinuerliga uppdateringar innebär inga fler större versionsuppgraderingar för kärnan.
* **Mikrotjänster och API-first**: Djupt beroende av API:er för utbyggbarhet och integrering.
* **Headless som standard (valfritt)**: Starkt stöd för fristående butiker (till exempel Commerce Storefront från Edge Delivery Services).
* **Edge Delivery Services**: Påverkar frontendens prestanda och distribution.

**Nya verktyg och koncept**

* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) och [API-nät för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE)
* Självbetjäning med [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Migreringssökvägar

[!DNL Adobe Commerce as a Cloud Service] har stöd för flera migreringssökvägar, beroende på tidslinjen, butiken och anpassningar.

Som ett alternativ till en fullständig migrering stöder [!DNL Adobe Commerce as a Cloud Service] en stegvis migrering med Commerce Optimizer eller en stegvis metod.

* **Inkrementell migrering** - Det här tillvägagångssättet innebär att migrera data, anpassningar och integreringar stegvis. Den här metoden är idealisk för stora handlare med många anpassningar som gradvis vill övergå sina komplexa anpassningar och data till [!DNL Adobe Commerce as a Cloud Service] i sin egen takt.

![inkrementell migrering](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** - Med den här metoden kan du migrera iterativt genom att använda Commerce Optimizer som en övergångsfas för att flytta komplexa anpassningar och data till [!DNL Adobe Commerce as a Cloud Service] i din egen takt. Commerce Optimizer ger tillgång till Merchandising Services som drivs av Catalog Views and Policies, Commerce Storefront från Edge Delivery samt produktvisualer från AEM Assets.

![iterativ migrering](../assets/optimizer.png){width="600" zoomable="yes"}

* **Fullständig migrering** - Detta innebär att migrera alla data, anpassningar och integreringar samtidigt. Den här metoden är perfekt för mindre handlare med få anpassningar som snabbt vill övergå till [!DNL Adobe Commerce as a Cloud Service].

I följande tabell visas en översikt över migreringsprocessen för olika butiker och konfigurationer:

|                    | LUMA Storefront | PWA Storefront | Commerce Storefront med Edge Delivery i botten | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Datamigrering | Obligatoriskt | Obligatoriskt | Obligatoriskt | Obligatoriskt |
| Storefront | Migrera till Commerce Storefront från Edge Delivery | Migrera till Commerce Storefront från Edge Delivery eller underhåll | Ingen effekt | Ingen effekt |
| API-nät | Skapa nytt nät | Skapa nytt nät eller konfigurera om befintligt nät | Skapa nytt nät eller konfigurera om befintligt nät | Skapa nytt nät eller konfigurera om befintligt nät |
| Integreringar | Utnyttja integreringens startpaket | Utnyttja integreringens startpaket | Utnyttja integreringens startpaket | Utnyttja integreringens startpaket |
| Anpassningar | Flytta till App Builder &amp; API Mesh | Flytta till App Builder &amp; API Mesh | Flytta till App Builder &amp; API Mesh | Flytta till App Builder &amp; API Mesh |
| Assets Management | Migrering krävs vid användning av OOTB | Migrering krävs vid användning av OOTB | Migrering krävs vid användning av OOTB | Migrering krävs vid användning av OOTB |
| Tillägg | Migrera till App Builder | Migrera till App Builder | Migrera till App Builder | Migrera till App Builder |

Som framgår av tabellen kommer åtgärderna för varje migrering att bestå av:

* **Datamigrering** - Använder det tillhandahållna [migreringsverktyget](./bulk-data.md) för att migrera data från din befintliga instans till [!DNL Adobe Commerce as a Cloud Service].
* **Storefront** - Befintliga Commerce Storefront med Edge Delivery-teknik och headless-butiker kräver inte reducering, men Luma-butiker kräver migrering till Commerce Storefront med Edge Delivery. PWA Studio butiker kan migreras till Commerce Storefront från Edge Delivery eller underhållas i sitt nuvarande skick. Adobe kommer att tillhandahålla acceleratorer för att underlätta migrering av butiker.
* **[API-nät](https://developer.adobe.com/graphql-mesh-gateway)** - Skapa ett nytt nät eller ändra det befintliga. Adobe kommer att tillhandahålla förkonfigurerade nät som hjälp i den här processen.
* **Integrationer** - Alla integreringar måste utnyttja antingen [startsatsen för integrering](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) eller [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/).
* **Anpassningar** - Alla anpassningar måste flyttas till App Builder och API Mesh.
* **Assets Management** - All resurshantering kräver migrering. Om du redan använder AEM Assets behöver du inte migrera.
* **Tillägg** - Alla pågående tillägg måste återskapas som obearbetade tillägg. I slutet av 2025 kommer Adobe att ge åtkomst till våra populäraste tillägg för att minimera byggtider.

## Migreringsfaser

I följande faser beskrivs de steg och överväganden som krävs för att migrera till [!DNL Adobe Commerce as a Cloud Service].

### Utvärdering och planering före migrationen

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
* **Identifiera viktiga affärsprocesser:** Prioritera funktioner som måste migreras först, till exempel:
   * Komplexa prisregler
   * Anpassade affärsregler som tillämpas innan en order officiellt läggs eller bearbetas
   * Komplexa skatteberäkningar
   * Adressvalideringar
   * Anpassad logik som utlöses efter att en order har placerats
* **Headless vs. monolitisk storefront:** Beslutspunkt för ny storefront-utveckling eller anpassning av befintliga storefront.
* **Integrationsstrategi:** Avgör hur befintliga integreringar omformas (API-nät, App Builder, direkt API).
* **Datamigreringsstrategi:** Kontrollera om du tänker migrera med fullständiga historiska data, partiella data eller inga migrerade data.

**Teamberedskap och utbildning:**

* Bekanta dig med [!DNL Adobe Commerce as a Cloud Service] koncept, utvecklingsarbetsflöden och nya verktyg.
* Delta i praktisk utbildning med Adobe App Builder, Edge Delivery Services och [!DNL Adobe Commerce as a Cloud Service]-distributionskanaler.

**Miljöinställningar och etablering:**

* Etablera din [!DNL Adobe Commerce as a Cloud Service]-sandlåda och dina utvecklingsmiljöer med Commerce Cloud Manager.

### Inkrementella migreringsfaser

**Strategisk omfaktorisering och externalisering**

Den här fasen består av kärnan i migreringen, med fokus på att anpassa kodbasen till det [!DNL Adobe Commerce as a Cloud Service]-molnbaserade paradigmet. Detta innebär att strategiskt implementera nya Adobe-tjänster och flytta bort anpassad logik från Commerce kärnplattform.

#### &#x200B;1. Migrera&quot;pågående&quot; anpassningar och tillägg till App Builder

Detta är en avgörande fas för att uppnå en&quot;låst kärna&quot; och framtidssäkra din lösning, som är central för arkitekturfilosofin i [!DNL Adobe Commerce as a Cloud Service].

* **Gör komplex logik externt för App Builder**: Analysera befintliga anpassade moduler och tredjepartstillägg i din PaaS-kodbas. För komplex affärslogik, skräddarsydda integreringar eller mikrotjänster som inte kräver direkt bearbetning av Commerce-datorns kärndatamodell kan de omfaktoriseras och användas på nytt som serverlösa program i Adobe Developer App Builder.
* **Utnyttja API-nät**: För scenarier som kräver data från flera backend-system (t.ex. din Commerce-backend, ERP, CRM och anpassade App Builder-mikrotjänster) ska du implementera ett API-nätlager i App Builder. Detta konsoliderar olika API:er till en enda, högpresterande GraphQL-slutpunkt som används av din nya butik eller andra tjänster, vilket förenklar komplex datainhämtning.
* **Händelsedriven arkitektur**: Använd Adobe I/O Events för att utlösa App Builder-åtgärder baserat på händelser som inträffar i din PaaS-instans (t.ex. produktuppdateringar, kundregistreringar, orderstatusändringar) eller andra anslutna system. Detta främjar asynkron kommunikation, minskar åtkopplingen och förbättrar systemets motståndskraft.

**Fördelar**: Det här steget minskar den tekniska skuld som är kopplad till djupt inbäddade anpassningar, snabbar upp övergången av din Commerce-instans till [!DNL Adobe Commerce as a Cloud Service] dramatiskt, förbättrar skalbarheten och den oberoende driftsättningen av anpassad logik samt främjar snabbare utvecklingscykler för tillägg.

#### &#x200B;2. Adobe SaaS-baserade Adobe Commerce marknadsföringstjänster och integrera katalogdata

Detta är en viktig inledande integrationspunkt med två alternativ för katalogdatahantering:

>[!BEGINTABS]

>[!TAB Alternativ 1 - Befintlig SaaS-tjänst för katalog]

**Utnyttja den befintliga SaaS-tjänsten för katalog som är integrerad med PaaS-serverdelen**

Det här alternativet är ett övergångssteg som bygger på en befintlig integrering där din PaaS-server fyller i en befintlig instans av Adobe Commerce SaaS-tjänsten med data från [katalogtjänsten](../../catalog-service/guide-overview.md), [direktsökning](../../live-search/overview.md) och [produktrekommendationer](../../product-recommendations/overview.md).

* **Synkronisering av katalogdata**: Kontrollera att din Adobe Commerce PaaS-instans fortsätter att synkronisera produkt- och katalogdata med din befintliga Adobe Commerce Catalog SaaS-tjänst. Detta är vanligtvis beroende av etablerade anslutningar eller moduler i din PaaS-instans. Catalog SaaS-tjänsten är fortfarande den auktoritativa källan för sök- och säljfunktioner och hämtar data från din PaaS-server.
* **API-nät för optimering**: Även om den headless storefront (på Edge Delivery Services) och andra tjänster kan förbruka data direkt från Catalog SaaS-tjänsten rekommenderar Adobe att du använder API Mesh (i App Builder). API Mesh kan kombinera API:er från Catalog SaaS-tjänsten med andra nödvändiga API:er från din PaaS-backend (t.ex. inventeringskontroller i realtid från transaktionsdatabasen eller anpassade produktattribut som inte helt replikerats till Catalog SaaS-tjänsten) till en enda högpresterande GraphQL-slutpunkt. Detta möjliggör även centraliserad cachelagring, autentisering och svarsomvandling.
* **Integrera Live Search och produktrekommendationer**: Konfigurera SaaS-tjänster för Live-sökning och produktrekommendationer till [att importera katalogdata](https://experienceleague.adobe.com/sv/docs/commerce/live-search/install#configure-the-data) direkt från din befintliga SaaS-tjänst för Adobe Commerce Catalog, som i sin tur fylls i av din AppaS-backend.

**Fördel**: Detta ger en snabbare väg till en headless Store och avancerade SaaS-försäljningsfunktioner genom att utnyttja en befintlig och fungerande Catalog SaaS-tjänst och dess integrering med din PaaS-backend. Den behåller emellertid beroendet av PaaS-serverdelen för den primära katalogdatakällan och tillhandahåller inte de sammanställningsfunktioner för flera källor som är inbyggda i den nya sammanställningsbara katalogdatamodellen. Det här alternativet är en giltig språngbräda mot en mer heltäckande sammansättningsbar arkitektur.

>[!TAB Alternativ 2 - Sammanställningsbar katalogdatamodell]

**Använd den nya CCDM-modellen (Composable Catalog Data Model)**

Detta är den strategiska, framtidssäkra lösningen för att utnyttja Adobe Commerce Optimizer. CCDM erbjuder en flexibel, skalbar och enhetlig katalogtjänst som är utformad för datagenerering från flera källor och dynamisk marknadsföring.

* **Intag och enhetlighet av data**
   * Börja med att importera produkt- och katalogdata från din befintliga Adobe Commerce PaaS-instans (och/eller andra PIM/ERP-system) till den nya Composable Catalog Data Model (CCDM).
   * Koppla befintliga produktattribut till CCDM:s flexibla schema. Prioritera viktiga produktdata för första intaget.
   * Skapa robusta dataledningar för kontinuerlig synkronisering. Detta kan omfatta:
      * **Händelsestyrd** (via App Builder): Använd Adobe I/O Events från din PaaS-instans för att utlösa offentligt tillgängliga eller anpassade Adobe App Builder-program. Dessa program omvandlar och skickar dataändringar (skapa, uppdatera och ta bort) till CCDM via dess API:er.
      * **Gruppinläsning**: För stora initiala inläsningar eller periodiska massuppdateringar använder du säkra filöverföringar (till exempel CSV eller JSON) till ett mellanlagringsområde som bearbetas av Adobe Experience Platform (AEP)-inmatningstjänster till CCDM.
      * **Direkt API-integrering** (med App Builder-koordinering): För mer komplexa scenarier kan App Builder fungera som ett orkestreringslager, göra direkta API-anrop till din PaaS-backend, omforma data och överföra dem till CCDM.
* **Katalogvy och principdefinition**: Konfigurera katalogvyer (logiska grupperingar för unik katalogpresentation, till exempel butiksvyer, regioner och B2B/B2C-segment) och definiera principer (regeluppsättningar för produktpresentation, filtrering och varuexponering) i CCDM. Detta ger dynamisk kontroll över produktsortiment och visningslogik per katalogvy.
* **Integrera Live Search och produktrekommendationer**: När katalogdata finns i CCDM integrerar du Adobe SaaS-baserade Live Search- och produktrekommendationer-tjänster. Dessa utnyttjar Adobe Sensei AI och maskininlärningsmodeller för överlägsen sökrelevans och personaliserade rekommendationer, och använder data direkt från CCDM.

**Fördel**: Genom att abstrahera kataloghantering och identifiering i CCDM och tillhörande SaaS-tjänster får du bättre prestanda, AI-drivna försäljningsfunktioner, avlastning av läsåtgärder från din gamla backend-server och en robust avskalning av den avancerade upplevelsen.

>[!ENDTABS]

#### &#x200B;3. Bygg upp din butik på Edge Delivery Services

När man har etablerat och anpassat data och anpassat dem externt blir fokus på att bygga upp en högpresterande frontlinje.

* **Inledande konfiguration**: Konfigurera ditt projekt med Adobe Commerce Storefront-standardmallen för Edge Delivery Services. Detta utgör en grundläggande, headless front som bygger på modern webbteknik.
* **Anslut till katalogtjänster och API-nät**: Commerce Storefront använder data främst via GraphQL API:er:
   * **Alternativ 1**: Från den befintliga katalogtjänsten SaaS (via API Mesh) för produktinformation och försäljningsregler.
   * **Alternativ 2**: Från CCDM för produktinformation och försäljningsregler.
   * Från API Mesh för alla orkestrerade data från din gamla backend-server (PaaS-instans) eller anpassade App Builder-tjänster (t.ex. realtidslager, anpassade produktattribut och lojalitetspunkter).
* **Innehållsmigrering (AEM Services)**: Migrera befintligt statiskt innehåll (till exempel&quot;Om oss&quot;-sidor, blogginlägg och marknadsföringsbanners) till AEM Services, som driver Commerce Storefront. Utnyttja AEM funktioner för framtagning av material och se till att materialet är optimerat för Edge Delivery Services.
* **Utveckla viktiga gränssnittskomponenter**: Bygg upp viktiga användargränssnittskomponenter för produktinformationssidor (PDP), produktlistningssidor (PLP) och sidor med allmänt innehåll med Edge Delivery Services instickskomponenter och anpassade React/Vue-komponenter. Prioritera centrala handelsflöden.
* **Integrering med befintlig kundvagn/utcheckning**: Till att börja med kommer Edge Delivery Services Store att skapa en leverans till din befintliga Adobe Commerce PaaS (eller någon annan tredjepartsplattform) för kundvagn och utcheckning. Detta innebär vanligtvis följande:
   * **Omdirigering**: Användaren omdirigeras till den gamla plattformens egna kundvagn- och utchecknings-URL:er och nödvändiga sessions- och kundvagnsidentifierare skickas.
   * **Direkt API-interaktion** (med App Builder orchestration): Skapa anpassade gränssnittskomponenter för kundvagn och utcheckning i Edge Delivery Services som interagerar direkt med kundvagn- och utchecknings-API:erna för din PaaS-backend. Detta inbegriper ofta App Builder som en BFF (Backend-for-Front end) för att samordna samtal till flera backend-tjänster (till exempel PaaS-kundvagn, betalningsgateways och leveransräknare).

**Fördelar**: Levererar en blixtsnabb SEO-optimerad och mycket flexibel butiksupplevelse. Denna fas bidrar direkt till en överlägsen kundupplevelse och lägger grunden till framtida innovation.

#### &#x200B;4. Datamigrering (stegvis process)

Datamigrering är en kritisk och mångfacetterad process som körs samtidigt med omfaktorisering och utveckling av butiker, vilket ger enhetlighet och integritet.

* **Rensa och optimera befintliga data**: Utför omfattande datarensning, borttagning av dubbletter och validering på din befintliga PaaS-databas innan du genomför en migrering i stor skala. Detta proaktiva steg är avgörande för att minimera överföringen av gamla dataproblem och säkerställa kvaliteten på data i den nya miljön.

**Massdatamigreringar**

Migrering av massdata innebär att du måste ta en fullständig datdump från Adobe Commerce PaaS-instansen, omvandla hela datauppsättningen och importera den till Adobe Commerce as a Cloud Service på en gång. Den här metoden används vanligtvis för den initiala datapifieringen.

* **Verktygstillgänglighet**: Dedikerat [verktyg för massdatamigrering](./bulk-data.md) för kundanvändning för Commerce massdatamigrering från första part kommer att vara tillgängligt på begäran i mitten av juli 2025. Om kunderna behöver hjälp med att migrera data satsvis på förhand kan Adobe på deras vägnar underlätta dataöverföringen.

* **Process**:
   * **Fullständig dataexport**: Extrahera en fullständig datauppsättning från din Adobe Commerce PaaS-instans (till exempel produkter, kategorier, kundkonton, historiska orderdata, statiska block och sidinnehåll).
   * **Datatransformering**: Använd nödvändiga omformningar för att justera extraherade data efter schemakraven för de nya komponenterna i Adobe Commerce as a Cloud Service, inklusive CCDM (Composable Catalog Data Model) om en sådan används, samt andra relevanta Adobe-tjänster eller -databaser. Detta kan omfatta anpassade skript eller specialiserade datamappningsverktyg.
   * **Inledande import**: Importera den omformade fullständiga datauppsättningen till respektive komponenter i Adobe Commerce as a Cloud Service. För produkt- och kategoridata fylls den valda katalogtjänsten (CCDM eller befintliga katalog-SaaS) i. För kund- och orderdata fylls transaktionsbackend-tjänster eller tillhörande tjänster i.
   * **Validering**: Verifiera importerade data noggrant för att säkerställa fullständighet, exakthet och konsekvens i alla nya system.

**Interaktiv datamigrering**

Interaktiv datamigrering fokuserar på synkronisering av inkrementella ändringar och borttagningar från källinstansen av PaaS till de nya Cloud Service-komponenterna, vilket säkerställer att data uppdateras fram till och efter avslutningen.

* **Verktygstillgänglighet**: Verktyg som är särskilt utformade för iterativ datamigrering kommer att vara tillgängliga under andra halvåret 2025.

* **Process**:
   * **Deltaidentifiering**: Upprätta mekanismer för att identifiera ändringar (skapande, uppdateringar och borttagningar) i viktiga datauppsättningar i din PaaS-miljö sedan den senaste synkroniseringen. Detta kan omfatta registrering av ändringsdata (CDC), tidsstämpeljämförelser eller händelsebaserade utlösare.
   * **Kontinuerlig synkronisering**: Implementera robusta mekanismer för kontinuerlig, inkrementell datasynkronisering från din PaaS-miljö till de nya Cloud Service-komponenterna (till exempel CCDM och transaktionell backend). Detta är avgörande för att upprätthålla datans aktualitet och minimera driftstoppen under en övergång.
   * **Utnyttja händelser**: Använd Adobe I/O Events där det är möjligt för att aktivera App Builder-åtgärder för realtidsuppdateringar eller nästan realtidsuppdateringar från din PaaS-instans till de nya tjänsterna. En produktuppdatering i PaaS kan till exempel utlösa en händelse som uppdaterar motsvarande post i CCDM.
   * **API-drivna uppdateringar**: För data som inte är händelsestyrda använder du schemalagda API-anrop (via App Builder eller andra integrationsplattformar) för att hämta ändringar från PaaS och överföra dem till de nya systemen.
   * **Felhantering och övervakning**: Implementera robust felhantering, loggning och övervakning för alla iterativa dataledningar för att säkerställa att dataintegriteten upprätthålls under hela processen.

### Eftermigrering och pågående verksamhet

**DNS-reducering och live:**

* Planera noggrant DNS-brytningen med minimala driftavbrott.
* Övervaka webbplatsens hälsa och prestanda direkt efter lanseringen.

**Åtgärder efter start:**

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
