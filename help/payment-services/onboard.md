---
title: Inbyggt [!DNL Payment Services]
description: Koppla instansen till  [!DNL Payment Services] funktionaliteten genom att slutföra några introduktionssteg.
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Inbyggt [!DNL Payment Services]

Om du vill komma igång med att använda [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] måste du slutföra några startsteg för att ansluta instansen med betalningsfunktionen.

## Startflöde

Det här flödesdiagrammet visar den allmänna processen för introduktion av [!DNL Payment Services].

![Startflöde](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> För Adobe Commerce version 2.4.7 eller senare kan du hoppa över Marketplace-tillägget eftersom [!DNL Payment Services] är tillgängligt direkt.

När du är klar med introduktionen av sandlådan eller livebetalningar är ekonomisk rapportering tillgänglig från [!DNL Payment Services] i Admin.

Om både sandlåda och live-betalningar är aktiverade kan du enkelt växla mellan dessa lägen från startsidan för [!DNL Payment Services].

## Förutsättningar

Om du vill använda [!DNL Payment Services] måste alla beroende moduler vara aktiverade och följande tillgängliga för din instans:

* Modulen Services Connector
* Tjänster-ID-modul
* API-nycklar

Services Connector- och Services ID-modulerna installeras automatiskt under [installationen av [!DNL Payment Services]](install.md).

När installationen är klar visas ett nytt avsnitt i konfigurationsinställningarna (**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**) om du expanderar **[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**.

Mer information om hur du skapar eller kommer åt API-nycklar finns i [API-autentiseringsuppgifter](#obtain-api-credentials).

## Onboarding-steg

1. [Installera  [!DNL Payment Services] tillägget](install.md#get-payment-services).
1. [Hämta API-autentiseringsuppgifter](connect.md#obtain-api-credentials).
1. [Anslut instansen](connect.md#configure-commerce-services) till Commerce Services. Anslutningen får endast göras en gång per Commerce-instans.
1. [Konfigurera sandlådetjänsten](sandbox.md#enable-sandbox-testing) (eller, alternativt, fortsätta till [aktivera live-betalningar](sandbox.md#enable-live-payments) om du har testat funktioner i en annan miljö) med ett PayPal-betalningshanteringskonto.
1. [Ange [!DNL Payment Services] som betalningsmetod](production.md#set-payment-services-as-payment-method), i sandlådeläge, för att börja bearbeta testbetalningar.
1. [Begär betalningsberättigande](production.md#request-payments-entitlement-from-adobe) för att aktivera liveintroduktion.
1. [Fullständig registrering av handlare](production.md#complete-merchant-onboarding) för att aktivera livebetalningar för dina Commerce-webbplatser.
1. [Hämta ditt  [!DNL Payment Services] handels-ID](production.md#configure-pricing-tier) och skicka det till Försäljning för att konfigurera rätt prisnivå.
1. [Aktivera [!DNL Payment Services] i direktläge](production.md#enable-live-payments) för att börja bearbeta direktbetalningar.
1. Testa betalningar i både [sandbox](sandbox.md#test-in-sandbox-environment)- och [production](production.md#test-in-production)-miljöer.

>[!NOTE]
>
>Om du inte konfigurerar dina Commerce-tjänster i Admin (steg 3) kan du inte konfigurera sandlådor eller livesändningar.

## Felsökning

* [Felsök [!DNL Payment Services] installationen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [PayPal-sandlådekontot har inte verifierats](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [Fördröjd [!DNL Payment Services] rapportdata](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
* [Testkreditkortet fungerar inte med PayPal när betalningar bearbetas i sandlådemiljö](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
