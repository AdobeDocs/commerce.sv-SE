---
title: Felsökning [!DNL App Management]
description: Lös vanliga problem med appassociation och konfiguration.
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Felsökning av [!DNL App Management]

Använd följande lösningar för att lösa vanliga problem med appassociering och konfiguration.

## Appen visas inte

Om programmet inte visas i listan efter distributionen kontrollerar du följande steg:

1. Kontrollera att appen är distribuerad och tillgänglig i din organisation.

1. Bekräfta att du är inloggad på rätt Adobe-organisation i Developer Console.

1. Kontrollera att appen är redo att ansluta (apputvecklaren eller partnern kan bekräfta).

Om appen fortfarande inte visas kontaktar du apputvecklaren eller går till [Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} -dokumentationen för att få teknisk information.

## Synkroniseringen av scopet misslyckades

Om scopesynkroniseringen misslyckas när du associerar en app kan du försöka med följande:

1. Kontrollera att din Commerce-instans är tillgänglig och online.

1. Kontrollera att dina API-autentiseringsuppgifter är giltiga och har rätt behörigheter.

1. Försök synkronisera manuellt från **[!UICONTROL Manage Scopes]** i appkonfigurationen.

## Konfigurationen har inte sparats

Om konfigurationsändringarna inte sparas kan du försöka med följande:

1. Kontrollera att alla obligatoriska fält är ifyllda och giltiga.

1. Kontrollera att du har rätt behörighet för att ändra appkonfigurationen.

1. Prova att uppdatera sidan och spara igen.

Om problemet kvarstår kan du kontrollera om det finns fel i webbläsarkonsolen eller kontakta apputvecklaren.

Mer information om teknisk felsökning finns i [Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}.
