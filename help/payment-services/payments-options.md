---
title: Betalningsalternativ
description: Ange betalningsalternativen för att anpassa de metoder som är tillgängliga för dina butikskunder.
feature: Payments, Checkout, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Betalningsalternativ

Med [!DNL Adobe Commerce] och [!DNL Magento Open Source] [!DNL Payment Services] har du flera betalningsalternativ tillgängliga.

Du kan konfigurera de här betalningsalternativen i [Hem-](payments-home.md) eller [Store-konfigurationen](configure-admin.md) (rekommenderas för äldre betalningsalternativ eller en konfiguration för flera butiker).

Det finns olika beteenden för varje betalningsmetod beroende på var du befinner dig i utcheckningsprocessen:

* Produktsida - produktsidan för en artikel
* Mini cart - Tillgängligt när du klickar på varukorgen när en produkt har lagts till i varukorgen
* Kundvagn - Tillgänglig när du klickar på _Visa och redigera kundvagnen_ från minivagnen
* Utcheckningsvy - Tillgängligt när du klickar på _Fortsätt till utcheckning_ från mini-kundvagn eller kundvagn

>[!IMPORTANT]
>
>[!DNL Payment Services]-introduktionen måste slutföras innan betalningar kan bearbetas.

## Standard vs. Advanced Payments Experience

[!DNL Payment Services] innehåller betalningsalternativ för **Avancerat** (stöds fullt ut) och **Standard** (Express Checkout) samt startflöden, beroende på vilket land du arbetar i.

