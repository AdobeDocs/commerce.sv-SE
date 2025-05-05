---
title: Komma igång med  [!DNL Adobe Commerce as a Cloud Service]
description: Lär dig hur du kommer igång med  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
source-git-commit: 9b90e6f79a394ec0941c9e48aee3859f0bcdedd5
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Komma igång

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] tillhandahåller de flesta konfigurationer som finns i paketet. När du har slutfört några grundläggande installationsprocesser kommer din butik att vara igång på nolltid. Den här guiden hjälper dig att skapa och arbeta med en instans.

Klicka på flikarna nedan om du vill se arbetsflödesöversikter på hög nivå för följande användartyper:

* Administratörer
* Merchants
* Utvecklare

>[!BEGINTABS]

>[!TAB Administratörs- och säljarbetsflöde]

Bilden ger en översikt på hög nivå över hur administratörer och handlare får åtkomst till och hanterar [!DNL Adobe Commerce as a Cloud Service] instanser. Mer information om administratörsarbetsflöden finns i [Adobe Admin Console-handboken](https://helpx.adobe.com/se/enterprise/admin-guide.html).

![[!DNL Adobe Commerce as a Cloud Service] handelsflödesdiagram](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Arbetsflöde för utvecklare]

I det här diagrammet ges en översikt på hög nivå över hur utvecklare skapar integreringar för [!DNL Adobe Commerce as a Cloud Service] med App Builder. Mer information finns i [API-dokumentationen](https://developer.adobe.com/commerce/services/cloud/).

![[!DNL Adobe Commerce as a Cloud Service] utvecklarflödesdiagram](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## Skapa en instans

>[!NOTE]
>
>Innan du kan skapa en instans måste din organisations produktadministratör eller systemadministratör lägga till dig som användare av produkten [!DNL Adobe Commerce as a Cloud Service]. Mer information finns i [Lägg till användare och administratörer](./user-management.md#add-users-and-admins).

[!DNL Adobe Commerce as a Cloud Service] instanser använder ett kreditbaserat system. Du kan skapa flera instanser, men varje instans kräver en relativ mängd krediter. Hur många krediter du har från början beror på prenumerationen.

1. Logga in på ditt [Adobe Experience Cloud](https://experience.adobe.com/)-konto.

1. Under [!UICONTROL Quick access] klickar du på [!UICONTROL **Commerce**] för att öppna [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visar en lista med [!DNL Adobe Commerce as a Cloud Service] instanser som är tillgängliga i din Adobe IMS-organisation.

1. Klicka på [!UICONTROL **Lägg till instans**] i skärmens övre högra hörn.

   ![Skapa instans](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Välj [!UICONTROL **Commerce as a Cloud Service**].

1. Ange ett **namn** och **beskrivning** för din instans.

1. Markera regionen där du vill att instansen ska vara värd.

   >[!NOTE]
   >
   >När du har skapat instansen kan du inte ändra regionen.

1. Välj [!UICONTROL **miljötyp**] för din instans. Du kan välja mellan följande alternativ:

   * [!UICONTROL **Sandbox**] - Perfekt för design- och testningsändamål. Du bör påbörja din [!DNL Adobe Commerce as a Cloud Service]-resa med sandlådemiljön.
   * [!UICONTROL **Produktion**] - För livebutiker och kundorienterade webbplatser.

   >[!NOTE]
   >
   >Sandlådeinstanser är för närvarande begränsade till Nordamerika.

1. _(Valfritt)_ Om du vill inkludera exempelproduktdata för testnings- och utbildningsändamål väljer du [!UICONTROL **Adobe Store**] i listrutan [!UICONTROL **Testdata**].

   Du kan hoppa över det här alternativet, men din butik har inga produkter om du gör det. Du måste [importera katalogen](#import-your-catalog) för att kunna se den fullständiga butiksupplevelsen.

1. Klicka på [!UICONTROL **Lägg till instans**].

## Åtkomst till en instans

När du har skapat en instans kan du komma åt den från [!UICONTROL Commerce Cloud Manager].

1. Logga in på ditt [Adobe Experience Cloud](https://experience.adobe.com/)-konto.

1. Under [!UICONTROL Quick access] klickar du på [!UICONTROL **Commerce**] för att öppna [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visar en lista med instanser som är tillgängliga i din Adobe IMS-organisation.

1. Om du vill öppna [!UICONTROL Commerce Admin] för en instans klickar du på instansnamnet.

>[!TIP]
>
>Om du vill visa information om instansen, inklusive REST- och GraphQL-slutpunkterna och Admin-URL:en, klickar du på informationsikonen bredvid instansnamnet.

## Importera katalogen

Som standard innehåller [!DNL Adobe Commerce as a Cloud Service] instanser inga produktdata. Du kan välja att ta med exempelproduktdata när du skapar en instans i testnings- och utbildningssyfte innan du importerar din egen katalog.

Det finns två sätt att importera katalogen till [!DNL Adobe Commerce as a Cloud Service]:

* [**Commerce Admin**](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/data-transfer/import/data-import) - Ett användarvänligt gränssnitt där du kan importera katalogdata med bara några klick.
* [**Importera JSON API**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - ett REST API som gör att du kan importera katalogdata programmatiskt.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## Konfigurera butiken

Nu när du har skapat en instans är du redo att fortsätta [konfigurera](storefront.md) din Commerce Storefront med Edge Delivery Services.
