---
title: Migrera till  [!DNL Adobe Commerce as a Cloud Service]
description: Lär dig hur du migrerar till  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# Migrera till [!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] tillhandahåller de flesta konfigurationer som finns i paketet. Om du migrerar från en befintlig Adobe Commerce i molnet eller en lokal instans måste du utföra olika migreringsåtgärder beroende på din konfiguration.

## Migreringssökvägar

[!DNL Adobe Commerce as a Cloud Service] har stöd för flera migreringssökvägar, beroende på tidslinjen, butiken och anpassningar.

Som ett alternativ till en fullständig migrering stöder [!DNL Adobe Commerce as a Cloud Service] en stegvis migrering med Commerce Optimizer eller en stegvis metod.

* **Inkrementell migrering** - Detta innebär att migrera data, anpassningar och integreringar stegvis. Den här metoden är idealisk för stora handlare med många anpassningar som gradvis vill övergå sina komplexa anpassningar och data till [!DNL Adobe Commerce as a Cloud Service] i sin egen takt.

![inkrementell migrering](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** - Med den här metoden kan du migrera iterativt genom att använda Commerce Optimizer som en övergångsfas för att flytta komplexa anpassningar och data till [!DNL Adobe Commerce as a Cloud Service] i din egen takt. Commerce Optimizer ger tillgång till Merchandising Services som drivs av Catalog Channels and Policies, Commerce Storefront från Edge Delivery samt produktvisualer från AEM Assets.

![iterativ migrering](./assets/optimizer.png){width="600" zoomable="yes"}

* **Fullständig migrering** - Detta innebär att migrera alla data, anpassningar och integreringar samtidigt. Den här metoden är perfekt för mindre handlare med få anpassningar som snabbt vill övergå till [!DNL Adobe Commerce as a Cloud Service].

I följande tabell visas en översikt över migreringsprocessen för olika butiker och konfigurationer:

|                    | LUMA Storefront | PWA Storefront | Commerce Storefront med Edge Delivery i botten | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Datamigrering | Obligatoriskt | Obligatoriskt | Obligatoriskt | Obligatoriskt |
| Storefront | Migrera till Commerce Storefront från Edge Delivery | Migrera till Commerce Storefront från Edge Delivery eller Underhåll | Ingen effekt | Ingen effekt |
| API-nät | Skapa nytt nät | Skapa nytt nät eller konfigurera om befintligt nät | Skapa nytt nät eller konfigurera om befintligt nät | Skapa nytt nät eller konfigurera om befintligt nät |
| Integreringar | Utnyttja integreringens startpaket | Utnyttja integreringens startpaket | Utnyttja integreringens startpaket | Utnyttja integreringens startpaket |
| Anpassningar | Flytta till App Builder &amp; API Mesh | Flytta till App Builder &amp; API Mesh | Flytta till App Builder &amp; API Mesh | Flytta till App Builder &amp; API Mesh |
| Assets Management | Migrering krävs om OTB används | Migrering krävs om OTB används | Migrering krävs om OTB används | Migrering krävs om OTB används |
| Tillägg | Migrera till App Builder | Migrera till App Builder | Migrera till App Builder | Migrera till App Builder |

Som framgår av tabellen kommer åtgärderna för varje migrering att bestå av:

* **Datamigrering** - Använder tillhandahållna migreringsverktyg för att migrera data från din befintliga instans till [!DNL Adobe Commerce as a Cloud Service].
* **Storefront** - Befintliga EDS-filer och headless-butiker kräver inte reducering, men LUMA-butiker kräver migrering till Commerce Storefront från Edge Delivery. PWA Studio butiker kan migreras till Commerce Storefront från Edge Delivery eller underhållas i sitt nuvarande skick. Adobe kommer att tillhandahålla acceleratorer för att underlätta migrering av butiker.
* **[API-nät](https://developer.adobe.com/graphql-mesh-gateway)** - Skapa ett nytt nät eller ändra det befintliga. Adobe kommer att tillhandahålla förkonfigurerade nät som hjälp i den här processen.
* **Integrationer** - Alla integreringar måste utnyttja antingen [startsatsen för integrering](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) eller [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/).
* **Anpassningar** - Alla anpassningar måste flyttas till App Builder och API Mesh.
* **Assets Management** - All resurshantering kräver migrering. Om du redan använder AEM Assets behöver du inte migrera.
* **Tillägg** - Alla pågående tillägg måste återskapas som obearbetade tillägg. I slutet av 2025 kommer Adobe att ge åtkomst till våra populäraste tillägg för att minimera byggtider.

## Migreringsfaser

Migrering från din nuvarande Adobe Commerce-instans till en ny [!DNL Adobe Commerce as a Cloud Service]-instans omfattar i första hand följande faser:

* **[Beredskap](#readiness-phase)** - Börja med att kontrollera om distributionen är klar att flyttas till ACCS. I den här fasen bör du också bekanta dig med de ändringar som ACCS har gjort. &#x200B;
* **[Implementering](#implementation-phase)** - Därefter förbereder du kod, storeFront, tillägg och integreringar för migrering. För att underlätta övergången tillåter Adobe både [kortsiktiga och långsiktiga iterativa strategier](#migration-paths). &#x200B;
* **[Go-Live](#go-live-phase)** - Testa och bekräfta att allt finns på plats och utför sedan datamigreringen.
* **[Efterbeställ Go-Live](#post-go-live-phase)** - I samarbete med Adobe kan du kontrollera om det finns några problem och förbättra prestanda efter att migreringen är klar.

### Beredskapsfas

1. Börja med att granska [!DNL Adobe Commerce as a Cloud Service]-arkitekturen, utökningsramverket och storefront-funktionerna:

   * [Adobe Commerce på Cloud Services-arkitekturen](./overview.md) - Granska plattformsarkitekturen och hur den skiljer sig från din nuvarande Adobe Commerce-instans.
   * [Adobe Commerce Extensibility Framework](https://developer.adobe.com/commerce/extensibility/) - Identifiera hur du vill ändra de aktuella anpassningarna.
   * [Commerce Storefront från Edge Delivery](https://experienceleague.adobe.com/developer/commerce/storefront/) - Granska den rekommenderade lösningen för Store.

1. Granska din anpassningskompatibilitet:

   * Identifiera era aktuella anpassade moduler och tredjepartsintegreringar.
   * Utvärdera anpassningar som behöver implementeras på nytt med App Builder.
   * Koppla de aktuella anpassningarna till motsvarande App Builder-tillägg.

1. Bekräfta dina butikskrav och se till att de är i linje med Adobe Edge Delivery-funktionerna.

1. Granska dina aktuella tredjepartsintegreringar och bekräfta API-kompatibiliteten med plattformen [!DNL Adobe Commerce as a Cloud Service].

### Implementeringsfas

Följande steg beskriver hur migreringen ska utvecklas och köras:

1. Skapa en ny [!DNL Adobe Commerce as a Cloud Service]-instans i [Commerce Cloud Manager](./getting-started.md#create-an-instance).

1. Installera nödvändiga program och anpassningar. [!DNL Adobe Commerce as a Cloud Service] har tillgång till våra populäraste appar. Om du behöver ytterligare program eller anpassningar kan du implementera dem på nytt med App Builder.

1. Ställ in någon av följande GraphQL-baserade butiker:

   * [Skapa en Commerce-butik](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)
   * [Använd PWA Studio för att skapa en anpassad GraphQL-baserad butik](https://developer.adobe.com/commerce/pwa-studio/)

1. Migrera data från din tidigare Commerce-instans till ACCS:

   * Migrera inbyggda Adobe Commerce-data med datamigreringsverktyg.
   * Migrera tillägg och anpassningar från tredje part
   * Migrera konfigurations- och integreringsdata:
      * Överför API-nätkonfigurationer, tredjepartstjänster och systemintegreringar med [Adobe Commerce Integration Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/).

### GoLive-fas

Innan du startar validerar och testar du den nya [!DNL Adobe Commerce as a Cloud Service]-instansen med en sandlådemiljö:

* **Funktionstestning** - Se till att migrerade data, butiksfunktioner och anpassningar fungerar sömlöst.

* **Prestandatestning** - Utvärdera butikernas hastighet och skalbarhet för att säkerställa optimala prestanda globalt.

* **Säkerhetsgranskning** - Granska säkerhetsåtgärder, inklusive API-åtkomstkontroll och eventuella säkerhetsluckor.

När du har validerat och testat din nya [!DNL Adobe Commerce as a Cloud Service]-sandlådeinstans kan du starta din produktionsinstans.

### Post GoLive phase

Utför följande efter lanseringen:

1. Gå live följning

   * Omdirigera trafik till den nya plattformen och övervaka prestandan.
   * Inaktivera din gamla Adobe Commerce-instans.

1. Övervakning efter start

   * Använd övervakningsverktyg för att säkerställa stabil drift och åtgärda eventuella problem efter lanseringen.
