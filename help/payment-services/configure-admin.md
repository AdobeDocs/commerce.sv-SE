---
title: Konfiguration av äldre betaltjänster
description: Efter installationen kan du konfigurera  [!DNL Payment Services]  i Admin på butikskonfigurationen.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration
exl-id: a4da36e2-4316-42d5-ae30-cf078f440444
source-git-commit: 24622b8a20b8cd95e13a68df6e0929206ffbb06b
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---

# Äldre [!DNL Payment Services]-konfiguration

Du kan anpassa [!DNL Payment Services] efter dina behov med hjälp av de praktiska konfigurationsalternativen i Admin.

När du konfigurerar [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] i Admin gäller dessa konfigurationer bara för den miljö som anges i fältet _[!UICONTROL Method]_&#x200B;i_[!UICONTROL General Configuration]_. Alla ändringar du gör i konfigurationsfälten är oberoende av om du byter _[!UICONTROL Method]_-val. Om du byter metod återställs inte dina val.

## Allmän konfiguration

Du kan aktivera [!DNL Payment Services] för din butik och din _[!UICONTROL Merchant Location]_&#x200B;och aktivera antingen sandlådetestning eller livesändningar i avsnittet&#x200B;_[!UICONTROL General Configuration]_.

1. Gå till **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;på sidofältet_ Admin _.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Ange fältet _[!UICONTROL Merchant Country]_&#x200B;i_[!UICONTROL Merchant Location]_. Om _[!UICONTROL Merchant Country]_&#x200B;inte anges används&#x200B;_[!UICONTROL Default Country]_ från den allmänna konfigurationen.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;för att komma åt avsnittet&#x200B;_[!UICONTROL [!DNL Payment Services]]_.
1. Expandera avsnittet _[!UICONTROL General Configuration]_&#x200B;i avsnittet&#x200B;_[!UICONTROL [!DNL Payment Services]]_.
1. För **Aktivera** anger du det till `Yes` för att aktivera [!DNL Payment Services] för din butik.
1. För **Metod** anger du `Sandbox` om du fortfarande testar [!DNL Payment Services] för din butik eller `Production` om du är redo att aktivera livebetalningar.
1. Dina **[!UICONTROL Payment Services Sandbox ID]**- och **[!UICONTROL Payment Services Production ID]**-värden fylls i automatiskt när du har konfigurerat [Commerce Services Connector](https://experienceleague.adobe.com/sv/docs/commerce/user-guides/integration-services/saas){target=_blank} och går till [!DNL Payment Services]-instrumentpanelen för första gången. Gör detta för att slutföra introduktionen av din sandlåda och/eller produktionsmiljö. Dessa värden kopplar ditt SaaS-ID till [!DNL Payment Services].

   >[!WARNING]
   >
   > Om du behöver ändra ditt dataområdes-ID i Commerce Services Connector måste du återställa ditt [!DNL Payment Services]-ID. Klicka på **Återställ betalnings-ID** om du vill återställa din sandlåda eller dina produktions-ID. Om du återställer dina [!DNL Payment Services] ID:n måste du registrera dig igen.

1. Dina **[!UICONTROL PayPal Merchant ID]**- och **[!UICONTROL PayPal Merchant Status]**-värden tillhandahålls automatiskt av PayPal när du för första gången besöker kontrollpanelen [!DNL Payment Services].
1. För **mjuk beskrivning** (anpassade värden som visas i kundtransaktionsbankutdrag för att skilja butiker/varumärken/kataloger åt) lägger du till din anpassade text (upp till 22 tecken) i textfältet och ersätter `Soft descriptor` eller det befintliga värdet.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

![Vyn Adobe-lösning](assets/featured-adobe-solution-view.png){width="700" zoomable="yes"}

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

1. Gå till **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;på sidofältet_ Admin _.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Credit Card Fields]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Payment Services]_.
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
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=sv-SE) för den angivna betalningsmetoden. Alternativ: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | butiksvy | Sorteringsordningen för den angivna betalningsmetoden på utcheckningssidan. `Numeric Only` värde |
| [!UICONTROL Show on checkout page] | webbplats | Aktivera eller inaktivera kreditkortsfält på utcheckningssidan. Alternativ: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | butiksvy | Aktivera eller inaktivera [kreditkortssäkringen](vaulting.md). Alternativ: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | butiksvy | Aktivera eller inaktivera möjligheten för [handlare att slutföra beställningar för kunder i administratören](vaulting.md) med en betalningsmetod som är skyddad. Alternativ: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | webbplats | Aktivera eller inaktivera [3DS-säker autentisering](security.md#3ds). Alternativ: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | webbplats | Aktivera eller inaktivera felsökningsläget. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Apple Pay]

Betalningsalternativet [!UICONTROL Apple Pay] gör det möjligt för handlaren att erbjuda Apple Pay till sina kunder, som kan använda Touch ID på sina enheter för att göra inköp från webbläsaren Safari. Handlare kan lägga till upp till 99 domäner per handelskonto.

Mer information finns i [Betalningsalternativ](payments-options.md#apple-pay-button).

1. Gå till **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;på sidofältet_ Admin _.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Apple Pay]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Payment Services]_.
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
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=sv-SE) för den angivna betalningsmetoden. Alternativ: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | webbplats | Aktivera eller inaktivera [!DNL Apple Pay] på utcheckningssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | butiksvy | Sorteringsordningen för den angivna betalningsmetoden på utcheckningssidan. `Numeric Only` värde |
| [!UICONTROL Show buttons on product detail page] | butiksvy | Aktivera eller inaktivera [!DNL Apple Pay] på produktinformationssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | butiksvy | Aktivera eller inaktivera [!DNL Apple Pay] i förhandsvisningen av minikundvagnen. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | butiksvy | Aktivera eller inaktivera [!DNL Apple Pay] på kundvagnssidan. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | webbplats | Aktivera eller inaktivera felsökningsläget. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

