---
title: Rekommendationsfilter
description: Lär dig hur du använder filter för att kontrollera vilka produkter som visas i  [!DNL Adobe Commerce Optimizer] rekommendationerna.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 746c016f149fb49b9c483968a8a5f40196b163ed
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Filterprodukter

[!DNL Adobe Commerce Optimizer] tillämpar automatiskt icke-konfigurerbara standardfilter på rekommendationsenheter. Om du har distribuerat flera rekommendationsenheter till en sida filtrerar [!DNL Adobe Commerce Optimizer] bort alla produkter som upprepas i enheterna. Endast den första referensen till en upprepad produkt används för att ge plats åt andra produkter som kan rekommenderas. [!DNL Adobe Commerce Optimizer] filtrerar även bort tidigare köpta produkter och produkter som finns i kundvagnen.

När du [skapar](create.md) en rekommendationsenhet kan du definiera filter som styr vilka produkter som kan visas i rekommendationer. Dessa filter baseras på en uppsättning villkor för inkludering eller exkludering som du anger. Endast produkter som uppfyller alla inkluderingsvillkor visas i rekommendationerna. Produkter som uppfyller något av exkluderingsvillkoren rekommenderas inte.

Du kan konfigurera flera filter och endast aktivera de du vill genom att markera växlingsknappen på varje filtersida. På så sätt kan du skapa utkast av filter för framtida bruk. Antalet aktiverade filter visas på varje flik.

## Villkor

Villkoren kan vara statiska eller dynamiska.

- Ett statiskt villkor använder befintliga produktattribut för att avgöra vilka produkter som kan visas i enheten. Du kan till exempel ange att endast lagerförda produkter med ett pris som är högre än $25 visas i enheten.

- Ett dynamiskt villkor som är avgörande för en kunds aktuella kontext, till exempel den kategori eller produkt som visas för tillfället. När du t.ex. skapar en produktrekommendation som ska distribueras på produktinformationssidor kan du skapa ett villkor som bara rekommenderar produkter som ligger inom ett relativt prisintervall för den produkt som visas.

### Logiska operatorer

De logiska operatorerna `AND` och `OR` används för att koppla flera villkor. Om du använder både inkluderings- och exkluderingsfilter utvärderas inkluderingarna först för att fastställa alla möjliga produkter som kan rekommenderas. Produkter som matchar eventuella exkluderingsfilter tas sedan bort från listan.

- `AND` - Förenar två inkluderingsfiltreringsvillkor
- `OR` - Förenar två villkor för exkluderingsfiltrering

## Olika typer av filter

![Filter](../../assets/rec-conditions.png)

### Produkt

Produktfiltren anger vilka specifika produkter som kan visas i rekommendationerna. Du kan inte välja produkter som är inaktiverade eller inte synliga separat eftersom dessa produkter aldrig kan visas i rekommendationerna.

>[!NOTE]
>
>Underordnade produkter för en konfigurerbar produkt visas inte i en rekommendationsenhet eftersom dessa underordnade produkter har synligheten _Inte synlig enskilt_.

### Pris

Ett filter baserat på produktpriset använder det slutliga priset för att göra jämförelsen. Slutpriset inkluderar rabatter eller specialpriser som är tillgängliga för anonyma kunder.

<!--### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
