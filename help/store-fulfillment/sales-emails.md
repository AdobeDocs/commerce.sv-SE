---
title: E-postmallar för försäljning
description: Konfigurera e-postmallar för transaktioner för att kommunicera med kunder och butiksadministratörer under leveransprocessen för butiksbeställningar.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---


# E-postmallar för försäljning

Store Fulfillment erbjuder en utökad uppsättning e-postmallar för transaktioner som stöder arbetsflöden för order och leveranser. De erbjuder enhetlig, automatiserad kommunikation och meddelanden över alla kanaler - vilket gör att kunder och butiksadministratörer informeras om orderstatusändringar, instruktioner för hämtningsorder i butik med mera.

E-postmallar för att uppfylla kraven har konfigurerats med standardmeddelanden och standardinställningar. Affärsadministratörer i Adobe Commerce kan hantera och ändra konfigurationer och välja e-postmallar för att kommunicera med kunder i olika scenarier. Administratörer kan även konfigurera och anpassa mallar.

Konfigurera e-postmallar för försäljning från administratören: **[!UICONTROL Stores > Configuration > Sales > Sales Emails]**.

## E-post - allmänna inställningar

<table>
<thead>
<tr>
<th><strong>Fält</strong></th>
<th><strong>Beskrivning</strong></th>
<th><strong>Omfång</strong></th>
<th><strong>Obligatoriskt</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Asynkron sändning</strong></td>
<td>Avgör om e-postmeddelanden från försäljning skickas asynkront. Alternativ: <br/>**`Inaktivera`** - (standard) E-post om försäljning skickas när den aktiveras av en händelse. Använd standardinställningen för snabbaste kommunikations- och svarstid för Store Pickup. <br/>**`Aktivera`** - Om du aktiverar det här alternativet flyttas processer som hanterar utcheckning och beställer e-postmeddelanden i bakgrunden så att de kan skickas med förbestämda, regelbundna intervall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
</tbody></table>

## Beställ klart för hämtning i Store

<table>
<thead>
<tr>
<th><strong>Fält</strong></th>
<th><strong>Beskrivning</strong></th>
<th><strong>Omfång</strong></th>
<th><strong>Obligatoriskt</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Aktiverad</strong></td>
<td>Det här e-postmeddelandet skickas till kunden när butikskollegiet har slutfört plockningen av sin order. Ange Nej om du vill inaktivera e-postmeddelandet. Om e-postmallen är inaktiverad förhindrar den inte att en order plockas av butiksassociationen.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Order Ready for Pickup Email Sender</strong></td>
<td>Avsändarens identitet som används när e-postmeddelandet skickas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>E-postmall för beställning klar för hämtning</strong></td>
<td>E-postmeddelandemallen som används för att meddela registrerade kunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<td><strong>E-postmall för beställning klar för hämtning för gäst</strong></td>
<td>E-postmeddelandemallen som används för att meddela gästkunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Beställningen är klar för att hämta e-postmall för alternativ kontaktperson för hämtning</strong></td>
<td>E-postmeddelandemallen som används för att meddela ytterligare kontakter namngivna i ordningen. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka beställningen klar för hämtning av e-postkopia till</strong></td>
<td>En kommaavgränsad lista med e-postadresser som skickar en kopia av varje meddelande.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka beställningen klar för hämtning av e-postkopieringsmetod</strong></td>
<td>E-postkopieringsmetoden - kopia - som ska användas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
</tbody></table>


## Ordern har plockats upp i butiken

<table>
<thead>
<tr>
<th><strong>Fält</strong></th>
<th><strong>Beskrivning</strong></th>
<th><strong>Omfång</strong></th>
<th><strong>Obligatoriskt</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Aktiverad</strong></td>
<td>Det här e-postmeddelandet skickas till kunden när de vill bekräfta att de har hämtat sin beställning från butiken. Ange Nej om du vill inaktivera e-postmeddelandet. Om e-postmallen är inaktiverad förhindrar den inte att en order plockas upp av kunden.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>E-postavsändare har fått en beställning</strong></td>
<td>Avsändarens identitet som används när e-postmeddelandet skickas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>E-postmall för beställning har hämtats</strong></td>
<td>E-postmeddelandemallen som används för att meddela registrerade kunder. En standardmall tillhandahålls med integreringen</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<td><strong>E-postmall för gäst har hämtats för beställningen</strong></td>
<td>E-postmeddelandemallen som används för att meddela gästkunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka har hämtats via e-postkopia till</strong></td>
<td>En kommaavgränsad lista med e-postadresser som skickar en kopia av varje meddelande.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka har hämtats via e-postkopia</strong></td>
<td>E-postkopieringsmetoden - kopia - som ska användas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
</tbody></table>

## Order fördröjd

