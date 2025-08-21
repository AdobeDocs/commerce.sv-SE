---
title: Beteendehändelser
description: Lär dig vilka data varje beteendehändelse fångar.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Data Connection] beteendehändelser

Nedan visas de Commerce beteendehändelser som är tillgängliga när du installerar tillägget [!DNL Data Connection]. De data som dessa händelser samlar in skickas till Adobe Experience Platform. Du kan också skapa [anpassade händelser](custom-events.md) för att samla in ytterligare data som inte anges i kartongen.

Förutom de data som samlas in av följande händelser, får du även [andra data](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=sv-SE) från Adobe Experience Platform Web SDK.

Beteendehändelserna samlar in anonyma beteendedata från era kunder när de surfar på er webbplats. Ni kan använda de data som dessa event samlar in för att skapa kampanjer och kampanjer som riktar sig till en viss uppsättning kunder.

>[!NOTE]
>
>Alla beteendehändelser inkluderar fältet [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=sv-SE), som innehåller kundens e-postadress, när den är tillgänglig, och ECID.

## Storefront-händelser

Händelser i Storefront hämtar data från kundernas interaktioner på webbplatsen och inkluderar händelser som `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut` och så vidare. Händelser i Storefront gäller endast enkla och konfigurerbara produkter.

Läs [utvecklardokumentationen](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) om du vill veta mer om butikshändelser.

## Kundprofilshändelser

Profilhändelser som hämtats från butiken innehåller kontoinformation, som `signIn`, `signOut`, `createAccount` och `editAccount`. Dessa data används för att fylla i viktig kundinformation som behövs för att bättre definiera segment eller genomföra marknadsföringskampanjer, som att skicka rabatterbjudanden, bekräftelser av kontoändringar osv.

Läs [utvecklardokumentationen](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) om du vill veta mer om kundprofilshändelser.

## Sök efter händelser

Sökhändelserna innehåller data som är relevanta för kundens avsikter. Insikt i en köpares avsikter hjälper handlarna att se hur kunderna letar efter artiklar, vad de klickar på och slutligen köper eller överger. Ett exempel på hur ni kan använda dessa data är om ni vill rikta er till befintliga kunder som söker efter den bästa produkten, men aldrig köper produkten. Du måste installera tillägget [[!DNL Live Search]](../live-search/install.md) för att komma åt de här händelserna.

Använd fälten `searchRequest.id` och `searchResponse.id` i både händelserna `searchRequestSent` och `searchResponseReceived` för att korsreferera en sökbegäran till motsvarande söksvar.

Mer information om sökhändelser finns i [utvecklardokumentationen](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection).

## B2B-event

![B2B för Adobe Commerce](../assets/b2b.svg) För B2B-handlare måste du [installera](install.md#install-the-b2b-extension) tillägget `experience-platform-connector-b2b` för att få åtkomst till de här händelserna.

B2B-händelserna innehåller information om [rekvisitionslistan](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=sv-SE), till exempel om en rekvisitionslista skapades, lades till eller togs bort från. Genom att spåra händelser som är specifika för rekvisitionslistor kan ni se vilka produkter era kunder köper ofta och skapa kampanjer baserade på dessa data.

Läs [utvecklardokumentationen](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) om du vill veta mer om B2B-händelser.
