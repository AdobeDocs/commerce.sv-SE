---
title: Verifiera händelsesamling
description: Lär dig hur du kontrollerar att beteendedata skickas till Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Verifiera händelsesamling

När du har [installerat och konfigurerat](install-configure.md) modulen `magento/product-recommendations` kan du verifiera att beteendedata skickas till Adobe Commerce. Du kan använda utvecklarverktygen i Chrome eller installera tillägget Snowplow Chrome. Om du behöver mer hjälp kan du läsa [Felsök [!DNL Product Recommendations] modulen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html?lang=sv-SE) i kunskapsbasen med supportfrågor.

## Verifiera med utvecklarverktygen i Chrome

Så här ser du till att händelsesamlarens JS-fil läses in på alla webbplatssidor:

1. I Chrome väljer du **Anpassa och styr Google Chrome** och sedan **Fler verktyg** > **Utvecklarverktyg**.
1. Välj fliken **Nätverk** och välj sedan typen **JS** .
1. Filter för `ds.`
1. Läs in sidan igen.
1. Du bör se `ds.js` eller `ds.min.js` i kolumnen **Namn**.

![Händelseinsamlings-JS](assets/filter-ds.png)
_Händelseinsamlings-JS_

Så här ser du till att händelser utlöses på sidor på din webbplats (hem, produkt, utcheckning och så vidare):

1. Se till att du inaktiverar alla annonsblockerare i webbläsaren och godkänner cookies på webbplatsen.
1. I Chrome väljer du **Anpassa och styr Google Chrome** (de tre lodräta prickarna i webbläsarens övre högra hörn) och sedan **Fler verktyg** > **Utvecklarverktyg**.
1. Välj fliken **Nätverk** och filtrera efter `tp2`.
1. Läs in sidan igen.
1. Anrop under `tp2` ska visas i kolumnen **Namn**.

![Startar händelser](assets/filter-tp2.png)
_Verifiera att händelser utlöses_

## Verifiera med Snowplow Chrome-tillägg

Installera felsökningstillägget [Snowplow Analytics för Chrome](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm). Det här tillägget visar de händelser som samlas in och skickas till Adobe Commerce.

1. Se till att du inaktiverar alla annonsblockerare i webbläsaren och godkänner cookies på webbplatsen.

1. I Chrome väljer du **Anpassa och styr Google Chrome** (de tre lodräta prickarna i webbläsarens övre högra hörn) och sedan **Fler verktyg** > **Utvecklarverktyg**.

1. Välj fliken **Felsökning för Snowplow Analytics**.

1. Under kolumnen **Händelse** väljer du **Strukturerad händelse**.

1. Bläddra nedåt tills du ser **kontextdata _n_**. Leta efter storefront-instansen i **Schema**.

1. Kontrollera att [SaaS-datamrådets ID ](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html?lang=sv-SE) är rätt inställt.

![Snöpfilter](assets/snowplow-filter.png)
_Snöpfilter_

>[!NOTE]
>
> Värdet `Data validity : NOT FOUND` i felsökaren anger ett internt schema. Snowplow Chrome-plugin kan inte validera händelser med ett internt schema. Detta påverkar inte den faktiska funktionaliteten.

## Verifiera att händelser utlöses korrekt

Kontrollera att händelserna som används för mätvärden utlöses korrekt genom att leta efter händelserna `impression-render`, `view` och `rec-click` i Felsökning för Snowplow Analytics. Se den fullständiga listan [med händelser](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html?lang=sv-SE).

>[!NOTE]
>
> Om [läget för cookie-begränsning](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=sv-SE) är aktiverat samlar Adobe Commerce inte in beteendedata förrän kunden godkänner det. Om läget för cookie-begränsning är inaktiverat samlas beteendedata in som standard.
