---
title: '[!DNL Catalog Service]'
description: '[!DNL Catalog Service] för Adobe Commerce erbjuder ett sätt att hämta innehållet på produktvisningssidor och produktlistsidor mycket snabbare än med de ursprungliga Adobe Commerce GraphQL-frågorna.'
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# [!DNL Catalog Service] för Adobe Commerce

Tillägget [!DNL Catalog Service] för Adobe Commerce innehåller omfattande katalogdata för visningsmodell (skrivskyddad) för att återge produktrelaterade butiksupplevelser snabbt och fullständigt, inklusive:

* Produktinformationssidor
* Produktlista och kategorisidor
* Sök på resultatsidor
* Produktkaruseller
* Produktjämförelsesidor
* Andra sidor som återger produktdata, t.ex. kundvagn, beställning och önskelistesidor

[!DNL Catalog Service] använder [GraphQL](https://graphql.org/) för att begära och ta emot katalogdata, inklusive produkter, produktattribut, lager och priser. GraphQL är ett frågespråk som en klientklient använder för att kommunicera med API:t som definierats på en serverdel som Adobe Commerce. GraphQL är ett populärt kommunikationssätt eftersom det är lätt och gör att en systemintegratör kan ange innehåll och ordning för varje svar.

Adobe Commerce har två GraphQL-system. GraphQL system innehåller ett stort antal frågor (läsoperationer) och mutationer (skrivåtgärder) som gör att en kund kan interagera med många olika typer av sidor, bland annat produkt, kundkonto, kundvagn, utcheckning med mera. De frågor som returnerar produktinformation är dock inte optimerade för snabbhet. De tjänster som GraphQL system kan bara utföra frågor om produkter och relaterad information. De här frågorna är mer prestandavänliga än liknande kärnfrågor.

De data som är tillgängliga för katalogtjänsten levereras av SaaS-tillägget för dataexport. Det här tillägget synkroniserar data mellan Commerce-programmet och anslutna Commerce-tjänster för att säkerställa att frågor till GraphQL API-ändpunkter returnerar den senaste kataloginformationen. Mer information om hur du hanterar och felsöker SaaS-dataexportåtgärder finns i [Exportguiden för SaaS-data](../data-export/overview.md).

[!DNL Catalog Service]-kunder kan använda prisindexeraren [SaaS](../price-index/price-indexing.md) som ger snabbare prisuppdateringar och synkroniseringstid.

## Arkitektur

I följande diagram visas de två GraphQL-systemen:

![Katalogarkitekturdiagram](assets/catalog-service-architecture.png)

I det centrala GraphQL-systemet skickar PWA en begäran till Commerce-programmet, som tar emot varje begäran, bearbetar den, skickar eventuellt en begäran via flera delsystem och returnerar sedan ett svar till butiken. Denna rundtur kan orsaka långsam sidinläsning vilket kan leda till lägre konverteringsgrader.

[!DNL Catalog Service] är en Storefront Services Gateway. Tjänsten har åtkomst till en separat databas som innehåller produktinformation och relaterad information, t.ex. produktattribut, varianter, priser och kategorier. Tjänsten synkroniserar databasen med Adobe Commerce genom indexering.
Eftersom tjänsten åsidosätter direkt kommunikation med programmet kan den minska fördröjningen för begäran- och svarscykeln.

De centrala systemen och tjänsterna i GraphQL kommunicerar inte direkt med varandra. Du kommer åt alla system från olika URL-adresser och anrop kräver olika rubrikinformation. De två GraphQL-systemen är utformade för att användas tillsammans. GraphQL-systemet [!DNL Catalog Service] utökar huvudsystemet för att göra produktbutiksupplevelserna snabbare.

Du kan också implementera [API-nät för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) för att integrera de två Adobe Commerce GraphQL-systemen med privata och tredje parts API:er och andra programgränssnitt med Adobe Developer. Nätet kan konfigureras så att anrop som dirigeras till varje slutpunkt innehåller rätt auktoriseringsinformation i rubrikerna.

## Arkitektinformation

I följande avsnitt beskrivs några av skillnaderna mellan de två GraphQL-systemen.

### Schemahantering

Eftersom Catalog Service fungerar som en tjänst behöver integratörer inte bekymra sig om den underliggande versionen av Commerce. Syntaxen för frågorna är densamma för alla versioner. Dessutom är schemat konsekvent för alla handlare. Den här konsekvensen gör det enklare att fastställa bästa praxis och ökar återanvändningen av widgetar för butiker avsevärt.

### Förenkling av produkttyper

Schemat minskar antalet olika produkttyper till två användningsområden:

* Enkla produkter är produkter som definieras med ett enda pris och en enda kvantitet. Katalogtjänsten mappar enkla, virtuella, hämtningsbara och presentkortsprodukter till `simpleProductViews`.

* Komplexa produkter består av flera enkla produkter. Komponentens enkla produkter kan ha olika priser. En komplex produkt kan också definieras så att kunden kan ange hur många av de enkla komponentprodukterna som ska ingå. Katalogtjänsten mappar de konfigurerbara, paketerade och grupperade produkttyperna till `complexProductViews`.

Komplexa produktalternativ förenas och särskiljs utifrån deras beteende, inte typ. Varje alternativvärde representerar en enkel produkt. Det här alternativvärdet ger tillgång till de enkla produktattributen, inklusive pris. När kunden väljer alla alternativ för en komplex produkt pekar kombinationen av de valda alternativen på en viss enkel produkt. Den enkla produkten är tvetydig tills kunden väljer ett värde för alla tillgängliga alternativ.

#### Produktvyattribut

Både enkla och komplexa produkter har kunddefinierade attribut som kan visas i butiken. Dessa attribut returneras som [ProductViewAttributes](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type). I Adobe Commerce definieras de tillgängliga attributen när produkten skapas. Du kan lägga till ytterligare attribut från Adobe Commerce backend eller programmatiskt. Se [Utöka och anpassa SaaS-dataexportfeed-data](../data-export/extensibility-and-customizations.md).

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

[!BADGE Endast PaaS]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."}

Installationsprocessen kräver att [Commerce Services Connector](../landing/saas.md) konfigureras. När det är klart är nästa steg att en systemintegratör ska uppdatera storefront-koden så att den innehåller [!DNL Catalog Service]-frågorna. Alla [!DNL Catalog Service]-frågor dirigeras till GraphQL gateway. URL:en anges under introduktionsprocessen.
