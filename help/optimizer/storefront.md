---
title: Konfigurera din butik
description: Lär dig hur du konfigurerar din  [!DNL Adobe Commerce Optimizer] butik.
role: Developer
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# Konfigurera din butik

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

I den här självstudiekursen visas hur du konfigurerar och använder [Adobe Commerce Storefront från Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=sv-SE) för att skapa en prestanda, skalbar och säker Commerce Storefront som drivs av data från din [!DNL Adobe Commerce Optimizer]-instans.


## Förutsättningar

* Se till att du har ett GitHub-konto (github.com) som kan skapa databaser och är konfigurerat för lokal utveckling.

* Bekanta dig med grundläggande arbetsflöden och vokabulär som är kopplade till att skapa en butik för Adobe Edge Delivery Services genom att läsa [översikten](https://experienceleague.adobe.com/developer/commerce/storefront/get-started?lang=sv-SE) i dokumentationen för Adobe Commerce Storefront.
* Konfigurera utvecklingsmiljön


### Konfigurera utvecklingsmiljön

Installera den version av Node.js och webbläsartillägget Sidekick som krävs för att konfigurera din utvecklingsmiljö.

#### Installera Node.js

Om du vill utveckla och testa din [!DNL Adobe Commerce Optimizer]-butik på Edge Delivery Services-projekt lokalt behöver du Node.js version 22.13.1 LTS.

Om det behövs utför du följande steg för att installera Node Version Manager (NVM) och den nödvändiga Node.js-versionen.

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
>Den här konfigurationen används för utveckling med [!DNL Adobe Commerce Optimizer] och Adobe Commerce Edge Delivery Service Store. Ytterligare resurser för att utöka och anpassa din [!DNL Adobe Commerce Optimizer]-lösning finns tillgängliga via [App Builder för Adobe Commerce](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) och [API Mesh för Adobe Developer App Builder](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Kontakta din Adobe-representant om du vill ha information om åtkomst och användning.

#### Installera Sidekick

Installera Sidekick webbläsartillägg om du vill redigera, förhandsgranska och publicera butiksinnehåll. Se [Installationsanvisningar för Sidekick](https://www.aem.live/docs/sidekick#installation).


## Skapa en butik

Det butiksområde du skapar för ditt [!DNL Adobe Commerce Optimizer]-projekt byggs med en anpassad version av Adobe Commerce på Edge Delivery Services Storefront-mallsidan. Mallen är en uppsättning filer och mappar som utgör en startpunkt för att skapa butiken.

Den här konfigurationsprocessen för butiken har anpassats specifikt för [!DNL Adobe Commerce Optimizer] projekt. Flödet skiljer sig från flödet för standardinställningen [Adobe Commerce på Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=sv-SE).

>[!NOTE]
>
>I den här självstudien används macOS, Chrome och Visual Studio Code som utvecklingsmiljö. Skärmen visar inställningarna och instruktionerna. Du kan använda ett annat operativsystem, en annan webbläsare och en annan kodredigerare, men det gränssnitt du ser och de steg du måste utföra varierar beroende på hur du gör.

### Översikt över arbetsflödet

Följ de här stegen för att konfigurera en butik som ska användas med Adobe Commerce Optimizer.

1. **[Skapa en innehållsmapp](#step-1-create-a-content-folder)**-Skapa en delad innehållsmapp i Google Drive eller Sharepoint. Den här mappen innehåller exempelinnehåll och resurser för din butik.

1. **[Skapa en koddatabas](#step-1-create-a-code-repository)**-Skapa en GitHub-databas från standardmallen Adobe Commerce + Edge Delivery Services. Inkludera alla grenar från källdatabasen.
1. **[Uppdatera skylten för lagerfront](#step-2-update-the-storefront-boilerplate)**-Uppdatera den anpassade mallen för mallsidor på grenen `aco` i databasen för att ansluta innehållsmappen till butiken, och granska butikskonfigurationen som levererar data från Adobe Commerce Optimizer demoinstans till butiken.
1. **[Ladda upp den uppdaterade butiksskyltkoden](#step-3-upload-the-updated-boilerplate-code)**-Skriv över koden i grenen `main` med den uppdaterade koden från grenen `aco`.
1. **[Lägg till appen CodeSync](#step-4-add-the-aem-code-sync-app)**-Anslut din databas till Edge Delivery-tjänsten. Anslut inte appen Code Sync förrän du har slutfört anpassningen av källkoden och är redo att skicka koden till grenen `main`.
1. **[Förhandsgranska och publicera ditt innehåll](#step-5-preview-and-publish-your-content)**-Använd Sidekick-tillägget för att förhandsgranska och publicera webbplatsinnehållet från innehållsmappen till butiken.
1. **[Förhandsgranska webbplatsen och visa exempeldata](#step-6-preview-your-site-and-view-sample-data)**-Anslut till din butiksplats för att visa exempelinnehåll och data från demoinstansen [!DNL Adobe Commerce Optimizer].
1. **[Utveckla butiken i den lokala miljön](#step-7-develop-the-storefront-in-your-local-environmentdevelop-the-storefront-in-your-local-environment)**-Installera de nödvändiga beroendena. Starta den lokala utvecklingsservern och uppdatera butikskonfigurationen för att ansluta till [!DNL Adobe Commerce Optimizer]-instansen som Adobe har etablerat åt dig.
1. **[Hantera webbplatsinnehåll](#step-8-manage-site-content)** - Läs mer om att uppdatera och hantera webbplatsinnehåll.

### Steg 1: Skapa en innehållsmapp

Följ instruktionerna i dokumentationen för Adobe Commerce Storefront för att lägga till en delad innehållsmapp i Google Drive eller Sharepoint och lägga till exempelinnehållet. Exempelinnehållet innehåller bilder, text och andra resurser som utgör din plats.

* [Skapa och dela en Google Drive- eller Sharepoint-mapp](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=sv-SE#create-and-share-folder)
* [Läs in exempelinnehållet](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=sv-SE#add-sample-content) i din mapp.

### Steg 2: Skapa en koddatabas

Skapa en koddatabas i GitHub med mallen Edge Delivery Services + Adobe Commerce Boilerplate. Den här mallen innehåller mallkoden för butiken.

1. Logga in på ditt GitHub-konto.

1. Navigera till GitHub-databasen [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) .

1. Välj **Använd den här mallen** och välj sedan **Skapa en ny databas** i listrutan.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Då öppnas konfigurationssidan för databasen.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Fyll i konfigurationsformuläret med följande information:

   * **Databasmall**—`hlxsites/aem-boilerplate-commerce` (standard).
   * **Inkludera alla grenar** - Välj alternativet att inkludera alla grenar.
   * **Ägare** - Din organisation eller ditt konto (krävs).
   * **Databasnamn** - Ett unikt namn för din nya repo (krävs).
   * **Beskrivning** - En kort beskrivning av ditt svar (valfritt).
   * **Offentlig eller privat** - Adobe rekommenderar public (standard).

1. Välj **Skapa databas**.

   Efter en minut eller två öppnas din nya databas.

   Ignorera meddelanden om pull-begäran som visas i den nya rapporten.

### Steg 3: Uppdatera storefront-mallsidan

I det här avsnittet utför du följande uppgifter:

* Kolla in grenen `aco` i din databas för att uppdatera den anpassade mallmallen för mallar för [!DNL Adobe Commerce Optimizer]-projekt
* Anslut innehållsmappen till butiken genom att uppdatera filen `fstab.yaml` så att den pekar på innehållsmappen.
* Granska konfigurationsfilen för butiken, `config.json`
* Konfigurera Sidekick-tillägget för att redigera, förhandsgranska och publicera innehåll från din delade innehållsmapp.

Du behöver följande information för att kunna utföra dessa steg:

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

1. Uppdatera konfigurationsfilen för butiken så att den pekar på innehålls-URL:en.

   1. Öppna konfigurationsfilen [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=sv-SE#vocabulary).

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. Ersätt `{YOUR_MOUNTPOINT_URL}` med URL:en för ditt innehållshanteringssystem.

      Om du till exempel använder Google Drive bör den uppdaterade koden se ut så här.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}
      ```

   1. Spara filen.

#### Granska dataanslutningskonfigurationen

Dataanslutningen upprättar kommunikation mellan Adobe Commerce Optimizer och butiken, vilket säkerställer att katalogdata smidigt flödar till butiken. Den här processen fyller i olika butiksgränssnitt, inklusive sökkomponenten, produktlistan och produktinformationssidor som krävs för [!DNL Adobe Commerce Optimizer].

För den första konfigurationen av storefront tillhandahåller Adobe en standardkonfigurationsfil som ansluter till en Adobe Commerce Optimizer demo-instans med exempeldata.

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

Granska konfigurationsfilen för butiken i din databas för att förstå hur dataanslutningen upprättas.

1. Gå till rotkatalogen i koddatabasen.

1. Öppna filen `config.json`.

   I den här filen anger följande nyckelvärden den Adobe Commerce Optimizer-instans som ska anslutas till och avgör vilka data som flödar till butiken:

   * `commerce-endpoint` definierar den Adobe Commerce Optimizer-instans som ska anslutas till.
   * `headers` avgör vilka data som flödar till butiken.
      * `ac-channel-id` är inställt på `west_coast_inc`
      * `ac-price-book-id` är inställt på `west_coast_inc`
      * `ac-scope-locale` är inställt på `en-US`
      * `ac-price-book-id` är inställt på `west_coast_inc`

   Dessa värden anger kanal-ID, språk och prisboks-ID för att skicka katalogdata till en viss försäljningskanal och filtrera dessa data baserat på angivna språk- och prisboksvärden. Senare får du lära dig hur du ändrar Adobe Commerce Optimizer-instansen och uppdaterar rubrikerna för att definiera vilka data som ska skickas till butiken.

1. När du har granskat filen stänger du den och fortsätter med självstudiekursen.


#### Konfigurera Sidekick-tillägget

Lägg till projektkonfigurationen för Sidekick-tillägget. Sidekick används för att redigera, förhandsgranska och publicera ditt butiksinnehåll. Med den här konfigurationen kan du använda Sidekick för att hantera innehåll både i din delade innehållsmapp och på webbplatssidor som publiceras i staging- och produktionsmiljöerna.

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

   * `{ORG}` är databasnamnet eller användarnamnet för koddatabasen

   * `{SITE}` är databasnamnet

1. Spara filen.

### Steg 4: Överför den uppdaterade mallkoden

Om du vill använda den anpassade mallkoden för butiksskylt skriver du över koden på grenen `main` med dina uppdateringar.

1. Spara de uppdaterade filerna i redigeraren eller IDE-redigeraren.

   ```bash
   git add .
   ```

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Skjut ändringarna på grenen `aco` och skriv över grenen `main`:

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

Om du vill lägga till innehåll i din butik måste du förhandsgranska och publicera ditt innehåll med Sidekick-tillägget.

1. Öppna innehållsmappen i Google Drive eller Sharepoint.

1. Aktivera Sidekick genom att klicka på ikonen Sidekick i webbläsarens verktygsfält.

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

1. Använd Sidekick verktygsfält för att förhandsgranska och publicera ditt innehåll.

   ![[Välj filer som ska förhandsgranskas och publiceras]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

1. Markera filerna i respektive mapp separat och använd verktygsfältet i Sidekick för att förhandsgranska och publicera alla filer.

   * **Förhandsgranska**-Överför innehåll till mellanlagringsmiljön. Lagringsutrymmet för mellanlagrings-URL:er avslutas med `.aem.page`.

   * **Publicera**-Överför innehåll till produktionsmiljön. Produktions-URL:er avslutas med `aem.live`.

Mer information finns i dokumentationen för Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick).

### Steg 7: Förhandsgranska webbplatsen

Förhandsgranska webbplatsen för att verifiera att både exempelinnehållet och Adobe Commerce Optimizer demodata visas korrekt.

* **Exempelinnehåll** hämtas från din delade innehållsmapp. Det innehåller sidlayouter, banners och annat innehåll som du publicerat med Sidekick.
* **Exempeldata** skickas från demoinstansen [!DNL Adobe Commerce Optimizer]. Data innehåller produktdata med produktattribut, bilder, produktbeskrivningar och priser ifyllda baserat på värdena som anges i konfigurationsfilen för butiken, `config.json`.


#### Anslut till webbplatsen för att visa exempelinnehåll och data

1. Anslut till din webbplats genom att navigera till `https://main--{SITE}--{ORG}.aem.live`.

   Ersätt `{ORG}` och `{SITE}` med organisationen och namnet för din standarddatabas.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Om sidan returnerar 404 kontrollerar du att du har publicerat innehållet med Sidekick-tillägget. Kontrollera också att den uppdaterade `fstab.yaml`-filen använder URL:en för innehållsmappen.

1. Visa exempelkatalogdata som kommer från Commerce Optimizer demoinstans.

   1. Sök efter `tires` om du vill visa en listruta med tillgängliga däckprodukter.

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   Sökkomponenten är en del av den främre mallkoden. Sökresultatdata fylls i baserat på butikskonfigurationen.

   1. Tryck på **Retur** för att visa sidan med produktlistan.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. Visa en produktinformationssida genom att välja en däckprodukt på sidan.

      Lägg märke till att vissa komponenter inte fungerar om du utforskar butiken. Om du till exempel lägger till en produkt i kundvagnen returneras ett fel och kontohanteringskomponenterna fungerar inte. Detta beror på att dessa komponenter inte har konfigurerats för att ta emot data från en Commerce-serverdel. Data från din Adobe Commerce Optimizer-instans fyller endast i sidorna för sökkomponent, produktlista och produktinformation.

   1. När du har utforskat butiken fortsätter du med självstudiekursen.


### Steg 8: Utveckla butiken i den lokala miljön

I det här avsnittet experimenterar du med butikskonfigurationen i den lokala utvecklingsmiljön genom att ansluta butiken till [!DNL Adobe Commerce Optimizer]-instansen som Adobe har etablerat åt dig.

För att kunna upprätta anslutningen behöver du GraphQL-slutpunkten för Merchandising Services som fanns i ditt e-postmeddelande om introduktion.

```text
https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

#### Starta lokal utveckling

1. I din utvecklingsmiljö checkar du ut huvudgrenen i din GitHub-koddatabas.

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

      Sökningen returnerar inga resultat eftersom rubrikerna i konfigurationsfilen för butiken använder rubrikvärden som baseras på demoinstansen. Nu när konfigurationen pekar på den [!DNL Adobe Commerce Optimizer]-instans som har etablerats åt dig är dessa värden ogiltiga.

### Nästa steg

I [Storefront och katalogadministratörens kompletta användningsexempel](./use-case/admin-use-case.md) kan du lära dig hur du visar innehåll i butiken genom att uppdatera butikskonfigurationen med värden från [!DNL Adobe Commerce Optimizer]-instansen.

>[!MORELIKETHIS]
>
>* Om du tänker använda [!DNL Adobe Commerce Optimizer] utan Adobe Commerce-serverdel kan du läsa [ Adobe Experience Manager storefront-dokumentationen](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE) om du vill veta mer om hur du uppdaterar webbplatsinnehåll och integrerar med Commerce klientkomponenter och backend-data.
></br></br>
>* Om du tänker använda [!DNL Adobe Commerce Optimizer] med en Adobe Commerce-serverdel kan du läsa [ Adobe Commerce Storefront-dokumentationen ](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE) för att lära dig hur du uppdaterar innehåll och konfigurerar butikskomponenter för kontohantering, utcheckning och andra funktioner.
