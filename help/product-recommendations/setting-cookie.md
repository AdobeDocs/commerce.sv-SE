---
title: Hantera cookie-begränsningar
description: Läs om hur produktrekommendationer hanterar begränsningar av cookies.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Hantera cookie-begränsningar

Både Adobe Commerce och Magento Open Source ber om samtycke innan data lagras i webbläsarcookies. Mer information finns i [Begränsningsläge för cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=sv-SE).

När du distribuerar modulen `magento/product-recommendations` till produktionen börjar den samla in interaktionshändelser för kunderna på din butik. Eftersom data för de här händelserna kan lagras i webbläsarcookies eller lokal lagring stöder funktionen läget för begränsning av cookies genom att inte samla in händelser förrän kunden har gett sitt samtycke till cookies.

Detta kanske inte fungerar med cookie-lösningar från tredje part. Det är varje handlares ansvar att se till att datainsamlingen inte sker innan cookie-samtycke har lämnats, vilket ofta krävs enligt lag. Om du hanterar cookie-samtycke med anpassad kod kan du använda en cookie som kallas för att inte spåra `mg_dnt` för att begränsa datainsamlingen.

- Namn på cookie:

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- Ställ in Do-not-track-cookie för att inaktivera datainsamling:

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- Så här rensar du cookie-filen när användaren har accepterat cookies:

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
