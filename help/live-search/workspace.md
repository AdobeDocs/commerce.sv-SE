---
title: Konfigurera Live Search
description: Arbetsytan  [!DNL Live Search] används för att konfigurera, hantera och övervaka sökprestanda.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Konfigurera Live Search

På arbetsytan kan du konfigurera, hantera och övervaka prestanda för [!DNL Live Search]. Menyn längst upp ger åtkomst till verktygen i varje funktionsområde. De tillgängliga funktionerna återspeglar det aktuella menyvalet.

![Workspace](assets/workspace.png)

## Datainsamling

För att säkerställa att alla funktionsområden på arbetsytan innehåller rätt data måste du konfigurera datainsamling baserat på den valda butiksimplementeringen:

1. Luma - Datainsamling är tillgänglig direkt.
1. Headless - Datainsamlingen måste konfigureras manuellt, beroende på butiksimplementering.

Om du använder en headless-butik kan du läsa följande dokumentation för att få mer information om vilka händelser som behöver läggas till:

- [Nödvändiga händelser](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) för Live Search-instrumentpanelen.
- [Storefront-händelseinsamlaren](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) som måste läggas till som en förutsättning.
- [Exempel](https://github.com/adobe/commerce-events/tree/main/examples) på händelsestrukturen.

### Sjukvårdskunder

Om du är vårdkund och har installerat [Data Services HIPAA-tillägget](../data-connection/hipaa-readiness.md#installation), som ingår i [dataanslutningen](../data-connection/overview.md) , hämtas inte längre data för händelsen storefront som används av [!DNL Live Search]. Detta beror på att händelsedata för storefront genereras på klientsidan. Om du vill fortsätta att hämta och skicka data för butikshändelser aktiverar du händelseinsamlingen för [!DNL Live Search] igen. Mer information finns i [allmän konfiguration](https://experienceleague.adobe.com/sv/docs/commerce-admin/config/general/general#data-services).

## Ange omfånget

Inledningsvis är [scope](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=sv-SE#scope-settings) för alla [!DNL Live Search]-inställningar inställda på `Default Store View`. Om din [!DNL Commerce]-installation innehåller flera butiksvyer anger du **Scope** till den [butiksvy](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=sv-SE) där dina facet-inställningar gäller.

## Menyalternativ

| Alternativ | Beskrivning |
|--- |--- |
| [Prestanda](performance.md) | Instrumentpanelen ger dig insikt i hur produktsökningar fungerar. |
| [Motstående](facets.md) | Högpresterande filtrering som använder flera dimensioner av attributvärden för att förfina sökvillkoren. |
| [Synonymer](synonyms.md) | Utvidga sökräckvidden och inkludera ord som kunderna kan använda för att hitta produkter som skiljer sig från dem i katalogen. |
| [Söka efter marknadsföring](rules.md) | Formge sökupplevelsen med logiska regler som utlöser schemalagda åtgärder. Öka, begrava, fästa eller dölj produkter för att kalibrera sökresultaten efter era affärsmål. |
| [Kategorimarknadsföring](category-merch.md) | Använd regler och intelligent marknadsföring på kategorinivå. |
| [GraphQL](graphql.md) | Utvecklare som är inloggade i administratören för din butik kan skapa och testa frågor med faktiska katalogdata. Mer information finns på [GraphQL Overview](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) i utvecklardokumentationen för [!DNL Live Search]. |
| [Inställningar](settings.md) | Bestäm hur prisfaktavärden grupperas efter prisintervall i butiken och ställ in indexeringsspråket. |

## Ange attribut som sökbara

Granska uppsättningen med [sökbara](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=sv-SE) (`searchable=true`) produktattribut om du vill skapa målinriktade resultat. Gör attributen sökbara för att säkerställa relevans om de innehåller innehåll som har en tydlig och koncis betydelse. Undvik att använda attribut som innehåller mindre exakt, lång text, till exempel `description`, som kan minska precisionen i sökresultaten även om sökfunktionen är aktiverad som standard. Om en person t.ex. söker efter &quot;kortfilmer&quot; och det finns skjortor med en beskrivning som innehåller ordet &quot;kortärmar&quot;, kommer skjortorna att inkluderas i sökresultaten.

Om du vill tillåta att attribut kan sökas igenom utför du följande steg:

1. Gå till **Store** > *Attribut* > **Produkt** i Admin.
1. Välj det attribut som du vill ska vara sökbart, till exempel `color`.
1. Välj **Egenskaper för Storefront** och ange **Använd i sökning** till `yes`.

   ![Workspace](assets/attribute-searchable.png)

[!DNL Live Search] respekterar också [weight](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html?lang=sv-SE#weighted-search) för ett produktattribut, som angetts i Adobe Commerce. Attribut med högre vikt visas högre i sökresultatet.

Följande attribut är alltid sökbara:

- `sku`
- `name`
- `categories`

[Fasetter](facets.md) är produktattribut som definieras i [!DNL Live Search] som ska kunna filtreras. Du kan ange alla filterbara attribut som en fasett i [!DNL Live Search], men det finns [begränsningar](boundaries-limits.md) för hur många aspekter du kan söka efter samtidigt.

[Synonymer](synonyms.md) är termer som du kan definiera för att hjälpa användarna att hitta rätt produkt. Användare som söker efter byxor kan skriva in &quot;byxor&quot; eller &quot;slacks&quot;. Du kan ställa in synonymer så att de här söktermerna får användarna att se resultatet.

## Konfigurationsinställningar för Commerce

I följande avsnitt beskrivs de Commerce-konfigurationsinställningar som stöds och inte stöds för [!DNL Live Search].

### Konfigurationsvärden som stöds

>[!IMPORTANT]
>
>Vi rekommenderar att du använder produktlistwidgetar som är aktiverade som standard i Live Search 4.0.0. Widgetarna är avsedda att ersätta implementeringen av adaptern helt i framtida versioner. Mer information finns i [aktivera widgetar för produktlistor](install.md#enable-product-listing-widgets).

| Konfigurationsinställning för Commerce | Beskrivning | Stöds av Popover | Stöds av kortet |
|---|---|---|---|
| Stores > Configuration > Catalog > Catalog > Catalog Search > Allow All Products per Page | Om värdet är `Yes` inkluderas alternativet `ALL` i kontrollen &quot;Visa per sida&quot;. | Ja. Max 500 produkter | Ja. Max 500 produkter |
| Lagrar > Konfiguration > Katalog > Katalog > Katalogsökning > Minimal frågelängd | Det minsta antalet tecken som tillåts i en katalogsökning. | Ja | Ja |
| Stores > Configuration > Catalog > Catalog > Catalog Search > Products per Page on Grid Allowed Valowed | Anger hur många produkter som visas i stödrastervyn. | Ja | Ja |
| Stores > Configuration > Catalog > Catalog > Catalog Search > Products per Page on Grid Default Value | Anger hur många produkter som visas per sida som standard i stödrastervyn. | Ja. Max 500 produkter | Ja. Max 500 produkter |
| Stores > Configuration > Catalog > Inventory > Display out of Stock Products | Visar produkter som inte finns i lager. | Ja | Ja |
| Lager > Konfiguration > Valuta > Standardvisningsvaluta | Den primära valuta som används för att visa priser. | Ja | Ja |
| Stores > Configuration > General > Currency Setup > Currency Options > Base Currency Options | Den primära valutan som används för alla onlinebetalningstransaktioner. | Ja | Ja |

Priserna på Widget Product Listing Page och Popover konverteras till standardvisningsvalutan med de konfigurerade valutakurserna.

### Konfigurationsvärden som inte stöds

| Konfigurationsinställning för Commerce | Beskrivning | Anteckningar |
|---|---|---|
| Stores > Configuration > Catalog > Storefront > List Mode | Bestämmer formatet för sökresultatlistan. | Återger korrekt, men händelser skickas inte för vissa sidinteraktioner |
| Stores > Configuration > Catalog > Catalog > Catalog Search > Maximum Query Length | Det maximala antalet tecken som tillåts i en katalogsökning. | Inte implementerad; Search Services kan innehålla upp till 255 tecken |
| Configuration > Sales > Tax > Price Display Settings > Display Product Prices in Catalog | Avgör om produktpriser som publiceras i katalogen innehåller eller exkluderar moms eller visar två versioner av priset; den ena med och den andra utan moms |  |
| Stores > Configuration > Catalog > Storefront > Product Listing Sort By | Bestämmer sorteringsordningen i sökresultatlistan. | Gäller inte för [!DNL Live Search] [Sidwidgeten Produktlista](plp-styling.md) |

### Sökvillkor

[!DNL Live Search] har stöd för [omdirigering av söktermer](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html?lang=sv-SE) i implementeringar där Adobe Commerce hanterar routningen, t.ex. Luma och andra PHP-baserade teman.
