---
title: Commerce Services Connector
description: Lär dig hur du integrerar din Adobe Commerce- eller Magento Open Source-instans med tjänster med hjälp av API-nycklar för produktion och sandlåda.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
source-git-commit: a1e7da7e4c49967e2975dfa133e246490bcff732
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Vissa Adobe Commerce- och Magento Open Source-funktioner drivs av [!DNL Commerce Services] och distribueras som SaaS (programvara som tjänst). Om du vill använda de här tjänsterna måste du ansluta [!DNL Commerce]-instansen med API-nycklar för produktion och sandlåda och ange datautrymmet i [konfigurationen](#saas-configuration). Du behöver bara konfigurera anslutningen en gång för varje instans.

Endast [!DNL Commerce]-licensägaren kan generera dessa API-nycklar. Om du inte är licensägare kan du begära nycklarna från den person eller det team som äger Commerce-licensen för din butik.

## Tillgängliga tjänster {#availableservices}

I följande lista visas de [!DNL Commerce]-funktioner som du kan komma åt via [!DNL Commerce Services Connector]:

| Tjänst | Tillgänglighet |
| --- | --- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) med Adobe AI | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) med Adobe AI | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe Commerce och Magento Open Source |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Arkitektur

På en hög nivå består [!DNL Commerce Services Connector] av följande kärnelement:

![Commerce Services Connector Architecture](assets/saas-config-sync-workflow.png)

I följande avsnitt beskrivs dessa element mer ingående.

## Referenser {#apikey}

Produktions- och sandbox-API-nycklarna genereras från [!DNL Commerce]-kontot för [licensägaren](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). Commerce-kontot identifieras av ett unikt [!DNL Commerce]-ID (MageID). Licensägaren för handlarens organisation kan generera API-nycklar för tjänster som produktrekommendationer eller Live Search så länge som kontot är i gott skick.

Nycklarna kan delas på behovsbasis med systemintegratören eller utvecklingsteamet som hanterar projekt och miljöer för licenshavarens räkning. Utvecklare som har beviljats [!DNL Shared Access] av licensägaren kan inte generera nycklarna för licensägarens räkning även om handlarens organisation finns i listrutan [!DNL Switch Accounts] för deras konto.

Dessutom är lösningsintegratörer berättigade att använda [!DNL Commerce Services]. Om du är en lösningsintegratör bör signeraren av partnerkontraktet [!DNL Commerce] generera API-nycklarna.

Nyckelidentifierarna *Produktion* och *Sandbox* avser SaaS-datautrymmesmiljöer där [!DNL Commerce Services] lagrar data (inte dina Adobe Commerce-miljöer). Du kan använda samma uppsättning API-nycklar i Adobe Commerce-miljöer för lokal utveckling, mellanlagring och produktion. Det viktiga är att du klistrar in rätt nyckelpar för den datamängd du konfigurerar.

Licensägaren är vanligtvis den primära kontakten på Adobe Commerce-kontot och är inte alltid densamma som Adobe Commerce projektägare i molninfrastrukturprojektet.

### Generera API-nycklar för produktion och sandlåda {#genapikey}

