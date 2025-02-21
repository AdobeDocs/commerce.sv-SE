---
title: Återbetalningar
description: Skapa återbetalningar för  [!DNL Payment Services] order i Admin som en del av kreditfakturaprocessen.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Återbetalningar

Återbetalningar för [!DNL Payment Services] order skapas i administratören som en del av kreditnotsprocessen. En kreditnota är ett dokument som visar det belopp som ska betalas till kunden, för en fullständig eller partiell återbetalning, som kan tillämpas på ett köp eller återbetalas direkt till kunden. Kreditnotor kan bara utfärdas för order som är [fakturerade](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

Se [Kreditnotor](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} i vår huvudanvändarhandbok för mer information och för att lära dig hur du utfärdar och skriver ut kreditnotor.

För beställningar som behandlas med PayPal eller ett kreditkort kan du:

* Återbetala hela orderbeloppet
* Återbetala en del av en order (eller flera delbelopp)
* Återbetala ett belopp som är mindre än värdet för en viss orderartikel

Mer information finns i [Utfärda kreditnota](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} i vår huvudanvändarhandbok.

>[!NOTE]
>
>Ett fel uppstår för PayPal- eller kreditkortsbeställningar om du försöker att delvis återbetala en order för mer än det återstående orderbeloppet (ursprungligt belopp minus summan av befintliga återbetalningar) eller om du utfärdar en återbetalning för ett belopp som är större än det fullständiga orderbeloppet.

Inställningen [!UICONTROL Payment Action] i din [!UICONTROL Payment Settings]-konfiguration - antingen `Authorize` eller `Authorize and Capture` - avgör det [grundläggande återbetalningsarbetsflödet](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} för order.

Mer information finns i avsnittet [Betalningsåtgärdsinställningar](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} i _Utfärda kreditnota_.
