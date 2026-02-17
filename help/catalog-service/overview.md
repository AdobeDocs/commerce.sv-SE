---
title: '[!DNL Catalog Service]'
description: Snabba upp Adobe Commerce Store med  [!DNL Catalog Service]  - ett högpresterande GraphQL API som minskar sidinläsningstiden för produktsidor, kategorisidor och sökresultat.
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: 4f3f8accd653dbee6fec45c065f55ff04b17bd2d
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# [!DNL Catalog Service] för Adobe Commerce

Tillägget [!DNL Catalog Service] för Adobe Commerce förbättrar inläsningstiderna för butiker genom att tillhandahålla optimerade, skrivskyddade katalogdata via ett dedikerat GraphQL-API. Den här tjänsten är särskilt utformad för att förbättra produktrelaterade sidupplevelser, vilket ger snabbare sidinläsning och förbättrad konverteringsgrad.

De omfattande vymodelldata som tillhandahålls av [!DNL Catalog Service] innehåller produktinformation, attribut, lager och priser, vilket möjliggör snabb återgivning av produktrelaterade butiksupplevelser som:

- Produktinformationssidor
- Produktlista och kategorisidor
- Sök på resultatsidor
- Produktkaruseller
- Produktjämförelsesidor
- Andra sidor som återger produktdata, t.ex. kundvagn, beställning och önskelistesidor


## Viktiga fördelar och funktioner

- **Snabbare sidinläsning**: Optimerade frågor för upp till 10 gånger snabbare hämtning av katalogdata jämfört med GraphQL huvudsystem
- **Förbättrade konverteringsgrader**: Snabbare inläsningstider ger bättre användarupplevelse
- **Förenklade produkttyper**: Ett enhetligt schema baserat på enkla och komplexa produkttyper minskar komplexiteten för utvecklare
- **Förbättrad prisprecision**: Stöd för 16-siffriga värden med 4 decimaler
- **Kopplad arkitektur**: Separat GraphQL-system för katalogdata ger höga prestanda utan att de viktigaste Commerce-åtgärderna påverkas
- **Datasynkronisering i realtid**: Katalogtjänsten synkroniseras med Adobe Commerce-programmet via SaaS-tillägget för dataexport, vilket säkerställer att frågor returnerar de senaste katalogdata
- **Instrumentpanel för datahantering**: Övervaka och hantera datasynkroniseringsåtgärder från Adobe Commerce Admin-gränssnittet
- **API-nätintegrering**: Om du vill kan du integrera med [API-nät för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) för att kombinera Adobe Commerce GraphQL-systemen med andra interna och externa API:er för att utöka GraphQL-schemat för katalogtjänsten och lägga till anpassade data eller funktioner


## Arkitektur - översikt

