---
title: '[!DNL Live Search] händelser'
description: Lär dig hur händelser samlar in data för  [!DNL Live Search].
feature: Services, Eventing
exl-id: a9f4f254-d8ff-46f1-8deb-a75b90d70d52
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search] händelser

[!DNL Live Search] använder händelser för att driva sökalgoritmer som&quot;Mest visade&quot; och&quot;Viewed This, Viewed That&quot;. [Commerce Lumatema](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/design/themes/themes#the-default-theme) är inte alltid tillgängligt, men headless-implementeringar och andra anpassade implementeringar måste implementera händelser för sina egna behov.

Den här tabellen beskriver de händelser som används av [!DNL Live Search] [rankningsstrategier](rules-add.md#intelligent-ranking).

| Rankningsstrategi | Händelser | Sida |
| --- | --- | --- |
| Mest visade | `page-view`<br>`product-view` | Produktinformationssida |
| Mest köpta | `page-view`<br>`place-order` | Kassa/kassa |
| Mest tillagt i kundvagn | `page-view`<br>`add-to-cart` | Produktinformationssida<br>Produktlistsida<br>Kundlista<br>Önskad lista |
| Visade det här, såg du att | `page-view`<br>`product-view` | Produktinformationssida |

>[!NOTE]
>
>Datainsamlingen för syftet med [!DNL Live Search] innehåller inte personligt identifierbar information (PII). Alla användaridentifierare, som cookie-ID:n och IP-adresser, är strikt anonymiserade. [Läs mer](https://www.adobe.com/privacy/experience-cloud.html).

## Nödvändiga instrumentpanelshändelser

Vissa händelser krävs för att fylla i [Live Search-instrumentpanelen](performance.md)

| Kontrollpanelsområde | Händelser | Kopplingsfält |
| ------------------- | ------------- | ---------- |
| Unika sökningar | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Inga resultatsökningar | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Nollresultatfrekvens | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Vanliga sökningar | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Medel. klickningsposition | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId` |
| Genomklickningsfrekvens | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId`, `sku`, `parentSku` |
| Konverteringsgrad | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | `searchRequestId`, `sku`, `parentSku` |

### Nödvändiga sammanhang

Alla händelser kräver kontexterna `Page` och `Storefront`. Detta bör ske på sidnivå/butiksprogramlager i stället för när enskilda händelser genereras (i en PHP-butik ansvarar PHP-programbehållaren för att ställa in dem vid körning).

## Användning

Här följer ett exempel på implementering av `search-request-sent`-händelsen:

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## Caveats

- Annonsblockerare och sekretessinställningar kan förhindra händelser från att fångas in och kan göra så att engagemanget och intäktsmåtten [på ](performance.md) inte rapporteras tillräckligt. Dessutom kanske vissa händelser inte skickas på grund av att kunderna lämnar sidan eller nätverksproblem.
- Huvudlösa implementeringar måste implementera händelser för att driva intelligent varuexponering.

>[!NOTE]
>
>Om [läget för cookie-begränsning](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) är aktiverat samlar Adobe Commerce inte in beteendedata förrän kunden samtycker till att använda cookies. Om läget för cookie-begränsning är inaktiverat samlar Adobe Commerce in beteendedata som standard.
