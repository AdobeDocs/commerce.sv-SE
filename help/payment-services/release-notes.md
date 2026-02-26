---
title: Versionsinformation för [!DNL Payment Services]
description: Läs versionsinformationen om du vill ha information om alla  [!DNL Payment Services] releaser.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: 6727102c54e0ac81df289ecd66ec61156662b8b9
workflow-type: tm+mt
source-wordcount: '4679'
ht-degree: 0%

---


# Versionsinformation

De här versionsinformationen beskriver alla versioner av [!DNL Payment Services] och innehåller:

![Nya](../assets/new.svg) nya funktioner
![&#x200B; Åtgärdat problem &#x200B;](../assets/fix.svg) Korrigeringar och förbättringar
![Kända fel](../assets/bug.svg)

Om du vill se funktionsändringar och korrigeringar som släppts utanför den vanliga versionen av funktionen går du igenom avsnitten _Uppdateringar för värdtjänsten_.

Läs mer om kommande versioner, produktsupport och vilka Adobe Commerce-versioner som stöder tillägget [!DNL Payment Services] i Adobe Commerce [Release Schedule](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) och [Product Availability](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) .

## Uppdateringar av värdtjänster

I versionsinformationen beskrivs funktionsändringar och korrigeringar som har gjorts och släppts utanför de vanliga funktionsreleaserna för värdtjänsten.

+++Uppdateringar av värdtjänster

_21 januari 2026_

![Nytt problem](../assets/new.svg)<!-- Issue PAY-6374 --> Nu omdirigeras knappen **Inställningar** på kontrollpanelen [!DNL Payment Services] till Admin-konfigurationssidan för betalningsmetoder, vilket ger ett smidigare arbetsflöde för hantering av betalningsinställningar.

_19 januari 2026_

![Nytt problem](../assets/new.svg)<!-- Issue PAY-6325 --> Nu kan handlare visa PayPal Seller ID som en kolumn i [transaktionsrapporten](reporting.md#transactions-report-view) för att identifiera transaktioner som en viss kund har placerat.

_25 april 2025_

![Nytt problem](../assets/new.svg)<!-- Issue PAY-6051 --> Nu visar kontrollpanelen [!DNL Payment Services] både den aktuella tilläggsversionen och instrumentpanelsversionen.

_30 augusti 2024_

![Nytt problem](../assets/new.svg)<!-- Issue PAY-5658 --> Nu kan handlare filtrera transaktioner med betalningsinformationen i [transaktionsrapporten](reporting.md#transactions-report-view) för mer detaljerade och korrekta betalningsmetoder.

_15 juli 2024_

![Ny utgåva](../assets/new.svg)<!-- Issue PAY-5571 --> Nu kan handlare filtrera transaktioner efter Commerce-kundens e-postadress i [transaktionsrapporten](reporting.md#transactions-report-view). Ange kundens e-postadress för att filtrera transaktioner för den specifika e-postadressen.

_9 juli 2024_

![Nytt problem](../assets/new.svg)<!-- Issue PAY-5488 --> Nu kan handlare visa Commerce kund-ID som en kolumn i [transaktionsrapporten](reporting.md#transactions-report-view) för att identifiera transaktioner som en viss kund har placerat ut. Dessutom kan handlare filtrera transaktionsrapporten efter detta Commerce-kund-ID för tillhörande order.

_5 mars 2024_

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-5252 --> Nu kan handlare kopiera data från instrumentpanelsrutnätet genom att markera innehållet i en enskild cell.

_10 oktober 2023_

![Ny utgåva](../assets/fix.svg)<!-- Issue PAY-4888 --> Nu kan handlare filtrera korttransaktioner med kredit- och betalkortstransaktioner med de fyra sista siffrorna i kortnumret i [Transaktionsrapporten](reporting.md#transactions-report-view).

_12 juli 2023_

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-4587 --> Ett problem som uppstod i version [!DNL Payment Services] 2.1.0 och som förhindrade auktoriseringsannulleringar som placerats av tidigare tilläggsversioner har nu åtgärdats. Handlare som använder någon version av [!DNL Payment Services] kan inte godkänna auktoriseringar.

_9 juni 2023_

![Nytt](../assets/new.svg)<!-- Issue PAY-4288 --> Nu kan handlare [konfigurera _endast_ betalningsknappar för PayPal](payments-options.md#use-only-paypal-payment-buttons) - och _inte_ använda betalningsalternativet för PayPal-kreditkort. På så sätt kan handlarna tillhandahålla olika betalningsalternativ, inklusive betalningsknapparna Venmo och PayPal, och använda en befintlig kreditkortsleverantör i stället för betalningsalternativet för PayPal-kreditkort.

![Ny](../assets/new.svg)<!-- Issue PAY-4050 --> har lagt till en [datavisualiseringsvy](/help/payment-services/payouts.md#payouts-data-visualization-view) som visas på startsidan för betalningstjänsten för statusrapporten för orderbetalning.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-4486--> Tidigare visades inte PayPal PayLater-knappen i utcheckningen för handlare i Storbritannien. Problemet är löst.

![Åtgärdat problem](../assets/fix.svg)<!-- Issue PAY-4485--> Visualiseringsvyer av rapportdata visas nu på [!DNL Payment Services] Hem när [!DNL Payment Services] är inaktiverat.

_25 januari 2023_

![Känt fel](../assets/bug.svg)<!-- Issue PAY-4102 --> Det går inte att konfigurera Commerce Services i nya installationer av [!DNL Payment Services]. Det går inte att återge [!DNL Payment Services]. Åtgärda problemet genom att uppdatera tillägget [!DNL Payment Services] till version 1.5.3.

_12 september 2022_

![Nytt](../assets/new.svg)<!-- Issue PAY-3705 --> `increment_id` är nu tillgängligt för användning i avstämning av utbetalningar i externa ERP-system. Den sprids till `custom_id` _och_ `invoice_id`, som visas både på PayPal-webkroken och i handlaraktivitetsinformationen för en utbetalning.

_31 augusti 2022_

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3629 --> När en ny handlare öppnar startsidan för [!DNL Payment Services] för första gången läses sidan nu in omedelbart för att visa innehållet i stället för att en uppdatering av sidan krävs.

_9 augusti 2021_

![Ny](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay är nu tillgänglig som en smart PayPal-knapp. Med det här [betalningsalternativet](payments-options.md#apple-pay-button) kan kunder använda Touch ID-funktionen på sin iOS- eller macOS-enhet för att välja Apple Pay. Apple Pay behandlar betalningen med hjälp av de betalnings- och betalkortsuppgifter som lagras på enheten.

_28 juni 2021_

![Nya](../assets/new.svg)<!-- Issue PAY-1720 --> tvister om butiksorder finns nu i [statusrapporten för orderbetalning](/help/payment-services/order-payment-status.md#view-disputes). Du kan lösa tvister genom att navigera direkt till PayPal Resolution Center från [!DNL Payment Services].

![Nya](../assets/new.svg)<!-- Issue PAY-2854 --> förbättringar av användarupplevelsen från startsidan för [!DNL Payment Services] inkluderar möjligheten att ändra en konfiguration på den aktuella arvsnivån och förbättringar av visningen av sidhuvudet och navigeringen.

![Nytt](../assets/new.svg)<!-- Issue PAY-2854 --> Du kan nu se varningar när du växlar från sandlådeläge till produktionsläge och när du försöker navigera bort från en vy med uppdateringar som inte har sparats.

![Nytt](../assets/new.svg)<!-- Issue PAY-2761 --> Nu kan du anpassa de data som visas i [rapporten om betalningsstatus](/help/payment-services/order-payment-status.md#show-and-hide-columns) och [utbetalningsrapporten](/help/payment-services/payouts.md#show-and-hide-columns) genom att visa eller dölja kolumner med hjälp av kontrollen Kolumninställningar.

+++

>[!NOTE]
>
> Versioner inträffar ofta för att leverera nya funktioner och korrigeringar efter behov. Versionsschemat är inte fast.

## v2.14.0

_26 februari 2026_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg)<!-- PAY-6400 --> har lagt till en **[!UICONTROL Line Items Enabled]**-konfiguration för att aktivera eller inaktivera sändning av radobjekt och mängduppdelning i PayPal. Den här inställningen hjälper dig att lösa utcheckningsproblem när tillägg från tredje part lägger till anpassade avgifter som inte stöds av [!DNL Payment Services]. Mer information finns i [Radobjekt](line-items.md).

![Ny](../assets/new.svg)<!-- PAY-6457 --> har lagt till [Express-betalningsknappar i början av utcheckningen](payments-options.md#express-checkout-buttons) för snabbare utcheckning.

![Nytt](../assets/new.svg)<!-- PAY-6458 --> Stöd har lagts till för [lokala betalningsmetoder (LPM)](payments-options.md#local-payment-methods) för regionspecifika och lokala betalningsalternativ. Marknadsförare kan aktivera eller inaktivera tillgängliga LPM:er direkt i [Commerce](configure-admin.md#local-payment-methods).

![Nytt](../assets/new.svg)<!-- PAY-6377 --> har lagt till en [köpares sandlådekonfiguration](sandbox.md#buyers-country) för att simulera köparens plats och kontrollera vilka betalningsmetoder som återges.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6458 --> Förbättrad kompatibilitet med PayPals bedrägerifilter genom att skicka data om köparens e-postadress, vilket förbättrar möjligheterna till bedrägeriskydd.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6413 --> Ett problem där PayPal-utcheckningen inte kunde slutföras för virtuella produkter på grund av en utebliven leveransadress har korrigerats.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6450 --> Ett problem där PayPal-knapputcheckningsfel inte hanterades korrekt på produktinformationssidor, minicart, kundvagn och övre delen av utcheckningen har åtgärdats.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6453 --> Inaktiverade återkopplingar på serversidan i GraphQL-utcheckning för att förhindra konflikter vid utcheckning.

![Ett problem har korrigerats](../assets/fix.svg)<!-- PAY-6456 --> Konfigurationsbeskrivningen för [Apple Pay](configure-admin.md#apple-pay) har uppdaterats för att klargöra att Apple avvisar betalningar från overifierade domäner. Handlare måste verifiera alla domäner där Apple Pay-knappar används. Begränsningar för länder gäller.

## v2.13.3

_14 januari 2026_

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6399 --> Ett problem där fel vaulterat kort användes vid en administratörsutcheckning har korrigerats. Nu används det valda kortet korrekt vid beställning.

## v2.13.2

_5 januari 2026_

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6390 --> Allmänna förbättringar och optimeringar genom att implementera förbättrad JS-miniatyrbild.

## v2.13.1

_18 december 2025_

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6355 --> Ett problem där handlare inte kunde välja leveransmetod vid utcheckning har korrigerats.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6347 --> Förbättrad motståndskraft mot utcheckning genom att ta bort onödiga API-anrop.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6368 --> Implementerade en reservmekanism för inläsning av Payments SDK när den primära domänen inte är tillgänglig, vilket säkerställer att kreditkortsfälten förblir tillgängliga vid utcheckning.

## v2.13.0

_10 november 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-xxxx --> Nu, [!DNL Payment Services] stöder PayPals **One-Time Checkout (OTC)** modal, med inbyggd kontakt- och leveransinformation.

![Nytt](../assets/new.svg)<!-- PAY-xxxx --> Förbättrad mobilupplevelse genom **PayPal app-switch-autentisering**, tillsammans med förbättrad API-integrering för smidigare användarresor. Den här funktionen är bara tillgänglig för [!DNL Payment Services]-baserade kunder i USA.

![Nytt](../assets/new.svg)<!-- PAY-xxxx --> **3D Secure-autentisering (3DS)** har lagts till **Stöd för Fastlane för att uppfylla kraven för** Stark kundautentisering (SCA). Detta gör att handlare i Storbritannien och EU [!DNL Payment Services] kan bearbeta transaktioner med **3DS-autentisering**, vilket förbättrar förebyggande av bedrägerier och säkerställer efterlevnad av regionala bestämmelser.

![Nytt](../assets/new.svg)<!-- PAY-xxxx --> Nu kan [!DNL Payment Services] handlare välja mellan **ljusa och mörka teman** för Fastlane-utcheckningskomponenten, så att utcheckningssidorna matchar webbplatsens design. Om anpassade format inte uppfyller tillgänglighetsstandarderna återställs systemet automatiskt till standardinställningarna.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-xxxx --> Ett inläsningsproblem har korrigerats under **administratörsutcheckning med 3DS-utmaning**.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-xxxx --> Förbättrad **validering vid lagring av betalningskonfiguration** via API.

## v2.12.2

_23 september 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6275 --> Avvisade [!DNL Fastlane] transaktioner i fångstläge skapar inte längre order i Commerce.

## v2.12.1

_18 september 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Åtgärdat problem](../assets/fix.svg)<!-- PAY-6164 --> Nu använder [!DNL Payment Services] basvalutan för de tillgängliga leveransmetoderna i [PayPals återanrop på serversidan (SSSC)](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/).

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6267 --> Blocket **Leverera till** är dolt på utcheckningssidan när **ISPU (In-Store Pickup)** har valts.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-6271 --> Nu [!DNL Payment Services] visar sparad kreditkortsinformation från PayPal PayFlow i avsnittet **Kundkonto** > **Lagrade betalningsmetoder**.

## v2.12.0

_20 augusti 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-6022 --> [Fastlane](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options) erbjuder ett snabbare köp vid gästutcheckningar.

![Nytt](../assets/new.svg)<!-- PAY-6168 --> har lagt till [`addProductsToNewCart`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)-mutationen i [!DNL Payment Services] för att möjliggöra mjukare övergångar och bättre återanvändning av kundvagnen.

![Nytt](../assets/new.svg)<!-- PAY-6169 --> har lagt till [`setCartAsInactive`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)-mutationen i [!DNL Payment Services] för att förbättra livscykelhanteringen för offerter.

![Nytt](../assets/new.svg)<!-- PAY-6227 --> Vid utcheckning med PayPal hoppar [!DNL Payment Services] över popup-fönstret för orderbekräftelse för en snabbare inköpsprocess. Detta aktiveras av [serversidans återanrop](payments-options.md#server-side-shipping-callback), som beräknar frakt och summor direkt på PayPals granskningssida.

![Ny](../assets/new.svg)<!-- PAY-6234 --> har lagt till en ny funktion för betalningsalternativet [Betala senare](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options). Nu erbjuder BNPL-meddelandekonfiguratorn större flexibilitet när det gäller att visa meddelanden om senare betalning på kundens utcheckningssidor.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5505 --> Nu anger [!DNL Payment Services] offerten som inaktiv när ett popup-fönster för Google Pay eller PayPal stängs på produktsidan.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services] tillåter inte längre att order skapas från tomma citattecken.

## v2.11.1

_14 mars 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5849 --> Ett problem som påverkade [Radobjekt](line-items.md) under utcheckningen har korrigerats. [!DNL Payment Services] har nu förbättrat tillförlitligheten i utcheckningsprocessen för **Radobjekt**. Om du stöter på ett liknande problem kontaktar du din [!DNL Payment Services]-säljare för att få hjälp.

## v2.11.0

_13 mars 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare


![Nytt](../assets/new.svg)<!-- PAY-5938 --> Nu, [!DNL Payment Services] tillåter handlare att hantera betalningsinställningar för att maximera flexibiliteten i sin verksamhet. Den här versionen förbättrar möjligheten att bifoga [flera PayPal-konton](configure-admin.md#use-multiple-paypal-accounts) för de regioner och varumärken som en handlare stöder. Vårt säljteam kan tillhandahålla en startlänk för att konfigurera din webbplats och lagra visningsomfattningar.

![Nytt](../assets/new.svg)<!-- PAY-5968 --> Nu [!DNL Payment Services] uppdaterar Admin-konfigurationen med värdena **PayPal Merchant ID** och **PayPal Merchant Status** . Dessa värden ger säljarna bättre synlighet för deras PayPal-kontostatus.

![Ett problem som orsakade fel i alla orderplaceringar med version v2.9.0 har åtgärdats.](../assets/fix.svg)<!-- PAY-5816 --> Normal ordningsfunktionalitet återställdes i [!DNL Payment Services].

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5825 --> Ett problem där Apple Pay mini-cart använde felaktig URL för beräknade summor för inloggade kunder har korrigerats. Nu säkerställer [!DNL Payment Services] korrekta totalberäkningar.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5826 --> Förbättrad tillförlitlighet för orderhantering genom att lösa ett problem som orsakade ett HTTP 500-fel när offertstatusen ändrades till `inactive`.

![Ett problem har korrigerats där &#x200B;](../assets/fix.svg)<!-- PAY-5849 --> orsakade undantag för decimalkvantiteter under 1. `LineItemProvider` [!DNL Payment Services] har nu bättre stöd för bråkkvantiteter.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5868 --> Korrigerade ett fel på presentkortsbeloppet vid utcheckning. [!DNL Payment Services] garanterar nu korrekta värden under utcheckningsprocessen.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5911 --> Korrigerade fel när leveranser skapades för beställningar som gjorts med icke-[!DNL Payment Services] onlinebetalningsmetoder, vilket förbättrar den övergripande tillförlitligheten.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services] erbjuder nu en smidigare utcheckning genom att lösa ett problem där Apple Pay inte kunde göra en beställning när ett annat kreditkort valdes i plånboken.

![Korrigerat problem](../assets/fix.svg)<!-- PAY-5971 --> [!DNL Payment Services] dirigerar inte längre om kunder till ordergranskningssidan när Apple Pay misslyckas, vilket förhindrar onödiga avbrott i utcheckningen.

## v2.10.3

_24 februari 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigerat problem](../assets/fix.svg)<!-- PAY-xxxx --> Förbättrad övergripande stabilitet och prestanda.

![Åtgärdat problem](../assets/fix.svg)<!-- PAY-xxxx --> Allmänna förbättringar och optimeringar. Korrigerade kritiska fel från v2.10.2.

## v2.10.2

_21 februari 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Känt fel](../assets/bug.svg)<!-- PAY-xxxx --> innehåller viktiga fel som kan påverka stabilitet och prestanda. Adobe rekommenderar att du uppgraderar till v2.10.3 i stället för att använda den här versionen (v2.10.2).

## v2.10.1

_5 februari 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-5813 --> Stöd för Adobe Commerce 2.4.8 och PHP 8.4 har lagts till.

## v2.10.0

_13 december 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services] har nu stöd för GraphQL-slutpunkter för säkringar utan köp, vilket gör att kunder kan spara sina betalningsmetoder utan att slutföra en transaktion.

![Nytt](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services] har nu stöd för [3D-säker autentisering med Google Pay](security.md#3ds), vilket förbättrar säkerheten för handlare och kunder under betalningstransaktioner.

![Korrigera](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services] ger [kunder möjlighet att spara kort direkt i sitt **Mitt konto**](vaulting.md#vaulting-without-purchase), vilket underlättar för dem och förenklar framtida utcheckningar. `Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms` &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/).

![Åtgärda](../assets/fix.svg)<!-- PAY-5762 --> Ett problem där kupongkoder inte tillämpades på ordergranskningssidan när ordern initierades från produktinformationssidan (PDP) har åtgärdats.

![Korrigera](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services] visar nu beskrivningar och faktureringsadresser för [vaulted-kort på utcheckningssidan](vaulting.md), vilket ger kunderna mer insyn i deras sparade betalningsmetoder.

![Korrigera](../assets/fix.svg)<!-- PAY-5793 --> Med [!DNL Payment Services] kan handlare lagra faktureringsadressen för vaultkort direkt från utcheckningssidan för att säkerställa korrekt och fullständig betalningsinformation.

## v2.9.0

_7 november 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services] har nu stöd för en **uppgraderad SDK-URL för Apple Pay**, vilket förbättrar integreringen för handlare med Apple Pay. Den här funktionen är kompatibel med macOS 14 och senare, och enheter som kör tidigare versioner av macOS kommer inte att visa den här funktionen.

![Nytt](../assets/new.svg)<!-- PAY-5630 --> Uppdaterade sidorna **Kassa**, **Produkt**, **Kart** och **MiniCart** med stöd för den **uppgraderade SDK-URL:en för Apple Pay**, vilket förbättrar användarupplevelsen för handlare som erbjuder Apple Pay som betalningsalternativ.

![Nytt](../assets/new.svg)<!-- PAY-5635 --> Förbättrade leveransuppskattningar **baserade på Apple-betalningsadress**, vilket gör att kunderna kan se korrekta fraktkostnader under utcheckningen.

![Åtgärdade](../assets/fix.svg)<!-- PAY-5661 --> olika **[!DNL Payment Services]problem vid utcheckning**, vilket förbättrade tillförlitligheten i betalningsprocessen för handlare och köpare.

![Korrigera](../assets/fix.svg)<!-- PAY-5692 --> Ett fel har korrigerats där **kundens för- och efternamn** inte lades till i ordningen när **smarta knappar användes för Express-utcheckning**.

![Korrigera](../assets/fix.svg)<!-- PAY-5712 --> Ett problem har korrigerats där handlare **inte kunde slutföra utcheckningen med betalningsalternativet Zero Subtotal Checkout** när det totala beloppet var kostnadsfritt.

## v2.8.1

_13 september 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg)<!-- PAY-5644 --> Ett problem med cacheminnet för SDK-parametrar när flera omfång användes i [!DNL Payment Services] har korrigerats. SDK-konfigurationen cachelagras nu separat för varje scope i stället för under en enda nyckel. Detta garanterar att varje omfångs cache ogiltigförklaras separat, vilket förbättrar tillförlitligheten vid hantering av flera omfång.

## v2.8.0

_13 september 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-5499 --> [!DNL Payment Services] har nu stöd för att skicka spårningsnummerinformation till PayPal när ett [spårningsnummer anges](track-shipment.md) i Adobe Commerce.

![Korrigera](../assets/fix.svg)<!-- PAY-5626 --> [!DNL Payment Services] har optimerat förfrågningsprocessen till handlarregistret när kunderna besöker Commerce utcheckningssida. Tidigare gjordes separata begäranden för varje betalningsmetod (värdfält, Google Pay, Apple Pay och Smart Buttons). Den här förbättringen minskar antalet samtal, vilket förbättrar prestanda och effektivitet under utcheckningsprocessen.

![Korrigera](../assets/fix.svg)<!-- PAY-5645 --> [!DNL Payment Services] förhindrar nu att popup-fönstret PayPal/Google Pay öppnas om kunden inte har godkänt anpassade villkor på utcheckningssidan.

![Korrigera](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services] har åtgärdat ett problem som rör radartikelnedbrytning av moms på PayPal-portalen. Om leveranskostnaden för en order har tillhörande moms inkluderas momsen som en del av leveranskostnaden och visas på det här sättet i den radartikelinformation som visas på PayPal-portalen.

## v2.7.0

_2 augusti 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services] har nu stöd för [radobjektdata på ordernivå](line-items.md). Med den här funktionen kan handlare se detaljerad information om artiklarna i en beställning, till exempel produktinformation, kvantitet och pris (inklusive moms, rabatter och annan relevant information).

![Nytt](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services] förbättrar [konfigurationen i Admin](configure-admin.md#general-configuration)-upplevelsen för handlare för en enklare och mer intuitiv introduktionsprocess. Med den här funktionen kan handlare återställa sina [!DNL Payment Services] ID:n.

![Nytt](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services] innehåller ett meddelande om [betalningsfel](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails). Den här funktionen ger i stort sett meddelanden i realtid om betalningsfel hos handlare, så att beställningarna kan sparas genom att man kontaktar kunden och potentiellt förbättrar problemlösningen.

![Korrigera](../assets/fix.svg)<!-- PAY-5469 --> Ett problem där popup-fönstret **Google Pay blockerades av Safari** har åtgärdats. Nu kan köpare slutföra sina betalningstransaktioner för Google Pay på Safari.

![Åtgärdade](../assets/fix.svg)<!-- PAY-5492 --> ett problem när en handlare lade till anpassade villkor på utcheckningssidan. Under en [Express-utcheckning](payments-options.md#standard-vs-advanced-payments-experience) kan en kund nu acceptera dessa villkor för att slutföra utcheckningen utan några problem.

![Korrigera](../assets/fix.svg)<!-- PAY-5532 --> Förbättrade ISPU-funktioner (In-Store Pickup) med **InstantPurchase**. **ISPU-leveransmetoder** visas inte längre när en kund gör en beställning med **InstantPurchase**.

![Korrigera](../assets/fix.svg)<!-- PAY-5606 --> Ett fel i landsväljaren för **konfigurationssidan** som uppstod när handlarens land är inställt på **Tyskland** har korrigerats.

## v2.6.0

_4 juni 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-4877 --> Nu har [!DNL Payment Services] stöd för [L2/L3-prisfunktioner](/help/payment-services/levels-card-payment-transactions.md#level-2-and-level-3). Den här funktionen är endast tillgänglig för [!DNL Payment Services] kunder med IC++-priser aktiverade. Om du vill använda L2/L3-bearbetningsdata för [!DNL Payment Services] kontaktar du kontohanteraren för [!DNL Payment Services].

Med ![Korrigera](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services] kan du aktivera Apple Pay direkt från tillägget utan att hämta och vara värd för [domänassociationsfilen](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).

## v2.5.0

_23 april 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services] har nu stöd för [Adobe Commerce-riktlinjer för `--db-prefix` parameter &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line) för Adobe Commerce version 2.4.7 och senare.

## v2.4.3

_16 april 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg)<!-- Issue PAY-5106 --> Ett problem som felaktigt fyllde i ordersummorna vid utcheckning mellan PayPal och Adobe Commerce har korrigerats. Nu kan Merchants se till att ordersummorna är korrekta när man gör en beställning.

## v2.4.2

_11 april 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- Issue xxx --> Stöd för Adobe Commerce 2.4.7 har lagts till.

## v2.4.1

_4 april 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg)<!-- PAY-5322 --> Korrigerade ett PCI-kompatibilitetsproblem med nyare Adobe Commerce-versioner. Nu är [!DNL Payment Services] anpassat till kassakrav i Adobe Commerce som betalningsalternativ.

![Korrigera](../assets/fix.svg)<!-- PAY-5323 --> PayLater och Venmo visas korrekt i Adobe Commerce. Korrigerade ett fel som medgav att administratören inte kunde visa alternativen PayLater och Venmo toggle.

## v2.4.0

_20 mars 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![New](../assets/new.svg)<!-- PAY-4868 --> Merchants kan [konfigurera Google Pay genom hela köpupplevelsen](/help/payment-services/payments-options.md), på samma sätt som andra betalningsknappar i [!DNL Payment Services] via Admin.

![Nytt](../assets/new.svg)<!-- PAY-4381 --> [Betalningstjänster har stöd för Google Pay via GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/) vilket gör att handlare kan ha en headless Commerce-upplevelse av betalningsmetoden Google Pay.

![Nytt](../assets/new.svg)<!-- PAY-4878 --> Nu har den grundläggande funktionen [!DNL Payment Services] för utcheckning paketerats för Adobe Commerce- och Magento Open Source-handlare.[!DNL Payment Services] kan nu stödja handlare med företag i någon av de 200 olika geografiska regionerna världen över.[!DNL Payment Services] grundläggande utcheckning ger alternativen debit/credit, PayPal, Venmo (där det är tillgängligt) och PayLater (där det är tillgängligt) i en självbetjäning.

![Korrigera](../assets/fix.svg)<!-- PAY-5291 --> Betalningsbekräftelse för vissa transaktioner kan fördröjas. I så fall kan säljarna nu få en uppdaterad betalningsstatus för en order. [Betalningstjänster identifierar väntande status för en betalningstransaktion](/help/payment-services/order-payment-status.md#payment-status-updates) i en order genom att identifiera väntande transaktioner och övervaka dessa transaktioner i förväg och uppdatera när den väntande statusen har hämtats.

## v2.3.4

_1 mars 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg)<!-- PAY-5244 --> Åtgärdade kompatibilitet för asynkron utcheckning.

![Åtgärdade](../assets/fix.svg)<!-- PAY-5253 --> ett fel där en valvtoken som inte tillhör [!DNL Payment Services] inte kunde tas bort.

## v2.3.3

_14 februari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-5048 --> Stöd för PHP 8.3 har lagts till

![Korrigera](../assets/fix.svg)<!-- PAY-5048 --> Ett fel med flaggan `is_deleted` har korrigerats. Beställningar misslyckas nu inte på grund av statusen `Rejected` som skickades från tillägget.

## v2.3.2

_26 januari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Åtgärda](../assets/fix.svg)<!-- PAY-5183 --> REST/GraphQL-prestandaproblem har åtgärdats. Nu återges kreditkortsknappen när den hämtas via API:t.

## v2.3.1

_7 december 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-5047 --> Varumärket eller betalningsmetoden för kreditkort eller betalkort är nu tillgängliga från följande platser:

- kundordersidan i butiken
- e-postmeddelande med orderbekräftelsen som skickas till kunden
- från vyn [beställningsinformation](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order) i Commerce Admin.

## v2.3.0

_1 december 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-4381 --> [Betalningstjänster har nu stöd för GraphQL-integrering](https://developer.adobe.com/commerce/webapi/graphql/payment-services/). Med GraphQL stöd för betalningsknappar för PayPal, värdbaserade fält och Apple Pay har [!DNL Payment Services] nu stöd för headless Commerce-konfigurationer.

## v2.2.1

_27 september 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-4870 --> Korrigerade ett problem som felaktigt fyllde i det nya rubrikattributet korrekt i Storefront när tilläggsversionen skickades med den senaste versionen. Tidigare kunde du inte utöka `1.3.0` från tillägget `User-Agent header` med [!DNL Payment Services]-versionen av Commerce Services Connector.

## v2.2.0

_30 augusti 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- PAY-4638 --> har lagt till en [integration med Signifyd](fraud-protection.md) som tillhandahåller automatiserade tjänster för bedrägeriskydd.

![Nytt](../assets/new.svg)<!-- PAY-3981 --> [Befordrad Apple Pay till ett separat betalningsalternativ](payments-options.md#apple-pay-button), utanför betalningsknapparna för PayPal, för att öka kundens synlighet för betalningsalternativet och för att tillåta handlare att styra placeringen och formateringen av Apple Pay.

![Nytt](../assets/new.svg)<!-- PAY-4002 --> Förbättrade användarupplevelsen vid utcheckning av kreditkortsfält, inklusive formateringsförbättringar som att lägga till betalningsikoner, för att minska kundens kognitiva belastning och öka konverteringarna.

![Ny](../assets/new.svg)<!-- PAY-4002 --> funktion har lagts till så att handlare kan [sortera ordningen på sina betalningsalternativ](configure-admin.md#paypal-payment-buttons) för att prioritera vissa betalningsalternativ. Den här funktionen uppmuntrar till högre utcheckningsfrekvens för konversationer.

![Nyhet](../assets/new.svg)<!-- PAY-4035 --> Affärsmän kan nu effektivt övervaka butikernas hälsa och identifiera eventuella transaktionsproblem med den nya [Transaktionsrapporten](reporting.md#transactions-report-view) som finns på startsidan för [!DNL Payment Services] Admin. Rapporten innehåller även uppgifter om auktoriseringstariffer för transaktioner och negativa trender för transaktioner.

## v2.1.0

_9 juni 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- Issue xxx --> Stöd för Adobe Commerce 2.4.7-beta1 har lagts till.

![Ny](../assets/new.svg)<!-- Issue xxx --> tillagd [tillgänglighet i följande länder och associerade valutor](introduction.md#availability): Australien, Frankrike, Storbritannien.

![Nytt](../assets/new.svg)<!-- Issue PAY-4296 --> tillagt [utökade resurser för administratörsroller](configure-admin.md#configure-roles) så att administratörsanvändare kan skapa och hantera beställningar för kunder och se[!DNL Payment Services] på menyn Försäljning.

![Nytt](../assets/new.svg)<!-- Issue PAY-4236 --> har lagts till [automatiskt annullering för order som orsakar fel vid utcheckning](checkout.md#order-auto-voided-if-error).

![Ny](../assets/new.svg)<!-- Issue PAY-4183 --> funktion har skapats för att [visa alternativknappen för betalning av kredit-/betalkort](payments-options.md#paypal-debit-or-credit-card-button) på utcheckningssidan.

## v2.0.0

_10 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg)<!-- Issue PAY-4152 --> Stöd för PHP 8.2 och Adobe Commerce 2.4.6 har lagts till. Inte kompatibelt med PHP 7.x.

## v1.6.1

_10 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Åtgärdade](../assets/fix.svg)<!-- Issue PAY-4226 --> ett fel som förhindrade nya [!DNL Payment Services]-handlare från att använda utcheckning i administratören.[!DNL Payment Services] använde tidigare Commerce kund-ID, som inte finns för nya kunder.

![Korrigera](../assets/fix.svg)<!-- Issue PAY-4205 --> Ett problem som orsakade att det angivna leveransadressläget ersattes av läget i standardskatteinställningarna vid utcheckning med alternativet [PayPal](payments-options.md#paypal-payment-buttons) har åtgärdats. Nu kan kunderna få sina beställningar levererade till ett annat tillstånd än det som konfigurerats som standard i handlarens skatteinställningar.

![Åtgärdade](../assets/fix.svg)<!-- Issue PAY-4202 --> ett problem som hindrade kunder från att använda kortvalsfunktionen för att slutföra ett köp eller ta bort en betalningsmetod i säkert läge för en butik [med `Authorize and Capture` betalningsåtgärden &#x200B;](production.md#set-payment-services-as-payment-method). Tidigare uppstod ett fel av typen &quot;Provider Vault ID not found&quot; när kunden försökte använda eller ändra sina kreditkort.

## v1.6.0

_17 februari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Nytt](../assets/new.svg)<!-- Issue PAY-3540 --> har lagts till [Kompatibilitetsfunktionen PCI 3DS för handlare som handlar i EU och Storbritannien](security.md#3ds). Detta extra säkerhetsskikt, som kräver att köpare autentiserar med kreditkortsutfärdaren, bidrar till att förhindra onlinebedrägerier och krävs som en del av EU:s regler för regelefterlevnad.

![Nytt](../assets/new.svg)<!-- Issue PAY-3609 --> har lagt till möjligheten att [aktivera kortvalsning i Admin](vaulting.md#use-vaulting-in-the-admin). Detta gör att handlare kan skapa en order för kunder i administratören med sina betalningsmetoder som är säkra.

## v1.5.4

_29 januari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-4110 --> Ett problem som hindrade köpare från att göra en beställning med hjälp av betalningsknappar på produktsidan, i minikundvagnen och i kundvagnen har åtgärdats. Köparna kan nu slutföra beställningarna.

## v1.5.3

_25 januari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-4102 --> har släppt en korrigering för ett bakåtkompatibelt, känt fel. Den här versionen låser tilläggversionen för tjänst-ID till den senaste stabila versionen, vilket innebär att nya [!DNL Payment Services]-installationer kan konfigurera Commerce Services igen.

## v1.5.2

_22 december 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3992 --> Förbättrad fakturering i [!DNL Payment Services] när en betalningsmetod avvisas.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services] visar nu PayPal-betalningsknappar korrekt för handlare med hjälp av [Fire Checkout-mallen](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} för utcheckningssidan. Tidigare visades knapparna i minikorgen ibland.

## v1.5.1

_23 november 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Nytt](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services] inkluderar nu versionsnumret i användaragenthuvudet så att begäranden kan spåra, filtrera eller ta bort oanvända slutpunkter.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services] visar nu orderdata korrekt när en order placeras från produktsidan med betalningsknappar.

## v1.5.0

_18 november 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Nytt](../assets/new.svg)<!-- Issue PAY-3880 --> En kund kan nu [vault (save) sin kreditkortsinformation vid utcheckning](vaulting.md) och använda den vid ett senare köp för samma eller en annan butik inom samma handlarkonto.

![Nya](../assets/new.svg)<!-- Issue PAY-3950 -->-handlare kan nu aktivera funktionen [Direktköp av Commerce](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) för sina butiker så att kunderna (med [betalkortsinformation](vaulting.md)) kan göra utcheckningen snabbare.

## v1.4.1

_14 oktober 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Åtgärda](../assets/fix.svg)<!-- Issue PAY-3766 --> När en kunds betalningsmetod avvisas är det synliga felmeddelandet mer beskrivande. Kunden uppmanas att ange betalningsinformation igen och försöka igen, prova en annan betalningsmetod eller kontakta sin bank om transaktionen avvisas.

## v1.4.0

_30 september 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Nytt](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services] innehåller nu möjligheten att konfigurera ett handlarkonto för att [använda flera PayPal-affärskonton](configure-admin.md#use-multiple-paypal-accounts). På så sätt kan handlaren driva butikerna i olika länder med olika valutor eller använda Adobe Commerce för en del av verksamheten.

![Nyhet](../assets/new.svg)<!-- Issue PAY-3231 --> Marknadsförare kan [lägga till en [!UICONTROL Soft Descriptor]](configure-admin.md) till webbplatser eller en enskild butiksvy som visas i kundtransaktionens bankutdrag för att identifiera varumärken, butiker eller produktrader.

![Nytt](../assets/new.svg)<!-- Issue PAY-3707 --> [Aktivera eller inaktivera kreditkortsfält och PayPal-betalningsknappar](configure-admin.md#paypal-payment-buttons) för utcheckning i inställningarna för [!DNL Payment Services].

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3546 --> När en kund klickar på **[!UICONTROL Edit cart]** dirigeras sidan om till kundvagnssidan och de uppdaterade objekten visas i stället för att en tom kundvagn visas.

## v1.3.1

_6 september 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Ett problem har åtgärdats](../assets/fix.svg)<!-- Issue PAY-3663 --> När en handlares butik hämtar en order som har auktoriserats med en icke-global valuta slutförs hämtningsprocessen och inget fel visas.

## v1.3.0

_9 augusti 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Ny](../assets/new.svg)<!-- Issue PAY-XX --> allmän tillgänglighetsversion -[!DNL Payment Services] stöds nu [av  [!DNL Adobe Commerce]  och [!DNL Magento Open Source] versionerna 2.4.0 till 2.4.5](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay är nu kompatibelt med webbläsaren Safari v15.5 på mobiler och datorer.

## v1.2.0

_29 juni 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Känt fel](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay är inte kompatibelt med webbläsaren Safari v15.5 på mobiler och datorer. När du använder Safari version 15.5 kan du inte slutföra utcheckningen med Apple Pay.

![Ett problem har korrigerats](../assets/fix.svg)<!-- Issue PAY-3264 --> När en inloggad användare valde en annan fakturerings-/leveransadress än standardadressen för sitt konto misslyckades utcheckningen. Nu skickas den valda fakturerings-/leveransadressen (i stället för den sparade standardadressen) och utcheckningen har slutförts.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3314 --> Om du inaktiverar betalningsknappar för PayPal för utcheckning visas inga fel.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3330 --> Betalningar misslyckas inte längre vid utcheckning när en gästanvändare anger ett telefonnummer som innehåller streck.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> När autentiseringsuppgifterna för Commerce Services är ogiltiga visas ett inloggningsfel i startsidan för [!DNL Payment Services] i Admin.[!DNL Payment Services]

![Känt fel](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] är inte kompatibelt med `commerce-data-export` v101.20 eller senare, vilket gör den inkompatibel med [[!DNL Channel manager] extension](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html).

## v1.1.0

_31 mars 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Ny](../assets/new.svg)<!-- Issue PAY-2127 --> allmän tillgänglighetsversion -[!DNL Payment Services] stöds nu [av  [!DNL Adobe Commerce]  och [!DNL Magento Open Source] versionerna 2.4.0 till 2.4.4](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![Nytt](../assets/new.svg)<!-- Issue PAY-2682 --> Tillägget [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] är nu tillgängligt för kanadensiska handlare. Handlare kan visa betalningskonfigurationen på antingen [franska](introduction.md?lang=fr#accepted-credit-cards-and-currencies) eller [engelska](introduction.md#accepted-credit-cards-and-currencies).

![Nytt](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services] stöder [kanadensiska dollar (CAD)](introduction.md#accepted-credit-cards-and-currencies) för kreditkort och PayPal-transaktioner.

![Nyhet](../assets/new.svg)<!-- Issue PAY-2680 --> Merchants kan [inboard [!DNL Payment Services]](onboard.md)-tillägg på engelska eller franska.

![Nya](../assets/new.svg)<!-- Issue PAY-2678 -->-handlare kan nu visa ekonomiska rapporter, både [Beställningsbetalningsstatus](order-payment-status.md) och [Utbetalningsrapporter](payouts.md), i kanadensiska dollar (CAD).

![Det åtgärdade problemet](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services] är nu kompatibelt med [PHP 8.1](https://www.php.net/releases/8.1/en.php).

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-3017 --> Förbättrad sandlådelägesvarning för att visa korrekta varningar i flera butiker.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-2742 --> Du kan nu aktivera och inaktivera tillgängliga betalningsmetoder, som Venmo, på butiksvynivå. Tidigare kunde du bara konfigurera betalningsmetoder per webbplats.

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-2277 --> Du kan nu selektivt [aktivera eller inaktivera enskilda PayPal-betalningsknappar](configure-admin.md#payment-buttons).

![Korrigerat problem](../assets/fix.svg)<!-- Issue PAY-2561 --> Produkter som tagits bort tidigare visas inte i kundvagnen på sidan _Granska beställning_.

![Känt fel](../assets/bug.svg)<!-- Issue PAY-2842 --> Testa kreditkortstransaktioner [&#x200B; kan misslyckas med PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html) när betalningar bearbetas i en sandlådemiljö.

## v1.0.0

_29 november 2021_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.0 och senare

![Ny](../assets/new.svg)<!-- Issue PAY-2127 --> allmän tillgänglighetsrelease -[[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html) stöds nu av [!DNL Adobe Commerce] och [!DNL Magento Open Source] version 2.4.0 till 2.4.3-p1.

![Nytt](../assets/new.svg)<!-- Issue PAY-124 --> Tillägget [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] kan installeras antingen för [[!DNL Adobe Commerce]  i molninfrastrukturen](install.md#adobe-commerce-on-cloud-infrastructure) eller för [lokala](install.md#on-premises) instanser. Dessa metoder kräver att ett kommandoradsgränssnitt används.

![Nytt](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] har stöd för ett [sandlådekonto](sandbox.md) som gör att handlare kan utvärdera tillägget i testläge.

![Nya](../assets/new.svg)<!-- Issue PAY-666 --> handlare kan [konfigurera tillägget Betalningstjänster](configure-admin.md) med grundläggande betalningsbeteenden, som att använda [`Authorize and Capture`](production.md#set-payment-services-as-payment-method)-växling mellan sandlådor och produktionsmiljöer.

![Nytt](../assets/new.svg)<!-- Issue PAY-780 --> Dina kunder kan checka ut med [!DNL Payment Services] eller via [manuell orderhantering](create-order.md).

![Ny](../assets/new.svg)<!-- Issue PAY-1856 --> Omfattande rapportering, via [status för orderbetalning](order-payment-status.md) och [Utbetalningsrapporter](payouts.md), finns tillgängliga för [!DNL Payment Services] så att du får en tydlig överblick över dina butiksbeställningar och relaterade betalningar.

![Nytt](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services] har stöd för flexibla nivåindelade priser, baserat på den totala bearbetningsvolymen, som är anpassade till alla handlare.

![Nytt](../assets/new.svg)<!-- Issue PAY-1443 --> Du kan enkelt [anpassa utseendet och känslan](payments-options.md) för betalningsknapparna och kreditkortsfälten för tillägget [!DNL Payment Services].

![Ett känt fel](../assets/bug.svg)<!-- Issue PAY-2473 --> [Om du använder &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html) felaktiga dispositionsnycklar under installationen av tillägget förhindrar du användaren från att [autentisera](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) med rätt `MAGEID`.

![Känt fel](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] rapporter [kanske inte synkroniseras omedelbart](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html).

![Känt fel](../assets/bug.svg)<!-- Issue PAY-2475 --> Ditt [PayPal-sandlådekonto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html) för [!DNL Payment Services] kan inte verifieras om du skapar det kontot under introduktionen.
