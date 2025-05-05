---
title: Testa och distribuera arkivuppfyllelse
description: Testa planen för att verifiera funktionen för att uppfylla kraven i Store. Testerna täcker inventeringssynkroniserings-API:t, arbetsflödet från början till slut för annullerade beställningar, användarhantering för appen Store Fulfillment samt upplevelsen av kundincheckning.
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# Testa och distribuera Store-uppfyllelse för Adobe Commerce

När du är klar med introduktionsprocessen i utvecklingsmiljön kan du testa och distribuera Store Fulfillment-lösningen i produktionsmiljön.

**Förutsättningar**

Innan du testar eller synkroniserar information, arkiv eller order måste du kontrollera att du har utfört följande uppgifter:

- Slutförde den [allmänna konfigurationen](enable-general.md) för Butiksuppfyllelsetjänsterna.

- [Lägg till och validera kontoinloggningsuppgifterna och anslutningsinformationen för din sandlåda och dina produktionsmiljöer](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- Bekräfta att [Adobe Commerce-integreringen](connect-set-up-service.md#configure-store-fulfillment-account-credentials) för Store Fulfillment-lösningen är tillgänglig och auktoriserad.

## Förbered för testning

Anslutningskonfigurationen måste slutföras innan du kan skapa testorder eller utföra integrationstestning. Innan du testar måste du även verifiera att dina lagringsdata är synkroniserade.

1. Synkronisera lagringskällor.

   - Gå till **[!UICONTROL Stores > Sources]**.

   - Välj **[!UICONTROL Synchronize Store Fulfillment Sources]**.

1. Verifiera från butiksrutnätet att butikerna har markerats som `Synced` innan du skapar testorder.

## Exempel på testplan

Återförsäljare validerar de grundläggande funktionerna i Store Fulfillment-lösningen under konfigurations- och testfaserna av en distribution. Denna exempeltestplan utgör en startpunkt för testningen. Lägg till ytterligare scenarier baserat på dina behov.

>[!NOTE]
>
>När du har slutfört den första introduktionen av Store Fulfillment-lösningen eller uppdaterat en befintlig installation ska du alltid testa programmet i en icke-produktionsmiljö innan du distribuerar till produktionen.

Denna exempeltestplan omfattar följande funktionsområden:

| Funktionsområde | Funktion | Roll |
|-------------------------------------|------------------------------------------|----------------------------------|
| Lager- och ordersynkronisering | Synkronisering av lager-API | Adobe Commerce Admin |
| Från början till slut | Arbetsflöden för annullering av order | Kund, Admin, Store Associate |
| Administratör | Lagra programbehörigheter för uppfyllelse | Administratör |
| Adobe Commerce Frontend | Produkttyper | Kund, administratör |
| Checka ut</br>Checka in formulär | Incheckningsfunktion | Kund, administratör |
| Store Assist App | Beställning</br>Välj</br>scen</br>och Leverans | Butikskoppling |

### Synkronisering av lager-API

Det här avsnittet av testplanen omfattar lager- och ordersynkronisering för att verifiera att uppdateringar av hämtningskällor och lager synkroniseras korrekt mellan Adobe Commerce och Store Fulfillment-lösningen.

**Funktionsområde**: Lager- och ordersynkronisering</br>
**Roll:** Admin </br>
**Testtyp:** Alla positiva

<table>
<thead>
<tr>
<th>Funktion</th>
<th>Testscenario</th>
<th>Förväntade resultat</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Lägg till hämtningslagerkälla</strong></td>
<td>Spara en ny hämtningskälla.</td>
<td>Synkroniseringen i realtid skickar källinformationen till Walmart GIF-tjänsten inom fem minuter.</td>
</tr>
<tr>
<td><strong>Uppdatera befintlig hämtningslagerkälla</strong></td>
<td>Spara uppdateringar av en befintlig hämtningskälla.</td>
<td>Synkroniseringsåtgärden i realtid skickar informationen till Walmart GIF inom fem minuter</td>
</tr>
<tr>
<td><strong>Status för hämtning av Stock-källa </br><code>Is Synced</code></strong></td>
<td>Spara uppdateringar av en befintlig hämtningskälla.</td>
<td>Efter en slutförd åtgärd uppdateras kolumnen <code>Is Synced</code> på sidan Hantera Source från <code>No</code> till <code>Yes</code>.</td>
</tr>
<tr>
<td><strong>Ändrad process för lagerreservation</strong></td>
<td>Skapa och skicka en ny order för en produkt.</td>
<td>Produktens säljbara kvantitet minskar i motsvarande grad.</td>
</tr>
<tr>
<td><strong>New Order Push, API Sync - Customer Order</strong></td>
<td>Kunden skickar en inköpsbeställning.</td>
<td><ul><li>I vyn Admin Order (Administratörsordning) ser en <strong>Adobe Commerce-administratör</strong> att statusen Order Sync har uppdaterats till <code>Sent</code></li><li>Orderinformationsloggen innehåller meddelandet <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Ny orderpush, API-synkronisering - Admin skickar order</strong></td>
<td>En Adobe Commerce <strong>Admin</strong> skickar en hämtningsorder.</td>
<td><ul><li>I vyn Admin Order (Administratörsordning) uppdateras statusen Order Sync till <code>Sent</code>.</li><li>Orderinformationsloggen innehåller meddelandet <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Ny orderpush, undantagskö<strong></td>
<td>Identifiera flera virtuella och hämtningsbara produkter i Adobe Commerce Admin som kan fullföljas via Adobe Commerce utan att det krävs interaktion med Fulfillment Service (FAAS).</td>
<td>Dessa produkter tas bort eller flaggas på rätt sätt i exporten för att förhindra konflikter längre fram i kedjan med FaaS.</td>
</tr>
</tbody>
</table>

### Arbetsflöden för annullering av order

Det här avsnittet av testplanen innehåller scenarier för att testa arbetsflödet från början till slut för order som annulleras via Adobe Commerce.

**Funktionsområde:** Adobe Commerce Admin</br>
**Roll:** End-to-End (Admin, Store Associate, Customer)</br>
**Testresultattyp:** Positiv för alla scenarier

<table style="table-layout:fixed">
<tr>
<th>Funktion</th>
<th>Scenario</th>
<th>Förväntade resultat</th>
</tr>
<tr>
<td><strong>Fullständig orderannullering</strong></td>
<td><ol>
<li>Montera order.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Verifiera att fakturan skapas (om auktorisering och hämtning sker) och att fakturameddelandet skapas.</li>
<li>Skapa kreditnota med alla beställda produkter från fakturavyn.</li>
</ol>
</td>
<td>
<ul>
<li>Orderhistoriken har uppdaterats med <code>We refunded $X online. Transaction ID: transactionID</code> och <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>Orderstatus är <code>Closed</code>. (Vi har ställt in BETALNINGSGRANSKNING nu.)</li>
<li>Kreditnota skapad i Adobe Commerce. (Vänta tills cron fungerar.)</li>
<li>Om alla objekt har plockats visar e-postmeddelandet <code>DISPLAY COMMENT HISTORY</code>, som är klart för hämtning, <code>Order is ready for pickup</code> (<code>CUSTOMER NOTIFIED</code>-flaggan är <code>true</code>).</li>
<li>Om alla artiklar inte plockas visas annullerings-e-post och VISA KOMMENTARHISTORIK <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> flaggan är <code>true</code>.)</li>
</ul>
</td>
</tr>
<tr><td><strong>Annullering av partiell order<strong></td>
<td>
<ol>
<li>Beställ med minst två produkter.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Kontrollera att fakturan har skapats (om auktorisering och hämtning har gjorts) och att fakturameddelandet har tagits emot.</li>
<li>Vänta i två timmar på transaktionskvittning.</li>
<li>Skapa kreditnota med endast en del av de beställda produkterna från fakturavyn.</li>
</td>
<td>
<ul>
<li>Uppdatering av orderhistorik: <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>Uppdatering av orderhistorik: <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>E-postadress för orderåterbetalning: <code>$x amount was refunded</code></li>
<li>Orderstatus är <code>Processing</code>.</li>
<li>Kreditnota skapad i Adobe Commerce (Vänta tills cron fungerar).</li>
<li>Om några artiklar inte plockades bekräftar du att e-postmeddelandet [!UICONTROL Ready for Pickup] med nollplockning eller återbetalningsavsnitt visas. <code>DISPLAY COMMENT HISTORY</code> visar <code>Order is ready for pickup, but some items not available.</code>.</li>
<li><code>CUSTOMER NOTIFIED</code> flaggan är <code>true</code>.</li>
</ul>
</td>
</tr>
<td><strong>Klar för hämtning</br></br>Fullständig annullering</br> (alla produkter anges som plockade med 0 kvantitet)</strong></td>
<td>
<ol>
<li>Beställ.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Kontrollera att fakturan har skapats (om auktorisering och hämtning har gjorts) och att fakturameddelandet har tagits emot.</li>
<li>Gå till Postman och kör begäran Ready for Pickup med alla produkter inställda på <code>picked</code> med <code>0 qty</code>.</li>
</ol>
</td>
<td>
<ul>
<li>Orderhistoriken har uppdaterats: <code>We refunded $X offline</code></li>
<li>Orderstatusen är <code>CLOSED</code>.
<li>Kreditnotan skapas. (Vänta tills cron fungerar.)</li>
<li>E-postmeddelande om återbetalning: <code>$x amount was refunded</code></li>
<li>E-postmeddelande om annullering av beställning har skickats.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Klar för hämtning - partiell annullering</strong></br></br><strong>(Vissa produkter plockas och andra plockas med <code>0 qty</code>)</strong>
</td>
<td>
<ol>
<li>Beställ.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Kontrollera att fakturan har skapats (om auktorisering och hämtning har gjorts) och att fakturameddelandet har tagits emot.</li>
<li>Gå till Postman och kör begäran om Ready for Pickup med en del av produkterna plockade med 0 kvantitet och resten plockade.</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> med [!UICONTROL Ready for Pickup Items] och [!UICONTROL Canceled Items] tabeller. </li>
<li>Orderstatusen är KLAR FÖR PICKUP. </li>
<li>Orderhistoriken har uppdaterats: <code>We refunded $X offline.</code>
<li>Orderhistoriken har uppdaterats: <code>Order notified as partly canceled at: Date and hour</code>
<li>Återbetalningsmeddelande har tagits emot: <code>$x amount was refunded</code>
<li>Kreditnotan skapas. (Vänta tills cron fungerar.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Klar för hämtning - delvis annullering</br></br>Vissa produkter plockas och andra plockas med <code>0 qty</code>)</strong>
</td>
<td><ol>
<li>Beställ.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Kontrollera att fakturan har skapats (om auktorisering och hämtning har gjorts) och att fakturameddelandet har tagits emot.</li>
<li>Gå till Postman och kör begäran om Ready for Pickup med en del av produkterna plockade med 0 kvantitet och resten plockade.</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> med [!UICONTROL Ready for Pickup Items] och [!UICONTROL Canceled Items] tabeller. </li>
<li>Orderstatusen är KLAR FÖR PICKUP. </li>
<li>Orderhistoriken har uppdaterats: <code>We refunded $X offline.</code>
<li>Orderhistoriken har uppdaterats: <code>Order notified as partly canceled at: Date and hour</code>
<li>Återbetalningsmeddelande har tagits emot: <code>$x amount was refunded</code>
<li>Kreditnotan skapas. (Vänta tills cron fungerar.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Skickas (under disponering) </br></br>Fullständig annullering (alla produkter anges som avvisade)</strong>
</td>
<td>
<ol>
<li>Beställ.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Kontrollera att fakturan har skapats (om auktorisering och hämtning har gjorts) och att fakturameddelandet har tagits emot.</li>
<li>Gå till Postman och kör begäran om Ready for Pickup med alla produkter som valts.</li>
<li>Öppna din postlåda och hitta e-postmeddelandet Klar för hämtning. Klicka sedan på **[!UICONTROL Confirm Arrival]**.</li>
<li>Kolla in.</li>
<li>Gå till Postman och kör den skickade begäran med alla produkter inställda som avvisade.</li>
</ol>
<td><ul>
<li>Orderhistoriken har uppdaterats: <code>We refunded $X offline.</code></li>
<li>E-postmeddelande om återbetalning: <code>$x amount was refunded</code></li>
<li>Status inställd på <code>CLOSED</code>.</li>
<li>Kreditnotan har skapats. (Vänta tills cron fungerar.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Skickat (under disponering)</br></br>Partiell annullering</br>(Vissa produkter är disponerade; andra ignoreras.)</strong>
</td>
<td>
<ol>
<li>Beställ.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Kontrollera att fakturan har skapats (om auktorisering och hämtning har gjorts) och att fakturameddelandet har tagits emot.</li>
<li>Gå till Postman och kör begäran om Ready for Pickup med alla produkter som valts.</li>
<li>Öppna din postlåda. Hitta e-postmeddelandet Klar för hämtning och välj <code>Confirm Arrival</code>.</li>
<li>Kolla in.</li>
<li>Gå till Postman och kör den skickade förfrågan med vissa produkter som är inställda på att dras ifrån och vissa är inställda på att avvisas</li>
</ol>
</td>
<td>
<li>Orderhistoriken har uppdaterats: <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>Återbetalningsmeddelande har tagits emot: <code>$x amount was refunded</code>
<li>Orderstatus inställd på <code>Ready for pickup Dispensed</code>
<li>Kreditnotan har skapats. (Vänta tills cron fungerar.)</li>
</td>
</tr>
<tr>
<td> <strong>Nytt RMA efter retur (fullständigt)</strong>
</td>
<td>
<ol>
<li>Beställ.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Om auktoriserings- och hämtningsalternativet är konfigurerat kontrollerar du att fakturan har skapats och att kunden har fått fakturameddelandet.</li>
<li>Välj alla produkter med Postman.</li>
<li>Kolla in.</li>
<li>Gör en lögn.</li>
<li>Gå till beställningen och välj <strong>[!UICONTROL Create returns]=
<li>Skapa RMA.</li>
</ol>
</td>
<td>
<ul>
<li>RMA skapades och visas under fliken <strong>[!UICONTROL Returns]</b> i ordervyn.</li>
<li>Kunden har fått RMA-bekräftelsemeddelande via e-post.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Nytt RMA efter retur — Delvis</strong>
</td>
<td>
<ol>
<li>Beställ.</li>
<li>Vänta tills ordern har synkroniserats.</li>
<li>Kontrollera att fakturan har skapats (om auktorisering och hämtning har gjorts) och att fakturameddelandet har tagits emot.</li>
<li>Välj alla produkter med Postman.</li>
<li>Kolla in.</li>
<li>Gör en lögn.</li>
<li>Gå till ordningen och välj  <strong>[!UICONTROL Create returns]</strong></li>
<li>Skapa RMA med en del av de beställda produkterna.</li>
</ol>
<td>
<ul>
<li>RMA skapades och visades under fliken <strong>[!UICONTROL Returns]</strong> i ordervyn.</li>
<li>Kunden har fått ett bekräftelsemeddelande från RMA.</li>
<li>När du har skapat RMA måste du skaffa RMA-auktoriseringen: Gå till <strong>[!UICONTROL Sales > Returns]</strong> från administratören. Välj den RMA som du skapade och auktorisera den.</li>
<li>Verifiera att kunden har fått bekräftelsemeddelandet via RMA-auktorisering.</li>
<li>Kontrollera att återbetalningen har lagts till i transaktionerna och orderhistoriken.</li>
</ul>
</td>
</tr>
</table>


### Lagra programbehörigheter för uppfyllelse

Det här avsnittet av testplanen omfattar kontohantering för användare av Store Fulfillment App.

- Bekräfta att en Store Associate kan autentisera med ett nytt användarkonto som har skapats i Adobe Commerce Admin.
- Bekräfta att uppdateringar av befintliga konton har tillämpats.

**Funktionsområde:** Adobe Commerce Admin</br>
**Roll:** Admin, Store Associate </br>
**Testtyp:** Alla positiva

<table style="table-layout:auto">
<tr>
<th>Funktion</th>
<th>Scenario</th>
<th>Förväntade resultat</th>
</tr>
<tr>
<td><strong>Hantering av användarkonto - Skapa konto</strong></br></br>
</td>
<td>
<ol>
<li><strong>Admin</strong> - Logga in i Adobe Commerce Admin</li>
<li>Gå till <strong>[!UICONTROL System] &gt; Store Fulfillment App Permissions &gt; All Store Fulfillment App Users</strong></li>
<li><strong>Lägg till ny användare.</strong></li>
</ol>
<td>
<ul>
<li>Kontot har skapats.</li>
<li>Det nya användarkontot visas på kontrollpanelen [!UICONTROL Store Fulfillment Users].</li>
<li><strong>Store Associate</strong> loggar in på Store Assist-appen med ett nytt användarkonto.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Hantering av användarkonto - Uppdatera befintligt användarkonto</strong>
</td>
<td>
<ol>
<li>Logga in på Adobe Commerce Admin med användarkontot Admin.</li>
<li>Gå till <strong>[!UICONTROL System] &gt; Store Fulfillment App Permissions &gt; All Store Fulfillment App Users</strong>.</li>
<li>Öppna ett befintligt aktivt användarkonto i listan Användarkonto genom att välja <strong>[!UICONTROL Edit]</strong>.
<li>Inaktivera kontot genom att ändra <strong>[!UICONTROL Is Active]</strong> till <strong>Nej</strong>.</li>
</ol>
</td>
<td>
<ul>
<li>Statusen för det uppdaterade kontot ändrades till <strong>[!UICONTROL Inactive]</strong> på kontrollpanelen <strong>[!UICONTROL Store Fulfillment App Users]</strong>.</li>
<li>Store Associate kan inte logga in på Store Assist-appen med inaktiva kontoautentiseringsuppgifter.</li>
</ul>
</td>
</tr>
</table>

## Adobe Commerce-produkttyper

Testscenarierna för Adobe Commerce-produkttyper verifierar att kunderna ser rätt produkt-, lager- och leveransmetodinformation för olika produkttyper:

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- [!UICONTROL Bundle products] i Adobe Commerce Store.

**Funktionsområde:** Adobe Commerce FrontEnd</br>
**Roll:** Store Assist App User (Store Associate) </br>
**Testtyp:** Alla positiva

<table style="table-layout:auto">
<tr>
<th>Funktion</th>
<th>Scenario</th>
<th>Kommentar</th>
</tr>
<tr>
<td><strong>Konfigurerbara produkter</strong>
</td>
<td>
<ul>
<li>Kontrollera att användaren bara kan se de konfigurerbara alternativen, vilken källa som är aktiverad, att Stock är tilldelat och att det finns några artiklar i Stock - kontrollera underordnade produkter.</li>
<li>Kontrollera att när du väljer en annan butik visas alternativ som inte är tillgängliga som överstrukna.</li>
<li>Kontrollera att konfigurerbara alternativ inte är markerade om användaren väljer en annan butik.</li>
<li>Kontrollera att om en konfigurerbar produkt redan finns i kundvagnen och en användare väljer en annan butik visas produkten som lagrad.</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>Grupperade produkter</strong>
</td>
<td>
<ul>
<li>Verifiera att leveransmetoderna och knappen [!UICONTROL Add to cart] är inaktiverade för kunden när alla underordnade produkter har
<code>qty</code> inställd på <code>0</code> .</li>
<li>Verifiera att leveransmetoderna är aktiverade för kunden när minst en av de underordnade produkterna har <code>qty</code> inställt på <code>0.</code></li>
<li>Kontrollera att metoden [!UICONTROL Store Pickup Delivery] bara är synlig och aktiv för de produkter som har [!UICONTROL Available for Store Pickup] aktiverat. (Kontrollera underordnad produkt.)</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>Virtuella produkter</strong>
</td>
<td>
Kontrollera att leveransmetoden [!UICONTROL In-store Pickup] inte finns för virtuella produkter.
<td></td>
</td>
</tr>
<tr>
<td><strong>Paketprodukter</strong>
</td>
<td>
<ul>
<li>Kontrollera att leveransalternativet Store Pickup inte är tillgängligt för kunden om minst en underordnad produkt har [!UICONTROL Available for Store Pickup] inaktiverat.</li>
<li>Kontrollera att alternativet Home Delivery inte är tillgängligt för kunden om minst en underordnad produkt har [!UICONTROL Available for Home Delivery] inaktiverat.</li>
<li>Kontrollera om minst en av de underordnade produkterna i ett paket inte finns i lager visas paketet (överordnad produkt) också
som [!UICONTROL Out of stock].</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## Incheckningsfunktion

Det här avsnittet av testplanen omfattar beställningar av Check-In Experience for Store-hämtning för följande funktioner:

- Alternativ upphämtningskontakt - Verifiera arbetsflödet för att lägga till en [!UICONTROL Alternate Pickup Contact] och välja en [!UICONTROL Preferred Contact] på butiksbeställningar.

- Incheckningsformulär - Verifiera arbetsflödet för att skicka in en incheckningsbegäran för Store-hämtningsorder.

**Funktionsområden:** Kassautcheckning, incheckningsformulär för butiksupphämtningsorder</br>
**Roll:** Admin, Customer, Store Associate </br>
**Testtyp:** Alla positiva

### Alternativ kontaktperson för hämtning


**Funktionsområde:** Kassa</br>
**Roll:** Kund</br>
**Testtyp:** Alla positiva

<table style="table-layout:auto">
<tr>
<th>Funktion</th>
<th>Scenario</th>
<th>Förväntade resultat</th>
</tr>
<tr>
<td><strong>Alternativ kontaktperson för hämtning </br>
Checka in<strong>
</td>
<td>
En kund skickar en beställning med alternativet Pickup i butik.</td>
<td>Under utcheckningsprocessen ser kunden alternativet [!UICONTROL Alternate Pickup Contact] i leveranssteget.
</td>
</tr>
<tr>
<td><strong>Kontakt som har valts för alternativ hämtning, checka in</strong>
<td>
En kund skickar en beställning med alternativet Pickup i butik. Under utcheckningen lägger kunden till en [!UICONTROL Alternate Pickup Contact].</td>
<td>Under utcheckningsprocessen ser kunden alternativet [!UICONTROL Preferred Contact] i leveranssteget.</td>
</td>
</tr>
<tr>
<td><strong>Kontaktinformation för alternativ hämtning, checka in</strong>
</td>
<td>
En kund skickar en beställning med alternativet Pickup i butik. Under utcheckningen väljer kunden [!UICONTROL Alternate Pickup Contact] i leveranssteget.
</td>
<td>Kunden ser indataalternativ för att ange kontaktinformation: [!UICONTROL First name], [!UICONTROL Last name], [!UICONTROL Phone] och [!UICONTROL Email].</td>
</tr>
<tr>
<td><strong>Alternativ hämtning, checka in e-post</strong>
</td>
<td>En kund skickar en beställning med alternativet Pickup i butik. Under utcheckningen väljer kunden [!UICONTROL Alternate Pickup Contact] i leveranssteget, lägger till kontaktinformationen och skickar ordern.</td>
<td>Både kunden och den alternativa kontakten får ett e-postmeddelande om incheckning av ordern.</td>
</tr>
<td><strong>Alternativ hämtning, orderdetaljer</strong></td>
<td>En kund skickar en beställning med alternativet Pickup i butik. Under utcheckningen väljer kunden [!UICONTROL Alternate Pickup Contact] i leveranssteget, lägger till kontaktinformationen och skickar ordern.</td>
<td>Administratören ser ytterligare kontaktinformation i den sparade ordern.</td>
</tr>
<tr>
<td><strong>Alternativ kontaktperson för hämtning, vyn för associerad beställning för butik</strong>
</td>
<td>En kund skickar en beställning med alternativet Pickup i butik. Under utcheckningen väljer kunden [!UICONTROL Alternate Pickup Contact] i leveranssteget, lägger till kontaktinformationen och skickar ordern.</td>
<td>Store Associate kan se ytterligare kontaktinformation på beställningen i faaS/ChaaS.</td>
</td>
</tr>
</tbody>
</table>

### Incheckningsformulär


**Funktionsområde:** Incheckningsformulär </br>
**Roll:** Kund</br>
**Testtyp:** Alla positiva

<table style="table-layout:auto">
<tr>
<th>Funktion</th>
<th>Scenario</th>
<th>Förväntade resultat</th>
</tr>
<tr>
<td><strong>Check in action—Submit request</strong>
</td>
<td>På incheckningsformuläret fyller kunden i alla obligatoriska fält och skickar begäran.</td>
<td>Kunden får ett lyckat svar.</td>
</tr>
<tr>
<td><strong>Check in Action - View request details</strong></td>
<td>En kund har skickat in en incheckningsbegäran.</td>
<td>Orderstatusen uppdateras i faaS-systemet och Store Associate kan se information om begäran om incheckning i faaS.
</td>
</tr>
<tr>
<td><strong>Check in Action - Submit request only once</strong></td>
<td>När kunden har skickat in en incheckningsbegäran för en order väljer han länken för att checka in en andra gång.</td>
<td>I formuläret Checka in ser kunden inget alternativ för att redigera eller skicka om formuläret.</td>
</tr>
<tr>
<td><strong>Check in action—Confirm Arrival</strong></td>
<td>En hämtningsorder i butiken har markerats som klar för hämtning i faaS. Kunden får ett e-postmeddelande om redo för hämtning och väljer [!UICONTROL Confirm Arrival].</td>
<td>Kunden ser incheckningsformuläret för ordern.</td>
</tr>
</tbody>
</table>

## App för Store Assist

Det här avsnittet av testplanen innehåller scenarier för testning av arbetsflöden för beställning, plockning och leverans i Store Assist App.

**Funktionsområde:** Store Assist App</br>
**Roll:** Store Associate</br>
**Testtyp:** Alla positiva

<table style="table-layout:auto">
<tr>
<th>Funktion</th>
<th>Scenario</th>
<th>Förväntade resultat</th>
</tr>
<tr>
<td>
<strong>Plockning av enstaka order - lycklig sökväg, kryssiga plockning</strong></td>
<td>Välj enstaka artiklar och artiklar med flera kvantiteter. Ingen nil-plockning och urbside-hämtning (med mellanlagring).
</td>
<td>
</td>
</tr>
<tr>
<td><strong>Plocka upp flera order - lyckad sökväg, hämtning av krullande bilder</strong></td>
<td>Enstaka artiklar och artiklar med flera kvantiteter. Inga nil-plockningar och urbside-hämtning (med mellanlagring)</td>
<td></td>
</tr>
<tr>
<td><strong>Plocka enkelt order - hitta en bra plats i butiken</strong></td>
<td>Enstaka artiklar och artiklar med flera kvantiteter. Inga nil-plockningar och in-store-hämtning (med mellanlagring)</td>
<td>
</td>
</tr>
<tr>
<td><strong>Plocka flera order - lyckliga sökvägar, hämtning i butik</strong></td>
<td>Välj enstaka artiklar och artiklar med flera kvantiteter. Ingen nil-plockning och urbside-hämtning (med mellanlagring).</td>
<td></td>
</tr>
<tr>
<td><strong>Plockning av enstaka order - ingen lycklig sökväg, plockning i butik</strong></td>
<td>Plocka enstaka och flera artiklar med partiell plockning och plockning i butik (med mellanlagring)</td>
</td>
<td></td>
</tr>
<td><strong>Plocka flera order - inte lyckad hämtning av utjämnad sökväg</strong></td>
<td>Plocka enstaka och flera artiklar med partiell plockning och plockning i butik (med mellanlagring)</td>
<td></td>
</tr>
<td><strong>Plockning av enstaka order - ingen lycklig sökväg, begränsad plockning</strong></td>
<td>Plocka enstaka och flera artiklar med partiell plockning och plockning (med mellanlagring)</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>Utplacerad order - annullerad före plockning</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Monterad beställning - annullerad före leverans</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Monterad order - sök i ordningsmodulen</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Monterad order - sök och checka in manuellt för leverans</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Monterad order - alla artiklar är plockade eller inte tillgängliga och markerade av väljaren</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Beställ med paketartiklar - plockning och leverans</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Beställ - skicka iväg med avvisning</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Monterad order - Lämna över alla objekt utan att ta hänsyn till dem</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## Distribuera

När du har verifierat att lösningen har konfigurerats och testats enligt dina specifikationer är du redo att driftsätta från mellanlagring till produktion.

Driftsättning och testning varierar beroende på din infrastruktur och dina funktioner.

>[!TIP]
>
>Distributionsriktlinjer, checklistor och metodtips för Adobe Commerce i molninfrastrukturprojekt finns i [Distribuera din butik](https://experienceleague.adobe.com/sv/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production) i dokumentationen för Adobe Commerce Developer.
