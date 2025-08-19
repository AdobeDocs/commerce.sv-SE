---
title: Konfiguration för [!DNL Payment Services]
description: Efter installationen kan du konfigurera  [!DNL Payment Services]  i Admin på butikskonfigurationen.
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 0%

---

# Konfiguration för [!DNL Payment Services]

Du kan anpassa [!DNL Payment Services] efter dina behov med hjälp av de praktiska konfigurationsalternativen i Admin.

När du konfigurerar [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] i Admin gäller dessa konfigurationer bara för den miljö som anges i fältet _[!UICONTROL Method]_&#x200B;i_[!UICONTROL General Configuration]_. Alla ändringar du gör i konfigurationsfälten är oberoende av om du byter _[!UICONTROL Method]_-val. Om du byter metod återställs inte dina val.

## Allmän konfiguration

Du kan aktivera [!DNL Payment Services] för din butik och din _[!UICONTROL Merchant Location]_&#x200B;och aktivera antingen sandlådetestning eller livesändningar i avsnittet&#x200B;_[!UICONTROL General Configuration]_.

1. Gå till _>_ > **[!UICONTROL Stores]** på sidofältet _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Ange fältet _[!UICONTROL Merchant Country]_&#x200B;i_[!UICONTROL Merchant Location]_. Om _[!UICONTROL Merchant Country]_&#x200B;inte anges används&#x200B;_[!UICONTROL Default Country]_ från den allmänna konfigurationen.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;för att komma åt avsnittet&#x200B;_[!UICONTROL [!DNL Payment Services]]_.
1. Expandera avsnittet _[!UICONTROL [!DNL Payment Services]]_&#x200B;i avsnittet&#x200B;_[!UICONTROL General Configuration]_.
1. För **Aktivera** anger du det till `Yes` för att aktivera [!DNL Payment Services] för din butik.
1. För **Metod** anger du `Sandbox` om du fortfarande testar [!DNL Payment Services] för din butik eller `Production` om du är redo att aktivera livebetalningar.
1. Dina **[!UICONTROL Payment Services Sandbox ID]**- och **[!UICONTROL Payment Services Production ID]**-värden fylls i automatiskt när du har konfigurerat [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} och går till [!DNL Payment Services]-instrumentpanelen för första gången. Gör detta för att slutföra introduktionen av din sandlåda och/eller produktionsmiljö. Dessa värden kopplar ditt SaaS-ID till [!DNL Payment Services].

   >[!WARNING]
   >
   > Om du behöver ändra ditt dataområdes-ID i Commerce Services Connector måste du återställa ditt [!DNL Payment Services]-ID. Klicka på **Återställ betalningstjänst-ID** om du vill återställa ditt sandbox-ID. Om du återställer ditt [!DNL Payment Services]-sandlåde-ID måste du anlita dig på det igen.

1. Dina **[!UICONTROL PayPal Merchant ID]**- och **[!UICONTROL PayPal Merchant Status]**-värden tillhandahålls automatiskt av PayPal när du för första gången besöker kontrollpanelen [!DNL Payment Services].
1. För **mjuk beskrivning** (anpassade värden som visas i kundtransaktionsbankutdrag för att skilja butiker/varumärken/kataloger åt) lägger du till din anpassade text (upp till 22 tecken) i textfältet och ersätter `Soft descriptor` eller det befintliga värdet.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

![Vyn Adobe-lösning](assets/config-view-all.png){width="700" zoomable="yes"}

### Konfigurationsalternativ

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Enable] | webbplats | Aktivera eller inaktivera [!DNL Payment Services] för webbplatsen. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | butiksvy | Ange metod, eller miljö, för din butik. Alternativ: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | butiksvy | Ditt handlar-ID för sandlådan, som genereras automatiskt vid introduktion av sandlådor. |
| [!UICONTROL Payment Services Production ID] | butiksvy | Ditt handlar-ID för produktion, som genereras automatiskt under introduktionen av produktionen (live). |
| [!UICONTROL PayPal Merchant ID] | butiksvy | Ditt unika konto-ID för PayPal Merchant som genereras när du skapar ditt PayPal-konto. |
| [!UICONTROL PayPal Merchant Status] | butiksvy | Status för ditt PayPal-handels-ID. |
| [!UICONTROL Soft Descriptor] | webbplats eller butiksvy | Lägg till en mjuk beskrivning till webbplatserna och butiksvyn för att lägga till information till kundtransaktioner som avgränsar varumärken, butiker eller produktrader. |

