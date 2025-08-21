---
title: Versionsinformation
description: Den senaste versionsinformationen för tillägget  [!DNL Data Connection] från Adobe Commerce.
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 90fcaa2cdd7c869ceddaeea7525cac00a41d94c5
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# Versionsinformation

>[!IMPORTANT]
>
>Namnet på Experience Platform-anslutningen har ändrats till [!DNL Data Connection].

Versionsinformationen innehåller uppdateringar av tillägget [!DNL Data Connection] och innehåller:

![Nytt](../assets/new.svg) - Nya funktioner
![Korrigera ](../assets/fix.svg) - Korrigeringar och förbättringar
![Fel](../assets/bug.svg) - Kända fel

Funktionsändringar och korrigeringar som rör tillägg som används av tillägget [!DNL Data Connection] finns i **Tjänsteuppdateringar som stöds**.

Läs [Kommande releaser](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) om du vill veta mer om releasescheman och support.

Läs utvecklardokumentationen för att [lära dig vilka Commerce-versioner som stöder den här modulen](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Uppdateringar av tjänster som stöds

I versionsinformationen beskrivs funktionsändringar och korrigeringar som rör tillägg som används av tillägget [!DNL Data Connection].

+++Uppdateringar av tjänster som stöds

_7 augusti 2025_

![Nytt](../assets/new.svg) - Med version 3.3.0 kan du nu lägga till [anpassade attribut till profiler](custom-identities.md).

_2 augusti 2024_

![Korrigera](../assets/fix.svg) - Fastställde totalt betalningsbelopp när ordersumman är konfigurerad att inkludera moms.
![Nytt](../assets/new.svg) - Ett `taxAmount`-fält har lagts till för att beställa inköpshändelser.
![Nytt](../assets/new.svg) - Möjligheten att lägga till anpassade data till händelser har lagts till. Se följande för ett [exempel](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md).

_24 januari 2024_

![Nytt](../assets/new.svg) - Tillägget `data-services-b2b` har uppdaterats så att det innehåller en ny rekvisitionshändelse med namnet `deleteRequisitionList` för B2B-handlare.

_16 november 2023_

![Korrigera](../assets/fix.svg) - Korrigerade ett problem där ett felmeddelande felaktigt visades när du gjorde en beställning med flera leveransadresser.
![Korrigera](../assets/fix.svg) - Korrigerade ett fel i `productPageView`-händelsen där `productListItems.priceTotal`-händelsefältet inte konverterade priset efter växling av valutan i butiksvyn.
![Korrigera](../assets/fix.svg) - Korrigerade ett fel i händelsefältet `productListItems` där valutakoden inte uppdaterades när handlaren växlade till butiksvyn.

_10 oktober 2023_

![Nytt](../assets/new.svg) - Nya händelser för orderstatus har lagts till: [Orderfakturerad](events-backoffice.md#orderinvoiced), [Returinitierad orderartikel](events-backoffice.md#orderitemsreturninitiated) och [Returnerad orderartikel slutförd](events-backoffice.md#orderitemreturncompleted).
![Korrigera](../assets/fix.svg) - Korrigerade ett problem där ändringar av valutakonfigurationen inte återspeglades i händelserna efter att cachen uppdaterades.
![Korrigera](../assets/fix.svg) - Ett fel har korrigerats när orderbekräftelsemeddelandet inte visas om asynkron orderplacering är aktiverad.
![Nytt](../assets/new.svg) - Data har lagts till i `addToRequisitionList`-händelsen för enkla produkter på kategorivysidan.
![Korrigera](../assets/fix.svg) - Ett problem i `selectedOptions`-data i `addToRequisitionList`-händelsen när produkter läggs till från orderbekräftelsesidan har korrigerats.
![Nytt](../assets/new.svg) - Produktdata har lagts till i `addToRequisitionList`-händelsen när produkter läggs till i rekvisitionslistan från kategorivysidan.
![Ny](../assets/new.svg) - `addToRequisitionList`-händelse har lagts till när konfigurerbara produkter läggs till i rekvisitionslistan från produktvysidan.
![Nytt](../assets/new.svg) - `addToRequisitionList`- och `removeFromRequisitionList`-händelser har lagts till när produktkvantiteten ökas och/eller minskas från en rekvisitionslista.

_10 juni 2023_

![Korrigera](../assets/fix.svg) - Korrigerade ett fel när `orderId` inte kunde skickas i kontexten på grund av prefix i Commerce-identifieraren för order.
![Korrigera](../assets/fix.svg) - Uppdaterade säkerhetsprincipkonfigurationer för innehåll.

_30 mars 2023_

![Nytt](../assets/new.svg) - Ett tillägg med namnet `data-services-b2b` som innehåller [rekvisitionslistehändelser](events.md#b2b-events) för B2B-handlare har lagts till.
![Nytt](../assets/new.svg) - `uniqueIdentifier`-fältet har lagts till i [sök](events.md#search-events)-händelser. I det nya fältet kan handlare korsreferera sökbegäranden och söksvar.

_12 oktober 2022_

![Nytt](../assets/new.svg) - Två [storefront-händelser ](events.md), `openCart` och `removeFromCart` har lagts till i Adobe Commerce Storefront Events SDK och Collector.
![Nytt](../assets/new.svg) - Stöd har lagts till för en [AEM store](overview.md#aem-support).

+++

## 3.3.0

_21 mars 2025_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd för PHP 8.4 har lagts till.

## 3.2.1

_17 januari 2025_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) - Det [HIPAA-klara tillägget](hipaa-readiness.md) har lagts till i [!DNL Data Connection] så att handlare kan dela [!DNL Commerce] back office-händelsedata med Experience Platform och upprätthålla HIPAA-kompatibilitet.
![Korrigera](../assets/fix.svg) - Korrigerade ett fel där [!DNL Data Connection]-tillägget skrev över `eventForwarding`-data och angav `HIPAA`-flaggan för alla kunder. Nu sätter tillägget bara flaggan för HIPAA-kunder.

## 3.2.0

_7 oktober 2024_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) - Möjligheten att skapa [anpassade orderattribut](custom-attributes.md) till back office-data har lagts till.
![Nytt](../assets/new.svg) - En ny tabell med [anpassade ordningsattribut](connect-data.md#data-customization) har lagts till som hjälp när du vill visa anpassade attribut som konfigurerats i [!DNL Commerce] och skickats till Experience Platform.
![Nytt](../assets/new.svg) - Lagt till möjlighet att [samla in och skicka profilposter](connect-data.md#send-customer-profile-data) och data till Experience Platform.

## 3.2.0-beta3

_27 augusti 2024_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) - Om du deltar i betaversionen kontrollerar du att `composer.json`-filen har följande på rotnivån: ` "minimum-stability": "beta"`. Lägg också till `composer require "magento/customers-connector: ^1.2.0"` för att skicka kundprofiler från din Commerce-instans till SaaS.
![Nytt](../assets/new.svg) - Den här versionen innehåller de korrigeringar som släpptes i 3.1.1, 3.1.2, 3.1.3 och 3.1.4.

## 3.1.4

_9 augusti 2024_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) - Metapaketet `experience-platform-connector` har uppdaterats för att ta bort ytterligare oanvända dataexporterare och indexerare.

## 3.1.3

_22 juli 2024_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) - Metapaketet `experience-platform-connector` har uppdaterats för att ta bort oanvända dataexporterare och indexerare.

## 3.1.2

_5 juni 2024_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) - Ett problem har korrigerats där fel datumformat användes när en [historik synkronisering](connect-data.md#specify-order-history-date-range) initierades.
![Korrigera](../assets/fix.svg) - Korrigerade ett fel där `startCheckout`-händelsen inte skickades till Adobe Commerce 2.4.7.

## 3.1.1

_4 april 2024_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) - Stöd för PHP 8.3 har lagts till för alla [!DNL Data Connection]-tillägg.
![Nytt](../assets/new.svg) - artikeln [Integrera](mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK med Commerce har lagts till.

## 3.2.0-beta2

_4 mars 2024_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) - Om du deltar i betaversionen kontrollerar du att `composer.json`-filen har följande på rotnivån: ` "minimum-stability": "beta"`. Lägg också till `composer require "magento/customers-connector: ^1.2.0"` för att skicka kundprofiler från din Commerce-instans till SaaS.
![Nytt](../assets/new.svg) - Lagt till möjlighet att [lägga till anpassade attribut](custom-attributes.md).
![Nytt](../assets/new.svg) - Lagt till möjlighet att [samla in och skicka profilposter](connect-data.md#send-customer-profile-data) och data till Experience Platform.

## 3.1.0

_16 november 2023_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) - Experience Platform-anslutningen har bytt namn till [!DNL Data Connection].
![Korrigera](../assets/fix.svg) - Möjlighet att logga felsvar har lagts till om Adobe IMS inte kan generera åtkomsttoken.
![Korrigera](../assets/fix.svg) - Ett meddelandemeddelande har lagts till om du försöker synkronisera historiska order men inte har angett kontoautentiseringsuppgifter.

## 3.0.0

_10 oktober 2023_

[!BADGE Kompatibilitet]{type=Informative tooltip="Kompatibilitet"} Adobe Commerce version 2.4.4 och senare

Det här är en större version. [Redigera](install.md#update-the-data-connection) projektets rotfil Composer.json.

![Nytt](../assets/new.svg) - Allmän tillgänglighet för att [skicka historik för order](connect-data.md#send-historical-order-data)-data och status till Experience Platform.
![Nytt](../assets/new.svg) - Stöd för OAuth 2.0 har lagts till när du [konfigurerar](connect-data.md#connect-commerce-data-to-adobe-experience-platform) tillägget [!DNL Data Connection].
![Nytt](../assets/new.svg) - Stöd för Adobe Commerce 2.4.3 har upphört.

## 2.3.0

_27 juni 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Nytt](../assets/new.svg) - Lagt till möjlighet att [inaktivera sändning av butikshändelser](connect-data.md#data-collection) till Experience Platform.
![Korrigera](../assets/fix.svg) - Uppdaterade säkerhetsprincipkonfigurationer för innehåll.
![Korrigera](../assets/fix.svg) - Fast stöd för back office-händelser i Commerce 2.4.7-versionen.
![Nytt](../assets/new.svg) - Ett meddelande om cacheogiltigförklaring har lagts till när du sparar ändringar i tilläggsformuläret [!DNL Data Connection].

## 3.0.0-beta1 (endast internt)

_13 juni 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Nytt](../assets/new.svg) - (Beta) Lagt till möjlighet att [skicka data och status för tidigare order](connect-data.md#beta-send-historical-order-data) till Experience Platform.

## 2.2.0

_30 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Nytt](../assets/new.svg) - Paketerade beroenden för `commerce-data-export` och `saas-export` med tillägget `experience-platform-connector`. Tidigare var du tvungen att installera dessa beroenden separat. Dessa beroenden, tillsammans med handelskonfigurationen, möjliggör bearbetning på serversidan av [back office-händelser](events-backoffice.md).
![Nytt](../assets/new.svg) - En ny back office-händelse med namnet [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted) har lagts till.

## 2.1.1

_28 februari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Nytt](../assets/new.svg) - Stöd för PHP 8.2 för alla [!DNL Data Connection]-tillägg har lagts till.

## 2.1.0

_17 januari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Nytt](../assets/new.svg) - [[!DNL Data Connection] tilläggsadministratören](connect-data.md) har uppdaterats så att du kan ange en egen AEP Web SDK (legering).
![Korrigera](../assets/fix.svg) Ändrad till att använda `identityMap` i stället för `personID` när den primära identiteten anges för data som skickas till kanten.

## 2.0.1

_10 november 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Korrigera](../assets/fix.svg) - Nu ställs Adobe Experience Platform-kontexten in först efter det att händelseinsamlaren i Store och StoreFront Event SDK har lästs in.

## 2.0.0

_12 oktober 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Nytt](../assets/new.svg) - Möjligheten att ange din egen AEP Web SDK när [du ansluter](connect-data.md) din Adobe Commerce-instans till Experience Platform har lagts till.
![Korrigera](../assets/fix.svg) - Uppdaterat datastream-scopekrav så att datastream-ID:n måste omfångas till webbplatsen i stället för att lagras.

## 1.0.0

_9 augusti 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.3 och senare

![Nytt](../assets/new.svg) - allmän tillgänglighetsrelease.
