---
title: Översikt över ansikten
description: Lär dig mer om aspekter i [!DNL Adobe Commerce Optimizer] och hur de förbättrar sökresultaten.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: b786a8675625dc969b9542b4b4f716de5342c1af
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---

# Fasetter

Ansikten är en metod för högpresterande filtrering som använder flera dimensioner av attributvärden som sökvillkor.

![Filtrerade sökresultat](../../assets/storefront-search-results-run.png)

Inom en aspekt kan kunderna välja flera alternativ, till exempel&quot;Grundläggande&quot; och&quot;Snug&quot; under&quot;Format&quot; och sökresultaten uppdateras så att endast dessa format visas. På samma sätt gäller att om en kund väljer alternativ i olika aspekter, till exempel&quot;Grundläggande&quot; under&quot;Format&quot; och&quot;Inomhus&quot; under&quot;Klimatteknik&quot;, uppdateras sökresultaten så att den valda stilen och det valda klimatet visas.

Alla definierade aspekter kan användas som URL-parametrar och resultaten filtreras baserat på parametervärdena: `http://yourstore.com?brand=acme&color=red`.

## Fasettaggregering

Akettaggregering utförs enligt följande: Om butiken har tre aspekter (kategorier, färg och pris) och shopparfiltren på alla tre (färg = blå, priset är från 10,00-50,00, kategorier = `promotions`).

- `categories`-aggregering - Aggregerar `categories` och tillämpar sedan filtren `color` och `price`, men inte filtret `categories`.
- `color`-aggregering - Aggregerar `color` och tillämpar sedan filtren `price` och `categories`, men inte filtret `color`.
- `price`-aggregering - Aggregerar `price` och tillämpar sedan filtren `color` och `categories`, men inte filtret `price`.

## Standardattributvärden

Följande produktattribut används av [!DNL Adobe Commerce Optimizer] och aktiveras som standard.

| Egenskap | Beskrivning | Attribut |
|---|---|---|
| Sorterbar | Används för sortering i produktlista | `price` |
| Sökbart | Använd i sökning | `price` <br />`sku`<br />`name` |

Se [API:t för datainmatningsmetadata](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) om du vill veta mer om produktattribut och deras egenskaper.

## Sök och expandera söktyper i flera lager

Sökning i flera lager, eller sökning i en sökning, är ett attributbaserat filtreringssystem som utökar den traditionella sökfunktionen så att den inkluderar ytterligare sökparametrar. Dessa ytterligare sökparametrar ger en mer exakt och flexibel produktupptäckt.

Med sökning i flera lager kan du

- Gör det möjligt för kunderna att söka i sökresultaten.
- Använd `startsWith` och `contains` sökindexering i det andra lagret i sökningen med lager om du vill förfina resultatet ytterligare.

De avancerade sökfunktionerna implementeras via parametern `filter` i [`productSearch` query &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) med hjälp av specifika operatorer:

- **Skiktad sökning** - Sök i ett annat söksammanhang - Med den här funktionen kan du utföra upp till två söklager för dina sökfrågor. Exempel:

   - **Layer 1-sökning** - Sök efter &quot;motor&quot; på `product_attribute_1`.
   - **Layer 2 search** - Search for &quot;part number 123&quot; on `product_attribute_2`. Det här exemplet söker efter &quot;part number 123&quot; i resultatet för &quot;engine&quot;.

  Skiktad sökning är tillgänglig för både `startsWith`-sökindexering och `contains`-sökindexering i det andra lagret i sökningen med lager, vilket beskrivs nedan:

- **börjarMed sökindexering** - Sök med `startsWith`-indexering. Den här funktionen tillåter:

   - Söker efter produkter där attributvärdet börjar med en angiven sträng.
   - Om du konfigurerar en&quot;slutar med&quot;-sökning kan kunderna söka efter produkter där attributvärdet slutar med en viss sträng.
      - Om du vill aktivera sökningen &quot;slutar med&quot; måste produktattributet vara inverterat och API-anropet ska också vara en omvänd sträng. Om du till exempel vill söka efter ett produktnamn som slutar med &quot;byxor&quot;, måste du skicka det som &quot;stnap&quot;.

- **innehåller sökindexering** - Sök efter ett attribut som använder innehåller indexering. Den nya funktionen gör att:

   - Söker efter en fråga i en större sträng. Om en kund till exempel söker efter produktnumret &quot;PE-123&quot; i strängen &quot;HAPE-123&quot;.

      - Obs! Den här söktypen skiljer sig från den befintliga [frassökningen](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase), som utför en automatisk sökning. Om produktattributvärdet till exempel är &quot;utomhusbyxor&quot; returnerar en frassökning ett svar för &quot;out pan&quot;, men returnerar inget svar för &quot;or ants&quot;. En sökning innehåller emellertid ett svar på &quot;eller ants&quot;.

De här nya villkoren förbättrar funktionen för filtrering av sökfrågor för att förfina sökresultaten. De här nya villkoren påverkar inte huvudsökfrågan.

### Implementering

1. [Ange attribut som sökbara](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata).

1. Ange sökfunktionen för det attributet, till exempel **Innehåller** (standard) eller **Börjar med**. Du kan ange högst sex attribut att aktivera för **Innehåller** och sex attribut att aktivera för **Börjar med**. Dessutom är stränglängden begränsad till högst 50 tecken för indexeringen **Innehåller**.

1. Se [utvecklardokumentationen](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) för exempel på hur du uppdaterar [!DNL Commerce Optimizer] API-anrop med de nya `contains`- och `startsWith`-sökfunktionerna.

   Du kan implementera dessa nya villkor på sökresultatsidan. Du kan till exempel lägga till ett nytt avsnitt på sidan där användaren kan förfina sina sökresultat ytterligare. Du kan ge kunderna möjlighet att välja specifika produktattribut, t.ex.&quot;Tillverkare&quot;,&quot;Artikelnummer&quot; och&quot;Beskrivning&quot;. Därifrån söker de i dessa attribut med villkoren `contains` eller `startsWith`.

### När sökning med flera lager ska användas i stället för fack

Sök i flera lager och ansikten har olika syften för att identifiera produkter, och om du väljer mellan dem beror det på ditt specifika användningssätt:

**Använd sökning i flera lager för:**

- Sök i sökresultat med flera villkor
- Arbeta med artikelnummer, SKU:er eller tekniska specifikationer där användarna vet delvis information
- Låt kunderna begränsa resultaten steg för steg med kapslade kriterier
- Minska antalet API-anrop genom att kombinera flera sökvillkor i en enda fråga
- Implementera affärsspecifika sökmönster som går längre än vanlig avancerad navigering

**Använd ansikten för:**

- Ange typisk kategori, pris, varumärke och attributfiltrering
- Erbjud intuitiva filteralternativ som användarna enkelt kan förstå och välja ut
- Visa tillgängliga alternativ baserat på aktuella sökresultat
- Visa antal filter och intervall som hjälper användarna att förstå tillgängliga alternativ
- Arbeta med gemensamma produktegenskaper som färg, storlek, material med mera

**Bästa praxis:** Använd lageruppbyggd sökning för komplexa, tekniska sökningar där användarna har specifika kriterier och använd aspekter för vanlig e-handelsfiltrering där användarna vill utforska och förfina alternativen visuellt.
