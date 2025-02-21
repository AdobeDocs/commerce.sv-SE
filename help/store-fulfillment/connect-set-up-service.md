---
title: Anslut lagringslösningen Store Fulfillment
description: Upprätta kopplingarna mellan Adobe Commerce och Store Fulfillment-lösningen. Skapa och auktorisera en Adobe Commerce-integrering och lägg till autentiseringsuppgifterna för Store Fulfillment-kontot i Adobe Commerce tjänstkonfiguration.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Anslut lagringslösningen Store Fulfillment

Anslut Store Fulfillment Services till Adobe Commerce genom att lägga till autentiseringsuppgifter och anslutningsdata till Adobe Commerce Admin.

- **[Konfigurera [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)**-Skapa en Adobe Commerce-integrering för Store Fulfillment-tjänster och generera åtkomsttoken för att autentisera inkommande begäranden från Store Fulfillment-servrar.

- **[Konfigurera kontoautentiseringsuppgifter för Store Fulfillment Services](#configure-store-fulfillment-account-credentials)**-Lägg till dina autentiseringsuppgifter för att ansluta Adobe Commerce till ditt Store Fulfillment-konto.

>[!NOTE]
>
>Slutför anslutningskonfigurationen och validera anslutningen innan du börjar testa.

## Integrera Adobe Commerce

Om du vill integrera Adobe Commerce med Store Fulfillment services skapar du en Commerce-integrering och skapar åtkomsttokens som kan användas för att autentisera begäranden från Store Fulfillment-servrar. Du måste också uppdatera alternativen för Adobe Commerce [!UICONTROL Consumer Settings] för att förhindra `The consumer isn't authorized to access %resources.` svarsfel på begäranden från Adobe Commerce till [!DNL Store Fulfillment]-tjänster.

1. I Admin skapar du integreringen för Butiksuppfyllelse.

   - Namnge tillägget
   - Ange din e-postadress
   - Ange ditt lösenord för administratörskontot

1. Konfigurera API-resursåtkomstbehörigheter för integrering med följande:

   - Försäljning > BOPIS-orderuppdatering
   - System > Store Fulfillment App Permissions

1. Generera åtkomsttoken för autentisering genom att spara och aktivera integreringen.

1. Kopiera och spara åtkomsttokens på en säker, krypterad plats.

1. Arbeta med din Account Manager för att slutföra konfigurationen på sidan för Store Fulfillment och för att godkänna integreringen.

1. Aktivera alternativet Adobe Commerce [!UICONTROL Consumer Settings] till [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens].

   - Gå till **[!UICONTROL Stores]** > [!UICONTROL Configuration] > **[!UICONTROL Services]** > **[!UICONTROL OAuth]** > **[!UICONTROL Consumer Settings]** i Admin

   - Ställ in alternativet [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] på **[!UICONTROL Yes]**.

>[!IMPORTANT]
>
> Integrationstoken är miljöspecifik. Om du återställer databasen för en miljö med källdata från en annan miljö - till exempel återställning av produktionsdata från en mellanlagringsmiljö - utelämnar du tabellen `oauth_token` från databasexporten så att integreringstokeninformationen inte skrivs över under återställningsåtgärden.


## Konfigurera autentiseringsuppgifter för lagringskontot för uppfyllelse

När du fyllt i formuläret skapas ett Walmart Store Fulfillment-konto åt dig. Du får följande autentiseringsuppgifter när de är tillgängliga:

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL] (vanligtvis samma som ovanstående konfiguration)

Dessa autentiseringsuppgifter krävs för att konfigurera och använda Store Fulfillment.

>[!NOTE]
>
>Det kan ta en stund att slutföra processen för att skapa kontot. När du väntar på autentiseringsuppgifter granskar och konfigurerar [andra inställningar för Store Fulfillment-lösningen](service-config-settings-overview.md).

### Lägg till autentiseringsuppgifter för att ansluta till Store Fulfillment

1. Konfigurera [kontoautentiseringsuppgifter](enable-general.md) för produktions- och sandlådemiljöerna.

1. Gå till **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]** från administratören

1. Ange kontoautentiseringsuppgifterna som har angetts för **[!UICONTROL Production environment]**. Alla fält är obligatoriska.

1. Välj **[!UICONTROL Save Config]**.

1. Testa anslutningen genom att välja **[!UICONTROL Validate Credentials]**.

>[!NOTE]
>
>Om inloggningsuppgifterna är ogiltiga kontrollerar du att du har angett rätt värden för varje miljö och validerar igen. Kontakta din kontorepresentant om du fortfarande har problem med att ansluta.