Med betalningsalternativet [!UICONTROL Google Pay] kan handlaren erbjuda sina kunder Google Pay, som kan använda Google Wallet på sina enheter för att göra inköp.

Mer information finns i [Betalningsalternativ](payments-options.md#google-pay-button).

1. Gå till **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;på sidofältet_ Admin _.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL Google Pay]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Payment Services]_.
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
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=sv-SE) för den angivna betalningsmetoden. Alternativ: `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
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

1. Gå till **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;på sidofältet_ Admin _.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL PayPal payment buttons]_&#x200B;i avsnittet&#x200B;_[!UICONTROL Payment Services]_.
1. Redigera fältet _[!UICONTROL Title]_&#x200B;om du vill ändra namnet på betalningsmetoden så som visas vid utcheckning.
1. Om du vill [ange betalningsåtgärden](production.md#set-payment-services-as-payment-method) väljer du **[!UICONTROL Authorize]** eller **[!UICONTROL Authorize and Capture]**.
1. Om du vill prioritera en betalningsmetod på utcheckningssidan anger du ett `Numeric Only`-värde i fältet **[!UICONTROL Sort order]**.
1. Om du vill aktivera/inaktivera [Betala senare meddelanden](payments-options.md#pay-later-button) väljer du `Yes`/`No` för **[!UICONTROL Display Pay Later Message]**.
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
| [!UICONTROL Payment Action] | webbplats | [betalningsåtgärden](https://experienceleague.adobe.com/sv/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} för den angivna betalningsmetoden. Alternativ: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | webbplats | Aktivera eller inaktivera meddelandet Betala senare i kundvagnen, på produktsidan, i minikundvagnen och under kassaflödet. Alternativ: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
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

1. Gå till **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;på sidofältet_ Admin _.
1. Expandera **[!UICONTROL Sales]** i den vänstra panelen och välj **[!UICONTROL Payment Methods]**.
1. Expandera avsnittet _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Expandera avsnittet _[!UICONTROL PayPal Smart Button Styling]_&#x200B;i avsnittet&#x200B;_[!UICONTROL [!DNL Payment Services]]_.
1. Om du vill ange layouten väljer du `Vertical` eller `Horizontal` för **[!UICONTROL Layout]**
1. Välj bland de tillgängliga färgerna i **[!UICONTROL Color]** för att ange färgen.
1. Ange formen genom att välja `Rectangular` eller `Pill` för **[!UICONTROL Shape]**.
1. Om du vill använda standardhöjden väljer du `Yes` eller `No` för **[!UICONTROL Use Default Height]**.
1. Om du vill ange den anpassade höjden lägger du till önskad pixelhöjd för **[!UICONTROL Height]**.
1. Ange tagline genom att välja `Yes` eller `No` för **[!UICONTROL Tagline]**.
1. Klicka på **[!UICONTROL Save Config]** om du vill spara ändringarna.
1. Navigera till **[!UICONTROL System]** > **[!UICONTROL Cache Management]** och klicka sedan på **[!UICONTROL Flush Cache]** för att uppdatera alla ogiltiga cacheminnen.

Du kan också konfigurera betalningsknappsformateringen [i Inställningar](settings.md#button-style) från startsidan för Betalningstjänster.

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

Om du ändrar konfigurationen tömmer [manuellt cachen](/help/payment-services/settings.md#flush-the-cache) så att butiken visar de senaste konfigurationsinställningarna.
