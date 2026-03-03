---
title: Kom igång med Adobe Commerce Optimizer Connector
description: Lär dig hur du installerar och konfigurerar kopplingen, anpassar exportkonfigurationen, ansluter till Adobe Commerce Optimizer och övervakar status för datasynkronisering.
feature: Personalization, Integration, Configuration
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
source-git-commit: 79a422b1de81b33c68078af5c082e84d3dfe5bec
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---


# Kom igång

Installera och konfigurera Commerce Optimizer Connector för att synkronisera dina Adobe Commerce-katalogdata med [!DNL Adobe Commerce Optimizer] och övervaka sedan datasynkroniseringsstatusen för att se till att din butik är uppdaterad.

## Krav för att använda integreringen

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 eller 8.4
   * Disposition 2.x

* [!DNL Adobe Commerce Optimizer]-licens med en tilldelad sandlådeinstans.

* Åtkomst till [repo.magento.com](https://repo.magento.com) för att hämta Commerce Connector-metapaketet med Composer.

* Administratörsåtkomst till en [Adobe Commerce Optimizer-sandlådeinstans](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

Adobe Commerce-användaren som konfigurerar integreringen måste ha:

* Administratörsåtkomst till Adobe Commerce Admin.

* [Kommandoradsåtkomst till Adobe Commerce-programservern](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Utvecklaråtkomst till den [IMS-organisation](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) där [!DNL Adobe Commerce Optimizer]-projektet har etablerats.

>[!BEGINSHADEBOX]

## Förutsättningar

Om du har något av följande tillägg installerat avinstallerar du dem innan du installerar Commerce Optimizer Connector:

* Adobe Commerce Live Search (`magento/live-search`)
* Adobe Commerce produktrekommendationer (`magento/product-recommendations`)
* Adobe Commerce Catalog Service (`magento/catalog-service`, `magento/catalog-service-installer`)
* Instrumentpanel för datahantering (`magento-catalog-sync-admin`)

Data som är kopplade till dessa tillägg är fortfarande tillgängliga i Commerce-databasen. Den exporteras dock inte till [!DNL Adobe Commerce Optimizer] när anslutningen är aktiverad. Om du vill implementera de sök- och säljfunktioner som ingår i dessa tillägg efter att du har aktiverat Connector konfigurerar du dem från [[!DNL Adobe Commerce Optimizer] administratörsgränssnittet](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!ENDSHADEBOX]

## Konfigurationssteg

1. **Konfigurera integreringen**

   1. **[Installera Commerce Optimizer Connector-paketet](#install-the-commerce-connector-package)** med Composer för att ansluta din Commerce-instans till [!DNL Adobe Commerce Optimizer].

   1. **[Granska och anpassa dataexportkonfigurationen](#customize-commerce-data-export-configuration)** från administratören.

   1. **[Hämta API-autentiseringsuppgifter som krävs för att upprätta anslutningen mellan Commerce och Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)**.

   1. **[Aktivera  [!DNL Adobe Commerce Optimizer] integreringen](#enable-the-adobe-commerce-optimizer-integration)**.

   1. **[Verifiera att datasynkroniseringen fungerar](#verify-that-the-data-sync-is-working)**.


## Installera Commerce Optimizer Connector-paketet

Adobe Commerce Optimizer Connector levereras som ett Composer-metapaket tillgängligt för alla Commerce-handlare med en aktiv licens för [!DNL Adobe Commerce Optimizer].

### Installationssteg

1. Lägg till modulen `adobe-commerce/commerce-data-export-aco-adapter` med Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Distribuera ändringarna i Adobe Commerce staging-miljö.

När distributionen är klar är Commerce Optimizer-alternativet tillgängligt på Commerce Admin-menyn. Klicka på **[!UICONTROL Commerce Optimizer]** för att öppna din Commerce Optimizer-instans direkt från Commerce Admin.

>[!NOTE]
>
>Detaljerade installationsanvisningar för tillägg finns i följande handböcker:
>
>[Installera tillägg på Adobe Commerce i molninfrastrukturen](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installera tillägg på Adobe Commerce lokalt](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

### Hämta nödvändig anslutningsinformation

Från Adobe Developer Console skapar du ett utvecklarprojekt som är aktiverat för [!DNL Adobe Commerce Optimizer]-tjänsten och genererar autentiseringsuppgifter för OAuth Server-till-Server. Detaljerade instruktioner finns i [Hämta IMS-autentiseringsuppgifter](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) i *Handboken för marknadsföringsutvecklare*.

>[!TIP]
>
>Om du redan har ett utvecklarprojekt konfigurerat med API:t för datainmatning i samma IMS-organisation som din Commerce Optimizer-instans kan du återanvända de befintliga autentiseringsuppgifterna för OAuth Server-till-Server.

Spara följande värden från inloggningssidan:

* **Organisations-ID** (`org_id`)
* **Klient-ID** (`client_id`)
* **Klienthemlighet** (`client_secret`)

### Hämta [!DNL Adobe Commerce Optimizer] instansinformation

Spara instans-ID:t (kallas även klient-ID) från din [!DNL Adobe Commerce Optimizer]-instans. Du hittar den i den URL som används för att komma åt instansen. I `https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home` är till exempel instans-ID `TToyu73daQRn66KAYaq8YZ`.

## Anpassa dataexportkonfigurationen för Commerce

Som standard är synkronisering av katalogdata aktiverat för alla Commerce-scope (webbplatser och butiksvyer). Du kan anpassa exportinställningarna för att synkronisera data endast för specifika omfattningar baserat på ditt företags behov. Om du till exempel har flera butiksvyer men bara vill exportera data för en av dem, kan du inaktivera exporteraren för de andra butiksvyerna.

>[!IMPORTANT]
>
>Om du ändrar exportinställningarna utlöses en fullständig omindexering, vilket kan ta lång tid beroende på katalogstorleken. Planera dessa ändringar under lågtrafikperioder för att minimera prestandapåverkan.

### Dataexport efter omfång

I följande tabell beskrivs vilka data som exporteras på varje omfångsnivå:

| Omfång | Exporterade data | Anteckningar |
| ------- | --------------- | ------- |
| Webbplats | Priser och prislistor | Varje prisuppsättning exporteras som en [prisbok](../optimizer/setup/pricebooks.md) med namnkonventionen `website::customergroupcode`. Alla kundgrupper för webbplatsen ingår. |
| Butiksvy | Produkter och produktattribut | I varje butiksvy skapas en separat katalogkälla i [!DNL Adobe Commerce Optimizer]. |

### Aktivera och inaktivera beteende

| Åtgärd | Resultat |
| -------- | -------- |
| Inaktivera en butiksvy | Katalogkällan finns kvar i [!DNL Adobe Commerce Optimizer], men alla data tas bort. |
| Inaktivera och återaktivera sedan en butiksvy | Samma katalogkälla fylls i igen med en fullständig omsynkronisering av data. |

### Uppdatera exportkonfigurationen

När du har installerat Connector-paketet visas exportkonfigurationsinställningarna för Commerce Optimizer i Store-stödrastret i Admin.

![Lagra stödraster med synkroniseringsinställningar för Commerce Optimizer](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**Så här ändrar du inställningarna för en webbplats- eller butiksvy:**

1. Gå till **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]** i Commerce Admin.

1. Välj webbplatsen eller butiksvyn som du vill konfigurera.

1. I **[!DNL Adobe Commerce Optimizer]-exportinställningarna** använder du kryssrutan för att aktivera eller inaktivera datasynkronisering efter behov.

   ![Uppdatera datasynkroniseringskonfiguration](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. Spara ändringarna.

## Aktivera integreringen av [!DNL Adobe Commerce Optimizer]

>[!IMPORTANT]
>
>Datasynkroniseringsbearbetningen startar så snart du kör konfigurationskommandot. Som standard är synkronisering av katalogdata aktiverat för alla Commerce-scope (webbplatser och butiksvyer). Beroende på storleken på katalogen kan datasynkroniseringsprocessen ta från några minuter till flera timmar.

Med API-autentiseringsuppgifterna och instansinformationen som du samlade in i föregående steg kan du nu konfigurera integreringen mellan dina Commerce- och [!DNL Adobe Commerce Optimizer]-instanser.

1. I Commerce Admin väljer du **[!UICONTROL Adobe Commerce Optimizer]** för att visa konfigurationssidan med instruktioner.

   ![[!DNL Adobe Commerce Optimizer] konfigurationssida &#x200B;](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Från kommandoraden [använder du SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) för att ansluta till Commerce mellanlagringsmiljö.

1. Kör följande Commerce CLI-kommando för att konfigurera integreringen och ersätt platshållarvärdena med värdena för ditt Commerce Optimizer-projekt:

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. Kontrollera anslutningen genom att gå tillbaka till Commerce Admin och välja alternativet [!UICONTROL Adobe Commerce Optimizer].

   När du klickar på alternativet öppnas användargränssnittet för [!DNL Adobe Commerce Optimizer] på en ny flik.

## Verifiera att datasynkroniseringen fungerar

När du har aktiverat integreringen startar datasynkroniseringen automatiskt. Beroende på katalogstorleken kan den inledande synkroniseringen ta från några minuter till flera timmar.

1. **Kontrollera synkroniseringsstatus i Commerce Admin:**

   Gå till **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.

   ![Statussida för synkronisering av dataflöden med statusrapportering för feed-objekt](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   När synkroniseringen körs visas poster som skickats. Välj en feed om du vill visa information eller felsöka synkroniseringsproblem.

1. **Bekräfta data som har tagits emot i Commerce Optimizer:**

   Välj [!DNL Adobe Commerce Optimizer] på menyn **[!UICONTROL Data Sync]**.

   ![Datasynkronisering](./assets/data-sync.png){width="500" zoomable="yes"}

   Kontrollera att förväntade produkter, priser och attribut visas.

>[!TIP]
>
>Om du har problem med datasynkroniseringen kan du läsa avsnittet [Felsökning](/help/data-export/troubleshooting-logging.md) i dokumentationen för *SaaS-dataexport* .

## Nästa steg

1. **[Konfigurera [!DNL Adobe Commerce Optimizer] katalogvyer och principer](#configure-adobe-commerce-optimizer-stores)**

   Skapa katalogvyer och principer i [!DNL Adobe Commerce Optimizer]-handboken. Observera att prisböcker skapas automatiskt av Adobe Commerce kundgrupper.

1. **[Konfigurera en Commerce Storefront på Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   Följ [Storefront-installationsdokumentationen](https://experienceleague.adobe.com/developer/commerce/storefront/setup/) för att ansluta din butik till instansen [!DNL Adobe Commerce Optimizer] och börja leverera personaliserade e-handelsupplevelser.


