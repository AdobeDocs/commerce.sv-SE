---
title: Kom igång
description: Lär dig hur du kommer igång med  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Kom igång

I den här artikeln får du lära dig hur du kommer igång med [!DNL Adobe Commerce Optimizer]. Den här guiden fokuserar på handlares och administratörers roller, men innehåller även kortfattade uppgifter på hög nivå som en utvecklare skulle utföra. Mer information om utvecklarspecifikt innehåll finns i [utvecklardokumentationen](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

## Vilken är din roll?

[!DNL Adobe Commerce Optimizer] har konfigurerats och omfattar vanligtvis följande teammedlemmar:

- Administratör
- Utvecklare
- Merchandiser

Varje teammedlem har sina egna roller och ansvarsområden enligt följande tabell:

| Roll(er) | Uppgift |
|---|---|
| Administratör | Använd Admin Console för att skapa &#x200B;, användargrupper, användare och utvecklare. |
|  | Skapa en ny [!DNL Adobe Commerce Optimizer]-instans i Commerce Cloud Manager. &#x200B; |
|  | Konfigurera principer och katalogvyer. |
| Utvecklare | Använd Developer Console för att skapa ett projekt, ge utvecklare API-åtkomst och installera nödvändiga program och anpassningar. |
|  | Anslut till ditt back office-system (kundvagn, utcheckning) med API Mesh och App Builder &#x200B;. |
|  | Infoga katalogdata från dina befintliga e-handelslösningar med API-&#x200B; för Merchandising Services-datainmatning |
|  | Konfigurera din butik |
| Merchandiser | Ställ in &#x200B; för produktupptäckt. |
|  | Ställ in produktrekommendationer. |

Varje roll spelar en viktig roll för att du ska kunna komma igång med och starta din [!DNL Adobe Commerce Optimizer]-miljö. I följande diagram visas ett arbetsflöde från början till slut för varje roll i organisationen:

![Arbetsflöde på hög nivå](./assets/high-level-workflow.png){zoomable="yes"}

### Administratör

Administratörer ansvarar för att konfigurera instanser, hantera användare, grupper och berättiganden för din organisation.

- **[Få tillgång till Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html)** - Hantera Adobe-berättiganden i hela organisationen. Mer information om hur du eller organisationens produktadministratör eller systemadministratör kan lägga till användare i produkten [!DNL Adobe Commerce Optimizer] finns i [användarhantering](./user-management.md).

- **Skapa en instans** - [!DNL Adobe Commerce Optimizer] instanser använder ett kreditbaserat system. Du kan skapa flera sandbox- och Production-instanser där varje instans kräver en motsvarande kredit. Hur många krediter du har från början beror på prenumerationen. [Läs mer](#create-an-instance).

- **Åtkomst till en instans** - När du har skapat en instans kan du komma åt den från [!UICONTROL Commerce Cloud Manager]. [Läs mer](#access-an-instance).

- **Konfigurera katalogvyer och principer** - Lär dig hur du [definierar katalogvyer och principer](./setup/catalog-view.md). Katalogen innehåller inte bara dina produktdata, utan även din affärsstruktur.

### Utvecklare

Utvecklare skapar projekt och autentiseringsuppgifter, installerar tillägg, importerar katalogdata och utför allmänna plattformsarkitekturuppgifter. Mer information om utvecklarspecifikt innehåll finns i [utvecklardokumentationen](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

- **Använd Developer Console** - Använd [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) för att skapa ett projekt för [!DNL Adobe Commerce Optimizer], generera åtkomsttoken och installera nödvändiga program och anpassningar.

- **Ingest catalog data** - Läs [API:t för datainhämtning](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) om du vill veta hur du kan importera katalogdata till [!DNL Adobe Commerce Optimizer].

  Katalogdata som är inkapslade visas på sidan [datasynkronisering](./setup/data-sync.md).

- **Konfigurera butiken** - Innan du ställer in butiken måste du först skapa en instans, vilket är en uppgift som vanligtvis utförs av organisationens [administratör](#administrator). När din instans har skapats är du redo att fortsätta [konfigurera](./storefront.md) din Commerce Storefront med Edge Delivery Services.

### Merchandiser

Försäljaren använder kunddata och analyser för att fatta strategiska beslut om produktplacering, priser och kampanjer i butiken, samtidigt som man optimerar shoppingupplevelserna genom produktupptäckt och rekommendationer.

- **Konfigurera produktidentifiering och rekommendationer** - Lär dig hur du [skapar personaliserade upplevelser](./merchandising/overview.md) för dina kunder genom produktupptäckt och rekommendationer.

## Skapa en instans

1. Logga in på ditt [Adobe Experience Cloud](https://experience.adobe.com/)-konto.

1. Under [!UICONTROL Quick access] klickar du på [!UICONTROL **Commerce**] för att öppna [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visar en lista med [!DNL Adobe Commerce] instanser som är tillgängliga i din Adobe IMS-organisation, inklusive båda instanser som har etablerats för [!DNL Adobe Commerce Optimizer] och [!DNL Adobe Commerce as a Cloud Service].

1. Klicka på [!UICONTROL **Lägg till instans**] i skärmens övre högra hörn.

   ![Skapa instans](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. Välj [!UICONTROL **Commerce Optimizer**].

1. Ange ett **namn** och **beskrivning** för din instans.

1. Markera regionen där du vill att instansen ska vara värd.

   >[!NOTE]
   >
   >När du har skapat en instans kan du inte ändra regionen.

1. Välj en av följande [!UICONTROL **miljötyper**] för din instans:

   - [!UICONTROL **Sandbox**] - Perfekt för design- och testningsändamål. Du bör påbörja din [!DNL Adobe Commerce Optimizer]-resa med sandlådemiljön.
   - [!UICONTROL **Produktion**] - För livebutiker och kundorienterade webbplatser.

   >[!NOTE]
   >
   >Sandlådeinstanser är för närvarande begränsade till Nordamerika.

1. Klicka på [!UICONTROL **Lägg till instans**].

   Den nya instansen är nu tillgänglig i Cloud Manager.

1. Om du vill visa instansinformation - inklusive slutpunkterna för GraphQL- och katalogtjänsten, URL:en för åtkomst till Adobe Commerce Optimizer-programmet och instans-ID:t (klientorganisations-ID) - klickar du på informationsikonen bredvid instansnamnet.

   ![Skapa instans](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## Åtkomst till en instans

1. Logga in på ditt [Adobe Experience Cloud](https://experience.adobe.com/)-konto.

1. Under [!UICONTROL Quick access] klickar du på [!UICONTROL **Commerce**] för att öppna [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visar en lista med instanser som är tillgängliga i din Adobe IMS-organisation.

1. Klicka på instansnamnet för att öppna programmet [!UICONTROL Commerce Optimizer] som är associerat med en instans.


