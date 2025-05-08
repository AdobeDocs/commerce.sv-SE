---
title: Checka ut i  [!DNL Payment Services]
description: Anpassa [!DNL Payment Services] utcheckningen efter kundens behov.
feature: Payments, Checkout, Paas, Saas
exl-id: 47df165f-2145-4e0e-b272-54b8e768cf19
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Utcheckning i [!DNL Payment Services]

Du kan konfigurera utcheckning för Adobe Commerce [!DNL Payment Services] så att den passar dina kunder bäst. Funktioner som [automatisk avbeställning](#order-auto-voided-if-error) och [kreditkortsbetalning](#credit-card-vaulting) säkerställer att kunderna får en smidig användarupplevelse.

## Beställningen annulleras automatiskt om fel uppstår

Om ett fel inträffar under utcheckningen annulleras/annulleras ordningen automatiskt av [!DNL Payment Services].

Ett felmeddelande visas på utcheckningssidan för kunden. Meddelandet kan variera.

![Fel vid utcheckning](assets/user-checkout-error.png "Fel vid utcheckning"){width="600" zoomable="yes"}

En kommentar om den annullerade ordningen visas också i administratören för en specifik [order](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/orders.html?lang=sv-SE).

![Avbruten orderkommentar i Admin för order](assets/admin-checkout-error.png "Avbruten orderkommentar i Admin för order"){width="600" zoomable="yes"}

Om en kund får auktorisering för en order, men ordern inte har skapats och konverterats till `Capture`, annulleras ordern automatiskt. Denna process garanterar att ingen kredit reserveras på kundens kreditkort och undviker den betalaravgift som uppstår när auktorisationen annulleras vid slutet av den vanliga 29-dagarsperioden.

>[!NOTE]
>
>Automatisk annullering av order sker endast när kunden använder en betalningsmetod som är inställd på läget `Authorize`, inte `Authorize and Capture`.

## Utcheckning från produktsida

När en kund checkar ut direkt från produktsidan med PayPal- eller [!DNL Pay Later]-knapparna, köps bara det objekt som finns representerat på den aktuella produktsidan. Artiklar som redan finns i kundens kundvagn läggs inte till i utcheckningsflödet och köps inte.

Med den här funktionen kan kunden snabbt köpa det objekt de för närvarande visar, samtidigt som artiklar som tidigare lagts till i kundvagnen behålls.
Om kunden avbryter beställningen läggs artikeln på den aktuella produktsidan till i kundvagnen.

När en kund går in i utcheckningsflödet från produktsidan förenklas utcheckningssidan - vyn visar endast orderrelaterade data och alternativ.

## Kreditkortssäkringar

Köpare kan vault - eller&quot;save&quot; - deras kreditkortsinformation för framtida inköp på webbplatsnivå (vilken butik som helst på samma handlares konto).

Mer information finns i [Säkring av kreditkort](vaulting.md)
