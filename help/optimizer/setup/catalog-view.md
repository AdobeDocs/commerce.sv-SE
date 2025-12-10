---
title: Katalogvy
description: Lär dig vilka katalogvyer som är och hur du skapar dem för att ordna din produktkatalog efter affärsstruktur, principer och priser.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 0%

---


# Katalogvyer för marknadsföringstjänster

Katalogvyer utgör grunden för Adobe Commerce Optimizer Merchandising Services, vilket gör att du kan ordna din produktkatalog efter affärsstruktur, policyer och priser. Denna flexibla datamodell stöder scenarier med flera varumärken, affärsenheter och flerspråkiga lösningar samtidigt som effektiviteten bibehålls.

## Vad är katalogvyer?

Katalogvyer definierar hur produktkatalogen ordnas och visas. De fungerar som filter som bestämmer:

- **Vilka produkter som visas** baserat på affärsstruktur (varumärken, regioner, återförsäljare)
- **Vilka priser som visas** via länkade prisböcker
- **Hur produkter filtreras** med hjälp av principer (attribut som märke, modell, kategori)
- **Vilken katalogkälla används** baserat på attribut som språkområde

Se katalogvyer som olika linser som kunderna kan använda för att se katalogen. Exempel:

- En katalogvy över återförsäljare kan visa endast produkter som är tillgängliga för den återförsäljaren
- En regional katalogvy kan visa produkter och priser som är specifika för ett geografiskt område
- En varumärkeskatalogvy kan visa endast produkter från ett visst varumärke

## Skapa en katalogvy

I det här avsnittet skapar du en katalogvy, väljer en [policy](policies.md) och en [prisbok](pricebooks.md).

Innan du skapar en katalogvy bör du kontrollera att:

- [Skapade profiler](policies.md) för att definiera produktfilter

- [Inlästa prisböcker](pricebooks.md) för priser

1. Gå till _Store setup_ på den vänstra menyn och klicka på **[!UICONTROL Catalog views]**.

1. Klicka på **[!UICONTROL Create catalog view]**. &#x200B;

1. Konfigurera information om katalogvyn:

   - **Namn** - Ange namnet på katalogvyn, till exempel `Celport`. &#x200B;
   - **Katalogkällor** - Välj katalogkälla (nationella inställningar), till exempel `en-US`.
   - **Profiler** - Använd listrutan för att välja relevanta profiler. Exempel: &quot;Varumärke&quot;, &quot;Modell&quot;. &#x200B;Kontrollera att du redan [har skapat en princip](policies.md).

1. Välj den prisbok som du vill länka till katalogvyn.

   - **Använd alla tillgängliga prisböcker**-Det här alternativet hämtar prisdata från alla tillgängliga prisböcker.
   - **Tillåt endast valda prisböcker**-Det här alternativet visar dialogrutan **Lägg till tillåtna prisböcker** där du kan välja vilken prisbok som ska användas för katalogvyn.
   - **Inaktivera pris**-Det här alternativet är inte tillgängligt just nu.

1. Klicka på **[!UICONTROL Add]** om du vill skapa katalogvyn med de länkade prisböckerna och profilerna.

Sidan Katalog visar uppdateringar för att visa den nya katalogvyn. &#x200B;

När du har utfört de här stegen är katalogvyn nu konfigurerad för att visa produkter och priser baserat på de valda källorna och profilerna.

## Hantera katalogvy

Följ dessa anvisningar för att uppdatera eller visa egenskaperna för befintliga katalogvyer.

### Redigera katalogvy

1. På arbetsytan för *katalogvyer* letar du reda på katalogvyn i det rutnät som du vill redigera och klickar på **..** för att öppna åtgärdsmenyn.
1. Klicka på **Redigera** för att öppna katalogvyredigeraren.
1. Uppdatera namn, katalogkällor, principer och prisboksinformation efter behov.
1. Spara ändringarna.

### Ta bort katalogvy

1. I arbetsytan för *katalogvyer* letar du reda på katalogvyn i det rutnät som du vill redigera och klickar på **..** för att öppna åtgärdsmenyn.
1. Klicka på **Ta bort**.

   När bekräftelsedialogrutan visas klickar du på **[!UICONTROL Delete]**.

