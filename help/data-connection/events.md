---
title: Beteendehändelser
description: Lär dig vilka data varje beteendehändelse fångar.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '4528'
ht-degree: 0%

---

# [!DNL Data Connection] beteendehändelser

Nedan visas de Commerce beteendehändelser som är tillgängliga när du installerar tillägget [!DNL Data Connection]. De data som dessa händelser samlar in skickas till Adobe Experience Platform. Du kan också skapa [anpassade händelser](custom-events.md) för att samla in ytterligare data som inte anges i kartongen.

Förutom de data som samlas in av följande händelser, får du även [andra data](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) från Adobe Experience Platform Web SDK.

Beteendehändelserna samlar in anonyma beteendedata från era kunder när de surfar på er webbplats. Ni kan använda de data som dessa event samlar in för att skapa kampanjer och kampanjer som riktar sig till en viss uppsättning kunder.

>[!NOTE]
>
>Alla beteendehändelser inkluderar fältet [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html), som innehåller kundens e-postadress, när den är tillgänglig, och ECID.

## Storefront-händelser

Händelser i Storefront hämtar data från kundernas interaktioner på webbplatsen och inkluderar händelser som [`addToCart`](#addtocart), [`pageView`](#pageview), [`createAccount`](#createaccount), [`editAccount`](#editaccount), [`startCheckout`](#startcheckout), [`completeCheckout`](#completecheckout), [`signIn`](#signin), [`signOut`](#signout) och så vidare. Händelser i Storefront gäller endast enkla och konfigurerbara produkter.

### addToCart

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en produkt läggs till i varukorgen eller när kvantiteten av en produkt i varukorgen ökas. | `commerce.productListAdds` |

#### Data som samlats in från addToCart

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListAdds` | Anger om en produkt har lagts till i en kundvagn. Värdet `1` anger att en produkt har lagts till. |
| `commerce.cart.cartID` | Det unika ID som identifierar kundens kundvagn. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### openCart

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en ny kundvagn skapas, det vill säga när en produkt läggs till i en tom kundvagn. | `commerce.productListOpens` |

#### Data som samlats in från openCart

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListOpens` | Anger om en vagn skapades. Värdet `1` anger att en vagn skapades. |
| `commerce.cart.cartID` | Det unika ID som identifierar kundens kundvagn. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### removeFromCart

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses varje gång en produkt tas bort eller varje gång som kvantiteten av en produkt i vagnen minskas. | `commerce.productListRemovals` |

#### Data som samlats in från removeFromCart

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListRemovals` | Anger om en produkt har tagits bort från kundvagnen. Värdet `1` anger att en produkt har tagits bort från kundvagnen. |
| `commerce.cart.cartID` | Det unika ID som identifierar kundens kundvagn. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### shoppingCartView

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kundvagnssida läses in. | `commerce.productListViews` |

#### Data som samlats in från shoppingCartView

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListViews` | Anger om en produktlista har visats. |
| `commerce.cart.cartID` | Det unika ID som identifierar kundens kundvagn. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `commerce.order` | Innehåller information om väntande order för en eller flera produkter. |
| `commerce.order.discountAmount` | Anger det rabattbelopp som tillämpas på hela ordern. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### pageView

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när någon sida läses in. | `web.webpagedetails.pageViews` |

#### Data som samlats in från pageView

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `web.webPageDetails.pageViews` | Anger om en sida har lästs in. En `value` av `1` anger att sidan lästes in. |
| `web.webPageDetails.URL` | Webbsidans normativa eller vanliga URL. Det här kan vara den faktiska URL som används för att nå sidan, som skulle spelas in med `Web Link`. |
| `web.webPageDetails.name` | Webbsidans normativa namn. Det här namnet är inte nödvändigtvis sidrubriken eller direkt kopplat till sidinnehållet, utan används för att ordna en webbplats sidor i klassificeringssyfte. |
| `web.webReferrer.URL` | URL-adressen till webbsidan som en kund besökte innan han/hon klickade på en länk till webbplatsen. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### productPageView

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när någon produktsida läses in. | `commerce.productViews` |

#### Data som samlats in från productPageView

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productViews` | Anger om produkten visades. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### startCheckout

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när kunden klickar på en utcheckningsknapp. | `commerce.checkouts` |

#### Data som samlats in från startCheckout

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.checkouts` | Anger om en åtgärd inträffade under utcheckningsprocessen. |
| `commerce.cart.cartID` | Det unika ID som identifierar kundens kundvagn. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### completeCheckout

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när kunden lägger en order. | `commerce.purchases` |

#### Data som samlats in från completeCheckout

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.purchases` | Anger om en order har godkänts. |
| `commerce.order` | Innehåller information om den placerade beställningen för en eller flera produkter. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.payments` | Listan över betalningar för den här ordern. |
| `commerce.order.payments.paymentTransactionID` | Unik identifierare för den här betalningstransaktionen. |
| `commerce.order.payments.paymentAmount` | Betalningens värde. |
| `commerce.order.payments.paymentType` | Betalningsmetoden för den här ordern. Alternativen är: `cash`, `credit_card`, `debit_card`, `gift_card`, `check`, `paypal`, `wire_transfer`, `credit_card_reference`, `other`. |
| `commerce.order.payments.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.order.taxAmount` | Det skattebelopp som köparen betalar som en del av den slutliga betalningen. |
| `commerce.order.discountAmount` | Anger det rabattbelopp som tillämpas på hela ordern. |
| `commerce.order.createdDate` | Tid och datum då en ny order skapas i handelssystemet. Exempel: `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Leveransinformation för en eller flera produkter. |
| `commerce.shipping.shippingMethod` | Leveranssätt som kunden väljer, t.ex. standardleverans, snabbare leverans, hämtning i butik osv. |
| `commerce.shipping.shippingAmount` | Det belopp som kunden måste betala för frakt. |  | `shipping` | Leveransinformation för en eller flera produkter. |
| `commerce.shipping.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

## Kundprofilshändelser

Profilhändelser som hämtats från butiken innehåller kontoinformation, som `signIn`, `signOut`, `createAccount` och `editAccount`. Dessa data används för att fylla i viktig kundinformation som behövs för att bättre definiera segment eller genomföra marknadsföringskampanjer, som att skicka rabatterbjudanden, bekräftelser av kontoändringar osv. Det finns liknande profilhändelser som hämtats från [serversidan](events-backoffice.md#customer-profile-events).

>[!NOTE]
>
>[Lär dig](custom-identities.md) hur du skapar anpassade identitetsattribut för att förbättra identifieringen av kundprofiler.

### signIn

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund försöker logga in. | `userAccount.login` |

>[!NOTE]
>
> Den här händelsen utlöses när ett försök görs att utföra den specifika åtgärden. Det indikerar inte att åtgärden lyckades.

#### Data som samlats in från signIn

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | En enskild aktör, kontakt eller ägare. |
| `person.accountID` | Hämtar användar-ID:t för kontot. |
| `person.accountType` | Hämtar typ av användarkonto, t.ex. `Personal` eller `Company`, om tillämpligt. |
| `person.personalEmailID` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `personalEmail` | Hämtar kontaktinformation - ett e-postmeddelande och tillhörande information. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `userAccount` | Anger information om lojalitet, inställningar, inloggningsprocesser och andra kontoinställningar. |
| `userAccount.login` | Anger om en besökare försökte logga in. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### signOut

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund försöker logga ut. | `userAccount.logout` |

>[!NOTE]
>
> Den här händelsen utlöses när ett försök görs att utföra den specifika åtgärden. Det indikerar inte att åtgärden lyckades.

#### Data som samlats in från signOut

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `userAccount` | Anger information om lojalitet, inställningar, inloggningsprocesser och andra kontoinställningar. |
| `userAccount.logout` | Anger om en besökare försökte logga ut. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### createAccount

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund försöker skapa ett konto. | `userAccount.createProfile` |

>[!NOTE]
>
> Den här händelsen utlöses när ett försök görs att utföra den specifika åtgärden. Det indikerar inte att åtgärden lyckades.

#### Data som samlats in från createAccount

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | En enskild aktör, kontakt eller ägare. |
| `person.accountID` | Hämtar användar-ID:t för kontot. |
| `person.accountType` | Hämtar typ av användarkonto, t.ex. `Personal` eller `Company`, om tillämpligt. |
| `person.personalEmailID` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `personalEmail` | Hämtar kontaktinformation - ett e-postmeddelande och tillhörande information. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `userAccount` | Anger information om lojalitet, inställningar, inloggningsprocesser och andra kontoinställningar. |
| `userAccount.updateProfile` | Anger om en användare har uppdaterat sin kontoprofil. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### editAccount

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund försöker redigera ett konto. | `userAccount.updateProfile` |

>[!NOTE]
>
> Den här händelsen utlöses när ett försök görs att utföra den specifika åtgärden. Det indikerar inte att åtgärden lyckades.

#### Data som samlats in från editAccount

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | En enskild aktör, kontakt eller ägare. |
| `person.accountID` | Hämtar användar-ID:t för kontot. |
| `person.accountType` | Hämtar typ av användarkonto, t.ex. `Personal` eller `Company`, om tillämpligt. |
| `person.personalEmailID` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `personalEmail` | Hämtar kontaktinformation - ett e-postmeddelande och tillhörande information. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `userAccount` | Anger information om lojalitet, inställningar, inloggningsprocesser och andra kontoinställningar. |
| `userAccount.updateProfile` | Anger om en användare har uppdaterat sin kontoprofil. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

## Sök efter händelser

Sökhändelserna innehåller data som är relevanta för kundens avsikter. Insikt i en köpares avsikter hjälper handlarna att se hur kunderna letar efter artiklar, vad de klickar på och slutligen köper eller överger. Ett exempel på hur ni kan använda dessa data är om ni vill rikta er till befintliga kunder som söker efter den bästa produkten, men aldrig köper produkten. Du måste installera tillägget [[!DNL Live Search]](../live-search/install.md) för att komma åt de här händelserna.

Använd fälten `searchRequest.id` och `searchResponse.id` i både händelserna `searchRequestSent` och `searchResponseReceived` för att korsreferera en sökbegäran till motsvarande söksvar.

### searchRequestSent

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses av följande händelser i sökaren:<br><br>Tryck på Retur, klicka på _Visa alla_<br><br> Utlöses av följande händelser på sökresultatsidor:<br><br>Välj ett filter, Ändra sorteringsordning (_Sortera efter_), Ändra sorteringsriktning (stigande eller fallande), Ändra antalet resultat per sida (_Visa # per sida_) ), Navigera till nästa sida, Navigera till föregående sida, Navigera till en annan sida | `searchRequest` |

>[!NOTE]
>
>Sökhändelser stöds inte på Adobe Commerce Enterprise Edition med B2B-tillägget installerat.

#### Data som samlats in från searchRequestSent

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchRequest` | Anger om en sökbegäran har skickats. |
| `searchRequest.id` | Unikt ID för den här särskilda sökbegäran. |
| `searchRequest.value` | Begärans kvantifierbara värde. |
| `siteSearch` | Innehåller information om sökningen. |
| `siteSearch.filter` | Anger om några filter har använts för att begränsa sökresultaten. |
| `siteSearch.filter.attribute` (filter) | Faktablad för ett objekt som används för att avgöra om det ska inkluderas i sökresultaten. |
| `siteSearch.filter.isRange` | När värdet är true anger värden slutpunkter i ett godkänt värdeintervall. |
| `siteSearch.filter.value` | Attributvärde som används för att avgöra vilka objekt som ska tas med i sökresultatet. |
| `siteSearch.sort` | Anger hur sökresultat ska sorteras. |
| `siteSearch.sort.attribute` (sortera) | Ett attribut som används för att sortera objekt i sökresultat. |
| `siteSearch.sort.order` | Den ordning som sökresultaten ska returneras i. |
| `siteSearch.query` | De termer du sökte efter. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### searchResponseReceived

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när Live Search returnerar resultat för&quot;sökningen när du skriver&quot;-povern eller sökresultatsidan. | `searchResponse` |

>[!NOTE]
>
>Sökhändelser stöds inte på Adobe Commerce Enterprise Edition med B2B-tillägget installerat.

#### Data som samlats in från searchResponseReceived

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchResponse` | Anger om ett söksvar har tagits emot. |
| `searchResponse.id` | Unikt ID för det här specifika söksvaret. |
| `searchResponse.value` | Responsens kvantifierbara värde. |
| `siteSearch.numberOfResults` | Antal returnerade produkter. |
| `siteSearch.suggestions` | En array med strängar som innehåller namnen på de produkter och kategorier som finns i katalogen som liknar sökfrågan. |
| `productListItems` | En array med produkter som lagts till i kundvagnen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

## B2B-event

![B2B för Adobe Commerce](../assets/b2b.svg) För B2B-handlare måste du [installera](install.md#install-the-b2b-extension) tillägget `experience-platform-connector-b2b` för att få åtkomst till de här händelserna.

B2B-händelserna innehåller information om [rekvisitionslistan](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html), till exempel om en rekvisitionslista skapades, lades till eller togs bort från. Genom att spåra händelser som är specifika för rekvisitionslistor kan ni se vilka produkter era kunder köper ofta och skapa kampanjer baserade på dessa data.

### createRequisitionList

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund skapar en rekvisitionslista. | `commerce.requisitionListOpens` |

#### Data som samlats in från createRequisitionList

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListOpens` | Anger initiering av en ny rekvisitionslista. |
| `commerce.requisitionList` | Egenskaperna för den rekvisitionslista som har skapats av kunden. |
| `commerce.requisitionList.ID` | Unik identifierare för rekvisitionslistan. |
| `commerce.requisitionList.name` | Namn på den rekvisitionslista som har angetts av kunden. |
| `commerce.requisitionList.description` | Beskrivning av rekvisitionslistan som anges av kunden. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### addToRequisitionList

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund lägger till en produkt i en befintlig rekvisitionslista eller när en lista skapas. | `commerce.requisitionListAdds` |

#### Data som samlats in från addToRequisitionList

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListAdds` | Anger tillägg av en eller flera produkter i en rekvisitionslista. |
| `commerce.requisitionList` | Egenskaperna för den rekvisitionslista som har skapats av kunden. |
| `commerce.requisitionList.ID` | Unik identifierare för rekvisitionslistan. |
| `commerce.requisitionList.name` | Namn på den rekvisitionslista som har angetts av kunden. |
| `commerce.requisitionList.description` | Beskrivning av rekvisitionslistan som anges av kunden. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `productListItems` | En array med produkter som har lagts till i rekvisitionslistan. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### removeFromRequisitionList

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund tar bort en produkt från en rekvisitionslista. | `commerce.requisitionListRemovals` |

#### Data som samlats in från removeFromRequisitionList

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requsitionListRemovals` | Anger borttagning av en eller flera produkter från en rekvisitionslista. |
| `commerce.requisitionList` | Egenskaperna för den rekvisitionslista som har skapats av kunden. |
| `commerce.requisitionList.ID` | Unik identifierare för rekvisitionslistan. |
| `commerce.requisitionList.name` | Namn på den rekvisitionslista som har angetts av kunden. |
| `commerce.requisitionList.description` | Beskrivning av rekvisitionslistan som anges av kunden. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `productListItems` | En array med produkter som har lagts till i rekvisitionslistan. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |

### deleteRequisitionList

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund tar bort en rekvisitionslista. | `commerce.requisitionListDeletes` |

#### Data som samlats in från deleteRequisitionList

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListDeletes` | Anger att en rekvisitionslista har tagits bort. |
| `commerce.requisitionList` | Egenskaperna för den rekvisitionslista som har skapats av kunden. |
| `commerce.requisitionList.ID` | Unik identifierare för rekvisitionslistan. |
| `commerce.requisitionList.name` | Namn på den rekvisitionslista som har angetts av kunden. |
| `commerce.requisitionList.description` | Beskrivning av rekvisitionslistan som anges av kunden. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
