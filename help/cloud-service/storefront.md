---
title: Konfigurera din butik
description: Lär dig hur du använder verktyget för att ställa in  [!DNL Adobe Commerce as a Cloud Service] butiken.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 6eda2197fde2e88292e58b2bb4fc4759f24da558
workflow-type: tm+mt
source-wordcount: '235'
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

* Mer information om hur du hanterar och visar innehåll och data i butiken finns i [Uppdatera butiksinnehåll](./use-cases.md#update-storefront-content).
* Mer information om kontextuella experimenteringsfunktioner finns i [sammanhangsberoende experimenterande](./use-cases.md#contextual-experimentation).
* Mer information om hur du använder generativ AI för att automatisera generering av högkvalitativt innehåll finns i [Generera variationer](./use-cases.md#generate-variations).
* Om du vill veta mer om hur du uppdaterar webbplatsinnehåll och integrerar med komponenter i Commerce Front och backend-data kan du läsa [[!DNL Adobe Commerce Storefront documentation]](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE).