### Visa detaljer

Med det här alternativet kan du snabbt se alla katalogens visningsparametrar, medan du arbetar i *katalogvytabellen*.

På arbetsytan för *katalogvyer* letar du reda på katalogvyn i det rutnät som du vill redigera och klickar på ![informationsikonen](../assets/info-icon.png).

![Information om katalogvyn](../assets/catalog-view-details.png)

Härifrån kan du se konfigurationsinformation för katalogvyn, som:

- Visa ID
- Namn
- Katalogkällor
- Profiler
- Skapad den
- Ändrade data

En del av dessa konfigurationsinställningar behövs när du konfigurerar butiken eller använder API:t för datainhämtning.

## Arkitektur - översikt

Katalogvyer är en del av Merchandising Services-ramverket som ersätter webbplatsen, butiken och butiksramverket som används i Adobe Commerce Foundation med en mer flexibel modell:

![[!DNL Merchandising Services]-arkitektur](../assets/merchandising-svcs-architecture.png)

### Så här fungerar det

**1. Inmatning av data**
Katalogdata från PIM, ERP och andra system hämtas in i ramverket för marknadsföringstjänster. Varje SKU innehåller språkinformation och produktattribut som mappas till katalogvyer, policyer och språkområden. Mer information om dataöverföring finns i [utvecklardokumentationen](https://developer.adobe.com/commerce/services/optimizer/).

**2. Enhetlig baskatalog**
Inkapslade data skapar en enhetlig baskatalog i dataredjan för katalogtjänsten. Med denna enda källa slipper ni datatypsbyte mellan olika affärsenheter.

**3. Katalogvyer**
Flera katalogvyer representerar olika affärsenheter (t.ex.&quot;Texas Retail&quot;,&quot;Texas Retail Seasonal&quot;). Språk, profiler och prisböcker kan delas mellan olika katalogvyer för ökad flexibilitet.

**4. Flerkanalsleverans**
Filtrerade katalogdata levereras till olika destinationer som Edge Delivery Services butiker, marknadsplatser, annonsplattformar och anpassade mikrobutiker. Mer information om leverans av katalogdata finns i [utvecklardokumentationen](https://developer.adobe.com/commerce/services/optimizer/).

### Viktiga komponenter

| Komponent | Syfte | Exempel |
|---|---|---|
| **Katalogvy** | Affärsenhet eller distributionskanal | Återförsäljarnätverk, regional butik |
| **Princip** | Produktfilter baserat på attribut | Varumärke, modell, kategori |
| **Språk** | Språk-/regioninställning | sv-SE, fr-CA, es-MX |
| **Prisbok** | Prisstruktur | Detaljhandel, grossist, anställd |

### Dataflöde

1. **Ingest** - Produktdata från PIM/ERP-system
2. **Process** - Använd katalogvyer, principer och priser
3. **Leverera** - Servera filtrerad katalog till butiker, marknadsplatser osv.

## Viktiga funktioner

| Funktion | Fördelar |
|---|---|
| **En baskatalog** | Eliminera datadubbletter mellan olika affärsenheter |
| **Flexibla priser** | Flera prisböcker per SKU för olika kundsegment |
| **Skalbar** | Hantera över 200 miljoner SKU:er effektivt |
| **Flera kanaler** | Hantera kataloger för butiker, marknadsplatser och annonsplattformar |
| **Realtidsuppdateringar** | Uppdatera snabbt katalogdata för kampanjer och kampanjer |

## Användningsexempel

### Konglomerat med flera varumärken

**Problem**: Hantera flera varumärken, länder och språk<br>
**Lösning**: En katalog med katalogvyer för varje kombination av märke/region

### Återförsäljare av reservdelar

**Utmaning**: 3 000 återförsäljare med samma produkter men olika priser<br>
**Lösning**: En katalog med katalogvisningar och prislistor som är specifika för återförsäljaren

### Detaljhandlare på flera platser

**Problem**: Olika priser och lager per plats<br>
**Lösning**: Platsbaserade katalogvyer med regionspecifika profiler

>[!INFO]
>
>Mer information om inmatning och leverans av katalogdata finns i [utvecklardokumentationen](https://developer.adobe.com/commerce/services/optimizer/).
