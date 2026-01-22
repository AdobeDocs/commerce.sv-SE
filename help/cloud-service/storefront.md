---
title: Konfigurera din butik
description: Lär dig hur du använder verktyget för att ställa in  [!DNL Adobe Commerce as a Cloud Service] butiken.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Konfigurera din butik

Så här konfigurerar du [!DNL Adobe Commerce Storefront] som drivs av [!DNL Edge Delivery Services] för [!DNL Adobe Commerce as a Cloud Service] (SaaS):

En mer anpassningsbar och detaljerad genomgång finns i [storefront-dokumentationen](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=sv-SE).

1. Öppna [webbplatsskaparverktyget](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Välj **[!UICONTROL Create New Site (Code & Content)]**.

1. Ange **[!UICONTROL Github Organization/Username]** där du vill skapa databasen för butikskoden.

1. Ange **[!UICONTROL Site Name]**.

1. I fältet **[!UICONTROL Commerce GraphQL Endpoint (optional)]** anger du din [!DNL Adobe Commerce as a Cloud Service] (SaaS) GraphQL-slutpunkt, som du kommer åt i Commerce Cloud Manager när du har [skapat din instans](./getting-started.md#create-an-instance).

   Om du använder [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic) kan du även ange din [!DNL API Mesh] GraphQL-slutpunkt i fältet **[!UICONTROL Commerce GraphQL Endpoint (optional)]**. Mer information finns i [Skapa ett nät](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh).

1. Klicka på **[!UICONTROL Create Site]**. Följ instruktionerna på skärmen för att godkänna åtkomst till din GitHub-databas.

När processen är klar kan du anpassa butiken på följande sätt:

* Anpassa koden: `https://github.com/<username or org>/<repo name>`
* Redigera ditt innehåll: `https://da.live/#/<username or org>/<repo name>`
* Hantera din konfiguration: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Förhandsgranska din butik: `https://main--<repo name>--<username or org>.aem.page/`

## Nästa steg

Mer information finns i följande artiklar:

* [Uppdaterar butiksinnehåll](./use-cases.md#update-storefront-content) - Hantera och visa innehåll och data i butiken.
* [Sammanhangsberoende experiment](./use-cases.md#contextual-experimentation) - Skapa och hantera experiment i butiken.
* [Generera variationer](./use-cases.md#generate-variations) - Använd generativ AI för att automatisera generering av högklassigt innehåll.
* [Adobe Commerce Storefront-dokumentation](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE) - Få detaljerad information om hur du uppdaterar webbplatsinnehåll och integrerar med Commerce klientkomponenter och backend-data.
* [Konfigurationstjänst](https://www.aem.live/docs/config-service-setup) - Lär dig mer om hur du migrerar din butikskonfiguration från `config.json` till att använda konfigurationstjänsten, som har stöd för avancerade användningsfall som replikerad konfiguration och övertäckningar.
