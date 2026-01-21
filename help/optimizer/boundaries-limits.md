---
title: Gränser och gränser
description: Förstå [!DNL Adobe Commerce Optimizer] gränser och gränser för att planera kapacitet och förebygga prestandaproblem.
role: Admin, Developer
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 4f238b002d1481126d4fec0a249b7f9ff437248e
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Gränser och gränser

[!DNL Adobe Commerce Optimizer] har två typer av begränsningar:

- **Licensbegränsningar** - Baserat på din inköpskapacitet kan du utöka genom att köpa ytterligare paket.
- **Systemgränser** - Fasta gränser som skyddar systemresurser och garanterar pålitliga prestanda för alla användare.

Din användning måste ligga inom dessa gränser. Överskridande av dem kan orsaka ökad fördröjning och begära begränsning.

## Begär ytterligare kapacitet

Licensgränserna kan höjas genom köp av de licenspaket som beskrivs i avsnittet [Licensbegränsningar och systemgränser](#license-limits-and-system-boundaries) eller genom förhandling om anpassad licensiering för unika användningsfall. Kontakta er kontorepresentant på Adobe för att diskutera era behov.

Kontakta [Adobe Support](https://experienceleague.adobe.com/home?lang=en#support) om du har frågor om systemgränser.

## Förhindra prestandaproblem

Följ dessa metodtips för att hålla dig inom gränserna och undvika operativa problem:

- **Granska dina gränser** - Förstå dina [kapacitetsgränser](#license-limits-and-system-boundaries) innan du startar nya butiker eller kampanjer.
- **Spåra din användning** - Använd inbyggda mätinstrumentpaneler eller CDN-loggar.

## Licensbegränsningar och systemgränser

I följande tabeller sammanfattas licensgränserna och systemgränserna per funktionsområde och information om hur man lägger till ytterligare licenser för att utöka kapaciteten där så är tillämpligt.

### Miljöbegränsningar

| **Miljö** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| **Sandlådemiljö** | Antalet sandlådemiljöer som ingår | 2 per instans | Ja<p>Lägg till ytterligare en miljölicens per instans</p> |
| **Produktionsmiljö** | Antalet produktionsmiljöer som ingår | 1 per instans | Licens<p>Lägg till ytterligare en miljölicens per instans</p> |

{style="table-layout:auto"}

### Katalog

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| Produkt- och intagningsfrekvens | Antal produkter som skapats eller uppdaterats | 1 000 uppdateringar per minut<p>Maximalt 100 000 uppdateringar per dag</p> | Ja<p>Lägg till ett licenspaket:</p><ul><li>5 000 uppdateringar per minut<br>Maximalt 500 000 uppdateringar per dag</li> <li>10 000 uppdateringar per minut<br>Maximalt 1 miljon uppdateringar per dag</li></ul><p>Den maximala kapaciteten för dataöverföring är 1 miljon uppdateringar per dag.</p> |
| Storlek på produktnyttolast | Maximal datamängd som tillåts när produktinformation skapas, uppdateras eller importeras med API:t | 200 kB | Nej |
| Katalogvariationer | Antalet vyer av en katalog som är tillgängliga för butiksanvändare,<p>som räknas som (*Antal katalogvyer × Antal prisböcker*)</p> | 100 variationer | Ja<p>Lägg till licenspaket för 100 katalogvarianter</p> |
| Produkter i en och samma katalogkälla | SKU:er som stöds i katalogen | 250 000 SKU | Ja<p>Lägg till 100 000 SKU-licenspaket</p> |
| Varianter per produkt | Antalet produktvarianter (storlek, färgkombinationer) som tillåts per produkt | 10 kB | Nej |
| Katalogkällor | Antalet katalogdatakontexter (till exempel språk eller datakällor som PIM och ERP) | 50 | Nej |

{style="table-layout:auto"}

### Prisböcker

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| Prisböcker | Antal tillåtna prisböcker per instans | Baserat på antalet [katalogvariationer](#catalog) | Ja<br>Öka katalogvariationer |
| Rabatter per prispost | Antalet rabatter som kan tillämpas på ett produktpris i en prisbok | 10 | Nej |

{style="table-layout:auto"}

### Produktvisualiseringar från AEM Assets

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| Produktvisuella effekter för avancerade användare | Licensierad användare med full digital resurshantering, inklusive AI-verktyg, Adobe Express/Firefly-integreringar och Content Hub-delning, hantering av grundläggande DAM-uppgifter och avancerade molnbaserade funktioner för optimal effektivitet. | 2 | Ja<p>Uppgradera till AEM Assets licens</p> |
| Användare av produktvisuellt samarbete | Få åtkomst till och arbeta med material genom integreringen med AEM Commerce, skapa och redigera innehåll med Adobe Express och Firefly och - om det är aktiverat - utnyttja godkänt material via Content Hub-portalen. | 2 | Ja<p>Uppgradera till AEM Assets licens</p> |
| Lagring av produktbilder | Allokerat lagringsutrymme för resurser | 1 TB lagring | Nej |
| Dynamisk medieanvändning | Beaktande av dynamiska mediebehandlingsåtgärder som omfattar:<ul><li>Bildleverans</li><li>Smart bildbehandling</li><li>Videoleverans</li></ul><p>Mer information finns i *Beräkna dynamisk medieanvändning* nedan. | Baserat på GMV<p>Minsta tilldelning: 5 miljoner operationer/månad</p> | Ja<ul><li>Inköpslicens för ytterligare operationer</li><li>Uppgradera till AEM Assets licens</li></ul> |
| Videoleverans | Erbjudande för leverans eller nedladdning av video | 300 videor, 1 minut per video | Ja<p>Uppgradera till AEM Assets licens</p> |
| Generering av tillgångar | Tillgång till generativ AI för Adobe Express och Adobe Firefly för att skapa bilder | Ingen | Köp Generative AI-krediter separat |

{style="table-layout:auto"}


>[!NOTE]
>
>**Power Users** har åtkomst till Adobe Express direkt eller inifrån Adobe Commerce Optimizer. **Medarbetare-användare** kan komma åt Adobe Express-programmet direkt. Användning styrs av [Adobe Express med Firefly produktspecifika licensvillkor](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


>[!BEGINSHADEBOX &quot;Beräkna användning av dynamiska media&quot;]

Dynamic Media-användningen spårar API-förfrågningar som kommer in i produktvisualiseringskomponenterna i Adobe Commerce Optimizer för att underlätta en av följande åtgärder:

- **Bildleverans förbrukar en dynamisk medieåtgärd** för varje förekomst av följande:
   - **grundläggande bildomformning** för en digital resurs, till exempel åtgärder för att ändra storlek, skala, formatkonvertering, komprimering eller beskärning.
   - **statisk bildleverans eller hämtning** av nämnda digitala resurser eller återgivning av digitala resurser (utom video)
- **Leverans av smarta bilder förbrukar 20 dynamiska medieåtgärder** för varje optimerad leverans av en enda digital resurs genom att automatiskt generera den lämpligaste bildåtergivningen för slutanvändarens enhet och webbläsare.
- **Videoleverans förbrukar 20 Dynamic Media Operations** för en enstaka leverans eller nedladdning av en video, eller en transformerad variant av en video.

>[!ENDSHADEBOX]


### Katalogvyer och principer

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| Katalogvyer | Antal konfigurerbara deluppsättningar av huvudkatalogen | Baserat på antalet [katalogvariationer](#catalog) | Ja<br>Öka katalogvariationer |
| Profiler per katalogvy | Antal datafilter som tillåts | 10 | Nej |
| Attributvärden i en profil | Antal produktegenskaper som kan konfigureras för filtrering | 100 | Nej |

{style="table-layout:auto"}

### Katalogarkiv

Basallokeringen för katalogbutiksfunktioner baseras på GMV-nivån. Tabellen anger minimiallokeringen för varje funktion.

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| Hämtningshastighet för katalog | Antal gånger ett katalog-API anropas per månad av ett system (storefront, transaction system, ERP eller annat) för att hämta data från katalogen | Baserat på GMV-nivån<p>Minsta tilldelning: 10 MB/månad</p> | Ja<p>Lägg till 1 miljon begäranden per månad i licenspaket</p> |
| Innehållsförfrågningar | Begäranden till Commerce Storefront för HTML sidvisningar eller JSON API-anrop. Räknas som en sidvy eller fem API-anrop. | Baserat på GMV-nivån<p>Minimiallokering: 2 MB/månad</p> | Ja<p>Lägg till 1 miljon licenser per månad</p> |
| Storefront GenAI-variationer | Möjlighet att generera textbaserat innehåll | Baserat på GMV-nivån<p>Minimiallokering: 1 000 variationer/månad</p> | Ja<p>Köp Generative AI-krediter separat</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>För bildgenerering krävs en Adobe Firefly-licens som har tilldelats samma IMS-organisation som Adobe Commerce Optimizer.


### Produktupptäckt

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| Produkter per sökbegäran | Högsta antal returnerade produkter per sida i sökresultat | 100 | Nej |
| Filterbara attribut | Antalet produktegenskaper (till exempel färg, storlek, varumärke eller material) som kan aktiveras för navigering i flera lager och för fasets | 200 | Nej |
| Sökbara attribut | Antalet produktegenskaper som kan konfigureras för användning med produktkatalogsöktjänsten | 200 | Nej |
| Sorterbara attribut | Antalet produktegenskaper som kan konfigureras för att bestämma ordningen för sökresultatvärden | 50 | Nej |
| Sidnumreringsdjup för sökning | Högsta antal produkter som är tillgängliga genom sidnumrering (t.ex. sidan 100 × 100 produkter/sida) | 10 kB | Nej |
| Fasetter | Antalet filterbara produktattribut (som varumärke, färg, storlek, pris) som kan konfigureras för att hjälpa kunderna att förfina sökresultaten och bläddra bland kategorier | 100<p>Måste vara filterbara attribut</p> | Nej |
| Alternativ per aspekt | Antalet filterbara produktattributvärden (som&quot;Red&quot;,&quot;Blue&quot; för Color;&quot;Small&quot;,&quot;Medium&quot; för Size) som kunderna kan välja från en lista | 100 | Ja<p>Kan öka via supportförfrågan</p> |

{style="table-layout:auto"}

### Rekommendationer

Följande funktioner är tillgängliga för produktrekommendationer. Vissa funktioner i andra Adobe Commerce-produkter stöds inte i [!DNL Adobe Commerce Optimizer].

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** |
| --- | --- | --- | --- |
| Aktiva rekommendationsenheter | Antal komponenter för direktrekommendationer i butiken (som&quot;Kunderna har också sett&quot; eller&quot;Du kanske också gillar&quot;) | 50 | Nej |
| Inkluderingar/uteslutningar av kategori eller attribut | Filtrera produkter till en viss uppsättning som uppfyller kraven för rekommendationer | Stöds inte | |

{style="table-layout:auto"}

### Utbyggbarhet

| **Funktion** | **Beskrivning** | **Basallokering** | **Kan utökas?** | **Anteckningar** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Kapacitet för molnbaserade tillägg och integreringar | Baserat på GMV-nivån<p>Minimiallokering: 1 paket/år</p> | Ja<p>Lägg till ytterligare paket</p> | För definierade gränser per paket, se:<ul><li>[App Builder produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html) för definierade begränsningar per paket.</li><li>[Systeminställningar och begränsningar](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) i *App Builder Runtime Guides*.</li><li>[Lagringskrav för App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each) -->
