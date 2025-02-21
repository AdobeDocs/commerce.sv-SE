---
title: Konfigurera testsandlådan
description: Använd ett PayPal-sandlådekonto om du vill använda  [!DNL Payment Services]  i testläge.
feature: Payments, Checkout, Configuration, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Konfigurera testsandlådan

Innan du påbörjar introduktionen av sandlådor måste du registrera dig för ett kostnadsfritt PayPal-utvecklarkonto och skapa både handlare (som ska användas för introduktion) och kundkonton (som ska användas för att testa utcheckningen). Du kan skapa flera utvecklarkonton om du vill.

Med ett PayPal-sandlådekonto kan du använda [!DNL Payment Services] i testläge. PayPal kräver att du använder ett PayPal Developer Portal-genererat Business Sandbox-testkonto, e-post och lösenord för sandlådeintroduktion. *Skapa inte ett annat konto under sandlådeintroduktionsprocessen.*

## Sandbox-introduktion

Så här slutför du introduktionen av sandlådor:

1. Gå till sidan [PayPal Developer Account](https://developer.paypal.com/developer/accounts/).
1. Klicka på **[!UICONTROL Log in to Dashboard]** och logga in med ditt befintliga PayPal Developer Portal-genererade Business Sandbox-testkonto eller klicka på **Registrera dig** för att skapa ett konto.
1. Skapa ett PayPal-sandlådekonto:
   1. Gå till _[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**.
   1. Klicka på **[!UICONTROL Create account]**.

      Om du skapade ett PayPal-sandlådekonto under PayPal-introduktionsprocessen i sandlådan måste du [återställa din introduktionssandlåda](#reset-your-sandbox-account) eftersom du inte kan verifiera din e-post.

   1. Välj **[!UICONTROL Business]** som kontotyp och klicka på **[!UICONTROL Create]**.
   1. Klicka i avsnittet _[!UICONTROL Sandbox Accounts]_på de tre punkterna i kolumnen_[!UICONTROL Manage accounts]_ för sandlådekontot som du skapade.
   1. Klicka på **[!UICONTROL View/edit account]**.

      ![PayPal - Visa/redigera sandlådekonto](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. Kopiera och spara e-post-ID och systemgenererat lösenord för framtida bruk.

1. Gå till **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** på sidofältet _Admin_.
1. Klicka på **[!UICONTROL Sandbox onboarding]**.

   Det här alternativet är synligt om du ännu inte har slutfört introduktionen av sandlådan för [!DNL Payment Services].

   Ett handlar-ID för sandlådan genereras automatiskt och fylls i i [inställningarna](settings.md). Ändra eller ändra inte detta ID.

   Du får ett PayPal-fönster där du kan ansluta ett PayPal-konto för att börja acceptera betalningar.

1. Ange e-postadress och lösenord för PayPal-sandlådekontot som du skapade i steg 3 (inte din PayPal-kontoinformation) och ditt land eller din region.
1. Klicka på **[!UICONTROL Next]**.

   ![PayPal - Anslut PayPal-konto för betalningar](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. Fortsätt att följa PayPal-flödet med dina tidigare sparade inloggningsuppgifter för sandlådekonton.
1. Gå till **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** på sidofältet _Admin_.

   Knappen **[!UICONTROL Sandbox onboarding]** är inte längre synlig och du ser texten&quot;väntande sandlådebetalningar&quot;.

När din introduktion till PayPal-sandlådan har godkänts bör du se ett meddelande om att ditt betalningssystem för närvarande är i sandlådeläge och inte hanterar livesändningar.

>[!IMPORTANT]
>
>Om du återkallar samtycke till [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] för att bearbeta dina betalningar (i dina PayPal-kontoinställningar) kan beställningar i din butik inte bearbetas av [!DNL Payment Services]. En varning om det återkallade medgivandet visas på startsidan för Betalningstjänster. Klicka på **[!UICONTROL Do not show again]** om du vill stänga varningen.

### Återställ ditt sandlådekonto

Om du skapade ett PayPal-sandlådekonto under PayPals introduktionsprocess i sandlådan måste du återställa din introduktionssandlåda eftersom du inte kan verifiera din e-post.

Så här återställer du ditt sandlådekonto:

1. Klicka på **[!UICONTROL Reset sandbox]**. [Skapa ett PayPal-affärssandlådekonto](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account).
1. Klicka på **[!UICONTROL Sandbox onboarding]** och slutför nästa uppsättning steg.

## Aktivera telefonnummer för kontakt

Med telefonnumret kan du få de telefonnummer som PayPal samlar in från dina kunder. PayPal samlar alltid in kontakttelefonnummer från PayPal-kontoinnehavare för att hjälpa dem att bekräfta sina identiteter och kontakta dem för att lösa problem på sina konton eller för att slutföra sina leveransprocesser. PayPal rekommenderar dock inte att telefonnummer används direkt från handlaren eftersom det kan påverka försäljningen negativt. Mer information finns i dokumentationen för [PayPal get-kontakttelefonnummer](https://www.sandbox.paypal.com/businessmanage/preferences/website).

Den här funktionen är `off` som standard. När du aktiverar det kan butiksadministratörer se telefonnummer när en kund slutför ett flöde för profilerad utcheckning utanför utcheckningssidan.

>[!IMPORTANT]
>
>Den här inställningen gäller inte andra utcheckningsflöden.

## Testa i sandlådemiljö

Vi rekommenderar att du använder testdatamängder för integrering och testmiljöer, och testar produktionsbetalningar med riktiga kreditkort och banker innan du exponerar den här funktionen för kunderna.

Mer information finns i [Testa och validera](test-validate.md).
