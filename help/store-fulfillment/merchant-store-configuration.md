---
title: Konfiguration av handelslager
description: Konfigurera förbättrade Inventory management-källor som butiker.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Konfiguration av Merchant Stores (Source)

Den här lösningen förbättrar de inbyggda Inventory management-funktionerna genom att utöka arkivkällorna med funktionsorienterade funktioner för handlare.

- Lägg till geografiska koordinater för butiksplatsen
- Ange källan som [!DNL Store Pickup Location] och ange tillgängliga leveransfunktioner (Ship to Store, Ship from Store)
- Ange tillgängliga upphämtningsalternativ (butiks- eller bside-filer), anpassade upphämtningsinstruktioner och annan information för att kommunicera upphämtningsinformation och instruktioner till kunderna

Termerna _source_ och _butiksplats_ används omväxlande. Alla poster är lagerkällor, men källorna kan också vara butiksplatser för handlare, beroende på konfigurationsinställningarna.

Hantera konfigurationen för handelslager från administratören: **[!UICONTROL Stores > Inventory > Sources >  Edit Source]**.

>[!NOTE]
>
>Under installationen kan det vara nödvändigt att tömma cachen efter att du har skapat källor eller uppdaterat befintliga källor.

## **Allmänt**

<table>
<tbody>
<tr>
<th>Fält</th>
<th>Beskrivning</th>
<th>Omfång</th>
<th>Obligatoriskt</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Latitudkoordinat för butikens plats. Den här obligatoriska informationen används vid platssökning och kartplacering i butiksupplevelsen. Värdet måste matcha butikens exakta adress för att validering ska kunna utföras.</td>
<td>Global</td>
<td>Ja</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Longitudinell koordinat för butiksplatsen. Den här obligatoriska informationen används vid platssökning och kartplacering i butiksupplevelsen. Värdet måste matcha butikens exakta adress för att validering ska kunna utföras.</td>
<td>Global</td>
<td>Ja</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Ange källan som en tillgänglig lagringsplats. Den här inställningen avgör om källan är synkroniserad och visas för besökare.</td>
<td>Global</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>Konfigurera funktioner för leverans till butik på källnivå. Mer information finns i alternativet [Allmän konfiguration](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Latitudkoordinat för butikens plats. Den här obligatoriska informationen används vid platssökning och kartplacering i butiksupplevelsen. Värdet måste matcha butikens exakta adress för att validering ska kunna utföras.</td>
<td>Global</td>
<td>Ja</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Longitudinell koordinat för butiksplatsen. Den här obligatoriska informationen används vid platssökning och kartplacering i butiksupplevelsen. Värdet måste matcha butikens exakta adress för att validering ska kunna utföras.</td>
<td>Global</td>
<td>Ja</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Ange källan som en tillgänglig lagringsplats. Den här inställningen avgör om källan är synkroniserad och visas för besökare.</td>
<td>Global</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>Konfigurera funktioner för leverans till butik på källnivå. Mer information finns i alternativet [Allmän konfiguration](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]</strong>.</td>
<td>Global</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>Konfigurera funktioner för leverans från butik på källnivå. Mer information finns i alternativet [Allmän konfiguration](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>Nej</td>
</tr>
<tr>
<td>Global</td>
<td>Nej</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>Konfigurera funktioner för leverans från butik på källnivå. Mer information finns i alternativet [Allmän konfiguration](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>Nej</td>
</tr>
</tbody>
</table>



| **Fält** | **Beskrivning** | **Omfång** | **Krävs** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | Latitudkoordinat för butikens plats. Den här obligatoriska informationen används vid platssökning och kartplacering i butiksupplevelsen. Värdet måste matcha butikens exakta adress för att validering ska kunna utföras. | Global | Ja |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | Longitudinell koordinat för butiksplatsen. Den här obligatoriska informationen används vid platssökning och kartplacering i butiksupplevelsen. Värdet måste matcha butikens exakta adress för att validering ska kunna utföras. | Global | Ja |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | Ange källan som en tillgänglig lagringsplats. Den här inställningen avgör om källan är synkroniserad och visas för besökare. | Global | Nej |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | Konfigurera funktioner för leverans till butik på källnivå. Mer information finns i alternativet [Allmän konfiguration](enable-general.md), **[!UICONTROL Enable Ship To Store]**. | Global | Nej |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | Konfigurera funktioner för leverans från butik på källnivå. Mer information finns i alternativet [Allmän konfiguration](enable-general.md), [!UICONTROL Enable Ship From Store] | Global | Nej |

{style="table-layout:auto"}

## Konfiguration av hämtningsplats

| **Fält** | **Beskrivning** | **Omfång** | **Krävs** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | Ett av två hämtningsalternativ. [!DNL In-Store Pickup] avser möjligheten att tillåta en kund att ange butiksplatsen för att hämta sin order. </br></br>När det här alternativet är aktiverat kan det visas för kunden i kassan. </br></br>Det här alternativet åsidosätter även den globala konfigurationen till [!UICONTROL Enable In-store Pickup] som konfigurerats på [!UICONTROL Delivery Method] för [!UICONTROL In-store Pickup] | Global | Nej |
| **Instruktioner för butiksinhämtning**</br>`Extension Attribute: store_pickup_instructions` | Ett anpassningsbart meddelande som levererats till kunden i e-postmeddelandet **Order Ready For Pickup in Store** . | Global | Nej |
| **Tillåt begränsning**</br>`Extension Attribute: curbside_enabled` | Ett av två hämtningsalternativ. Med rabattköp kan kunden parkera sin bil på en viss plats i butiken. I det här scenariot levereras beställningen till kunden av en butikspartner. </br></br>När det här alternativet är aktiverat kan det visas för kunden i kassan. Kunden kan också bli ombedd att beskriva sitt fordon och sin parkeringsplats under incheckningsprocessen. </br></br>Det här alternativet åsidosätter också den globala konfigurationen till **Aktivera Blockside Pickup** som konfigurerats på **leveransmetoden** för **Pickup i butik** | Global | Nej |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | Ett anpassningsbart meddelande som levererats till kunden i e-postmeddelandet [!UICONTROL Order Ready For Pickup in Store]. | Global | Nej |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | Antal minuter som krävs innan en order tas emot, plockas och är klar att hämtas. </br></br>Den här informationen används för att visa beräknade tider för orderhämtning till kunder på webbplatsen.</br></br> Om du anger det här alternativet åsidosätts den globala konfigurationen för **beräknad hämtningstid** som konfigurerats för **leveransmetoden** i konfigurationen för **hämtningen** i butiken. | Global | Nej |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | Etikett som visar antalet minuter tills en order är klar att plockas upp.</br></br> När du anpassar den här etiketten kan du använda koden %1 för att infoga din **beräknade hämtningstid**.</br></br> Om det här alternativet anges åsidosätts den globala konfigurationen för [!UICONTROL Estimated Pickup Time Label] som konfigurerats för [!UICONTROL Delivery Method] i [!UICONTROL In-store Pickup]. | Global | Nej |

### **Öppettider**

| **Fält** | **Beskrivning** | **Omfång** | **Krävs** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | Tidszonen för butiksplatsen för handlare. Ange öppnings- och sluttider för varje dag.</br></br>De här inställningarna används för att optimera beräknade upphämtningstider och i rapporter om uppfyllandetjänster. | Global | Ja |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | Driftstimmar för butiksplatsen för handlare. </br></br>Den här informationen kan användas för att optimera beräknade upphämtningstider och i tjänstrapportering för uppfyllelse. | Global | Ja |

### Konfigurera gränssnittsalternativ för incheckning



| **Fält** | **Beskrivning** | **Omfång** | **Krävs** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | Ange om butiksplatsen för handlare har parkeringspunkter för urbside-hämtning. </br></br>När det här alternativet är aktiverat kan du konfigurera tillgängliga parkeringsplatser. | Global | Nej |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | Ange om det krävs identifiering av parkeringsplats för kunder under shoppingupplevelsen.</br></br>Om det här alternativet är aktiverat uppmanas kunden att ange sin parkeringsplats vid ankomsten. Om detta är inaktiverat kan kunden hoppa över indata. | Global | Nej |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | De tillgängliga parkeringsplatserna på den här butiksplatsen för hämtning av reklamskyltar. Använd det angivna gränssnittet för att namnge varje dekorfärg.</br></br> Du behöver inte namnge varje parkeringsplats, bara de punkter som är avsedda för krökning. Du kan till exempel ha rader A-G på parkeringen tillgängliga, men bara de första 8 punkterna på rad A är avsedda för hämtning på sidan. I det här fallet kan du definiera 8 punkter, t.ex. A1, A2, A3 och så vidare. | Global | Nej |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | När den här inställningen är aktiverad kan kunden beskriva sin parkeringsplats under incheckning. | Global | Nej |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | Ange om det finns stöd för insamling av fordonsfärg från kunden vid incheckning. </br></br> De tillgängliga valen för [!UICONTROL Car Color] har konfigurerats i systeminställningarna för administratörsinställningarna [ för inloggningsupplevelsen ](check-in-experience-setup.md). | Global | Nej |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | Ange om identifiering av fordonsfärg krävs för kunder vid incheckning.</br></br>Om det här alternativet är aktiverat uppmanas kunden att ange färgen på sitt fordon vid ankomsten. Om detta är inaktiverat kan kunden hoppa över indata. | Global | Nej |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | Ange om det ska finnas stöd för insamling av fordon från kunden vid incheckning.</br></br> De tillgängliga valen för [!UICONTROL Car Make] har konfigurerats i systeminställningarna för administratörsinställningarna [ för inloggningsupplevelsen ](check-in-experience-setup.md). | Global | Nej |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | Ange om det krävs identifiering av fordonet för kunderna vid incheckning.</br></br>Om det här alternativet är aktiverat uppmanas kunden att ange vilket märke som ska användas för deras fordon vid ankomsten. Om detta är inaktiverat kan kunden hoppa över indata. | Global | Nej |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | Ange om det finns stöd för insamling av ytterligare information från kunden under incheckning. | Global | Nej |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | Ange om ytterligare information krävs för kunder vid incheckning. </br></br>Om det här alternativet är aktiverat uppmanas kunden att ange ytterligare information vid ankomsten. Om detta är inaktiverat kan kunden hoppa över indata. | Global | Nej |
