---
title: Användarhantering
description: Lär dig hantera användare i  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud, Integration
role: Admin
level: Intermediate
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: f71795ab6a10a28e6352d7adfcffd11a40e8ef67
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 0%

---

# Användare och Identity Management

Om du vill ge användare åtkomst till administratören i [!DNL Adobe Commerce as a Cloud Service] lägger du till dem som användare i din organisation och ser till att de har åtkomst till Cloud Service-produkten i [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Den här processen kräver en IMS-organisation med åtkomst till [!DNL Adobe Commerce as a Cloud Service]. Dessa processer kan endast utföras av systemadministratören eller produktadministratören för organisationen.

>[!TIP]
>
>Om du vill lägga till flera användare samtidigt kan du utföra en [massöverföring av en CSV](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
> Du kan också lägga till flera användare till en roll genom att skapa en [användargrupp](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Sedan kan du lägga till [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]-produkten i användargruppen.

## Förstå roller

Följande roller är tillgängliga för [!DNL Adobe Commerce as a Cloud Service]. Om du vill visa eller redigera de här rollerna går du till [!UICONTROL **System**] > [!UICONTROL **Behörigheter**] > [!UICONTROL **Användarroller**] i Commerce Admin.

* **Användare** - Användare har administratörsåtkomst till Commerce Admin men kan inte hantera åtkomst på produktnivå i Admin Console. Användare kan också använda krediter för att [skapa instanser](./getting-started.md#create-an-instance) i [!DNL Commerce Cloud Manager].

  >[!NOTE]
  >
  >Alla Commerce-användare, inklusive utvecklare och administratörer, måste också ha tilldelats användarrollen. Det krävs för grundläggande Commerce-behörigheter.

* [**Utvecklare**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} - Utvecklare har användarbehörigheter och läggs till i Commerce-instansen som utvecklaranvändare. De kan använda [[!DNL Admin UI SDK]](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [konfigurera händelser](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} och [skapa webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Administratörer - Det finns tre olika typer av administratörer:
   * [Systemadministratörer](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - Systemadministratören har åtkomst till alla produkter och produktprofiler i organisationen via Admin Console.
   * [Produktadministratörer](#add-a-product-admin) - Produktadministratörer kan [hantera användare, roller och behörigheter för produkten](#add-users) i [!DNL Adobe Admin Console] och [hantera användare i Commerce Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Administratörer för produktprofiler](#add-developers-and-product-profile-admins) - Administratörer för produktprofiler har inte tillgång till Adobe Commerce Admin, men kan hantera användare för produkten i [!DNL Adobe Admin Console].

Mer information om behörigheter för varje roll i Adobe Commerce finns i [användarbehörigheter](#user-permissions).

## Lägg till en produktadministratör

>[!BEGINTABS]

>[!NOTE]
>
>Tilldela produktadministratörer [användarrollen](#add-users) innan du lägger till dem som produktadministratörer. Användarrollen krävs för grundläggande Commerce-behörigheter.

>[!TAB GA (tillhandahålls efter 13 oktober 2025)]

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. Välj fliken [!UICONTROL **Användare**].

1. Välj fliken [!UICONTROL **Administratörer**].

1. Klicka på [!UICONTROL **Lägg till administratör**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till som administratörer och klicka på [!UICONTROL **Nästa**].

1. Välj rollen [!UICONTROL **Produktprofiladministratör**].

1. Klicka på [!UICONTROL **+**] för att lägga till produkter.

1. Markera den befintliga Commerce-instansen som administratören ska läggas till i. Commerce-instanser har följande format: `Adobe Commerce - <instance-name> - ACCS - <environment-type> - <tenant-id>`.

1. Välj produktprofil.

1. Klicka på [!UICONTROL **Använd**].

1. Klicka på [!UICONTROL **Spara**].

>[!TAB Tidig åtkomst (tillhandahålls före 13 oktober 2025)]

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**] väljer du [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] under [!UICONTROL **Produkter och tjänster**].

   ![Produkturval i Admin Console som visar Adobe Commerce Cloud Manager](./assets/backend.png){width="600" zoomable="yes"}

1. Välj fliken [!UICONTROL **Administratörer**].

1. Klicka på [!UICONTROL **Lägg till administratör**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till som administratörer och klicka på [!UICONTROL **Spara**].

>[!ENDTABS]

## Lägg till användare

Följande instruktioner innehåller information om hur du lägger till användare i [!DNL Commerce Cloud Manager] och Commerce Admin. Med gränssnittet [!DNL Commerce Cloud Manager] kan du skapa och hantera dina Commerce-instanser. Den här processen krävs för alla användare, inklusive utvecklare och administratörer.

>[!NOTE]
>
>Endast produktadministratörer och systemadministratörer kan lägga till användare och utvecklare i Adobe Commerce as a Cloud Service.

>[!BEGINTABS]

>[!TAB GA (tillhandahålls efter 13 oktober 2025)]

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. Välj fliken [!UICONTROL **Produkter**].

1. Välj [!UICONTROL **Adobe Commerce**]-produkten.

1. Markera Commerce Cloud Manager-produkten om du vill lägga till användaren i molnhanterargränssnittet, där användaren kan skapa och hantera Commerce-instanser, eller markera den befintliga Commerce-instansen som användaren ska läggas till i. Commerce-instanser har följande format: `Adobe Commerce - <instance-name> - ACCS - <environment-type> - <tenant-id>`.

1. Välj fliken [!UICONTROL **Användare**] och klicka på [!UICONTROL **Lägg till användare**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till och klicka på [!UICONTROL **Spara**].

1. Välj önskad produktprofil.

1. Klicka på [!UICONTROL **Använd**].

1. Klicka på [!UICONTROL **Spara**].

>[!TAB Tidig åtkomst (tillhandahålls före 13 oktober 2025)]

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**] väljer du [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] under [!UICONTROL **Produkter och tjänster**].

   ![Adobe Commerce Cloud Manager-produkt i Admin Console](./assets/backend.png){width="600" zoomable="yes"}

1. Klicka på produktprofilen [!UICONTROL **Standard - Cloud Manager**].

1. Välj fliken [!UICONTROL **Användare**] och klicka på [!UICONTROL **Lägg till användare**].

   ![Valt på fliken Användare i Admin Console produktprofil](./assets/tab-select.png){width="600" zoomable="yes"}

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till och klicka på [!UICONTROL **Spara**].

>[!ENDTABS]

### Lägg till utvecklare och produktprofiladministratörer

Om du vill lägga till utvecklare och produktprofiladministratörer upprepar du processen [Lägg till användare](#add-users), men väljer fliken [!UICONTROL **Utvecklare**] eller [!UICONTROL **Administratörer**] i stället för fliken [!UICONTROL **Användare**] .

>[!NOTE]
>
>Produktprofiladministratörer har inte tillgång till Commerce Admin. Mer information finns i [Förstå roller](#understanding-roles).
>
>Tilldela utvecklare användarrollen innan du lägger till dem som utvecklare. Användarrollen krävs för grundläggande Commerce-behörigheter.

![Flikalternativen Utvecklare och Administratörer i Admin Console](./assets/tab-select.png){width="600" zoomable="yes"}

## Rollresurser

I följande lista beskrivs de resurser som standardroller har behörighet att komma åt i [!DNL Adobe Commerce] Admin. Om du vill redigera standardbehörigheterna för varje roll går du till [!UICONTROL **System**] > [!UICONTROL **Behörigheter**] > [!UICONTROL **Användarroller**] i Commerce Admin.

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

## Lägg till en användare i [!DNL AEM Assets] eller [!DNL Product Visuals]

Följande konfiguration krävs för [!DNL Adobe Experience Manager Assets]- och [!DNL Product Visuals powered by AEM Assets]-användare.

Om ditt konto har åtkomst till [[!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service) och du vill tillåta en användare att få åtkomst till de avancerade funktionerna i [[!DNL AEM Assets]](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview){target="_blank"} tillsammans med [!DNL Adobe Commerce as a Cloud Service], slutför du följande process:

>[!NOTE]
>
>Användare utan rätt behörighet för resurser kommer inte att kunna komma åt avancerade funktioner i [!DNL AEM Assets], till exempel [AI-bildgenerering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}, [genererade varianter](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"} och mer.

>[!TIP]
>
>Om du vill lägga till flera användare samtidigt kan du utföra en [massöverföring av en CSV](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
>Du kan också lägga till flera användare till en roll genom att skapa en [användargrupp](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Sedan kan du lägga till [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]-produkten i användargruppen.

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**], under [!UICONTROL **Produkter och tjänster**], väljer du produkten [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**].

   ![AEM Cloud Manager produktval i Admin Console](./assets/backend-aem.png){width="600" zoomable="yes"}

1. Välj fliken [!UICONTROL **Användare**].

1. Klicka på [!UICONTROL **Lägg till användare**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till.

1. Klicka på [!UICONTROL **Lägg till produkt**].

1. Välj följande produktprofiler som krävs för att integrera [!DNL AEM Assets] med Commerce:

   * Företagsägare - krävs för att skapa och hantera program.
   * Distributionshanteraren - Krävs för att distribuera kod från dina databaser till AEM.

   Om du lägger till en utvecklare som inte behöver åtkomst till Cloud Manager- eller Experience Manager-gränssnitten kan du i stället tilldela dem utvecklarrollen.

   >[!NOTE]
   >
   >Mer information om hur dessa behörigheter påverkar din åtkomst till [!DNL AEM Assets] finns i [Cloud Manager produktprofiler](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}.

1. Klicka på [!UICONTROL **Använd**].

1. Klicka på [!UICONTROL **Spara**].

Om du vill bekräfta att användaren har åtkomst klickar du på användarens namn för att öppna profilsidan. I avsnittet [!UICONTROL **Produkter**] ska det stå [!UICONTROL **Slutfört**] under produkten [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]. Det kan ta några sekunder efter att användaren har lagts till att se statusen uppdaterad för sin profil. Uppdatera sidan för att se den uppdaterade statusen.

![Användarprofil som visar status för slutförd produktåtkomst](./assets/product-access.png){width="600" zoomable="yes"}

## Gå till Experience Manager gränssnitt

När en användare har lagts till i [!DNL AEM Assets] kan de komma åt [!DNL Experience Manager]-gränssnittet genom att gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}.

1. Klicka på [!UICONTROL **Experience Manager**] i avsnittet [!UICONTROL **Snabbåtkomst**] eller klicka på [!UICONTROL **Visa alla**] om du inte ser [!UICONTROL **Experience Manager**]. Klicka sedan på [!UICONTROL **Cloud Manager**] eller navigera direkt till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}.

1. På sidan [!UICONTROL **Cloud Manager**] klickar du på [!UICONTROL **Lägg till program**] för att komma igång.

1. [Skapa ett nytt program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}.

1. [Skapa en ny miljö](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}.

1. När du har skapat miljön går du tillbaka till [Admin Console](https://adminconsole.adobe.com){target="_blank"} och väljer [!UICONTROL **Adobe Experience Manager as a Cloud Service**].

1. Nu bör du se nya produktprofiler. Markera som innehåller `- author -`. Exempel: `<environment-name> - author - <program-id> - <environment-id>`.

1. [Lägg till användare i produktprofilen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}.

* [Konfigurera [!DNL AEM Assets] för stöd av Commerce-metadata](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [Integrera [!DNL AEM Assets] med Commerce för resurssynkronisering](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)

{{aem-assets-instance-mapping}}

## Identitetshantering och konfiguration för enkel inloggning

{{ims-identity-and-sso-config}}

