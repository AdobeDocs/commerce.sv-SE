---
title: Konfigurera din butik
description: Lär dig hur du konfigurerar din  [!DNL Adobe Commerce Optimizer] butik.
role: Developer
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och [!DNL Adobe Commerce Optimizer] projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: e46c55cba21501c6fa12db6c130493b99de0e4da
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 0%

---

# Konfigurera din butik

I den här guiden får du hjälp med att konfigurera en butiksadress för din [!DNL Adobe Commerce Optimizer]-instans med Adobe Edge Delivery Services. Din butik innehåller standardkod, exempelinnehåll och stöd för produktinformationssidor och produktidentifiering (sökning och filtrering).

**Beräknad tid för slutförande:** 30-45 minuter

## Förutsättningar

* **GitHub-konto** som kan skapa databaser och är konfigurerat för lokal utveckling (github.com)
* **[!DNL Adobe Commerce Optimizer]instans** med exempeldata och konfigurerade katalogvyer och principer
   * Se [Lägg till exempeldata](get-started.md#add-sample-data) för installationsanvisningar.

### Nödvändiga instansdata

Innan du börjar samlar du in följande information från din [!DNL Adobe Commerce Optimizer]-instans:

* **Klient-ID** (kallas även instans-ID)
   * Tillgängligt från sidan [med instansinformation](get-started.md#manage-instances)
* **GraphQL-slutpunkt** för din instans
   * Tillgängligt från sidan [med instansinformation](get-started.md#manage-instances)
* **Katalogvy-ID** för den globala katalogvyn
   * Tillgänglig från sidan [Kataloginformation](./setup/catalog-view.md#manage-catalog-view)
* **Source-språk** för katalogvyn
   * Standardvärdet för exempeldata är `en-US`

>[!NOTE]
>
>Kunder som har tillgång till testversionen hittar GraphQL-slutpunkten i det välkomstmeddelande som togs emot när din instans skapades. Testinstanser är förkonfigurerade med exempeldata, katalogvyer och principer.

## Konfigurera steg

1. **[Skapa ditt storefront-projekt](#create-your-storefront-project)**-Använd verktyget [Site Creator](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) för att skapa ett nytt storefront-projekt med mallkod, exempelinnehåll och en konfigurationsfil.

1. **[Anpassa butikskonfigurationen](#customize-the-storefront-configuration)**-Uppdatera `config.json`-filen i databasen för att ansluta till [!DNL Adobe Commerce Optimizer]-instansen.

1. **[Verifiera installationen](#verify-your-setup)** (10 minuter)
   * Förhandsgranska webbplatsen för butiken
   * Testa produktinformationssidor och sökfunktioner

## Skapa ett butiksprojekt

Med verktyget Site Creator kan du skapa ett helt butiksprojekt med följande komponenter:

* **Plats**: Startsida för butiken med standardinnehåll
* **Kod**: Databas med mallkällfiler
* **Innehåll**: Dokumentförfattarmiljö med webbplatsinnehållsfiler
* **Commerce Config**: `config.json`-fil för instansspecifik konfiguration

### Steg 1: Generera ditt projekt

1. Öppna [verktyget Webbplatsskapare](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Välj **Skapa ny plats (kod och innehåll)**.

1. Slutför platskonfigurationen:

   * **GitHub-organisation/användarnamn**: Ange ditt GitHub-användarnamn eller -organisationsnamn
   * **Platsnamn**: Välj ett beskrivande namn för butiken
   * **Commerce GraphQL Endpoint (valfritt)**: Ange GraphQL-slutpunkten för din [!DNL Adobe Commerce Optimizer]-instans

1. Klicka på **Skapa plats** om du vill skapa GitHub-databasen med standardkoden för lagerfront.

   När databasen har skapats uppdateras Site Creator och du uppmanas att installera appen Code Sync.

### Steg 2: Installera appen Code Sync

1. Klicka på **[!UICONTROL Install AEM Code Sync App]** för att öppna installationsprogrammet för kodsynkronisering på en ny flik.

1. Konfigurera appen Kodsynkronisering:
   * Välj din GitHub-organisation och klicka sedan på **[!UICONTROL Configure]**.
   * Klicka på **[!UICONTROL Only select repositories]** i kodsynkroniseringsgränssnittet.
   * Klicka på menyn **[!UICONTROL Select repositories]** och välj sedan lagringskoddatabasen som du skapade.
   * Klicka på **[!UICONTROL Save]** för att registrera databasen.

1. Gå tillbaka till webbläsarfönstret där Site Creator är öppet och klicka på **Create Site**.

   Webbplatsskaparen kopierar det främre mallinnehållet till dokumentförfattarmiljön. Den här processen tar 1-2 minuter.

### Steg 3: Spara projektlänkar

1. Granska länkarna till ditt butiksprojekt i delen Platsinformation:

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   Använd de här länkarna för att hantera kod, innehåll och konfiguration för butiken.

1. Kopiera och spara länkarna för framtida referens: Klicka på **[!UICONTROL Copy].

## Konfigurera din butik

Uppdatera din butikskonfiguration för att ansluta till din [!DNL Adobe Commerce Optimizer]-instans.

1. Öppna filen `config.json` i din standardkoddatabas.

   `https://github.com/<username or org>/<repo name>/config.json`

1. Leta reda på avsnittet `cs` (katalogtjänst) i konfigurationen.

1. Ersätt platshållarvärdena med värdena för instansen. Se [Krav](#prerequisites).

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en-US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >Om du vill hitta prisbokens ID kan du kontrollera [katalogvyns konfigurationsinformation](./setup/catalog-view.md) i Adobe Commerce Optimizer för att se de tilldelade prisböckerna. Om inga prisböcker har tilldelats kan du ta bort den här rubriken från konfigurationsfilen. Lägg tillbaka den när en prisbok har tilldelats katalogvyn.

1. Spara konfigurationsfilen.

   Det kan ta några minuter att sprida konfigurationsändringarna. Om du inte ser data direkt, vänta 2-3 minuter innan du felsöker.

## Verifiera installationen

Testa din butik för att kontrollera att den är korrekt ansluten till din [!DNL Adobe Commerce Optimizer]-instans.

### Steg 1: Visa din startsida för butiken

1. Navigera till webbadressen för direktförhandsvisning:

   `https://main--{SITE}--{ORG}.aem.live`

   Ersätt `{ORG}` och `{SITE}` med din GitHub-organisation och ditt webbplatsnamn.

1. **Villkor för lyckade**: Du bör se butikens startsida med mallinnehåll.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### Steg 2: Testa produktinformationssidor

Visa standardinformationssidan för att kontrollera att produktdata läses in korrekt.

1. Navigera till en exempelproduktsida:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   Använd valfri SKU från exempeldata, till exempel:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   För standardbutiken kan du använda värdet `placeholder` i vägen för att visa produkten. När du börjar anpassa din butik kan du anpassa storefront-koden för att ange sökvägen till produktinformationssidan baserat på de produktvägar som definierats i din katalog.

   >[!TIP]
   >
   >Visa tillgängliga SKU:er från sidan [Datasynkronisering](./setup/data-sync.md) i din [!DNL Adobe Commerce Optimizer]-instans.

1. **Slutförandevillkor**: Sidan ska visas:
   * Produktnamn, beskrivning och prissättning
   * Produktbilder
   * Lägg till i kundvagnen
   * Data har hämtats från din [!DNL Adobe Commerce Optimizer]-instans

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### Steg 3: Testa standardsökfunktionen

Testa standardfunktionerna, inklusive sökning och filtrering.

1. På butikens startsida klickar du på förstoringsglaset i sidhuvudet.

1. Skriv söksträngen `tires` och tryck på **Retur**.

1. **Slutförandevillkor**: Du bör se:
   * Sökresultatsida med däckprodukter
   * Filtreringsalternativ i sidofältet
   * Produktlistor med bilder och priser

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. Klicka på en däckprodukt för att visa detaljsidan.

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## Felsökning

Om du stöter på problem under installationen kan du söka efter fel med hjälp av webbsidans konsol. Försök även rensa webbläsarens cache eller använda en annan webbläsare.

Använd följande vägledning för att kontrollera vanliga problem:

### Vanliga problem

| Problem | Symtom | Lösning |
|-------|----------|----------|
| **Installationen av kodsynkronisering misslyckas** | Det gick inte att slutföra kodsynkroniseringsinstallationen | <ul><li>Se till att du har administratörsåtkomst till din GitHub-organisation.</li><li>Försök använda en personlig databas istället för en organisation.</li><li>Kontrollera GitHub-behörigheter och försök igen.</li></ul> |
| **Webbplatsen läses inte in** | 404 eller anslutningsfel | <ul><li>Verifiera URL-formatet för din plats: `https://main--{SITE}--{ORG}.aem.live`</li><li>Kontrollera att appen Code Sync är korrekt installerad.</li><li>Se till att databasen är offentlig eller korrekt konfigurerad.</li></ul> |
| **Inga produktdata visas** | På produktsidor visas platshållare eller fel | <ul><li>Verifiera dina konfigurationsvärden i `config.json`</li><li>Kontrollera sidan Datasynkronisering i instansen [!DNL Adobe Commerce Optimizer] för att bekräfta att exempelprodukterna har lästs in. Om inga produkter är tillgängliga läser du in exempeldata igen eller lägger till en produkt med [API:t för datainmatning](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request). Vänta några minuter tills konfigurationsändringarna har spridits.</li><li>Försök att hämta produktinformationen med hjälp av Merchandising Service-frågan [products](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details) med samma huvuden som konfigurerats i filen `config.json`. Om du kan hämta data är det troligen ett problem med katalogvykonfigurationen eller ett indexfel.</li></ul> |
| **Sökningen returnerar inga resultat** | Tom sökresultatsida | <ul><li>Kontrollera att du kan hämta produktsökresultaten med Merchandising Services [productSearch-frågan](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search) med samma huvuden som konfigurerats i filen `config.json`. Om du kan hämta data är det troligen ett problem med katalogvykonfigurationen eller ett indexfel.</li><li>Bekräfta att katalogvyns ID i filen `config.json` matchar katalogvyns ID i [!DNL Adobe Commerce Optimizer].</li><li>Kontrollera konfigurationen av de principer, språk och prisböcker som du använde i rubrikkonfigurationen för storefront i Adobe Commerce Optimizer.</li><li>Kontrollera att inställningarna för [attributmetadata](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) har angetts korrekt för sökning.</li></ul> |

### Checklista för validering

Innan du fortsätter till nästa steg kontrollerar du att din storefront fungerar som den ska genom att verifiera följande:

![Checklista](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Konfigurationsvärden matchar instansinställningarna<br>
![ Checklista ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Startsidan för Storefront läses in utan fel <br>
![Checklista](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Minst en produktinformationssida visar fullständig information <br>
![Checklista](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Sökfunktionen returnerar relevanta resultat <br>
![Checklista](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Produktbilder läses in korrekt <br>
![Checklista](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Konfigurationsvärden matchar instansinställningarna <br>

### Få hjälp

Om problemen kvarstår:

* Granska [dokumentationen för Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)
* Kontrollera [Adobe Commerce Optimizer utvecklarhandbok](https://developer.adobe.com/commerce/services/optimizer/)
* Gå till [Adobe Commerce supportresurser](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)

## Nästa steg

När du har konfigurerat och verifierat din butik kan du:

1. **[Installera Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#install-and-configure-sidekick)** - webbläsartillägg för redigering, förhandsgranskning och publicering av innehåll direkt från webbplatsen

2. **[Konfigurera en lokal utvecklingsmiljö](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)** - Skapa en lokal miljö för att anpassa din butikskod och ditt innehåll

### Utforska och lär dig mer

* **[Slutför hela användningsexemplet](./use-case/admin-use-case.md)** - Läs mer om konfiguration och kataloghantering av butiker med [!DNL Adobe Commerce Optimizer]

* **[Utforska anpassning av butiker](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)** - Lär dig avancerade inställningar och konfigurationsalternativ

* **[Använd Commerce-insticksprogram för att anpassa butiksupplevelsen](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)**-Lägg till färdiga komponenter för att förbättra butiksupplevelsen

>[!MORELIKETHIS]
>
> Läs [dokumentationen för Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) om du vill veta mer om hur du uppdaterar webbplatsinnehåll och integrerar med komponenterna i Commerce Front och backend-data.
