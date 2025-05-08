---
title: Voids
description: Med Voids kan du frigöra medel på ett kredit- eller betalkortskonto som blockeras eller hålls isär genom en auktorisering för beloppet av ett inköp.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Voids

[!DNL Payment Services] har stöd för Commerce befintliga funktioner för annullering av transaktioner. En void frigör medel i ett kredit- eller betalkortskonto som innehas av en auktorisering för inköpsbeloppet. Transaktioner kan bara annulleras om betalningen ännu inte har hämtats.

* Om din butik är [konfigurerad](https://experienceleague.adobe.com/sv/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} att endast auktorisera (inte hämta) medel vid försäljningstillfället, resulterar ett köp från din butik i en beställning med statusen `Processing` i Commerce Admin.

* Du kan också [avbryta en beställning](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} som inte fakturerats. Alla ej inhämtade auktoriseringar annulleras också som en del av den annulleringsprocessen.

>[!NOTE]
>
>Om du avbryter en order skapas också en void, men om du annullerar en order utlöses ingen annullering.

Om du vill veta mer om de grundläggande steg som en order går igenom läser du avsnittet [Orderarbetsflöde](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} i huvudanvändarhandboken.

Mer information om funktionen void och hur du annullerar en ordertransaktion finns i [Bearbeta en beställning](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} i huvudanvändarhandboken.
