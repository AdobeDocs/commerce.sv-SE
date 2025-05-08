---
title: Kompatibilitet för  [!DNL Payment Services]
description: Lär dig om  [!DNL Payment Services] finns i ditt land och om det är kompatibelt med din Adobe Commerce-version.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Kompatibilitet för [!DNL Payment Services]

[!DNL Payment Services] finns för Adobe Commerce och Magento Open Source. [!DNL Payment Services] är nu kompatibelt med Adobe Commerce version 2.4.x.

## Förutsättningar

Om du vill använda [!DNL Payment Services] måste du först ansluta din Commerce-instans. **Du konfigurerade den här anslutningen endast en gång**.

1. Om du är osäker på om din instans är ansluten navigerar du till **System** > Tjänster > **Commerce Services Connector** och visar nyckelvärdena för offentlig och privat API i avsnitten Sandbox-nycklar och produktionsnycklar, samt till fälten Projekt och datautrymd i avsnittet SaaS-identifierare. Om dessa värden finns är instansen ansluten.

1. Om du fortfarande behöver ansluta din instans kan du läsa instruktionerna på sidan [Commerce Services Connector](../landing/saas.md) .

   >[!TIP]
   >
   > Mer information finns i videon [Adobe Commerce Services Connector](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector).

1. Om du redan har anslutit din instans går du till sidan [onboarding](onboard.md) för nästa steg.

>[!IMPORTANT]
>
> Alla handlare som är berättigade för [!DNL Payment Services] kan använda **ett produktionsdatautrymme** och **två testdatautrymme**.

## Standard vs. avancerad [!DNL Payment Services]-upplevelse

[!DNL Payment Services] tillhandahåller **Standard** (Express Checkout) och **Advanced** (helt stöds) betalningsalternativ och startflöden, beroende på vilket land du arbetar i.

>[!NOTE]
>
> [!DNL Payment Services] innehåller [Express Checkout-funktioner](../payment-services/payments-options.md) (delmängd av betalningsalternativ) för andra [tillgängliga länder under introduktionen](../payment-services/production.md#complete-merchant-onboarding).

### Vilket [!DNL Payment Services]-alternativ passar dig?

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

Mer information om hur du konfigurerar tillägget [!DNL Payment Services] finns i [Anslut](connect.md).

>[!BEGINTABS]

>[!TAB Standard (Express Checkout)]

![kontrollera](assets/icon-check.png) PayPal-utcheckning

![kontrollera](assets/icon-check.png) PayPal Debit- eller kreditkortsknapp

![checka](assets/icon-check.png) Anpassade utcheckningskonfigurationer

![kontrollera](assets/icon-check.png) Standardpriser

![check](assets/icon-check.png) **Tillgänglig i XX länder**

[![läs mer](assets/learn-more-button.svg)](onboard.md)

>[!TAB Avancerat (stöds fullt ut)]

![check](assets/icon-check.png) Debetkort

![check](assets/icon-check.png) PayPal-kredit

![kontrollera](assets/icon-check.png) Kreditkortsfält

![kontrollera](assets/icon-check.png) Apple Pay-knapp

![kontrollera](assets/icon-check.png) Google Pay-knapp

![kontrollera](assets/icon-check.png) PayPal-betalningsknappar

![kontrollera](assets/icon-check.png) Venmo-knappen

![kontrollera](assets/icon-check.png) PayPal Debit- eller kreditkortsknapp

![kontrollera](assets/icon-check.png) Knappen Betala senare

![checka](assets/icon-check.png) Anpassade utcheckningskonfigurationer

![check](assets/icon-check.png) Anpassade priser

![check](assets/icon-check.png) (L2/L3-pris - endast USA)

![check](assets/icon-check.png) **Endast tillgängligt i USA (USA), Kanada (CA), Australien (AUS). Frankrike (FR), Storbritannien (UK)**

[![läs mer](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

Se sidorna för [Livscykelprincipen](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=sv-SE) och [[!DNL Payment Services] versionsinformationen](release-notes.md) för mer information om version och version.

Mer information om hur du får de fullständiga instruktionerna och startar introduktionsprocessen finns i [Kom igång med [!DNL Payment Services]](onboard.md).

### Godkända kreditkort och valutor

[!DNL Payment Services] accepterar valutorna för de länder [där den är tillgänglig](#availability). Mer information om hur du ställer in valutakurser finns i [Valutakonfiguration](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=sv-SE).

Mer information om valutor och betalningsmetoder för PayPal-produkter och -tjänster finns på följande sidor:

* [Dokumentation för valutor som stöds](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Dokumentation om betalningsmetoder](https://developer.paypal.com/docs/checkout/payment-methods/).
