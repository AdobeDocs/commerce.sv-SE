---
title: Konfigurera Live Search
description: Arbetsytan  [!DNL Live Search] används för att konfigurera, hantera och övervaka sökprestanda.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: 4634df5ef5421275d44a6a3419a4f55c11e4be45
workflow-type: tm+mt
source-wordcount: '2013'
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

Om du är vårdkund och har installerat [Data Services HIPAA-tillägget](../data-connection/hipaa-readiness.md#installation), som ingår i [dataanslutningen](../data-connection/overview.md) , hämtas inte längre data för händelsen storefront som används av [!DNL Live Search]. Detta beror på att händelsedata för storefront genereras på klientsidan. Om du vill fortsätta att hämta och skicka data för butikshändelser aktiverar du händelseinsamlingen för [!DNL Live Search] igen. Mer information finns i [allmän konfiguration](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Ange omfånget

Inledningsvis är [scope](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) för alla [!DNL Live Search]-inställningar inställda på `Default Store View`. Om din [!DNL Commerce]-installation innehåller flera butiksvyer anger du **Scope** till den [butiksvy](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) där dina facet-inställningar gäller.

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

Granska uppsättningen med [sökbara](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`) produktattribut om du vill skapa målinriktade resultat. Gör attributen sökbara för att säkerställa relevans om de innehåller innehåll som har en tydlig och koncis betydelse. Undvik att använda attribut som innehåller mindre exakt, lång text, till exempel `description`, som kan minska precisionen i sökresultaten även om sökfunktionen är aktiverad som standard. Om en person t.ex. söker efter &quot;kortfilmer&quot; och det finns skjortor med en beskrivning som innehåller ordet &quot;kortärmar&quot;, kommer skjortorna att inkluderas i sökresultaten.

Om du vill tillåta att attribut kan sökas igenom utför du följande steg:

1. Gå till **Store** > *Attribut* > **Produkt** i Admin.
1. Välj det attribut som du vill ska vara sökbart, till exempel `color`.
1. Välj **Egenskaper för Storefront** och ange **Använd i sökning** till `yes`.

[!DNL Live Search] respekterar också [weight](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search) för ett produktattribut, som angetts i Adobe Commerce. Attribut med högre vikt visas högre i sökresultatet.

Följande attribut är alltid sökbara:

- `sku`
- `name`
- `categories`

### Sök och expandera söktyper i flera lager

Sökning i flera lager, eller sökning i en sökning, är ett kraftfullt, attributbaserat filtreringssystem som utökar den traditionella sökfunktionen till att omfatta ytterligare sökparametrar. Dessa ytterligare sökparametrar ger en mer exakt och flexibel produktupptäckt.

>[!NOTE]
>
>Sök i flera lager finns i Live Search 4.6.0.

Med sökning i flera lager kan du

- Gör det möjligt för kunderna att söka i sökresultaten.
- Använd `startsWith` och `contains` sökindexering i det andra lagret i sökningen med lager om du vill förfina resultatet ytterligare.

De avancerade sökfunktionerna implementeras via parametern `filter` i [`productSearch` query ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) med hjälp av specifika operatorer:

- **Skiktad sökning** - Sök i ett annat söksammanhang - Med den här funktionen kan du utföra upp till två söklager för dina sökfrågor. Exempel:

   - **Layer 1-sökning** - Sök efter &quot;motor&quot; på `product_attribute_1`.
   - **Layer 2 search** - Search for &quot;part number 123&quot; on `product_attribute_2`. Det här exemplet söker efter &quot;part number 123&quot; i resultatet för &quot;engine&quot;.

  Skiktad sökning är tillgänglig för både `startsWith`-sökindexering och `contains`-sökindexering i det andra lagret i sökningen med lager, vilket beskrivs nedan:

- **börjarMed sökindexering** - Sök med `startsWith`-indexering. Den nya funktionen gör att:

   - Söker efter produkter där attributvärdet börjar med en angiven sträng.
   - Om du konfigurerar en&quot;slutar med&quot;-sökning kan kunderna söka efter produkter där attributvärdet slutar med en viss sträng. Om du vill aktivera sökningen &quot;slutar med&quot; måste produktattributet vara inverterat och API-anropet ska också vara en omvänd sträng. Om du till exempel vill söka efter ett produktnamn som slutar med &quot;byxor&quot;, måste du skicka det som &quot;stnap&quot;.

- **innehåller sökindexering** - Sök efter ett attribut som använder innehåller indexering. Den nya funktionen gör att:

   - Söker efter en fråga i en större sträng. Om en kund till exempel söker efter produktnumret &quot;PE-123&quot; i strängen &quot;HAPE-123&quot;.

      - Obs! Den här söktypen skiljer sig från den befintliga [frassökningen](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase), som utför en automatisk sökning. Om produktattributvärdet till exempel är &quot;utomhusbyxor&quot; returnerar en frassökning ett svar för &quot;out pan&quot;, men returnerar inget svar för &quot;or ants&quot;. En sökning innehåller emellertid ett svar på &quot;eller ants&quot;.

De här nya villkoren förbättrar funktionen för filtrering av sökfrågor för att förfina sökresultaten. De här nya villkoren påverkar inte huvudsökfrågan.

#### Implementering

1. I Admin anger [ett produktattribut](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) som sökbart.

   Se listan med sökbara [attribut](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types).

1. Ange sökfunktionen för det attributet, till exempel **Innehåller** (standard) eller **Börjar med**. Du kan ange högst sex attribut som ska aktiveras för **Innehåller** och sex attribut som ska aktiveras för **Börjar med**. Dessutom är stränglängden begränsad till högst 50 tecken för indexeringen **Innehåller**.

   ![Ange sökfunktion](./assets/search-filters-admin.png)

1. Se [utvecklardokumentationen](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) för exempel på hur du uppdaterar [!DNL Live Search] API-anrop med de nya `contains`- och `startsWith`-sökfunktionerna.

   Du kan implementera dessa nya villkor på sökresultatsidan. Du kan till exempel lägga till ett nytt avsnitt på sidan där användaren kan förfina sina sökresultat ytterligare. Du kan ge kunderna möjlighet att välja specifika produktattribut, t.ex.&quot;Tillverkare&quot;,&quot;Artikelnummer&quot; och&quot;Beskrivning&quot;. Därifrån söker de i dessa attribut med villkoren `contains` eller `startsWith`.

### När sökning med flera lager ska användas i stället för fack

Sök i flera lager och ansikten har olika syften för att identifiera produkter, och om du väljer mellan dem beror det på ditt specifika användningssätt:

**Använd sökning i flera lager när:**

- Du måste söka i sökresultat med hjälp av flera villkor.
- Arbeta med artikelnummer, SKU:er eller tekniska specifikationer där användarna vet partiell information.
- Shoppare måste begränsa resultaten steg för steg med kapslade kriterier.
- Du vill minska antalet API-anrop genom att kombinera flera sökvillkor i en enda fråga.
- Ni måste implementera affärsspecifika sökmönster som går utöver vanlig funktionsnavigering.

**Använd ansikten när:**

- Ger typisk filtrering av kategori, pris, varumärke och attribut
- Intuitiva filteralternativ som användarna enkelt kan förstå och välja
- Visa tillgängliga alternativ baserat på aktuella sökresultat
- Visa antal filter och intervall som hjälper användarna att förstå tillgängliga alternativ
- Arbeta med gemensamma produktegenskaper som färg, storlek, material och så vidare.

**Bästa praxis:** Använd lageruppbyggd sökning för komplexa, tekniska sökningar där användarna har specifika kriterier, och använd aspekter för vanlig e-handelsfiltrering där användarna vill utforska och begränsa alternativen visuellt.

## Ansikten och synonymer

Ansikten och synonymer är ett annat sätt att förbättra sökupplevelsen för era kunder.

[Fasetter](facets.md) är produktattribut som definieras i [!DNL Live Search] som ska kunna filtreras. Du kan ange alla filterbara attribut som en fasett i [!DNL Live Search], men det finns [begränsningar](boundaries-limits.md) för hur många aspekter du kan söka efter samtidigt.

>[!NOTE]
>
>Ett produktattribut kan bara filtreras om produktattributkonfigurationen har de nödvändiga egenskaperna: *Använd i sökning = Ja*, *Använd i sökresultat med lagernavigering=ja* och *Använd i lagernavigering=filtrerbar (med resultat)*. Om dessa egenskaper saknas eller inte är korrekt angivna visas inte attributet i Fasetkonfigurationen. Konfigurationsanvisningar finns i [Lägg till en fasett](facets-add.md#add-a-facet).

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

[!DNL Live Search] har stöd för [omdirigering av söktermer](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html) i implementeringar där Adobe Commerce hanterar routningen, t.ex. Luma och andra PHP-baserade teman.

## Standardattributvärden

Följande produktattribut har [storefront-egenskaper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) som används av [!DNL Live Search] och är aktiverade som standard.

| Egenskap | Storefront-egenskap | Attribut |
|---|---|---|
| Sorterbar | Används för sortering i produktlista | `price` |
| Sökbart | Använd i sökning | `price` <br />`sku`<br />`name` |
| FilterableInSearch | Använd i navigering i lager - filtrerbar (med resultat) | `price`<br />`visibility`<br />`category_name` |

## Standardegenskaper för icke-systemattribut

I följande tabell visas standardegenskaperna för sökning och filtrering av attribut som inte finns i systemet, inklusive de som är specifika för Luma-exempeldata. Om attributegenskapen *Använd i sökning* anges till `Yes` blir attributet sökbart i både [!DNL Live Search] och Adobe Commerce.

| Attributkod | Sökbart | Använd i navigering i lager |
|--- |--- |--- |
| aktivitet | Ja | Filterbar (med resultat) |
| attributes_brand | Ja | Nej |
| varumärke | Ja | Nej |
| klimat | Ja | Filterbar (med resultat) |
| räntekrage | Ja | Filterbar (med resultat) |
| färg | Ja | Filterbar (med resultat) |
| kostnad | Ja | Nej |
| eco_collection | Ja | Filterbar (med resultat) |
| kön | Ja | Filterbar (med resultat) |
| tillverkare | Ja | Filterbar (med resultat) |
| material | Ja | Filterbar (med resultat) |
| syfte | Ja | Filterbar (med resultat) |
| strap_bag | Ja | Filterbar (med resultat) |
| style_general | Ja | Filterbar (med resultat) |

## Standardegenskaper för systemattribut

I följande tabell visas standardegenskaperna för sökning och filterbarhet för systemattribut.

| Attributkod | Sökbart | Använd i navigering i lager |
|--- |--- |--- |
| allow_open_amount | Ja | Filterbar (med resultat) |
| description | Ja | Nej |
| name | Ja | Nej |
| pris | Ja | Filterbar (med resultat) |
| short_description | Ja | Nej |
| sku | Ja | Nej |
| status | Ja | Nej |
| tax_class_id | Ja | Nej |
| url_key | Ja | Nej |
| vikt | Ja | Nej |
