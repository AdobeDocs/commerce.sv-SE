---
title: Konfigurera din butik
description: Lär dig hur du kör byggnadsverktyget för att konfigurera  [!DNL Adobe Commerce as a Cloud Service] butiken.
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 408f28bdc20708022c8eca0fbfea4adb17014bf7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Konfigurera din butik

Gör så här för att konfigurera din Adobe Commerce Storefront från Edge Delivery Services för Adobe Commerce as a Cloud Service (SaaS).

Om du vill ha en mer anpassningsbar och detaljerad genomgång läser du [storefront-dokumentationen](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=sv-SE).

1. Öppna [webbplatsskaparverktyget](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Välj **Skapa ny plats (kod och innehåll)**.

1. Ange den **Github-organisation/användarnamn** där du vill skapa lagringskoddatabasen.

1. Ange ett **platsnamn**.

1. I fältet **Commerce GraphQL Endpoint (valfritt)** anger du din Adobe Commerce as a Cloud Service (SaaS) GraphQL-slutpunkt, som du kommer åt i Commerce Cloud Manager när du har [skapat instansen](./getting-started.md#create-an-instance).

   Om du använder [API-nät](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic) kan du även ange GraphQL-slutpunkten för API-nät i fältet **Commerce GraphQL Endpoint (valfritt)**. Mer information finns i [Skapa ett nät](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh).

1. Klicka på **Skapa plats**. Följ instruktionerna på skärmen för att godkänna åtkomst till din Github-databas.

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
* Mer information om hur du uppdaterar webbplatsinnehåll och integrerar med Commerce klientkomponenter och backend-data finns i [Adobe Commerce Storefront-dokumentationen](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=sv-SE).
