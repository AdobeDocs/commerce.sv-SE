---
title: Migrera från sökadapter till PLP-widget
description: Lär dig hur du migrerar från det borttagna sökkortet till  [!DNL Live Search] Sidwidgeten Produktlista.
source-git-commit: 8811f0f271928fbc827e5a0164542da473c57224
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# Migrera från sökadapter till PLP-widget

Sökkortet har [ersatts](release-notes.md#live-search-400) från och med [!DNL Live Search] 4.0.0 och kommer endast att få säkerhetsuppdateringar. Widgeten [Produktlistsida (PLP)](plp-styling.md) är den lösning som stöds för alla [!DNL Live Search] implementeringar framåt. Den här guiden hjälper dig att förstå när migreringen är enkel och när ytterligare arbete krävs.

## Förutsättningar

Kontrollera att miljön uppfyller dessa krav innan du startar migreringsprocessen.

Innan du startar migreringen:

**Tekniska krav**:

- Adobe Commerce 2.4.4 eller senare.
- Tillägget [!DNL Live Search] har installerats.
- Åtkomst till kommandoraden (CLI).
- Tillgång till Commerce Admin.
- Mellanlagringsmiljö eller QA-miljö för testning.

**Säkerhetskopiering och förberedelse**:

1. Säkerhetskopiera databasen och koden.
1. Dokumentera aktuella anpassningar.
1. Gränser och gränser [&#x200B; för att kontrollera att PLP-widgeten uppfyller dina behov.](boundaries-limits.md)
1. Schemalägg migrering under en lågtrafikperiod.
1. Meddela berörda parter om eventuella förändringar i butikens beteende.

**Granska den aktuella implementeringen**:

- Kontrollera din aktuella [!DNL Live Search]-version.
- Dokumentera vilka aspekter som används och deras konfiguration.
- Testa alla sökfunktioner och dokumentera förväntade beteenden.
- Ta skärmdumpar av aktuella sökresultatpresentationer.

**Versionskompatibilitet**:

- Kör Adobe Commerce 2.4.4 eller senare.
- Klar att uppgradera till [!DNL Live Search] 4.0.0 eller senare.

## Migreringsscenarier

### Direktmigrering (inget ytterligare arbete krävs)

Du kan migrera direkt till PLP-widgeten om implementeringen uppfyller ALLA av följande kriterier:

**Lumatabaserad standardbutik**:

- Du använder Luma-temat eller ett tema som ärver från Luma med minimala anpassningar.
- Du har inte gjort anpassade ändringar i PLP-layouter eller -mallar.
- Du har inte skapat anpassade JavaScript-tillägg som interagerar med sökresultaten.

**Standardproduktkatalog**:

- Alla produktattribut använder standardkällmodeller (inte anpassade källmodeller).
- Det finns inga anpassade produkttyper som kräver särskild återgivningslogik.
- Katalogen använder endast standardaspekter och -filtrering.

**Standardintegreringar**:

- Du använder inte Google Tag Manager (GTM) för analys.
- Du använder inte tillägg från tredje part som ändrar sökbeteendet.

Om implementeringen matchar dessa villkor fortsätter du till [Standardmigreringssteg](#standard-migration-steps).

### Migrering som kräver ytterligare arbete

Ytterligare arbete krävs om implementeringen har NÅGOT av följande:

**Anpassade temaändringar**:

- Anpassade PLP-layouter som åsidosätter Luma-mallar.
- Anpassad CSS eller JavaScript som är avsedd för sökkortsspecifika element.
- Anpassade malländringar för PLP eller relaterade filer.
- Temat ärvs inte från Luma (till exempel anpassat tema från början).

**Anpassade produktattribut**:

- Produktattribut med anpassade källmodeller som används som fasetter.
- Anpassade produkttyper med särskilda krav för visning.
- Programmatiska attribut med `"is_user_defined": false`.

**Avancerade integreringar**:

- Google Tag Manager (GTM) används aktivt för spårning.
- Analys- eller personaliseringsverktyg från tredje part som är integrerade med sökfunktionen.
- Anpassad händelsespårning eller datalagerimplementering.
- Integrering med externa sök- och rekommendationsmotorer.

**Headless-implementeringar eller PWA-implementeringar**:

- Använda headless-arkitektur (till exempel PWA Studio, Vue Storefront).
- Anpassat ramverk (React, Vue, Angular).
- Använda GraphQL enbart för katalogfrågor.
- Implementering av anpassade butikshändelser.

**Anpassad widgetkod**:

- Tidigare anpassat sökkortskoden.
- Skapa anpassade versioner av widgetar på ditt eget CDN.
- Anpassade JavaScript-tillägg för sökfunktioner.

Om implementeringen har något av dessa scenarier, se [Komplexa migreringsscenarier](#complex-migration-scenarios).

## Standardmigreringssteg

Följ de här stegen för implementeringar utan särskilda anpassningar:

### Steg 1: Uppgradera [!DNL Live Search]

Uppgradera tillägget [!DNL Live Search] till version 4.0 eller senare för att få tillgång till PLP-widgeten.

**Roll**: Marknadsförare eller partner

1. Kontrollera din aktuella [!DNL Live Search]-version:

   ```bash
   composer show magento/live-search | grep version
   ```

1. Om du använder version 3.x eller tidigare aktiverar du modulen Avancerad sökning innan du uppgraderar:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. Uppdatera `composer.json` så att [!DNL Live Search] 4.0 eller senare krävs:

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. Kör uppgraderingen:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Kör uppgraderingen och kompileringen:

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. Distribuera statiskt innehåll vid behov:

   ```bash
   bin/magento setup:static-content:deploy
   ```

### Steg 2: Aktivera PLP-widgeten

Konfigurera PLP-widgeten i Commerce Admin.

**Role**: Merchant

PLP-widgeten är aktiverad som standard för nya installationer av [!DNL Live Search] 4.0.0+. Om du uppgraderar från en tidigare version:

1. Gå till **[!UICONTROL Stores]** > Inställningar > **[!UICONTROL Configuration]**.
1. Navigera till **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**.
1. Expandera avsnittet **[!UICONTROL Storefront Features]**.
1. Ange **[!UICONTROL Enable Product Listing Widgets]** som **Ja**.
1. Klicka på **[!UICONTROL Save Config]**.
1. Töm cacheminnet: **[!UICONTROL System]** > Verktyg > **[!UICONTROL Cache Management]** > **[!UICONTROL Flush Magento Cache]**.

### Steg 3: Test on staging

Validera migreringen i en icke-produktionsmiljö innan du publicerar.

**Roll**: Marknadsförare/partner

Innan du distribuerar till produktion bör du noggrant testa sökfunktionen:

**Funktionstestning**:

- Kontrollera att sökresultaten visas korrekt.
- Testa alla konfigurerade aspekter.
- Verifiera att kategorinavigering fungerar.
- Testa sidnumrering genom resultaten.
- Kontrollera att sorteringsalternativen fungerar som förväntat.
- Testa tilläggsfunktioner för enkla produkter.

**Visuell testning**:

- Bekräfta att produktbilderna visas korrekt.
- Kontrollera att produktnamnen och priserna återges korrekt.
- Testa färgrutor (om de används).
- Kontrollera responsivt beteende på mobila enheter.
- Verifiera att formateringen matchar ert varumärke.

**Prestandatestning**:

- Mät sidans laddningstider.
- Testa med realistisk katalogstorlek.
- Övervaka resursanvändning för servern.
- Kontrollera om det finns fel i JavaScript i webbläsarkonsolen.

### Steg 4: Distribuera till produktion

Flytta den validerade konfigurationen till din livebutik.

**Roll**: Marknadsförare/partner

1. Schemalägg driftsättning under underhållsperioden om det är möjligt.
1. Följ din standarddistributionsprocess.
1. Aktivera PLP-widgeten i produktion med [Steg 2: Aktivera PLP-widgeten](#step-2-enable-the-plp-widget).
1. Övervaka eventuella problem direkt efter distributionen.
1. Ha en återställningsplan klar om det uppstår allvarliga problem.

### Steg 5: Validera och övervaka

Spåra sökresultat och kundupplevelser efter migreringen.

**Role**: Merchant

Efter driftsättningen kan du övervaka nyckelvärden:

- Sökfrekvens för nollresultat
- Konverteringsgrad för sökning till kundvagn
- Sidinläsningsprestanda
- Kundfeedback eller supportärenden
- JavaScript-fel i webbläsarkonsolen

## Komplexa migreringsscenarier

Följande scenarier kräver ytterligare planering, anpassad utveckling eller specialiserad support utöver de vanliga migreringsstegen.

### Eget tema med layoutändringar

I det här scenariot har du anpassade mallar eller layouter som åsidosätter standardbeteendet för produktlistor.

**Roll**: Utvecklare/partner

1. **Granska anpassningar**:
   - Dokumentera alla anpassade layout-XML-filer i temat.
   - Granska eventuella ändringar av egna mallar på produktlistsidor eller relaterade filer.
   - Identifiera anpassade CSS-klasser som används för formatering.
   - Dokumentera anpassade interaktioner med JavaScript.

1. **Migrera till CSS-baserade anpassningar**:
   - PLP-widgeten använder specifika CSS-klasser (se [PLP-formatguiden](plp-styling.md)).
   - Återskapa visuella anpassningar med hjälp av CSS-klasser för PLP-widget.
   - Testa att anpassade format används korrekt.

1. **Ta bort anpassningar som är i konflikt**:
   - Ta bort layout-XML som ändrar produktlistans struktur.
   - Rensa JavaScript som har specifika sökkortselement som mål.
   - Uppdatera mallåsidosättningar som är i konflikt med widgetåtergivning.

1. **Testa noggrant**:
   - Kontrollera att alla visuella anpassningar fungerar med PLP-widgeten.
   - Se till att inga layoutkonflikter uppstår.
   - Testa över alla brytpunkter och enheter.

### Produktattribut med anpassade källmodeller

I det här scenariot har du ansikten som använder produktattribut med anpassade källmodeller som inte stöds av sökadaptern men stöds av PLP-widgeten.

**Roll**: Merchant (Admin-konfiguration)

1. **Identifiera attribut som påverkas**:
   - Granska produktattribut som används som faktablad.
   - Identifiera vilka som använder anpassade källmodeller.
   - Dokumentera aktuell facet-konfiguration.

1. **Uppgradera och aktivera PLP-widgeten**:
   - Följ [Standardmigreringssteg](#standard-migration-steps).
   - PLP-widgeten har stöd för anpassade källmodellattribut.

1. **Konfigurera om ansikten**:
   - Gå till **[!UICONTROL Marketing]** > SEO &amp; Search > **[!UICONTROL Live Search]**.
   - Granska ansiktskonfigurationen för de attribut som påverkas.
   - Testmetoderna fungerar korrekt med anpassade källmodeller.

1. **Validera**:
   - Testa filtrering med anpassade källmodellaspekter.
   - Kontrollera att alla attributvärden visas korrekt.
   - Se till att prestanda är godtagbara.

### Integrering med Google Tag Manager (GTM)

I det här scenariot finns det ett känt fel där aktivering av PLP-widgeten kan göra att GTM misslyckas.

**Roll**: Utvecklare/partner + kundkonstruktion

**Alternativ 1: Fortsätt med sökkortet (endast temporärt)**

- Låt sökkortet vara aktiverat om GTM är affärskritiskt.
- Förstå att du bara får säkerhetsuppdateringar.
- Planera att migrera när GTM-kompatibiliteten är löst.
- Kontakta Adobe Support för att få uppdateringar om GTM-kompatibilitet.

**Alternativ 2: Migrera GTM-spårning till en alternativ metod**

1. **Implementera en anpassad händelsesamling**:

   - Använd [StoreFront Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/).
   - Samla in sök- och produktinteraktionshändelser.
   - Skicka händelser till GTM-datalagret manuellt.

1. **Slutför följande steg**:

   - Granska aktuella GTM-spårningskrav.
   - Mappa GTM-händelser till Store-händelser.
   - Implementera anpassade händelseavlyssnare.
   - Testa dataflödet till GTM.
   - Validera analysrapporter.

**Alternativ 3: Ersätt GTM med Adobe Analytics**

- Överväg att migrera till [Adobe Analytics](https://business.adobe.com/products/adobe-analytics.html) om det är tillämpligt.
- Kontakta kundkonstruktionsavdelningen för vägledning.

**Vem du ska kontakta**: Skicka in en supportanmälan för GTM-kompatibilitetsuppdateringar eller kundteknisk hjälp.

### Scenario: Headless eller PWA

I det här scenariot har du ett headless-gränssnitt eller en PWA-butik som kräver anpassad händelsesamling och som inte kan använda standardgränssnittet för PLP-widgeten.

**Roll**: Utvecklare/partner

1. **Granska referensimplementeringar**:
   - Studera källkoden för [PLP-widgeten](https://github.com/adobe/storefront-product-listing-page).
   - Granska API-dokumentation för [[!DNL Live Search] GraphQL](graphql.md).
   - Förstå [katalogtjänstfrågorna](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).

1. **Implementera ett anpassat användargränssnitt**:
   - Använd [!DNL Live Search] GraphQL API för frågor.
   - Bygg anpassade produktlistekomponenter.
   - Implementera användargränssnittet för faceting.
   - Hantera sidnumrering och sortering.

1. **Implementera händelsesamling**:
   - Granska dokumentationen för [StoreFront Events](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search).
   - Implementera nödvändiga händelser:
      - `search-request-sent`
      - `search-response-received`
      - `search-results-view`
      - `product-page-view`
      - `add-to-cart`
   - Testa händelsedataflöden till Adobe Commerce.

1. **Konfigurera facet-sortering**:
   - För headless-implementationer kan facets sorteras efter antal.
   - Konfigurera i arbetsytan **[!UICONTROL Live Search]** > **[!UICONTROL Facets]**.
   - Ange **[!UICONTROL Sort Type]** som **Antal** för bättre användargränssnitt.

1. **Testa och validera**:
   - Verifiera sökresultatens exakthet.
   - Testa ansiktsfunktioner.
   - Bekräfta att händelser spåras korrekt.
   - Övervaka prestandamått.
   - Validera smarta marknadsföringsfunktioner.

### Scenario: Anpassade kodändringar för widget

I det här scenariot har du tidigare anpassat sökadapterkoden eller widgetkoden och behöver migrera anpassningar.

**Roll**: Utvecklare/partner

1. **Dokumentera befintliga anpassningar**:
   - Visa alla anpassningar som gjorts i sökadaptern.
   - Identifiera de affärskrav som driver varje anpassning.
   - Kontrollera om anpassningar fortfarande behövs.

1. **Kontrollera om de inbyggda funktionerna uppfyller dina behov**:
   - Granska [PLP-widgetfunktioner](plp-styling.md#widget-features).
   - Kontrollera om CSS-baserad anpassning är tillräcklig.
   - Testa standardbeteendet för PLP-widget.

1. **Om anpassad kod fortfarande behövs**:
   - Klona [PLP-widgetdatabasen](https://github.com/adobe/storefront-product-listing-page).
   - Implementera dina anpassningar.
   - Använd ditt eget CDN.
   - Uppdatera Commerce-konfigurationen så att du kan använda din anpassade widget.

   >[!WARNING]
   >
   >Om du anpassar PLP-widgeten med kod från databasen ansvarar du för underhåll och uppdateringar. Nya PLP-widgetfunktioner från Adobe kan vara inkompatibla med dina anpassningar.

1. **Testa noggrant**:
   - Testa alla anpassade funktioner.
   - Kontrollera att Commerce-uppdateringar inte bryter anpassningen.
   - Dokumentera er anpassade implementering.
   - Planera för löpande underhåll.

## Kända begränsningar och kanter

Tänk på följande begränsningar när du migrerar:

**PLP-widgetbegränsningar**:

- **Sorteringsordningsriktning**: När PLP-widgeten är aktiverad går det inte att ändra sorteringsordningen på produktlistsidor (stigande/fallande).
- **Lägg till i kundvagn**: Knapparna Lägg till i kundvagn är bara tillgängliga för enkla produkter i widgeten.
- **Nivåpriser**: Stöds inte i PLP-widgeten.
- **Momsvisning**: Priserna inkluderar moms, men moms kan inte visas som ett separat värde.

**Skillnader i funktioner jämfört med sökadapter**:

- **Färgrutor**: Attributet `color` måste stavas exakt som `color` (inte &quot;color&quot; eller egna namn) för att färgrutorna ska fungera korrekt.
- **Temastalling**: Anpassade temaklasser ärvs inte av widgeten; måste vara målinriktade för widgetspecifika CSS-klasser.
- **Anpassade produkttyper**: Stöds inte i widgeten.

**Prestandaöverväganden**:

- Stora kataloger (fler än 50 000 produkter) kan få längre inledande sidinläsning.
- Flera aspekter med många värden kan påverka prestandan.
- Prestanda för mobila enheter kan variera beroende på katalogstorlek.

**Kompatibilitetsproblem**:

- Google Tag Manager-kompatibilitetsproblem (se [GTM-scenario](#google-tag-manager-gtm-integration)).
- Vissa tillägg från tredje part kan hamna i konflikt med PLP-widgeten.
- Anpassade utcheckningstillägg kan behöva uppdateras.

## Få hjälp

Kontakta lämplig resurs baserat på dina specifika behov.

**Adobe Support** kan hjälpa dig med:

- Migreringsprocedurer för Live Search
- Konfigurationsproblem för PLP-widget
- Problem med begränsnings- eller attributindexering
- Prestandaproblem med standardimplementeringar
- Uppgraderingsfel

**Utvecklingspartners/systemintegratörer** bör kontaktas för:

- Anpassade temaändringar
- Implementering av anpassad widgetkod
- Kompatibilitet med tillägg från tredje part
- Headless- eller PWA-implementeringar
- Anpassad händelsespårning

Om du vill kontakta Adobe Support läser du [användarhandboken för hjälpcentret](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

## Vanliga frågor

Hitta svar på vanliga frågor om migrering från sökadaptern till PLP-widgeten.

**F: Kommer sökadaptern att få felkorrigeringar eller funktionsuppdateringar?**

S: Nej. Sökkortet är inaktuellt och kommer endast att få säkerhetsuppdateringar. Felkorrigeringar, prestandaförbättringar och nya funktioner är bara tillgängliga i PLP-widgeten. Om du stöter på problem med sökadaptern är migrering till PLP-widgeten den rekommenderade lösningen.

**F: Kommer migreringen att störa min butik?**

S: Om du följer rätt testprocedurer i mellanlagring bör migreringen vara sömlös. Ha en återställningsplan klar för driftsättning.

**F: Hur lång tid tar migreringen?**

S: För standardimplementeringar: 1-2 timmar. För anpassade implementeringar: 1-4 veckor beroende på komplexitet.

**F: Fungerar mina regler för sökmarknadsföring fortfarande?**

S: Ja, alla regler för sökmarknadsföring, synonymer och facets som konfigurerats på arbetsytan [!DNL Live Search] fortsätter att fungera med PLP-widgeten.

**F: Måste jag konfigurera om mina ansikten?**

S: Normalt nej, men om du var begränsad av anpassade källmodellattribut med sökadaptern kan du nu använda dem med PLP-widgeten.

**Q: Vad gäller för min anpassade CSS?**

S: Du måste uppdatera CSS för att kunna rikta in dig på klasserna för PLP-widgeten. Se [CSS-klassreferensen](plp-styling.md#css-classes).

**F: Kommer detta att påverka min sökningsprestanda?**

S: PLP-widgeten är utformad för att vara performant. De flesta handlare ser lika bra eller bättre resultat. Stora kataloger bör testas i mellanlagring.
