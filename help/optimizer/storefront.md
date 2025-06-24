---
title: Konfigurera din butik
description: Lär dig hur du konfigurerar din  [!DNL Adobe Commerce Optimizer] butik.
role: Developer
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Konfigurera din butik

I den här självstudiekursen visas hur du konfigurerar och använder [Adobe Commerce Storefront från Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) för att skapa en prestanda, skalbar och säker Commerce Storefront som drivs av data från din [!DNL Adobe Commerce Optimizer]-instans.


## Förutsättningar

- Se till att du har ett GitHub-konto (github.com) som kan skapa databaser och är konfigurerat för lokal utveckling.

- Lär dig mer om begreppen och arbetsflödet för att utveckla Commerce-butiker på Adobe Edge Delivery Services genom att läsa [Översikt](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) i dokumentationen för Adobe Commerce Storefront.
- Konfigurera utvecklingsmiljön


### Konfigurera utvecklingsmiljön

Installera Node.js och det webbläsartillägg för Sidekick som krävs för att utveckla och testa din [!DNL Adobe Commerce Optimizer]-butik på Edge Delivery Services.

#### Installera Node.js

Installera Node Version Manager (NVM) och den nödvändiga Node.js-versionen (22.13.1 LTS).

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

1. Verifiera installationen.

   ```bash
   npm -v
   ```

