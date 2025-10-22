---
title: Hantera resurser
description: Använd AEM Assets Integration för Commerce för att hantera mediematerial för butiken.
feature: CMS, Media
exl-id: 40ca36e0-d617-4814-852d-bc60ff53b2b3
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Hantera Commerce medieresurser

<!--In ACAP-844, this topic was linked to from the Commerce Admin products images and videos when the Assets integration is enabled. If the URL to the topic changes, be sure to add a redirect.-->

Du kan hantera följande medietyper när AEM Assets-integreringen för Commerce har aktiverats:

* Produktbilder
* Innehållsbilder
* Produktvideor
* Kategoribilder

## Produktbilder

När integreringen är aktiverad centraliseras bildhanteringen i DAM-systemet (Digital Asset Management). Adobe Commerce fungerar sedan som en viktig engagemangskanal och ser till att endast godkända, högkvalitativa bilder används i alla butiker. Den här installationen förbättrar varumärkets enhetlighet, minimerar det manuella arbetet och effektiviserar innehållsuppdateringar, vilket eliminerar behovet av att handlarna manuellt överför eller hanterar bilder inom Adobe Commerce.

### Visa produktbilder i Adobe Commerce

Produktbilder hämtas automatiskt från AEM Assets baserat på förkonfigurerade matchningsregler:

1. Navigera till _>_ på sidofältet **[!UICONTROL Catalog]** Admin **[!UICONTROL Products]**.

1. Välj en produkt.

