---
title: Kontorsaktiviteter
description: Lär dig vilka data varje back office-händelse samlar in.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 0%

---

# [!DNL Data Connection] Tidigare Office-händelser

Följande visar vilka Commerce-händelser för backoffice som är tillgängliga när du installerar tillägget [!DNL Data Connection]. De data som dessa händelser samlar in skickas till Adobe Experience Platform. Du kan också skapa [anpassade händelser](custom-events.md) för att samla in ytterligare data som inte anges i kartongen.

Förutom de data som samlas in av följande händelser, får du även [andra data](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=sv-SE) från Adobe Experience Platform Web SDK.

Back office-händelser innehåller data på serversidan. Dessa data omfattar [orderstatus](#order-status), t.ex. om en order har placerats, annullerats, återbetalats, levererats eller slutförts. Data på serversidan innehåller även information om [kundprofilshändelser](#customer-profile-events), t.ex. om ett konto har skapats, uppdaterats eller tagits bort.

>[!NOTE]
>
>Alla back office-händelser innehåller fältet [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=sv-SE), som innehåller kundens e-postadress, om den är tillgänglig, och ECID.

## Orderstatus

Beställningsstatusdata visar en 360-vy över kundordern. Den här vyn hjälper handlare att målinrikta eller analysera hela orderstatusen bättre när de utvecklar marknadsföringskampanjer. Du kan till exempel upptäcka trender i vissa produktkategorier som fungerar bra vid olika tidpunkter på året. Till exempel vinterkläder som säljer bättre under längre månader eller vissa produktfärger som kunderna är intresserade av under årens lopp. Dessutom kan orderstatusdata hjälpa er att beräkna kundens livslängdvärde genom att förstå en kunds benägenhet att konvertera baserat på tidigare order.

### orderPlaced

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund gör en beställning. | `commerce.backofficeOrderPlaced` |

#### Data som samlats in från orderPlacerade

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.payments` | Listan över betalningar för den här ordern. |
| `commerce.order.payments.paymentTransactionID` | Unik identifierare för den här betalningstransaktionen. |
| `commerce.order.payments.paymentAmount` | Betalningens värde. |
| `commerce.order.payments.paymentType` | Betalningsmetoden för den här ordern. Räknade, anpassade värden tillåtna. |
| `commerce.order.payments.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.order.taxAmount` | Det skattebelopp som köparen betalar som en del av den slutliga betalningen. |
| `commerce.order.discountAmount` | Anger det rabattbelopp som tillämpas på hela ordern. |
| `commerce.order.createdDate` | Tid och datum då en ny order skapas i handelssystemet. Exempel: `2022-10-15T20:20:39+00:00`. |
| `commerce.order.currencyCode` | ISO 4217-valutakoden som används för ordersummor. |
| `commerce.shipping` | Leveransinformation för en eller flera produkter. |
| `commerce.shipping.shippingMethod` | Leveranssätt som kunden väljer, t.ex. standardleverans, snabbare leverans, hämtning i butik osv. |
| `commerce.shipping.shippingAmount` | Det belopp som kunden måste betala för frakt. |
| `commerce.shipping.currencyCode` | ISO 4217-valutakoden som används för leveranssumman. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `commerce.billing.address` | Betalningsadress. |
| `commerce.billing.address.street1` | Information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn |
| `commerce.billing.address.street2` | Ytterligare fält för gatuminivåinformation. |
| `commerce.billing.address.city` | Namnet på staden. |
| `commerce.billing.address.state` | Namnet på läget. Det här är ett frihandsfält. |
| `commerce.billing.address.postalCode` | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `commerce.billing.address.country` | Namnet på det statligt administrerade territoriet. Förutom `xdm:countryCode` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter i ordningen. |
| `productListItems.id` | Identifierare för radartikel för den här produktposten. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |
| `productListItems.categories` | Innehåller information om en produkts kategori. |
| `productListItems.categories.id` | Kategorins unika identifierare. |
| `productListItems.categories.name` | Namnet på kategorin. |
| `productListItems.categories.path` | Sökvägen till kategorin. |
| `productListItems.productImageUrl` | Produktens huvudbild-URL. |

### orderFakturerad

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en handlare skickar en faktura för att begära betalning. | `commerce.backofficeOrderInvoiced` |

#### Data insamlade från orderFakturerade

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.priceTotal` | Det totala priset för den här ordern efter att alla rabatter och skatter har tillämpats. |
| `commerce.order.currencyCode` | ISO 4217-valutakoden som används för ordersummor. |
| `commerce.order.purchaseOrderNumber` | Unik identifierare som tilldelats av köparen för detta inköp eller kontrakt. |
| `commerce.order.payments` | Listan över betalningar för den här ordern. |
| `commerce.order.payments.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.order.payments.paymentType` | Betalningsmetoden för den här ordern. Räknade, anpassade värden tillåtna. |
| `commerce.order.payments.paymentAmount` | Betalningens värde. |
| `commerce.shipping` | Leveransinformation för en eller flera produkter. |
| `commerce.shipping.shippingMethod` | Leveranssätt som kunden väljer, t.ex. standardleverans, snabbare leverans, hämtning i butik osv. |
| `commerce.shipping.shippingAmount` | Det belopp som kunden måste betala för frakt. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter i ordningen. |
| `productListItems.id` | Identifierare för radartikel för den här produktposten. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.categories` | Innehåller information om en produkts kategori. |
| `productListItems.categories.id` | Kategorins unika identifierare. |
| `productListItems.categories.name` | Namnet på kategorin. |
| `productListItems.categories.path` | Sökvägen till kategorin. |

### orderItemsShipped

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en order skickas. | `commerce.backofficeOrderItemsShipped` |

#### Data som samlats in från orderItemsShipped

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.payments` | Listan över betalningar för den här ordern. |
| `commerce.order.payments.paymentTransactionID` | Unik identifierare för den här betalningstransaktionen. |
| `commerce.order.payments.paymentAmount` | Betalningens värde. |
| `commerce.order.payments.paymentType` | Betalningsmetoden för den här ordern. Räknade, anpassade värden tillåtna. |
| `commerce.order.payments.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.order.priceTotal` | Det totala priset för den här ordern efter att alla rabatter och skatter har tillämpats. |
| `commerce.order.purchaseOrderNumber` | Unik identifierare som tilldelats av köparen för detta inköp eller kontrakt. |
| `commerce.order.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.order.lastUpdatedDate` | Den tidpunkt då en viss orderpost senast uppdaterades i handelssystemet. |
| `commerce.shipping` | Leveransinformation för en eller flera produkter. |
| `commerce.shipping.shippingMethod` | Leveranssätt som kunden väljer, t.ex. standardleverans, snabbare leverans, hämtning i butik osv. |
| `commerce.shipping.shippingAmount` | Det belopp som kunden måste betala för frakt. |
| `commerce.shipping.address` | Den fysiska leveransadressen. |
| `commerce.shipping.address.street1` | Primär information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn. |
| `commerce.shipping.address.street2` | Ytterligare gatuinformation, andra raden. |
| `commerce.shipping.address.city` | Namnet på staden. |
| `commerce.shipping.address.state` | Statens namn. Det här är ett frihandsfält. |
| `commerce.shipping.address.postalCode` | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `commerce.shipping.address.country` | Namnet på det statligt administrerade territoriet. Förutom `xdm:countryCode` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `commerce.shipping.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.shipping.trackingNumber` | Spårningsnumret som fraktfirman anger för en orderartikelleverans. |
| `commerce.shipping.trackingURL` | URL:en som spårar leveransstatus för en orderartikel. |
| `commerce.shipping.shipDate` | Det datum då en eller flera artiklar från en order skickas. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `commerce.billing.address` | Betalningsadress. |
| `commerce.billing.address.street1` | Information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn |
| `commerce.billing.address.street2` | Ytterligare fält för gatuminivåinformation. |
| `commerce.billing.address.city` | Namnet på staden. |
| `commerce.billing.address.state` | Namnet på läget. Det här är ett frihandsfält. |
| `commerce.billing.address.postalCode` | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `commerce.billing.address.country` | Namnet på det statligt administrerade territoriet. Förutom `xdm:countryCode` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter i ordningen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |
| `productListItems.categories` | Innehåller information om en produkts kategori. |
| `productListItems.categories.id` | Kategorins unika identifierare. |
| `productListItems.categories.name` | Namnet på kategorin. |
| `productListItems.categories.path` | Sökvägen till kategorin. |

### orderCanceled

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund annullerar en order. | `commerce.backofficeOrderCancelled` |

#### Data insamlade från orderAvbrutna

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.purchaseOrderNumber` | Unik identifierare som tilldelats av köparen för detta inköp eller kontrakt. |
| `commerce.order.cancelDate` | Datum och tid då en kund annullerar en order. |
| `commerce.order.lastUpdatedDate` | Den tidpunkt då en viss orderpost senast uppdaterades i handelssystemet. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |

### orderLineItemRefunded

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund återbetalas för en returartikel. | `commerce.backofficeCreditMemoIssued` |

#### Data insamlade från orderLineItemRefunded

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.lastUpdatedDate` | Den tidpunkt då en viss orderpost senast uppdaterades i handelssystemet. |
| `commerce.order.purchaseOrderNumber` | Unik identifierare som tilldelats av köparen för detta inköp eller kontrakt. |
| `commerce.refunds` | Listan över återbetalningar för den här ordern. |
| `commerce.refunds.transactionID` | Unik identifierare för denna återbetalning. |
| `commerce.refunds.refundAmount` | Återbetalningsvärdet. |
| `commerce.refunds.refundPaymentType` | Betalningsmetoden för den här ordern. Räknade, anpassade värden tillåtna. |
| `commerce.refunds.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter i ordningen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |
| `productListItems.categories` | Innehåller information om en produkts kategori. |
| `productListItems.categories.id` | Kategorins unika identifierare. |
| `productListItems.categories.name` | Namnet på kategorin. |
| `productListItems.categories.path` | Sökvägen till kategorin. |

### orderItemsReturnInitiated

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund begär att få returnera ett objekt. | `commerce.backofficeOrderItemsReturnInitiated` |

#### Data insamlade från orderItemsReturnInitiated

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.returns` | RMA-informationen (Return Merchandise Authorization) för den här beställningen. |
| `commerce.order.returns.returnID` | Unik identifierare för denna RMA (Return Merchandise Authorization). |
| `commerce.order.returns.returnStatus` | Status för RMA (Return Merchandise Authorization), t.ex. Pending, Closed osv. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter i ordningen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |
| `productListItems.categories` | Innehåller information om en produkts kategori. |
| `productListItems.categories.id` | Kategorins unika identifierare. |
| `productListItems.categories.name` | Namnet på kategorin. |
| `productListItems.categories.path` | Sökvägen till kategorin. |
| `productListItems.returnItem` | RMA-informationen (Return Merchandise Authorization) för det här objektet. |
| `productListItems.returnItem.returnStatus` | Status för returnerat objekt, som Väntande, Godkänd och så vidare. |
| `productListItems.returnItem.returnReason` | Orsaken till varför en retur begärs för den här artikeln. |
| `productListItems.returnItem.returnItemCondition` | Villkoret för artikeln som returen begärs för. |
| `productListItems.returnItem.returnResolution` | Den begärda upplösningen för det objekt som returneras, till exempel Återbetalning, Exchange och så vidare. |
| `productListItems.returnItem.returnQuantityRequested` | Numret på det här objektet som kunden begärde att få returnera. |
| `productListItems.returnItem.returnQuantityAuthorized` | Numret på den här artikeln som är auktoriserad att returneras. |
| `productListItems.returnItem.eturnQuantityReceived` | Antalet returnerade artiklar som tagits emot. |
| `productListItems.returnItem.returnQuantityApproved` | Numret på det här objektet med fullständig och godkänd retur. |

### orderItemReturnCompleted

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när ett objekt som en kund har begärt att få returnera har slutförts. | `commerce.backofficeOrderItemsReturnCompleted` |

#### Data insamlade från orderItemReturnCompleted

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.returns` | RMA-informationen (Return Merchandise Authorization) för den här beställningen. |
| `commerce.order.returns.returnID` | Unik identifierare för denna RMA (Return Merchandise Authorization). |
| `commerce.order.returns.returnStatus` | Status för RMA (Return Merchandise Authorization), t.ex. Pending, Closed osv. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter i ordningen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |
| `productListItems.categories` | Innehåller information om en produkts kategori. |
| `productListItems.categories.id` | Kategorins unika identifierare. |
| `productListItems.categories.name` | Namnet på kategorin. |
| `productListItems.categories.path` | Sökvägen till kategorin. |
| `productListItems.returnItem` | RMA-informationen (Return Merchandise Authorization) för det här objektet. |
| `productListItems.returnItem.returnStatus` | Status för returnerat objekt, som Väntande, Godkänd och så vidare. |
| `productListItems.returnItem.returnReason` | Orsaken till varför en retur begärs för den här artikeln. |
| `productListItems.returnItem.returnItemCondition` | Villkoret för artikeln som returen begärs för. |
| `productListItems.returnItem.returnResolution` | Den begärda upplösningen för det objekt som returneras, till exempel Återbetalning, Exchange och så vidare. |
| `productListItems.returnItem.returnQuantityRequested` | Numret på det här objektet som kunden begärde att få returnera. |
| `productListItems.returnItem.returnQuantityAuthorized` | Numret på den här artikeln som är auktoriserad att returneras. |
| `productListItems.returnItem.eturnQuantityReceived` | Antalet returnerade artiklar som tagits emot. |
| `productListItems.returnItem.returnQuantityApproved` | Numret på det här objektet med fullständig och godkänd retur. |

### orderShiEquipmentCompleted

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en leverans är slutförd. | `commerce.backofficeOrderShipmentCompleted` |

#### Data som samlats in från orderShiEquipmentCompleted

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `commerce.order` | Innehåller information om ordern. |
| `commerce.order.purchaseID` | Unik identifierare som tilldelats av säljaren för detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt. |
| `commerce.order.payments` | Listan över betalningar för den här ordern. |
| `commerce.order.payments.paymentTransactionID` | Unik identifierare för den här betalningstransaktionen. |
| `commerce.order.payments.paymentAmount` | Betalningens värde. |
| `commerce.order.payments.paymentType` | Betalningsmetoden för den här ordern. Räknade, anpassade värden tillåtna. |
| `commerce.order.payments.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `commerce.order.taxAmount` | Det skattebelopp som köparen betalar som en del av den slutliga betalningen. |
| `commerce.order.createdDate` | Tid och datum då en ny order skapas i handelssystemet. Exempel: `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Leveransinformation för en eller flera produkter. |
| `commerce.shipping.shippingMethod` | Leveranssätt som kunden väljer, t.ex. standardleverans, snabbare leverans, hämtning i butik osv. |
| `commerce.shipping.shippingAmount` | Det belopp som kunden måste betala för frakt. |
| `commerce.shipping.shipDate` | Det datum då en eller flera artiklar från en order skickas. |
| `commerce.shipping.address` | Den fysiska leveransadressen. |
| `commerce.shipping.address.street1` | Primär information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn. |
| `commerce.shipping.address.street2` | Ytterligare gatuinformation, andra raden. |
| `commerce.shipping.address.city` | Namnet på staden. |
| `commerce.shipping.address.state` | Statens namn. Det här är ett frihandsfält. |
| `commerce.shipping.address.postalCode` | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `commerce.shipping.address.country` | Namnet på det statligt administrerade territoriet. Förutom `xdm:countryCode` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `commerce.billing.address` | Betalningsadress. |
| `commerce.billing.address.street1` | Information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn |
| `commerce.billing.address.street2` | Ytterligare fält för gatuminivåinformation. |
| `commerce.billing.address.city` | Namnet på staden. |
| `commerce.billing.address.state` | Namnet på läget. Det här är ett frihandsfält. |
| `commerce.billing.address.postalCode` | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `commerce.billing.address.country` | Namnet på det statligt administrerade territoriet. Förutom `xdm:countryCode` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `productListItems` | En array med produkter i ordningen. |
| `productListItems.SKU` | Lagerhållningsenhet. Unik identifierare för produkten. |
| `productListItems.name` | Produktens visningsnamn eller läsbara namn. |
| `productListItems.priceTotal` | Det totala priset för produktartikeln. |
| `productListItems.quantity` | Antalet produktenheter i kundvagnen. |
| `productListItems.discountAmount` | Anger vilket rabattbelopp som används. |
| `productListItems.currencyCode` | Valutakoden [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) som används, till exempel `USD` eller `EUR`. |
| `productListItems.selectedOptions` | Fält som används för en konfigurerbar produkt. |
| `productListItems.selectedOptions.attribute` | Identifierar ett attribut för den konfigurerbara produkten, till exempel `size` eller `color`. |
| `productListItems.selectedOptions.value` | Identifierar värdet för attributet som `small` eller `black`. |
| `productListItems.categories` | Innehåller information om en produkts kategori. |
| `productListItems.categories.id` | Kategorins unika identifierare. |
| `productListItems.categories.name` | Namnet på kategorin. |
| `productListItems.categories.path` | Sökvägen till kategorin. |

## Kundprofilshändelser

Profilhändelser som hämtats från serversidan innehåller kontoinformation, som `accountCreated`, `accountUpdated` och `accountDeleted`. Dessa data används för att fylla i viktig kundinformation som behövs för att bättre definiera segment eller genomföra marknadsföringskampanjer, som att skicka rabatterbjudanden, bekräftelser av kontoändringar osv. Det finns liknande profilhändelser som hämtats från [storefront](events.md#customer-profile-events).

>[!NOTE]
>
>Varje kundprofilhändelse innehåller även fältet [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=sv-SE), som innehåller det systemgenererade Commerce-kund-ID:t som primär identifierare för profilen och ett e-post-ID som används som en sekundär identifierare. [Lär dig](custom-identities.md) hur du skapar anpassade identitetsattribut för att förbättra identifieringen av kundprofiler.

### accountCreated

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund försöker skapa ett konto. | `userAccount.backofficeCreateProfile` |

#### Data insamlade från kontoSkapade

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `person` | Innehåller information om kunden. |
| `person.name` | Innehåller information om kundens namn. |
| `person.name.firstName` | Innehåller kundens förnamn. |
| `person.name.lastName` | Innehåller kundens efternamn. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### accountUpdated

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund försöker redigera ett konto. | `userAccount.backofficeUpdateProfile` |

#### Data insamlade från kontoUppdaterade

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `person` | Innehåller information om kunden. |
| `person.name` | Innehåller information om kundens namn. |
| `person.name.firstName` | Innehåller kundens förnamn. |
| `person.name.lastName` | Innehåller kundens efternamn. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |

### accountDeleted

| Beskrivning | XDM-händelsenamn |
|---|---|
| Utlöses när en kund försöker ta bort ett konto. | `userAccount.backofficeDeleteProfile` |

#### Data som samlats in från accountDeleted

I följande tabell beskrivs de data som samlats in för den här händelsen.

| Fält | Beskrivning |
|---|---|
| `person` | Innehåller information om kunden. |
| `person.name` | Innehåller information om kundens namn. |
| `person.name.firstName` | Innehåller kundens förnamn. |
| `person.name.lastName` | Innehåller kundens efternamn. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `commerce.commerceScope` | Anger var en händelse inträffade (butiksvy, butik, webbplats och så vidare). |
| `commerce.commerceScope.environmentID` | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID avgränsat med bindestreck. |
| `commerce.commerceScope.storeCode` | Den unika butikskoden. Du kan ha många butiker per webbplats. |
| `commerce.commerceScope.storeViewCode` | Den unika koden för butiksvyn. Du kan ha många butiksvyer per butik. |
| `commerce.commerceScope.websiteCode` | Den unika webbplatskoden. Du kan ha många webbplatser i en miljö. |
