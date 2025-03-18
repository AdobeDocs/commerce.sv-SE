---
title: Konfigurera din butik
description: Lär dig hur du använder verktyget för att ställa in din Adobe Commerce as a Cloud Service-butik.
role: Developer
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Konfigurera din butik

Följande steg visar hur du snabbt konfigurerar din Adobe Commerce Storefront som drivs av Edge Delivery med kommandot `aio commerce init`. I den här processen ställs följande in:

* [Commerce Storefront från Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) - En prestanda, skalbar och säker lagringsplats från Adobe Edge Delivery Services.
* [API-nät för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/mesh/) - en API-plattform där utvecklare kan kombinera flera datakällor till en enda GraphQL-slutpunkt. API Mesh koordinerar tredjeparts-API med Adobe API via en enda gateway. En fråga till en enda GraphQL-slutpunkt kan returnera resultat från flera källor.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - En samling utvecklarverktyg med tillgång till API:er, händelser, körningsfunktioner och plugin-program, som du kan använda för att skapa projekt för Adobe-program.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - En serverlös motor för att distribuera anpassad kod som svarar på händelser och kör funktioner i molnet.

## Förutsättningar

Innan du kör kommandot `aio commerce init` måste du uppfylla följande krav:

1. Installera NVM (Node Version Manager).

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. Installera Node.js och NPM. Mer information finns i [Node.js](https://nodejs.org/en/).

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. Installera [Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Installera Adobe I/O API Mesh-plugin.

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. Installera plugin-programmet Adobe I/O Commerce.

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Uppdatera befintliga plugin-program.

   ```bash
   aio plugins:update
   ```

1. Logga in på ditt Adobe Experience Cloud-konto.

   ```bash
   aio login
   ```

1. Välj IMS-organisation, projekt och arbetsyta. Använd piltangenterna och tryck på **Retur** för att göra ditt val. Mer information om `aio`-kommandon finns i [Adobe I/O CLI-dokumentationen](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands).

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. Om du inte redan har det godkänner du användarvillkoren för utvecklare i Adobe Developer-konsolen genom att gå till https://developer.adobe.com/console/home och klicka på **Acceptera och fortsätt**.

## Kör kommandot `aio commerce init`

Om du kör följande kommando skapas en ställningar för din Commerce-butik. Den här byggnadsställningen är en bra startpunkt för att bygga upp och förstå din butiksplats. Mer information om hur du arbetar med butiken finns i [dokumentationen för Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).


1. Kör kommandot `init`:

   ```bash
   aio commerce init
   ```

1. Om du redan är inloggad på GitHub anger du `Y` för att skapa svaret under ditt användarnamn.

1. Ange namnet på den databas som du vill skapa.

1. Välj den mall som ska användas, till exempel `adobe-commerce/adobe-demo-store`.

1. Välj något av följande alternativ:

   * **Använd Adobe demoinstans (standardslutpunkter)** - Använd Commerce-instans med Adobe-exempel.
      * Om du väljer det här alternativet uppmanas du att installera AEM Code Sync-roboten i ett webbläsarfönster. Du måste ange den databas du skapade och auktorisera roboten. Återgå till CLI och ange `y` för att bekräfta installationen av AEM Code Sync-roboten.
   * **Välj ett tillgängligt API (Nät -> SaaS)** - Välj en befintlig Commerce-instans i den valda organisationen.
      * Om du väljer det här alternativet måste du markera projektet och arbetsytan för att skapa ett nät i.

   >[!NOTE]
   >
   >Om du väljer alternativet `Pick an available API (Mesh -> SaaS)` måste du ha ett befintligt projekt och Workspace i Adobe Developer Console. [Om du skapar ett mallprojekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) och väljer App Builder skapas de nödvändiga arbetsytorna automatiskt.

1. När processen är klar kan du anpassa butiken på följande sätt:

   * Anpassa koden: `https://github.com/<username or org>/<repo name>`
   * Redigera ditt innehåll: `https://da.live/#/<username or org>/<repo name>`
   * Hantera din konfiguration: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * Förhandsgranska din butik: `https://main--<repo name>--<username or org>.aem.page/`
   * Kör lokalt: `aio commerce:dev`

Mer information om hur du anpassar din butik finns i [dokumentationen för Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).
