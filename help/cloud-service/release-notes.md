---
title: Versionsinformation för [!DNL Adobe Commerce as a Cloud Service]
description: Läs om de senaste funktionerna och förbättringarna i  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 925df19c2827f474efe85708ea49974b285df29e
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Versionsinformation

Följande versionsinformation innehåller uppdateringar för [!DNL Adobe Commerce as a Cloud Service]. Versionsinformation om andra produkter finns i [Adobe Commerce Optimizer](../optimizer/release-notes.md) eller [Adobe Commerce lokalt och Adobe Commerce i molnet](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

[!DNL Adobe Commerce as a Cloud Service] innehåller de senaste versionerna av marknadsföringstjänster, betaltjänster och utökningsmöjligheter. Använd följande länkar om du vill visa versionsinformationen för var och en:

* Tjänster
   * [Katalogtjänst](../catalog-service/release-notes.md)
   * [Live Search](../live-search/release-notes.md)
   * [Betalningstjänster](../payment-services/release-notes.md)
   * [Produktrekommendationer](../product-recommendations/release-notes.md)
   * [SaaS-dataexport](../data-export/release-notes.md)
* Utbyggbarhet
   * [Administratörsgränssnitt SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
   * [API-nät](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
   * [Händelser](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
   * [Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

## November 2025

>[!BEGINSHADEBOX]

### Förbättringar

* [Användarhantering](./user-management.md) - Ändrad **produktadministratörsroll** i Admin Console för att automatiskt uppdatera användaråtkomst till Commerce Admin. <!-- CCSAAS-3012 -->

* Lagt till möjligheten att överföra och hämta bifogade offerter samt filer och bilder som är kopplade till kunder och kundadresser till Amazon S3 med försignerade URL:er i [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) och [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Med REST kan du även överföra kategoribilder. <!-- CCSAAS-3250 -->

* `POST /V1/customers`- och `PUT /V1/customers/{customerId}`-slutpunkterna har lagts till i [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) för att skapa och uppdatera kunder. Dessa slutpunkter kräver administratörsbehörighet. <!-- CCSAAS-3112 -->

* [`exchangeOtpForCustomerToken`-mutationen &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) har lagts till, vilket kräver en kunds e-postadress och engångslösenord (OTP) och tar emot en kundtoken i utbyte. Denna mutation används vanligtvis i scenarier där en kund måste autentisera med hjälp av en engångslösenord som skickas till deras e-post eller telefon.

* Om en adress som definieras i konfigurationsskärmen [!UICONTROL **Store Email Addresses**] i Admin innehåller ett värde som slutar med `example.com`, skickar inte Commerce e-post till den här adressen. Systemet loggar i stället att e-postmeddelandet inte skickades.  <!-- CCSAAS-3533 -->

#### Anpassade orderattribut

* Administratörsanvändare kan nu visa och redigera [anpassade orderattribut](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) direkt från sorteringsvyn, redigeringsskärmen och skapa-skärmen på Admin-panelen. Den här förbättringen förbättrar hanteringen av anpassade orderdata som skapats via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
