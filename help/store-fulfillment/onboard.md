---
title: Onboarding Overview for Store Fulfillation Services
description: '[!DNL Live Search] introduktionsflöde, systemkrav, gränser och begränsningar.'
role: Admin, Leader
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Onboarding Overview for Store Fulfillment

Kom igång med [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] genom att konfigurera, konfigurera och aktivera följande komponenter:

- **Lagra uppfyllelsetillägg**-Installera och konfigurera det här tredjepartstillägget på din Adobe Commerce-instans. Efter installationen kan du konfigurera och hantera Store Fulfillment-lösningen från Admin för att stödja [!DNL buys online, pickup in store]-scenarier (BOPIS) i Commerce Store.

  ![[!DNL Store Fulfillment Service]-konfiguration i administratörsvyn ](assets/store-fulfillment-admin-home.png)

- **Lagra uppfyllandekonto**-Under aktiveringsprocessen skapar en kontohanterare ditt Store-uppfyllelsekonto och ger dig kontoinformation och autentiseringsuppgifter. Dessa autentiseringsuppgifter krävs för att aktivera anslutningen mellan Adobe Commerce och Store Fulfillment-lösningen.

- **Store Assist-appen** - Tillhandahåller butikskopplingar som är kopplade till ett arbetsflöde för att hantera BOPIS-beställningar från mobila enheter. Store Associates kan hämta och installera Walmarts [!DNL Store Assist] för iOS- och Android™-enheter. Processen för att introducera appar hanteras av Walmart Commerce Technologies Client Center som en separat process. [Vissa programkonfigurationsinställningar](user-setup.md) har dock slutförts från Adobe Commerce Admin.

  | Store Assist App - vyn Kom igång | Store Assist App - Modulvy |
  |-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | Vyn ![[!DNL Store Assist App Getting Started] på den mobila enheten ](assets/store-assist-get-started-small.png) | ![[!DNL Store Assist App Orders view] på den mobila enheten ](assets/store-assist-orders-small.png) |

## Etableringssteg

- **Registrera dig för[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]**-Fyll i anmälningsformuläret på [business.adobe.com](https://business.adobe.com/resources/store-fulfillment.html) eller kontakta din kontoansvarige på Adobe Commerce om du behöver hjälp.

- **Initiera etableringsbegäran för Store Fulfillment**-Fyll i det formulär för intag som din kontohanterare tillhandahåller för att tillhandahålla den information som krävs för att påbörja etableringsprocessen.

- **Hämta autentiseringsuppgifter för ditt Store Fulfillment-konto**-När ditt Store Fulfillment-konto har skapats för dig får du de autentiseringsuppgifter som krävs för att integrera Store Fulfillment-lösningen med Adobe Commerce.

- **[Hämta källkoden för att installera  [!DNL Store Fulfillment] tillägget](install.md)**

## Onboarding-steg

1. [Installera Store Fulfillment-tillägget för Adobe Commerce](install.md).

1. [aktivera lösningen](enable-general.md) från administratören.

1. [Konfigurera Store Fulfillment-tillägget från Adobe Commerce Admin](service-config-settings-overview.md).

1. [Anslut  [!DNL Store Fulfillment] tjänsten med de Store Fulfillment-autentiseringsuppgifter som du har fått](connect-set-up-service.md).

1. [Skapa användare och roller för Store Assist-appen](user-setup.md).

1. [Hämta Walmarts [!DNL Store Assist] app till den önskade enheten. Appen finns både i Apple App (iOS) och Google Play (Android™)](app-setup.md).

När du har installerat, konfigurerat, slutfört introduktionen och har tillgång till appen [!DNL Store Assist] kan du [börja skapa order och testa](test-and-deploy.md).
