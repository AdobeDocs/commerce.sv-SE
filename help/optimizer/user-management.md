---
title: Användarhantering
description: Lär dig hantera användare i  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 02758aa5cc14af6d46bfc4bb7865fa37a787d4cb
workflow-type: tm+mt
source-wordcount: '458'
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

1. Navigera till [Admin Console](https://adminconsole.adobe.com) och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**], under [!UICONTROL **Produkter och tjänster**], väljer du [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**] .

   ![välj produkt](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Välj fliken [!UICONTROL **Administratörer**].

1. Klicka på [!UICONTROL **Lägg till administratör**].

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till som administratörer och klicka på [!UICONTROL **Spara**].

## Lägga till användare, utvecklare och produktprofiladministratörer

>[!BEGINSHADEBOX &quot;Förutsättningar&quot;]
>
>Följande etablering krävs för användarhantering:

- IMS-organisation har etablerats för [!DNL Adobe Commerce Optimizer]
- Ett Adobe Experience Cloud-konto i samma IMS-organisation med system- eller produktadministratörsroll

>[!ENDSHADEBOX]

Följ de här instruktionerna för att lägga till användare och utvecklare i [!DNL Commerce Cloud Manager], där du hanterar dina Commerce-instanser.

1. Navigera till [Adobe Admin Console](https://adminconsole.adobe.com) och logga in med din Adobe ID.

1. Välj organisation.

1. På fliken [!UICONTROL **Produkter**], under [!UICONTROL **Produkter och tjänster**], väljer du [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**] .

   ![välj produkt](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Klicka på produktprofilen [!UICONTROL **Standard - Cloud Manager**].

1. Välj fliken [!UICONTROL **Användare**], [!UICONTROL **Utvecklare**] eller [!UICONTROL **Administratörer**] och klicka på [!UICONTROL **Lägg till användare**] eller [!UICONTROL **Lägg till utvecklare**] eller [!UICONTROL **Lägg till administratörer**].

   Administratörer som läggs till från den här skärmen tilldelas gruppen [produktprofiladministratörer](#understanding-roles).

   ![tabbmarkera](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Ange användarnamn eller e-postadress för de användare som du vill lägga till som administratörer och klicka på [!UICONTROL **Spara**].

## Hantering av flera användare

Du kan lägga till flera användare effektivare med någon av följande metoder:

- Använd funktionen **Lägg till användare via CSV** i Adobe Admin Console för att utföra en [massöverföring via CSV](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Lägg till flera användare i en roll genom att skapa en [användargrupp](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Lägg sedan till [!UICONTROL **Adobe Commerce as a Cloud Service - serverdel**] i användargruppen.

