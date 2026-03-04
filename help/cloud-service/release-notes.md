---
title: Versionsinformation för [!DNL Adobe Commerce as a Cloud Service]
description: Läs om de senaste funktionerna och förbättringarna i  [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 34dd7446e2c620436b1377fde977cca018ebf55f
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 0%

---

# Versionsinformation

Följande versionsinformation innehåller uppdateringar för [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Om du använder Adobe Commerce lokalt eller Adobe Commerce i molninfrastrukturen kan du läsa [Adobe Commerce versionsinformation](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## Mars 2026 {#latest}

[!BADGE Sandbox]{type=Caution tooltip="Objekten i listan är för närvarande bara tillgängliga i sandlådemiljöer. Adobe gör nya releaser tillgängliga i sandlådemiljöer först för att ge dig tid att testa kommande ändringar innan releasen är tillgänglig i produktionsmiljöer."}

Följande objekt är för närvarande tillgängliga i sandlådemiljöer i [!DNL Adobe Commerce as a Cloud Service] och kommer att släppas i produktionsmiljöer den 9 mars 2026.

>[!BEGINSHADEBOX]

### Kodningsverktyg och självstudiekurser för App Builder AI

Nu kan du använda [AI-utvecklingsverktyget](./migration/coding-tools.md) för att skapa nya [!DNL App Builder]-program och konvertera befintliga [!DNL Adobe Commerce] PHP-tillägg till [!DNL App Builder]-program. Följande självstudier finns för att visa hur du använder verktygen:

* [Förutsättningar](./tutorials/tutorial-prerequisites.md)
* [Självstudiekurs om klassificeringstillägg](./tutorials/ratings-extension.md)
* [Tilläggssjälvstudiekurs för leveransmetod](./tutorials/shipping-method-extension.md)

### Få åtkomst till App Builder apphantering via administratören

[!DNL Commerce Admin] innehåller nu ett menyalternativ som länkar till [apphantering](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}, ett enhetligt gränssnitt för att hantera [!DNL App Builder] appar som är kopplade till Commerce-instansen. Det här tillägget drivs av den senaste uppdateringen av användargränssnittet för administratörer för SDK. <!-- CEXT-5755 -->

### Begär ändring av gräns för att skapa entitet

Begränsningen för antalet webbplatser, butiker och butiksvyer var tidigare begränsad till 50. Du kan nu skicka en [supportförfrågan](https://experienceleague.adobe.com/home?support-tab=home#support) om du vill ändra dessa begränsningar, om det behövs. <!-- ACCS-398 -->

### Anpassa butiksautentiseringsmeddelanden med strukturerade felkoder

[`generateCustomerToken` GraphQL-mutationen &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} returnerar nu inskrivna felkoder tillsammans med felmeddelanden, vilket gör att butiker kan visa specifika gränssnittsmeddelanden per felorsak. Tillgängliga felkoder är: `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` och `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Skicka automatiska e-postpåminnelser för inaktivitet i kundvagn och önskelista

Modulen [E-postpåminnelse](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) är nu aktiv i [!DNL Adobe Commerce as a Cloud Service], vilket gör att handlare kan skapa automatiska påminnelseregler som utlöser e-postmeddelanden till kunder baserat på inaktivitet i kundvagn och önskelista. <!-- CCSAAS-4597 -->

### Prenumerera på webbkrok för kategoriborttagningshändelser

Webbkroken `observer.catalog_category_delete_before` är nu tillgänglig i [!DNL Adobe Commerce as a Cloud Service]. Använd det för att köra logik innan en kategori tas bort. <!-- CEXT-5862 -->

### Spåra gästorder som har placerats med ett registrerat e-postmeddelande

En ny valfri konfiguration på butiksnivå (inaktiverad som standard) gör att handlare kan spåra gästorder som placerats med en e-postadress som matchar ett registrerat kundkonto. När det här alternativet är aktiverat är beställningar av gäster som gjorts med ett registrerat e-postmeddelande fortfarande tillgängliga, samtidigt som de visas i kundens orderhistorik.

Om du vill aktivera den här funktionen går du till **Butiker** > Inställningar > **Konfiguration** > Försäljning > **Försäljning** > **Gästutcheckning** och anger inställningen **Tillåt gästorderåtkomst för registrerade e-postmeddelanden** till `Yes`.
<!-- ACCS-289 -->

### Förbättringar och felkorrigeringar

Följande valda förbättringar, optimeringar och felkorrigeringar ingår i den här versionen:

* Ett problem har korrigerats där vissa organisationsadministratörer felaktigt kunde få åtkomst till klientinstanser utan tillstånd per innehavare. <!-- ACCS-335 -->

* Ett problem som kunde logga ut en användare från [!DNL Commerce Admin] när en delad katalog ändrades har åtgärdats. <!-- ACCS-318 -->

* Korrigerade ett problem som gjorde att vissa webhooks-fält visades felaktigt i [!DNL Commerce Admin]-gränssnittet. <!-- CEXT-5874 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Februari 2026 - utgåva nr 2

[!BADGE Produktion]{type=Neutral tooltip="Objekten i listan är för närvarande tillgängliga i produktionsmiljöer."}

Följande objekt släpptes till produktionsmiljöer i [!DNL Adobe Commerce as a Cloud Service] den 24 februari 2026.

>[!BEGINSHADEBOX]

### Skicka kontextfält med e-handelshändelser

[!DNL Adobe Commerce as a Cloud Service] har nu stöd för [kontextfält](https://developer.adobe.com/commerce/extensibility/events/context-fields/) i händelsenyttolaster, vilket gör att du kan inkludera data som inte är en del av händelsen som standard. <!-- CEXT-5713 -->

### Prenumerera för att citera objekt spara händelser med en ny webkrok

Webbkroken `observer.sales_quote_item_save_before` är nu tillgänglig i [!DNL Adobe Commerce as a Cloud Service]. Använd det för att köra logik innan ett offertobjekt sparas. <!-- ACCS-346 -->

### Förbättringar och felkorrigeringar

Följande valda förbättringar, optimeringar och felkorrigeringar ingår i den här versionen:

* Ett fel som kan orsaka visningsproblem i produktlistan [!DNL Commerce Admin] har korrigerats. Produktlistan begränsar nu antalet delade kataloger som visas för att förbättra prestandan. <!-- CCSAAS-1242 -->

* Ett GraphQL-fel som kan förhindra att anpassningsbara presentkort läggs till i kundvagnen har åtgärdats. <!-- ACCS-313 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Februari 2026 - utgåva nr 1

[!BADGE Produktion]{type=Neutral tooltip="Objekten i listan är för närvarande tillgängliga i produktionsmiljöer."}

Följande objekt släpptes till produktionsmiljöer i [!DNL Adobe Commerce as a Cloud Service] den 10 februari 2026.

>[!BEGINSHADEBOX]

### Anpassa leveransmetoder och visa administratörsrapporter

Följande förbättringar har gjorts i [!DNL Commerce Admin]:

* [Leveranswebbhollösningar](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) har förbättrats och innehåller anpassade attribut för leveransadress. Den här ändringen gör det möjligt för handlare att implementera anpassade leveransmetoder. <!-- ACCS-235 -->

* Åtkomst till administratörsrapporter har lagts till, inklusive rapporter för [kunder](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports), [marknadsföring](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports), [produkter](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports) och [försäljning](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>Rapporter som inte är tillgängliga i [!DNL Adobe Commerce as a Cloud Service] är endast märkta som PaaS ([!BADGE Endast PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."}).

### Hämta anpassade fakturabelopp via REST API

Faktura-API:t har nu stöd för [anpassade fångstmängder](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) med tilläggsattribut. <!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>På grund av juridiska begränsningar är det anpassade fångstbeloppet endast tillgängligt i Nordamerika-regionen och i andra regioner där överbetalning är tillåten.

### Förbättringar och felkorrigeringar

Följande valda förbättringar, optimeringar och felkorrigeringar ingår i den här versionen:

* Korrigerade kupongstödrasterfiltret så att alla anpassade kuponger som skapats via API:t eller genom import visades. <!-- CCSAAS-4509 -->

* Korrigerade ett problem i [!DNL Storefront Compatibility B2B Package] där `setNegotiableQuoteShippingAddress`-mutationen inte sparade manuellt angivna adresser i kundens adressbok, även när `save_in_address_book` var inställd på `true`. <!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* Ett problem där produktbilder inte visades korrekt i [!DNL Edge Delivery Services] har åtgärdats på grund av skadade `no_selection`-värden i anpassade attribut relaterade till resursroller. <!-- ACAP-1206 -->

* Ett problem som förhindrar att federerade användarkonton med null-värden för förnamn eller efternamn får åtkomst till Commerce Admin har åtgärdats. <!-- ACCS-200 -->

* Förenklade konfigurationen av resursväljaren genom att automatiskt tillhandahålla regionspecifika IMS-klient-ID:n. Handlare behöver inte längre skicka supportärenden för att konfigurera resursväljaren för mappning av produktkategoribilder med resurser. Systemet använder nu automatiskt dedikerade IMS-klient-ID:n baserat på Commerce-regionen. <!-- ACCS-175 -->

* Olika prestanda- och optimeringsförbättringar. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Januari 2026

[!BADGE Produktion]{type=Neutral tooltip="Objekten i listan är för närvarande tillgängliga i produktionsmiljöer."}

Följande objekt släpptes till produktionsmiljöer för [!DNL Adobe Commerce as a Cloud Service] den 20 januari 2026.

>[!BEGINSHADEBOX]

### B2B-tillägg

Följande ändringar har gjorts i komponenter för B2B-insticksprogram:

* [!DNL Commerce Storefront on Edge Delivery Services] innehåller nu [komponenter för B2B-släppning](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). Följande B2B-tillägg är nu tillgängliga:

   * **[Företagshantering](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** - Aktiverar hantering av företagsprofiler och rollbaserade behörigheter för Adobe Commerce-butiker.
   * **[Företagsväljare](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** - Tillhandahåller en UI-komponent som användare kan växla mellan flera företag som de är associerade med.
   * **[Inköpsorder](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** - Hanterar arbetsflöden för inköpsorder, godkännanderegler och inköpsorderhistorik för B2B-transaktioner.
   * **[Offerthantering](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** - Aktiverar överlåtbara offerter för B2B-kunder med arbetsflöden för anbudsförfrågan, förhandling och godkännande.
   * **[Rekvisitionslistor](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)** - Tillhandahåller verktyg för att skapa och hantera rekvisitionslistor för upprepade köp och bulkbeställning.

* Lanserade B2B Store-kompatibilitetspaketet. Det här paketet förbättrar GraphQL-schemat för [!DNL Adobe Commerce] B2B för att förbättra utvecklingen på B2B-system.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Klickbara länkar till externa leveransspår

Omvandla försändelsens spårningsnummer som finns i e-postmeddelanden från oformaterad text till klickbara länkar genom att [aktivera anpassade spårnings-URL:er](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Den här funktionen stöds för USPS, UPS, FedEx och DHL. <!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise - support

[!DNL Adobe Commerce as a Cloud Service] butiker har nu stöd för [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Den här funktionen ger avancerat robotskydd genom att använda adaptiv riskanalys och maskininlärning för att exakt skilja människor från automatiserade robotar. Det stärker webbplatsens säkerhet, förhindrar bedrägliga aktiviteter och minskar risken för skräppost och missbruk för att upprätthålla en säker shoppingupplevelse. <!-- CCSAAS-4242 -->

### Instansspecifik administratörsåtkomst

Du kan nu [tilldela användare åtkomst](./user-management.md#add-users) till enskilda [!DNL Adobe Commerce as a Cloud Service]-instanser i Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Observationer

Genom att använda [!DNL App Builder] kan du få djupare synlighet i [!DNL Adobe Commerce as a Cloud Service]-instansen med [OpenTelemetry-synlighet](https://developer.adobe.com/commerce/extensibility/observability/), som nu är automatiskt tillgänglig. OpenTelemetry tillhandahåller mätvärden, loggar och spårningar som hjälper dig att övervaka prestanda, felsöka problem snabbare och optimera din butik. Denna funktion ger proaktiva insikter i systemhälsan och ökar kundens tillförlitlighet.

>[!NOTE]
>
>För OpenTelemetry-synlighet krävs [!DNL App Builder] eller andra OOPE-erbjudanden (out-of-process extensibility).

### Priser för kataloger

Du kan nu kombinera nivåindelade prisrabatter med katalogregelrabatter med hjälp av [katalogprisregler](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Tack vare den här förbättringen kan ni skapa mer dynamiska och konkurrenskraftiga prissättningsstrategier och belöna massinköp samtidigt som ni lägger på kampanjrabatter. Resultatet är större flexibilitet för att locka kunder, öka ordervärdet och driva konverteringar.<!-- See PR #708 in commerce-admin -->

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

* Administratörsanvändare kan nu visa och redigera [anpassade orderattribut](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) direkt från sorteringsvyn, redigeringsskärmen och skapa-skärmen på Admin-panelen. Den här förbättringen förbättrar hanteringen av anpassade orderdata som skapats via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
