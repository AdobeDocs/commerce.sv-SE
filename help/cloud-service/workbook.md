---
title: Självstudiekurs om klassificeringstillägg
description: Lär dig hur du bygger ett produktklassificeringstillägg för Adobe Commerce as a Cloud Service med hjälp av App Builder och AI-stödda utvecklingsverktyg.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce labbarbetsbok

Det här labbet vägleder dig genom att skapa ett produktklassificeringstillägg för [!DNL Adobe Commerce as a Cloud Service] med hjälp av [!DNL Adobe App Builder] och AI-stödda utvecklingsverktyg.

## Verifiera krav

Kontrollera att följande krav är installerade:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## Logga in på Adobe Developer Console

1. Gå till [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Om du redan är inloggad klickar du på din profilikon i det övre högra hörnet och sedan på knappen **Logga ut** .
1. Logga in med labbets e-post-ID och lösenord för din licens.
1. Om du uppmanas att lägga till en andra e-postadress eller ett annat telefonnummer klickar du på **Inte nu**.
1. När du uppmanas att välja en organisationsprofil väljer du **Adobe Commerce Labs**.

   ![select-organization](./assets/select-org.png){width="600" zoomable="yes"}

1. Om du uppmanas att acceptera villkoren klickar du på länken för att läsa villkoren, klickar sedan på **Godkänn och fortsätter**.

   ![accept-terms](./assets/accept-terms.png){width="600" zoomable="yes"}

## Kör installationsskriptet

Hämta och kör installationsskriptet om [förutsättningarna](#verify-prerequisites) är installerade och du har loggat in på Adobe Developer Console. Du kan också konfigurera skriptet manuellt genom att följa stegen i [labbkraven](workbook-prerequisites.md).

1. Klona databasen som innehåller installationsskriptet:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >Om skriptet misslyckas, gå till [förutsättningarna](workbook-prerequisites.md) och fortsätt där skriptet påträffade ett fel.

1. Navigera till databasen:

   ```bash
   cd commerce-adl-2025
   ```

1. Kör installationsskriptet:

   ```bash
   bash adl-setup.sh
   ```

   När skriptet körs uppmanas du att ange ditt användarnamn och lösenord, som kommer att anges i labbet. Ditt användarnamn återspeglar platsen och platsnumret. Om du till exempel är i San Jose, CA, licens 123 blir ditt användarnamn `sjc-adl-123@adobeeventlab.com`.

   Dessutom bör du välja det projekt som motsvarar ditt platsnummer och arbetsytan **stage**. Projektnamnet återspeglar platsen och platsnumret. Om du till exempel befinner dig i San Jose, CA, licens 123 blir ditt projektnamn `SJC ADL 123`.

## Tilläggsutveckling

I det här avsnittet får du hjälp med att utveckla ett klassificeringstillägg för Adobe Commerce as a Cloud Service med hjälp av AI-stödda utvecklingsverktyg.

### Installera AI-verktyg för tillägg

Konfigurera AI-stödda utvecklingsverktyg i mappen `extension`:

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![Installera AI-verktyg](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### Öppna markör

>[!NOTE]
>
>När du arbetar med AI-stödda utvecklingsverktyg kommer det att finnas naturliga variationer i koden och svaren som genereras av agenten.
>Om du stöter på problem med koden kan du alltid be agenten att hjälpa dig felsöka den.

Öppna programmet [!DNL Cursor] och gå till mappen `extension` eller, om du har installerat [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands), ange följande kommando i terminalen:

```bash
cursor .
```

![Öppna markör](./assets/open-cursor.png){width="600" zoomable="yes"}

Alla [!DNL Cursor]-regler är nu installerade i mappen `.cursor/rules`. MCP-verktygen finns i **MCP-inställningarna** i [!DNL Cursor]. Kontrollera att verktygsuppsättningen `commerce-extensibility` är aktiverad utan fel. Om du ser fel kan du slå av och på verktygslådan.

![Markörinställningar](./assets/cursor-settings.png){width="600" zoomable="yes"}

Om du har lagt till någon dokumentation i markörens kontext måste du inaktivera den. Navigera till [!UICONTROL **Markören**] > [!UICONTROL **Inställningar**] > [!UICONTROL **Markörinställningar**] > [!UICONTROL **Indexering och dokument**] och ta bort all dokumentation som visas.

![Inaktivera dokumentation](./assets/disable-documentation.png){width="600" zoomable="yes"}

### Kodgenerering

I det här avsnittet visas hur du använder AI-stödda verktyg för att generera kod för ett produktklassificeringstillägg.

#### Definiera krav

Du implementerar ett tillägg som visar produktklassificeringar som ett API. Tillägget [!DNL App Builder] svarar med klassificeringsinformation för en given SKU.

**Inledande fråga:**

Använd följande uppmaning i [!DNL Cursor]:

1. Öppna chattfönstret i Markör.
1. Välj läget **Agent**.
1. Ange följande uppmaning:

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. Om agenten begär att få söka i dokumentationen, tillåt det.

![Ange uppmaning i markören](./assets/enter-prompt.png){width="600" zoomable="yes"}

Medarbetaren undersöker kraven och frågar om man kan klargöra några frågor. Svara på agentens frågor så att den kan generera den bästa koden.

![Agenten frågar om klargörande frågor](./assets/agent-questions.png){width="600" zoomable="yes"}

**Svarsfråga:**

Använd följande svar för att svara på agentens frågor:

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

Agenten skapar en `requirements.md`-fil som fungerar som källa för sanningen för implementeringen.

![Kravfilen har skapats](./assets/requirements-file.png){width="600" zoomable="yes"}

#### Verifiera kraven och planens arkitektur

1. Granska filen `requirements.md`.
1. Om allt ser korrekt ut instruerar du agenten att gå till **Fas 2 - Arkitekturplanering**.
1. Se arkitekturplanen.
1. Instruera agenten att fortsätta med kodgenerering.

![Arkitekturplanering](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### Generera kod

Agenten genererar den nödvändiga koden och ger en detaljerad sammanfattning med nästa steg.

![Sammanfattning av kodgenerering](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![Nästa steg](./assets/next-steps.png){width="600" zoomable="yes"}

### Lokal testning

Be agenten att hjälpa dig att testa koden lokalt.

```text
Test the ratings API locally on a dev server using cURL.
```

Följ agentens instruktioner och bekräfta att API:t fungerar lokalt.

![Lokal testning](./assets/local-testing.png){width="600" zoomable="yes"}

![Lokala testresultat](./assets/local-testing-1.png){width="600" zoomable="yes"}

### Distribuera tillägget

När du har verifierat den genererade koden kan du distribuera tillägget med följande uppmaning:

```text
Deploy the ratings API.
```

#### Utvärdering före driftsättning

Agenten utför en bedömning av beredskapen inför driftsättningen innan den distribueras.

![Utvärdering före distribution](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### Distribuera

När du är säker på utvärderingsresultaten instruerar du agenten att fortsätta med distributionen. Agenten använder MCP-verktygen för att verifiera, bygga och driftsätta automatiskt.

![Distribution](./assets/deployment-process.png){width="600" zoomable="yes"}

### Testa API:t

Du kan testa API:t innan du integrerar det i butiken.

Agenten anger platsen för den nya åtgärden och en testningsstrategi.

![Testningsstrategi](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### Testa manuellt med cURL

Testa API:t manuellt med cURL i en terminal:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cURL-test](./assets/curl-test.png){width="600" zoomable="yes"}

### Integrera med Edge Delivery Services

Om du vill integrera klassificerings-API:t med en [!DNL Adobe Commerce]-butik som drivs av [!DNL Edge Delivery Services] ber du agenten att skapa ett tjänstkontrakt med krav för klassificerings-API:

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Tjänstkontrakt](./assets/create-contract.png){width="600" zoomable="yes"}

![Information om servicekontrakt](./assets/contract.png){width="600" zoomable="yes"}

Återgå till terminalen och kör följande kommando i mappen `extension` för att kopiera filen till mappen `storefront`:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Anslut till butiken

I det här avsnittet får du hjälp att implementera riktiga butiksfunktioner som visar hur du kan kommunicera effektivt med AI-agenter när du arbetar med [!DNL Adobe Commerce] dropins och [!DNL Edge Delivery Services].

>[!NOTE]
>
>De uppmaningar som ges är startpunkter. Du bör känna dig fri att ha en naturlig konversation med agenten. När du arbetar med AI-stödda utvecklingsverktyg kommer det att finnas naturliga variationer i koden och svaren som genereras av agenten.
>
>Om du stöter på problem med koden kan du alltid be agenten att hjälpa dig felsöka den.

### Implementera stjärngraderingar och antal granskningar

1. Navigera till mappen `storefront`:

   ```bash
   cd storefront
   ```

1. Öppna mappen storefront i ett nytt markörfönster. Om du har installerat [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) anger du följande kommando i terminalen:

   ```bash
   cursor .
   ```

1. Starta den lokala utvecklingsservern:

   ```bash
   npm run start
   ```

1. I en webbläsare går du till sidan Klar:

   ```text
   http://localhost:3000/apparel
   ```

1. Lägg märke till gränssnittslayouten för mallskyltspaletten.

1. Använd följande uppmaning till din agent:

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >Om du uppmanas att starta den lokala utvecklingsservern ska du informera agenten om att den redan körs.

1. Observera ändringarna i kodbasen och se på sidan Skalförändra för uppdateringar.

**Förväntat resultat:**

* En&quot;komponent&quot; skapas automatiskt.
* Komponenten är integrerad i produktinformation, produktlistsida och produktrekommendationsblock med hjälp av Sitts.
* Stjärnor visas med rätt fyllningsproportioner baserat på modellklassificeringsvärden.

![Produktgraderingsimplementering](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### Ändra stjärnfärgerna

Använd följande uppmaning till din agent:

```text
Change the star fill color to red.
```

**Förväntat resultat:**

Stjärnorna ändras till rött.

![Röda stjärnfärger](./assets/red-star-colors.png){width="600" zoomable="yes"}

## Rektangulärt lager

Under den här självstudiekursen har vi gått igenom följande ämnen:

* **Funktionsimplementering**: Så här beskriver du nya funktioner för en AI-agent.
* **Interaktiva ändringar**: Gör snabba ändringar i befintlig kod.
* **Komplexa gränssnittskomponenter**: Skapa interaktiva funktioner med visuella referenser.
* **Dropin-integrering**: Arbeta med [!DNL Adobe Commerce] dropin-behållare och -platser.
* **Återanvändbarhet för komponent**: Skapar delade komponenter som används i flera block.

## Nästa steg

Om tiden tillåter kan du anpassa ditt klassificeringstillägg ytterligare genom att lägga till följande funktioner:

### Lägg till modal värderingsfördelning (valfritt)

Följande steg visar hur agenten hanterar komplexa gränssnittsfunktioner med visuella referenser.

1. **Innan du startar:** Spara följande modellbild och klistra in den i chatten med din storefront-agent.

   ![Värderingsdistributionssammanställning](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Följ de här stegen för att vägleda dig genom att skapa klassificeringsdistributionen modal baserat på referensbilden:

   * Uppdatera API:t för att returnera ytterligare data som representerar klassificeringsdistributionen.
   * Uppdatera API-kontraktet.
   * Uppdatera kontakten i butikens kodbas.
   * Be storefront-agenten att använda referensbilden och det uppdaterade API-kontraktet för att lägga till klassificeringsdistributionen på PDP-sidan.

1. Observera följande ändringar i kodbasen och se efter om det finns uppdateringar på sidan Klar:

   * Hur agenten tolkar den visuella dummyn
   * Om lämplig HTML-struktur används för tillgänglighet
   * Så här hanterar det lägena för placering och interaktion

**Felsökning:**

* Om spärren inte visas kontrollerar du om webbläsarkonsolen innehåller fel.
* Om positionering är avaktiverad kan du be agenten att:

  ```text
  adjust the modal position to be...
  ```

![Värderingsdistributionsmodul](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
