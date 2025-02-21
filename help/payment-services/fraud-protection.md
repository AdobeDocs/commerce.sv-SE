---
title: Skydd mot signering av bedrägeri
description: Aktivera automatiskt bedrägeriskydd för  [!DNL Payment Services] med signering.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Skydd mot bedrägeri

Du kan aktivera automatiskt bedrägeriskydd för [!DNL Payment Services] med tillägget [Signera](https://commercemarketplace.adobe.com/signifyd-module-connect.html).

Adobe Commerce har stöd för Signifyd version 5.4.0 och senare. [!DNL Payment Services] har stöd för signeringsflöden före och efter autentisering.

Integreringen Signifyd/[!DNL Payment Services] ger täckning för kreditkort, debetkort, vaultkort, utcheckning via Admin samt betalningsmetoderna PayPal och Apple Pay. Vissa detaljer om transaktionerna delas inte mellan Betalningstjänster och Signifyd, men Signifyd erbjuder en omfattande risktäckning för alla betalningsmetoder och garanterar ett så gott skydd som möjligt.

Mer information om hur du installerar och konfigurerar tillägget finns i [Signera dokumentation](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension).

## Onboarding

Du måste kommunicera direkt med Signifyd för att kunna ta med tillägget för användning med [!DNL Payment Services] - det behövs ingen [!DNL Payment Services]-konfiguration. Du kan konfigurera signeringstillägget i Admin när det har installerats. Allt stöd som hör till det här tillägget hanteras av Signifyd.

Vid introduktion med Signifys måste du:

1. Kontakta Signified om du vill konfigurera ett nytt konto.
1. Signifyd är som standard [tillåtslista](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md) för att säkerställa att Signifyd inte aktiveras för andra betalningsalternativ som för närvarande inte stöds. Om du vill förbjuda en viss betalningsmetod måste du göra ändringar.
1. Bekräfta med Signifyd att PayPal inte kommer att avslå beställningar, via handlarens inställning för bedrägeriskydd i Paypal, som skulle kunna godkännas av Signifyd.
1. Aktivera signeringstillägget så att det är kompatibelt med [!DNL Payment Services]:
   * När du använder [!DNL Payment Services] i _Live_-läge måste Signify vara i produktionsläge.
   * När du använder [!DNL Payment Services] i läget _Sandbox_ måste Signify vara i testläge.

## Konfiguration

Eftersom Signified utför en åtgärd på dina beställningar är det nödvändigt att konfigurera tillägget så att det beter sig korrekt baserat på den betalningsåtgärd som du har angett för [!DNL Payment Services].

De här konfigurationsalternativen är inte kompatibla med betaltjänster och signeringsintegrering:

* När [!DNL Payment Services] har konfigurerats med `Authorize` betalningsåtgärden _och_ Signifyd är i läget `PostAuth` med alternativet _[!UICONTROL Decline Guarantees]_inställt på&#x200B;**Skapa kreditnota**.

  Orsak: [!DNL Payment Services] skapar en auktoriseringstransaktion som Signify sedan försöker återbetala.


* [!DNL Payment Services] har konfigurerats med `Authorize and Capture` betalningsåtgärd _och_ Signifyd är i `PostAuth`-läge med alternativet _[!UICONTROL Decline Guarantees]_inställt på&#x200B;**Avbryt order**.

  Orsak: [!DNL Payment Services] skapar en hämtningstransaktion som Signified sedan försöker annullera.


Mer information om hur [konfigurerar tillägget](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension) finns i Signera dokumentation.

Läs Signera dokumentation för att [lära dig mer om orderarbetsflödena](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works).
