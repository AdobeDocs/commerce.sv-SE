---
title: Aktivera [!DNL Payment Services] för produktion
description: Slutför introduktionsprocessen genom att aktivera  [!DNL Payment Services]  för produktion.
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Aktivera [!DNL Payment Services] för produktion

Du kan sätta igång tjänsten och slutföra [introduktionsprocessen](onboard.md) enligt stegen i det här avsnittet efter att du:

* [!BADGE PaaS endast]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."} [Installera](install.md) tillägget Betalningstjänster
* [!BADGE Endast PaaS]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."} [Konfigurera och ansluta](connect.md) din instans
* [Konfigurera](sandbox.md) och [testa](test-validate.md) din sandlåda

## Ange [!DNL Payment Services] som betalningsmetod

När du har [konfigurerat dina Commerce-tjänster](connect.md#configure-commerce-services) och aktiverat antingen [sandlådetestning](sandbox.md#enable-sandbox-testing) eller [direktbetalningar](#enable-live-payments) måste du ange [!DNL Payment Services] som betalningsmetod.

1. Gå till _>_ på sidofältet **[!UICONTROL Sales]** Admin **[!UICONTROL Payment Services]**.
1. Klicka på **[!UICONTROL Enable Payment Services]**.

   Det här alternativet är synligt om du ännu inte har konfigurerat [!DNL Payment Services] som betalningsmetod för en eller flera av dina webbplatser.

   Du dirigeras till inställningsområdet i hemvyn med de relevanta alternativen utökade (**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_), där du kan aktivera [!DNL Payment Services]-alternativen som [betalningsmetod](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}.

1. I _[!UICONTROL General Configuration]_anger du **[!UICONTROL Enable]**till `Yes`.
1. Ange **[!UICONTROL Payment Action]** för både _[!UICONTROL Credit Card Fields]_och_[!UICONTROL PayPal payment buttons]_ till något av följande:

   | Inställning | Beskrivning |
   |---|---|
   | `Authorize` | Godkänner köpet och spärrar medlen. Beloppet dras inte tillbaka förrän handlaren&quot;fångar&quot; det. |
   | `Authorize and Capture` | Godkänner köpet och handlaren&quot;fångar&quot; pengarna. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] har stöd för partiella klipp. En handlare kan delvis hämta (fakturera) delar av en order. Du kan till exempel hämta varje objekt individuellt, eller ett objekt nu och resten senare.

1. Klicka på **[!UICONTROL Save]**.
1. Klicka på **[!UICONTROL Go to Payment Services]** om du vill gå tillbaka till startsidan för [!DNL Payment Services].
1. [Rensa cachen](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html).

   Rensning bör göras efter varje konfigurationsändring.

Mer information om hur du konfigurerar kreditkortsfält och PayPal-betalningsknappar finns i [Konfigurera [!DNL Payment Services]](configure-admin.md).

## fullständig registrering av handlare

Nästa steg på vägen mot att göra era butiker tillgängliga med betaltjänster är att slutföra direktintroduktionen.