* **Avancerat** - Alla tillgängliga [betalningsalternativ](../payment-services/payments-options.md) är tillgängliga för aktuella [länder med fullt stöd](../payment-services/overview.md#availability). Under introduktionen för att aktivera livebetalningar väljer du alternativet [Avancerad introduktion](../payment-services/production.md#advanced-onboarding).
* **Standard** - En delmängd av betalningsalternativ (Express Checkout) - PayPal-kort för kredit och debitering - finns för andra tillgängliga länder som stöds. [Kreditkortsfälten](#credit-card-fields) och [Apple Pay](#apple-pay-button) är inte tillgängliga för det här startalternativet. Under introduktionen för att aktivera livebetalningar väljer du alternativet [Standard onboarding](../payment-services/production.md#standard-onboarding).

Se [Aktivera [!DNL Payment Services] för produktion](../payment-services/production.md#complete-merchant-onboarding) för information om hur du slutför avancerad introduktion och standardintroduktion.

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] erbjuder en enkel och säker utcheckning för betalningsmetoder med kreditkort eller betalkort. När en kund checkar ut med kreditkortsfält anger han/hon sitt namn, sin faktureringsadress och kreditkortsinformation för att göra sin beställning. Deras kundinformation används säkert under köpsessionen för att smidigt vägleda dem genom utcheckningsflödet.

![Kreditkortsfält i kassan](assets/credit-card-fields.png){width="500" zoomable="yes"}

Aktivera [kreditkortsvalveringen](#vaulting) för dina butiker så att kunderna kan vault (save) sin kreditkortsinformation för en snabb utcheckning senare.

Du kan konfigurera [!UICONTROL Credit Card Fields] i butikskonfigurationen eller startsidan för [!DNL Payment Services]. Mer information finns i [Inställningar](settings.md#credit-card-fields).

Du kan också ändra layout, bredd, höjd och yttre format för kreditkortsfälten. Mer information finns i [PayPal-dokumentation](https://developer.paypal.com/docs/checkout/advanced/customize/card-field-style/).

## [!DNL Apple Pay]-knapp

Kunder kan använda [[!DNL Apple Pay]](https://www.apple.com/apple-pay/), som använder kreditkortsbetalningsreferenser som lagras på en iOS- eller macOS-enhet, för att göra inköp.

[!DNL Apple Pay] är bara tillgängligt i webbläsaren Safari. Handlare kan lägga till upp till 99 domäner per handelskonto.

![Apple Pay-knappen i minikorgen](assets/applepay-button.png){width="500" zoomable="yes"}

Knappen [!DNL Apple Pay] visas på produktsidan, i minikundvagnen, i kundvagnen och i kassan.

Om du vill använda [!DNL Apple Pay] för dina butiker fyller du i [självregistrering med  [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Registrera endast din livedomän_) och [konfigurerar den för dina butiker i [!DNL Payment Services]](settings.md#payment-buttons).

>[!NOTE]
>
> Se [avancerad utcheckning](https://www.paypal.com/us/cshelp/article/what-is-paypal-advanced-checkout-and-how-do-i-get-started-help953){target=_blank} i dokumentationen för PayPal-utvecklare för att kontrollera hur du gör det möjligt för köpare att betala med Apple Pay på din webbplats.

Du kan konfigurera [!UICONTROL Apple Pay] i butikskonfigurationen eller startsidan för betalningstjänsterna. Mer information finns i [Inställningar](settings.md#apple-pay).

## [!DNL Google Pay]-knapp

Kunder kan använda [[!DNL Google Pay]](https://pay.google.com/about/) genom att lägga till betalningsinformation till sitt Google-konto, där de lagras säkert för en smidig utcheckning.

[!DNL Google Pay] är bara tillgängligt i vissa länder eller regioner och på vissa enheter. Mer information finns i [[!DNL Google Pay] dokumentationen](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration).

![Knappen Google Pay (Betala) i kassan](assets/google-pay-button.png){width="500" zoomable="yes"}

Knappen [!DNL Google Pay] visas på produktsidan, i minikundvagnen, i kundvagnen och i kassan.

Du kan konfigurera [!UICONTROL Google Pay] i butikskonfigurationen eller startsidan för betalningstjänsterna. Mer information finns i [Inställningar](configure-admin.md).

>[!NOTE]
>
> API:t [!DNL Google Pay] kan bara användas på webbplatser i en säker kontext. Mer information finns i [Felsökning](https://developers.google.com/pay/api/web/support/troubleshooting) -dokumentationen.

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons], som använder PayPal för att slutföra ett köp, lagrar kundens leveransadress, faktureringsadresser och betalningsinformation för senare bruk. Köpare kan använda vilken betalningsmetod som helst som tidigare lagrats eller erbjuds av PayPal.

![PayPal-knapp](assets/paypal-button.png){width="350" zoomable="yes"}

Du kan konfigurera [!UICONTROL PayPal payment buttons] i butikskonfigurationen eller startsidan för [!DNL Payment Services]. Mer information finns i [Inställningar](settings.md#payment-buttons).

Lär dig mer om tillgängligheten för betalningsmetoder per land i PayPals [dokumentation om betalningsmetoder](https://developer.paypal.com/docs/checkout/payment-methods/).

### [!DNL PayPal]-knapp

Med PayPal-knappen kan kunderna enkelt och säkert kolla in resultatet.

Knappen [!DNL PayPal] visas på produktsidan, i minikundvagnen, i kundvagnen och i kassan.

### [!DNL Venmo]-knapp

Kunder kan checka ut med knappen [Venmo](https://venmo.com/).

Knappen [!DNL Venmo] visas på produktsidan, i minikundvagnen, i kundvagnen och i kassan.

### PayPal Debit eller kreditkortsknapp

Kunder kan checka ut med PayPal Debit- eller kreditkortsknappen.

Knappen PayPal Debit eller Kreditkort visas på utcheckningssidan.

Det här alternativet kan användas för att visa kunderna ett betalnings- eller kreditkortsalternativ med en PayPal-värdbaserad knapp som ett alternativ till en kreditkortsintegrering.

### [!DNL Pay Later]-knapp

Erbjud dina kunder kortfristiga räntefria betalningar och andra finansieringsalternativ så att de kan köpa nu och betala senare med knappen [!DNL Pay Later].

Knappen [!DNL Pay Later] visas på produktsidan, i minikundvagnen, i kundvagnen och i kassan.

Mer information om erbjudandet om Betala senare finns i [PayPals Betala senare erbjuder dokumentation](https://developer.paypal.com/docs/checkout/pay-later/us/). Använd listrutan **Land eller region** för att välja ett område av intresse.

Lär dig hur du inaktiverar eller aktiverar meddelandet [!DNL Pay Later] genom att uppdatera konfigurationen för [Inställningar](settings.md#payment-buttons).

## Använd endast PayPal-betalningsknappar

Om du snabbt vill försätta din butik i produktionsläge kan du konfigurera _endast_ betalningsknappar för PayPal (Venmo, PayPal osv.)- i stället för att också använda betalningsalternativet PayPal-kreditkort.

På så sätt kan du:

* Ange olika betalningsalternativ för dina kunder, inklusive betalningsknapparna Venmo och PayPal, med möjlighet att stänga av värdkortsfälten för PayPal och använda en befintlig kreditkortsleverantör.
* Använd din befintliga kreditkortsleverantör för kreditkortsbetalningar, samtidigt som du använder PayPals andra betalningsalternativ.
* Använd PayPals betalningsknappar i regioner där PayPal inte stöder kreditkort som betalningsalternativ.

Om du vill **hämta betalningar med _only_ PayPal-betalningsknappar (_inte_ betalningsalternativet PayPal-kreditkort)**:

1. Kontrollera att din butik är [i produktionsläge](settings.md#enable-payment-services).
1. [Konfigurera önskade PayPal-betalningsknappar](settings.md#payment-buttons) i Inställningar.
1. Stäng av _Av_, alternativet **[[!UICONTROL Show PayPal Credit and Debit card button]](settings.md#payment-buttons)** i avsnittet _[!UICONTROL Payment buttons]_.

Så här **tar du emot betalningar med din befintliga kreditkortsleverantör _och_ betalningsknappar för PayPal**:

1. Kontrollera att din butik är [i produktionsläge](settings.md#enable-payment-services).
1. [Konfigurera önskade PayPal-betalningsknappar](settings.md#payment-buttons).
1. Stäng av _Av_, alternativet **[[!UICONTROL PayPal Show Credit and Debit card button]](settings.md#payment-buttons)** i avsnittet _[!UICONTROL Payment buttons]_.
1. Aktivera alternativet _Av_ **[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)** i avsnittet _[!UICONTROL Credit card fields]_&#x200B;och använd ditt [befintliga kreditkortsleverantörskonto](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html#payments).

## Orderomberäkning

När en kund går in i kassan från minikorgen, kundvagnen eller produktsidan dirigeras de till en ordergranskningssida där de kan se den valda leveransadressen i ett popup-fönster i PayPal. När kunden har valt leveranssätt beräknas orderbeloppet om på lämpligt sätt och kunden kan se fraktkostnader och skatter.

När en kund går in i utcheckningsflödet från utcheckningssidan är systemet redan medvetet om leveransadressen och det slutliga beräknade beloppet, och summorna representeras korrekt.

Skattehelgdagar, fraktkostnader och moms kan variera mycket mellan olika platser. När [!DNL Payment Services] har tagit emot leveransadressen och fraktkostnaden beräknas alla tillämpliga kostnader snabbt om och visas korrekt under de sista stegen i utcheckningen.

## Kreditkortssäkringar

Köpare kan vault - eller&quot;save&quot; - deras kreditkortsinformation för framtida inköp på webbplatsnivå (vilken butik som helst på samma handlares konto).

Mer information finns i [Kreditkortssäkringar](vaulting.md).

## Säkerhet

Mer information finns i [PCI-kompatibilitet](security.md#pci-compliance).
