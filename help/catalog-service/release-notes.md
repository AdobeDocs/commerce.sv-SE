---
title: Versionsinformation för [!DNL Catalog Service]
description: Den senaste versionsinformationen för  [!DNL Catalog Service]  för Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 93adab667d1d8ed40c9d5668db376493bd8ae684
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Versionsinformation för [!DNL Catalog Service]

De här versionsinformationen beskriver de senaste versionerna av [!DNL Catalog Service].
Support ges för den aktuella större versionen. Versionsinformation för äldre versioner finns som referens.
Bland uppdateringarna finns:

![Nya](../assets/new.svg) nya funktioner
![Korrigera &#x200B;](../assets/fix.svg) Korrigeringar och förbättringar
![Fel](../assets/bug.svg) Kända fel

## Aktuell huvudversion

### Version V1.26

_22 oktober 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) GraphQL-schemat innehåller nu attributet `lastModifiedAt` i produktinformationen. Den exakta tidsstämpeln hjälper kunderna att säkerställa att webbplatskartorna korrekt återspeglar de senaste uppdateringarna av deras produkter. Det hjälper även sökmotorer som Google att avgöra när omindexering är nödvändig, att optimera crawlningsprocessen och förhindra problem med aggressiva ändringsdatum som används när exakt information inte finns tillgänglig. <!--DATA-6209-->

## Tidigare versioner

+++ Tidigare versioner

### Version V1.23

_22 augusti 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Korrigera](../assets/fix.svg) Du kan nu hämta produktinformation utan produktåsidosättningsdata (priser). I tidigare versioner returnerade dessa frågor följande fel:
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### Version V1.22

_13 augusti 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd har lagts till för att hämta alla varianter efter produkt-SKU. Se [API-referens för katalogtjänst](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Version V1.22

_13 augusti 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd har lagts till för att hämta alla varianter efter produkt-SKU. Se [API-referens för katalogtjänst](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Version V1.19

_23 maj 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare


![Korrigera](../assets/fix.svg) <!--DATA-5033-->Flaggan `InStock` för alternativvärden tar nu hänsyn till produktvariantens omfångsstatus `enabled` .

![Korrigera](../assets/fix.svg) <!--DATA-5888-->Lägg till stöd för produktpriser som kräver stora tal (upp till 16 siffror) och större decimalprecision (upp till 4 decimaler). Om du vill tillämpa priskonfigurationsuppdateringarna på din befintliga katalog synkroniserar du om katalogdata från [kontrollpanelen för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard), eller genom att använda kommandoradsgränssnittet [Adobe Commerce](../landing/catalog-sync.md#command-line-interface).

#### Kända begränsningar

Följande funktioner stöds ännu inte:

* Den största tillåtna storleken för dynamisk attributnyttolast är 9 MB.
* Gruppens produktpris kan beräknas med enkla produktpriser.
* I en bildarray innehåller endast den första bilden roller.

Lös följande begränsningar med API Mesh och Core GraphQL API:

* Lägsta kampanjpris
* Nivåpriser
* Paketprodukter med fasta priser

Mer information och exempel finns i [Katalogtjänst och API-nät](mesh.md)

### Version V1.18

_11 april 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Stöd för PHP 8.3 har lagts till.

![Nytt](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) - och [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)-frågorna returnerar nu anpassningsbara alternativdata för både enkla och komplexa produkter.<!--DATA-5538-->

### Version V1.17

_22 februari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) är nu tillgängligt. Den här förbättrade instrumentpanelen ger insikter i dataströmmar för [!DNL Product Recommendations], [!DNL Live Search] och [!DNL Catalog Service]. Stöd för den här funktionen introducerades i v3.1.0 i metapaketet `catalog-service`.

### Version V1.16

_13 februari 2024_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nya](../assets/new.svg) produktvideor stöds nu av katalogtjänstens API.
![Korrigera](../assets/fix.svg) Utmediefiler visas nu i PDP-widgeten.

#### Kända begränsningar

Dessa funktioner stöds ännu inte:

* Den största tillåtna storleken för dynamisk attributnyttolast är 9 MB.
* Gruppproduktpris. Detta värde kan beräknas med enkla produktpriser.
* I en bildarray innehåller endast den första bilden roller.

Följande begränsningar kan åtgärdas med API Mesh och Core GraphQL API:

* Lägsta kampanjpris
* [Nivåpriser](mesh.md)

### Version V1.13

_12 oktober 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst stöder flaggan `inStock` för produktvarianter.
![Nytt](../assets/new.svg) Fälten `urlKey` och `externalId` har lagts till i GraphQL-schemat.
![Nya](../assets/new.svg) hämtningsbara produkter och presentkort stöds nu.

### Version V1.12

_19 september 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst använder nu [SaaS-prisindexering](../price-index/price-indexing.md).
![Korrigera](../assets/fix.svg) Den här versionen innehåller felkorrigeringar och förbättringar på tjänstsidan.

### Version V1.11

_18 juli 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst har nu stöd för GraphQL-frågan [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) för produktrekommendationer.

### Version V1.10

_27 juni 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nytt](../assets/new.svg) Katalogtjänstens API har nu stöd för `related products`.

