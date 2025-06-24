---
title: Översikt över händelser
description: Lär dig mer om de händelser som  [!DNL Adobe Commerce Optimizer]  använder för att förbättra sökningar och rekommendationer.
role: Admin, Developer
recommendations: noCatalog
source-git-commit: 356b10704c9e7c7329d3e9c0e10baa15d5142ec0
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# Händelser

Händelser är ett viktigt verktyg för att förbättra shoppingupplevelsen och öka konverteringsgraden genom att utnyttja datainsikter i realtid.

[!DNL Adobe Commerce Optimizer] distribuerar butikshändelser till din plats automatiskt. Dessa händelser hämtar in data från kundernas interaktioner på er webbplats. Dessa anonyma data driver [rekommendationer](../../manage-results/recommendation-performance.md), [produktidentifiering](../../manage-results/search-performance.md) och [framgångsmått](../../manage-results/success-metrics.md).

>[!NOTE]
>
>Datainsamlingen innehåller ingen personligt identifierbar information. Alla användaridentifierare, som cookie-ID:n och IP-adresser, är strikt anonymiserade. [Läs mer](https://www.adobe.com/privacy/experience-cloud.html).

På sidan **Händelser** kan du observera de data för händelsen storefront som samlas in. Med en översikt över händelsedatainsamlingen kan handlare verifiera att de har implementerat butikshändelser korrekt och att händelser har hämtats. Handlare kan använda den här sidan för att identifiera potentiella problem och vidta åtgärder för att lösa eventuella händelseproblem.

## Antal händelser

Fliken **Antal händelser** spårar kundinteraktioner, som sökningar, klick och köp, så att du kan analysera trender och förbättra shoppingupplevelsen.

![Antal händelser](../../assets/event-counts.png){zoomable="yes"}

| Fält | Beskrivning |
|---|---|
| **Datumintervall** | Låt oss ange datumintervallet för att se en viss delmängd data. |
| **StoreFront-händelser per timme** | Visar ett diagram över antalet händelser som utlöses i butiken. |
| **Totalt antal butikshändelser** | En filtrerbar tabell som visar information om alla händelser som utlöses i din butik. |

## Sanitetskontroll

Fliken **Sanitetskontroll** ger dig insikt i hälsotillståndet för varje beteendehändelse och säkerställer korrekt datainsamling och funktionalitet. &#x200B;

![Sanitetskontroll](../../assets/sanity-check.png){zoomable="yes"}

| Fält | Beskrivning |
|---|---|
| **Datumintervall** | Låt oss ange datumintervallet för att se en viss delmängd data. |
| **Produktidentifiering** | Visar de händelser som krävs för att anpassa sökresultaten. Kolumnen **Status** anger om händelserna togs emot. |
| **Rekommendationer** | Visar de händelser som krävs för att anpassa produktrekommendationer. Kolumnen **Status** anger om händelserna togs emot. |

I följande avsnitt beskrivs händelseinformation för [produktidentifiering](#product-discovery) och [rekommendationer](#recommendations).

### Produktupptäckt

Vid produktupptäckt används händelser för att driva sökalgoritmer som&quot;Mest visade&quot; och&quot;Viewed This, Viewed That&quot;.

Den här tabellen beskriver de händelser som används av produktidentifieringsstrategierna [rankning](../../merchandising/rules/add.md#intelligent-ranking).

| Rankningsstrategi | Händelser | Sida |
| --- | --- | --- |
| Mest visade | `page-view`<br>`product-view` | Produktinformationssida |
| Mest köpta | `page-view`<br>`place-order` | Kassa/kassa |
| Mest tillagt i kundvagn | `page-view`<br>`add-to-cart` | Produktinformationssida<br>Produktlistsida<br>Kundlista<br>Önskad lista |
| Visade det här, såg du att | `page-view`<br>`product-view` | Produktinformationssida |

### Nödvändiga instrumentpanelshändelser

Vissa händelser krävs för att fylla i [kontrollpanelen för sökprestanda](../../manage-results/search-performance.md)

| Kontrollpanelsområde | Händelser | Kopplingsfält |
| ------------------- | ------------- | ---------- |
| Unika sökningar | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Inga resultatsökningar | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |

### Rekommendationer

Det finns två typer av data som används i rekommendationerna:

- **Beteende** - Data från en kunds engagemang på din webbplats, t.ex. produktvyer, objekt som lagts till i en kundvagn och inköp.
- **Katalog** - Produktmetadata som namn, pris, tillgänglighet och så vidare.

Adobe Sensei samlar in beteendedata och katalogdata och skapar rekommendationer för varje rekommendationstyp. Rekommendationstjänsten distribuerar sedan dessa rekommendationer till din butik i form av en widget som innehåller den rekommenderade produkten _items_.

Vissa rekommendationstyper använder beteendedata från era kunder för att utbilda maskininlärningsmodeller för att skapa personaliserade rekommendationer. Andra rekommendationstyper använder bara katalogdata och använder inga beteendedata. Om du snabbt vill börja använda rekommendationer på din webbplats kan du använda rekommendationstypen `More like this`.

#### Cold start

När kan du börja använda rekommendationstyper som använder beteendedata? Det beror på. Detta kallas för problemet med _kallstart_.

Problemet med _kallstart_ avser den tid det tar för en modell att träna och börja gälla. För rekommendationer innebär detta att man måste vänta på att Adobe Sensei ska samla in tillräckligt med data för att utbilda sina maskininlärningsmodeller innan rekommendationsenheter distribueras på er webbplats. Ju mer data modellerna har, desto mer exakt och användbar är rekommendationerna. Eftersom datainsamling sker på en aktiv webbplats är det bäst att börja den här processen tidigt.

I följande tabell visas några allmänna riktlinjer för hur lång tid det tar att samla in tillräckligt med data för varje rekommendationstyp:

| Rekommendationstyp | Utbildningstid | Anteckningar |
|---|---|---|
| Popularitetsbaserad (`Most viewed`, `Most purchased`, `Most added to cart`) | Varierar | Beroende på antalet händelser - vyerna är de vanligaste och lär sig därför snabbare. Sedan läggs de till i kundvagnen och sedan köps |
| `Viewed this, viewed that` | Kräver mer utbildning | Produktvyerna är volymmässigt låga |
| `Viewed this, bought that`, `Bought this, bought that` | Kräver den senaste utbildningen | Inköpshändelser är de mest ovanliga händelserna på en e-handelsplats, särskilt jämfört med produktvisningar |
| `Trending` | Kräver tre dagars data för att fastställa en popularitetsbaslinje | Trendsättning är ett mått på den senaste tiden i en produkts popularitet jämfört med dess egen popularitetsbaslinje. En produkts trendpoäng beräknas med hjälp av en förgrundsuppsättning (färsk popularitet över 24 timmar) och en bakgrundsuppsättning (popularitetsbaslinje över 72 timmar). Om ett objekts popularitet ökar avsevärt inom en 24-timmarsperiod jämfört med dess popularitet vid baslinjen får det ett högt trendresultat. Alla produkter har den här poängen och de produkter som har den högsta poängen när som helst utgör de mest populära trendprodukterna. |

Andra variabler som kan påverka den tid som krävs för att utbilda:

- Högre trafikvolym bidrar till snabbare inlärning
- Vissa rekommendationstyper tränar snabbare än andra
- [!DNL Adobe Commerce Optimizer] beräknar om beteendedata var fjärde timme. Rekommendationer blir exaktare ju längre de används på er webbplats.

På sidan [Skapa rekommendation](../../merchandising/recommendations/create.md#readiness-indicators) visas beredskapsindikatorer så att du kan visualisera utbildningsförloppet för varje rekommendationstyp.

Medan data samlas in på din webbplats och maskininlärningsmodellerna håller på att tränas kan du slutföra andra test- och konfigureringsuppgifter som behövs för att skapa rekommendationer. När du är klar med det här arbetet har modellerna tillräckligt med data för att skapa användbara rekommendationer, så att du kan distribuera dem till butiken.

Om din webbplats inte får tillräckligt med trafik (visningar, köp, trender) för de flesta SKU:er kanske det inte finns tillräckligt med data för att slutföra inlärningsprocessen. Detta kan göra att beredskapsindikatorn på arbetsytan Rekommendationer verkar fastna. Beredskapsindikatorerna är avsedda att förse handlarna med en annan datapunkt när de väljer vilken typ av rekommendationer som är bäst för deras butik. Siffrorna är en stödlinje som kanske aldrig når 100 %. [Läs mer](../../merchandising/recommendations/create.md#readiness-indicators) om beredskapsindikatorer.

#### Rekommendationer för säkerhetskopiering

Om indata inte räcker till för att tillhandahålla alla begärda rekommendationsobjekt i en enhet ger [!DNL Adobe Commerce Optimizer] säkerhetskopieringsrekommendationer för att fylla i rekommendationsenheter. Om du till exempel distribuerar rekommendationstypen `Recommended for you` till din hemsida, har en förstagångskund på din webbplats inte genererat tillräckligt med beteendedata för att korrekt rekommendera anpassade produkter. I det här fallet ytor [!DNL Adobe Commerce Optimizer] objekt baserat på rekommendationstypen `Most viewed` till den här kunden.

Om indatainsamlingen inte är tillräcklig återgår följande rekommendationstyper till rekommendationstypen `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Rekommendationsspecifika händelser

I följande tabell visas de händelser som utlöses när kunderna interagerar med rekommendationsenheter i butiken. De händelsedata som samlas in gör att [måtten](../../manage-results/recommendation-performance.md) kan analysera hur bra dina rekommendationer fungerar.

| Händelse | Beskrivning |
| --- | --- |
| `impression-render` | Skickas när rekommendationsenheten återges på sidan. Om en sida har två rekommendationsenheter (köpta, vy-vy) skickas två `impression-render`-händelser. Den här händelsen används för att spåra mätvärden för visningar. |
| `rec-add-to-cart-click` | Köparen klickar på knappen **Lägg till i kundvagnen** för ett objekt i rekommendationsenheten. |
| `rec-click` | Köparen klickar på en produkt i rekommendationsenheten. |
| `view` | Skickas när rekommendationsenheten blir minst 50 procent visningsbar, t.ex. genom att rulla nedåt på sidan. Om en rekommendationsenhet till exempel har två rader skickas en `view`-händelse när en rad plus en pixel på den andra raden blir synlig för kunden. Om användaren rullar sidan uppåt och nedåt flera gånger skickas händelsen `view` lika många gånger som användaren ser hela rekommendationsenheten igen på sidan. |

#### Nödvändiga instrumentpanelshändelser

Följande händelser krävs för att fylla i kontrollpanelen [Rekommendationer ](../../manage-results/recommendation-performance.md)

| Kontrollpanelskolumn | Händelser | Kopplingsfält |
| ---------------- | --------- | ----------- |
| Impressions | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Vyer | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Klickningar | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Intäkter | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| LT intäkt | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

Följande händelser är inte specifika för Rekommendationer, men krävs för att Adobe Sensei ska tolka kunddata korrekt:

- `view`
- `add-to-cart`
- `place-order`

#### Rekommendationstyp

I den här tabellen beskrivs de händelser som används av varje rekommendationstyp.

| Rekommendationstyp | Händelser | Sida |
| --- | --- | --- |
| Mest visade | `page-view`<br>`product-view` | Produktinformationssida |
| Mest köpta | `page-view`<br>`place-order` | Kassa/kassa |
| Mest tillagt i kundvagn | `page-view`<br>`add-to-cart` | Produktinformationssida<br>Produktlistsida<br>Kundlista<br>Önskad lista |
| Visade det här, såg du att | `page-view`<br>`product-view` | Produktinformationssida |
| En titt på det här, köpte det | `page-view`<br>`product-view` | Produktinformationssida<br>Kopia/utcheckning |
| Köpte den här, köpte den där | `page-view`<br>`product-view` | Produktinformationssida |
| Trender | `page-view`<br>`product-view` | Produktinformationssida |
| Konvertering: Visa för köp | `page-view`<br>`product-view` | Produktinformationssida |
| Konvertering: Visa för köp | `page-view`<br>`place-order` | Kassa/kassa |
| Konvertering: Visa i kundvagn | `page-view`<br>`product-view` | Produktinformationssida |
| Konvertering: Visa i kundvagn | `page-view`<br>`add-to-cart` | Produktinformationssida<br>Produktlistsida<br>Kart<br>Önskslista |

## Support

Om du märker att det finns avvikelser i data eller om rekommendationer och sökresultat inte fungerar som förväntat, [skickar du en supportanmälan](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