1. Öppna avsnittet **Bilder och video**.

   ![Produktbild](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Ett meddelande indikerar att integreringen är aktiverad, vilket gör detta till ett **skrivskyddat** -avsnitt när bildhanteringen är centraliserad i DAM.

### Hantera produktbilder i AEM Assets

Om du vill hantera produktrelaterade bilder måste alla ändringar göras direkt i **AEM Assets**. Denna process är helt automatiserad och säkerställer att alla ändringar synkroniseras med Adobe Commerce utan att manuell åtgärd krävs.

### SLA för synkronisering

Mer information om det här ämnet finns i [Synkronisera SLA](get-started/setup-synchronization.md#synchronization-sla).

## Innehållsbilder

Adobe Commerce tillhandahåller Page Builder som ett **innehållshanteringssystem (CMS)** för handlare som inte använder verktygsuppsättningen Adobe Experience Manager (AEM). För att förbättra skapandet av innehåll utnyttjar vår integrering [AEM Resursväljare](synchronize/asset-selector-integration.md), vilket gör att marknadsförare smidigt kan komma åt och bädda in bilder direkt från **DAM**. Detta garanterar att endast godkända och högkvalitativa bilder används vid innehållsskapande, vilket eliminerar behovet av redundant lagring i Adobe Commerce.

### Använda AEM Resursväljare i Page Builder

[!BADGE Endast sökvägar]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."} Om du vill använda **AEM-resursväljaren** för inbäddning av bilder:

1. Navigera till ett avsnitt i **Adobe Commerce Admin** som har stöd för `content enrichment` med **Page Builder**.

1. Öppna [Page Builder](https://developer.adobe.com/commerce/frontend-core/page-builder/){target=_blank}.

   En ny medietyp med namnet **AEM Asset** kommer att vara tillgänglig.

1. Dra och släpp medietypen AEM Asset i ett innehållsblock.

1. Ange inloggningsuppgifterna när du uppmanas att göra det.

1. Välj en bild från DAM och infoga den direkt i innehållet.

Kopplingen till den valda bilden kommer att lagras i Adobe Commerce som en direkt URL som pekar på **Dynamiska media**, vilket säkerställer att:

* Bildfiler behöver inte lagras i Adobe Commerce.

* Marknadsförarna arbetar exklusivt med godkända mediefiler från DAM.

* Innehållet är enhetligt och uppdaterat för alla kundkontaktytor.

>[!TIP]
>
> [DA.live (Document Authoring)](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/#dalive-document-authoring){target=_blank} innehåller också en resursväljare som förbättrar data.

## Produktvideor

Adobe Commerce är en viktig engagemangskanal för digitala resurser. När integreringen med AEM Assets har aktiverats centraliseras videohanteringen inom **DAM** för att säkerställa konsekvens, efterlevnad och optimerad leverans i alla e-handelslager.

### Hantera produktvideor

1. Navigera till _>_ på sidofältet **[!UICONTROL Catalog]** Admin **[!UICONTROL Products]**.

1. Välj en produkt.

1. Öppna avsnittet **Bilder och video**.

   ![Produktbild](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Ett meddelande indikerar att integreringen är aktiverad, vilket gör det här avsnittet **skrivskyddat** eftersom videoklipp styrs i AEM Assets.

### Associera videofilmer i AEM Assets

1. I AEM Assets navigerar du till den video du vill associera med en produkt.

1. Länka videon till en eller flera produkter i Adobe Commerce.

1. Integrationen synkroniserar automatiskt associationen och visar videospelaren Dynamic Media direkt i butiken. Detta eliminerar behovet av att handlare hanterar videouppspelningskonfigurationer.

### Endast API-första video

För närvarande stöder integreringen videor via API, vilket gör att partners kan hämta videor programmatiskt.

>[!WARNING]
>
> Videor är ännu inte integrerade i befintliga Adobe Commerce Store-lösningar.

Tack vare den här integreringen kan handlare enkelt hantera produktvideor på ett skalbart och optimerat sätt och utnyttja AEM Assets och Dynamic Media för smidig leverans.

### SLA för synkronisering

Mer information om det här ämnet finns i [Synkronisera SLA](get-started/setup-synchronization.md#synchronization-sla).

## Kategoribilder

Med Adobe Commerce kan handlare associera bilder med produktkategorier och skapa en visuellt engagerande butik. AEM Assets-integreringen utnyttjar AEM Resursväljare så att marknadsförarna smidigt kan välja resurser direkt från **DAM-systemet (Digital Asset Management)**. Detta säkerställer att endast godkända bilder används och eliminerar behovet av att lagra dem i Adobe Commerce, samtidigt som enhetlighet och effektivitet bibehålls i alla engagemangskanaler.

### Använd AEM Resursväljare för kategoribilder

När du har konfigurerat [AEM Resursväljare](synchronize/asset-selector-integration.md) kan du använda den för att lägga till resurser i katalogkategoriinnehåll.

1. Navigera till _>_ på sidofältet **[!UICONTROL Catalog]** Admin **[!UICONTROL Categories]**.

1. Välj en kategori som du vill uppdatera.

1. Expandera ![expanderingsväljaren](../assets/icon-display-expand.png) i avsnittet **[!UICONTROL Content]**.

1. I avsnittet **[!UICONTROL Content]** letar du reda på det *bildfält* som är associerat med kategorin.

   ![Kategoriinnehåll](assets/category-asset.png){width="600" zoomable="yes"}

1. Klicka på **[!UICONTROL Select from Assets]** om du vill ändra kategoribilden.

   ![Kategoriinnehåll](assets/asset-view.png){width="600" zoomable="yes"}

1. Välj en bild i AEM Resursväljare.

   ![Kategoriinnehåll](assets/select-image.png){width="600" zoomable="yes"}

1. Klicka på **[!UICONTROL Save]** och fortsätt.

   Mer information om hur du skapar en kategori finns i [Slutför kategoriinnehållet](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/create/category-create#step-3-complete-the-category-content) i **Commerce Catalog Management Guide**.

## Uppdatera en resurs

När du har uppdaterat och godkänt en mediefil i AEM Assets skickas uppdateringarna automatiskt till Adobe Commerce med den automatiska matchningsfunktionen. Den här processen aktiveras vid godkännande av tillgångar. Om du vill vara säker på att alla slutliga ändringar och metadatauppdateringar ingår måste du bearbeta resursen igen innan du godkänner den.

Mer information finns i följande AEM Assets-dokumentation.

* [Bearbetar digitala resurser](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing)

* [Godkänn en resurs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/approve-assets)
