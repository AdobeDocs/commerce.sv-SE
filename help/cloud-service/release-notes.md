---
title: Versionsinformation för [!DNL Adobe Commerce as a Cloud Service]
description: Läs om de senaste funktionerna och förbättringarna i  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: f08921e0e431219ef28c431ce46f5831bde1461e
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Versionsinformation

Följande versionsinformation innehåller uppdateringar för [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Om du använder Adobe Commerce lokalt eller Adobe Commerce i molninfrastrukturen kan du läsa [Adobe Commerce versionsinformation](https://experienceleague.adobe.com/sv/docs/commerce-operations/release/notes/overview).

## Januari 2026 {#latest}

[!BADGE Produktion]{type=Neutral tooltip="Objekten i listan är för närvarande tillgängliga i produktionsmiljöer."}

Följande objekt släpptes till produktionsmiljöer för [!DNL Adobe Commerce as a Cloud Service] den 20 januari 2026.

>[!BEGINSHADEBOX]

### B2B-tillägg

Följande ändringar har gjorts i komponenter för B2B-insticksprogram:

* [!DNL Commerce Storefront on Edge Delivery Services] innehåller nu [komponenter för B2B-släppning](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=sv-SE). Följande B2B-tillägg är nu tillgängliga:

   * **[Företagshantering](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/?lang=sv-SE)** - Aktiverar hantering av företagsprofiler och rollbaserade behörigheter för Adobe Commerce-butiker.
   * **[Företagsväljare](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/?lang=sv-SE)** - Tillhandahåller en UI-komponent som användare kan växla mellan flera företag som de är associerade med.
   * **[Inköpsorder](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/?lang=sv-SE)** - Hanterar arbetsflöden för inköpsorder, godkännanderegler och inköpsorderhistorik för B2B-transaktioner.
   * **[Offerthantering](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/?lang=sv-SE)** - Aktiverar överlåtbara offerter för B2B-kunder med arbetsflöden för anbudsförfrågan, förhandling och godkännande.
   * **[Rekvisitionslistor](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/?lang=sv-SE)** - Tillhandahåller verktyg för att skapa och hantera rekvisitionslistor för upprepade köp och bulkbeställning.

* Lanserade B2B Store-kompatibilitetspaketet. Det här paketet förbättrar GraphQL-schemat för [!DNL Adobe Commerce] B2B för att förbättra utvecklingen på B2B-system.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=sv-SE). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/?lang=sv-SE). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Klickbara länkar till externa leveransspår

Omvandla försändelsens spårningsnummer som finns i e-postmeddelanden från oformaterad text till klickbara länkar genom att [aktivera anpassade spårnings-URL:er](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Den här funktionen stöds för USPS, UPS, FedEx och DHL. <!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise - support

[!DNL Adobe Commerce as a Cloud Service] butiker har nu stöd för [reCAPTCHA Enterprise](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Den här funktionen ger avancerat robotskydd genom att använda adaptiv riskanalys och maskininlärning för att exakt skilja människor från automatiserade robotar. Det stärker webbplatsens säkerhet, förhindrar bedrägliga aktiviteter och minskar risken för skräppost och missbruk för att upprätthålla en säker shoppingupplevelse. <!-- CCSAAS-4242 -->

### Instansspecifik administratörsåtkomst

Du kan nu [tilldela användare åtkomst](./user-management.md#add-users) till enskilda [!DNL Adobe Commerce as a Cloud Service]-instanser i Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Observationer

Genom att använda [!DNL App Builder] kan du få djupare synlighet i [!DNL Adobe Commerce as a Cloud Service]-instansen med [OpenTelemetry-synlighet](https://developer.adobe.com/commerce/extensibility/observability/), som nu är automatiskt tillgänglig. OpenTelemetry tillhandahåller mätvärden, loggar och spårningar som hjälper dig att övervaka prestanda, felsöka problem snabbare och optimera din butik. Denna funktion ger proaktiva insikter i systemhälsan och ökar kundens tillförlitlighet.

>[!NOTE]
>
>För OpenTelemetry-synlighet krävs [!DNL App Builder] eller andra OOPE-erbjudanden (out-of-process extensibility).

### Priser för kataloger

Du kan nu kombinera nivåindelade prisrabatter med katalogregelrabatter med hjälp av [katalogprisregler](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Den här förbättringen gör att ni kan skapa mer dynamiska och konkurrenskraftiga prissättningsstrategier - att belöna massinköp samtidigt som ni tillämpar kampanjrabatter. Resultatet är större flexibilitet för att locka kunder, öka ordervärdet och driva konverteringar.<!-- See PR #708 in commerce-admin -->

### Förbättringar och felkorrigeringar

Följande valda förbättringar, optimeringar och felkorrigeringar ingår i den här versionen:

* Ett fel som kan inträffa vid överföring av en fil till S3 har åtgärdats. <!-- CCSAAS-4189 -->

* Ett `User is not entitled to access this instance`-fel som kan inträffa vid inloggning till Commerce Admin eller åtkomst till REST API har åtgärdats. <!-- CCSAAS-4324 -->

* Ett fel som uppstod när ett nyhetsbrev från rutnätet med nyhetsbrevmallar förhandsvisades eller köades har korrigerats. <!-- CCSAAS-4398 -->

* Korrigerade ett `404`-fel som inträffade när du klickade på knappen [!UICONTROL **Läs in data igen**] på Admin Dashboard. <!-- CCSAAS-4468 -->

* Ett problem där anpassade produktattribut inte kunde uppdateras via REST API när [!DNL AEM Assets integration] var aktiverat och produkten innehöll bilder har åtgärdats. <!-- ACAP-1178 -->

* Olika prestanda- och optimeringsförbättringar.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## November 2025

>[!BEGINSHADEBOX]

### Förbättringar

* [Användarhantering](./user-management.md) - Ändrad **produktadministratörsroll** i Admin Console för att automatiskt uppdatera användaråtkomst till Commerce Admin. <!-- CCSAAS-3012 -->

* Lagt till möjligheten att överföra och hämta bifogade offerter samt filer och bilder som är kopplade till kunder och kundadresser till Amazon S3 med försignerade URL:er i [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) och [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Med REST kan du även överföra kategoribilder. <!-- CCSAAS-3250 -->

* `POST /V1/customers`- och `PUT /V1/customers/{customerId}`-slutpunkterna har lagts till i [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/) för att skapa och uppdatera kunder. Dessa slutpunkter kräver IMS-auktorisering. <!-- CCSAAS-3112 -->

* [`exchangeOtpForCustomerToken`-mutationen &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) har lagts till, vilket kräver en kunds e-postadress och engångslösenord (OTP) och tar emot en kundtoken i utbyte. Denna mutation används vanligtvis i scenarier där en kund måste autentisera med hjälp av en engångslösenord som skickas till deras e-post eller telefon.

* Om en adress som definieras i konfigurationsskärmen [!UICONTROL **Store Email Addresses**] i Admin innehåller ett värde som slutar med `example.com`, skickar inte Commerce e-post till den här adressen. Systemet loggar i stället att e-postmeddelandet inte skickades.  <!-- CCSAAS-3533 -->

#### Anpassade orderattribut

* Administratörsanvändare kan nu visa och redigera [anpassade orderattribut](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) direkt från sorteringsvyn, redigeringsskärmen och skapa-skärmen på Admin-panelen. Den här förbättringen förbättrar hanteringen av anpassade orderdata som skapats via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