>[!TIP]
>
>Ytterligare resurser för att utöka och anpassa din [!DNL Adobe Commerce Optimizer]-lösning finns tillgängliga via [App Builder för Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) och [API Mesh för Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Kontakta din Adobe-representant om du vill ha information om åtkomst och användning.

#### Installera Sidekick

Installera Sidekick webbläsartillägg om du vill redigera, förhandsgranska och publicera material i butiken. Se [Installationsanvisningar för Sidekick](https://www.aem.live/docs/sidekick#installation).

## Skapa en butik

I butiken som du skapar för ditt [!DNL Adobe Commerce Optimizer]-projekt används en anpassad version av Adobe Commerce på Edge Delivery Services Storefront-mallsidan. Mallen är en uppsättning filer och mappar som utgör en startpunkt för utveckling av butiker. Den här installationsprocessen skiljer sig från standardkonfigurationsprocessen för en [Adobe Commerce på Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>I den här självstudien används macOS, Chrome och Visual Studio Code som utvecklingsmiljö. Skärmen visar inställningarna och instruktionerna. Du kan använda ett annat operativsystem, en annan webbläsare och en annan kodredigerare, men användargränssnittet som visas och stegen som du utför varierar beroende på detta.

### Översikt över arbetsflödet

Följ de här stegen för att konfigurera en butiksplats som ska användas med [!DNL Adobe Commerce Optimizer].

1. **[Skapa en koddatabas](#step-1-create-site-code-repository)**-Skapa en GitHub-databas från standardmallen Adobe Commerce + Edge Delivery Services. Inkludera alla grenar från källdatabasen.
1. **[Uppdatera storefront-mallsidan](#step-2-update-the-storefront-boilerplate)**-Uppdatera den anpassade mallmallen på grenen `aco` för att ansluta innehållsmappen till butiken.
1. **[Distribuera ändringar](#step-3-deploy-changes)**-Skriv över koden i grenen `main` med den uppdaterade koden från grenen `aco`.
1. **[Lägg till appen CodeSync](#step-5-add-the-aem-code-sync-app)**-Anslut din databas till Edge Delivery-tjänsten. Anslut inte appen Kodsynkronisering förrän du har slutfört anpassningen av källkoden och överfört koden till grenen `main`.
1. **[Lägg till innehåll](#step-6-add-content)**-Använd klonverktyget för demoinnehåll för att skapa och initiera ditt butiksinnehåll i dokumentförfattarmiljön som finns på `https://da.live`.
1. **[Förhandsgranska demowebbplatsen](#step-7-preview-demo-site)**-Anslut till din butiksplats för att visa exempelinnehåll och data från demoinstansen [!DNL Adobe Commerce Optimizer].
1. **[Utveckla i din lokala miljö](#step-8-develop-in-your-local-environment)**-Installera de beroenden som krävs. Starta den lokala utvecklingsservern och uppdatera butikskonfigurationen för att ansluta till [!DNL Adobe Commerce Optimizer]-instansen som Adobe har etablerat åt dig.
1. **[Nästa steg](#next-steps)**-Lär dig mer om att hantera och visa innehåll och data i butiken.


### Steg 1: Skapa platskoddatabas

Skapa en GitHub-databas för webbplatsens mallkod för butiken med hjälp av mallen Edge Delivery Services + Adobe Commerce-standardmall.

1. Logga in på ditt GitHub-konto.

1. Navigera till GitHub-databasen [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) .

1. Välj **Använd den här mallen** och välj sedan **Skapa en ny databas** i listrutan.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Konfigurationssidan för databasen visas.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Fyll i konfigurationsformuläret med följande information:

   - **Databasmall**—`hlxsites/aem-boilerplate-commerce` (standard).
   - **Inkludera alla grenar** - Välj alternativet att inkludera alla grenar.
   - **Ägare** - Din organisation eller ditt konto (krävs).
   - **Databasnamn** - Ett unikt namn för din nya repo (krävs).
   - **Beskrivning** - En kort beskrivning av ditt svar (valfritt).
   - **Offentlig eller privat** - Adobe rekommenderar public (standard).

1. Välj **Skapa databas**.

   Efter flera minuter öppnas din nya databas.

   Ignorera meddelanden om pull-begäran som visas i GitHub-användargränssnittet.

### Steg 2: Uppdatera storefront-skylten

Du behöver följande information för att kunna uppdatera koden för skyltplattan för butiken:

- **GitHub-databas-URL från steg 2**— `github.com/{ORG}/{SITE}`
   - `{ORG}` är organisationens namn eller användarnamn för databasen
   - `{SITE}` är ditt databasnamn
- **URL för innehållsmapp från steg 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}` är ID:t för mappen som du skapade med exempelinnehållsdata.

#### Länka databasen till dokumentförfattarmiljön

1. Klona databasen till din lokala dator.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   Om du får problem när du klonar databasen läser du [Felsöka kloningsfel](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) i GitHub-dokumentationen.

1. Öppna databasen i din terminal eller IDE.

1. Kolla in grenen `aco`

   ```bash
   git checkout aco
   ```

1. Skapa konfigurationsfilen genom att kopiera filen `default-fstab.yaml` till `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Uppdatera monteringspunkten i butikskonfigurationsfilen så att den pekar på innehålls-URL:en.

   1. Öppna konfigurationsfilen [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. Ersätt strängarna `{ORG}` och `{SITE}` med värdena för GitHub-databasen som du skapade för din standardkod.

      Den uppdaterade koden ska till exempel se ut så här.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. Spara filen.

#### Konfigurera Sidekick-tillägget

1. Lägg till projektkonfigurationen för Sidekick-tillägget. Med den här konfigurationen kan du vara säker på att Sidekick är tillgängligt för att hantera innehåll för ditt butiksprojekt.

>[!NOTE]
>
>Kontrollera att du har installerat [Sidekick-tillägget](https://www.aem.live/docs/sidekick#installation) i webbläsaren.

1. Öppna filen `tools/sidekick/config.json`.

   +++Sidekick konfigurationsfil

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   Mer information finns i [dokumentationen för Sidekick-biblioteket](https://www.aem.live/docs/sidekick-library).

+++

1. Uppdatera nyckelvärdena för `url` med värdena för din GitHub-databas.

   - Ersätt strängen `{ORG}` med organisationen eller användarnamnet för din databas.

   - Ersätt strängen `{SITE}` med databasnamnet

   +++Exempel på uppdaterad konfigurationsfil

   Om din GitHub-databas har namnet `aco-storefront` och din organisation är `early-adopter`, ska den uppdaterade URL:en se ut så här:

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