## [!UICONTROL Credit Card Fields]

Betalningsalternativen för [!UICONTROL Credit Card Fields] erbjuder en enkel och säker utcheckning för betalningsmetoder med kreditkort eller betalkort.

Mer information finns i [Betalningsalternativ](payments-options.md#paypal-smart-buttons).

1. Gå till _>_ > **[!UICONTROL Stores]** på sidofältet _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Payment Services]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Credit Card Fields]_.
1. För **[!UICONTROL Title]** anger du text (om det behövs) för att ändra namnet på betalningsmetoden så som visas vid utcheckning.
1. Om du vill [ange betalningsåtgärden](production.md#set-payment-services-as-payment-method) väljer du **[!UICONTROL Authorize]** eller **Auktorisera och hämta**.
1. Om du vill prioritera en betalningsmetod på utcheckningssidan anger du ett `Numeric Only`-värde i fältet **[!UICONTROL Sort order]**.
1. För **[!UICONTROL Show on checkout page]** väljer du `Yes` för att aktivera kreditkortsfält på utcheckningssidan.
1. För **[!UICONTROL Vault Enabled]** väljer du `Yes` om du vill aktivera kreditkortsvalv för utcheckning.
1. För **[!UICONTROL Vault Enabled in Admin]** väljer du `Yes` om du vill att handlaren ska kunna skapa beställningar för kunder med hjälp av deras kreditkort.
1. Om du vill aktivera **[!UICONTROL 3D Secure authentication]** (`Off` som standard) väljer du `Always` eller `When required`.
1. För **[!UICONTROL Debug Mode]** väljer du `Yes` för att aktivera felsökningsläget eller `No` för att inaktivera det.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

### Konfigurationsalternativ

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Title] | butiksvy | Lägg till texten som ska visas som rubrik för det här betalningsalternativet i vyn Betalningsmetod vid utcheckning. Alternativ: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) för den angivna betalningsmetoden. Alternativ: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | butiksvy | Sorteringsordningen för den angivna betalningsmetoden på utcheckningssidan. `Numeric Only` värde |
| [!UICONTROL Show on checkout page] | webbplats | Aktivera eller inaktivera kreditkortsfält på utcheckningssidan. Alternativ: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | butiksvy | Aktivera eller inaktivera [kreditkortssäkringen](vaulting.md). Alternativ: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | butiksvy | Aktivera eller inaktivera möjligheten för [handlare att slutföra beställningar för kunder i administratören](vaulting.md) med en betalningsmetod som är skyddad. Alternativ: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | webbplats | Aktivera eller inaktivera [3DS-säker autentisering](security.md#3ds). Alternativ: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | webbplats | Aktivera eller inaktivera felsökningsläget. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096) är ett snabbt och enkelt sätt att betala säkert online. Under en **gästutcheckning** kan du på ett säkert sätt lagra ditt kort och leveransinformation för ännu snabbare inköp i framtiden.

Mer information finns i [Betalningsalternativ](payments-options.md#fastlane-button).

1. Gå till _>_ > **[!UICONTROL Stores]** på sidofältet _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Payment Services]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Fastlane]_.
1. Om du vill aktivera den väljer du `Yes` för **[!UICONTROL Enable Fastlane]** (`No` inaktiverar den).

   >[!NOTE]
   >
   > Om [!UICONTROL Fastlane] är aktiverat är betalningsalternativet [!UICONTROL Credit Card Fields] inaktiverat.

