---
title: Kom igång
description: Lär dig hur du kommer igång med  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: f920cfe7cd433e85f343fefe1062a1972e5e5e5f
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Kom igång

Den här guiden hjälper dig att konfigurera [!DNL Adobe Commerce Optimizer] från början till slut. Den här guiden täcker alla roller, men mer information om utvecklarspecifikt innehåll finns i [utvecklardokumentationen](https://developer.adobe.com/commerce/services/optimizer/).

## Förutsättningar

Kontrollera att du har:

- **Adobe Experience Cloud-konto** med [!DNL Adobe Commerce Optimizer] berättiganden
- **Organisationsadministratörsåtkomst** för att skapa instanser och hantera användare
- **GitHub-konto** (för inläsning av exempeldata och utveckling av butiker)
- **Grundläggande förståelse** av e-handelsbegrepp

## Snabbstartsguide

Så här kör du [!DNL Adobe Commerce Optimizer]-miljön:

### Steg 1. Skapa en instans

1. Logga in på [Adobe Experience Cloud](https://experience.adobe.com/).
1. Navigera till **Commerce** > **Commerce Cloud Manager**.
1. Klicka på **Lägg till instans** > **Commerce Optimizer**.

   ![Skapa instans](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Konfigurera instansinställningar:
   - **Namn**: Beskrivande namn (till exempel &quot;Min företagssandlåda&quot;)
   - **Beskrivning**: En kort beskrivning av syftet
   - **Region**: Välj önskad region
   - **Miljötyp**: Börja med en **sandlådemiljö** för testning

1. Klicka på **Lägg till instans**.

   Cloud Manager uppdaterar och inkluderar din nya instans. Mer information om hur du kommer åt och hanterar den finns i [Hantera en instans](#manage-an-instance).

>[!NOTE]
>
>Sandlådeinstanser är begränsade till Nordamerika. Du kan inte ändra regionen efter att den har skapats.

### Steg 2. Konfigurera din miljö

När du har skapat instansen:

1. [Hantera din instans](#manage-an-instance) från Commerce Cloud Manager.
1. Konfigurera användaråtkomst med hjälp av [handboken för användarhantering](./user-management.md).

### Steg 3. Lägg till exempeldata (valfritt)

Följ instruktionerna för [Läs in exempeldata](#add-sample-data) om du vill testa och lära dig mer.

## Rollbaserade arbetsflöden

Installationen och hanteringen av [!DNL Adobe Commerce Optimizer] bygger på tre nyckelroller. Varje roll har specifika uppgifter och ansvarsområden:

![Arbetsflöde på hög nivå](./assets/high-level-workflow.png){zoomable="yes"}

### Administratörsuppgifter

Administratörer hanterar instanser, användare och organisationsinställningar.

| Uppgift | Beskrivning | Länk |
|---|---|---|
| **Hantera användare** | Lägga till användare, utvecklare och administratörer | [Användarhantering](./user-management.md) |
| **Skapa instanser** | Konfigurera sandbox- och produktionsmiljöer | [Skapa instans](#create-an-instance) |
| **Konfigurera åtkomst** | Ställ in katalogvyer och principer | [Katalogvyer](./setup/catalog-view.md) |

### Utvecklaruppgifter

Utvecklarna hanterar teknisk implementering och dataintegrering, inklusive plattformsarkitekturuppgifter.

| Uppgift | Beskrivning | Länk |
|---|---|---|
| **Öppna Developer Console** | Skapa projekt och generera autentiseringsuppgifter | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Importera katalogdata** | Importera produktdata från befintliga system | [API för datainmatning](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) |
| **Konfigurera Storefront** | Konfigurera Edge Delivery Services store | [Inställningar för Storefront](./storefront.md) |

### Handläggaruppgifter

Handläggarna optimerar och personaliserar shoppingupplevelsen genom produktupptäckt och rekommendationer. De använder också kunddata och analyser för att fatta strategiska beslut om produktplacering, priser och kampanjer i butiken.

| Uppgift | Beskrivning | Länk |
|---|---|---|
| **Produktidentifiering** | Konfigurera sökning och filtrering | [Merchandising - översikt](./merchandising/overview.md) |
| **Rekommendationer** | Konfigurera AI-baserade produktrekommendationer | [Produktrekommendationer](./merchandising/recommendations/overview.md) |
| **Prestandaspårning** | Övervaka framgångsmått | [Resultatvärden](./manage-results/success-metrics.md) |

## Hantera en instans

1. Logga in på [Adobe Experience Cloud](https://experience.adobe.com/).

1. Öppna Commerce Cloud Manager:
   - Klicka på **Commerce** under **Snabbåtkomst**.
   - Visa tillgängliga instanser.

1. Få åtkomst till din instans:

   Klicka på instansnamnet för att öppna programmet [!DNL Adobe Commerce Optimizer]. I programmet kan du växla mellan olika [!DNL Adobe Commerce Optimizer] instanser med hjälp av listrutan högst upp på sidan:

   ![Instansväxlare](./assets/context-switcher.png){zoomable="yes"}

   Alla förekomster som visas tillhör samma organisation. Du kan växla mellan instanser för att visa data och inställningar för var och en av dem, till exempel mellan sandlådor och produktionsmiljöer.

1. Hämta instansinformation:
   - Klicka på informationsikonen bredvid instansnamnet.
   - Observera GraphQL-slutpunkten, katalogtjänstslutpunkten för datainmatning och instans-ID (kallas även `tenant ID`).

   ![Instansinformation](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

   Information om slutpunkt och instans-ID (tenant-ID) krävs för integrering med klientprogram och backend-system. URL:en för åtkomst till programmet [!DNL Adobe Commerce Optimizer] anges också här.

   Alla Adobe Commerce Optimizer-användare har inte tillgång till Cloud Manager och instansinformationen. Åtkomsten beror på vilken roll och vilka behörigheter som tilldelats användarkontot. Om du inte har åtkomst kontaktar du organisationens administratör för att få information om instansen.

1. Redigera instansnamn och beskrivning:
   - Klicka på ikonen **Redigera** bredvid ett instansnamn.
   - Uppdatera namn och beskrivning efter behov.
   - Klicka på **Spara**.

   Du kan också använda sök- och filteralternativen för att snabbt hitta specifika instanser.

## Lägg till exempeldata

Adobe tillhandahåller en GitHub-databas med exempeldata och verktyg som hjälper dig att lära dig och testa [!DNL Adobe Commerce Optimizer]-funktioner.
Exempeldata baseras på [Carvelo-affärsscenariot](./use-case/admin-use-case.md) och innehåller:

- Produktkatalog med fordonsdelar
- Flera prislistor och prissättningsscenarier
- Katalogvyer och policyer för olika återförsäljare
- Komplett arbetsflödesexempel från början till slut

**Läs in exempeldata:**

1. Gå till GitHub-databasen:
   - Besök [databasen för datainmatning i exempelkatalog](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion)

1. Följ instruktionerna i databasens README-fil.

   - Konfigurera och kör datainmatningen
   - Konfigurera katalogprinciper och vyer med exempeldata
   - Rensa exempeldata (valfritt)

## Nästa steg

När installationen är klar:

1. Konfigurera din butik:
   - Konfigurera [Edge Delivery Services storefront](./storefront.md)
   - Anslut till katalogdata

1. Se Carvelos exempel:
   - Följ arbetsflödet [från början till slut](./use-case/admin-use-case.md)
   - Öva med verkliga scenarier

1. Konfigurera marknadsföring:
   - Konfigurera [produktidentifiering](./merchandising/overview.md)
   - Skapa [rekommendationer](./merchandising/recommendations/overview.md)

1. Bildskärmsprestanda:
   - Spåra [framgångsmått](./manage-results/success-metrics.md)
   - Analysera [sökprestanda](./manage-results/search-performance.md)

## Felsökning

### Vanliga problem

| Problem | Lösning |
|---|---|
| **Kan inte skapa en instans** | Kontrollera att du har [!DNL Adobe Commerce Optimizer] berättiganden och administratörsbehörigheter. |
| **Instansen visas inte** | Kontrollera din Adobe IMS-organisation och uppdatera sidan. |
| **Det går inte att komma åt instansen** | Se till att du läggs till som användare i Admin Console. |
| **Exempeldata läses inte in** | Verifiera dina instansreferenser och API-slutpunkter. |

### Få hjälp

- **Resurser för utvecklare**: [Dokumentation för utvecklare](https://developer-stage.adobe.com/commerce/services/composable-catalog/)
- **Storefront-resurser**: [Commerce Storefront Documentation](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE)
- **Support**: [Adobe Commerce supportresurser](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/overview)
