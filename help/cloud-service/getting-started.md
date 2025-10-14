---
title: Komma igång med  [!DNL Adobe Commerce as a Cloud Service]
description: Lär dig hur du kommer igång med  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 911d984efa9587c0154db3ab97f6136bf6c34166
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 0%

---

# Komma igång

[!DNL Adobe Commerce as a Cloud Service] tillhandahåller de flesta konfigurationer som finns i paketet. När du har slutfört några grundläggande installationsprocesser kommer din butik att vara igång på nolltid. Den här guiden hjälper dig att skapa och arbeta med en instans. Den här guiden hjälper dig även att konfigurera din organisation för att lyckas genom att se till att dina team har korrekt åtkomst till [!DNL Adobe Commerce as a Cloud Service] och de verktyg du behöver för att komma igång.

[!DNL Adobe Commerce as a Cloud Service] är en molnbaserad handelsplattform som ger flexibilitet, skalbarhet och effektivitet för att leverera digitala handelsupplevelser. Det här SaaS-erbjudandet är en helt hanterad, versionslös plattform som ger en sömlös uppgradering utan att man behöver göra något manuellt.

## Viktiga komponenter

[!DNL Adobe Commerce as a Cloud Service] består av följande komponenter:

* **[Adobe Experience Cloud](https://experience.adobe.com/)** - Din centrala startpunkt pekar på alla [!DNL Adobe Commerce] produkter på [experience.adobe.com](https://experience.adobe.com/)
   * Klicka på [!UICONTROL **Commerce**] under [!UICONTROL **Snabbåtkomst**] för att öppna Commerce Cloud Manager
* **[Commerce Cloud Manager](https://experience.adobe.com/#/commerce/cloud-service)** - Skapa och hantera instanser, få åtkomst till API:er och Commerce Admin
* **[Adobe Admin Console](https://adminconsole.adobe.com/)** - Hantera användare och roller
* **Commerce Admin** - Hantera produkter, beställningar, kunder och butikskonfiguration
* **[Storefront från Edge Delivery Services](./storefront.md)** - Skapa och anpassa en kundriktad butik med ett sammanställbart, högpresterande system som levererar exceptionell hastighet, SEO och användarupplevelse för handlare och utvecklare
* **[Adobe Developer App Builder](https://developer.adobe.com/app-builder/)** - Skapa anpassade integreringar med App Builder, tillsammans med andra utökningsverktyg som [startsatsen för integrering](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) och [API-nät](https://developer.adobe.com/graphql-mesh-gateway/)

## Installation och hantering

Som en del av konfigurationsprocessen för [!DNL Adobe Commerce as a Cloud Service] konfigurerar din systemadministratör, handlare och utvecklare åtkomst och resurser för din organisation, inklusive tilldelning av molnresurser och tilldelning av användare till lämpliga roller baserat på deras ansvarsområden.

### Arbetsflöde för konfiguration och hantering

Som en kombinerad grupp måste systemadministratören, handlaren och utvecklaren följa de här stegen för att få igång Commerce-instansen:

1. **Alla användare**: [Skapa en instans](#create-an-instance)
1. **Systemadministratör**: [Lägg till användare och tilldela roller](user-management.md#add-users-and-admins)
1. **Handlare**: [Öppna Commerce Admin](#access-an-instance) och [importera katalogen](#import-your-catalog)
1. **Utvecklare**: [Konfigurera din butik](storefront.md) och utforska [utvecklarplattformen](overview.md#developer-platform)

#### Arbetsflöde för AEM Assets och produktvisuella

Följande steg krävs för att integrera [!DNL Adobe Experience Manager Assets] eller [!DNL Product Visuals powered by AEM Assets] med [!DNL Adobe Commerce as a Cloud Service]:

1. **Systemadministratör**: [Lägg till användare i produktprofilen AEM Assets och produktbilder](user-management.md#add-a-user-to-aem-assets-or-product-visuals)
1. **Utvecklare**: [Integrera AEM Assets och produktbilder](../aem-assets-integration/overview.md)
1. **Handlare**: [Få tillgång till dina AEM Assets- och produktbilder](./user-management.md#access-the-experience-manager-interface)

### Rollbaserade installations- och hanteringsuppgifter

Välj en flik nedan om du vill visa arbetsflödesgrafik på hög nivå för motsvarande roll:

>[!BEGINTABS]

>[!TAB Systemadministratör och handlararbetsflöde]

Bilden ger en översikt på hög nivå över hur systemadministratörer och handlare får åtkomst till och hanterar [!DNL Adobe Commerce as a Cloud Service] instanser. Mer information om administratörsarbetsflöden finns i [Adobe Admin Console-handboken](https://helpx.adobe.com/enterprise/admin-guide.html).

![[!DNL Adobe Commerce as a Cloud Service] handelsflödesdiagram](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Arbetsflöde för utvecklare]

I det här diagrammet ges en översikt på hög nivå över hur utvecklare skapar integreringar för [!DNL Adobe Commerce as a Cloud Service] med App Builder. Mer information finns i [API-dokumentationen](https://developer.adobe.com/commerce/webapi/rest/).

![[!DNL Adobe Commerce as a Cloud Service] utvecklarflödesdiagram](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

Välj din roll för att hitta resurser som ska komma igång med installationsprocessen:

>[!BEGINTABS]

>[!TAB Systemadministratör]

Som systemadministratör ansvarar du för att konfigurera organisationen och hantera användaråtkomst.

| Uppgift | Beskrivning | Resurs |
|------|-------------|----------|
| Förstå plattformen | Läs om Adobe Commerce as a Cloud Service-arkitektur och fördelar | [Översikt](overview.md) |
| Jämför funktioner | Förstå skillnaderna mellan Cloud Service och andra Adobe Commerce-erbjudanden | [Funktionsjämförelse](feature-comparison.md) |
| Skapa en instans | Etablera sandlådor och produktionsmiljöer | [Skapa en instans](#create-an-instance) |
| Ställ in användarhantering | Lägga till användare, tilldela roller och hantera behörigheter | [Användarhantering](user-management.md) |
| Konfigurera AEM Assets och produktvisuella effekter (valfritt) | Lägga till användare, tilldela roller och hantera behörigheter | [Användarhantering](user-management.md#add-a-user-to-aem-assets-or-product-visuals) |

>[!TAB Merchant]

Som handlare fokuserar du på att hantera produkter, beställningar och butiksinnehåll.

| Uppgift | Beskrivning | Resurs |
|------|-------------|----------|
| Åtkomst till din instans | Logga in på Commerce Admin för att hantera din butik | [Åtkomst till en instans](#access-an-instance) |
| Utforska användningsexempel | Lär dig praktiska affärsscenarier och arbetsflöden | [Användningsexempel](./use-cases.md) |
| Importera katalog | Läs om hur du importerar produktdata till plattformen | [Importera katalogen](#import-your-catalog) |
| Få åtkomst till AEM Assets och produktbilder (tillval) | Använd Experience Manager för att börja använda AEM Assets och produktvisualer | [Använd Experience Manager-gränssnittet](./user-management.md#access-the-experience-manager-interface) |

>[!TAB Utvecklare]

Som utvecklare måste ni veta hur ni bygger anpassade integreringar och utökar plattformsfunktionaliteten.

| Uppgift | Beskrivning | Resurs |
|------|-------------|----------|
| Förstå arkitekturen | Läs mer om plattformens utbyggbarhet och API:er | [Översikt - plattform för utvecklare](overview.md#developer-platform) |
| Konfigurera en utvecklingsmiljö | Skapa en sandlådeinstans för utveckling och testning | [Skapa en instans](#create-an-instance) |
| Bygg storefront | Lär dig konfigurera och anpassa Commerce Storefront | [Inställningar för Storefront](./storefront.md) |
| Konfigurera din butik | Läs om hur du konfigurerar din butik | [Inställningar för Storefront](./storefront.md) |
| Utforska integreringsalternativ | Läs om App Builder, API Mesh och andra utökningsverktyg som du har tillgång till | [Översikt - plattform för utvecklare](overview.md#developer-platform) |
| Integrera AEM Assets och produktbilder (tillval) | Lär dig hur du integrerar AEM Assets- och produktvisuella effekter med Adobe Commerce | [Integrering med AEM Assets](../aem-assets-integration/overview.md) |

>[!ENDTABS]

### Nästa steg

När du har slutfört dina rollspecifika konfigurationsuppgifter:

* **Systemadministratörer**: Granska [riktlinjerna för delat ansvar](shared-responsibility.md)
* **Affärskommunikation**: Utforska [användningsfall](use-cases.md) för vanliga affärsscenarier
* **Utvecklare**: Läs [dokumentationen för Adobe Commerce-utvecklare](https://developer.adobe.com/commerce/docs)

## Grundläggande om Adobe Commerce as a Cloud Service

I följande avsnitt beskrivs de grundläggande processer du behöver utföra för att din Commerce-instans ska komma igång.

### Skapa en instans

>[!NOTE]
>
>Innan du kan skapa en instans måste din organisations produktadministratör eller systemadministratör lägga till dig som användare av produkten [!DNL Adobe Commerce as a Cloud Service]. Mer information finns i [Lägg till användare och administratörer](./user-management.md#add-users-and-admins).

[!DNL Adobe Commerce as a Cloud Service] instanser använder ett kreditbaserat system. Du kan skapa flera instanser, men varje instans kräver tillgängliga krediter. Hur många krediter du har från början beror på prenumerationen.

1. Logga in på ditt [Adobe Experience Cloud](https://experience.adobe.com/)-konto.

1. Under [!UICONTROL Quick access] klickar du på [!UICONTROL **Commerce**] för att öppna [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visar en lista med [!DNL Adobe Commerce as a Cloud Service] instanser som är tillgängliga i din Adobe IMS-organisation.

1. Klicka på [!UICONTROL **Lägg till instans**] i skärmens övre högra hörn.

   ![Skapa instans](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Välj [!UICONTROL **Commerce as a Cloud Service**].

1. Ange ett **namn** och **beskrivning** för din instans.

1. Välj [!UICONTROL **miljötyp**] för din instans. Du kan välja mellan följande alternativ:

   * [!UICONTROL **Sandbox**] - Perfekt för design- och testningsändamål. Du bör påbörja din [!DNL Adobe Commerce as a Cloud Service]-resa med sandlådemiljön.
   * [!UICONTROL **Produktion**] - För livebutiker och kundorienterade webbplatser.

   >[!NOTE]
   >
   >* Sandlådeinstanser är begränsade till Nordamerika.
   >* Alternativet att installera exempeldata är för närvarande inte tillgängligt.

1. Markera regionen där du vill att instansen ska vara värd.

   >[!NOTE]
   >
   >När du har skapat instansen kan du inte ändra regionen.

1. Klicka på [!UICONTROL **Lägg till instans**].

### Åtkomst till en instans

När du har skapat en instans kan du komma åt den från [!UICONTROL Commerce Cloud Manager].

1. Logga in på ditt [Adobe Experience Cloud](https://experience.adobe.com/)-konto.

1. Under [!UICONTROL Quick access] klickar du på [!UICONTROL **Commerce**] för att öppna [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visar en lista med instanser som är tillgängliga i din Adobe IMS-organisation.

1. Om du vill öppna [!UICONTROL Commerce Admin] för en instans klickar du på instansnamnet.

>[!TIP]
>
>Om du vill visa information om instansen, inklusive REST- och GraphQL-slutpunkterna och Admin-URL:en, klickar du på informationsikonen bredvid instansnamnet.

Bas-URL:erna för din administratör och slutpunkter skiljer sig åt beroende på region och miljö, enligt följande mönster:

* Administratör
   * Produktionsadministratör för Nordamerika: `https://na1.admin.commerce.adobe.com`
   * Sandlådeadministratör för Nordamerika: `https://na1-sandbox.admin.commerce.adobe.com`
   * Europeisk produktionsadministratör: `https://eu1.admin.commerce.adobe.com`
* REST och GraphQL
   * Nordamerikas produktion - GraphQL: `https://na1.api.commerce.adobe.com`
   * Nordamerika, sandlåda GraphQL: `https://na1-sandbox.api.commerce.adobe.com`
   * GraphQL för produktion i Europa: `https://eu1.api.commerce.adobe.com`

### Importera katalogen

Som standard innehåller [!DNL Adobe Commerce as a Cloud Service] instanser inga produktdata. Du kan välja att ta med exempelproduktdata när du skapar en instans i testnings- och utbildningssyfte innan du importerar din egen katalog.

Det finns två sätt att importera katalogen till [!DNL Adobe Commerce as a Cloud Service]:

* [**Commerce Admin**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - Ett användarvänligt gränssnitt där du kan importera katalogdata med bara några klick.
* [**Importera JSON API**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - ett REST API som gör att du kan importera katalogdata programmatiskt.

### Konfigurera butiken

Nu när du har skapat en instans är du redo att [konfigurera din butik](storefront.md) med Edge Delivery Services.

## Ytterligare resurser

* [Versionsinformation](release-notes.md)
* [Migreringsguide](migration/overview.md)
* [Commerce Storefront-dokumentation](https://experienceleague.adobe.com/developer/commerce/storefront/)
