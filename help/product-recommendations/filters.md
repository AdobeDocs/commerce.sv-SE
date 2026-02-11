---
title: Filterprodukter
description: Definiera villkor som antingen inkluderar eller utesluter produkter från att användas som rekommendationer.
exl-id: 140bf047-4f6a-48da-b536-d96e78ae3d17
source-git-commit: 1b10163c39d9f309afd24aa2e808a57e069258f8
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---

# Filterprodukter

Adobe Commerce tillämpar automatiskt icke-konfigurerbara standardfilter på rekommendationsenheter. Om du har flera rekommendationsenheter distribuerade till en sida filtrerar Adobe Commerce bort produkter som upprepas i enheterna. Endast den första referensen till en upprepad produkt används för att ge plats åt andra produkter som kan rekommenderas. Adobe Commerce filtrerar även bort produkter som köpts tidigare och produkter som finns i varukorgen.

När du [skapar](create.md) en rekommendationsenhet kan du definiera filter som styr vilka produkter som kan visas i rekommendationer. Dessa filter baseras på en uppsättning villkor för inkludering eller exkludering som du anger. Endast produkter som uppfyller alla inkluderingsvillkor visas i rekommendationerna. Produkter som uppfyller något av exkluderingsvillkoren rekommenderas inte.

Du kan konfigurera flera filter och endast aktivera de du vill genom att markera växlingsknappen på varje filtersida. På så sätt kan du skapa utkast av filter för framtida bruk. Antalet aktiverade filter visas på varje flik.

## Villkor

Villkoren kan vara statiska eller dynamiska.

- Ett statiskt villkor använder befintliga produktattribut för att avgöra vilka produkter som kan visas i enheten. Du kan till exempel ange att endast lagerförda produkter med ett pris som är högre än $25 visas i enheten. Statiska villkor är tillgängliga för alla sidtyper.

- Ett dynamiskt villkor som är avgörande för en kunds aktuella kontext, till exempel den kategori eller produkt som visas för tillfället. När du t.ex. skapar en produktrekommendation som ska distribueras på produktinformationssidor kan du skapa ett villkor som bara rekommenderar produkter som ligger inom ett relativt prisintervall för den produkt som visas. Dynamiska villkor är tillgängliga för alla sidtyper utom hemsidan och på sidor med rekommendationer som har placerats med Page Builder.

### Logiska operatorer

De logiska operatorerna `AND` och `OR` används för att koppla flera villkor. Om du använder både inkluderings- och exkluderingsfilter utvärderas inkluderingarna först för att fastställa alla möjliga produkter som kan rekommenderas. Produkter som matchar eventuella exkluderingsfilter tas sedan bort från listan.

- `AND` - Förenar två inkluderingsfiltreringsvillkor
- `OR` - Förenar två villkor för exkluderingsfiltrering

>[!NOTE]
>
> Inkluderings- och exkluderingsfilter ersätter de äldre kategoriundantagen i version 3.2.2 och senare av modulen `magento/product-recommendations`. Mer information om Adobe Commerce-versioner finns i [versionsinformationen](release-notes.md).

## Olika typer av filter {#filtertypes}

![Filter](assets/rec-conditions.png)

### Kategori

Filtrerar produkter baserat på deras kategori. Kategorifiltret använder direkta kategoritilldelningar och deras underkategorier. Om du till exempel aktiverar ett exkluderingsvillkor för kategorin `Gear` utesluts produkter som tilldelats `Gear` och alla dess underkategorier, till exempel `Gear/Bags` eller `Gear/Fitness Equipment`. Detsamma gäller för ett inkluderingsfilter för en kategori. Om du t.ex. aktiverar ett inkluderingsvillkor för kategorin `Gear` omfattar det produkter som har tilldelats `Gear` och alla dess underkategorier som `Gear/Bags` eller `Gear/Fitness Equipment`.

Kategorifältet visar kategorier som tillhör den aktuella butiksgranskningen.

>[!NOTE]
>
>För B2B-handlare följer kategorifiltret de [kundspecifika produktkategorier](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=sv-SE) som du har konfigurerat.

Adobe Commerce rekommenderar att du använder följande kategorifilterkonfiguration när du distribuerar rekommendationer till dina sidtyper:

| Sida | Filtrera efter |
|---|---|
| Startsida | Filtrera inte produkter. |
| Kategori | Filtrera produkter i den specifika kategorin. |
| Produktinformation | Filtrera produkter i samma kategorier. |
| Kundvagn | Filtrera produktkategorier i kundvagnen. |
| Orderbekräftelse | Filtrera inköpta produktkategorier. |

### Produkt

Produktfiltren anger vilka specifika produkter som kan visas i rekommendationerna. Du kan inte välja produkter som är inaktiverade eller inte synliga separat eftersom dessa produkter aldrig kan visas i rekommendationerna.

>[!NOTE]
>
>Underordnade produkter för en konfigurerbar produkt visas inte i en rekommendationsenhet eftersom dessa underordnade produkter har synligheten _Inte synlig enskilt_.

### Typ

Ett filter baserat på produkttyp innehåller eller utesluter antingen alla produkter av en viss typ. Typer som stöds är _simple_, _configurable_, _virtual_, _downloadable_ eller _presentcard_. _Paket_, _grupperad_ och anpassade produkttyper stöds inte.

### Synlighet

Filtrerar produkter baserat på synlighet, till exempel: _Katalog_, _Sök_ eller båda.

### Pris

Ett filter baserat på produktpriset använder det slutliga priset för att göra jämförelsen. Slutpriset inkluderar alla rabatter som anonyma kunder kan få. För B2B-handlare återspeglar det pris som visas de [kundspecifika grupppriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=sv-SE) som du har konfigurerat.

### Lagerstatus

Följande exkluderingsfilter kan användas för att filtrera produkter baserat på lagerstatus:

- Slut på lager - (endast undantag) Exkluderar produkter som inte finns i lager.
- Låga lagernivåer - (endast undantag) Exkluderar produkter med låga lagernivåer. Låg lagerstatus baseras på värdet _Endast X vänster tröskelvärde_ i [lagerkonfigurationen](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/inventory.html?lang=sv-SE).
