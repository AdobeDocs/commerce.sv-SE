---
title: Testa och validera
description: Testning och validering säkerställer att  [!DNL Payment Services] funktioner fungerar som förväntat och ger de bästa betalningsalternativen för dina kunder
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 91a4b8fa7228fb91c8ee0bf0a1623d104f061894
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Testa och validera

Innan du visar [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] för dina kunder är det en bra idé att testa _och_ i din sandlådemiljö i produktionen. Testning och validering hjälper till att säkerställa att [!DNL Payment Services]-funktioner fungerar som förväntat och tillhandahåller de bästa betalningsalternativen för din butik och dina kunder.

## Testa i sandlådemiljö

Testning av [!DNL Payment Services] i en sandlådemiljö är ett viktigt valideringssteg, även om det är en simulerad miljö som bara är ansluten till PayPal-sandlådan, inte till riktiga banker och handlare.

1. Slutför en utcheckning från din butik, antingen med [Kreditkortsfält](payments-options.md#credit-card-fields) eller någon av [betalningsknapparna för PayPal](payments-options.md#paypal-smart-buttons). Mer information om hur du använder falska kreditkort för testning finns i [Testa autentiseringsuppgifter](#testing-credentials).
1. Fånga (när din betalningsåtgärd är [inställd på `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)), [återbetalning](refunds.md) eller [void](voids.md) den senast slutförda ordern. Du kan också [skapa en faktura](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"} för en order om betalningsåtgärden är inställd på `Authorize` i stället för `Authorize and Capture`.
1. Visa transaktionen och annan information i [Utbetalningsrapporten](payouts.md) inom 24-48 timmar.
1. Se information om ordern i rapporten [Status för orderbetalning](order-payment-status.md).

### Testa lokala utvecklingsmiljöer

Om du testar betalningsmetoderna PayPal, PayLater och Venmo i lokala utvecklingsmiljöer måste din miljö vara tillgänglig från Internet. Dessa betalningsmetoder använder ett [serverbaserat återanrop](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/) som kräver att PayPal kommunicerar med din Commerce-instans för att hämta leveransalternativ och beräkna summor.

>[!INFO]
>
>Utan en URL som är tillgänglig för Internet fungerar inte återanropet för leverans, vilket ger ett annat utcheckningsflöde än produktionen. Testa alltid med en tillgänglig URL för att säkerställa korrekta resultat.

Så här visar du din lokala miljö:

1. Använd en tunnlingstjänst som [ngrok](https://ngrok.com/) för att skapa en allmänt tillgänglig URL för din lokala miljö.

1. Uppdatera konfigurationen för Commerce bas-URL så att den matchar ngrok-URL:

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. Slutför testningen med betalningsmetoderna PayPal, PayLater eller Venmo.

1. Återställ den ursprungliga bas-URL-konfigurationen när testningen är klar.

Om slutpunktens svarstid är mindre än 5 sekunder visas ett felmeddelande i popup-fönstret.

#### Lokal utveckling av Apple Pay

Apple Pay kräver ytterligare konfiguration för lokal utveckling. Apple Pay använder domänregistrering för att verifiera att din webbplats har behörighet att acceptera Apple Pay-betalningar. Detta innebär att Apple måste kunna nå din domän för att validera en domänverifieringsfil på `/.well-known/apple-developer-merchantid-domain-association`.

För lokal utveckling måste miljön uppfylla följande krav:

* **Offentligt tillgänglig**, Apple måste kunna nå din domän från Internet.
* **HTTPS-protokoll**, Apple Pay fungerar bara på säkra anslutningar.

Om du använder en tunnlingstjänst som [ngrok](https://ngrok.com/) uppfyller båda kraven. När du har konfigurerat ngrok enligt beskrivningen ovan [registrerar du din sandlådedomän](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains) med PayPal med URL:en **ngrok** .

### Testa autentiseringsuppgifter

När du testar och validerar din sandlåda måste du använda falska kreditkortsnummer, så att du inte skapar riktiga avgifter för ett befintligt kreditkortskonto.

Använd PayPals kreditkortsgenerator för att [generera slumpmässig kreditkortsinformation](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) för testning.

Så här testar du Apple Pay i sandlådeläge:

* Skapa ett [Apple-konto för sandlådeprovare](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account), komplett med falska kreditkort och faktureringsinformation.
* [Registrera dina sandlådedomäner](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains).

>[!NOTE]
>
>PayPals betalningshantering i sandlådan är ibland långsam och tjänsten kan ibland gå ner. Denna situation är inte en indikation på hur snabb och effektiv handläggningen av produktbetalningar är.

## Test i produktion

Vi rekommenderar att du testar [!DNL Payment Services] i produktionen, med riktiga kreditkort och banker, innan du visar den här funktionen för kunderna. Även om det är viktigt att testa [!DNL Payment Services] i sandlådan är testning i produktion den mest dummista metoden för att säkerställa att [!DNL Payment Services] fungerar som förväntat.

Du kan testa [!DNL Payment Services] i produktionen på ett av två sätt:

* Välj en tid då du vet att kunderna inte kommer att beställa.
* Använd en webbutik som tillfälligt inte är tillgänglig för kunderna, men som är tillgänglig för dig för testning.

Slutför produktionstestningen med riktiga kreditkort och PayPal-konton och testa betalningens hela livscykel, inklusive hämtning och återbetalning. Om du slutför hela utcheckningen och betalningsflödet under testningen får du den tydligaste bilden av hur din [!DNL Payment Services]-funktion kommer att fungera när kunder använder den.

Du bör också kontrollera att informationen som visas på kontoutdragen för betalningsmetoderna som du använder i produktionstestningen är korrekt och förväntad (inklusive beskrivningen av ditt företag).

### Testa Apple Pay i produktionen

Om du vill testa Apple Pay i produktionsläge måste du [registrera dina produktionsdomäner](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).
