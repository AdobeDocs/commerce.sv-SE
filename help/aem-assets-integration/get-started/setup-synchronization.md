---
title: Konfigurera integreringen
description: Lär dig hur du kopplar ihop dina Adobe Commerce-projekt och Experience Manager Assets-projekt för att möjliggöra resurssynkronisering mellan dessa två system.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: d59c9d179018318d7a0ab1685d8e9e172eefa3ed
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---

# Konfigurera integreringen

Konfigurera integreringen genom att ansluta Commerce till AEM Assets-instansen och välja matchningsstrategi för resurssynkronisering.

När du har identifierat AEM Assets-projektet väljer du matchningsregel för att synkronisera resurser mellan Adobe Commerce och AEM Assets.

* **[!UICONTROL Match by product SKU]** - Standardregel som matchar SKU:n i resursmetadata med [Commerce-produktens SKU](https://experienceleague.adobe.com/sv/docs/commerce-operations/implementation-playbook/glossary#sku) för att se till att resurserna är kopplade till rätt produkter.

* **[!UICONTROL Custom match]** - Matchningsregel för mer komplexa scenarier eller specifika affärskrav som kräver anpassad matchningslogik. Implementering av anpassad matchning kräver utveckling av anpassad kod i Adobe Developer App Builder för att definiera hur resurser matchas med produkter. Mer information kommer snart...

Använd standardregeln *Matcha efter produktsku* för den första konfigurationen.

## Krav

Innan du konfigurerar AEM Assets Integration bör du kontrollera att du har utfört följande steg:

* [Konfigurera AEM Assets-projektet](configure-aem.md)

* [!BADGE PaaS endast]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."} [Installera Adobe Commerce-paket](configure-commerce.md) om du vill lägga till tillägget och generera nödvändiga autentiseringsuppgifter och anslutningar för att använda tillägget.

### IMS och användarbehörigheter

Följande behörigheter krävs för att du ska kunna använda resursväljaren och få en smidigare konfiguration i Commerce:

>[!BEGINTABS]

>[!TAB ACCS]

[!BADGE Endast SaaS]{type=Positive tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."}

IMS-autentisering är aktiverat som standard. Lägg till användaren i produktprofilen **AEM Assets DM OpenAPI Users - leverans** i [Adobe Admin Console](https://adminconsole.adobe.com/) för att ge åtkomst till AEM Assets leveransskikt.

![Admin Console produktprofil för AEM Assets](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB PaaS]

[!BADGE Endast PaaS]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."}

1. [Aktivera Adobe IMS för Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=sv-SE){target=_blank} genom att följa instruktionerna i *Commerce Admin Guide*.

1. [Öppna en supportbiljett](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) för att begära ett anpassat IMS-klient-ID för resursväljaren.

1. Lägg till användaren i produktprofilen **AEM Assets DM OpenAPI Users - leverans** i [Adobe Admin Console](https://adminconsole.adobe.com/) för att ge åtkomst till AEM Assets leveransskikt.

>[!ENDTABS]

## Konfigurera anslutningen

1. Öppna AEM Assets Integration-konfigurationen i Commerce Admin.

   1. Gå till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

      ![AEM Assets-integrering aktiverar integreringen](../assets/aem-assets-view.png){width="600" zoomable="yes"}

>[!INFO]
>
> AEM Assets-integreringen stöder bara konfiguration i det globala (standardomfånget). Konfiguration på webbplatsnivå stöds inte. När du försöker konfigurera integreringen på webbplatsnivå ignorerar systemet inställningarna på webbplatsnivå och använder globala konfigurationsvärden i stället.

1. [!BADGE PaaS endast]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."} Ange **[!UICONTROL Asset Selector IMS Client ID]**.

   Detta ID krävs för att aktivera tillgångsväljaren och funktionen för automatisk ifyllning för fälten Program-ID och Miljö-ID. Se [IMS och användarbehörigheter](#ims-and-user-permissions) för att få detta ID. Mer information om resursväljaren finns i [Markera resurser manuellt](../synchronize/asset-selector-integration.md).

1. Välj AEM Assets-miljön **[!UICONTROL Program ID]** och **[!UICONTROL Environment ID]** i listrutorna.

   Listrutorna fylls i automatiskt baserat på användarens IMS-session. Om du vill använda den här funktionen måste du ha rätt [IMS och användarbehörigheter](#ims-and-user-permissions).

   Om listrutorna inte är tillgängliga kan du ange ID:n manuellt från AEM Cloud Manager URL: `https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

   Redigera konfigurationsvärdena genom att ta bort markeringen från *[!UICONTROL Use system value]*.

1. [!BADGE PaaS endast]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."} Välj [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) för autentisering av begäranden mellan Commerce och tjänsten för resursmatchning.

1. Ange **[!UICONTROL Synchronization enabled]** till `Yes` om du vill tillåta att Commerce accepterar inkommande uppdateringar från AEM Assets.

   När integreringen har aktiverats finns det ytterligare konfigurationsalternativ som du kan använda för att ange matchningsvillkor för resurser.

1. Välj en av resursmatchningsreglerna för resurssynkronisering i listrutan **[!UICONTROL Asset matching rule]**.

   * Välj **[!UICONTROL Match by SKU]** för [standardautomatisk matchning](../synchronize/default-match.md),
   * Välj **[!UICONTROL Custom match]** för [anpassad automatisk matchning](../synchronize/custom-match.md) (kräver [Adobe Developer App Builder](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)).

1. Lägg till det [AEM Assets-metadatafältnamn](configure-aem.md#configure-metadata) som är definierat för Commerce-produkter-SKU:er i fältet **[!UICONTROL Match by product SKU attribute name]**, `commerce:skus` som standard.

1. Välj **[!UICONTROL Save Config]** om du vill använda uppdateringar och initiera resurssynkronisering.

   Konfigurationsuppdateringen utlöser den inledande synkroniseringsprocessen så att Commerce kan acceptera inkommande uppdateringar från AEM Assets. Den tid som krävs för synkronisering beror på mängden resurser och specifika konfigurationer. Integreringen utnyttjar automatiserade processer för att minimera den tid som krävs för synkronisering.

### Synkronisera SLA

Integreringen garanterar följande nivåer för synkroniseringsprestanda:

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

På så sätt ser du till att produktsidorna alltid visar de mest aktuella bilderna och att butiksinnehållet är exakt och snyggt.

### Konfigurera visualiseringsägaren

Inställningen **Visualiseringsägare** avgör vilket system som skickar produktbilder i integreringen:

* Adobe Commerce - Använder bilder från Commerce.

* AEM Assets - Använder bilder som synkroniserats från AEM.

Admin visar de tillgängliga bilderna för den ägaren, medan resten av bilderna är nedtonade och visas med en **dold** -etikett.

Mer information om bildvisningsbeteende finns i avsnittet [Ange bildinformation](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}.

>[!TIP]
>
> Under en migrering från Commerce till AEM Assets anger du Commerce som ägare av **visualisering** så att inga bildlänkar bryts. När alla produkter har synkroniserats med AEM Assets kan du växla till AEM Assets ägare för att slutföra övergången. Detta garanterar kontinuerlig bildtillgänglighet under hela processen.

1. Navigera till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![Ägarfunktionen för visualisering av AEM Assets-integrering](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. Välj källan **Visualiseringsägare** om du vill visa bilderna.

1. Klicka på **[!UICONTROL Save Config]** för att tillämpa uppdateringar och initiera resurssynkronisering.

### Valfritt. Konfigurera URL för anpassad domän

Om AEM Assets as a Cloud Service-projektet har konfigurerats med ett [anpassat domännamn](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank} måste du lägga till domännamnet i Commerce Store-konfigurationen så att AEM Assets-integreringen för Commerce kan använda det.

1. Navigera till **[!UICONTROL Store]** > Konfiguration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![AEM Assets-integrering aktiverar integreringen](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. Lägg till **URL:en för den anpassade domänen** i fältet **[!UICONTROL Asset Custom Domain]**.

1. Klicka på **[!UICONTROL Save Config]** för att tillämpa uppdateringar och initiera resurssynkronisering.

## Nästa steg

* **Konfigurera din Commerce Storefront** - Om du vill använda AEM Assets med Commerce Storefront som drivs av Edge Delivery Services slutför du den konfiguration som beskrivs i avsnittet [AEM Assets-integrering](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=sv-SE) i *dokumentationen för Adobe Commerce Storefront*.

* Konfigurera [matchande regler](../synchronize/default-match.md) mellan Adobe Commerce och AEM Assets-integreringen.

* [Hantera Commerce-resurser](../manage-assets.md).
