---
title: Användarhantering
description: Lär dig hur du skapar och hanterar användare och tilldelar användarroller för  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 36a953d4fb0e1e14c7cb88a80f3b59d6fe8eb49e
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Användarhantering

Om du vill aktivera åtkomst till [!DNL Adobe Commerce Optimizer] lägger du till användare från [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} och ser till att de har åtkomst till Commerce-produkten.

Du kan tilldela användare till någon av följande roller:

- **Användare** - Användare har tillgång till användargränssnittet i [!DNL Adobe Commerce Optimizer] för att visa och hantera katalogvyer och försäljningsregler samt spåra prestandamått.

- [**Utvecklare**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} - Utvecklare har användarbehörigheter och åtkomst till Adobe Developer Console. Det innebär att de kan skapa projekt och konfigurera autentiseringsuppgifter för att använda utvecklarverktyg som [!DNL Adobe Commerce Optimizer] API:er och SDK:er tillsammans med Adobe utökningsverktyg som App Builder och API Mesh.

- **Admin** - Det finns tre olika typer av administratörsroller:
   - [Systemadministratörer](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - Systemadministratören har åtkomst till alla produkter och produktprofiler i organisationen via Adobe Admin Console.
   - [Produktadministratörer](#add-a-product-admin) - Produktadministratörer kan [hantera användare, roller och behörigheter för produkten](#add-users-and-admins) i [!DNL Adobe Admin Console].
   - [Administratörer för produktprofiler](#add-users-developers-and-product-profile-admins) - Administratörer för produktprofiler kan hantera användare för produkten i [!DNL Adobe Admin Console].

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

1. Klicka på **+** för att lägga till produkter.

1. Markera den befintliga Commerce Optimizer-instansen som administratören ska läggas till i. Commerce Optimizer-instanser har följande format: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Välj produktprofil.

1. Klicka på [!UICONTROL **Använd**].

1. Klicka på [!UICONTROL **Spara**].

>[!TAB Tidig åtkomst (tillhandahålls före 13 oktober 2025)]

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**] väljer du [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] under [!UICONTROL **Produkter och tjänster**].

   ![välj produkt](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Välj fliken [!UICONTROL **Administratörer**].

1. Klicka på [!UICONTROL **Lägg till administratör**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till som administratörer och klicka på [!UICONTROL **Spara**].

>[!ENDTABS]

## Lägg till användare

Följande instruktioner innehåller information om hur du lägger till användare i [!DNL Commerce Cloud Manager] och Commerce Optimizer. Med gränssnittet [!DNL Commerce Cloud Manager] kan du skapa och hantera dina Commerce Optimizer-instanser. Den här processen krävs för alla användare, inklusive utvecklare och administratörer.

>[!NOTE]
>
>Endast produktadministratörer och systemadministratörer kan lägga till användare och utvecklare i Adobe Commerce Optimizer-produkten.

>[!BEGINTABS]

>[!TAB GA (tillhandahålls efter 13 oktober 2025)]

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. Välj fliken [!UICONTROL **Produkter**].

1. Välj [!UICONTROL **Adobe Commerce**]-produkten.

1. Markera Commerce Cloud Manager-produkten om du vill lägga till användaren i molnhanterargränssnittet, där användaren kan skapa och hantera Commerce Optimizer-instanser, eller markera den befintliga Commerce Optimizer-instansen som användaren ska läggas till i. Commerce Optimizer-instanser har följande format: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Välj fliken [!UICONTROL **Användare**] och klicka på [!UICONTROL **Lägg till användare**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till och klicka på [!UICONTROL **Spara**].

1. Välj önskad produktprofil.

1. Klicka på [!UICONTROL **Använd**].

1. Klicka på [!UICONTROL **Spara**].

>[!TAB Tidig åtkomst (tillhandahålls före 13 oktober 2025)]

1. Navigera till <https://adminconsole.adobe.com> och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**] väljer du [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] under [!UICONTROL **Produkter och tjänster**].

   ![välj produkt](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. Klicka på produktprofilen [!UICONTROL **Standard - Cloud Manager**].

1. Välj fliken [!UICONTROL **Användare**] och klicka på [!UICONTROL **Lägg till användare**].

   ![tabbmarkera](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till och klicka på [!UICONTROL **Spara**].

>[!ENDTABS]

### Lägg till utvecklare och produktprofiladministratörer

Om du vill lägga till utvecklare och produktprofiladministratörer upprepar du processen [Lägg till användare](#add-users), men väljer fliken [!UICONTROL **Utvecklare**] eller [!UICONTROL **Administratörer**] i stället för fliken [!UICONTROL **Användare**] .

>[!NOTE]
>
>Tilldela utvecklare användarrollen innan du lägger till dem som utvecklare. Användarrollen krävs för grundläggande Commerce-behörigheter.

![tabbmarkera](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## Hantering av flera användare

Du kan lägga till flera användare effektivare med någon av följande metoder:

- Använd funktionen **Lägg till användare via CSV** i Adobe Admin Console för att utföra en [massöverföring via CSV](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Lägg till flera användare i en roll genom att skapa en [användargrupp](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Lägg sedan till [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] i användargruppen.

