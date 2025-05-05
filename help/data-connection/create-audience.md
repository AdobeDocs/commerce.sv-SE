---
title: Skapa en målgrupp i Real-Time CDP med  [!DNL Commerce] händelsedata
description: Lär dig hur du använder  [!DNL Commerce] händelsedata för att skapa en målgrupp i Real-Time CDP
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---

# Skapa målgrupper i Real-Time CDP med [!DNL Commerce] händelsedata

Använd händelsedata som hämtats från din [!DNL Commerce]-butik för att skapa målgrupper i Real-Time CDP. De data som samlas in är baserade på webbläsarbeteende, tidigare köp, profilattribut, egenskaper att konvertera eller ändra, lojalitetsstatus, högt och lågt kundvärde och mycket annat.

## Vilka data bör jag överväga att använda?

Skapa målgrupper i Real-Time CDP med data från butiker, back office och profilevent.

| Datatyper | data från Storefront (beteendehändelser) | Back office-data (händelser på serversidan) | Kundprofil och segmentdata |
|---|---|---|---|
| **Definition** | Klicka på eller vidta de åtgärder som kunderna ska vidta på er webbplats. | Information om livscykeln och detaljer för varje order (tidigare och aktuell). | Vilka era kunder är och vilka segment är de kvalificerade för? |
| **Händelser som hämtats av Adobe Commerce** | [productPageView](events.md#productpageview)<br>[addToCart](events.md#addtocart) | [placeOrder](events.md#completecheckout)<br>[orderplaced](events-backoffice.md#orderplaced)<br>[orderLineItemRefunded](events-backoffice.md#orderlineitemrefunded)<br>[order Canceled](events-backoffice.md#ordercancelled)<br>[orderhistorik](connect-data.md#send-historical-order-data) | [createAccount](events.md#createaccount)<br>[editAccount](events.md#editaccount)<br>[Profilpost](events-profilerecord.md) |

## Vad har andra kunder gjort?

Adobe [!DNL Commerce]-kunder har uppnått betydande affärsmässiga konsekvenser genom att aktivera målgrupper som är inbyggda i Real-Time CDP och distribuera dem till sin [!DNL Commerce] -instans.

En global klädhandlare med flera varumärken har uppnått följande:

- En källa till sanning med 10 miljoner enhetliga kundprofiler
- Skapade över 40 unika målgrupper av&quot;kunder med hög återgivning&quot; för att engagera olika kanaler

Ett globalt dryckesföretag som samlat in

- 98 miljoner kundprofiler från över 100 länder

## Kom så börjar vi

I den här artikeln får du lära dig att:

- Skapa en målgrupp i Real-Time CDP baserat på de [!DNL Commerce] data som händelserna samlar in
- Aktivera den målgruppen för din [!DNL Commerce]-butik
- Använd målgruppen i [!DNL Commerce] för att informera om en kundprisregel

>[!IMPORTANT]
>
>Slutför uppgifterna som beskrivs i den här artikeln med sandlådemiljön [!DNL Commerce]. Detta säkerställer att händelsedata för butiken och back office som du skickar till Experience Platform inte späder ut dina data för produktionshändelser.

### Förutsättningar

Innan du börjar, se till att:

- Du är redo att använda Real-Time CDP. Om du är osäker kan du kontakta systemintegratören eller utvecklingsteamet som hanterar projekt och miljöer.
- Du [installerade](install.md) och [konfigurerade](connect-data.md) tillägget [!DNL Data Connection] i [!DNL Commerce].
- Du [bekräftade](connect-data.md#confirm-that-event-data-is-collected) att dina [!DNL Commerce]-händelsedata kommer till Experience Platform.

### 1. Skapa en målgrupp

En målgrupp är en uppsättning kunder som har liknande beteenden eller egenskaper. I den här övningen skapar ni en målgrupp som kvalificerar personer som är intresserade av en viss produkt från er butik.

Om du vill förenkla den här övningen använder du händelsedata från [productPageView](events.md#productpageview) -händelsen. Den här händelsen innehåller information om produkten som visades, t.ex. produktnamn, SKU, pris och så vidare.

Använd dessa händelsedata för att ange att målgruppen omfattar personer som har minst en&quot;produktvy&quot;-händelse där SKU (produktidentifierare) är lika med en viss produkt på din webbplats och händelsen inträffar under den sista dagen. &#x200B;

1. Öppna Experience Platform och välj **[!UICONTROL Audiences]** på den vänstra navigeringsmenyn.

   ![Målkontrollpanel](assets/audience-left-rail.png)

1. Klicka på **[!UICONTROL Create Audience]**.

   ![Skapa publik](assets/browse-create-audience.png)

   Arbetsytan **Segment Builder** visas.

1. I arbetsytan **Segment Builder** väljer du metoden **Skapa regel** .

   ![Skapa regel](assets/build-rule.png)

   På arbetsytan **Segment Builder** kan du definiera regler och villkor för din målgrupp. &#x200B; Dessa regler och villkor baseras på händelse- och profildata från din Commerce Store och definierar de kriterier som avgör om en användare uppfyller kraven för målgruppen. Du kan t.ex. skapa en regel som omfattar användare som har visat en viss produkt eller användare som har gjort ett köp inom en viss tidsram. Läs mer om [Segment Builder](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder) och regler och villkor.

1. Välj fliken [Händelser](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder#events).

   ![Fliken Händelser](assets/audience-events-tab.png)

1. Sök efter händelsetypen&quot;Produktvyer&quot;. Dra och släpp det sedan på arbetsytan **Segment Builder** .

1. Gå tillbaka till fliken **Händelser** och sök efter&quot;SKU&quot;, som är ett datafält under fältet `productListItems`. Dra och släpp den på arbetsytan i **Segment Builder** ovanpå händelsen **Produktvy**.

   Avsnittet **Händelseregler** visar var du kan ange den specifika produkt du vill skapa din publik av.

   ![Välj SKU](assets/audience-addsku.png)

1. Ange tidsintervallet till en dag genom att klicka på **Valfri tid** och välja *Under senaste* med värdet *1*.

   När du skapar en målgrupp kan du ange ett tidsintervall för att hämta den senaste aktiviteten. Om du anger ett tidsintervall kan du rikta in dig på användare baserat på deras senaste interaktioner eller beteenden inom en viss tidsram.

1. I avsnittet **Målgruppsegenskaper** till höger om arbetsytan anger du målgruppsegenskaperna genom att ange ett namn, en beskrivning och en utvärderingsmetod för målgruppen.

1. Klicka på **[!UICONTROL Save and Close]** om du vill spara målgruppen.

   Information om din målgrupp visas på kontrollpanelen **Målgrupp**.

### 2. Aktivera målgruppen för målet [!DNL Commerce]

Du gör en målgrupp tillgänglig i [!DNL Commerce] genom att aktivera den för målet [!DNL Commerce].

>[!IMPORTANT]
>
>Om du inte redan har angett [!DNL Commerce] som ett tillgängligt mål för att ta emot data kan du läsa avsnittet [Adobe [!DNL Commerce] Connection](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/personalization/adobe-commerce) .

1. Klicka på **Aktivera till mål** på fliken **Detaljer** för målgruppen.

1. Välj ditt [!DNL Commerce]-mål. Klicka sedan på **Nästa**.

1. Slutför aktiveringsprocessen genom att klicka på **[!UICONTROL Finish]**.

## 3. Visa målgruppen på Publikkontrollpanelen

I [!DNL Commerce] kan du visa alla [aktiva](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations) målgrupper som kan anpassas för din [!DNL Commerce]-instans med kontrollpanelen **Real-Time CDP Audiences** .

Gå till sidofältet _Admin_ och gå till **[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]** för att komma åt kontrollpanelen **Real-Time CDP Audiences**.

På kontrollpanelen letar du efter den målgrupp du har skapat. Observera att det inte används i en kundprisregel eller ett dynamiskt block. I nästa avsnitt länkar du målgruppen till en kundvagnsprisregel.

![Real-Time CDP Audiences Dashboard](assets/real-time-cdp-dashboard.png)

### 4. Skapa en kundprisregel baserad på målgruppen

I det här avsnittet visas hur du skapar en kundprisregel baserat på din nya målgrupp.

1. Bekräfta att din nya målgrupp visas på kontrollpanelen **Real-Time CDP Audiences**.
1. [Skapa en kundprisregel](https://experienceleague.adobe.com/sv/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create).
1. [Ange villkoret](https://experienceleague.adobe.com/sv/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#use-real-time-cdp-audiences-to-set-a-condition) för kundvagnsprisregeln med din nya målgrupp.
1. [Ange den åtgärd](https://experienceleague.adobe.com/sv/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#step-3-define-the-actions) som du vill ska utföras när produkten läggs till i kundvagnen.
1. Fortsätt att konfigurera kundvagnsprisregeln.
1. Gå till kundvyn för din sandlådeinstans.
1. Lägg den produkt du baserar målgruppen på i kundvagnen. Observera att kundvagnsprisregeln är aktiverad.

## Radbryt

I den här övningen skapade du en målgrupp i Real-Time CDP och aktiverade den till målet [!DNL Commerce]. I [!DNL Commerce]-administratören skapade du sedan en kundprisregel baserad på den målgruppen och aktiverade regeln i din sandlådemiljö.