1. Logga in på ditt [!DNL Commerce]-konto på [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. Under fliken **Magento** väljer du **API-portal** i sidofältet.

1. Välj _Produktion_ eller **Sandbox** på menyn **Miljö**.

1. Ange ett namn i avsnittet _API-nycklar_ och klicka på **Lägg till ny** för att öppna dialogrutan för att hämta den nya nyckeln.

   ![Hämta privat nyckel](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Du kan bara kopiera eller hämta den privata nyckeln en gång. Lagra den säkert.

1. Klicka på **Hämta** för att spara den privata nyckeln och stäng sedan dialogrutan.

1. Upprepa stegen ovan för varje miljö (produktion och sandlåda).

   Avsnittet **API-nycklar** visar nu dina API-nycklar (offentliga). Du behöver alla fyra nycklarna (både produktions- och sandlådenycklar, Public+Private) när du [väljer eller skapar ett SaaS-projekt](#createsaasenv) i någon av de miljöer eller installationer som är associerade med licensen.

## SaaS-konfiguration {#saasenv}

[!DNL Commerce] instanser måste konfigureras med ett SaaS-projekt och ett SaaS-datautrymme så att [!DNL Commerce Services] kan skicka data till rätt plats. Ett SaaS-projekt grupperar alla SaaS-datautrymmen. SaaS-datamallarna används för att samla in och lagra data som gör att [!DNL Commerce Services] kan arbeta. Vissa av dessa data kan exporteras från instansen [!DNL Commerce] och vissa kan samlas in från shoppingbeteendet i butiken. Dessa data lagras sedan för att skydda molnlagringen.

För [!DNL Product Recommendations] och [!DNL Live Search] innehåller SaaS-datautrymmet katalog- och beteendedata. Du kan peka en [!DNL Commerce]-instans mot ett SaaS-datautrymme genom att [markera den](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) i [!DNL Commerce]-konfigurationen.

>[!WARNING]
>
> Använd endast ditt **SaaS-datautrymme för produktion** med din [!DNL Commerce]-produktionsinstallation. Om du använder den i icke-produktionsmiljöer kan du blanda testdata och livedata (till exempel testnings-URL:er eller testkatalogdata). Om detta händer [skickar du en supportförfrågan](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) för att begära datarensning.

Om du inte kan hitta konfigurationsfälten för Live Search i Admin kontrollerar du att du har angett rätt API-nyckelpar för den datamängd du har valt (produktionsdatamallar använder produktionsnycklar, medan testdatamallar använder sandlådenycklar). Om du konfigurerar felaktiga nycklar är inte SaaS-tjänster som Live Search tillgängliga i den Adobe Commerce-miljön.

### Ta bort en API-nyckel {#delapikey}

>[!WARNING]
>
>Om du tar bort en nyckel som fortfarande används avbryts de anslutna tjänsterna omedelbart.

Generera och lagra en ersättningsnyckel på ett säkert sätt innan du tar bort en API-nyckel. Uppdatera alla integreringar så att de använder den nya nyckeln och bekräfta att beroende tjänster fungerar som förväntat.

Om du inte ser **[!DNL Live Search]** konfigurationsfält på Admin Panel kontrollerar du att du har angett rätt SaaS API-nyckel för den miljön. Använd SaaS-nyckeln för produktion för produktionsdatautrymmet och mellanlagringsnyckeln för mellanlagringsdatautrymmet. Om fel nyckel har konfigurerats är SaaS-tjänster (inklusive **[!DNL Live Search]**) inte tillgängliga i din Adobe Commerce-miljö.

Klicka på **[!UICONTROL Delete]** på API-nyckeln som ska tas bort. Bekräfta åtgärden för att permanent ta bort nyckeln när du uppmanas till detta.

### Etablering av SaaS-datautrymme

Alla Adobe Commerce-handlare har tillgång till ett produktionsdatautrymme och två testdatamallar per SaaS-projekt.

Du kan använda testdatamallarna i icke-produktionsmiljöer, men undvika att använda samma dataminne i flera miljöer samtidigt. Om du vill flytta ett testdatautrymme till en annan miljö utför du en datarensning innan du väljer och konfigurerar det i den nya miljön.

För Adobe Commerce Cloud Pro-projekt med flera mellanlagringsmiljöer kan du begära ytterligare testdatamallar för varje mellanlagringsmiljö genom att [skicka en supportförfrågan](https://experienceleague.adobe.com/home?support-tab=home#support). Om du bara har en mellanlagringsmiljö och behöver ytterligare testdatamallar har du följande alternativ:

- Kontakta Customer Success-teamet eller en utsedd Customer Success Manager för att begära en extra staging-miljö.

- [Skicka en supportförfrågan](https://experienceleague.adobe.com/home?support-tab=home#support) om du vill begära ytterligare testdatautrymme och ange affärsjusteringen för det extra dataområdet. Denna begäran måste godkännas.

Magento Open Source-kunder som använder Adobe Payment Services kan också beställa ytterligare ett datautrymme. Kontakta betalningsteamet om du vill ha förhandsgodkännande av ytterligare datautrymme innan du skickar en [supportförfrågan](https://experienceleague.adobe.com/home?support-tab=home#support) för att begära testdatautrymmet.

Kunder som äger flera Cloud-projekt eller lokala (live/produktion) installationer kan också begära ytterligare produktions- och testdatamallar för varje projekt eller instans genom att [skicka en supportförfrågan](https://experienceleague.adobe.com/home?support-tab=home#support).

### Välja eller skapa ett SaaS-projekt {#createsaasenv}

Om du vill välja eller skapa ett SaaS-projekt begär du API-nycklarna [!DNL Commerce] från [!DNL Commerce]-licensägaren för din butik:

1. Gå till _System_ > Tjänster > **Commerce Services Connector** på sidofältet **Admin**.

   Om du inte ser avsnittet **[!UICONTROL Commerce Services Connector]** installerar du [!DNL Commerce]-modulerna för den [[!DNL Commerce] tjänst](#availableservices) som du vill använda och kontrollerar att paketet `magento/module-services-id` är installerat.

1. Klistra in dina nyckelvärden i avsnitten _[!UICONTROL Sandbox API Keys]_och_[!UICONTROL Production API Keys]_.

   - Privata nycklar måste innehålla `-----BEGIN PRIVATE KEY-----` i början av nyckeln och `-----END PRIVATE KEY-----` i slutet av nyckeln.
   - Om du inte har någon kopia av de faktiska nycklarna ber du licensägaren om dem och kopplar sedan värdena till konfigurationen.

   Klistra inte in nyckelvärden som kopierats från en säkerhetskopia eller ögonblicksbild av en databas. När konfigurationen sparas används ytterligare ett krypteringslager och nycklarna fungerar inte.

1. Klicka på **Spara**.

   Alla SaaS-projekt som är associerade med dina nycklar visas i fältet **Projekt** i avsnittet **SaaS-identifierare** .

1. Om det inte finns några SaaS-projekt klickar du på **Skapa projekt**. Ange sedan ett namn för SaaS-projektet i fältet **Projekt** .

   Undvik förvirring genom att inte använda en specifik Commerce-tjänst som namn för ditt projekt (till exempel *Live Search*, *Produktrekommendationer* eller *Dataanslutning*). Om din licens inte har etablerats för flera SaaS-projekt kan du använda samma SaaS-projekt för flera tjänster.

1. Välj det **datautrymme** som ska användas för den aktuella konfigurationen av [!DNL Commerce]-arkivet.

   Om du har olika instanser att integrera med Commerce Services [skickar du en supportanmälan](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) för att begära ett nytt SaaS-projekt för varje ytterligare instans. När supporten har skapat SaaS-projektet konfigurerar du integreringen för instansen med samma API-nycklar och väljer det nya SaaS-projektet för datamängden.

>[!WARNING]
>
> Om du genererar nya nycklar i API-portalen ska du omedelbart uppdatera API-nycklarna i Admin-konfigurationen. Om administratören fortfarande använder gamla nycklar slutar dina SaaS-tillägg att fungera och datainsamlingen avbryts.

Om du vill ändra namn på ditt SaaS-projekt eller din datautrymme klickar du på **Byt namn** bredvid ett av dem. Om du ändrar namnet påverkas inte tjänsten eftersom namnet bara är en etikett som hjälper dig att identifiera och skilja mellan projekt och datautrymme.

## IMS-organisation (valfritt) {#organizationid}

Om du vill ansluta din Adobe Commerce-instans till Adobe Experience Platform loggar du in på ditt Adobe-konto med din Adobe ID. När du har loggat in visas den IMS-organisation som är kopplad till ditt Adobe-konto i det här avsnittet.

## SaaS-dataexport

När din [!DNL Commerce]-instans har anslutit till [!DNL Commerce Services] exporterar SaaS-dataexportprocessen Commerce-data från din [!DNL Commerce]-server till [!DNL Commerce SaaS Services] så att den kan synkroniseras med anslutna Commerce-tjänster. I Admin kan du kontrollera synkroniseringsstatus med [kontrollpanelen för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Mer information finns i [Exportguiden för SaaS-data](../data-export/overview.md).
