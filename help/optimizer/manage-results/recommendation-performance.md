---
title: Rekommendationsprestanda
description: Sidan Rekommendationer ger dig insikt i hur bra dina produktrekommendationer fungerar.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 1b77e2ea-412b-4c78-9d38-390bd8fda87e
source-git-commit: 0eea4658d554f2913c7c2d25e0c0753f22016aaa
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# Rekommendationsprestanda

På sidan Recommendations Performance (Rekommendationer prestanda) visas en lista med konfigurerade rekommendationer tillsammans med viktiga mätvärden som hjälper dig att utvärdera hur effektiva de är. Du kan konfigurera vyn så att den visar mått för den senaste dagen, veckan eller månaden. Dessa insikter visar hur ofta varje rekommendationsenhet visas eller klickas, vilket hjälper dig att utvärdera prestanda och identifiera möjligheter till optimering.

>[!INFO]
>
>En rekommendationsenhet är en widget som innehåller den rekommenderade produkten _items_.

![Rekommendationsprestanda](../assets/rec-performance.png){zoomable="yes"}

## Välj **katalogvyn**

Välj den [katalogvy](../setup/catalog-view.md) där dina rekommendationer gäller.

![Katalogvy](../assets/catalog-view.png)

## Visa en rapport

Klicka på **[!UICONTROL Date Range]** och välj ett av följande intervall:

![Rekommendationer, datumintervall](../assets/rec-perf-date-range.png)

Rekommendationstabellen uppdateras och visar mått för det datumintervallet.

## Anpassa tabell

1. Klicka på ikonen ![Kolumnväljare](../assets/icon-show-hide-columns.png) i det övre vänstra hörnet för att anpassa tabellen.

   De synliga kolumnerna är markerade.

1. Gör något av följande på menyn:

   - Om du vill visa en dold kolumn klickar du på ett kolumnnamn utan bockmarkering.
   - Om du vill dölja en synlig kolumn klickar du på ett kolumnnamn med en bock.

   Tabellen uppdateras så att den endast innehåller de markerade kolumnerna.

## Ange filter

Klicka på filterikonen om du vill filtrera mätvärdena på arbetsytan för prestandarekommendationer.

![Filtermått](../assets/rec-filters.png)

Du kan konfigurera flera värden för varje filter. Se tabellen [nedan](#column-descriptions) för beskrivningar av varje filter.

## Visa detaljer

1. Klicka på ikonen (![Mer väljare](../assets/btn-more.png)) bredvid den rekommendation du vill granska i tabellen.

1. Om du vill ändra rekommendationens status klickar du på **Aktivera** eller **Inaktivera**.

## Skapa eller hantera rekommendationer

Lär dig hur du kan [skapa en ny eller hantera en befintlig](../merchandising/recommendations/create.md)-rekommendation.

## Workspace Controls

| Kontroll | Beskrivning |
|---|---|
| ![Datumintervall](../assets/rec-perf-date-range.png) | Anger det tidsintervall som används för måttberäkningar. |
| ![Kolumnväljare](../assets/icon-show-hide-columns.png) | Anger vilka kolumner som visas i tabellen Rekommendationer. |
| Skapa rekommendation | Öppnar sidan [Skapa ny rekommendation](../merchandising/recommendations/create.md). |

## Kolumnbeskrivningar

| Kolumn | Beskrivning |
|---|---|
| Namn | Rekommendationens namn. |
| Sida | Sidan där rekommendationen visas. |
| Typ | Rekommendationstypen. |
| Status | Rekommendationsstatus. Alternativ: Inaktiv/aktiv/Utkast |
| Skapad | Det datum då rekommendationen skapades. |
| Senast redigerad | Det datum då rekommendationen senast redigerades. |
| Impressions | Antalet gånger som en rekommendationsenhet läses in och återges på en sida. En rekommendationsenhet som ligger under förskjutningen av webbläsarens visningsruta återges på sidan, även om den inte visas av användaren. I det här fallet räknas den återgivna enheten som ett intryck, men en vy räknas bara om kunden rullar enheten så att den syns. |
| vImpressions | (Synliga exponeringar) Antal rekommendationsenheter som registrerar minst en vy. Om rekommendationsenheten till exempel har två rader, var och en med två produkter, och de sista två produkterna inte ses av kunden, men de första två är, kommer aktiviteten fortfarande att räknas som ett intryck. |
| Vyer | Antalet rekommendationsenheter som visas i visningsrutan i kundens webbläsare. Om användaren rullar sidan uppåt eller nedåt flera gånger utlöses händelsen flera gånger, varje gång enheten visas. |
| Klickningar | Summan av antalet gånger en kund klickar på ett objekt i rekommendationsenheten och antalet gånger som användaren klickar på knappen **Lägg till i kundvagnen** i rekommendationsenheten |
| Intäkter | Den intäkt som rekommenderas för det aktuella tidsintervallet. |
| Intäkt | (Livstidsintäkt) Den livstidsintäkt som drivs av en rekommendation. |
| Synlighet | Procentandel av rekommendationsenheter som registreras för vyn. |
| CTR | (Genomklickningsfrekvens) Procentandel av enhetsvisningar för den rekommendation som registrerar ett klick. CTR räknar alla exponeringar även om enheten inte kommer in i kundens vy. Om rekommendationsenheten inte visas är det osannolikt att någon klickar på den. De exponeringar som inte visas räknas emellertid av mot CTR-poängen och minskar den totala procentandelen för CTR. |
| vCTR | (Genomklickningsfrekvens som kan ses) mäter klickningar enbart utifrån visningar (rekommendationer som faktiskt visas i den synliga delen av kundens skärm), vilket ger en mer korrekt bild av kundernas engagemang. |
