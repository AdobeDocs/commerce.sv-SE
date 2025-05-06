---
title: Carvelo - användningsfall
description: Lär dig hur du använder  [!DNL Adobe Commerce Optimizer] för att hantera din katalog med hjälp av kanaler och principer och hur du konfigurerar din butik baserat på din katalogkonfiguration.
hide: true
role: Admin, Developer
feature: Personalization, Integration
exl-id: d11663f8-607e-4f1d-b68f-466a69bcbd91
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '1672'
ht-degree: 0%

---

# Carvelo - användningsfall

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

Följande exempel visar hur du kan använda [!DNL Adobe Commerce Optimizer] för att ordna din katalog så att den matchar butiksåtgärder med en enda baskatalog. Det visar också hur man skapar en butik som drivs av Edge Delivery Services.

## Förutsättning

Innan du går igenom det här användningsexemplet bör du kontrollera att du har [konfigurerat din butik](../storefront.md).

## Kom så börjar vi

I det här fallet arbetar du med följande:

1. [!DNL Adobe Commerce Optimizer]-gränssnitt - Konfigurera nödvändiga kanaler och principer för att hantera driftsinställningar för komplexa kataloger.

1. Commerce Storefront - Återge butiken med katalogdata som är konfigurerade i [!DNL Adobe Commerce Optimizer]-gränssnittet och konfigurationsfilerna för Commerce Storefront, `fstab.yaml` och `config.json`.

### ‌ viktiga uppgifter

I slutet av den här artikeln ska du:

- Lär dig grunderna i [!DNL Adobe Commerce Optimizer] med dess unika prestanda och skalbara katalogdatamodell.
- Lär dig hur katalogdatamodellen sömlöst kopplas ihop med plattformsoberoende butikskomponenter som byggts av Adobe.
- Lär dig hur du använder Adobe Commerce Optimizer kanaler och profiler för att skapa anpassade katalogvyer och dataåtkomstfilter och skickar data till en Adobe Commerce-butik som drivs av Edge Delivery.

## Affärsscenario - Carvelo Automoble

Carvelo Automomobile är ett fiktivt bilkonglomerat med en komplex driftskonfiguration.

![Carvelo Automomobile](../assets/carvelo.png)

I det här diagrammet ser du att Carvelo säljer bilprodukter från tre varumärken. Varje varumärke är ett eget underordnat företag:

- Aurora (elfordon)
- Bult (SUV)
- Cruz (hybrid)

Den säljer dessa varumärken genom tre återförsäljare:

- Arkbridge
- Kingsbluff
- Celport

Dessa återförsäljare tillhör två olika moderbolag:

- West Coast Inc. (Arkbridge)
- East Coast Inc. (Kingsblå, Celport)

Varje företag har två prislistor som används för att sälja produkter till ett visst pris för olika kunder (bas, VIP).

- `west_coast_inc` och `vip_west_coast_inc`
- `east_coast_inc` och `vip_east_coast_inc`

Som du ser är detta ett mycket komplext affärsexempel. Med [!DNL Adobe Commerce Optimizer] kan en handlare stödja en komplex affärsstruktur genom att använda en enda baskatalog för att syndikera data utan katalogduplicering, skala prisböcker (30 kB+ prisböcker) och leverera alla dessa data till en Edge Delivery Services-butik.

Nu när du har en översikt över användningsfallet för företag kan du göra följande:

>[!BEGINSHADEBOX]

Carvelo vill sälja delar av sina tre varumärken (Aurora, Bolt och Cruz) genom de olika återförsäljarna (Akbridge, Kingsbluff och Celport). Carvelo vill se till att återförsäljarna bara har tillgång till rätt delar och priser enligt sina respektive licensavtal.

I slutändan har Carvelo två viktiga mål:

1. Upprätthåll en&quot;global&quot; webbplats som har alla SKU:er för alla tre varumärkena.
1. Tillhandahåll en väg för återförsäljare att skapa egna butiker baserat på unik SKU-synlighet och priser för varje SKU för varje återförsäljare. Allt samtidigt som du använder en enda baskatalog, vilket eliminerar katalogduplicering.

>[!ENDSHADEBOX]

Gå till din [!DNL Adobe Commerce Optimizer]-instans nu.

## 1. Få åtkomst till instansen [!DNL Adobe Commerce Optimizer]

När du har anslutit till programmet Tidig åtkomst skickar Adobe ett e-postmeddelande med en URL som ger dig åtkomst till den [!DNL Adobe Commerce Optimizer]-instans som du har fått. Den här instansen är förkonfigurerad med allt du behöver för att slutföra stegen som beskrivs i den här självstudiekursen, inklusive katalogdata som stöder Carvelo Automoble-användningsexemplet.

När du startar [!DNL Adobe Commerce Optimizer] ser du följande:

![[!DNL Adobe Commerce Optimizer]-gränssnitt](../assets/user-interface.png)

>[!NOTE]
>
>Läs artikeln [overview](../overview.md) om du vill veta mer om de olika delarna som utgör användargränssnittet i [!DNL Adobe Commerce Optimizer].