Betalningstjänster tillhandahåller [**avancerade** (stöds fullt ut) och **Standard** (Express Checkout) betalningsalternativ](../payment-services/payments-options.md#standard-vs-advanced-payments-experience) och startflöden, beroende på vilket land du arbetar i och vilken betalningsupplevelse du föredrar.

1. Gå till _>_ på sidofältet **[!UICONTROL Sales]** Admin **[!UICONTROL Payment Services]**.
1. Klicka på **[!UICONTROL Live onboarding]**.

   Det här alternativet är synligt om du ännu inte har slutfört live-introduktionen för [!DNL Payment Services].

1. I _Välj land_ väljer du det land du arbetar från.

   Betalningstjänster ger fullständigt stöd för alla betalningsalternativ i [fem länder](../payment-services/introduction.md#availability) för närvarande. Betalningstjänster erbjuder funktioner för Express Checkout (en deluppsättning av betalningsalternativ) för alla andra länder som finns representerade i landslistan.

   Det land du väljer i listan avgör vilka betalningsalternativ och vilket introduktionsflöde -[Avancerat](#advanced-onboarding) (stöds fullt ut) eller [Standard](#standard-onboarding) (Express Checkout) - som är tillgängliga för dig.

>[!TIP]
>
> När du valt och fortsätter med ett introduktionsalternativ - Standard eller Avancerat - måste du slutföra introduktionen på nytt för att antingen uppgradera eller nedgradera från det ursprungliga valet.

### Avancerad introduktion

Det här introduktionsflödet är tillgängligt för handlare i [länder som stöds fullt ut](../payment-services/introduction.md#availability).

När landet har valts:

1. Välj **Avancerat** i det modala som visas.

   För alternativet **Standard** fortsätter du till [standardstartflödet](#standard-onboarding).

1. Klicka på **Fortsätt**.
1. Fortsätt med PayPal-flödet för avancerad introduktion som stöds fullt ut med dina PayPal-kontoinloggningsuppgifter (inte dina autentiseringsuppgifter för sandlådekonton) _eller_ och registrera dig för ett nytt PayPal-konto.

>[!IMPORTANT]
>
>**Avancerad introduktion** kräver att handlare [begär betalningsbehörighet](#request-payments-entitlement-from-adobe) för att aktivera live-introduktion.

### Standard onboarding

Det här standardintroduktionsflödet är tillgängligt för handlare i tillgängliga länder där [endast support för Express Checkout ](../payment-services/introduction.md#availability) tillhandahålls.

När landet har valts:

1. Klicka på länken _Betalningstjänstavtal_ i det spärrade **avtalet för betaltjänster** för att visa avtalet för Adobe Commerce betaltjänster.
1. Klicka på _Jag accepterar_ i det spärrade **avtalet för betaltjänster**.
1. Fortsätt med PayPal-flödet för Express Checkout-introduktion, med dina PayPal-kontoinloggningsuppgifter (inte dina autentiseringsuppgifter för sandlådekonton) eller registrera dig för ett nytt PayPal-konto.

>[!IMPORTANT]
>
>[Apple Betala- och kreditkortsfält](../payment-services/payments-options.md) är inte tillgängliga för **Standard onboarding**.

## Bekräfta e-postadress

1. Gå till **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** på sidlisten Admin

   Knappen _[!UICONTROL Live onboarding]_visas inte längre och du ser textrutan [!UICONTROL Live payments pending].

   I den textrutan kan du också bli ombedd att bekräfta din e-postadress hos PayPal för att slutföra introduktionen.

1. Om du uppmanas att bekräfta din e-postadress kontrollerar du om det finns ett bekräftelsemeddelande från PayPal i din e-postadress och klickar för att bekräfta din e-postadress.
1. Gå till **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** på sidlisten Admin.
1. Uppdatera webbläsarfönstret.

   När din PayPal-handlares introduktion har godkänts bör du se ett meddelande om att ditt betalningssystem är i sandlådeläge och inte hanterar livebetalningar.

   >[!IMPORTANT]
   >
   >Om du återkallar samtycke till [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] för att bearbeta dina betalningar (i dina PayPal-kontoinställningar) kan beställningar i din butik inte bearbetas av [!DNL Payment Services]. På startsidan för betalningstjänsterna visas en varning om det återkallade medgivandet.

## Begär berättigande för betalningar från Adobe

Om du vill att dina butiker ska kunna publiceras begär du betalningstillstånd från Adobe (för [endast avancerad introduktion](#advanced-onboarding)):

1. Gå till _>_ på sidofältet **[!UICONTROL Sales]** Admin **[!UICONTROL Payment Services]**.
1. Klicka på **[!UICONTROL Get Live Payments]** på startsidan för [!DNL Payment Services].

   ![Begär berättiganden](assets/request-entitlements.png){width="500" zoomable="yes"}

1. Fyll i formuläret.
1. En medlem i säljteamet kommer att kontakta dig.

Du kan också begära betalningstillstånd från Adobe på [business.adobe.com](https://business.adobe.com/resources/payment-services.html).

>[!IMPORTANT]
>
>**Live-introduktion** är inte tillgänglig förrän betalningsberättigandet har godkänts.

## Konfigurera prisnivå

Hämta ditt [!DNL Payment Services] _handels-ID_:

1. Gå till _>_ på sidofältet **[!UICONTROL Sales]** Admin **[!UICONTROL Payment Services]**.
1. Klicka på **[!UICONTROL Settings]** i hemvyn. Mer information finns i [Hem](payments-home.md).
1. Välj det _Merchant ID_ som krävs och skicka det till din försäljningsrepresentant som konfigurerar rätt prisnivå.

Mer information om betalningstransaktioner finns i [Nivå 2- och Nivå 3-bearbetning](levels-card-payment-transactions.md).

## Aktivera direktbetalningar

Ett _handlar-ID för produktion_ genereras automatiskt och fylls i i [konfigurationen](configure-admin.md). Ändra eller ändra inte detta ID.

Aktivera direktbetalningar:

1. Gå till _>_ på sidofältet **[!UICONTROL Sales]** Admin **[!UICONTROL Payment Services]**.
1. Klicka på **[!UICONTROL Settings]** längst upp till höger på sidan på Hem. Mer information finns i [Hem](payments-home.md).
1. I avsnittet _[!UICONTROL General Configuration]_ställer du in **[!UICONTROL Payment mode]**på `Production`.
1. Klicka på **[!UICONTROL Save]**.
1. [Rensa cachen](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"}.

   >[!IMPORTANT]
   >
   >Om du inte rensar ditt cacheminne kan kunderna inte se betalningsalternativ för PayPal under utcheckningen.

Om du går tillbaka till startsidan för [!DNL Payment Services] visas inte längre meddelandet om sandlådeläge eftersom du nu bearbetar direktbetalningar.

Se [Konfigurera i Admin](configure-admin.md) för äldre konfigurationsalternativ.

>[!IMPORTANT]
>
>Om du återkallar samtycke till [!DNL Payment Services] för bearbetning av dina betalningar (i dina PayPal-kontoinställningar) kan beställningar i din butik inte bearbetas av [!DNL Payment Services]. Om du vill återaktivera betalningshanteringen måste du slutföra introduktionen igen. På startsidan för betalningstjänsterna visas en varning om det återkallade medgivandet.

## Test i produktion

Vi rekommenderar att du testar produktionsbetalningar med riktiga kreditkort och banker innan du exponerar denna funktion för kunderna.

Mer information finns i [Testa och validera](test-validate.md).