1. För **[!UICONTROL Title]** anger du text (om det behövs) för att ändra namnet på betalningsmetoden så som visas vid utcheckning. Standardtiteln är `Credit Card (via Fastlane)`
1. Om du vill [ange betalningsåtgärden](production.md#set-payment-services-as-payment-method) väljer du **[!UICONTROL Authorize]** eller **Auktorisera och hämta**.
1. Om du vill prioritera en betalningsmetod på utcheckningssidan anger du ett `Numeric Only`-värde i fältet **[!UICONTROL Sort order]**.
1. Ange om varumärket [!UICONTROL Fastlane] är aktiverat under utcheckning i Adobe Commerce genom att ställa in fältet **[!UICONTROL Enable messaging]** på `Yes`.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Enable Fastlane] | butiksvy | Aktivera eller inaktivera [!DNL Fastlane] på utcheckningssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | butiksvy | Lägg till texten som ska visas som rubrik för det här betalningsalternativet i vyn Betalningsmetod vid utcheckning. Standardvärdet är `Credit Card (via Fastlane)`. Alternativ: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) för den angivna betalningsmetoden. Alternativ: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | butiksvy | Sorteringsordningen för den angivna betalningsmetoden på utcheckningssidan. `Numeric Only` värde |
| [!UICONTROL Enable messaging] | butiksvy | Ange om varumärket [!UICONTROL Fastlane] är aktiverat under utcheckning i Adobe Commerce. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### Valfritt. Avancerade formatinställningar

Dessa valfria inställningar kan anpassa hur [!UICONTROL Fastlane] visas på webbplatsen.

>[!TIP]
>
>Format som inte uppfyller hjälpmedelsriktlinjerna återställs till standardinställningarna.

1. Navigera till avsnittet _[!UICONTROL Payment Services]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Fastlane]_.
1. Expandera avsnittet _[!UICONTROL Advanced Style Settings (optional)]_.
1. Ändra inställningarna efter behov.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.

Mer information om anpassning finns i [PayPal Developer Docs](https://developer.paypal.com/limited-release/accelerated-checkout-bt/).

#### Rotinställningar

Dessa valfria inställningar ändrar den övergripande [!UICONTROL Fastlane]-utcheckningskomponenten.

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Background Color] | butiksvy | Definierar komponentens bakgrundsfärg. Endast `RGB` värden |
| [!UICONTROL Border Color] | butiksvy | Definierar komponentens kantfärg. Endast `RGB` värden |
| [!UICONTROL Font Family] | butiksvy | Anger komponentens teckensnitt. Endast teckensnitt som är tillgängliga i ditt tema visas |
| [!UICONTROL Font Size Base] | butiksvy | Definierar storleken på teckensnittet. Endast `px` (pixel) värden |
| [!UICONTROL Padding] | butiksvy | Ställer in utfyllnaden i komponenten. Endast `px` (pixel) värden |
| [!UICONTROL Primary Color] | butiksvy | Definierar komponentens huvudfärg. Endast `RGB` värden |
| [!UICONTROL Text Color] | butiksvy | Definierar huvudfärgen för texten i komponenten. Endast `RGB` värden |

#### Indatainställningar

Dessa valfria inställningar gäller för kundinmatningsfälten i [!UICONTROL Fastlane]-komponenten.

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Background Color] | butiksvy | Definierar komponentens bakgrundsfärg. Endast `RGB` värden |
| [!UICONTROL Border Color] | butiksvy | Definierar komponentens kantfärg. Endast `RGB` värden |
| [!UICONTROL Border Radius] | butiksvy | Definierar kantens radie. Endast `px` (pixel) värden |
| [!UICONTROL Border Width] | butiksvy | Anger kantens bredd. Endast `px` (pixel) värden |
| [!UICONTROL Focus Border Color] | butiksvy | Definierar komponentens fokuskantfärg. Endast `RGB` värden |
| [!UICONTROL Text Color Base] | butiksvy | Definierar huvudfärgen för texten i komponenten. Endast `RGB` värden |

## [!UICONTROL Apple Pay]

Med [!DNL Apple Pay] kan handlarna erbjuda en säker, snabb och sömlös utcheckning i Safari - med stöd för upp till 99 domäner per handlarkonto. Knappen [!DNL Apple Pay] fyller automatiskt i betalnings-, kontakt- och leveransinformation från kundens iOS- eller macOS-enhet, vilket möjliggör snabba köp med ett klick som kan öka konverteringsgraden.

