---
title: Adobe Commerce Optimizer Connector for Commerce
description: Lär dig hur du kopplar data från ditt molnbaserade Commerce-projekt eller lokala projekt till Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
hidefromtoc: true
hide: true
source-git-commit: 36cfafff243a2310a17a2c9ec8a00f10403bc133
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---


# Adobe Commerce Optimizer Connector for Commerce

Adobe Commerce Connector är den integreringsbrygga som synkroniserar katalog- och prisdata mellan en befintlig Adobe Commerce Cloud i molnet eller lokal distribution och Adobe Commerce Optimizer datamodell för en sammansatt katalog. Detta möjliggör funktioner som dynamisk AI-sökning, rekommendationer, snabbladdande headless-butiker, inklusive Adobe Commerce storefront på Edge Delivery Services, samt realtidsanalyser av prestanda.

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

## Arkitektur och upplevelse

Adobe Commerce Connector fungerar genom att mappa Commerce `website/store/storeview`-kataloghierarkin till Adobe Commerce Optimizer `channel/policy/source`-datamodellen.

I stället för att konfigurera och hantera Commerce Services (Live Search och Product Recommendations) från Commerce Admin använder du [Adobe Commerce Optimizer Merchandising tools](../optimizer/merchandising/overview.md) för att hantera konfigurationen av produktidentifieringsregler (Live Search) och rekommendationer (produktrekommendationer).  Adobe Commerce-instansen blir datakälla för katalog- och prisdata. När data uppdateras i Commerce synkroniseras uppdateringarna med Adobe Commerce Optimizer-instansen.

## Arbetsflöden

Kopplingen möjliggör flera viktiga arbetsflöden:

* **Exportera Commerce-katalogdata till Adobe Commerce Optimizer** - pris- och prisboksdata exporteras på nivån `website`. Produkt- och produktattributdata exporteras på `store view`-nivå. Som standard är synkronisering av katalogdata aktiverat för alla Commerce-scope (webbplatser och butiksvyer).

  Om du vill aktivera det här arbetsflödet använder du Composer för att installera PHP-tillägget `adobe-commerce/commerce-data-export-aco-adapter` och anger sedan IMS-autentiseringsuppgifterna för att autentisera anslutningen mellan Commerce-projektet.

* **Mappa Commerce `website/store/storeview`-data som ska exporteras till Adobe Commerce Optimizer**

  Du kan anpassa inställningarna för Adobe Commerce Optimizer-exporteraren så att endast data exporteras för specifika omfattningar genom att uppdatera exportörens konfiguration från Store-stödrastret i Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* **Konfiguration och hantering av marknadsföringsregler**

  När Connector är aktiverat definieras och hanteras försäljningsregler för produktidentifiering och rekommendationer från Adobe Commerce Optimizer-gränssnittet, inte från sidorna [!UICONTROL Live Search] och [!UICONTROL Product Recommendations] i Commerce Admin.

* **Distribuera din Commerce Storefront på Edge Delivery Services**

  När du har konfigurerat integreringen med Adobe Commerce Optimizer kan du konfigurera och driftsätta en Commerce Storefront på Edge Delivery-tjänster för att leverera ultrasnabba prestanda, skalbarhet, smidig innehållsutveckling, integrerad personalisering och minskade driftskostnader med den sammansatta API-drivna arkitekturen och modulära komponenter som finns i Adobe Commerce Optimizer.

## Krav för att använda integreringen

* Adobe Commerce 2.4.5+

   * PHP 8.1, 8.2, 8.3 eller 8.4
   * Disposition 2.x

* Adobe Commerce Optimizer-licens med en etablerad sandlådeinstans.