<table>
<thead>
<tr>
<th><strong>Fält</strong></th>
<th><strong>Beskrivning</strong></th>
<th><strong>Omfång</strong></th>
<th><strong>Obligatoriskt</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Aktiverad</strong></td>
<td>Det här e-postmeddelandet skickas till kunden för att meddela dem om en fördröjning i bearbetningen eller plockningen av deras order på handlarbutiken. Ange Nej om du vill inaktivera e-postmeddelandet. Om e-postmallen är inaktiverad förhindrar funktionen inte att en beställning försenas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Order Deled Email Sender
</strong></td>
<td>Avsändarens identitet som används när e-postmeddelandet skickas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>E-postmall för fördröjd beställning</strong></td>
<td>E-postmeddelandemallen som används för att meddela registrerade kunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<td><strong>E-postmall för fördröjd beställning för gäst</strong></td>
<td>E-postmeddelandemallen som används för att meddela gästkunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka orderfördröjd e-postkopia till</strong></td>
<td>En kommaavgränsad lista med e-postadresser som skickar en kopia av varje meddelande.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka försenad kopieringsmetod för order</strong></td>
<td>E-postkopieringsmetoden - kopia - som ska användas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
</tbody></table>



## Ordern har avbrutits

<table>
<thead>
<tr>
<th><strong>Fält</strong></th>
<th><strong>Beskrivning</strong></th>
<th><strong>Omfång</strong></th>
<th><strong>Obligatoriskt</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Aktiverad</strong></td>
<td>Det här e-postmeddelandet skickas till kunden för att meddela dem att deras beställning har annullerats på handlarbutiken. Ange till <code>No</code> om du vill inaktivera e-postmeddelandet. Om e-postmallen är inaktiverad förhindrar funktionen inte att en beställning annulleras.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Beställningen avbröts av e-postavsändaren
</strong></td>
<td>Avsändarens identitet som används när e-postmeddelandet skickas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>E-postmall för beställning avbruten</strong></td>
<td>E-postmeddelandemallen som används för att meddela registrerade kunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<td><strong>Ordern har avbrutits för gäst</strong></td>
<td>E-postmeddelandemallen som används för att meddela gästkunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka beställningen avbruten e-postkopia till</strong></td>
<td>En kommaavgränsad lista med e-postadresser som skickar en kopia av varje meddelande.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka beställningen avbruten kopieringsmetod</strong></td>
<td>E-postkopieringsmetoden - kopia - som ska användas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
</tbody></table>


## Order delvis annullerad

<table>
<thead>
<tr>
<th><strong>Fält</strong></th>
<th><strong>Beskrivning</strong></th>
<th><strong>Omfång</strong></th>
<th><strong>Obligatoriskt</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Aktiverad</strong></td>
<td>Det här e-postmeddelandet skickas till kunden för att meddela dem att en del av deras beställning har annullerats hos handlaren. Ange till <code>No</code> om du vill inaktivera e-postmeddelandet. Om e-postmallen är inaktiverad förhindrar den inte att en order delvis annulleras.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Order - delvis annullerad e-postavsändare
</strong></td>
<td>Avsändarens identitet som används när e-postmeddelandet skickas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>E-postmall för delvis annullerad beställning</strong></td>
<td>E-postmeddelandemallen som används för att meddela registrerade kunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<td><strong>Beställ delvis annullerad e-postmall för alternativ kontaktperson för hämtning</strong></td>
<td>E-postmeddelandemallen som används för att meddela ytterligare kontakter namngivna i ordningen. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Order delvis annullerad för gäst</strong></td>
<td>E-postmeddelandemallen som används för att meddela gästkunder. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka beställningen delvis annullerad e-postkopia till</strong></td>
<td>En kommaavgränsad lista med e-postadresser som skickar en kopia av varje meddelande.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Skicka order delvis annullerad kopieringsmetod</strong></td>
<td>E-postkopieringsmetoden - kopia - som ska användas.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
</tbody></table>

## Leverera till butik

<table>
<thead>
<tr>
<th><strong>Fält</strong></th>
<th><strong>Beskrivning</strong></th>
<th><strong>Omfång</strong></th>
<th><strong>Obligatoriskt</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Ordern har leverans att lagra e-postavsändare för produkter</strong></td>
<td>E-post som skickas till angiven handlarpersonal som en sammanställd rapport över alla öppna order som inte kan plockas i en handlarbutik förrän deras lager är tillgängligt. </br></br>-handlare kan använda den här rapporten för att initiera och hantera lageröverföringar från butik till butik eller lagerpåfyllnad. </br></br>Det här meddelandet gäller bara när [!DNL Ship-to-Store]-funktionerna är aktiverade.
</br></br>Den här etiketten påverkar inte det valda transportföretaget eller deras tillgängliga etiketter för leveransmetoder.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>Leverera till butik för e-postmottagare</strong></td>
<td>En kommaavgränsad lista med e-postadresser som skickar en kopia av varje meddelande.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>E-postmall</strong></td>
<td>E-postmeddelandemallen som används för att meddela mottagare. Integreringen innehåller en standardmall.</td>
<td>Butiksvy</td>
<td>Nej</td>
</tr>
</tbody></table>

>[!NOTE]
>
>Om du tillåter restorder måste du ange en administratörs-e-postadress för att få meddelanden om dessa order. Lägg till adressen i följande konfigurationsinställningar: **[!UICONTROL Send Order Delayed Email Copy To]** i mallen [Orderfördröjning](#order-delayed) och [!UICONTROL Ship To Store Email Recipients] i mallen [Leverera till butik](#ship-to-store).