I den vänstra navigeringen expanderar du avsnittet **[!UICONTROL Catalog]** och klickar på **[!UICONTROL Channels]**. Observera att återförsäljarna Arkbridge och Kingsbluff redan har skapat kanaler:

![Förkonfigurerade kanaler](../assets/existing-channels-list.png)

>[!NOTE]
>
>Du kan för tillfället ignorera den **globala**-kanalen.

Klicka på informationsikonen för att granska kanalinformation.

Arkbridge har följande policyer:

- Varumärke
- Modell
- West Coast Inc-varumärken
- Arkbridge-delkategorier

Kingsbluff har följande policyer:

- Varumärke
- Modell
- East Coast Inc-varumärken
- Kingsbluff - delkategorier

I nästa avsnitt skapar du en kanal och profiler för Celport-återförsäljaren.

## 2. Skapa en policy och kanal

Carvelos handelschef måste skapa en ny butik för en återförsäljare som heter *Celport* som tillhör företaget *East Coast Inc*. Celport säljer bromsar och suspensioner för varumärkena Bolt och Cruz.

![Celport Dealer](../assets/celport-dealer.png)

Med [!DNL Adobe Commerce Optimizer] kan e-handelshanteraren:

1. Skapa en ny policy som heter *Celport part categories* för Celport så att bara broms- och suspensionsdelar säljs.
1. Skapa en ny kanal för Celport-butiken.

   I den här kanalen används din nya policy *Celport part-kategorier* och befintliga *East Coast Inc-varumärken* för att säkerställa att Celport bara kan sälja de Bolt- och Cruz-varumärken som en del av avtalet med East Coast Inc. Celport-kanalen använder prisboken `east_coast_inc` för att stödja produktprisscheman som är anpassade till varumärkeslicensavtal.
1. Uppdatera butikskonfigurationen för e-handel så att den använder data från den Celport-kanal som du skapade.

I slutet av det här avsnittet kommer Celport att vara igång och redo att sälja Carvelos produkter.

### Skapa en profil

Låt oss skapa en ny policy som kallas *Celport-delkategorier* för att filtrera SKU:er som Celport-återförsäljaren säljer, som innehåller broms- och suspensionsdelar.

1. I den vänstra navigeringen expanderar du avsnittet **[!UICONTROL Catalog]** och klickar på **[!UICONTROL Policies]**.

1. Klicka på **[!UICONTROL Add Policy]**.

   En ny sida visas där profilinformationen läggs till.

1. Lägg till nödvändig information:

   **Namn** = *Exportera delkategorier*

1. Klicka på **[!UICONTROL Add Filter]**.

   En dialogruta visas där du kan lägga till filterinformation.

