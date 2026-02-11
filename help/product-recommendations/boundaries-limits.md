---
title: Gränser och begränsningar
description: Lär dig mer om gränserna och gränserna för  [!DNL Product Recommendations] så att du kan vara säker på att det uppfyller behoven i din verksamhet.
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Gränser och begränsningar

Granska följande gränser och begränsningar för att säkerställa att [!DNL Product Recommendations] uppfyller ditt företags behov. Genom att förstå dessa begränsningar kan du planera implementering, konfigurera filter och undvika vanliga problem.

## Allmänt

- **Produkttyper** - De produkttyper som stöds är bland annat _simple_, _configurable_, _virtual_, _downloadable_ och _presentcard_. _Paket_, _grupperad_ och anpassade produkttyper stöds inte. Om din katalog innehåller ett stort antal produkttyper som inte stöds kan du förvänta dig ett lågt [beredskapsläge](create.md#readiness-indicators). Se [Filtrera efter produkttyp](filters.md#type).
- **SKU:er med blanksteg** - SKU:er som innehåller blanksteg kan minska rekommendationens relevans och bör undvikas när det är möjligt.
- **Kundsida** - Produktrekommendationer stöds inte på kundvagnssidan när din butik är konfigurerad att [visa kundvagnssidan omedelbart efter att en produkt har lagts till i kundvagnen](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration). Se [Skapa rekommendationer](create.md).
- **Underordnade produkter** - Underordnade produkter för en konfigurerbar produkt (synlighet _Inte synlig enskilt_) visas inte i en rekommendationsenhet. Endast den konfigurerbara (överordnade) produkten kan visas. Se [Filtrera produkter](filters.md#product).
- **Inaktiverade eller osynliga produkter** - Produkter som är inaktiverade eller inte synliga individuellt kan aldrig visas i rekommendationer och kan inte väljas i produktfilter.
- **Specialpriser** - [Specialpriser](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) med start- och slutdatum stöds inte i rekommendationsenheter. En produkt med ett specialpris kan visas i rekommendationer, men enheten visar inte specialpriset, startdatumet eller slutdatumet. Kunderna ser det ordinarie priset (eller andra prisuppgifter från din katalog/prisfeed) tills de öppnar produktsidan.

## Rekommendationsenheter

- **Aktiva enheter per sidtyp** - Du kan skapa upp till 50 aktiva rekommendationsenheter för varje sidtyp (Home, Category, Product Detail, Cart, Confirmation). Sidtypen är nedtonad i skapandeflödet när gränsen nås.
- **Produkter per enhet** - Antalet produkter som visas i en rekommendationsenhet kan anges från 5 (standard) till högst 20.
- **Utkastläge** - När du har sparat en rekommendation som utkast kan du inte ändra sidtypen eller rekommendationstypen för den enheten. Andra inställningar kan redigeras före aktiveringen.

## Filter och villkor

- **Dynamiska villkor** - Dynamiska villkor (t.ex.&quot;produkter i samma kategori som den aktuella produkten&quot; eller&quot;relativt prisintervall&quot;) är tillgängliga på alla sidtyper utom hemsidan. De är inte heller tillgängliga på sidor där rekommendationer har placerats med Page Builder. Se [Villkor](filters.md#conditions).

## Förhandsgranskning och icke-produktionsmiljöer

- **Förhandsgranskning** som visades nyligen - Rekommendationstypen _Nyligen visades_ kan inte förhandsgranskas i Admin eftersom data baseras på webbläsarhistorik och inte är tillgängliga i Admin-kontexten. Se [Förhandsgranska rekommendationer](create.md#preview).
- **Rekommendationer från ett annat datautrymme** - När du [hämtar rekommendationer från ett annat SaaS-datautrymme](settings.md) (till exempel produktion) i en icke-produktionsbutik kan du visa rekommendationerna, men inte klicka dig igenom till produktsidor från dem. Detta är utformat för förhandsgranskning och testning.
- **GraphQL och alternativt datautrymme** - När du använder produktrekommendationer via [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) är parametern `alternateEnvironmentId` (används för att hämta rekommendationer från ett annat datautrymme) inte tillgänglig. Använd REST API eller Admin Settings för att växla rekommendationskälla i icke-produktion.

## API och konfiguration

- **API-nycklar (4.x och senare)** - Du måste ange offentliga och privata API-nycklar för både sandbox- och produktionsmiljöer. Om du inte anger båda paren med API-nycklar kan du inte komma åt funktionen Produktrekommendationer i Admin. Datainsamlingen i din butik och befintliga rekommendationer fortsätter att fungera. Se [Installera och konfigurera](install-configure.md).

## Cookie-begränsningar

- När [läget för begränsning av cookies](setting-cookie.md) är aktiverat och kunderna inte har accepterat cookies, kanske vissa rekommendationstyper som förlitar sig på beteendedata inte visas eller kan visa begränsade resultat.
- Rekommendationstyper som inte är beroende av beteendedata (till exempel _De mest visade_, _Visuell likhet_) fortsätter att fungera när cookie-begränsningar är aktiverade.
- När cookie-begränsningar är aktiverade samlar produktrekommendationer inte in eller lagrar beteendedata i cookies eller lokal lagring förrän kunden ger sitt samtycke.

## Page Builder

- **Mätvärden och butiksvyer** - Mätvärden för rekommendationsenheter i Page Builder visas bara i standardbutiksvyn på arbetsytan Produktrekommendationer. Om du vill visa rekommendationsmått för Page Builder i en icke-standardbutiksvy måste du öppna och [redigera](edit.md) rekommendationsenheten för Page Builder i den butiksvyn och spara den. Måtten visas sedan för den butiksvyn. Se [Integrering med Page Builder](page-builder.md).

## B2B

- Produktrekommendationer följer [kategoribehörigheter](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html), [delade kataloger](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) och kundgruppsspecifika priser. Shoppare ser endast rekommendationer för produkter som de har tillgång till enligt sitt segment och sin katalogtilldelning. Se [Onboarding](onboarding.md).

## Data och beredskap

- **Beteendedata** - Många rekommendationstyper kräver tillräckliga beteendedata för butiken (vyer, tillägg till kundvagn, inköp). Nya butiker eller lågtrafikbutiker kan se begränsade eller inga resultat för dessa typer förrän tillräckliga data har samlats in. Övervaka [beredskapsindikatorer](create.md#readiness-indicators) i administratören.
- **Mellanlagring utan produktionsdata** - I en icke-produktionsmiljö utan beteendedata är den enda rekommendationstypen som du kan testa utan att hämta från produktionen _Mer som denna_, som endast använder katalogbaserad likhet. Se [Mellanlagringsmiljö](staging-environment.md).

## Felsökning

Om du vill ha hjälp med katalogsynkronisering, visning av rekommendationer eller andra vanliga problem kan du söka i [Commerce Knowledge Base](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) eller kontakta [support](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
