---
title: Konfigurera din butik
description: Lär dig hur du konfigurerar din  [!DNL Adobe Commerce Optimizer] butik.
role: Developer
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: f1aa8439d6322e5278ab787f5cd096e16b7813a2
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 0%

---

# Konfigurera din butik

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

I den här självstudiekursen visas hur du konfigurerar och använder [Adobe Commerce Storefront från Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) för att skapa en prestanda, skalbar och säker Commerce Storefront som drivs av data från din [!DNL Adobe Commerce Optimizer]-instans.


## Förutsättningar

* Se till att du har ett GitHub-konto (github.com) som kan skapa databaser och är konfigurerat för lokal utveckling.

* Lär dig mer om begreppen och arbetsflödet för att utveckla Commerce-butiker på Adobe Edge Delivery Services genom att läsa [Översikt](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) i dokumentationen för Adobe Commerce Storefront.
* Konfigurera utvecklingsmiljön


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
>Den här konfigurationsprocessen för butiken är att använda [!DNL Adobe Commerce Optimizer] med Adobe Commerce Edge Delivery Service Storefront. Ytterligare resurser för att utöka och anpassa din [!DNL Adobe Commerce Optimizer]-lösning finns tillgängliga via [App Builder för Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) och [API Mesh för Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Kontakta din Adobe-representant om du vill ha information om åtkomst och användning.

#### Installera Sidekick

Installera Sidekick webbläsartillägg om du vill redigera, förhandsgranska och publicera material i butiken. Se [Installationsanvisningar för Sidekick](https://www.aem.live/docs/sidekick#installation).


## Skapa en butik

I butiken som du skapar för ditt [!DNL Adobe Commerce Optimizer]-projekt används en anpassad version av Adobe Commerce på Edge Delivery Services Storefront-mallsidan. Mallen är en uppsättning filer och mappar som utgör en startpunkt för utveckling av butiker. Den här installationsprocessen skiljer sig från standardkonfigurationsprocessen för en [Adobe Commerce på Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>I den här självstudien används macOS, Chrome och Visual Studio Code som utvecklingsmiljö. Skärmen visar inställningarna och instruktionerna. Du kan använda ett annat operativsystem, en annan webbläsare och en annan kodredigerare, men användargränssnittet som visas och stegen som du utför varierar beroende på detta.

### Översikt över arbetsflödet

Följ de här stegen för att konfigurera en butiksplats som ska användas med [!DNL Adobe Commerce Optimizer].

1. **[Skapa en innehållsmapp](#step-1-create-a-content-folder)**-Skapa en delad innehållsmapp i Google Drive eller Sharepoint. Den här mappen innehåller exempelinnehåll och resurser för din butik.

1. **[Skapa en koddatabas](#step-2-create-a-code-repository)**-Skapa en GitHub-databas från standardmallen Adobe Commerce + Edge Delivery Services. Inkludera alla grenar från källdatabasen.
1. **[Uppdatera storefront-mallsidan](#step-3-update-the-storefront-boilerplate)**-Uppdatera den anpassade mallmallen på grenen `aco` för att ansluta innehållsmappen till butiken.
1. **[Ladda upp den uppdaterade butiksskyltkoden](#step-4-upload-the-updated-boilerplate-code)**-Skriv över koden i grenen `main` med den uppdaterade koden från grenen `aco`.
1. **[Lägg till appen CodeSync](#step-5-add-the-aem-code-sync-app)**-Anslut din databas till Edge Delivery-tjänsten. Anslut inte appen Code Sync förrän du har slutfört anpassningen av källkoden och är redo att skicka koden till grenen `main`.
1. **[Förhandsgranska och publicera ditt innehåll](#step-6-preview-and-publish-your-content)**-Använd Sidekick-tillägget för att förhandsgranska och publicera webbplatsinnehållet från innehållsmappen till butiken.
1. **[Förhandsgranska webbplatsen och visa exempeldata](#step-7-preview-your-site)**-Anslut till din butiksplats för att visa exempelinnehåll och data från demoinstansen [!DNL Adobe Commerce Optimizer].
1. **[Utveckla butiken i den lokala miljön](#step-8-develop-the-storefront-in-your-local-environment)**-Installera de nödvändiga beroendena. Starta den lokala utvecklingsservern och uppdatera butikskonfigurationen för att ansluta till [!DNL Adobe Commerce Optimizer]-instansen som Adobe har etablerat åt dig.
1. **[Nästa steg](#next-steps)**-Lär dig mer om att hantera och visa innehåll och data i butiken.

### Steg 1: Skapa en innehållsmapp

Följ instruktionerna i dokumentationen för Adobe Commerce Storefront för att lägga till en delad innehållsmapp i Google Drive eller Sharepoint och lägga till exempelinnehållet. Exempelinnehållet innehåller bilder, text och andra resurser som utgör din plats.

* [Skapa och dela en Google Drive- eller Sharepoint-mapp](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder)
* [Läs in exempelinnehållet](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content) i din mapp.

### Steg 2: Skapa en koddatabas

Skapa en lagringsplats för mallkod i GitHub med Edge Delivery Services + Adobe Commerce-mallen för mallsidor.

1. Logga in på ditt GitHub-konto.

1. Navigera till GitHub-databasen [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) .

1. Välj **Använd den här mallen** och välj sedan **Skapa en ny databas** i listrutan.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Konfigurationssidan för databasen visas.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Fyll i konfigurationsformuläret med följande information:

   * **Databasmall**—`hlxsites/aem-boilerplate-commerce` (standard).
   * **Inkludera alla grenar** - Välj alternativet att inkludera alla grenar.
   * **Ägare** - Din organisation eller ditt konto (krävs).
   * **Databasnamn** - Ett unikt namn för din nya repo (krävs).
   * **Beskrivning** - En kort beskrivning av ditt svar (valfritt).
   * **Offentlig eller privat** - Adobe rekommenderar public (standard).

1. Välj **Skapa databas**.

   Efter flera minuter öppnas din nya databas.

   Ignorera meddelanden om pull-begäran som visas i GitHub-användargränssnittet.

### Steg 3: Uppdatera storefront-mallsidan

Du behöver följande information för att kunna uppdatera koden för skyltplattan för butiken:

* **GitHub-databas-URL från steg 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` är organisationens namn eller användarnamn för databasen

   * `{SITE}` är ditt databasnamn

* **URL för innehållsmapp från steg 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` är ID:t för mappen som du skapade med exempelinnehållsdata.

#### Uppdatera mallkoden för att ansluta till innehållsmappen

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

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. Ersätt `{YOUR_MOUNTPOINT_URL}` med URL:en för din innehållsmapp.

      Om du till exempel använder Google Drive bör den uppdaterade koden se ut så här.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/1HXPWdQT-EK09IxVQV5HBSHN4QCA1a56Y
      ```

   1. Spara filen.

#### Granska dataanslutningskonfigurationen

Dataanslutningskonfigurationen upprättar kommunikation mellan storefront och den angivna [!DNL Adobe Commerce Optimizer]-instansen. Med den här anslutningen kan katalogdata flöda till butiken och fylla i olika butiksgränssnitt, inklusive sökkomponenten, produktlistan och produktinformationssidor.

Du ansluter till standardinstansen [!DNL Adobe Commerce Optimizer] med exempeldata för den första konfigurationen av butiken.

```json
{
  "public": {
    "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
        "cs": {
          "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
          "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
          "ac-price-book-id": "west_coast_inc",
          "ac-scope-locale": "en-US"
        }
      },
      "analytics": {
        "base-currency-code": "USD",
        "environment": "Production",
        "store-id": 1,
        "store-name": "ACO Demo",
        "store-url": "https://www.aemshop.net",
        "store-view-id": 1,
        "store-view-name": "Default Store View",
        "website-id": 1,
        "website-name": "Main Website"
      }
    }
  }
}
```

I den här filen anger följande nyckelvärden den [!DNL Adobe Commerce Optimizer]-instans som ska anslutas till och avgör vilka data som flödar till butiken:

* `commerce-endpoint` anger instansen som ska anslutas. Den är inställd på att använda standardinstansen [!DNL Adobe Commerce Optimizer]. Den här slutpunkten används för att hämta katalogdata.
* `ac-environment-id` är klientorganisations-ID för instansen [!DNL Adobe Commerce Optimizer].
* `headers` avgör vilka data som flödar från instansen till butiken.
   * `ac-channel-id` är inställt på `west_coast_inc`
   * `ac-price-book-id` är inställt på `west_coast_inc`
   * `ac-scope-locale` är inställt på `en-US`
   * `ac-price-book-id` är inställt på `west_coast_inc`

Dessa värden anger kanal-ID, språk och prisboks-ID för att skicka katalogdata till en viss försäljningskanal och filtrera dessa data baserat på angivna språk- och prisboksvärden. Senare uppdaterar du slutpunkten för att ansluta till [!DNL Adobe Commerce Optimizer]-instansen som Adobe har etablerat åt dig och ersätter rubrikvärdena för att hämta data från den instansen.

#### Konfigurera Sidekick-tillägget

Lägg till projektkonfigurationen för Sidekick-tillägget. Med den här konfigurationen kan du vara säker på att Sidekick är tillgängligt för att hantera innehåll för ditt butiksprojekt.

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

   * Ersätt strängen `{ORG}` med organisationen eller användarnamnet för din databas.

   * Ersätt strängen `{SITE}` med databasnamnet

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

+++

1. Spara filen.

### Steg 4: Överför den uppdaterade mallkoden

Om du vill använda den anpassade mallkoden för butiksskylt skriver du över koden på grenen `main` med dina uppdateringar.

1. Spara de uppdaterade filerna i redigeraren eller IDE-redigeraren.

   ```bash
   git add .
   ```

1. Kontrollera att du implementerar de två uppdaterade filerna.

   ```bash
   git status
   On branch aco
   Your branch is up to date with 'origin/aco'.
   
   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. Genomför ändringarna i grenen `aco`.

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Skriv över standardmallen i grenen `main` med ändringarna i grenen `aco`.

   ```bash
   git push origin aco:main -f
   ```

### Steg 5: Lägg till appen AEM Code Sync

Anslut databasen till Edge Delivery-tjänsten genom att lägga till appen AEM Code Sync GitHub i databasen.

>[!IMPORTANT]
>
>Anslut inte appen Code Sync förrän du har överfört den uppdaterade mallkoden till huvudgrenen i GitHub-databasen.

1. Öppna konfigurationssidan för [AEM Code Sync-appen](https://github.com/apps/aem-code-sync).

1. Välj **Konfigurera** och autentisera sedan med det **företag** eller **konto** som innehåller databasen som du skapade.

1. Välj **Markera endast databaser** i formuläret och välj den databas du skapade.

1. Välj **Installera** om du vill lägga till appen AEM Code Sync i din databas.

   Du bör se ett meddelande om att appen har installerats.

### Steg 6: Förhandsgranska och publicera ditt innehåll

Om du vill lägga till innehåll i butiken förhandsgranskar och publicerar du butiksinnehållet med Sidekick-tillägget.

1. Öppna innehållsmappen i Google Drive eller Sharepoint.

1. Aktivera Sidekick genom att klicka på ikonen Sidekick i webbläsarens verktygsfält.

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

   Om du inte ser ikonen Sidekick kontrollerar du att Sidekick konfigurationsfil `tools/Sidekick/config.json` i `main`-grenen i din GitHub-databas är [korrekt konfigurerad](#configure-the-sidekick-extension).

1. Använd Sidekick verktygsfält för att förhandsgranska och publicera ditt innehåll.

   ![[Välj filer som ska förhandsgranskas och publiceras]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

   Markera filerna i respektive mapp separat och använd verktygsfältet i Sidekick för att förhandsgranska och publicera alla filer.

   * **Förhandsgranska**-Överför innehåll till mellanlagringsmiljön. Lagringsutrymmet för mellanlagrings-URL:er avslutas med `.aem.page`.

   * **Publicera**-Överför innehåll till produktionsmiljön. Produktions-URL:er avslutas med `aem.live`.

Mer information finns i dokumentationen för Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick).

### Steg 7: Förhandsgranska webbplatsen

Kontrollera att exempelinnehållet och data från Adobe Commerce Optimizer demoinstans visas korrekt.

* **Exempelinnehåll** hämtas från din delade innehållsmapp. Det innehåller sidlayouter, banners och annat innehåll som du publicerat med Sidekick.
* **Exempeldata** skickas från demoinstansen [!DNL Adobe Commerce Optimizer]. Data innehåller produktdata med produktattribut, bilder, produktbeskrivningar och priser ifyllda baserat på rubrikvärdena som anges i konfigurationsfilen för butiken, `config.json`.


#### Anslut till webbplatsen för att visa exempelinnehåll och data

1. Anslut till din webbplats genom att navigera till `https://main--{SITE}--{ORG}.aem.live`.

   Ersätt `{ORG}` och `{SITE}` med organisationen och namnet för din standarddatabas.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Om sidan returnerar 404 kontrollerar du att du har publicerat innehållet med Sidekick-tillägget. Dubbelkontrollera också att monteringspunkten i den uppdaterade `fstab.yaml`-filen pekar på innehållsmappen som du skapade.

1. Visa exempelkatalogdata som kommer från Commerce Optimizer standardinstans.

   1. Sök efter `tires` om du vill visa en listruta med tillgängliga däckprodukter.

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   Sökkomponenten är en del av den främre mallkoden. Sökresultatdata fylls i baserat på butikskonfigurationen i `config.json`.

   1. Tryck på **Retur** för att visa sidan med produktlistan.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. Visa en produktinformationssida genom att välja en däckprodukt på sidan.

      Lägg märke till att vissa komponenter inte fungerar om du utforskar butiken. Om du till exempel lägger till en produkt i kundvagnen returneras ett fel och kontohanteringskomponenterna fungerar inte. Dessa problem uppstår eftersom de här komponenterna inte har konfigurerats för att ta emot data från en Commerce-backend. Data från instansen [!DNL Adobe Commerce Optimizer] fyller bara i sidorna för sökkomponenten, produktlistan och produktinformationen.

   1. När du har utforskat butiken fortsätter du med självstudiekursen.


### Steg 8: Utveckla butiken i den lokala miljön

I det här avsnittet uppdaterar du butikskonfigurationen från den lokala utvecklingsmiljön.

* Uppdatera butikskonfigurationen för att ansluta till GraphQL-slutpunkten för instansen [!DNL Adobe Commerce Optimizer] som Adobe har etablerat åt dig.
* Uppdatera rubrikvärdena för att hämta data från din instans.

#### Starta lokal utveckling

1. I din utvecklingsmiljö ska du kontrollera huvudgrenen i din GitHub-koddatabas.

   ```bash
   git checkout main
   ```

1. Installera nödvändiga beroenden.

   ```bash
   npm install
   ```

1. Starta den lokala utvecklingsservern.

   ```bash
   npm start
   ```

   Den första sidan i mallbutiken ska vara synlig i webbläsaren på `http://localhost:3000`.

![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Uppdatera butikskonfigurationen

Uppdatera konfigurationsfilen för butiken och förhandsgranska ändringarna i den lokala utvecklingsmiljön.


1. I din IDE ska du uppdatera butikskonfigurationen så att den ansluter till [!DNL Adobe Commerce Optimizer]-instansen som Adobe har etablerat åt dig.

   1. Öppna filen `config.json`.

   1. Uppdatera följande värden med slutpunkten för instansen [!DNL Adobe Commerce Optimizer]:

      * **`commerce-endpoint`**-Ersätt det befintliga värdet med din slutpunkts-URL.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`** - Ersätt det befintliga värdet med klient-ID från din slutpunkts-URL.

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. Spara filen.

      Om den lokala förhandsvisningen fungerar som den ska används uppdateringarna i din lokala butik.

1. Kontrollera platsen för att se resultatet av konfigurationsändringen.

   1. Navigera till `http://localhost:3000` i webbläsaren och uppdatera sidan.

   1. Klicka på förstoringsglaset i butikshuvudet för att söka efter `tires`.

      ![Sök efter däck](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

      Observera att listrutan inte fylls i.

   1. Tryck på **Retur** för att visa sidan med produktlistan.

      ![Tomma sökresultat med ogiltiga huvudvärden](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      Sökningen returnerar inga resultat eftersom rubrikvärdena i konfigurationsfilen för butiken baseras på standardinstansen. Nu när konfigurationen pekar på den [!DNL Adobe Commerce Optimizer]-instans som har etablerats åt dig är dessa värden ogiltiga.

### Nästa steg

Se [Handboken för Storefront och katalogadministratören från början till slut](./use-case/admin-use-case.md) om du vill veta mer om hur du hanterar och visar innehåll och data i butiken.

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager storefront-dokumentation](https://experienceleague.adobe.com/developer/commerce/storefront/) om du vill veta mer om hur du uppdaterar webbplatsinnehåll och integrerar med dina klientkomponenter och backend-data för Commerce.
></br></br>
>* [Adobe Commerce Storefront-dokumentation](https://experienceleague.adobe.com/developer/commerce/storefront/) om du vill veta mer om hur du uppdaterar webbplatsinnehåll och integrerar med Adobe Commerce klientkomponenter och backend-data.