Mer information finns i [Betalningsalternativ](payments-options.md#apple-pay-button).

1. Gå till _>_ > **[!UICONTROL Stores]** på sidofältet _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Payment Services]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Apple Pay]_.
1. För **[!UICONTROL Title]** anger du text (om det behövs) för att ändra namnet på betalningsmetoden så som visas vid utcheckning.
1. Om du vill [ange betalningsåtgärden](production.md#set-payment-services-as-payment-method) väljer du **[!UICONTROL Authorize]** eller **[!UICONTROL Authorize and Capture]**.
1. Ange var alternativet [!DNL Apple Pay] är aktiverat i Adobe Commerce genom att välja `Yes` i följande alternativ efter behov:
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. Om du vill aktivera felsökningsläget väljer du `Yes` för **[!UICONTROL Debug Mode]** (`No` inaktiverar det).
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

### Konfigurationsalternativ

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Title] | butiksvy | Lägg till texten som ska visas som rubrik för det här betalningsalternativet i vyn Betalningsmetod vid utcheckning. Alternativ: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) för den angivna betalningsmetoden. Alternativ: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | webbplats | Aktivera eller inaktivera [!DNL Apple Pay] på utcheckningssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | butiksvy | Sorteringsordningen för den angivna betalningsmetoden på utcheckningssidan. `Numeric Only` värde |
| [!UICONTROL Show buttons on product detail page] | butiksvy | Aktivera eller inaktivera [!DNL Apple Pay] på produktinformationssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | butiksvy | Aktivera eller inaktivera [!DNL Apple Pay] i förhandsvisningen av minikundvagnen. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | butiksvy | Aktivera eller inaktivera [!DNL Apple Pay] på kundvagnssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | webbplats | Aktivera eller inaktivera felsökningsläget. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

Med betalningsalternativet [!UICONTROL Google Pay] kan handlaren erbjuda sina kunder Google Pay, som kan använda Google Wallet på sina enheter för att göra inköp.

