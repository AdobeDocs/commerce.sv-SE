---
title: ADL Commerce labbkrav
description: Lär dig förutsättningarna för klassificeringstilläggslabbet.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce labbkrav

På den här sidan visas förutsättningarna och andra manuella konfigurationssteg för [klassificeringstilläggslabbet](./workbook.md). Labbet innehåller också ett skript som automatiserar de flesta av dessa steg.

## Förutsättningar för tillägg

Innan du börjar slutför du följande krav:

* Installera [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installera Commerce-plugin-programmet

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* Hämta en AI-assisterad IDE, t.ex. [Cursor](https://cursor.com/download) (rekommenderas), stöds även andra IDE:er, t.ex. Claude Code, Gemini CLI eller Copilot, men du kan behöva ändra uppmaningarna och andra steg i den här självstudiekursen.
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### Konfigurera AIO CLI

1. Rensa befintlig konfiguration:

   ```bash
   aio config clear
   ```

   Logga in med AIO CLI:

   ```bash
   aio auth login -f
   ```

1. Välj organisation, projekt och arbetsyta med hjälp av följande kommandon:

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![CLI-konfiguration](./assets/cli-configuration.png){width="600" zoomable="yes"}

### Startpaket för klonintegrering

Klona Commerce startpaket för integrering och förbered ditt projekt:

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Klona startpaket](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Skapa .env-filen

Skapa din miljökonfigurationsfil:

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### Hämta arbetsytekonfiguration

Kör följande kommando för att hämta arbetsytans konfigurationsfil:

```bash
aio console workspace download workspace.json
```

### Ansluta den lokala arbetsytan till fjärrarbetsytan

Länka ditt lokala projekt till den fjärranslutna arbetsytan:

```bash
aio app use workspace.json -m
```

![Anslut till arbetsyta](./assets/connect-workspace.png){width="600" zoomable="yes"}

## Krav för Storefront

Följande objekt krävs för att slutföra avsnittet [storefront](#connect-to-the-storefront) i den här självstudiekursen och för att se produktklassificeringarna i din butik.
<!-- 
* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### Hämta projektfilerna

Du kan hämta projektfilerna på ett av två sätt:

<!-- 
#### Option A: Clone the repository (recommended) -->

Om du har [!DNL Git] installerat öppnar du terminalen och klonar databasen:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### Installera rotberoenden

Installera huvudprojektberoenden:

```bash
npm install
```

Då installeras alla paket som krävs för storefront-programmet.

### Installera MCP-serverberoenden

Navigera till MCP-serverkatalogen och installera dess beroenden:

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### Aktivera MCP i markören

MCP-servern (Model Context Protocol) ger AI-agenter åtkomst till [!DNL Adobe Commerce] Storefront-dokumentation.

#### Öppna MCP-inställningar för markör

![Öppna MCP-inställningar för markör](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Öppna [!DNL Cursor]
1. Gå till **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**

#### Aktivera och konfigurera MCP-funktioner

Projektet innehåller en MCP-konfigurationsfil på `.cursor/mcp.json`. Filen bör redan vara konfigurerad att använda den lokala MCP-servern.

Verifiera MCP-konfigurationen:

1. Kontrollera att servern&quot;commerce-documentation-rag&quot; är listad och aktiverad

Konfigurationen bör se ut ungefär så här:

![MCP-konfiguration](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Skriptet `start-mcp.sh` läser automatiskt in miljövariablerna från din `.env`-fil i katalogen `mcp-server`.

#### Starta om pekaren

När du har aktiverat MCP och konfigurerat servern:

1. Avsluta [!DNL Cursor] helt
1. Öppna [!DNL Cursor] igen och öppna projektet `aem-boilerplate-commerce`

#### Verifiera MCP-anslutning

Kontrollera att MCP-servern körs som den ska:

1. Öppna en ny chatt i [!DNL Cursor]
1. Leta efter en indikator som visar att MCP-servern är ansluten (vanligtvis i chattgränssnittet)
1. Försök att ställa en fråga som: &quot;Sök i butiksdokumenten efter information om fack&quot;

Om MCP-servern fungerar bör du se relevanta dokumentationsresultat.

![MCP-anslutningen har verifierats](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### Starta utvecklingsservern

Starta den lokala utvecklingsservern:

```bash
npm run start
```

Utvecklingsservern börjar `http://localhost:3000`.

Navigera till sidan Kläder på `http://localhost:3000/apparel`.

![Utvecklingsservern körs](./assets/development-server-running.png){width="600" zoomable="yes"}
