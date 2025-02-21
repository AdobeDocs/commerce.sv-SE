---
title: Voids
description: Med Voids kan du frigöra medel på ett kredit- eller betalkortskonto som blockeras eller hålls isär genom en auktorisering för beloppet av ett inköp.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Voids

Med [!DNL Payment Services] kan du använda den befintliga Commerce-funktionen för annullering av transaktioner. Med Voids kan du frigöra medel på ett kredit- eller betalkortskonto som blockeras eller hålls isär genom en auktorisering för beloppet av ett inköp.

>[!NOTE]
>
>Du kan bara annullera en transaktion om betalningen ännu inte har hämtats.

Om din butik är [konfigurerad](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} att endast auktorisera (inte hämta) medel vid försäljningstillfället, resulterar ett köp från din butik i en beställning med statusen `Processing` i Commerce Admin.

Du kan också [avbryta en beställning](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} som inte fakturerats. Alla ej inhämtade auktoriseringar annulleras också som en del av den annulleringsprocessen.

>[!NOTE]
>
>Om du avbryter en order skapas också en void, men om du annullerar en order utlöses ingen annullering.

Om du vill veta mer om de grundläggande steg som en order går igenom läser du avsnittet [Orderarbetsflöde](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} i huvudanvändarhandboken.

Mer information om funktionen void och hur du annullerar en ordertransaktion finns i [Bearbeta en beställning](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} i huvudanvändarhandboken.