>[!NOTE]
>
>Om du implementerar katalogen med hjälp av den sammanställningsbara katalogen med Adobe Commerce Optimizer eller Adobe Commerce Optimizer Connector läser du [Adobe Commerce Optimizer Guide](../optimizer/overview.md#architecture) och Merchandising Services Developer Guide.

[!DNL Catalog Service] använder [GraphQL](https://graphql.org/) för att begära och ta emot katalogdata, inklusive produkter, produktattribut, lager och priser. GraphQL är ett frågespråk som en klientklient använder för att kommunicera med API:t som definierats på en serverdel som Adobe Commerce. GraphQL är ett populärt kommunikationssätt eftersom det är lätt och gör att en systemintegratör kan ange innehåll och ordning för varje svar.

Adobe Commerce har två GraphQL-system som har olika syften:

### GraphQL Core System

- **Syfte**: Komplett API för alla Commerce-åtgärder
- **Funktioner**: Frågor (läs) och mutationer (skriv) för produkter, kunder, kundvagn, utcheckning med mera
- **Begränsning**: Produktfrågor är inte optimerade för hastighet
- **Använd skiftläge**: Allmänna Commerce-åtgärder och skrivåtgärder

### Katalogtjänst - GraphQL System

- **Syfte**: Enbart högpresterande produktkatalogfrågor
- **Funktioner**: Skrivskyddade frågor om produkter, attribut, lager och priser
- **Fördel**: betydligt snabbare än grundsystemet för produktdata
- **Använd fall**: Produkthistorik där hastighet är avgörande

De data som är tillgängliga för katalogtjänsten levereras av SaaS-tillägget för dataexport. Det här tillägget synkroniserar data mellan Commerce-programmet och anslutna Commerce-tjänster för att säkerställa att frågor till GraphQL API-ändpunkter returnerar den senaste kataloginformationen. Mer information om hur du hanterar och felsöker SaaS-dataexportåtgärder finns i [Exportguiden för SaaS-data](../data-export/overview.md).

[!DNL Catalog Service]-kunder kan använda prisindexeraren [SaaS](../price-index/price-indexing.md) som ger snabbare prisuppdateringar och synkroniseringstid.

## Arkitekturinformation

Följande diagram visar de arkitektoniska skillnaderna mellan GraphQL centrala system och katalogtjänstens GraphQL-system, och visar hur de arbetar tillsammans för att optimera prestanda i butiken:

![Katalogarkitekturdiagram](assets/catalog-service-architecture.png)

### Hur systemen fungerar

**Core GraphQL System (traditionell metod):**
PWA (Progressive Web App) skickar begäranden direkt till Commerce-programmet, som bearbetar varje begäran via flera delsystem innan ett svar returneras. Denna rundtur i flera steg kan orsaka långsam sidinläsning vilket kan leda till lägre konverteringsgrader.

**Katalogtjänst (optimerad metod):**
Katalogtjänsten fungerar som en Storefront Services Gateway som har åtkomst till en dedikerad, optimerad databas med produktinformation, attribut, varianter, priser och kategorier. Tjänsten upprätthåller synkronisering med Adobe Commerce genom automatiserad indexering och kringgår den traditionella svarscykeln för att dramatiskt minska fördröjningen.

De centrala systemen och tjänsterna i GraphQL kommunicerar inte direkt med varandra. Du kommer åt alla system från olika URL-adresser och anrop kräver olika rubrikinformation. De två GraphQL-systemen är utformade för att användas tillsammans. GraphQL-systemet [!DNL Catalog Service] utökar huvudsystemet för att göra produktbutiksupplevelserna snabbare.

Du kan också implementera [API-nät för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) för att integrera de två Adobe Commerce GraphQL-systemen med privata och tredje parts API:er och andra programgränssnitt med Adobe Developer. Nätet kan konfigureras så att anrop som dirigeras till varje slutpunkt innehåller rätt auktoriseringsinformation i rubrikerna.

## Arkitektinformation

I följande avsnitt beskrivs några av skillnaderna mellan de två GraphQL-systemen.

### Schemahantering

Eftersom Catalog Service fungerar som en tjänst behöver integratörer inte bekymra sig om den underliggande versionen av Commerce. Syntaxen för frågorna är densamma för alla versioner. Dessutom är schemat konsekvent för alla handlare. Den här konsekvensen gör det enklare att fastställa bästa praxis och ökar återanvändningen av widgetar för butiker avsevärt.

### Förenkling av produkttyper

Schemat minskar antalet olika produkttyper till två användningsområden:

- **Enkla produkter** - Katalogtjänsten mappar Adobe Commerce enkla, virtuella, hämtningsbara och presentkortsprodukter till `simpleProductViews`. Den här typen har:
   - Ett enda fast pris och en kvantitet
   - Normalpris (före rabatt) och slutpris (efter rabatt)
   - Stöd för produktattribut som färg, storlek och andra egenskaper

- **Komplexa produkter** - Katalogtjänsten mappar Adobe Commerce konfigurerbara, paketerade och grupperade produkttyper till `complexProductViews`. Komplexa produkter är samlingar av flera enkla produkter som kan konfigureras eller paketeras tillsammans.
   - Varje enkel komponentprodukt kan ha ett eget pris.
   - Shoppare kan ange kvantiteter för enskilda komponentprodukter.
   - Produktalternativen (som storlek, färg, material) är enhetliga och fungerar på samma sätt oavsett produkttyp. Varje alternativ pekar på en viss enkel produkt med egna attribut och pris. Slutprodukten är odefinierad tills kunden väljer alla alternativ som behövs.

#### Produktvyattribut

Både enkla och komplexa produkter har kunddefinierade attribut som kan visas i butiken. Dessa attribut returneras som [ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type). I Adobe Commerce definieras de tillgängliga attributen när produkten skapas. Du kan lägga till ytterligare attribut från Adobe Commerce backend eller programmatiskt. Se [Utöka och anpassa SaaS-dataexportfeed-data](../data-export/extensibility-and-customizations.md).

>[!TIP]
>
>I stället för att lägga till datatyper i Commerce serverdel kan du använda [API Mesh med katalogtjänsten](mesh.md) för att utöka GraphQL-schemat för katalogtjänsten och lägga till data eller konfigurera befintliga katalogdata för att aktivera nya funktioner.

### Priser

Enkla produkter representerar den basförsäljningsenhet som har ett pris. [!DNL Catalog Service] beräknar det reguljära priset före rabatter samt det slutliga priset efter rabatter. Prisberäkningarna kan inkludera fasta produktskatter. De utesluter personaliserade kampanjer.

En komplex produkt har inget fast pris. Katalogtjänsten returnerar i stället priset för länkade exempel. Som exempel kan en handlare till en början tilldela samma priser till alla varianter av en konfigurerbar produkt. Om vissa storlekar eller färger är opopulära kan handlaren sänka priserna på dessa varianter. Priset på den komplexa (konfigurerbara) produkten visar alltså först ett prisintervall som återspeglar priset på både standardvarianter och impopulära varianter. När kunden har valt ett värde för alla tillgängliga alternativ visas ett pris i butiken.

Katalogtjänsten säkerställer korrekta prisuppdateringar och beräkningar genom att stödja priser med stora värden (upp till 16 siffror) och hög decimalprecision (upp till 4 decimaler).

>[!NOTE]
>
> Commerce-kunder med [!DNL Catalog Service] kan dra nytta av snabbare prisändringar och synkroniseringstid på sina webbplatser med prisindexeraren [SaaS](../price-index/price-indexing.md).

## Implementering

Implementeringsprocessen omfattar:

1. [!BADGE Endast PaaS]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."} **[Installera och konfigurera katalogtjänsten](installation.md)** - Installera och konfigurera katalogtjänsttillägget och konfigurera SaaS-anslutningen med [!DNL Commerce Services Connector].
2. **Uppdatera butikskod**: Integrera katalogtjänster med GraphQL-frågor i klientorganisationen.
3. **Flödesfrågor**: Alla katalogtjänstfrågor skickas via GraphQL-gatewayen (URL tillhandahålls vid introduktion)
4. **Övervaka och felsöka datasynkronisering**: Verifiera förbättrade prestanda och övervakningsresultat


