---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Den senaste versionsinformationen för  [!DNL Catalog Service]  för Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 7b05da07d185c5495642037c6ef3b7ff5fcaa8e6
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 0%

---

# Versionsinformation för [!DNL Commerce Storefront Catalog Service]

Versionsinformationen innehåller de senaste uppdateringarna av Commerce Catalog Service, inklusive:

- **Storefront Catalog Service släpper**

   - API-schemaförbättringar för katalogtjänst för förbättrad datahämtning.
   - Förbättringar av säkerhet, prestanda och tillförlitlighet för Catalog Service API och underliggande infrastruktur.

- **Metapaketversioner för katalogtjänst**

   - Uppdaterade beroenden för bättre prestanda, stabilitet och kompatibilitet med andra Adobe Commerce-komponenter.

Uppdateringar kategoriseras efter typ:

![Nya](../assets/new.svg) nya funktioner
![Korrigera ](../assets/fix.svg) Korrigeringar och förbättringar
![Fel](../assets/bug.svg) Kända fel

Stöd finns för den senaste versionen. Versionsinformation för äldre versioner finns med som referens.

## Katalogtjänsten Storefront

### Version v1.47

_12 februari 2025_

![Nytt](../assets/new.svg) API-tjänsten har nu stöd för typen `CategoryProductView`, vilket möjliggör förbättrade vyer och frågor för produkter per kategori. Med den här uppdateringen kan utvecklare effektivt hämta och filtrera produktdata baserat på kategori, vilket förbättrar flexibiliteten och prestandan för kategoristyrda användningsfall. Mer information finns i [Implementera kategorier på butiken](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/categories-storefront-implementation/). Stöds endast för Commerce-implementeringar som använder datamodellen [composiable catalog](https://developer.adobe.com/commerce/services/optimizer/) för headless Store<!--DATA-6949-->

### Version v1.46

_11 december 2025_

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra prestanda och stabilitet. <!--DATA-6852, DATA-6864-->

### Version v1.45

_17 november 2025_

![Nytt](../assets/new.svg) **Attributfiltrering efter namn**-GraphQL-frågan `productSearch` har nu stöd för filtrering av produktattribut med fältet `names`. <!--DATA-6831--> Med detta filter kan du:

- Minska svarsnyttolastens storlek genom att endast begära specifika attribut
- Kombinera med det befintliga `roles`-filtret för att begränsa efter synlighetsroll och attributnamn
- Exempel:

  **Filtrera endast efter attributnamn**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **Filtrera efter både roller och namn:**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>Om du vill hämta alla attribut utan filtrering utelämnar du argumentet `names` eller anger en tom array.

### Version v1.44

_6 november 2025_

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra prestanda och stabilitet. <!--DATA-6852, DATA-6864-->

### Version v1.43

_3 november 2025_

![Nytt](../assets/new.svg) **Produktlager för flerdimensionell produktanpassning** - Stöd har lagts till för kanalspecifik lokal innehållsleverans för Adobe Commerce Optimizer-implementeringar.<!--DATA-6632-->

- Leverera olika produktinnehåll till olika kundsegment
- Använda språkspecifika anpassningar utan att duplicera basdata
- Kontrollera fältnivååsidosättningar med lagermasker
- Stöd för förstklassiga, säsongsrelaterade och mobiloptimerade innehållslager

  Lager hämtas med den befintliga `products`-frågan, används på serversidan från begärandehuvuden och inga schemaändringar krävs. Se [Kataloglager](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-layer) i _Adobe Commerce Optimizer Guide_.

![Korrigera](../assets/fix.svg) Grupperade produkter kan nu efterfrågas när den överordnade inte har några priser. Underordnade produkter returnerar sina egna synlighetsroller.<!--DATA-6779-->

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra prestanda och stabilitet. <!--DATA-6721, DATA-6864-->

### Version v1.42

_8 september 2025_

![Nytt](../assets/new.svg) **Stöd för nivåprissättning har lagts till** för att fråga efter volympriser:<!--DATA-6643-->

Så här hämtar du nivåpriser:

1. Använd `products`-frågan med de SKU:er du vill använda
2. För **SimpleProductView**, gå till `price.tiers`
3. För **ComplexProductView**, gå till `priceRange.minimum.tiers` och `priceRange.maximum.tiers`
4. Varje skikt innehåller det rabatterade priset `tier` och villkoren `quantity`
5. Definiera tröskelvärden för kvantitet med `gte` (större än eller lika med) och `lt` (mindre än)

**Exempel:**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![Korrigera](../assets/fix.svg) **Nivåpriser filtrerade efter lägsta slutpris** <!--DATA-6643-->

API:t returnerar nu bara skikt vars rabatterade pris är **lägre än** produktens lägsta slutliga pris. Högre nivåer utelämnas eftersom det slutliga minimipriset i stället skulle gälla för butiken.

Gäller för:

- **Enkla produkter**: `price.tiers` innehåller bara lager med `tier.amount.value` &lt; `price.final.amount.value` (minimum final).
- **Komplexa produkter**: `priceRange.minimum.tiers` och `priceRange.maximum.tiers` använder samma regel när prisintervallet skapas.

### Version v1.41

_2 september 2025_

![Korrigera](../assets/fix.svg) **Förbättrad felhantering för saknad prisinformation** - När prisdata inte har tagits emot ännu returnerar API `null` för prisfältet i stället för att utlösa ett fel, vilket gör att klienter kan hantera saknade data på ett bra sätt.<!--DATA-6612-->

![Korrigera](../assets/fix.svg) Förbättringar på systemnivå och infrastruktur för att förbättra prestanda och stabilitet.<!--DATA-6671-->

### Version v1.40

_30 juli 2025_

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6619-->

### v1.39-utgåvan

_24 juli 2025_

![Nytt](../assets/new.svg) **Hämta rekommendationsenheter efter enhets-ID**-Ny GraphQL-slutpunkt `recommendationsByUnitIds` hämtar rekommendationsenheter med deras unika ID för mer flexibel, riktad åtkomst.

- `unitIds` krävs (lista över recIds som ska hämtas).
- Kontextparametrar (`currentSku`, `cartSkus`, `userViewHistory`, `userPurchaseHistory`, `category`) fungerar på samma sätt som i den befintliga rekommendationsfrågan.

- **Exempel**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6316-->

### v1.38-utgåvan

_15 juli 2025_

![Ny](../assets/new.svg) **Presentkortsprodukter**-Katalogtjänsten Storefront stöder nu produktattribut som JSON-objekt eller -matriser, vilket möjliggör flexibel hantering av komplexa typer som presentkort.<!--DATA-6573-->


### Version v1.37

_20 juni 2025_

![Ny](../assets/new.svg) **Hierarkisk prisbokskonfiguration** - Korrekta prisintervall för överordnade/underordnade prisböcker. Beräkningar respekterar hierarkin och ärvda regler. Minskar prissättningsfel när flera prisböcker är kopplade. Endast Adobe Commerce Optimizer. Se [Prisböcker](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![Nytt](../assets/new.svg) **Skiftlägeskänsliga tangenter** - Nyckelsökningar i frågor är nu skiftlägeskänsliga, vilket minskar antalet fel som beror på tangentförskjutning. <!--DATA-6494, DCAT-2495-->

### Version v1.36

_20 juni 2025_

![Nytt](../assets/new.svg) **Publika IO-händelser för katalogbutiken** - Lagt till offentliga IO-händelser för realtidsintegrering och observerbarhet (CSS och EDS).<!--DATA-6329-->

![Nytt](../assets/new.svg) **SSR (Server-Side Rendering)** - Arkitekturförbättringar som stöder SSR för bättre prestanda, SEO och UX för stora kataloger.<!--DATA-6278, DATA-6280-->

![Nytt](../assets/new.svg) **Infrastruktur och säkerhet** - Nya AWS-roller, ServiceNow-integrering och CI/CD-pipelines för händelsetjänsten.

![Nytt](../assets/new.svg) **Händelseformat och observerbarhet** - Effektivare nyttolaster, förbättrad övervakning, förbättrade data för varianthändelser.<!--DATA-6332, DATA-6402, -->

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6404, DATA-6410, -->

+++ Tidigare versioner

## Version v1.35

_13 juni 2025_

![Nytt](../assets/new.svg) **Hämta ocachelagrade data**-Aktivera `Magento-Is-Preview`-rubriken för att skicka ocachelagrade data från katalogslutpunkten till söktjänsten.<!--DATA-6345-->

![Nytt](../assets/new.svg) **Flervalsproduktalternativ**-GraphQL-API:t visar nu om produktalternativ tillåter flera val (t.ex.&quot;välj flera objekt&quot;).<!--DATA-6487-->

![Nytt](../assets/new.svg) Prisvalidering vid dataöverföring har uppdaterats för att ge stöd åt produkter utan priser.<!--DATA-6098-->

![Åtgärda](../assets/fix.svg) Förbättrad felhantering för enkla paketpriser i Adobe Commerce Optimizer.<!--DATA-6541-->

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6273, DATA-6485, -->

## Version v1.34

_23 mars 2025_

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-5732-->

## Version v1.33

_29 april 2025_

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen. Infrastrukturen har nu stöd för extremt stora kataloger (upp till ca 440 miljoner SKU:er) utan att påverka befintliga arbetsbelastningar.

### Version v1.32

_28 mars 2025_

![Korrigera](../assets/fix.svg) Attribut utan roller indexeras inte längre som standard för den sammansatta katalogen, vilket förbättrar indexeringstiden och minskar lagringsutrymmet. Äldre beteenden kan återaktiveras via en funktionsflagga.

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet. <!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### Version v1.31

_18 februari 2025_

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6389, DATA-6367, DATA-6373-->

### Version v1.30

_9 december 2024_

Huvudversion: [sammansättningsbar katalogdatamodell](https://developer.adobe.com/commerce/services/optimizer/) för headless-butiker, rubrikhantering och hantering av produktdata.

![Ny](../assets/new.svg) **CCDM (Composable Catalog Data Model)** - Stöder kunder som använder den sammansatta katalogen för headless-butiker. Nya slutpunkter accepterar katalogvy och princip-ID (bakåtkompatibla). Konfigurerbar produktinformation och priser med inbyggd sidnumrering.<!--DATA-6018, DATA-6288-->

![Nytt](../assets/new.svg) **Sidhuvudshantering**-`AC-Locale` har bytt namn till `AC-Scope-Locale` för API-åtgärder för sammansättningsbar katalog. Huvudmappning och standardvärden har angetts.<!--DATA-6303, DATA-6078-->

![Nytt](../assets/new.svg) **Produktdata och priser**-Stöd för datamodell för sammanställningsbar katalog och förbättrad prishantering för konfigurerbara produkter.<!--DATA-6279-->

`CurrencyEnum` har uppdaterats med stöd för `NONE` för produktsökningsfrågor, i linje med federationslogik.<!--DATA-6285-->

![Korrigera](../assets/fix.svg) **Infrastruktur och uppgraderingar** - Förbättringar på systemnivå för säkerhet, prestanda och stabilitet.

![Åtgärda](../assets/fix.svg) Produktalternativen för paketet visar nu bara aktiverade produkter.<!--DATA-6347-->

### Version v1.29

_9 december 2024_

![Nytt](../assets/new.svg) **Bildbeställning i produktfrågor** - Produktbilder i fältet GraphQL `images` följer nu katalogexport `sortOrder` för konsekvent butiks- och API-beteende.<!--DATA-6258-->

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6619-->

### Version v1.28

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### Version v1.27

_26 september 2024_

![Åtgärda](../assets/fix.svg) Förbättringar på systemnivå och i infrastrukturen för att förbättra säkerhet, prestanda och stabilitet.<!--DATA-6243-->

### Version v1.26

_22 oktober 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) GraphQL-schema innehåller nu `lastModifiedAt` i produktinformationen för korrekt webbplatskartor och omindexering av sökmotorer (t.ex. Google). <!--DATA-6209-->

### Version v1.23

_22 augusti 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Produktinformation kan nu hämtas utan data för produktåsidosättning (priser). Tidigare returnerades följande frågor: `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### Version v1.22

_13 augusti 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd har lagts till för att hämta alla varianter efter produkt-SKU. Se [API-referens för katalogtjänst](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Version v1.19

_23 maj 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare


![Korrigera](../assets/fix.svg) <!--DATA-5033-->Flaggan `InStock` för alternativvärden respekterar nu produktvariantens omfångsstatus `enabled` .

![Korrigera](../assets/fix.svg) <!--DATA-5888-->Stöd för produktpriser med upp till 16 siffror och 4 decimaler har lagts till. Synkronisera om från [kontrollpanelen för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) eller [CLI](../landing/catalog-sync.md#command-line-interface) för att tillämpa uppdateringar.

#### Kända begränsningar

Följande funktioner stöds ännu inte:

- Den största tillåtna storleken för dynamisk attributnyttolast är 9 MB.
- Gruppens produktpris kan beräknas med enkla produktpriser.
- I en bildarray innehåller endast den första bilden roller.

Använd API Mesh och Core GraphQL API för:

- Lägsta kampanjpris
- Nivåpriser
- Paketprodukter med fasta priser

Mer information och exempel finns i [Katalogtjänst och API-nät](mesh.md).

### Version v1.18

_11 april 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd för PHP 8.3 har lagts till.

![Nytt](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) - och [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)-frågorna returnerar nu anpassningsbara alternativdata för både enkla och komplexa produkter.<!--DATA-5538-->

### Version v1.17

_22 februari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) är nu tillgängligt för dataströmmar (produktrekommendationer, Live Search, katalogtjänst). Kräver `catalog-service` metapaket v3.1.0+.

### Version v1.16

_13 februari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nya](../assets/new.svg) produktvideor stöds nu av katalogtjänstens API.
![Korrigera](../assets/fix.svg) Utmediefiler visas nu i PDP-widgeten.

#### Kända begränsningar

Dessa funktioner stöds ännu inte:

- Den största tillåtna storleken för dynamisk attributnyttolast är 9 MB.
- Gruppproduktpris. Detta värde kan beräknas med enkla produktpriser.
- I en bildarray innehåller endast den första bilden roller.

Använd API Mesh och Core GraphQL API för:

- Lägsta kampanjpris
- [Nivåpriser](mesh.md)

### Version v1.13

_12 oktober 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst stöder flaggan `inStock` för produktvarianter.
![Nytt](../assets/new.svg) Fälten `urlKey` och `externalId` har lagts till i GraphQL-schemat.
![Nya](../assets/new.svg) hämtningsbara produkter och presentkort stöds nu.

### Version v1.12

_19 september 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst använder nu [SaaS-prisindexering](../price-index/price-indexing.md).
![Korrigera](../assets/fix.svg) Den här versionen innehåller felkorrigeringar och förbättringar på tjänstsidan.

### Version v1.11

_18 juli 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst har nu stöd för GraphQL-frågan [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) för produktrekommendationer.

### Version v1.10

_27 juni 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Katalogtjänstens API har nu stöd för `related products`.

### v1.7-utgåva

_12 april 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst rensar nu bort produktvarianter som tagits bort.
![Korrigera](../assets/fix.svg) Infrastrukturskalbarhet och prestandaförbättringar.

### v1.6-utgåva

_28 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nya](../assets/new.svg) tillagda färgrutor i frågan [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nytt](../assets/new.svg) har lagt till möjligheten att hämta `entityId` med [API-nät](mesh.md).

### v1.5-utgåva

_6 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) tillagd [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL-funktionalitet.
![Korrigera](../assets/fix.svg) Förbättrade prestanda och API-skalbarhet.

### v1.4-utgåva

_7 februari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Katalogtjänstmetapaket har publicerats för att förenkla installationsstegen.
![Åtgärda](../assets/fix.svg) API-skalbarhet och prestandaförbättringar.

### v1.3-utgåva

_17 januari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Förenklat och förbättrat startupplevelsen.
![Nya](../assets/new.svg) slutpunkter för kundsandlådan är tillgängliga för testning före produktion.
![Nytt](../assets/new.svg)-stöd har lagts till för virtuella produkter.
![Åtgärda](../assets/fix.svg) API-skalbarhet och prestandaförbättringar.

### v1.1-utgåva

_18 november 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Ny](../assets/new.svg) katalogtjänst har nu stöd för Adobe [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/).
![Korrigera](../assets/fix.svg) Förbättrad API-skalbarhet och övergripande prestanda.

### v1.0-utgåva

_4 oktober 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg)-stöd för paketerade och grupperade produkter.
![Ny](../assets/new.svg) har lagt till åsidosättningar av B2B-synlighet. Produkterna är nu sökbara och kan läggas till i kundvagnen för specifika kundgrupper.
![Korrigera](../assets/fix.svg)-tjänsten är nu stabilare och har förbättrat prestandan.

### 0.3-utgåvan - Beta+

_12 september 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Variantbilder: produktbilder returneras baserat på valda alternativ.
![Ny](../assets/new.svg) Prisroller: endast medlemmar i specifika kundgrupper kan se produktpriser.
![Korrigera](../assets/fix.svg) Förbättrad stabilitet och prestanda för tjänsten.
![Nya](../assets/new.svg) uppdateringar tas emot när produkter tas bort från katalogen.

### Beta Release

_9 augusti 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nya](../assets/new.svg) `products` - och `refineProduct`-frågor returnerar följande data:

- Fördefinierade produktattribut (system).
- Dynamiska produktattribut och filtrera dem efter roll (produktvisningssida/produktlistsida).
- Produktalternativ.
- Produktbilder och filtrera dem efter roll (PDP/PLP).
- Ett specifikt pris för enkla produkter och prisintervall för konfigurerbara produkter.
- Kundgruppspriser och prisintervall. De returnerar ett standardgrundpris för kunderna utan någon kundgrupp.
- Produkttyper där B2B-kundspecifika priser används.

+++

## Metapaket för katalogtjänst

Uppdateringar av PHP-metapaketet för katalogtjänsten (`magento/catalog-service`).

- För Adobe Commerce as a Cloud Service-kunder installeras den senaste versionen i din miljö.

- För Adobe Commerce i molnet rekommenderar Adobe att du använder Composer för att uppgradera Catalog Service-metapaketet i dina molnmiljöer.

### v3.3.0-utgåva

_14 oktober 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) **Data Services-uppgradering**—`magento/data-services`-beroendet har uppdaterats till ^8.0.0. Verifiera miljön och anpassad API-användning för datatjänster för 8.x-kompatibilitet innan du uppgraderar.
ea
![Nytt](../assets/new.svg) Uppdaterad version och metadata för version 3.3.0.

### v3.2.0-utgåva

_12 april 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg)-version och metadata har uppdaterats för 3.2.0. Inga andra beroendeändringar.

### v3.1.0-utgåva

_26 januari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) har lagt till nya paketberoenden:

- **Datautexporterare för kategoribehörighet** (`magento/module-category-permission-data-exporter`) för export av kategoribehörighetsdata som används av katalogtjänsten.
- **Katalogsynkroniseringsadministratör** `magento/module-catalog-sync-admin` för administratörsgränssnitt och konfiguration som är relaterad till katalogsynkronisering.

![Nytt](../assets/new.svg) Uppdaterad version och metadata för version 3.1.0.

## Relaterad dokumentation

- För projekt som distribueras på **Adobe Commerce i molnet, lokalt eller Adobe Commerce as a Cloud Service, se följande dokumentation:

   - [Handbok för katalogtjänst](overview.md)
   - [API-referens för katalogtjänsten GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Adobe Commerce Admin Guide](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Adobe Commerce as a Cloud Service Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Adobe Commerce on Cloud-guide](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- För projekt som använder **Adobe Commerce Optimizer** eller **Adobe Commerce Optimizer Connector** finns följande dokumentation:

   - [Utvecklarhandbok för marknadsföringstjänster](https://developer.adobe.com/commerce/services/optimizer/)
   - [Merchandising GraphQL API Reference](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Adobe Commerce Optimizer Guide](../optimizer/overview.md)
