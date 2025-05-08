---
title: Spåra dina leveranser i  [!DNL Payment Services]
description: Anpassa [!DNL Payment Services] leveranser och spårningsinformation som visas på PayPal Merchant Dashboard.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Spåra dina leveranser i [!DNL Payment Services]

[!DNL Payment Services] gör att handlare kan se spårningsinformationen för en leverans i sin PayPal Merchant Dashboard.

Mer information om leveransrutnätet för Adobe Commerce finns i avsnittet [försändelser](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank}.

## Hur spårning av leveransen fungerar

Den här funktionen beror på om ordern har fakturerats, eftersom PayPal måste ta emot en `capture_id` för att bearbeta spårningsinformationen. Om en handlare levererar sina produkter före hämtningen skickas inte spårningsinformationen till PayPal.

>[!NOTE]
>
> Vi rekommenderar att du skapar en leverans per spårningsnummer och associerar rätt artiklar med leveransen.

## Lägga till spårningsnumret

Följande instruktioner hjälper dig genom processen att skapa en leverans i Adobe Commerce med [!DNL Payment Services]:

1. Gå till **[!UICONTROL Sales]** > **[!UICONTROL Orders]** på sidofältet _Admin_.

1. Klicka på **[!UICONTROL View]** i kolumnen **[!UICONTROL Action]** för den markerade ordningen.

1. Klicka på **[!UICONTROL Ship]**.

1. Bläddra ned till blocket **[!UICONTROL Payment & Shipping Method]** och klicka på **[!UICONTROL Add Tracking Number]** i **[!UICONTROL Shipping Information]**.

1. Ange **[!UICONTROL Carrier]**.

1. Om du vill spåra leveransen anger du **[!UICONTROL Title]** och **[!UICONTROL Number]** .

1. Klicka på **[!UICONTROL Submit Shipment]**.

>[!NOTE]
>
> Du kan också använda en leveransmodul för att ange information om spårningsnummer. Kontrollera att leveransmodulen sparar information om spårningsnummer i fältet `tracking_number`.

### Förenlighet med tredje part

Alla tillägg från tredje part är kompatibla med funktionen när en försändelseenhet skapas via [Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}.
