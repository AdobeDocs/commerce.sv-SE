---
title: Krav för klassificeringstillägg - självstudiekurs
description: Lär dig förutsättningarna för klassificeringstilläggslabbet.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e153e974be1dc5ec8ff2eff8d699ce87ef6708dc
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Krav för klasstillägg - självstudiekurs (Beta)

>[!NOTE]
>
>AI-verktygen som används i den här självstudiekursen finns för närvarande i Beta och kan innehålla buggar eller andra problem.

På den här sidan visas förutsättningarna och konfigurationsstegen för självstudiekurser som använder [!DNL Adobe Commerce as a Cloud Service], t.ex. självstudiekursen [för klassificeringstillägg](./ratings-extension.md).

## Krav för Adobe Commerce as a Cloud Service

* Installera [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installera Commerce-plugin-programmet

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* Hämta en AI-assisterad IDE, t.ex. [Cursor](https://cursor.com/download) (rekommenderas), stöds även andra IDE:er, t.ex. Claude Code, Gemini CLI eller Copilot, men kan kräva ändringar i uppmaningarna och andra steg i självstudiekursen.

### Krav för Adobe Developer Console

1. Gå till [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Logga in med din e-postadress och ditt lösenord.

#### Skapa ett nytt projekt

1. Navigera till [Adobe Developer Console](https://developer.adobe.com/).
1. Klicka på [!UICONTROL **Skapa projekt från en mall**].
1. Välj mallen [!UICONTROL **App Builder**].
1. Ange en [!UICONTROL **projekttitel**] och [!UICONTROL **programnamn**].
1. Kontrollera att kryssrutan **[!UICONTROL Include Runtime]** är markerad.

   ![Skapa projekt med App Builder-mall](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Klicka på **Spara**.

#### Lägg till API:er på arbetsytan

1. Klicka på arbetsytan [!UICONTROL **Stage**] och upprepa sedan följande steg för varje API.

   ![API:er har lagts till på arbetsytan](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Klicka på [!UICONTROL **Lägg till tjänst**] och välj [!UICONTROL **API**].

1. Välj någon av följande API:er. Du måste upprepa den här processen för varje API som anges nedan:

   * [!UICONTROL **Adobe Services**]-filter:
      * [!UICONTROL **API för I/O-hantering**]
      * [!UICONTROL **I/O-händelser**] API
   * [!UICONTROL **Experience Cloud**]-filter:
      * [!UICONTROL **Adobe I/O Events för Adobe Commerce**] API

1. Klicka på [!UICONTROL **Nästa**].

1. Klicka på&#x200B;[!UICONTROL **Spara konfigurerat API**].

1. Upprepa föregående steg tills alla API:er har lagts till på arbetsytan.

   ![API:er har lagts till på arbetsytan](../assets/apis-added.png){width="600" zoomable="yes"}

### Konfigurera Adobe I/O CLI

1. Rensa befintlig konfiguration:

   ```bash
   aio config clear
   ```

   Logga in med [!DNL Adobe I/O CLI]:

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

   ![CLI-konfiguration](../assets/cli-configuration.png){width="600" zoomable="yes"}

### Klona startpaketet för integrering

Klona Commerce startpaket för integrering och förbered ditt projekt:

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Klona startpaket](../assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Skapa en .env-fil

Skapa din miljökonfigurationsfil:

```bash
cp env.dist .env
```

Öppna filen `.env` i en textredigerare och lägg till följande OAuth-autentiseringsuppgifter:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Du kan kopiera dessa värden från sidan **[!UICONTROL Credential details]** i [Developer Console](https://developer.adobe.com/) genom att klicka på fliken **[!UICONTROL OAuth Server-to-Server]** på arbetsytan.

![OAuth-autentiseringsuppgifter](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Lägg till Commerce-konfigurationen

Lägg till följande Commerce-instansinformation i din `.env`-fil:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Så här hittar du dessa värden:

1. Navigera till [Commerce Cloud Service-instanser](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Klicka på informationsikonen bredvid instansen.
1. Kopiera REST-slutpunkten som `COMMERCE_BASE_URL`.
1. Kopiera GraphQL-slutpunkten som `COMMERCE_GRAPHQL_ENDPOINT`.

#### Ange händelseprefix

Ange ett tillfälligt värde för händelseprefixet:

```text
EVENT_PREFIX=test
```

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

![Anslut till arbetsyta](../assets/connect-workspace.png){width="600" zoomable="yes"}

### Installera AI-verktyg för tillägg

Uppdatera markörregelfilen och MCP-konfigurationen så att det innehåller paketet `commerce-extensibility-tools`.

1. Konfigurera AI-stödda utvecklingsverktyg i mappen `extension` med följande kommandon:

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Installera AI-verktyg](../assets/install-ai-tools.png){width="600" zoomable="yes"}
<!--
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and see the product ratings in your store.

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
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Get the project files

You can obtain the project files using one of the following methods:

#### Option A: Clone the repository (recommended)

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

#### Option B: Download the zip file

If you do not have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ```

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create an `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values:

```env
RAG_MODE=worker
WORKER_RAG_URL=
```

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](../assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor].
1. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](../assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely.
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project.

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor].
1. Look for an indicator showing the MCP server is connected. This indicator is typically located in the chat interface.
1. Try entering a prompt like the following:

   ```text
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