1. Lägg till filterinformation:

   - **Attribut** = *part_category*
   - **Operator** = **IN**
   - **Värde Source** = **STATIC**
   - **Värde** = *bromsar*, *suspension*

   >[!IMPORTANT]
   >
   >Kontrollera att det attributnamn du anger exakt matchar SKU-attributnamnet i katalogen.

   Mer information om skillnaden mellan en STATIC- och TRIGGER-värdekälla finns i [värdekälltyper](../catalog/policies.md#value-source-types).

1. Klicka på **[!UICONTROL Save]** i dialogrutan **[!UICONTROL Filter details]**.

1. Om du vill aktivera filtret som du nyss skapade klickar du på åtgärdspunkterna (...) och väljer **Aktivera**.

1. Klicka på **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Om knappen **[!UICONTROL Save]** inte är aktiv (blå) kanske du saknar principnamnet. Klicka på pennikonen bredvid *Ny profil* för att lägga till den.

1. Gå tillbaka till listan med profiler genom att klicka på bakåtpilen.

   Din nya princip för *Delkategorier för att exportera* visas i listan.

### Skapa en kanal

Skapa en ny kanal för återförsäljaren av *Celport* och länka följande profiler: *East Coast Inc-varumärken* och *Celport Part Categories*.

1. I den vänstra navigeringen expanderar du avsnittet **[!UICONTROL Catalog]** och klickar på **[!UICONTROL Channels]**.

   ![Kanaler](../assets/channels.png)

   Observera de befintliga kanalerna: *Arkbridge*, *Kingsbluff* och *Global*.

   ![Sidan Befintliga kanaler](../assets/existing-channels-list.png)

1. Klicka på **[!UICONTROL Add Channel]**.

1. Fyll i kanalinformation:

   - **Namn** = *Cirkapp*
   - **Omfång** = *en-US* (tryck på Retur)
   - **Profiler** (använd listruta) = *East Coast Inc-varumärken*; *Exportera delkategorier*; *Märke*; *Modell*                          

1. Klicka på **[!UICONTROL Add]** för att skapa kanalen.

   Sidan Kanaler uppdateras för att visa den nya kanalen.

   ![Uppdaterad kanallista](../assets/updated-channels-list.png)

   >[!NOTE]
   >
   >Om knappen **[!UICONTROL Add]** inte är blå kontrollerar du att omfånget är markerat genom att placera markören i avsnittet **[!UICONTROL Scopes]** och trycka på **enter**.

1. Hämta CellPort-kanal-ID:t.

   Klicka på informationsikonen för Celport-kanalen på sidan **Kanaler**.

   ![Exportera kanal-ID](../assets/celport-channel-id.png)

   Kopiera och spara kanal-ID:t. Du behöver detta ID när du uppdaterar butikskonfigurationen för att kunna leverera data till din nya Celport-katalog.

När du har skapat Celport-kanalen och associerade profiler är nästa steg att konfigurera storefront för att skapa din nya Celport-katalog.

## 3. Uppdatera din butik

Den sista delen av den här självstudien är att uppdatera butiken som [du redan har skapat](#prerequisite) för att leverera data till den nya Celport-katalogen. I det här avsnittet ersätter du channel ID:t i konfigurationsfilen för butiken med channel ID:t för Celport.

1. I den lokala utvecklingsmiljön öppnar du den mapp där du klonade GitHub-databasen med konfigurationsfilerna för lagerplatserna.

1. Öppna filen `config.json` i mappens rotkatalog.

   +++config.json-kod

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

   Observera att kanalhuvudet innehåller följande rader:

   - `ac-channel-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-environment-id`: `"Fwus6kdpvYCmeEdcCX7PZg"`
   - `ac-price-book-id`: `"west_coast_inc"`

+++

1. Ersätt värdet `ac-channel-id` med det Celerport-kanal-ID som du kopierade tidigare.
1. Ersätt värdet `ac-environment-id` med klientorganisations-ID:t för din [!DNL Adobe Commerce Optimizer]-instans. Du kan hitta ID:t i e-postmeddelandet om introduktion för programmet för tidig åtkomst, eller genom att kontakta din Adobe-kontorepresentant.

   >[!IMPORTANT]
   >
   >Kontrollera att värdet `commerce-endpoint` matchar GraphQL-slutpunkten för din [!DNL Adobe Commerce Optimizer]-instans. Detta anges i ditt välkomstmeddelande.

1. Ersätt värdet `ac-price-book-id` med `"east_coast_inc"`.
1. Spara filen.

När du sparar ändringarna uppdaterar du katalogkonfigurationen så att den använder Carvelo-kanalen, som har konfigurerats att endast sälja broms- och suspensionsdelar.

1. Starta butiken för att visa den Celport-specifika katalogupplevelse som har skapats i din storefront-konfiguration.

   1. Från terminalfönstret i IDE-miljön startar du den lokala förhandsgranskningen i butiken.

      ```shell
      npm start
      ```

   Webbläsaren öppnas för den lokala utvecklingsförhandsgranskningen på `http://localhost:3000`.

   Om kommandot misslyckas eller om webbläsaren inte öppnas går du igenom [instruktionerna för lokal utveckling](../storefront.md) i installationsavsnittet för Storefront.

   1. Sök efter `brakes` i webbläsaren och tryck på **Retur**.

      Lagerfronten uppdateras för att visa sidan med produktlistan med bromsdelarna.

   ![Bromsar produktlistsidan](../assets/brakes-listing-page.png)

   Klicka på en bild av en bromsdel för att visa produktinformationen med prisinformation och notera produktprisinformationen.

1. Sök nu efter `tires`, som är en annan delkategori som är tillgänglig i användningsfalldata för din [!DNL Adobe Commerce Optimizer]-instans.

   ![Konfiguration för Storefront med felaktiga rubriker](../assets/storefront-configuration-with-incorrect-headers.png)

   Observera att inga resultat returneras. Detta beror på att Celport-kanalen har konfigurerats att endast sälja broms- och upphängningsdelar.

1. Experimentera med att uppdatera konfigurationsfilen för butiken (`config.json`).

   1. Ändra värdena för `ac-channel-id` och `ac-price-book`.

      Du kan till exempel ändra kanal-ID:t till Kingsbluff-kanalen och prisbokens ID till `east_coast_inc`. Du kan se vilka kategorier som är tillgängliga för Kingsbluff genom att granska principen för *Kingsbluff-delen*.

   1. Spara filen.

      När du sparar filen uppdateras den lokala förhandsvisningen i butiken automatiskt.

   1. Förhandsgranska ändringarna i webbläsaren genom att använda sökfunktionen för att hitta däckdelar.

      Lägg märke till de olika tillgängliga deltyperna och observera priserna som tilldelats Kingsbluff-kanalen.

      Genom att ändra rubrikvärden i konfigurationsfilen för butiken och utforska den uppdaterade butiken kan du se hur enkelt det är att uppdatera katalogvyn och datafiltren för att anpassa butiksupplevelsen.

## Så ja!

I den här självstudiekursen lärde du dig hur [!DNL Adobe Commerce Optimizer] kan hjälpa dig att ordna din katalog så att den matchar dina återförsäljningsåtgärder med en enda baskatalog. Du lärde dig också att skapa en butik som drivs av Edge Delivery Services.

## Vart ska du gå härifrån?

Mer information om hur du kan använda produktidentifiering och rekommendationer för att anpassa shoppingupplevelsen för dina kunder finns i [försäljningsöversikten](../merchandising/overview.md).
