---
title: Appinställningar
description: Konfigurera appen  [!DNL Store Assist] för att hantera kompletta arbetsflöden och processer för att köpa online och hämta in butiksorder.
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Appinställningar

Store Assist är en faaS-plattformsapp (fulfillment-as-a-service) som drivs av Walmart Commerce Technologies. Appen har funktioner för leverans i butik för att hantera [!DNL buy online, pick up in store] (BOPIS)-order. Med hjälp av Store Assist kan butikspersonalen se vilka artiklar kunderna beställt, hämta rätt artiklar snabbare och lägga upp färdiga order för kundmottagning i butik eller i butik.

Store Assist-appen får all beställnings- och kundinformation - från beställningsinformation till hämtningstider - och gör data tillgängliga för att lagra partners online, via mobila enheter. Appen innehåller modulerna [!UICONTROL Pick], [!UICONTROL Stage], [!UICONTROL Handoff] och [!UICONTROL Orders] som kan hjälpa Store Associates att utföra följande aktiviteter:

- Tilldela leveransdatum och leveranstid för order.
- Få meddelanden från kunderna när de kommer för orderhämtning.
- Scenbeställningar för kundleverans.
- Spåra orderstatus för alla order på deras tilldelade butiksplatser.

>[!NOTE]
>
>Läs mer om Store Assist-appen genom att läsa avsnittet [Butiksassistentens arbetsflöden](store-assist-modules.md).

## Konfigurera Store Assist App

Store Assist-appen kräver två typer av konfigurationer:

- Adobe Commerce Admin-systeminställningar för att [hantera användarkonton, användarroller, resursbehörigheter](user-setup.md) och [göra bilfabrikat och modellval tillgängliga för kunder under incheckningsprocessen](check-in-experience-setup.md).

- Anpassa Store Assist-appgränssnittet och andra inställningar:

   - **Förse Store Assist-appen** - Anpassa appens användargränssnitt med företagets logotyp och färger.

   - **Uppdatera standardinstruktionerna** - Anpassa instruktionerna i arkivassistentväljaren, scenen, leveransen och beställningsmodulen för att vägleda Store Associates genom varje steg i arbetsflödet för leverans för ditt företag.

   - **Lokalisering** - Välj tillgängligt språk för appen. Välj datum- och tidsformat och välj standardmåttenheter och standardvaluta.

   - **Inaktivitetstid** - Ange hur lång tid appen måste vara inaktiv innan den loggas ut.

   - **Annullering från butiken** - Ange om beställningar kan avbrytas från butiken och vilka roller som har annulleringsbehörigheter

   - **Fönstret för orderrensning** - Ange hur långt efter den [beräknade lead-tiden för hämtning](enable-general.md#delivery-method-title-configuration) som en plockad order stannar kvar i mellanlagringen innan den återställs, till exempel tre dagar. Standardvärdet är sju dagar. Om den här konfigurationen är aktiverad avbryts ordern automatiskt när den här tiden går ut. Objekten återställs och handlaren får ett e-postmeddelande.

   - Anpassa allt i appinstruktioner (plockning, mellanlagring, utleverans).

   - **Plockningsmeddelanden** - Ange om du vill skicka ett push-meddelande för att starta plockprocessen efter att en kund har gjort en beställning.

   - **Incheckningsmeddelanden** - Ange om du vill skicka ett push-meddelande under incheckningsprocessen för orderplockningar efter incheckning, när kundväntetiden överskrider en angiven tidsperiod. Eller inaktivera meddelanden.

   - **Avaktivera process** - Aktivera valfria processer när Store Associate levererar order till kund, t.ex. kräver en kundsignatur eller ber den associerade att kontrollera kund-ID.

   - **Aktivera avvisning av objekt vid leverans** - Tillåt att kunder returnerar eller avbryter orderobjekt vid beställningsleverans.

  Samarbeta med Walmart Commerce Technologies Client Services-teamet för att slutföra konfigurationen av frontend för Store Assist App.

## Appnedladdning och installation

När Store Assist-appen har konfigurerats och konfigurerats kan Store Associates hämta, installera och logga in på Store Assist-appen från sina mobila enheter.

- Kontrollera att den mobila enheten uppfyller [maskin- och programvarukraven](solution-requirements.md#store-assist-app-requirements) för Store Fulfillment-lösningen.

- Hämta Store Assist-appen från [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} eller [Google Play Store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.

- Store Associates kräver följande information för att kunna logga in:

   - **[!UICONTROL Company name]** som är associerad med Store Assist-kontot

   - **Butiksassistentkontots autentiseringsuppgifter** - användarnamn och lösenord för deras konto.

  En Adobe Commerce-administratör kan skapa och hantera [!DNL Store Assist app]-användarkonton för alla butiksplatser där [In-Store-hämtning](merchant-store-configuration.md#pickup-location-configuration) är aktiverad i inställningarna för Admin Stores.
