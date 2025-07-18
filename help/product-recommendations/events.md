---
title: Samla in data
description: Lär dig hur händelser samlar in data för  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: fe96b2922583c0fcb0fcadbdacead6267806f44b
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# Samla in data

När du installerar och konfigurerar SaaS-baserade Adobe Commerce-funktioner som [[!DNL Product Recommendations]](install-configure.md) eller [[!DNL Live Search]](../live-search/install.md) distribuerar modulerna beteendedatainsamling till din butik. Den här funktionen samlar in anonyma beteendedata från era kunder och driver [!DNL Product Recommendations]. Händelsen `view` används till exempel för att beräkna rekommendationstypen `Viewed this, viewed that` och händelsen `place-order` används för att beräkna rekommendationstypen `Bought this, bought that`.

>[!NOTE]
>
>Datainsamlingen för syftet med [!DNL Product Recommendations] innehåller inte personligt identifierbar information (PII). Alla användaridentifierare, som cookie-ID:n och IP-adresser, är strikt anonymiserade. Läs [mer](https://www.adobe.com/privacy/experience-cloud.html).

## Sjukvårdskunder

Om du är vårdkund och har installerat [Data Services HIPAA-tillägget](../data-connection/hipaa-readiness.md#installation), som ingår i [dataanslutningen](../data-connection/overview.md) , hämtas inte längre data för händelsen storefront som används av [!DNL Product Recommendations]. Detta beror på att händelsedata för storefront genereras på klientsidan. Om du vill fortsätta att hämta och skicka data för butikshändelser aktiverar du händelseinsamlingen för [!DNL Product Recommendations] igen. Mer information finns i [allmän konfiguration](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services).

## Datatyper och händelser

Det finns två typer av data som används i produktrekommendationer:

- **Beteende** - Data från en kunds engagemang på din webbplats, t.ex. produktvyer, objekt som lagts till i en kundvagn och inköp.
- **Katalog** - Produktmetadata som namn, pris, tillgänglighet och så vidare.

När du installerar modulen `magento/product-recommendations` samlar Adobe Sensei in beteendedata och katalogdata och skapar produktrekommendationer för varje rekommendationstyp. Tjänsten Produktrekommendationer distribuerar sedan rekommendationerna till din butik i form av en widget som innehåller den rekommenderade produkten _items_.

Vissa rekommendationstyper använder beteendedata från era kunder för att utbilda maskininlärningsmodeller för att skapa personaliserade rekommendationer. Andra rekommendationstyper använder bara katalogdata och använder inga beteendedata. Om du snabbt vill börja använda produktrekommendationer på din webbplats kan du använda följande rekommendationstyper som bara finns i en katalog:

- `More like this`
- `Visual similarity`

### Cold start

När kan du börja använda rekommendationstyper som använder beteendedata? Det beror på. Detta kallas för problemet med _kallstart_.

Problemet med _kallstart_ avser den tid det tar för en modell att träna och börja gälla. För produktrekommendationer innebär detta att man väntar på att Adobe Sensei ska samla in tillräckligt med data för att utbilda sina maskininlärningsmodeller innan rekommendationsenheter distribueras på er webbplats. Ju mer data modellerna har, desto mer exakt och användbar är rekommendationerna. Eftersom datainsamling sker på en aktiv webbplats är det bäst att starta den här processen tidigt genom att installera och konfigurera modulen `magento/production-recommendations`.

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
- Adobe Commerce beräknar om beteendedata var fjärde timme. Rekommendationer blir exaktare ju längre de används på er webbplats.

På sidan [Skapa rekommendation](create.md#readiness-indicators) visas beredskapsindikatorer så att du kan visualisera utbildningsförloppet för varje rekommendationstyp.

Medan data samlas in på din webbplats och maskininlärningsmodellerna håller på att tränas kan du slutföra andra test- och konfigureringsuppgifter som behövs för att skapa rekommendationer. När du är klar med det här arbetet har modellerna tillräckligt med data för att skapa användbara rekommendationer, så att du kan distribuera dem till butiken.

Om din webbplats inte får tillräckligt med trafik (visningar, köp, trender) för de flesta SKU:er kanske det inte finns tillräckligt med data för att slutföra inlärningsprocessen. Detta kan få beredskapsindikatorn i administratören att fastna. Beredskapsindikatorerna är avsedda att förse handlarna med en annan datapunkt när de väljer vilken typ av rekommendationer som är bäst för deras butik. Siffrorna är en stödlinje som kanske aldrig når 100 %. [Läs mer](create.md#readiness-indicators) om beredskapsindikatorer.

### Rekommendationer för säkerhetskopiering {#backuprecs}

Om indata inte räcker till för att tillhandahålla alla begärda rekommendationsobjekt i en enhet ger Adobe Commerce säkerhetskopieringsrekommendationer för att fylla i rekommendationsenheter. Om du till exempel distribuerar rekommendationstypen `Recommended for you` till din hemsida, har en förstagångskund på din webbplats inte genererat tillräckligt med beteendedata för att korrekt rekommendera anpassade produkter. I det här fallet yter Adobe Commerce objekt baserat på rekommendationstypen `Most viewed` till den här kunden.

Om indatainsamlingen inte är tillräcklig återgår följande rekommendationstyper till rekommendationstypen `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### Händelser

Händelseinsamlaren [Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start) visar alla händelser som distribuerats till din butik. I den listan finns det en delmängd av händelser som är specifika för [!DNL Product Recommendations]. Dessa händelser samlar in data när kunderna interagerar med rekommendationsenheter i butiken och styr mätvärdena för att analysera hur bra era rekommendationer fungerar.

| Händelse | Beskrivning |
| --- | --- |
| `impression-render` | Skickas när rekommendationsenheten återges på sidan. Om en sida har två rekommendationsenheter (köpta, vy-vy) skickas två `impression-render`-händelser. Den här händelsen används för att spåra mätvärden för visningar. |
| `rec-add-to-cart-click` | Köparen klickar på knappen **Lägg till i kundvagnen** för ett objekt i rekommendationsenheten. |
| `rec-click` | Köparen klickar på en produkt i rekommendationsenheten. |
| `view` | Skickas när rekommendationsenheten blir minst 50 procent visningsbar, t.ex. genom att rulla nedåt på sidan. Om en rekommendationsenhet till exempel har två rader skickas en `view`-händelse när en rad plus en pixel på den andra raden blir synlig för kunden. Om användaren rullar sidan uppåt och nedåt flera gånger skickas händelsen `view` lika många gånger som användaren ser hela rekommendationsenheten igen på sidan. |

Även om produktrekommendationsmätvärden är optimerade för Luma store-fronts fungerar de även med andra storefront-implementeringar:

- [Edge Delivery Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/?lang=sv-SE)
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- [Anpassad överordnad (React, Vue JS)](headless.md)

#### Nödvändiga instrumentpanelshändelser

Följande händelser krävs för att fylla i [[!DNL Product Recommendations] kontrollpanelen](workspace.md)

| Kontrollpanelskolumn | Händelser | Kopplingsfält |
| ---------------- | --------- | ----------- |
| Impressions | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Vyer | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Klickningar | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Intäkter | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| LT intäkt | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

Följande händelser är inte specifika för produktrekommendationer, men krävs för att Adobe Sensei ska kunna tolka kunddata korrekt:

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
| En titt på det här, köpte det | Produktrecept | `page-view`<br>`product-view` | Produktinformationssida<br>Kopia/utcheckning |
| Köpte den här, köpte den där | Produktrecept | `page-view`<br>`product-view` | Produktinformationssida |
| Trender | `page-view`<br>`product-view` | Produktinformationssida |
| Konvertering: Visa för köp | Produktrecept | `page-view`<br>`product-view` | Produktinformationssida |
| Konvertering: Visa för köp | Produktrecept | `page-view`<br>`place-order` | Kassa/kassa |
| Konvertering: Visa i kundvagn | Produktrecept | `page-view`<br>`product-view` | Produktinformationssida |
| Konvertering: Visa i kundvagn | Produktrecept | `page-view`<br>`add-to-cart` | Produktinformationssida<br>Produktlistsida<br>Kart<br>Önskslista |

#### Caveats

- Annonsblockerare och sekretessinställningar kan förhindra händelser från att fångas in och kan göra så att engagemanget och intäktsmåtten [på ](workspace.md#column-descriptions) inte rapporteras tillräckligt. Dessutom kanske vissa händelser inte skickas på grund av att kunderna lämnar sidan eller nätverksproblem.
- [Headless-implementeringar](headless.md) måste implementera händelser för att instrumentpanelen för produktrekommendationer ska fungera.
- För konfigurerbara produkter använder produktrekommendationer avbildningen av den överordnade produkten i rekommendationsenheten. Om den konfigurerbara produkten inte har någon angiven bild kommer rekommendationsenheten att vara tom för den specifika produkten.

>[!NOTE]
>
>Om [läget för cookie-begränsning](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=sv-SE) är aktiverat samlar Adobe Commerce inte in beteendedata förrän kunden samtycker till att använda cookies. Om läget för cookie-begränsning är inaktiverat samlar Adobe Commerce in beteendedata som standard.
