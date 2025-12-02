---
title: AI-kodningsverktyg för tillägg
description: Lär dig hur du använder AI-verktygen för att skapa Commerce App Builder-tillägg.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: b62dafbf381eb11501c901d6e8d6ad3da972a307
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 0%

---

# AI-kodningsverktyg för tillägg

När du migrerar till [!DNL Adobe Commerce as a Cloud Service] kan du använda AI-kodningsverktygen för att konvertera befintliga [!DNL Adobe Commerce] PHP-tillägg till [!DNL Adobe Developer App Builder] tillägg. Den kan också användas för att skapa nya [!DNL App Builder]-tillägg.

Att använda AI-kodningsverktygen ger följande fördelar:

* **Förbättrat utvecklingsarbetsflöde**: Integrerade Adobe Commerce-utvecklingsverktyg.
* **AI-baserad hjälp**: Kontextmedveten kodgenerering och felsökning.
* **Commerce-specifika funktioner**: Specialiserade verktyg för Adobe Commerce App Builder-utveckling.
* **Automatiska arbetsflöden**: Effektivare utvecklings- och distributionsprocesser.

## Förutsättningar

* Ett av följande kodningsagenter:
   * [Markör](https://cursor.com/download) (rekommenderas)
   * [Github Copilot](https://github.com/features/copilot)
   * [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)
   * [Claude Code](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download): LTS-version
* Pakethanteraren: [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) eller [garn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git): För databaskloning och versionskontroll

## Installation

1. Installera den senaste [Adobe I/O CLI](https://github.com/adobe/aio-cli) globalt:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Installera [Adobe I/O CLI Commerce-plugin](https://github.com/adobe-commerce/aio-cli-plugin-commerce):

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Klona startsatsen för Commerce [integration](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration):

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. Gå till startpaketkatalogen:

   ```bash
   cd commerce-integration-starter-kit
   ```

1. Installera Commerce AI-utökningsverktygen genom att köra det interaktiva installationskommandot:

   ```bash
   aio commerce extensibility tools-setup
   ```

Konfigurationsalternativen visas i installationsprocessen. För installationsplatsen väljer du Aktuell katalog för att installera verktygen på den aktuella arbetsytan:

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

När du väljer kodningsagenten rekommenderar Adobe att du väljer `Cursor` för att få den bästa utvecklingsupplevelsen:

```terminal
? Which coding agent would you like to use?
❯ Cursor
  Copilot
  Gemini CLI
  Claude Code
```

När du väljer pakethanteraren bör du använda `npm` för konsekvens:

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. När kodningsverktygen har installerats konfigureras följande under installationen:

   * MCP-serverintegration för Adobe Commerce-utveckling
   * Markörens IDE-regler för förbättrad utvecklingsupplevelse
   * Commerce-specifika utvecklingsverktyg och arbetsflöden

   Följande filer läggs till på arbetsytan:

   **Markör**

   * MCP-konfiguration: `.cursor/mcp.json`
   * Regelkatalog: `.cursor/rules/`

   **Copilot**

   * MCP-konfiguration: `.vscode/mcp.json`
   * Regelkatalog: `.github/copilot-instructions.md`

>[!NOTE]
>
>Innan du distribuerar ditt projekt måste du utföra följande konfigurationsåtgärder:
>
>* Logga in på [Adobe Developer Console](https://developer.adobe.com/console) med Adobe I/O CLI.
>* Skapa ett App Builder-projekt (se [Projektinställningar](https://developer.adobe.com/commerce/extensibility/events/project-setup)).
>* Konfigurera miljövariabler i en `.env`-fil.
>
>Du kan slutföra dessa konfigurationssteg manuellt eller använda AI-kodningsverktygen för att få hjälp med processen. Mer information finns i [Skapa en integrering](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/).

## Konfiguration efter installation

### Logga in på [!DNL Adobe I/O CLI]

När du har installerat [!DNL Adobe I/O CLI] måste du logga in när du vill använda MCP-servern.

```bash
aio auth login
```

Kör följande kommando för att verifiera att du är inloggad:

```bash
aio where
```

Om du råkar ut för problem provar du med att logga ut och logga in igen:

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>Vissa funktioner i MCP-servern fungerar utan inloggning, men tjänsten RAG (Retrieval-Augmented Generation) fungerar inte. RAG-tjänsten ger AI-kodningsagenten tillgång i realtid till den fullständiga Adobe Commerce-dokumentationsuppsättningen, så att den kan besvara frågor och generera kod baserat på Commerce nuvarande utvecklingsmetoder, API:er och arkitekturmönster.
>
>I en framtida version kommer RAG-tjänsten att vara tillgänglig oberoende av varandra utan att du behöver installera andra verktyg.

### Markör

1. Starta om markörutvecklingsmiljön för att läsa in de nya MCP-verktygen och konfigurationen.

1. Kontrollera installationen genom att bekräfta att reglerna finns i mappen `.cursor/rules/`.

1. Aktivera MCP-servern:

   * Öppna MCP-inställningarna för markören med **Cmd+Skift+P** (macOS) eller **Ctrl+Skift+P** (Windows och Linux).
   * Typ **Visa: Öppna MCP-inställningar**
   * Leta upp **Commerce-extensibility MCP Server** i listan
   * Aktivera kodningsverktygen genom att växla servern **PÅ**

1. Kontrollera serverstatusen - Commerce Extensibility MCP Server ska visas som:

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. Använd följande uppmaning för att se om agenten använder MCP-servern. Om så inte är fallet ber du agenten uttryckligen att använda de tillgängliga MCP-verktygen.

```terminal
What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
```

### Copilot

1. Starta om Visual Studio Code för att läsa in de nya MCP-verktygen och konfigurationen.

1. Kontrollera installationen genom att bekräfta att filen `copilot-instructions.md` finns i mappen `.github`.

1. Aktivera MCP-servern:

   * Öppna panelen Tillägg genom att klicka på ikonen **Tillägg** i aktivitetsfältet till vänster eller genom att använda **Cmd+Skift+X** (macOS) eller **Ctrl+Skift+X** (Windows och Linux).
   * Klicka på **MCP-SERVRAR - INSTALLERADE**.
   * Klicka på kugghjulsikonen bredvid **Commerce-extensibility MCP Server** och välj **Start Server** om servern stoppas.
   * Klicka på kugghjulsikonen igen och välj **Visa utdata**.

1. Kontrollera serverstatusen. `MCP:commerce-extensibility`-utdata ska matcha följande:

   ```terminal
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running
   
   (...)
   
   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. Använd följande uppmaning för att se om agenten använder MCP-servern. Om så inte är fallet ber du agenten uttryckligen att använda de tillgängliga MCP-verktygen.

   ```terminal
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## Exempelfråga

I följande exempelfråga skapas ett tillägg som skickar meddelanden när en beställning placeras.

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## Fråga om kommandon

Förutom att fråga kan du använda kommandot `/search-commerce-docs` för att söka efter dokumentation i konversationer med din agent. Exempel:

```text
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Bästa praxis

Adobe rekommenderar att du följer följande metodtips när du använder AI-kodningsverktygen:

### Checklista

Innan du startar en utvecklingssession:

* Sök efter `REQUIREMENTS.md`
* Kontrollera att MCP-verktygen fungerar
* Granska den aktuella fasen och målen
* Börja med exempelkod eller skräddarsydda projekt

Under utvecklingen:

* Lita på det fyrfasade [protokollet](#protocol)
* Begär implementeringsplaner för komplex utveckling
* Använd MCP-verktyg när de är tillgängliga
* Testa varje funktion efter implementering
* Testa lokalt först, distribuera och testa igen
* Utnyttja kodningsverktygen för att testa stödet
* Onödig komplexitet
* Driftsätt stegvis för snabbare utveckling

När du startar en ny chatt:

* Ge rätt sessionsöverlämning
* Referensnyckelfiler med `@`
* Ange tydliga mål för sessionen
* Använd fasbaserade gränser

### Arbetsflöde

När du utvecklar med AI-kodningsverktygen börjar du med exempelkod eller med skräddarsydda projekt. Med den här metoden kan du bygga på en stabil grund i stället för att börja från ingenting, samtidigt som du optimerar arbetsflödet för AI-utveckling.

På så sätt kan du också utnyttja Adobe mallar och bygga vidare på beprövade mönster och arkitekturer, samtidigt som du behåller etablerade katalogstrukturer och konventioner.

Se följande resurser för att komma igång:

* [Startpaket för integrering](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Adobe Commerce startkit-mallar](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Adobe I/O Events startmallar](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [App Builder exempelprogram](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### Därför bör du använda dessa resurser

* **Beprövade mönster**: Startpaket innehåller Adobe bästa praxis och arkitektoniska beslut
* **Snabbare utveckling**: Minskar tiden för mallplåt och konfiguration
* **Konsekvens**: Ser till att tillägget följer etablerade konventioner
* **Underhållbarhet**: Enklare att underhålla och uppdatera när du följer standardmönster
* **Dokumentation**: Startpaket innehåller exempel och dokumentation
* **Community-stöd**: Det är enklare att få hjälp när du använder standardstrategier
* **AI-kontexteffektivitet**: Använd välbekanta mönster och strukturer för att arbeta med, minska behovet av omfattande förklaringar och förbättra exaktheten vid kodgenerering
* **Minskad tokenanvändning**: Referera till befintliga mönster i stället för att generera allt från början, vilket leder till effektivare konversationer och färre kontextsammanfattningar

### Protokoll

Följande fyrstegsprotokoll tillämpas automatiskt av regelsystemet. Verktygen bör följa detta protokoll automatiskt när tillägg utvecklas:

* Fas 1: Analys och förtydligande av kraven
   * Lämna fullständiga svar när ni får frågan om hur ni ska klargöra frågorna.
* Fas 2: Arkitekturplanering och användargodkännande
   * Granska planen noggrant innan du godkänner den.
* Fas 3: Kodgenerering och implementering
* Fas 4: Dokumentation och validering

### Begär implementeringsplaner för komplex utveckling

För komplex utveckling som innefattar flera runtime-åtgärder, kontaktytor eller integreringar, krävs uttryckligen att AI-verktygen skapar en detaljerad implementeringsplan. När du ser en plan på hög nivå i [fas 2](#protocol) som omfattar flera komponenter ber du om en detaljerad implementeringsplan för att dela upp den i hanterbara uppgifter:

```terminal
Create a detailed implementation plan for this complex development.
```

Komplexa Adobe Commerce-tillägg omfattar ofta:

* Flera körningsåtgärder
* Händelsekonfiguration över flera kontaktytor
* Integrering med externa system
* Krav på statshantering
* Testa i flera komponenter

### Använd MCP-verktyg

>[!NOTE]
>
>Kontrollera att du är [inloggad på Adobe I/O CLI](#log-in-to-the-adobe-io-cli) innan du använder MCP-verktygen.

Som standard används MCP-verktyg, men i vissa fall kan CLI-kommandon användas. Om du vill vara säker på att MCP-verktygen används, begär du dem uttryckligen i uppmaningen.

Om CLI-kommandon används och du vill använda MCP-verktygen i stället, ska du göra så här:

```terminal
Use only MCP tools and not CLI commands
```

* MCP-verktyg: aio-app-deploy, aio-app-dev, aio-dev-invoke
* CLI-kommandon: aio app deployment, aio app dev

CLI-kommandon kan användas för följande scenarier:

* Komplexa driftsättningsscenarier
* Felsöka specifika problem
* När MCP-verktyg har begränsningar
* Engångsoperationer som inte drar nytta av MCP-integrering

### Utveckling

Det är viktigt att ifrågasätta den onödiga komplexitet som skapas av AI-verktygen.

När onödiga filer läggs till (`validator.js`, `transformer.js`, `sender.js`) för enkla skrivskyddade slutpunkter ska du följa följande anvisningar:

```terminal
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### Testning

Använd följande metodtips vid testning:

#### Testa varje funktion efter implementering

När du är klar med utvecklingen av en funktion i din implementeringsplan ska du testa den omedelbart. Tidig testning förhindrar sammansatta problem och gör felsökningen enklare.

* Vänta inte tills alla funktioner har slutförts
* Testa stegvis för att fånga upp problem tidigt
* Validera funktionaliteten innan du går till nästa funktion

#### Testa lokalt först

Testa alltid lokalt först med verktyget `aio-app-dev`. Detta ger omedelbar feedback och möjliggör snabbare iterationscykler, enklare felsökning och inga driftsättningsförluster.

1. Starta lokal utvecklingsserver:

   ```bash
   aio-app-dev
   ```

1. Testa åtgärder lokalt:

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### Distribuera och testa igen

När den lokala testningen har slutförts distribueras och testas den i körningsmiljön. Körningsmiljöer kan ha andra beteenden än lokal utveckling.

1. Distribuera till körningsversion:

   ```bash
   aio-app-deploy
   ```

1. Testa distribuerade åtgärder

1. Använd webbläsare eller direkt HTTP-begäran

1. Kontrollera aktiveringsloggar för felsökning

#### Utnyttja kodningsverktygen för att testa stödet

Be om hjälp med testning. Verktygen kan hjälpa dig med felsökning, logganalys och att skapa lämpliga testdata för specifika körningsåtgärder.

**Testa körningsåtgärder**:

```terminal
Help me test the customer-created runtime action running locally
```

**Felsökning**:

```terminal
Why did the subscription-updated runtime action activation fail?
```

**Kontrollera loggar**:

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Skapa testnyttolaster**:

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**Sök efter körningsslutpunkter**:

```terminal
What's the URL for this deployed action?
```

**Hantera autentisering**:

```terminal
How do I authenticate with this external API?
```

**Felsök**:

```terminal
Help me debug why this action is returning 500 errors
```

### Felsökning

Stoppa och utvärdera när saker och ting går fel. Om du stöter på problem:

* Stoppa och utvärdera - Fortsätt inte i ett brutet läge
* Kontrollera loggar - Använd aktiveringsloggar för att identifiera problem
* Förenkla - Ta bort komplexitet för att isolera problem
* Testa stegvis - Åtgärda ett problem i taget
* Validera - Testa varje korrigering innan du fortsätter

### Distribution

Använd följande metodtips vid distribution:

#### Driftsätt stegvis

Driftsätt endast ändrade åtgärder för att snabba upp utvecklingen. Detta minskar risken för att befintliga funktioner bryts och ger snabbare feedback på ändringar. Det minskar också risken för att befintliga funktioner bryts.

* Använd MCP-verktyg för att distribuera specifika åtgärder

  ```bash
  aio-app-deploy --actions action-name
  ```

* Distribuera enskilda åtgärder efter lokal testning
* Driftsätt stegvis och undvik fullständig driftsättning under utvecklingen

#### Rensning vid körning

Efter större förändringar kan du använda verktygen för att rensa bort överblivna händelser. Med AI-verktygen hanterar man enkelt rensningsprocessen på ett systematiskt sätt och kan effektivt identifiera överblivna åtgärder, verifiera deras status och säkert ta bort dem utan manuell åtgärd.

```terminal
Help me identify and clean up orphaned runtime actions
```

Begär AI-verktygen för att lista distribuerade åtgärder och identifiera oanvända åtgärder

```terminal
List all deployed actions and identify which ones are no longer needed
```

Låt AI-verktygen ta bort överblivna åtgärder med lämpliga kommandon

```terminal
Remove the orphaned actions that are no longer part of the current implementation
```

### Övervakning

Använd följande metodtips när du övervakar programmet:

#### Håll utkik efter sammanhangsbaserade kvalitetsindikatorer

* **Bra kontext**: AI kommer ihåg senaste beslut, refererar till korrekta filer
* **Dålig kontext**: AI frågar efter tidigare tillhandahållen information, upprepar lösta problem

#### Spåra utvecklingshastighet

* **Hög hastighet**: Tydliga framsteg, minimalt klargörande krävs
* **Låg hastighet**: Upprepade förklaringar, AI-förvirring, långsamma förlopp

#### Övervaka kostnadseffektivitet

Spåra användningsmönster för token:

* **Effektiv**: Låg tokenanvändning, få kontextsammanfattningar
* **Ineffektiv**: Hög tokenanvändning, flera sammanfattningar, upprepat arbete

## Vad du ska undvika

Du bör undvika följande mönster när du använder AI-kodningsverktygen:

* **Hoppa inte över klargörandefasen** - Se alltid till att fas 1 slutförs före implementeringen.
* **Hoppa inte över testning efter varje funktion** - Testa stegvis, vänta inte tills allt är klart.
* **Komplexitet behöver inte läggas till utan rotorsaksanalys** - Fråga om onödiga filtillägg och begär en korrekt utredning.
* **Deklarera inte lyckade utan riktig datatestning** - Testa alltid med verkliga data, inte bara kantfall.
* **Glöm inte rensning vid körning** - Rensa alltid bort överblivna åtgärder efter större ändringar.
