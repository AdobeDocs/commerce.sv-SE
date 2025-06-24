---
title: Användarhantering
description: Lär dig hantera användare i  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
role: Admin
source-git-commit: a06d64566fda76c0527aabfa9e8fdf27e7c149ca
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Användarhantering

Om du vill att användare ska få åtkomst till Admin i [!DNL Adobe Commerce as a Cloud Service] måste du lägga till dem som användare i din organisation och se till att de har åtkomst till Cloud Service-produkten i [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Den här processen kräver en IMS-organisation med åtkomst till [!DNL Adobe Commerce as a Cloud Service]. Dessa processer kan endast utföras av systemadministratören eller produktadministratören för organisationen.

>[!TIP]
>
>Om du vill lägga till flera användare samtidigt kan du utföra en [massöverföring av en CSV](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> Du kan också lägga till flera användare till en roll genom att skapa en [användargrupp](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Sedan kan du lägga till [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**] -produkten i användargruppen.

## Förstå roller

Följande roller är tillgängliga för [!DNL Adobe Commerce as a Cloud Service]. Om du vill visa eller redigera de här rollerna går du till **System** > **Behörigheter** > **Användarroller** i Commerce Admin.

* **Användare** - Användare har administratörsåtkomst till Commerce Admin, men kan inte hantera åtkomst på produktnivå i Admin Console. Användare kan också använda krediter för att [skapa instanser](./getting-started.md#create-an-instance) i [!DNL Commerce Cloud Manager].

* [**Utvecklare**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Utvecklare har användarbehörigheter och läggs till i Commerce-instansen som utvecklaranvändare. Det innebär att de kan använda användargränssnittet [Admin SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [konfigurera händelser](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} och [skapa webbböcker](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Administratörer - Det finns tre olika typer av administratörer:
   * [Systemadministratörer](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - Systemadministratören har åtkomst till alla produkter och produktprofiler i organisationen via Admin Console.
   * [Produktadministratörer](#add-a-product-admin) - Produktadministratörer kan [hantera användare, roller och behörigheter för produkten](#add-users-and-admins) i [!DNL Adobe Admin Console] och [hantera användare i Commerce Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Administratörer för produktprofiler](#add-users-developers-and-product-profile-admins) - Administratörer för produktprofiler har inte tillgång till Adobe Commerce Admin, men kan hantera användare för produkten i [!DNL Adobe Admin Console].

Mer information om behörigheter för varje roll i Adobe Commerce finns i [användarbehörigheter](#user-permissions).

## Lägg till en produktadministratör

1. Navigera till https://adminconsole.adobe.com och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**], under [!UICONTROL **Produkter och tjänster**], väljer du [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**] .

   ![välj produkt](./assets/backend.png){width="600" zoomable="yes"}

1. Välj fliken [!UICONTROL **Administratörer**].

1. Klicka på [!UICONTROL **Lägg till administratör**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till som administratörer och klicka på [!UICONTROL **Spara**].

## Lägga till användare, utvecklare och produktprofiladministratörer

Följande instruktioner innehåller information om hur du lägger till användare och utvecklare i [!DNL Commerce Cloud Manager] och Commerce Admin. Med gränssnittet [!DNL Commerce Cloud Manager] kan du skapa och hantera dina Commerce-instanser.

>[!NOTE]
>
>Endast produktadministratörer och systemadministratörer kan lägga till användare och utvecklare i Adobe Commerce as a Cloud Service.

1. Navigera till https://adminconsole.adobe.com och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**], under [!UICONTROL **Produkter och tjänster**], väljer du [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**] .

   ![välj produkt](./assets/backend.png){width="600" zoomable="yes"}

1. Klicka på produktprofilen [!UICONTROL **Standard - Cloud Manager**].

1. Välj fliken [!UICONTROL **Användare**], [!UICONTROL **Utvecklare**] eller [!UICONTROL **Administratörer**] och klicka på [!UICONTROL **Lägg till användare**] eller [!UICONTROL **Lägg till utvecklare**] eller [!UICONTROL **Lägg till administratörer**].

   >[!NOTE]
   >
   >Administratörer som läggs till från den här skärmen är [produktprofiladministratörer](#understanding-roles) och har inte åtkomst till Commerce Admin.

   ![tabbmarkera](./assets/tab-select.png){width=600 zoomable="yes"}

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till som administratörer och klicka på [!UICONTROL **Spara**].

## Rollresurser

I följande lista beskrivs de resurser som standardroller har behörighet att komma åt inifrån Adobe Commerce Admin. Om du vill redigera standardbehörigheterna för varje roll går du till **System** > **Behörigheter** > **Användarroller** i Commerce Admin.

**Användare**

* Katalog
   * Lager
      * Produkter
         * Läs produktpris

**Utvecklare**

* Katalog
   * Lager
      * Produkter
         * Läs produktpris
* System
   * Dataöverföring
      * Importera historik
* Konfiguration av Adobe IO-händelser
   * Konfigurationskontroll
   * Skapa händelseprovider
   * Konfigurationsuppdatering
   * Synkronisera händelser
   * Hämta händelseproviderlista
* Eventing Framework
   * Händelselista
   * Testa händelseanslutning
   * Prenumerera på en händelse
   * Avbeställ en händelse
   * Händelsestatus
   * API för att hämta händelseprenumerationer
   * Visa användargränssnitt för administratörer för händelseprenumerationer
   * Skapa användargränssnitt för händelseprenumerationer
   * Begär nytt användargränssnitt för händelseadministratör
* Webhooks
   * Webhooks Digital Signature
      * Webhooks-inställningar för digitala signaturer
      * Skapa nycklar för digitala signaturer på webbhooks
   * Hantering av webbhotell
      * Webhooks Grid
      * Redigera webbhotell
      * Testa webbhotell
      * API-prenumeration på webkrok
      * API - avbeställning från webkrok
      * Webhooks-lista
      * Begär ny webbkrok
      * Webhooks-loggar
      * Få en lista över webbhooks

**Administratörer**

Administratörer har åtkomst till alla behörigheter.
