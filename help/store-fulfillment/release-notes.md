---
title: Versionsinformation för [!DNL Store Fulfillment by Walmart Commerce Technologies]
description: Läs versionsinformationen om du vill ha information om alla  [!DNL Store Fulfillment by Walmart Commerce Technologies] releaser.
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Versionsinformation

Dessa versionsinformation beskriver den första versionen av [!DNL Store Fulfillment Services by Walmart Commerce Technologies] och innehåller:

![Nya](../assets/new.svg) nya funktioner
![ Åtgärdat problem ](../assets/fix.svg) Korrigeringar och förbättringar
![Kända fel](../assets/bug.svg)

Läs [Kommande releaser](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html?lang=sv-SE) om du vill veta mer om releasescheman och support.

Se [Produkttillgänglighet](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=sv-SE) om du vill veta vilka Adobe Commerce-versioner som stöder det här tillägget.

## v1.5.0

*3 augusti 2023*

[!BADGE Stöds]{type=Informative tooltip="Stöds"}[Adobe Commerce 2.4.4 till 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=sv-SE), inklusive säkerhetsuppdateringarna 2.4.6-p1, 2.4.5-p3 och 2.4.4-p4

Den här versionen innehåller följande uppdateringar:

![Nytt](../assets/fix.svg) Tillägget har uppdaterats med stöd för [Adobe Commerce säkerhetsuppdateringar](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html?lang=sv-SE) 2.4.6-p1, 2.4.5-p3 och 2.4.4-p4.

![Nytt](../assets/new.svg)<!-- WMTP-918 --> Stöd har lagts till för konfigurationsalternativet [Asynkron sändning](sales-emails.md) för försäljningsmeddelanden. Handlare som uppgraderar till version 1.5.0 kan skicka e-postmeddelanden direkt (standard) eller asynkront.

![Nytt](../assets/new.svg)<!-- WMTP-916--> [Källkonfigurationen](merchant-store-configuration.md) har uppdaterats med stöd för internationella telefonnummerformat.

![Ny](../assets/new.svg) logik har lagts till för att förhindra att återbetalningsbeloppen överskrider det återstående eller fakturerade beloppet.

![Nytt](../assets/new.svg)<!-- WMTP-882 --> ersatt `google.map.LatLng` objekt med JSON-litteraler som stöder kompatibilitet med äldre versioner av [!DNL Google Maps].

![Korrigerat problem](../assets/fix.svg)<!-- WMTP- --> Uppdaterade skriptet som skapar produktattributen `[!DNL Available for Store Pickup]` och `[!DNL Available for Home Delivery]` för att förhindra konflikter mellan attributkategorier.

![Korrigerat problem](../assets/fix.svg)<!-- WMTP-915 --> Korrigerade ett kompatibilitetsproblem som orsakade en oändlig loop när vissa entiteter lästes in och sparades.

![Korrigerat problem](../assets/fix.svg)<!-- WMTP-921 --> Ett problem som hindrade [!DNL Ship to Store] offertvalidering från att utlösas när ett objekt läggs till i vagnen från en produktinformationssida (PDP) har åtgärdats.

![Korrigerat problem](../assets/fix.svg)<!-- WMTP- 932 --> Ett utcheckningsproblem som gjorde att kunderna kunde välja hemleveransmetod för artiklar som inte är berättigade för hemleverans har korrigerats.

![Ett problem har åtgärdats](../assets/fix.svg) Installationsuppdateringar:

- &#x200B;<!-- WMTP-880--> Ett problem som orsakade att en felaktig webbplatskod returnerades när tillägget [!DNL Store Fulfillment] installerades har åtgärdats.

- &#x200B;<!-- WMTP-878--> Korrigerade ett problem för SKU-heltal som krävde att datatypen skulle konverteras till strängtyp under installationen.

![Korrigerat problem](../assets/fix.svg)<!-- WMTP-915--> Korrigerade ett fel som orsakats av en felkod för incheckning som saknas.

![Korrigerat problem](../assets/fix.svg)<!-- WMTP-932 --> Korrigerade ett fel relaterat till partiell avvisning under utdelningsåtgärder.

![Nytt](../assets/new.svg)<!-- WMTP-953 --> Uppdaterade API-slutpunkten för Avbryt för att använda statusparametern som ett valfritt objekt.

![Nytt](../assets/new.svg)<!-- WMTP-960 --> Förbättrad loggningsinformation för API-slutpunkten för dispensering.

## v1.4.0

*13 april 2023*

[!BADGE Stöds]{type=Informative tooltip="Stöds"}

![Nytt](../assets/fix.svg) [!DNL Store Fulfillment] är nu [kompatibelt med  [!DNL Adobe Commerce]  2.4.4 till 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=sv-SE).


## v1.3.0

*27 februari 2023*

[!BADGE Stöds]{type=Informative tooltip="Stöds"}

Den här versionen innehåller följande uppdatering:

![Nytt](../assets/fix.svg)<!-- WMTP-795 --> har lagt till möjligheten att inaktivera Store Fulfillment-lösningen för en specifik plats genom att ändra standardomfånget för systemkonfigurationsinställningen från webbplats till global.

## v1.2.0

*27 september 2022*

[!BADGE Stöds]{type=Informative tooltip="Stöds"}

Den här versionen innehåller följande uppdatering:

![Nytt](../assets/fix.svg) [!DNL Store Fulfillment] är nu [kompatibelt med  [!DNL Adobe Commerce]  2.4.4 till 2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=sv-SE).


## v1.1.0

*15 juli 2022*

[!BADGE Stöds]{type=Informative tooltip="Stöds"}

Stabilitet: Allmän tillgänglighet

![Nytt](../assets/fix.svg)<!-- WMTP-731 --> Förenklade konfigurationen [Incheckningsgränssnittet](check-in-experience-setup.md) för Store Assist-appen genom att lägga till standardbiltillverkare och modellval. I den tidigare versionen var handlarna tvungna att konfigurera bilfabrikat och modellval manuellt.

## v1.0.0

*4 mars 2022*

[!BADGE Stöds]{type=Informative tooltip="Stöds"}

Stabilitet: Allmän tillgänglighet

## App för Store Assist

Mer information om nya versioner av Store Assist-appen finns i appinformationen i [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} eller [Google Play Store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.
