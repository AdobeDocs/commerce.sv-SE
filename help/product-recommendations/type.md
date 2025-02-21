---
title: Rekommendationstyper
description: Lär dig mer om rekommendationer som du kan distribuera till olika sidor på din webbplats.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# Rekommendationstyper

Adobe Commerce tillhandahåller en stor uppsättning rekommendationer som du kan distribuera till olika sidor på din webbplats. Alla rekommendationstyper är databaserade. De bygger på beteendedata, produktattributdata och mätvärden. Rekommendationstyperna grupperas enligt följande:

- [Personligt](#personalized)
- [Korsförsäljning och merförsäljning](#crossup)
- [Popularitet](#popularity)
- [Högpresterande](#highperf)

Som en god praxis rekommenderar Adobe följande riktlinjer när du använder rekommendationer:

- Diversifiera dina rekommendationstyper. Kunderna börjar ignorera rekommendationer om de föreslår samma produkter om och om igen.

- Distribuera inte samma rekommendationer till kundvagnssidan och orderbekräftelsesidan. Använd `Most Added to Cart` som kundvagnssida och `Bought This, Bought That` som orderbekräftelsesida.

- Håll sajten aktuell. Distribuera inte fler än tre rekommendationsenheter på samma sida.

- Om din butik säljer kläder kan `More like this`-rekommendationen föreslå könsspecifika produkter som inte matchar kön för den produkt som visas. Använd endast den här rekommendationstypen för kategorier som inte är kläder.

>[!NOTE]
>
>Mer information om händelserna som beskrivs i den här artikeln finns i [events](events.md).

## Personligt {#personalized}

Dessa rekommendationstyper rekommenderar produkter som baseras på den specifika kundens beteendehistorik på er webbplats. Om en kund t.ex. tidigare har bläddrat efter en jacka eller köpt en jacka på din webbplats, kan de här rekommendationerna i princip fortsätta där de slutade och rekommendera andra kavajer eller liknande produkter.

| Typ | Beskrivning |
|---|---|
| Rekommenderas för dig | Rekommenderar produkter baserat på varje kunds aktuella och tidigare beteende på plats. Visar ytterst relevanta rekommendationer baserat på kundens webbsurfnings- och inköpshistorik. Den här typen av rekommendationer är effektiv på hemsidan där de flesta shoppare börjar sin resa på en webbplats. För förstagångskunder på er webbplats som inte har genererat någon signal om att personalisera upplevelsen visar Adobe Commerce produkter baserat på den mest visade rekommendationstypen. När kunderna börjar interagera med produkterna på webbplatsen rekommenderar vi dock att produkterna anpassar sig i realtid till deras beteende.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori <br/><br/>**Föreslagna etiketter:**<br/> - Endast för dig<br/>- Rekommenderas för dig<br/> - Inspirerad av dina shoppingtrender |
| Nyligen visade | Visar produkter som kunden senast tittat på, baserat på webbläsarhistorik. Alla borttagna produkter tas bort av rekommendationsenheten. Rekommendationsenheten visas inte om det inte finns någon webbläsarhistorik eller om det inte finns tillräckligt med historik när filterregler tillämpas. Om resultatet innehåller färre produkter än vad som är konfigurerat, visar rekommendationsenheten endast de returnerade produkterna.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori<br/> - Produktinformation<br/>- Kundvagn<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/>- Nyligen visade<br/>- Ta en annan titt |

## Korsförsäljning och merförsäljning {#crossup}

Dessa rekommendationstyper är sociala bevis som hjälper kunderna att hitta det andra gillar eller produktdrivna för att hjälpa dem att hitta andra liknande produkter. De rekommenderade produkterna kompletterar ofta den valda produkten.

>[!NOTE]
>
>Rekommendationstyperna &quot;visade detta, visade att&quot;, &quot;såg det här, köpte det&quot; och &quot;köpte det här&quot;, använde inte enkla förekomstmått utan snarare en mer avancerad samarbetsfiltreringsalgoritm som letar efter *intressanta likheter* som inte skevas mot populära produkter. De data som används för att informera om de här rekommendationstyperna baseras på kundens samlade beteende som härrör från flera sessioner på er webbplats. Informationen baseras inte på kundbeteende som härletts från en enstaka sessionsförekomst på er webbplats. De här rekommendationstyperna hjälper kunderna att hitta närliggande produkter som kanske inte är självklara att kombinera med den produkt som visas just nu.

| Typ | Beskrivning |
|---|---|
| Visade det här, såg du att | Rekommenderar produkter som kunderna ser oproportionerligt oftare med den produkt de nu använder.<br/><br/>**Var används:**<br/>- Produktinformation<br/>- Kundvagn<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/>- Kunder som visade den här produkten visade också (PDP) |
| En titt på det här, köpte det | Rekommenderar produkter som kunderna tenderar att köpa oproportionerligt oftare efter att ha tittat på den aktuella produkten. Den här typen hjälper kunderna att upptäcka produkter som de annars kanske inte har märkt.<br/><br/>**Var används:**<br/>- Produktinformation<br/>- Kundvagn<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/>- Kunder som har tittat på den här ultimata versionen har köpt<br/>- Kunder som har köpt <br/> - Vad köper andra efter att ha tittat på den här produkten? |
| Köpte den här, köpte den där | Rekommenderar produkter som kunderna köper oproportionerligt oftare med den produkt de nu använder. Den här typen visar mycket relevanta produkter som kunderna kan lägga till i sina varukorgar genom att aggregera vad andra kunder har köpt med den aktuella produkten.<br/><br/>**Var den används:**<br/>- Produktinformation<br/>- Kundvagn<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/>- Hämta allt du behöver<br/>- Glöm inte dessa<br/>- Köps ofta tillsammans |
| Mer som detta | Rekommenderar produkter baserade på liknande metadata som namn, beskrivning, kategoritilldelning och attribut. Genom att utvärdera attributen för de produkter som visas rekommenderar den här typen liknande produkter i samma kategori. Om en kund till exempel surfar på yogamattor rekommenderar vi andra produkter i kategorin. Eftersom den här rekommendationstypen inte särskiljer gendrar rekommenderas inte kläder, mode eller andra könsspecifika vertikaler.<br/><br/>**Var används:**<br/>- Produktinformation<br/>- KART<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/> - Fler produkter som detta<br/> - Liknar detta |
| [Visuell likhet](#visualsim) | Rekommenderar produkter som ser ut ungefär som den produkt som visas. Den här rekommendationstypen är mest användbar om bilder och de visuella aspekterna av produkter är viktiga för shoppingupplevelsen. |

## Popularitet {#popularity}

Rekommendationstyperna rekommenderar produkter som är populäraste eller trendaste inom de senaste sju dagarna.

| Typ | Beskrivning |
|---|---|
| Mest visade | Rekommenderar produkter som har visats mest genom att räkna antalet sessioner där en visningsåtgärd har utförts under de senaste sju dagarna.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori<br/>- Produktinformation<br/>- Kart<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/>- Den populäraste <br/>- Trending<br/> - Populär just nu<br/>- Nyligen populära<br/> - Populära produkter inspirerade av den här produkten (PDP)<br/>- De populäraste försäljarna |
| Mest köpta | Rekommenderar de produkter som oftast köpts av kunder under de senaste sju dagarna.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori<br/> - Produktinformation<br/>- Kart<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/> - Den populäraste <br/>- Trending<br/> - Populär just nu<br/>- Nyligen populära<br/> - Populära produkter inspirerade av den här produkten (PDP)<br/>- De populäraste försäljarna |
| Mest tillagt i kundvagn | Rekommenderar produkter som oftast läggs till i varukorgar av shoppare under de senaste sju dagarna. Den här rekommendationstypen kan användas på alla sidor.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori<br/> - Produktinformation<br/>- Kart<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/> - Den populäraste <br/>- Trending<br/> - Populär just nu<br/>- Nyligen populära<br/> - Populära produkter inspirerade av den här produkten (PDP)<br/>- De populäraste försäljarna |
| Trender | Rekommenderar produkter baserat på den senaste tiden för en produkts popularitet på webbplatsen.<br/><br/>Adobe Sensei samlar ihop information om surfning och köp på hela webbplatsen för att avgöra och rangordna vilka produkter som är mest populära hos era kunder. Eftersom Trending analyserar den senaste produktutvecklingen är det en effektiv rekommendationstyp för kataloger med hög omsättning. Om din katalog är mer statisk kanske den inte är lika användbar om inte målgruppens shoppingmönster är mycket varierande.<br/><br/>När det används på startsidan rekommenderar Trending produkter som nyligen är populära på hela webbplatsen. Trending visar inte produkter som är konsekvent populära, utan de som nyligen har blivit populära. Om du t.ex. har en e-postmarknadsföringskampanj som marknadsför vissa produkter ökar den popularitet som e-postmeddelandet genererar sannolikheten för att de produkter som marknadsförs klassificeras som trender.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori<br/> - Produktinformation<br/>- Kundvagn<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/>- Trending<br/> - Trending now<br/> - Recent trending<br/> - Hot products<br/> - Trending related products (PDP) |

## Högpresterande {#highperf}

Rekommendationstyperna rekommenderar högpresterande produkter baserat på kriterier för framgång, som tillägg till kundvagnen eller konverteringsgrader.

| Typ | Beskrivning |
|---|---|
| Visa för köpkonvertering | Rekommenderar produkter med den högsta konverteringsgraden mellan visningar och köp. Av alla kundsessioner som registrerade en produktvy, hur stor andel är det som till slut registrerade ett köp av kunden?<br/><br/>**Var används:**<br/>- Startsida<br/>- Kategori<br/>- Produktinformation<br/>- Kundvagn<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/> -De viktigaste säljarna<br/>- Populära produkter<br/>- Du kan vara intresserad av |
| Konvertering av vy till kundvagn | Rekommenderar produkter med den högsta konverteringsgraden för visning till kundvagn. Av alla kundsessioner som registrerade en produktvy, hur stor andel av kunderna som till slut registrerade ett tillägg i kundvagnen.<br/><br/>**Var används:**<br/>- Startsida<br/>- Kategori<br/> - Produktinformation<br/>- Kundvagn<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/> - De viktigaste säljarna<br/> - Populära produkter<br/> - Du kan vara intresserad av |
| Mest köpta | Den här rekommendationstypen kallas ofta&quot;Top Sellers&quot; och räknar antalet sessioner där en platsbeställningsåtgärd utfördes under de senaste sju dagarna. Den här rekommendationstypen kan användas på alla sidor.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori<br/> - Produktinformation<br/>- Kart<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/> - Den populäraste <br/>- Trending<br/> - Populär just nu<br/>- Nyligen populära<br/> - Populära produkter inspirerade av den här produkten (PDP)<br/>- De populäraste försäljarna |
| Mest tillagt i kundvagn | Rekommenderar produkter som oftast läggs till i varukorgar av shoppare under de senaste sju dagarna. Den här rekommendationstypen kan användas på alla sidor.<br/><br/>**Var används:**<br/>- Hemsida<br/>- Kategori<br/> - Produktinformation<br/>- Kart<br/>- Bekräftelse <br/><br/>**Föreslagna etiketter:**<br/> - Den populäraste <br/>- Trending<br/> - Populär just nu<br/>- Nyligen populära<br/> - Populära produkter inspirerade av den här produkten (PDP)<br/>- De populäraste försäljarna |

## Visuell likhet {#visualsim}

Rekommendationstypen _Visuell likhet_ rekommenderar produkter som liknar den produkt som visas. Rekommendationstypen är mest användbar när bilder och visuella aspekter av produkterna är viktiga delar av shoppingupplevelsen.

### Så här fungerar det

Rekommendationstypen _Visuell likhet_ ger rekommendationer för andra produkter i din katalog som har en visuell likhet med den bild som visas för tillfället. Visuell likhet omfattar aspekter som:

- Färg
- Form
- Storlek
- Textur
- Material
- Stil

Adobe Sensei använder AI för att bearbeta och analysera bilderna i din katalog och skapa attribut som används för att fastställa visuella likheter.

>[!NOTE]
>
> Om du testar den här rekommendationstypen i en icke-produktionsmiljö måste du se till att dina bild-URL:er är tillgängliga för alla.

>[!NOTE]
>
> För närvarande måste produktbilderna vara högst 10 MB stora.

Eftersom den här rekommendationstypen inte kan användas för de flesta kataloger är den inte aktiverad som standard. Du måste uttryckligen aktivera den här rekommendationstypen.

### Aktivera rekommendationstyp för visuell likhet

>[!NOTE]
>
> Rekommendationstypen _Visuell likhet_ är tillgänglig när du [installerar](install-configure.md) den som en valfri modul.

1. Gå till **Marknadsföring** > _Kampanjer_ > **Produktrekommendationer** på sidofältet _Admin_ för att visa kontrollpanelen _Produktrekommendationer_.

1. Klicka på **Inställningar** (kugghjulsikon) för att visa sidan _Inställningar_ .

1. I avsnittet _Visuella rekommendationer_ väljer du att **aktivera visuella rekommendationer**.

1. Klicka på **Spara ändringar** när du är klar.

   Sidan [Skapa ny rekommendation](create.md) visar nu **Visuell likhet** som en valbar rekommendationstyp när sidtypen är **Produktinformation**.

När du har aktiverat visuella rekommendationer initierar Adobe Sensei bildbearbetningen. Hur lång tid det tar beror på storleken på katalogen.

### Används

- Produktinformation

### Föreslagna butiksetiketter

- Du kanske också gillar
- Vi hittade andra produkter du kanske gillar
- Inspirerad av denna stil

### Exempel

Följande bild visar produktinformationssidan för _Klammerbevakningen_:

![Klammerklocka](assets/visual-sim-pdp.png)

Nedan visas rekommendationsenheten _Visuell likhet_ för _Klammerbevakning_:

![Visuell likhetsenhet](assets/visual-sim-unit.png)
