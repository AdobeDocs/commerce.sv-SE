---
title: Rekommendationsprestanda
description: Sidan Rekommendationer ger dig insikt i hur bra dina produktrekommendationer fungerar.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och [!DNL Adobe Commerce Optimizer] projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 1b77e2ea-412b-4c78-9d38-390bd8fda87e
source-git-commit: 9cb231055df45bbfcff3303c6e1c257c883cb852
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# Rekommendationsprestanda

På sidan Recommendations Performance (Rekommendationer prestanda) visas en lista med konfigurerade rekommendationer tillsammans med viktiga mätvärden som hjälper dig att utvärdera hur effektiva de är. Du kan konfigurera vyn så att den visar mått för den senaste dagen, veckan eller månaden. Dessa insikter visar hur ofta varje rekommendationsenhet visas eller klickas, vilket hjälper dig att utvärdera prestanda och identifiera möjligheter till optimering.

>[!INFO]
>
>En rekommendationsenhet är en widget som innehåller den rekommenderade produkten _items_.

![Rekommendationsprestanda](../assets/rec-performance.png){zoomable="yes"}

## Visa en rapport

1. Välj **katalogvyn**, t.ex. *Alla vyer* som dina rekommendationer gäller för.

   Läs mer om [katalogvyer](#select-catalog-view) i rekommendationerna.

1. Klicka på **[!UICONTROL Date Range]** och välj ett av följande intervall:

   ![Rekommendationer, datumintervall](../assets/rec-perf-date-range.png)

   Rekommendationstabellen uppdateras och visar mått för det datumintervallet och katalogvyn.

## Anpassa tabell

1. Klicka på ikonen ![Kolumnväljare](../assets/icon-show-hide-columns.png) i det övre vänstra hörnet för att anpassa tabellen.

   De synliga kolumnerna är markerade.

1. Gör något av följande på menyn:

   - Om du vill visa en dold kolumn klickar du på ett kolumnnamn utan bockmarkering.
   - Om du vill dölja en synlig kolumn klickar du på ett kolumnnamn med en bock.

   Tabellen uppdateras så att den endast innehåller de markerade kolumnerna.

## Visa detaljer

1. Klicka på ikonen (![Mer väljare](../assets/btn-more.png)) bredvid den rekommendation du vill granska i tabellen.

1. Om du vill ändra rekommendationens status klickar du på **Aktivera** eller **Inaktivera**.

## Skapa eller hantera rekommendationer

Lär dig hur du kan [skapa en ny eller hantera en befintlig](../merchandising/recommendations/create.md)-rekommendation.

## Workspace

| Kontroll | Beskrivning |
|---|---|
| ![Datumintervall](../assets/rec-perf-date-range.png) | Anger det tidsintervall som används för måttberäkningar. |
| ![Kolumnväljare](../assets/icon-show-hide-columns.png) | Anger vilka kolumner som visas i tabellen Rekommendationer. |
| Skapa rekommendation | Öppnar sidan [Skapa ny rekommendation](../merchandising/recommendations/create.md). |
| [Katalogvy](#select-catalog-view) | Markera katalogvyn om du vill filtrera tabellen så att endast rekommendationer som gäller för den valda katalogvyn visas. Den här markeringen används också som katalogvy när du [skapar](../merchandising/recommendations/create.md) en ny rekommendation. Alternativen är *Alla vyer* eller en specifik [katalogvy](../setup/catalog-view.md). |

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

## Välj katalogvy

>[!IMPORTANT]
>
>Den här funktionen är för närvarande i betaversion.

**[!UICONTROL Catalog view]**-väljaren på sidan **Rekommendationer** gör två saker:

1. **Filtrerar tabellen** - Visar endast rekommendationer (och deras mått) som gäller för den valda katalogvyn.
1. **Anger omfånget för nya rekommendationer** - När du [skapar](../merchandising/recommendations/create.md) en rekommendation används den valda katalogvyn som enhetens omfång. Alternativen är *Alla vyer* eller en specifik [katalogvy](../setup/catalog-view.md).

   - **Alla vyer** - Rekommendationen gäller för alla katalogvyer (produkttillgängligheten filtreras fortfarande per vy).
   - **Katalogvy** - Rekommendationen gäller bara för den valda katalogvyn (till exempel en butiks-, språk- eller varumärkeskommentar).

Genom att ange en katalogvy för varje rekommendation kan du:

- Konfigurera rekommendationer för alla katalogvyer (globala) eller för en katalogvy.
- Förhandsgranska och filtrera produkter efter katalog på rekommendationssidan [skapa](../merchandising/recommendations/create.md).
- Visa endast produkter som är tillgängliga för varje butik.
- Visa mått och butiksbeteenden per katalogvy.

### Så här filtrerar katalogvyn produkter

Produkttillgängligheten upprätthålls per katalogvy även för rekommendationsenheter under valet **Alla vyer**. Detta fungerar utöver alla [inkluderings- eller exkluderingsfilter](../merchandising/recommendations/filters.md) som du anger i rekommendationsenheten.

**Exempel: Rekommendation med inkluderingsfilter under markeringen Alla vyer**

- Rekommendationen **Alla vyer** innehåller SKU:er: SKU_ABC, SKU_CDE, SKU_XYZ.
- **Katalogvy: Kingsbluff** kan inte sälja SKU_ABC eller SKU_CDE. **Visas:** SKU_XYZ plus andra SKU:er som är giltiga för Kingsbluff.
- **Katalogvy: Arkbridge** kan inte sälja någon av de inkluderade SKU:erna. **Visas:** Endast SKU:er tillåts av Arkbridge. Om det inte finns någon tillgänglig visas inte rekommendationsenheten på den butiken.
