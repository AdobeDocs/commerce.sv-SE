---
title: Kom igång
description: Lär dig hur du kommer igång med  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 15a708db9a9a31798877ea3a400d5a9f6f930bda
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# Kom igång

Den här guiden hjälper dig att konfigurera [!DNL Adobe Commerce Optimizer] från början till slut. Den här guiden täcker alla roller, men mer information om utvecklarspecifikt innehåll finns i [utvecklardokumentationen](https://developer.adobe.com/commerce/services/optimizer/).

## Förutsättningar

Kontrollera att du har:

- **Adobe Experience Cloud-konto** med [!DNL Adobe Commerce Optimizer] berättiganden
- **Organisationsadministratörsåtkomst** för att skapa instanser och hantera användare
- **GitHub-konto** för inläsning av exempeldata och butiksutveckling
- **Grundläggande förståelse** av e-handelsbegrepp

## Snabbstartsguide

Så här kör du [!DNL Adobe Commerce Optimizer]-miljön:

### Steg 1. Skapa en instans

1. Logga in på [Adobe Experience Cloud](https://experience.adobe.com/).
1. Navigera till **Commerce** > **Commerce Cloud Manager**.
1. Klicka på **Lägg till instans** > **Commerce Optimizer**.

   ![Skapa instans](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Konfigurera instansinställningar:
   - **Instansnamn**: Beskrivande namn (till exempel &quot;Min företagssandlåda&quot;)
   - **Beskrivning**: En kort beskrivning av syftet
   - **Miljötyp**: Börja med en **sandlådemiljö** för testning
   - **Region**: Välj önskad region

1. Klicka på **Lägg till instans**.

   Cloud Manager uppdaterar och inkluderar din nya instans. Mer information om hur du kommer åt och hanterar den finns i [Hantera en instans](#manage-instances).

>[!NOTE]
>
>Du kan bara skapa sandlådemiljöer i den nordamerikanska regionen. När en instans har skapats kan du inte ändra regionen.

### Steg 2. Konfigurera din miljö

När du har skapat instansen:

1. [Hantera din instans](#manage-instances) från Commerce Cloud Manager.
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
| **Hantera instanser** | Kontrollera status, uppdatera instansnamn och beskrivning och hämta nyckel-URL:er för program- och API-åtkomst | [Hantera instanser](#manage-instances) |
| **Konfigurera åtkomst** | Ställ in katalogvyer och principer | [Katalogvyer](./setup/catalog-view.md) |

### Utvecklaruppgifter

Utvecklarna hanterar teknisk implementering och dataintegrering, inklusive plattformsarkitekturuppgifter.

| Uppgift | Beskrivning | Länk |
|---|---|---|
| **Öppna Developer Console** | Skapa projekt och generera autentiseringsuppgifter | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Importera katalogdata** | Importera produktdata från befintliga system | [API för datainmatning](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) |
| **Konfigurera Storefront** | Konfigurera Edge Delivery Services store | [Inställningar för Storefront](./storefront.md) |

### Handläggaruppgifter

Handläggarna optimerar och personaliserar shoppingupplevelsen genom produktupptäckt och rekommendationer. De använder också kunddata och analyser för att fatta strategiska beslut om produktplacering, priser och kampanjer i butiken.

| Uppgift | Beskrivning | Länk |
|---|---|---|
| **Produktidentifiering** | Konfigurera sökning och filtrering | [Merchandising - översikt](./merchandising/overview.md) |
| **Rekommendationer** | Konfigurera AI-baserade produktrekommendationer | [Produktrekommendationer](./merchandising/recommendations/overview.md) |
| **Prestandaspårning** | Övervaka framgångsmått | [Resultatvärden](./manage-results/success-metrics.md) |

## Hantera instanser

Hantera instanser från Commerce Cloud Manager.

>[!NOTE]
>
>Alla Adobe Commerce Optimizer-användare har inte tillgång till Cloud Manager. Åtkomsten beror på vilken roll och vilka behörigheter som tilldelats användarkontot.

1. Logga in på [Adobe Experience Cloud](https://experience.adobe.com/).

1. Öppna Commerce Cloud Manager:

   - Klicka på **Commerce** under **Snabbåtkomst**.
   - Visa tillgängliga instanser.

### Söka efter och filtrera instanser

När du har loggat in visas alla Commerce produktinstanser som är tillgängliga i organisationen på kontrollpanelen.
Produktkolumnen anger vilket Commerce-program instansen är avsedd för.

![Instanssökning och filter](./assets/search-filter-instances.png){zoomable="yes"}

Använd verktygen Filter och Sök för att snabbt hitta specifika instanser per skapat datum, region, skapare, produkttyp, miljö eller status.

### Åtkomst till programmet [!DNL Adobe Commerce Optimizer]

När appen är öppen växlar du enkelt mellan miljöer som sandlådor och produktion för att visa data och inställningar för var och en utan att behöva gå tillbaka till Commerce Cloud Manager.

1. Öppna programmet [!DNL Adobe Commerce Optimizer] genom att klicka på instansnamnet i Commerce Cloud Manager.

1. Växla mellan [!DNL Adobe Commerce Optimizer] instanser utan att lämna programmet.

   I den nedrullningsbara listan visas alla Optimizer-instanser som är tillgängliga i organisationen. Markera instansen som ska visas.

   ![Instansväxlare](./assets/context-switcher.png){zoomable="yes"}

### Hämta instansinformation

Visa instansinformationen genom att klicka på informationsikonen bredvid instansnamnet.

![Instansinformation](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

Observera följande viktiga information:

- **GraphQL-slutpunkt** om du vill hämta Commerce-katalogdata med API:t för marknadsföring
- **Katalogtjänstslutpunkt** för datainmatning med REST API
- **Commerce Optimizer URL** för att komma åt programmet [!DNL Adobe Commerce Optimizer]
- **Instans-ID** är det unika klient-ID som identifierar instansen

Om du är utvecklare behöver du dessa uppgifter för att konfigurera utvecklingsmiljön och ansluta till [!DNL Adobe Commerce Optimizer] API:er.

>[!NOTE]
>
>Du måste ha nödvändig behörighet i din Adobe IMS-organisation för att få tillgång till instansinformationen. Om du inte ser instansinformationen eller inte kan komma åt programmet kontaktar du organisationens administratör.

### Redigera instansnamn och beskrivning

Uppdatera instansnamnet och beskrivningen efter behov.

1. Klicka på ikonen **Redigera** bredvid ett instansnamn.
1. Uppdatera **instansnamnet** och **beskrivningen** efter behov.
1. Klicka på **Spara**.

## Lägg till exempeldata

Adobe tillhandahåller en GitHub-databas med exempeldata och verktyg som hjälper dig att lära dig och testa [!DNL Adobe Commerce Optimizer]-funktioner.
Exempeldata baseras på [Carvelo-affärsscenariot](./use-case/admin-use-case.md) och innehåller:

- Produktkatalog med fordonsdelar
- Flera prislistor och prissättningsscenarier
- Katalogvyer och policyer för olika återförsäljare
- Komplett arbetsflödesexempel från början till slut

**Läs in exempeldata:**

1. Åtkomst till GitHub-databasen [Sample Catalog Data Inghit](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion).

1. Följ instruktionerna i databasens README-fil för att utföra följande åtgärder:

   - Konfigurera din miljö
   - Slutför dataöverföringsprocessen
   - Skapa katalogvyer och principer med exempeldata
   - Verifiera datainmatningen genom att kontrollera katalogtjänstdata på sidan [Datasynkronisering](./setup/data-sync.md)

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

- **Resurser för utvecklare**: [Dokumentation för utvecklare](https://developer.adobe.com/commerce/services/optimizer/)
- **Storefront Resources**: [Commerce storefront-dokumentation](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE)
- **Självstudiekurser**: [Commerce Optimizer självstudiekurser](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)
- **Support**: [Adobe Commerce supportresurser](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/overview)