Mer information finns i [Betalningsalternativ](payments-options.md#google-pay-button).

1. Gå till _>_ > **[!UICONTROL Stores]** på sidofältet _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Payment Services]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Google Pay]_.
1. (Valfritt) Ändra namnet på betalningsmetoden som visas vid utcheckning genom att ange det nya namnet i fältet **[!UICONTROL Title]**.
1. [Ange betalningsåtgärden](production.md#set-payment-services-as-payment-method) genom att välja **[!UICONTROL Authorize]** eller **[!UICONTROL Authorize and Capture]**.
1. Ange var alternativet [!DNL Google Pay] är aktiverat i Adobe Commerce genom att välja `Yes` i följande alternativ efter behov:
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. Om du vill aktivera **[!UICONTROL 3D Secure authentication]** (`Off` som standard) väljer du `Always` eller `When required`.
1. Om du vill aktivera felsökningsläget väljer du `Yes` för **[!UICONTROL Debug Mode]** (`No` inaktiverar det).
1. Konfigurera utseendet på knappen _[!UICONTROL Google Pay]_&#x200B;genom att markera **[!UICONTROL Button Color]**,**[!UICONTROL Button Type]**&#x200B;och **[!UICONTROL Button Style]**&#x200B;efter behov.
1. Om du vill ange höjden använder standardvärdet för höjd som definieras i **[!UICONTROL Button Style]**.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

### Konfigurationsalternativ

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Title] | butiksvy | Anger textetiketten som visas för det här betalningsalternativet i vyn Betalningsmetod vid utcheckning. Alternativ: `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) för den angivna betalningsmetoden. Alternativ: `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | webbplats | Aktivera eller inaktivera [!DNL Google Pay] på utcheckningssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | butiksvy | Sorteringsordningen för den angivna betalningsmetoden på utcheckningssidan. `Numeric Only` värde |
| [!UICONTROL Show buttons on product detail page] | butiksvy | Aktivera eller inaktivera [!DNL Google Pay] på produktinformationssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | butiksvy | Aktivera eller inaktivera [!DNL Google Pay] i förhandsvisningen av minikundvagnen. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | butiksvy | Aktivera eller inaktivera [!DNL Google Pay] på kundvagnssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | butiksvy | Aktivera eller inaktivera [Säker 3D-autentisering](security.md#3ds). Alternativ: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | webbplats | Aktivera eller inaktivera felsökningsläget. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | Butiksvy | Definiera färg för knappen [!DNL Google Pay]. Alternativ: `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | Butiksvy | Definiera typen för knappen [!DNL Google Pay]. Alternativ: `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

Mer information finns i [Information om objektalternativ för Google Pay API-begäran](https://developers.google.com/pay/api/web/reference/request-objects) .

## [!DNL PayPal Payment Buttons]

Betalningsalternativen för [!DNL PayPal payment buttons] erbjuder en enkel, snabb och säker utcheckningsprocess för din kund.

Mer information finns i [Betalningsalternativ](payments-options.md#paypal-smart-buttons).

Konfigurera [!DNL PayPal payment buttons]

Du kan aktivera och konfigurera betalningsalternativen för betalningsknapparna i PayPal i Admin:

1. Gå till _>_ > **[!UICONTROL Stores]** på sidofältet _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Payment Services]_&#x200B;i avsnittet&#x200B;_[!UICONTROL PayPal payment buttons]_.
1. Redigera fältet _[!UICONTROL Title]_&#x200B;om du vill ändra namnet på betalningsmetoden så som visas vid utcheckning.
1. Om du vill [ange betalningsåtgärden](production.md#set-payment-services-as-payment-method) väljer du **[!UICONTROL Authorize]** eller **[!UICONTROL Authorize and Capture]**.
1. Om du vill prioritera en betalningsmetod på utcheckningssidan anger du ett `Numeric Only`-värde i fältet **[!UICONTROL Sort order]**.
1. Om du vill aktivera/inaktivera [Betala senare meddelanden](payments-options.md#pay-later-button) väljer du `Yes`/`No` för **[!UICONTROL Display Pay Later Message]**.

   * Om du aktiverar meddelandet [Betala senare](payments-options.md#pay-later-button) visas en spärrknapp för **[!UICONTROL Configure Messaging]** så att du kan ange format för **[!UICONTROL PayPal Pay Later messaging]**.

1. Ange var betalningsknapparna för PayPal är aktiverade i Adobe Commerce genom att välja `Yes` i följande alternativ efter behov:
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Om du vill aktivera Venmo som betalningsalternativ väljer du `Yes` för **[!UICONTROL Venmo Enabled]**.
1. Om du vill aktivera kredit- och debetkort som betalningsalternativ (smart PayPal-knapp) väljer du `Yes` för **[!UICONTROL Credit and Debit Card Enabled]**.
1. Om du vill aktivera/inaktivera betalningsalternativet [PayPal Pay Senare](payments-options.md#pay-later-button) väljer du `Yes`/`No` för **[!UICONTROL PayPal Pay Later Enabled]**.
1. Om du vill aktivera felsökningsläget väljer du `Yes` för **[!UICONTROL Debug Mode]** (`No` inaktiverar det).
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

### Konfigurationsalternativ

| Fält | Omfång | Beskrivning |
|---|---|---|
| [!UICONTROL Title] | butiksvy | Lägg till texten som ska visas som rubrik för det här betalningsalternativet i vyn Betalningsmetod vid utcheckning. Alternativ: textfält |
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} för den angivna betalningsmetoden. Alternativ: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | webbplats | Aktivera eller inaktivera PayPal Pay Senare-meddelanden i kundvagnen, på produktsidan, i minikundvagnen och under kassaflödet. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | butiksvy | Ändra stilarna för PayPal Pay Senare Messaging. Alternativ: `[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | butiksvy | Aktivera eller inaktivera [!DNL PayPal payment buttons] på utcheckningssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | butiksvy | Aktivera eller inaktivera [!DNL PayPal payment buttons] på produktinformationssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | butiksvy | Aktivera eller inaktivera [!DNL PayPal payment buttons] i förhandsvisningen av minikundvagnen. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | butiksvy | Aktivera eller inaktivera [!DNL PayPal payment buttons] på kundvagnssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | butiksvy | Aktivera eller inaktivera betalalternativet Venmo där betalningsknappar visas. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | butiksvy | Aktivera eller inaktivera alternativ för kredit- och betalkort där betalningsknappar visas. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | butiksvy | Aktivera eller inaktivera utseendet för betalningsalternativ för PayPal Senare där betalningsknappar visas. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | webbplats | Aktivera eller inaktivera felsökningsläget. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Knappformat

Du kan också konfigurera alternativen för _[!UICONTROL Button style]_&#x200B;för betalningsknapparna:

1. Gå till _>_ > **[!UICONTROL Stores]** på sidofältet _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL [!DNL Payment Services]]_&#x200B;i avsnittet&#x200B;_[!UICONTROL PayPal Smart Button Styling]_.
1. Om du vill ange layouten väljer du `Vertical` eller `Horizontal` för **[!UICONTROL Layout]**
1. Välj bland de tillgängliga färgerna i **[!UICONTROL Color]** för att ange färgen.
1. Ange formen genom att välja `Rectangular` eller `Pill` för **[!UICONTROL Shape]**.
1. Om du vill använda standardhöjden väljer du `Yes` eller `No` för **[!UICONTROL Use Default Height]**.
1. Om du vill ange den anpassade höjden lägger du till önskad pixelhöjd för **[!UICONTROL Height]**.
1. Ange tagline genom att välja `Yes` eller `No` för **[!UICONTROL Tagline]**.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

### Konfigurationsalternativ

| Fält | Omfång | Beskrivning |
|--- |--- |--- |
| [!UICONTROL Layout] | Butiksvy | Definiera layoutstil för Paypal Payment-knappar. Alternativ: `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | Butiksvy | Definiera färg på knapparna för PayPal-betalning. Alternativ: [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | Butiksvy | Definiera formen på knapparna för PayPal-betalning. Alternativ: `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | Butiksvy | Definierar om betalningsknapparna för PayPal använder en standardhöjd. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | Butiksvy | Definiera höjden på PayPal-betalningsknapparna. Standardvärde: ingen |
| [!UICONTROL Label] | Butiksvy | Definiera etikett som visas i PayPal-betalningsknapparna. Alternativ: `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | Butiksvy | Aktiverar tagline. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Töm cachen

Om du ändrar konfigurationen i _Inställningar_, till exempel genom att växla knapparna Apple Pay, Venmo eller PayPal PayLater, måste du manuellt tömma cachen så att butiken visar de senaste konfigurationerna.

1. Gå till _>_ på sidofältet **[!UICONTROL System]** Admin **[!UICONTROL Cache Management]**.
1. Klicka på **[!UICONTROL Flush Cache]** om du vill uppdatera alla ogiltiga cacheminnen.

Om en cachetyp i cacheminneshanteringstabellen har statusen `INVALIDATED` kanske arkivet inte visar den senaste konfigurationen för det objektet. Töm cacheminnet för att uppdatera butiken så att den senaste konfigurationen visas.

Om du vill vara säker på att rätt konfiguration visas på din butik [tömmer du cachen](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) med jämna mellanrum.

## Kortsäkring

Du kan aktivera funktioner som gör att dina kunder kan vault - eller&quot;save&quot; - sina kreditkortsuppgifter i Mitt konto och använda dem för framtida inköp.

Du kan också använda kortvalsfunktionen i Admin för att slutföra efterföljande beställningar för befintliga kunder.

Aktivera eller inaktivera kortvalsning i [inställningarna för kreditkortsfältet](#credit-card-fields).

Mer information finns i [Kreditkortssäkringar](vaulting.md).

## 3DS

3DS skyddar kunder och handlare från bedräglig verksamhet i deras butiker och möjliggör efterlevnad av EU:s standarder.

Aktivera eller inaktivera 3DS i [Inställningar för kreditkortsfält](#credit-card-fields).

Mer information finns i [3DS i säkerhet](security.md#3ds).

## Använd flera PayPal-konton

I [!UICONTROL Payment Services] kan du använda flera PayPal-konton i **one**-handelskontot på webbplatsnivå. Om du till exempel har butik(er) i flera länder (som använder olika [valutor](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency)) eller vill använda Adobe Commerce för vissa delar av din verksamhet, men inte _alla_, kan du konfigurera ditt handlarkonto så att du använder flera PayPal-konton.

Mer information om hierarkin för webbplatser, butiker och vyer [ finns i ](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)Webbplats, Lagra och Vyområde.

Mer information om hur du konfigurerar scope för flera PayPal-konton via CLI finns i [Kommandoradskonfiguration](configure-cli.md#configure-scope-via-cli).

Säljaren kan skapa ett nytt [scope](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) för ditt handlarkonto och lägga till ytterligare en webbplats med PayPal så att alla PayPal-knappar som du konfigurerar visas på din webbplats. Kontakta din säljare
-representant för att få hjälp med att använda flera PayPal-konton för dina webbplatser.
