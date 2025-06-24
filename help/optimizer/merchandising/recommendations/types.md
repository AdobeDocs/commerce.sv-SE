---
title: Rekommendationstyper
description: Lär dig mer om rekommendationer som du kan distribuera till olika sidor på din webbplats.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# Rekommendationstyper

Adobe Commerce Optimizer tillhandahåller en stor uppsättning rekommendationer som du kan distribuera till olika sidor på din webbplats. Alla rekommendationstyper är databaserade. De bygger på beteendedata, produktattributdata och mätvärden. Rekommendationstyperna grupperas enligt följande:

- [Personligt](#personalized)
- [Korsförsäljning och merförsäljning](#crossup)
- [Popularitet](#popularity)
- [Högpresterande](#highperf)

>[!NOTE]
>
>Mer information om händelserna som beskrivs i den här artikeln finns i [events](../../setup/events/overview.md).

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