* Åtkomst till [repo.magento.com](https://repo.magento.com) för att hämta Commerce Connector-metapaketet med Composer.

* Administratörsåtkomst till en [Adobe Commerce Optimizer-sandlådeinstans](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

Adobe Commerce-användaren som konfigurerar integreringen måste ha:

* Administratörsåtkomst till Adobe Commerce Admin.

* [Kommandoradsåtkomst till Adobe Commerce-programservern](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Utvecklaråtkomst till den [IMS-organisation](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) där Adobe Commerce Optimizer-projektet har etablerats.

## Kom igång

1. **Konfigurera integreringen**

   1. [Installera Commerce Connector-paketet](#install-the-commerce-connector-package).

   1. [Hämta de värden som krävs för att konfigurera Commerce Optimizer-anslutningen](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Aktivera Adobe Commerce Optimizer-integreringen](#enable-the-adobe-commerce-optimizer-integration).

   1. [Verifiera att datasynkroniseringen fungerar](#verify-that-the-data-sync-is-working).

   1. [Anpassa dataexportkonfigurationen](#customize-commerce-data-export-configuration) (valfritt).

1. **[Konfigurera Adobe Commerce Optimizer-butiker](#configure-adobe-commerce-optimizer-stores)**

1. **[Konfigurera en Commerce Storefront på Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Installera Commerce Connector-paketet

Metapaketet Adobe Commerce Connector Composer är tillgängligt för alla Commerce-handlare med en aktiv licens för Adobe Commerce Optimizer.

### Installationssteg

1. Lägg till modulen `adobe-commerce/commerce-data-export-aco-adapter` med Composer:

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. Distribuera ändringarna i Adobe Commerce staging-miljö.

När ändringarna har distribuerats är alternativet Commerce Optimizer Optimizer tillgängligt på Commerce Admin-menyn.

>[!NOTE]
>
>Detaljerade installationsanvisningar för tillägg finns i följande handböcker:
>
>[Installera tillägg på Adobe Commerce i molninfrastrukturen](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installera tillägget Adobe Commerce lokalt](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Hämta de värden som krävs för att konfigurera Commerce Optimizer-anslutningen

### Hämta API-autentiseringsuppgifter

>[!NOTE]
>
>Om du redan har ett App Builder Developer-projekt i den IMS-organisation där din Commerce Optimizer-instans är distribuerad, kan du hämta nödvändiga API-autentiseringsuppgifter och organisations-ID från autentiseringsuppgifterna för OAUTH-server-till-server i det projektet.

Skapa ett nytt utvecklarprojekt i Adobe Developer Console för att få API-autentiseringsuppgifter för att konfigurera integrationen mellan Commerce- och Commerce Optimizer-instanser. Instruktioner finns i [Skapa ett App Builder-projekt](https://developer.adobe.com/commerce/extensibility/events/project-setup/) i utvecklardokumentationen.

När du har skapat projektet sparar du följande värden från inloggningssidan för OAUTH-servern till-servern:

* **Organisations-ID** (`org_id`)

* **IMS `client_id` och`client_secret`**

### Hämta Adobe Commerce Optimizer-instansinformation

Spara följande värden från instansinformationen för Adobe Commerce Optimizer.

* **Instans-ID—**&#x200B;Den unika identifieraren för din Adobe Commerce Optimizer-instans. Kallas även innehavar-ID.

  Hämta instans-ID:t från URL:en för att komma åt din Adobe Commerce Optimizer-instans. I URL:en `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef` är till exempel instans-ID `1234567890abcdef`.

* **Region—**&#x200B;Den region där din Adobe Commerce Optimizer-sandlådeinstans finns.

  Hämta regionen från Adobe Commerce Optimizer URL. I URL:en `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef` är regionen till exempel `na1`.

## Aktivera Adobe Commerce Optimizer-integrering

>[!IMPORTANT]
>
>Datasynkroniseringsbearbetningen startar när du kör konfigurationskommandot. Som standard är synkronisering av katalogdata aktiverat för alla Commerce-scope (webbplatser och butiksvyer). Beroende på storleken på katalogen kan datasynkroniseringsprocessen ta många timmar.

Med API-autentiseringsuppgifterna och instansinformationen som du samlade in i föregående steg kan du nu konfigurera integreringen mellan dina Commerce- och Adobe Commerce Optimizer-instanser.

1. I Commerce Admin väljer du **[!UICONTROL Adobe Commerce Optimizer]** för att visa konfigurationssidan med instruktioner.

   ![Adobe Commerce Optimizer konfigurationssida](../assets/aco-connector-config-page.png)

1. Från kommandoraden [använder du SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) för att ansluta till Commerce mellanlagringsmiljö.

1. Kör följande Commerce CLI-kommando för att konfigurera integreringen och ersätt platshållarvärdena med värdena för ditt Commerce Optimizer-projekt:

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. Kontrollera anslutningen genom att gå tillbaka till Commerce Admin och välja alternativet [!UICONTROL Adobe Commerce Optimizer].

   När du klickar på alternativet öppnas Adobe Commerce Optimizer-gränssnittet på en ny flik.

## Verifiera att datasynkroniseringen fungerar

Du kan kontrollera datasynkroniseringen både från Commerce Admin och Commerce Optimizer.

* Statussidan **[Synkronisering av dataflöden](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)** visar förloppet för synkroniseringen av katalogdata från Commerce till Adobe Commerce Optimizer.

* **[[!UICONTROL Data Sync]-sidan &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)** i Adobe Commerce Optimizer visar katalogdata som överförts från din Commerce-instans.

1. Kontrollera att katalogdata flödar från Commerce till Commerce Optimizer:

   Öppna sidan [!UICONTROL Data Feed Sync Status] i Commerce Admin genom att välja [!UICONTROL System] **&#x200B; > [!UICONTROL Data Transfer] > &#x200B;** [!UICONTROL Data Feed Sync Status]**.

   ![Statussida för synkronisering av dataflöden med statusrapportering för feed-objekt](./assets/data-feed-sync-status.png)

   Om datasynkroniseringen har startat visas poster som har skickats i feed-data. Du kan även visa och felsöka synkroniseringsproblem genom att visa informationen för varje feed.

1. Kontrollera att Adobe Commerce Optimizer tar emot katalogdata:

   På Commerce Optimizer-menyn väljer du **[!UICONTROL Data Sync]** för att öppna sidan Datasynkronisering.

   ![Datasynkronisering](./assets/data-sync.png)

### Felsökning

Om datasynkroniseringen inte har startats kontrollerar du att katalogindexen är giltiga. Om indexen är ogiltiga kör du följande kommando från Commerce CLI för att indexera om katalogdata:

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Anpassa Commerce dataexportkonfiguration

Du kan anpassa inställningarna för Adobe Commerce Optimizer-exporteraren så att endast data exporteras för specifika omfattningar genom att uppdatera exportörens konfiguration från Store-stödrastret i Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* Om du inaktiverar exportörsinställningen på `website`-nivå avbryts exporten av priser och prisboksdata till Adobe Commerce Optimizer.

* Om du inaktiverar exportinställningen på nivån `storeview` avbryts exporten av produkter och produktattribut till Adobe Commerce Optimizer.

När konfigurationen ändras blir motsvarande index ogiltiga för att utlösa återexport av de berörda enheterna.

## Konfigurera Adobe Commerce Optimizer butiker

Konfigurera Adobe Commerce Optimizer butiker genom att skapa katalogvyer och principer. &#x200B; Se [Skapa katalogvyer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) i Adobe Commerce Optimizer Guide.

Observera att prisböcker skapas automatiskt av Adobe Commerce kundgrupper.

## Konfigurera en Commerce Storefront på Edge Delivery Services

I det här avsnittet finns en översikt på hög nivå över de steg som krävs för att konfigurera din Commerce-butik. Detaljerad information finns på dokumentationswebbplatsen för [Adobe Commerce Storefront] (https://experienceleague.adobe.com/developer/commerce/storefront/).

1. Klona och distribuera Adobe Commerce Storefront-mallsidor till EDS med verktyget [Webbplatsskapare](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. [Konfigurera en lokal utvecklingsmiljö](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment).

1. [Installera GraphQL Storefront-kompatibilitetspaket](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/). &#x200B;

1. [Konfigurera CORS-huvuden för Commerce-instansen i molnmiljön](#configure-cors-headers-for-commerce-instance).

1. [Anslut butiken till Commerce datakällor](#connect-the-storefront-to-commerce-data-sources).

### Konfigurera CORS-rubriker för Commerce-instans

Om du vill tillåta GraphQL-begäranden att komma från en Edge Delivery Services-butik (EDS) till Adobe Commerce i molnet eller lokal miljö använder du något av följande alternativ för att lägga till särskilda CORS-rubriker (Cross-Origin Resource Sharing) i Adobe Commerce GraphQL-slutpunkter. &#x200B;

1. Lägg till CORS-rubriker (Cross-Origin Resource Sharing) i slutpunkterna för Adobe Commerce GraphQL. &#x200B;

   **Alternativ 1: Implementera en anpassad PHP-modul för Adobe Commerce Foundation för att kunna lägga till CORS-huvuden. &#x200B;**

   **Alternativ 2: Installera en tredjepartsmodul för grycore/magento2-cors &#x200B;** - Se [CORS-konfiguration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/) i dokumentationen för *Adobe Commerce Storefront* .

1. Lägg till följande CORS-variabler i konfigurationsfilen för Commerce i molninstansen `app.yaml`:

   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_HEADERS: *`
   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_ORIGINS: *`

### Koppla butiken till Commerce datakällor

I GitHub-databasen för Storefront-mallkoden uppdaterar du konfigurationsfilen för storeFront, `config.json`, med följande parametrar:

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"` - Hämta det här värdet från [Commerce Optimizer-&#x200B; &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/optimizer/get-started#get-instance-details)

* `"AC-Environment-Id": "Customer organization ID"` - Hämta det här värdet från [Commerce molnprojekt](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/overview#project-overview)

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` - Hämta det här värdet från Adobe Commerce Optimizer Admin.

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` - Hämta det här värdet från Adobe Commerce Optimizer Admin. &#x200B;

* `"AC-Source-Locale": "Catalog source – Store View code from Commerce cloud instance"`

Mer information finns i [Storefront-konfiguration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/) i dokumentationen för *Adobe Commerce Storefront* .