### Version V1.7

_12 april 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) katalogtjänst rensar nu bort produktvarianter som tagits bort.
![Korrigera](../assets/fix.svg) Infrastrukturskalbarhet och prestandaförbättringar.

### Version V1.6

_28 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Nya](../assets/new.svg) tillagda färgrutor i frågan [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nytt](../assets/new.svg) har lagt till möjligheten att hämta `entityId` med [API-nät](mesh.md).

### Version V1.5

_6 mars 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.4 och senare

![Ny](../assets/new.svg) tillagd [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL-funktionalitet.
![Korrigera](../assets/fix.svg) Förbättrade prestanda och API-skalbarhet.

### Version V1.4

_7 februari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Katalogtjänstmetapaket har publicerats för att förenkla installationsstegen.
![Åtgärda](../assets/fix.svg) API-skalbarhet och prestandaförbättringar.

### Version V1.3

_17 januari 2023_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Förenklat och förbättrat startupplevelsen.
![Nya](../assets/new.svg) slutpunkter för kundsandlådan är tillgängliga för testning före produktion.
![Nytt](../assets/new.svg)-stöd har lagts till för virtuella produkter.
![Åtgärda](../assets/fix.svg) API-skalbarhet och prestandaförbättringar.

### Version V1.1

_18 november 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Ny](../assets/new.svg) katalogtjänst har nu stöd för Adobe [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/).
![Korrigera](../assets/fix.svg) Förbättrad API-skalbarhet och övergripande prestanda.

### Version V1.0

_4 oktober 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nytt](../assets/new.svg) Nu stöd för paketerade och grupperade produkter.
![Ny](../assets/new.svg) har lagt till åsidosättningar av B2B-synlighet. Produkterna är nu sökbara och kan läggas till i kundvagnen för specifika kundgrupper.
![Korrigera](../assets/fix.svg)-tjänsten är nu stabilare och har förbättrat prestandan.

### 0.3-utgåvan - Beta+

_12 september 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nya](../assets/new.svg) bilder för variantstöd: produktbilder returneras baserat på de valda alternativen
![Nytt](../assets/new.svg) Roller för prissupport: Tillåt endast medlemmar i specifika kundgrupper att se priset på produkter
![Åtgärda](../assets/fix.svg) Förbättrad stabilitet och prestanda för tjänsten
![Nya](../assets/new.svg) uppdateringar tas emot när produkter tas bort från katalogen

### Beta Release

_9 augusti 2022_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.x och senare

![Nya](../assets/new.svg) `products` - och `refineProduct`-frågor returnerar följande data:

* Fördefinierade produktattribut (system).
* Dynamiska produktattribut och filtrera dem efter roll (produktvisningssida/produktlistsida).
* Produktalternativ.
* Produktbilder och filtrera dem efter roll (PDP/PLP).
* Ett specifikt pris för enkla produkter och prisintervall för konfigurerbara produkter.
* Kundgruppspriser och prisintervall. De returnerar ett standardgrundpris för kunderna utan någon kundgrupp.
* Produkttyper där B2B-kundspecifika priser används.
