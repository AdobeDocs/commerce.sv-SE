---
title: Rekommendationsfilter
description: Lär dig hur du använder filter för att kontrollera vilka produkter som visas i  [!DNL Adobe Commerce Optimizer] rekommendationerna.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: 032a19183b79cea1bfe27e8a4e20c60ba5ac6b8b
workflow-type: tm+mt
source-wordcount: '403'
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

<!--### Price

A filter based on the product price uses the final price to perform the comparison. The final price includes any discounts or special pricing available to anonymous shoppers.

### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
