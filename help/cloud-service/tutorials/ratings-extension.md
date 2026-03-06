---
title: Självstudiekurs om klassificeringstillägg
description: Lär dig hur du bygger ett produktklassificeringstillägg för Adobe Commerce as a Cloud Service med hjälp av App Builder och AI-stödda utvecklingsverktyg.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 33ba97fd6766c9d11baea74170a7119d72e06379
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 0%

---

# Självstudiekurs om klassificeringstillägg

Den här självstudiekursen vägleder dig genom att skapa ett produktklassificeringstillägg för [!DNL Adobe Commerce as a Cloud Service] med [!DNL Adobe App Builder] och AI-stödda utvecklingsverktyg.

Innan du börjar slutför du [förutsättningarna](./tutorial-prerequisites.md).

## Verifiera krav

Kontrollera att följande krav är installerade:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

Om något av de föregående kommandona inte returnerar det förväntade resultatet kan du få hjälp i [kravavsnitten](./tutorial-prerequisites.md).

## Tilläggsutveckling

I det här avsnittet får du hjälp med att utveckla ett klassificeringstillägg för Adobe Commerce as a Cloud Service med hjälp av AI-stödda utvecklingsverktyg.

1. Navigera till **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]** och kontrollera att `commerce-extensibility`-verktygsuppsättningen är aktiverad utan fel. Om du ser fel kan du slå av och på verktygslådan.

   ![Inställningarna för markörorientering visar MCP-verktygsuppsättningen för e-handel-utbyggbarhet aktiverad](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >När du arbetar med AI-stödda utvecklingsverktyg kan du förvänta dig naturliga variationer i koden och svaren som genereras av agenten.
   >Om du stöter på problem med koden kan du alltid be agenten att hjälpa dig felsöka den.

1. Inaktivera all dokumentation i markörens sammanhang:

   * Navigera till **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** och ta bort all dokumentation som visas.

   ![Markörindexering och dokumentinställningar med dokumentationslistan tom](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Generera kod för ett produktklassificeringstillägg:
   * Välj **[!UICONTROL Agent]**-läge i markörchattfönstret.
   * Ange följande uppmaning:

   ```shell-session
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >Om agenten begär att få söka i dokumentationen, tillåt det.

1. Svara på agentens frågor så att den kan generera den bästa koden.

   ![Markörchattfönstret i agentläge med tilläggsfråga aktiverat](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![AI-agent som frågar om frågor om tilläggskrav kan klargöras](../assets/agent-questions.png){width="600" zoomable="yes"}

1. Använd följande exempeltext för att besvara agentens frågor för att ställa in slumpmässiga klassificeringsdata:

   ```shell-session
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension is called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   Agenten skapar en `requirements.md`-fil som fungerar som källa för sanningen för implementeringen.

   ![Filen Requirements.md har skapats av AI-agenten med implementeringsinformation](../assets/requirements-file.png){width="600" zoomable="yes"}

1. Granska filen `requirements.md` och verifiera planen.

   Om allt ser korrekt ut instruerar du agenten att gå till **Fas 2 - Arkitekturplanering**.

1. Se arkitekturplanen.

1. Instruera agenten att fortsätta med kodgenerering.

   Agenten genererar den nödvändiga koden och ger en detaljerad sammanfattning med nästa steg.

   ![AI-agentens fas 2-arkitekturplan för klassificerings-API](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![Sammanfattning av genererade kodfiler och struktur](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![AI-agenten tillhandahåller nästa steg för testning och distribution](../assets/next-steps.png){width="600" zoomable="yes"}

### Testa tillägget lokalt

Följande steg beskriver hur du verifierar att tillägget fungerar innan du distribuerar det.

1. Be agenten att hjälpa dig att testa koden lokalt.

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. Följ agentens instruktioner och bekräfta att API:t fungerar lokalt.

   ![AI-agentinstruktioner för lokal API-testning](../assets/local-testing.png){width="600" zoomable="yes"}

   ![Terminalen visar lyckade testresultat för det lokala API:t med cURL](../assets/local-testing-1.png){width="600" zoomable="yes"}

### Distribuera tillägget

Distribuera tillägget till [!DNL Adobe I/O Runtime] med agenten.

1. När du har verifierat den genererade koden distribuerar du tillägget med följande uppmaning:

   ```shell-session
   Deploy the ratings API.
   ```

   Agenten utför en bedömning av beredskapen inför driftsättningen innan den distribueras.

   ![Checklista för utvärdering av beredskap för AI-agent före distribution](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. När du är säker på utvärderingsresultaten instruerar du agenten att fortsätta med distributionen.

   Agenten använder MCP-verktygen för att verifiera, bygga och driftsätta automatiskt.

   ![Verifiering av MCP-verktygspaket och distributionsprocess](../assets/deployment-process.png){width="600" zoomable="yes"}

### Verifiera distributionen

Testa API:t innan du integrerar det i butiken. Agenten bör tillhandahålla platsen för den nya åtgärden och en testningsstrategi.

![AI-agenttestningsstrategi med distribuerad åtgärds-URL och testkommandon](../assets/testing-strategy.png){width="600" zoomable="yes"}

Du kan också testa API:t manuellt med cURL i en terminal:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![Terminal som visar lyckat cURL-test av distribuerat klassificerings-API](../assets/curl-test.png){width="600" zoomable="yes"}

### Integrera med Edge Delivery Services

Om du vill integrera klassificerings-API:t med en [!DNL Adobe Commerce]-butik som drivs av [!DNL Edge Delivery Services] ber du agenten att skapa ett tjänstkontrakt med krav för klassificerings-API:

```shell-session
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![AI-agenten skapar tjänstekontraktfil för integrering mellan butiker](../assets/create-contract.png){width="600" zoomable="yes"}

![Kontraktmarkeringsfil för graderings-API med slutpunkts- och svarsinformation](../assets/contract.png){width="600" zoomable="yes"}

Återgå till terminalen och kör följande kommando i mappen `extension` för att kopiera kontraktsfilen till mappen `storefront`:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Anslut till butiken

I det här avsnittet får du hjälp med att implementera storefront-delen av klassificeringstillägget med [!DNL Edge Delivery Services] och AI-stödda utvecklingsverktyg.

>[!NOTE]
>
>De uppmaningar som ges är startpunkter. Även om du kan använda dem utan ändringar bör du överväga att föra en naturlig konversation med agenten.
>
>När du arbetar med AI-stödda utvecklingsverktyg finns det alltid naturliga variationer i koden och svaren som genereras av agenten.
>
>Om du råkar ut för problem med koden ber du agenten att hjälpa dig felsöka den.

### Krav för Storefront

Kontrollera att du har följande innan du startar integreringen av butiken:

* Ett butiksprojekt som är anslutet till din [!DNL Commerce]-instans
* Commerce storefront AI-verktyg [installerade med CLI](./tutorial-prerequisites.md#install-the-storefront-ai-tools)

### Konfigurera arbetsytan för lagerfront

Förbered din lokala butiksmiljö för utveckling.

1. Navigera till mappen `storefront`:

   ```bash
   cd storefront
   ```

1. Öppna mappen storefront i ett nytt markörfönster.

   Om du har [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installerat kan du öppna fönstret med följande kommando i terminalen:

   ```bash
   cursor .
   ```

1. Starta den lokala utvecklingsservern:

   ```bash
   npm run start
   ```

1. Navigera till en produktsida i en webbläsare:

   ```shell-session
   http://localhost:3000/products/llama-plush-shortie/adb336
   ```

1. Observera informationssidan (PDP) för framsidan av standardbutiksprodukter och notera att det inte finns några visuella produktbetyg.

### Integrera API:t för omdömen

Använd agenten för att integrera klassificerings-API:t i butikens produktinformationssida.

1. Använd följande uppmaning till din agent:

   ```shell-session
   Integrate the ratings API into the PDP to show star ratings and a review count for products. Here's the service contract: @RATINGS_API_CONTRACT.md
   ```

1. Agenten utvärderar uppgiftens komplexitet och anropar ett fasat arbetsflöde. Under **fas 1 (kravinsamling)** skapar agenten ett kravdokument och frågar om klargörande frågor som:

   * Var på PDP ska omdömen visas?
   * Bör detta vara ett nytt fristående block eller en platsanpassning inuti den befintliga PDP-instickskomponenten?
   * Vad är reservvärdet om API:t inte är tillgängligt eller inte returnerar några data?
   * Ska graderingar även visas på PLP (produktlista) eller endast PDP?
   * Finns det några designspecifikationer eller dummies?

   Svara på de här frågorna baserat på dina projektbehov. Agenten uppdaterar kravdokumentet och markerar fasen som slutförd.

1. Under **fas 2 (arkitekturplanering)** undersöker agenten dokumentation och din kodbas innan han föreslår en arkitektur. Förvänta dig att agenten ska:

   * Sök i [!DNL Commerce]-dokumentationen efter PDP-insticksbehållare, fack och händelsenyttolaster.
   * Sök igenom katalogen `blocks` och mappen `scripts/initializers/` efter befintlig PDP-relaterad kod.
   * Utforska TypeScript-definitioner för tillgängliga behållare och platskontextformer.

   Agenten presenterar sedan arkitekturalternativ som:

   * **Alternativ A:** Anpassa en befintlig PDP-insticksplats för att mata in klassificeringar nära produkttiteln - en lättare touch som är uppgraderingsvänlig.
   * **Alternativ B:** Skapa ett nytt fristående `product-ratings` -block som hämtar från API:t oberoende av varandra - flexiblare och frikopplat.
   * **Alternativ C:** Skapa ett nytt block som även lyssnar på PDP-släppningshändelser för produktens SKU - en hybridmetod.

   Planen innehåller även information om API-integrering, prestandaöverväganden (lazy loading, caching), säkerhet (indatasanitifiering) och en testmetod.

   Granska arkitekturplanen och instruera agenten att fortsätta.

1. Under **fas 3 (implementeringsmetod)** ber agenten dig välja mellan:

   * **Alternativ A:** Granska en detaljerad implementeringsplan före kodgenerering (se alla filer, mönster och kodstrukturen först).
   * **Alternativ B:** Fortsätt direkt till kodgenerering.

   Välj önskat tillvägagångssätt.

1. Under **fas 4 (implementering)** genererar agenten kod baserat på den valda arkitekturen. Beroende på hur man arbetar använder agenten flera specialkunskaper:

   * **Innehållsmodellering:** Om ett nytt block behövs utformar agenten en designvänlig innehållsstruktur, till exempel en konfigurationstabell med API-slutpunkts-URL:en.
   * **Blockutveckling:** Agenten skapar blockfiler enligt [!DNL Edge Delivery Services] konventioner, inklusive JavaScript-dekorationsfunktioner, CSS-format med omfång, ARIA-etiketter för tillgänglighet samt inläsning och felhantering.
   * **Anpassning av insticksprogram:** Om arkitekturen använder anpassning av kortplats importerar agenten rätt behållare, använder en verifierad kortplats nära produkttiteln och prenumererar på produktdatahändelser för aktuell SKU.

   Se koden som genereras och ställ frågor eller omdirigera agenten efter behov. Agenten skapar en sammanfattning av produktionsberedskapen när kodgenereringen är klar.

1. Under **fas 4.5 (testning)** erbjuder agenten att testa implementeringen. Om du godkänner det:

   * Skapar en lokal testsida med rätt skript och format.
   * Startar en utvecklingsserver.
   * Kör webbläsarbaserad verifiering för visuell återgivning, interaktivitet, responsivt beteende, tillgänglighet och prestanda.
   * Skapar en strukturerad testrapport med resultaten.

   Följ med i webbläsaren för att bekräfta beteendet och rapportera eventuella problem.

1. Observera ändringarna i kodbasen och se efter om produktsidan innehåller uppdateringar.

   Du bör se följande ändringar i utvecklingsmiljön och webbläsaren:

   * En produktklassificeringskomponent skapas automatiskt.
   * Komponenten är integrerad i PDP med [in-platser](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots) eller som ett fristående block, beroende på vald arkitektur.
   * Stjärnor visas med rätt fyllningsproportioner baserat på klassificeringsvärden från ditt API.

   ![Produktinformationssida med stjärngraderingar som är integrerade under produkttiteln](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Självstudiekurs

Här följer en sammanfattning av ämnen som ingår i kursen:

* **Tilläggsutveckling:** Lär dig att beskriva nya funktioner för en AI-agent och generera ett fungerande REST API med [!DNL App Builder].
* **Lokal testning och distribution:** Testa API:t lokalt och distribuera det med MCP-verktygslådan.
* **Tjänstkontrakt:** Skapa API-kontrakt som förenar serverdelstillägg och butiksimplementeringar.
* **Avfasad integrering av butiker:** Arbeta genom krav, arkitektur och implementering med hjälp av AI-stödda kunskaper.
* **Insticksintegrering:** Arbeta med [!DNL Adobe Commerce] insticksbehållare och fack.
* **Återanvändbarhet av komponent:** Skapar delade komponenter som används i flera block.

## Nästa steg

Använd följande förslag för att anpassa ditt klassificeringstillägg eller skapa egna ändringar:

### Ändra stjärnfärgerna

Använd följande uppmaning till din agent:

```shell-session
Change the star fill color to red.
```

**Förväntat resultat:**

Stjärnorna ändras till rött.

![Produktomdömen visas med röd stjärnfyllningsfärg](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Lägg till en modal klassificeringsdistribution

Följande steg visar hur agenten hanterar komplexa gränssnittsfunktioner med visuella referenser.

1. **Innan du startar:** Spara följande modellbild och klistra in den i chatten med din storefront-agent.

   ![Mockup med klassificeringsfördelning efter stjärnnivå](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Följ de här stegen för att skapa klassificeringsdistributionen modal med hjälp av referensbilden som vägledning:

   * Uppdatera API:t för att returnera ytterligare data som representerar klassificeringsdistributionen.
   * Uppdatera API-kontraktet.
   * Uppdatera kontraktet i butikskodbasen.
   * Be storefront-agenten att använda referensbilden och det uppdaterade API-kontraktet för att lägga till klassificeringsdistributionen på PDP-sidan.

1. Observera följande ändringar i kodbasen och se efter om produktsidan innehåller uppdateringar:

   * Hur agenten tolkar den visuella dummyn
   * Om lämplig HTML-struktur används för tillgänglighet
   * Så här hanterar det lägena för placering och interaktion

#### Felsöka den modala distributionen

Om modalen inte fungerar som förväntat kan du prova följande:

* Om spärren inte visas kontrollerar du om webbläsarkonsolen innehåller fel.
* Om positionering är inaktiverad ber du agenten att åtgärda den med följande format:

  ```shell-session
  adjust the modal position to be...
  ```

![Modal som visar detaljerad graderingsfördelning med staplar på stjärnnivå](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
