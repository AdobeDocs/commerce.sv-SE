---
title: Använd Adobe Journey Optimizer för att skicka ett övergivet kundvagn
description: Lär dig hur du använder Adobe Journey Optimizer för att skicka övergivna kundvagnsmeddelanden.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---

# Använd Adobe Journey Optimizer för att skicka ett övergivet kundvagnsmeddelande

Lär dig hur du kan leverera ett personligt e-postmeddelande om återengagemang om en kundvagn eller webbläsarsession har övergivits. I den här artikeln använder du data som genererats från kunder som har tittat på ett antal produkter och kategorier, använt en produkt eller använt en sida.

## Vilka data bör jag överväga att använda?

Bygg en övergiven kundvagn, bläddra i e-post eller meddelanden med data från butiks- och back office-händelser.

| Datatyper | data från Storefront (beteendehändelser) | Back office-data (händelser på serversidan) |
|---|---|---|
| **Definition** | Klicka på eller vidta de åtgärder som kunderna ska vidta på er webbplats. | Information om livscykeln och detaljer för varje order (tidigare och aktuell). |
| **Händelser som hämtats av Adobe Commerce** | [pageView](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/event-forwarding/events#pageview)<br>[productPageView](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/event-forwarding/events)<br>[addToCart](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/event-forwarding/events#addtocart)<br>[openCart](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/event-forwarding/events#opencart)<br>[startCheckout](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/event-forwarding/events#startcheckout)<br>[completeCheckout](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/event-forwarding/events#completecheckout) | [orderPlaced](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/event-forwarding/events-backoffice#orderplaced)<br>[Orderhistorik](https://experienceleague.adobe.com/sv/docs/commerce/data-connection/fundamentals/connect-data#send-historical-order-data) |

### Vad har andra kunder gjort?

Adobe [!DNL Commerce]-kunder har fått betydande affärsresultat genom att implementera skräddarsydda övergivningskampanjer med Adobe [!DNL Commerce], Adobe [!DNL Journey Optimizer] och Adobe [!DNL Real-Time CDP].

En global klädhandlare med flera varumärken har uppnått följande:

- 1,9 gånger fler klick från nya kampanjer
- 57 % ökning av intäkterna från avhandlingar i flera kanaler
- 41 % ökning av konverteringsgraden för återengagemangskampanjer
- Över 1 000 nya kunder engagerade per vecka

Ett globalt dryckesföretag:

- 36 % återengagerade öppningsfrekvenser för e-post
- 21 % ökning av klickfrekvens
- 8,5 % ökning av konverteringsgraden
- 89 % av alla som överger sitt engagemang konverterar

## Kom så börjar vi

Det här användningsfallet fokuserar på att skapa ett övergivet kundvagnsmeddelande med data från din [!DNL Commerce]-instans och skicka det till Adobe [!DNL Journey Optimizer].

### Vad är Adobe Journey Optimizer?

[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=sv-SE) hjälper dig att anpassa e-handelsupplevelsen för dina kunder. Du kan till exempel använda Journey Optimizer för att skapa och leverera schemalagda marknadsföringskampanjer, till exempel veckokampanjer för en butik, eller generera ett övergivet kundvagnsmeddelande om kunden har lagt till en produkt i en kundvagn men sedan inte slutfört utcheckningsprocessen.

I det här avsnittet får du lära dig att skapa ett övergivet kundvagnsmeddelande genom att lyssna på en `checkout`-händelse som genereras från din [!DNL Commerce]-instans och svara på den händelsen i Journey Optimizer.

>[!IMPORTANT]
>
>I demonstrationssyfte använder du sandlådemiljön [!DNL Commerce] så att du inte späder dina data för produktionshändelser med händelsedata för butiker och back office som du skickar till Experience Platform.

### Förutsättningar

Innan du börjar med de här stegen måste du se till:

- Du har etablerats för att använda Adobe [!DNL Journey Optimizer]. Om du är osäker kan du kontakta systemintegratören eller utvecklingsteamet som hanterar projekt och miljöer.
- Du [installerade](install.md) och [konfigurerade](connect-data.md) tillägget [!DNL Data Connection] i [!DNL Commerce].
- Du [bekräftade](connect-data.md#confirm-that-event-data-is-collected) att dina [!DNL Commerce]-händelsedata kommer till Experience Platform.

## Steg 1: Skapa en användare i din [!DNL Commerce]-sandlådemiljö

Skapa en användare i sandlådemiljön och bekräfta att användarkontoinformationen visas i Experience Platform. Kontrollera att den e-postadress du angav är giltig eftersom den används senare i det här avsnittet för att skicka övergiven e-postvagn.

1. Logga in eller skapa ett konto i din [!DNL Commerce]-sandlådemiljö.

   ![Logga in på ditt testkonto](assets/sign-in-account.png){width="700" zoomable="yes"}

   Med tillägget [!DNL Data Connection] installerat och konfigurerat skickas den här kontoinformationen till Experience Platform som en profil.

1. Bekräfta att din användarkontoinformation visas i avsnittet **[!UICONTROL Profile]** i Experience Platform.

   Gå till **[!UICONTROL Profiles]** i Adobe Experience Platform. Klicka på **[!UICONTROL Detail]** i profilen för att visa profilen som du skapade.

   ![Bekräfta profil](assets/check-event-profile.png){width="700" zoomable="yes"}

## Steg 2: Visa händelser i Journey Optimizer

I din [!DNL Commerce]-sandlådemiljö kan du utlösa händelser på din butik genom att visa produktsidor, lägga till objekt i en kundvagn och slutföra olika andra aktiviteter som en kund skulle utföra. Bekräfta sedan att dessa händelser skickas till Journey Optimizer.

1. Starta [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=sv-SE).
1. Välj **[!UICONTROL Profiles]**.
1. Ange **[!UICONTROL Identity namespace]** till `Email`.
1. Ange **[!UICONTROL Identity value]** som din e-postadress.
1. Markera din profil och välj sedan fliken **[!UICONTROL Events]**.

   ![Kontrollera händelseinformation](assets/check-event-details.png){width="700" zoomable="yes"}

   Leta efter händelsen `commerce.checkouts` och granska händelsens nyttolast:

   ```json
   "personID": "84281643067178465783746543501073369488", 
   "eventType": "commerce.checkouts", 
   "_id": "4b41703f-e42e-485b-8d63-7001e3580856-0", 
   "commerce": { 
       "cart": {}, 
       "checkouts": { 
           "value": 1 
       } 
   ```

   Som du ser innehåller den fullständiga händelsenyttolasten omfattande händelsedata. I nästa avsnitt kommer du att konfigurera händelser i Journey Optimizer så att de lyssnar efter och svarar på `commerce.checkouts`-händelsen som genereras från din [!DNL Commerce]-butik.

## Steg 3: Konfigurera händelser i Journey Optimizer

Konfigurera två händelser i Journey Optimizer: en händelse avlyssnar händelsen `commerce.checkouts` från Commerce, och den andra är en grundläggande timeout-händelse som väntar en viss tid innan en övergiven kundvagnse-post aktiveras.

### Skapa en avlyssnarhändelse

1. Starta [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=sv-SE).

1. Klicka på **[!UICONTROL Configurations]** under avsnittet **[!UICONTROL Administration]** i den vänstra rutan.

1. Klicka på **[!UICONTROL Manage]** i rutan **[!UICONTROL Events]**.

   ![Journey Optimizer Event Configuration](assets/ajo-config.png){width="700" zoomable="yes"}

1. Klicka på **[!UICONTROL Create Event]** på sidan **[!UICONTROL Events]**.

1. Ställ in händelsen på följande sätt i den högra navigeringen:

   1. Ange **[!UICONTROL Name]** till: `firstname_lastname_checkout`.
   1. Ange **[!UICONTROL Type]** till **[!UICONTROL Unitary]**.
   1. Ange **[!UICONTROL Event id typ]e** till **[!UICONTROL Rule based]**.
   1. Ange **[!UICONTROL Schema]** till ditt [!DNL Commerce] [schema](update-xdm.md).
   1. Välj **[!UICONTROL Fields]** för att öppna sidan **[!UICONTROL Fields]**. Markera sedan de fält som är användbara för den här händelsen. Markera till exempel alla fält under **[!UICONTROL Product list items]**, **[!UICONTROL Commerce]**, **[!UICONTROL eventType]** och **[!UICONTROL Web]**.
   1. Klicka på **[!UICONTROL OK]** för att spara de markerade fälten.
   1. Klicka inuti fältet **[!UICONTROL Event id condition]**. Skapa sedan ett villkor: `eventType` är lika med `commerce.checkouts` AND `personalEmail.address` är lika med den e-postadress som du använde när du skapade profilen i föregående avsnitt.

      ![Journey Optimizer Ange villkor](assets/ajo-set-condition.png){width="700" zoomable="yes"}

   1. Klicka på **[!UICONTROL OK]**.
   1. Klicka på **[!UICONTROL Save]** om du vill spara aktiviteten.

### Skapa en timeout-händelse

1. Skapa ett event i Journey Optimizer som du gjorde tidigare.

1. Ställ in händelsen på följande sätt i den högra navigeringen:

   1. Ange **[!UICONTROL Name]** till: `firstname_lastname_timeout`.
   1. Ange **[!UICONTROL Type]** till **[!UICONTROL Unitary]**.
   1. Ange **[!UICONTROL Event id type]** till **[!UICONTROL Rule based]**.
   1. Ange **[!UICONTROL Schema]** till ditt [!DNL Commerce] [schema](update-xdm.md).
   1. Ange **[!UICONTROL Schema]**, **[!UICONTROL Fields]** och **[!UICONTROL Event id condition]** till samma som ovan.
   1. Klicka på **[!UICONTROL Save]** om du vill spara aktiviteten.

När dessa två händelser är konfigurerade kan du skapa en resa som skickar ett övergivet kundvagnsmeddelande.

## Steg 4: Bygg en utcheckningsresa

Skapa en resa som lyssnar efter händelsen `commerce.checkouts` och skickar sedan ett övergivet kundvagnsmeddelande när en viss tid har gått.

1. I Journey Optimizer väljer du **[!UICONTROL Journeys]** under **J[!UICONTROL OURNEY MANAGEMENT]**.
1. Klicka på **[!UICONTROL Create Journey]**.
1. Ange namnet på din resa.
1. Klicka på **[!UICONTROL OK]** för att spara resan.
1. I den vänstra navigeringen under avsnittet **[!UICONTROL EVENTS]** söker du efter den utcheckningshändelse som du skapade tidigare: `firstname_lastname_checkout` och drar och släpper den på arbetsytan.

   >[!TIP]
   >
   >Om du dubbelklickar på händelsen läggs den automatiskt till på arbetsytan.

1. Sök efter timeout-händelsen och lägg till den på arbetsytan.
1. Dubbelklicka på timeout-händelsen.

   1. Markera kryssrutan **[!UICONTROL Define the event time]** i avsnittet **[!UICONTROL Timeout]**.
   1. I fältet **[!UICONTROL Wait for]** anger du `1` och `Minute`.
   1. Markera kryssrutan **[!UICONTROL Set a timeout path]**.

   Med den här timeoutkonfigurationen utlöses den här tidsgränsen av en kund som utför en utcheckning men inte slutför ordern inom en minut. I en faktisk produktionsmiljö skulle du ange detta för en längre period, som 24 timmar.

1. I den vänstra navigeringen under **[!UICONTROL ACTIONS]** lägger du till åtgärden **[!UICONTROL Email]** i timeout-grenen. Resan ska se ut så här:

   ![Journey Optimizer Canvas](assets/ajo-canvas.png){width="700" zoomable="yes"}

### Skapa en övergiven kundvagn

Skapa en övergiven kundvagn som skickas när en övergiven kundvagn identifieras.

1. Dubbelklicka på ikonen **[!UICONTROL Email]** på arbetsytan under den resa du skapade ovan.

1. Följ [stegen](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/personalization/personalization-use-cases/personalization-use-case-helper-functions.html?lang=sv-SE#configure-email) i Journey Optimizer-guiden för att skapa det övergivna e-postmeddelandet.

Du har nu en resa i Journey Optimizer som lyssnar efter händelsen `commerce.checkouts` från din [!DNL Commerce]-butik och ett övergivet kundvagnsmeddelande som skickas efter en tidsperiod. I nästa avsnitt visas hur du testar resan.

## Steg 5: Starta utcheckningshändelsen i realtid

I det här avsnittet testar du händelsen i realtid.

1. I Journey Optimizer växlar du till testläge.

   ![Aktivera testläge](assets/ajo-enable-test.png){width="700" zoomable="yes"}

1. Om du vill testa den här resan i realtid öppnar du en annan webbläsarflik och går till webbplatsen [!DNL Commerce] i din sandlådemiljö.

   1. Lägg en produkt i kundvagnen.
   1. Gå till utcheckningssidan.
   1. Gå till kassan och överge vagnen genom att gå tillbaka till huvudsidan eller stänga fliken.

      Resan är nu utlöst. Bekräfta genom att öppna fliken som du har besökt i Journey Optimizer. Du bör se en grön pil som visar den sökväg som användaren gick igenom.

1. Kontrollera din inkorg för e-postmeddelandet.
