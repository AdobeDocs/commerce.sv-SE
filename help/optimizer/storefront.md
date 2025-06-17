---
title: Konfigurera din butik
description: Lär dig hur du konfigurerar din  [!DNL Adobe Commerce Optimizer] butik.
role: Developer
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 134e5faeb13c37e10ccd14ae2b43f788c7d39d06
workflow-type: tm+mt
source-wordcount: '1808'
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

   * **Databasmall**—`hlxsites/aem-boilerplate-commerce` (standard).
   * **Inkludera alla grenar** - Välj alternativet att inkludera alla grenar.
   * **Ägare** - Din organisation eller ditt konto (krävs).
   * **Databasnamn** - Ett unikt namn för din nya repo (krävs).
   * **Beskrivning** - En kort beskrivning av ditt svar (valfritt).
   * **Offentlig eller privat** - Adobe rekommenderar public (standard).

1. Välj **Skapa databas**.

   Efter flera minuter öppnas din nya databas.

   Ignorera meddelanden om pull-begäran som visas i GitHub-användargränssnittet.

### Steg 2: Uppdatera storefront-skylten

Du behöver följande information för att kunna uppdatera koden för skyltplattan för butiken:

* **GitHub-databas-URL från steg 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` är organisationens namn eller användarnamn för databasen

   * `{SITE}` är ditt databasnamn

* **URL för innehållsmapp från steg 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` är ID:t för mappen som du skapade med exempelinnehållsdata.

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

### Steg 3: Distribuera ändringar

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

1. Välj **Markera endast databaser** i formuläret och välj sedan den databas som du skapade.

1. Välj **Installera** om du vill lägga till appen AEM Code Sync i din databas.

   Du bör se ett meddelande om att appen har installerats.

### Steg 6: Lägg till innehåll

Skapa och initiera ditt butiksinnehåll i dokumentredigeringsmiljön på `https://da.live` med hjälp av verktyget Platsskapare. Det här verktyget importerar exempelinnehållet till dokumentförfattarmiljön och slutför innehållsförhandsgranskningen och publiceringsprocessen för alla dokument i exempelinnehållet. Exempelinnehållet innehåller sidlayouter, banderoller, etiketter och andra element som fyller i butiken.

1. Öppna [webbplatsskaparverktyget](https://da.live/hlxsites/aem-boilerplate-commerce/tools/site-creator/site-creator).

1. Konfigurera din databas:

   * Välj **[!UICONTROL Use Existing Repository]**.
   * Ange **[!UICONTROL Organization/Username]** för ditt storefront-mallprojekt.
   * Ange **[!UICONTROL Repository Name]**.

1. Importera, förhandsgranska och publicera innehållet i dokumentförfattarmiljön genom att välja **Skapa webbplats**.

   ![[!DNL AEM demo content clone tool]](./assets/storefront-edit-initial-content.png){width="700" zoomable="yes"}

   När webbplatsen har skapats kan du använda länkarna i avsnitten [!UICONTROL Edit content] och [!UICONTROL View Site] för att utforska demobutiken.

   Huvudlänkarna till ditt innehåll och din webbplats har följande format:

   * **Rotinnehållsmapp**— `https://da.live/#/{ORG}/{SITE}`
   * **Förhandsgranskning av webbplats**—   `https://main--{SITE}--{ORG}.aem.page/`
   * **Platsproduktion:**— `https:/main--{SITE}--{ORG}.ae.live/`

1. Öppna länken till rotinnehållsmappen för att visa innehållet.

   ![[!DNL Storefront Document Author environment]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   >[!TIP]
   >
   >Använd länkarna [!UICONTROL **Lär dig**] och [!UICONTROL **Upptäck**] för att komma åt utbildningsresurser för att hantera din webbplats och ditt webbplatsinnehåll.

### Steg 7: Förhandsgranska demowebbplats

Kontrollera att exempelinnehållet och data från Adobe Commerce Optimizer demoinstans visas korrekt.

* **Exempelinnehåll** hämtas från innehållsmappen i dokumentförfattarmiljön. Den innehåller sidlayouter, banners och etiketter för din webbplats.
* **Exempeldata** skickas från demoinstansen [!DNL Adobe Commerce Optimizer]. Data innehåller produktdata med produktattribut, bilder, produktbeskrivningar och priser ifyllda baserat på rubrikvärdena som anges i konfigurationsfilen för butiken, `config.json`.

#### Anslut till webbplatsen för att visa exempelinnehåll och data

1. Visa din webbplats genom att navigera till `https://main--{SITE}--{ORG}.aem.live`.

   Ersätt `{ORG}` och `{SITE}` med organisationen och namnet för din standarddatabas.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Om sidan returnerar 404 kontrollerar du följande:

   * [Monteringspunkten i `fstab.yaml`-filen pekar på rätt innehålls-URL](#link-the-repository-to-the-document-author-environment): `https://content.da.live/{ORG}/{SITE}/`
   * [Du har konfigurerat appen Kodsynkronisering för att ansluta till din GitHub-databas](#step-5%3A-add-the-aem-code-sync-app).
   * [Du har publicerat innehållet i dokumentförfattarmiljön med hjälp av klonverktyget för demoinnehåll](#step-6%3A-add-content-documents-for-your-storefront).


1. Visa exempelkatalogdata som kommer från Commerce Optimizer standardinstans.

   1. Klicka på förstoringsglaset i butikshuvudet för att söka efter `tires`.

      ![[!DNL View product list page]](./assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

   1. Tryck på **Retur** för att visa sökresultatsidan.

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

      Komponenterna för sökresultatsidan definieras av `search`-innehållsdokumentet. Sökresultatdata fylls i baserat på butikskonfigurationen i `config.json`.

   1. Visa sidan med produktinformation genom att välja en däckprodukt på sidan.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

      Sidkomponenterna för produktinformation definieras av `default`-innehållsdokumentet i mappen `product`.

### Steg 8: Utveckla i din lokala miljö

I det här avsnittet uppdaterar du butikskonfigurationen från den lokala utvecklingsmiljön.

* Uppdatera butikskonfigurationen för att ansluta till GraphQL-slutpunkten för instansen [!DNL Adobe Commerce Optimizer] som Adobe har etablerat åt dig.
* Uppdatera rubrikvärdena för att hämta data från din instans.

#### Starta lokal utveckling

1. I din utvecklingsmiljö checkar du ut huvudgrenen och återställer den till den senaste implementeringen på fjärrgrenen.

   ```bash
   git checkout main
   git reset --hard origin/main
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

   1. Tryck på **Retur** för att visa sidan Sökresultat.

      ![Tomma sökresultat med ogiltiga huvudvärden](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      Sökningen returnerar inga resultat eftersom rubrikvärdena i konfigurationsfilen för butiken baseras på standardinstansen. Nu när konfigurationen pekar på den [!DNL Adobe Commerce Optimizer]-instans som har etablerats åt dig är dessa värden ogiltiga.

### Nästa steg

Se [Handboken för Storefront och katalogadministratören från början till slut](./use-case/admin-use-case.md) om du vill veta mer om hur du hanterar och visar innehåll och data i butiken.

>[!MORELIKETHIS]
>
> Läs [dokumentationen för Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) om du vill veta mer om hur du uppdaterar webbplatsinnehåll och integrerar med komponenterna i Commerce Front och backend-data.
