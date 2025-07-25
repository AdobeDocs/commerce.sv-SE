---
title: Kom igång med  [!DNL Live Search]
description: Lär dig systemkraven och installationsstegen för  [!DNL Live Search] från Adobe Commerce.
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
source-git-commit: d07f36a71247a96bc2dd950867c2862205238d88
workflow-type: tm+mt
source-wordcount: '3139'
ht-degree: 0%

---

# Konfigurera för slutförande med [!DNL Live Search]

Adobe Commerce [!DNL Live Search] och [[!DNL Catalog Service]](../catalog-service/guide-overview.md) samarbetar för att tillhandahålla en prestandabaserad, relevant och intuitiv söklösning så att dina kunder snabbt kan hitta precis vad de behöver. [!DNL Catalog Service] hämtar dina katalogdata för SaaS-tjänster, t.ex. [!DNL Live Search], så att de kan användas.

I den här artikeln finns stegvisa instruktioner för hur du implementerar [!DNL Live Search] med [!DNL Catalog Service].

>[!IMPORTANT]
>
>När det gäller webbplatssökningar har Adobe Commerce fler alternativ. Läs [Gränser och gränser](boundaries-limits.md) innan du implementerar, för att se till att [!DNL Live Search] passar ditt företags behov.

## Målgrupp

Den här artikeln är avsedd för utvecklare eller systemintegratörer i ditt team som ansvarar för att installera och konfigurera din Adobe Commerce-instans.

## Krav

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP version 8.1, 8.2 eller 8.3
- [!DNL Composer]

## Plattformar som stöds

- Adobe Commerce on Cloud (ECE): 2.4.4+
- Adobe Commerce on-prem (EE): 2.4.4+

## Översikt över arbetsflödet

På en hög nivå kräver introduktionen av [!DNL Live Search] att du:

1. [Installera](#1-install-the-live-search-extension) tillägget [!DNL Live Search]
1. [Konfigurera](#2-configure-api-keys) API-nycklarna
1. [Synkronisera](#3-sync-your-catalog-data) katalogdata
1. [Verifiera](#4-verify-that-the-data-was-exported) att katalogdata exporterades
1. [Konfigurera](#5-configure-the-data) data
1. [Testa](#6-test-the-connection) anslutningen
1. [Verifiera](#7-validate-events-are-capturing-data) att händelser hämtar data
1. [Anpassa](#8-customize-for-your-storefront) din butik

## &#x200B;1. Installera tillägget [!DNL Live Search]

[!DNL Live Search] installeras som ett tillägg från [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) till [Composer](https://getcomposer.org/). När du har installerat och konfigurerat [!DNL Live Search] börjar Adobe [!DNL Commerce] dela sök- och katalogdata med SaaS-tjänster. I det här läget kan *Admin*-användare konfigurera, anpassa och hantera regler för sökning, synonymer och försäljning.

>[!NOTE]
>
>Från och med [!DNL Live Search] 3.0.2 paketeras tillägget [!DNL Catalog Service] i med installationen av [!DNL Live Search].

>[!IMPORTANT]
>
>Från och med [!DNL Live Search] 4.0.0 är sökkortet föråldrat. Framöver kommer sökadaptern endast att uppdateras för att åtgärda säkerhetsproblem.

1. Bekräfta att [cron-jobb](https://experienceleague.adobe.com/sv/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) och [indexerare](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/tools/index-management) körs.

   >[!IMPORTANT]
   >
   >På grund av att supporten för Elasticsearch 7 upphör i augusti 2023 rekommenderar vi att alla Adobe Commerce-kunder migrerar till sökmotorn OpenSearch 2.x. Mer information om hur du migrerar sökmotorn under en produktuppgradering finns i [Migrera till OpenSearch](https://experienceleague.adobe.com/sv/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) i _uppgraderingshandboken_.

1. Hämta paketet `live-search` från [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html).

1. Kör följande från kommandoraden:

   ```bash
   composer require magento/live-search
   ```

   Om du lägger till tillägget [!DNL Live Search] i en **ny** Adobe Commerce-installation kör du följande kommando för att inaktivera [!DNL OpenSearch] och relaterade moduler tillfälligt och installerar [!DNL Live Search]. Fortsätt sedan till steg 4.

   ```bash
      bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   Om du lägger till tillägget [!DNL Live Search] i en **befintlig** Adobe Commerce-installation kör du följande för att inaktivera [!DNL Live Search]-modulerna som hanterar sökresultat för butiker. Fortsätt sedan till steg 4:

   ```bash
      bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing 
   ```

   [!DNL Elasticsearch] fortsätter att hantera sökbegäranden från butiken medan tjänsten [!DNL Live Search] synkroniserar katalogdata och indexerar produkter i bakgrunden.

1. Kör följande:

   ```bash
   bin/magento setup:upgrade
   ```

1. Kontrollera att följande [indexerare](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/tools/index-management) är inställda på &quot;Update by Schedule&quot;:

   - Produktfeed
   - Produktvariantfeed
   - Matning för katalogattribut
   - Produktprisfeed
   - Omfattningar för webbplatsdatafeed
   - Omfång Datamatning för kundgrupper
   - Kategoriflöde
   - Kategoribehörighetsfeed

1. Om du installerar [!DNL Live Search] på en ny Commerce-instans är du klar och kan hoppa till [ 2. Konfigurera API-nycklar för avsnittet ](#2-configure-api-keys). Om du installerar Live Search i en befintlig Commerce-instans fortsätter du till nästa steg.

1. Kör följande kommandon för att aktivera tillägget [!DNL Live Search], inaktivera [!DNL OpenSearch] och köra `setup`.

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing 
   ```

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch 
   Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   ```bash
   bin/magento setup:upgrade
   ```

### Installera betaversionen av [!DNL Live Search]

>[!IMPORTANT]
>
>Följande funktion är i betaversionen. Om du vill delta i betaversionen skickar du en e-postförfrågan till [commerce-storefront-services](mailto:commerce-storefront-services@adobe.com).

Den här betaversionen stöder tre nya funktioner i [`productSearch`-frågan ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/):

- **Skiktad sökning** - Sök i ett annat söksammanhang - Med den här funktionen kan du utföra upp till två söklager för dina sökfrågor. Exempel:

   - **Layer 1-sökning** - Sök efter &quot;motor&quot; i &quot;product_attribute_1&quot;.
   - **Layer 2 search** - Search for &quot;part number 123&quot; on &quot;product_attribute_2&quot;. Det här exemplet söker efter &quot;part number 123&quot; i resultatet för &quot;engine&quot;.

  Skiktad sökning är tillgänglig för både `startsWith`-sökindexering och `contains`-sökindexering enligt beskrivningen nedan:

- **börjarMed sökindexering** - Sök med `startsWith`-indexering. Den nya funktionen gör att:

   - Söker efter produkter där attributvärdet börjar med en viss sträng.
   - Om du konfigurerar en&quot;slutar med&quot;-sökning kan kunderna söka efter produkter där attributvärdet slutar med en viss sträng. Om du vill aktivera sökningen &quot;slutar med&quot; måste produktattributet vara inverterat och API-anropet ska också vara en omvänd sträng.

- **innehåller sökindexering** -Sök efter ett attribut som använder innehåller indexering. Den nya funktionen gör att:

   - Söker efter en fråga i en större sträng. Om en kund till exempel söker efter produktnumret &quot;PE-123&quot; i strängen &quot;HAPE-123&quot;.

      - Obs! Den här söktypen skiljer sig från den befintliga [frassökningen](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase), som utför en automatisk sökning. Om produktattributvärdet till exempel är &quot;utomhusbyxor&quot; returnerar en frassökning ett svar för &quot;out pan&quot;, men returnerar inget svar för &quot;or ants&quot;. En sökning innehåller emellertid ett svar på &quot;eller ants&quot;.

De här nya villkoren förbättrar funktionen för filtrering av sökfrågor för att förfina sökresultaten. De här nya villkoren påverkar inte huvudsökfrågan.

Du kan implementera dessa nya villkor på sökresultatsidan. Du kan till exempel lägga till ett nytt avsnitt på sidan där användaren kan förfina sina sökresultat ytterligare. Du kan ge kunderna möjlighet att välja specifika produktattribut, t.ex.&quot;Tillverkare&quot;,&quot;Artikelnummer&quot; och&quot;Beskrivning&quot;. Därifrån söker de i dessa attribut med villkoren `contains` eller `startsWith`. I administratörshandboken finns en lista med sökbara [attribut](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/attributes-input-types).

1. Om du vill installera betaversionen lägger du till följande beroende i ditt projekt:

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. Genomför och skicka ändringarna till dina `composer.json`- och `composer.lock`-filer till ditt molnprojekt. [Läs mer](https://experienceleague.adobe.com/sv/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension).

   Den här betaversionen lägger till **[!UICONTROL Search types]** kryssrutor för **[!UICONTROL Autocomplete]**, **[!UICONTROL Contains]** och **[!UICONTROL Starts with]** i Admin. GraphQL-API:t [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) uppdateras också så att de innehåller dessa nya sökfunktioner.

1. I Admin anger [ett produktattribut](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) som sökbart och anger sökfunktionen för det attributet, till exempel **Innehåller** (standard) eller **Börjar med**. Du kan ange högst sex attribut som ska aktiveras för **Innehåller** och sex attribut som ska aktiveras för **Börjar med**. För betaversioner bör du vara medveten om att Admin inte tillämpar den här begränsningen, men den tillämpas vid API-sökningar.

   ![Ange sökfunktion](./assets/search-filters-admin.png)

1. Läs [utvecklardokumentationen](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) om du vill veta mer om hur du uppdaterar [!DNL Live Search] API-anrop med de nya `contains`- och `startsWith`-sökfunktionerna.

### Fältbeskrivningar

| Fält | Beskrivning |
|--- |--- |
| `Autocomplete` | Aktiveras som standard och kan inte ändras. Med `Autocomplete` kan du använda `contains` i [sökfiltret](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering). Här returnerar sökfrågan i `contains` ett automatiskt typsöksvar. Adobe rekommenderar att du använder den här typen av sökning för beskrivningsfält som vanligtvis innehåller fler än 50 tecken. |
| `Contains` | Aktiverar en sann&quot;text som finns i en sträng&quot;-sökning i stället för en automatisk komplettering-sökning. Använd `contains` i [sökfiltret](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability). Mer information finns i [Begränsningar](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations). |
| `Starts with` | Gör att du kan fråga strängar som börjar med ett visst värde. Använd `startsWith` i [sökfiltret](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability). |

## &#x200B;2. Konfigurera API-nycklar

Adobe Commerce API-nyckeln och den associerade privata nyckeln krävs för att ansluta [!DNL Live Search] till en installation av Adobe Commerce. API-nyckeln genereras och underhålls på kontot för [!DNL Commerce]-licenshavaren, som kan dela den med utvecklaren eller systemintegratorn. Utvecklaren kan sedan skapa och hantera SaaS Data Spaces för licenshavarens räkning. Om du redan har en uppsättning API-nycklar behöver du inte generera om dem.

Lär dig hur du konfigurerar dina API-nycklar i artikeln [Commerce Services Connector](../landing/saas.md) .

## &#x200B;3. Synkronisera katalogdata

[!DNL Live Search] flyttar katalogdata till Adobe SaaS-infrastruktur. Data indexeras och sökresultat levereras från detta index direkt till butiken. Beroende på storlek och komplexitet kan indexeringen ta mellan 30 minuter och några timmar.

Kör följande kommandon i den ordning som du vill börja synkronisera katalogdata till SaaS-tjänster:

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

När du kör dessa kommandon börjar den inledande synkroniseringen av katalogdata till SaaS-tjänster.

>[!WARNING]
>
> När data indexeras och synkroniseras är söknings- och kategoribläddringsåtgärderna inte tillgängliga i butiken. Beroende på storleken på din katalog kan det ta minst en timme från det att `cron` körs att synkronisera dina data till SaaS-tjänster.

### Övervaka synkroniseringsförlopp

Du kan visa data som är synkroniserade och delade med [Dashboard för datahantering](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/data-transfer/data-dashboard). Den här instrumentpanelen ger värdefulla insikter om tillgängligheten av produktdata för butiken, så att den snabbt kan visas för kunderna.

![Instrumentpanel för datahantering](assets/data-management-dashboard.png)

Du kan också köra synkroniseringskommandon och felsöka synkroniseringsprocessen med hjälp av [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) och tilläggsloggarna för dataexport.

#### Framtida produktuppdateringar

Efter den första synkroniseringen kan det ta upp till 15 minuter innan ytterligare produktuppdateringar blir tillgängliga för butikssökning. Mer information finns i [Direktuppspelning av produktuppdateringar](indexing.md) i indexeringsdokumentationen.

## &#x200B;4. Verifiera att data exporterades

Om du vill kontrollera om katalogdata har exporterats från Adobe Commerce och synkroniserats med [!DNL Live Search] har du några alternativ:

- Leta efter poster i följande tabeller:

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >Om du får ett `table does not exist`-fel söker du efter poster i tabellerna `catalog_data_exporter_products` och `catalog_data_exporter_product_attributes`. De här tabellnamnen används i [!DNL Live Search] tidigare versioner än 4.2.1.

- Använd [GraphQL playground](https://experienceleague.adobe.com/sv/docs/commerce/live-search/live-search-admin/graphql) med standardfrågan (se [GraphQL reference](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) för mer information) för att verifiera följande:

   - Det returnerade antalet produkter är nästan vad du förväntar dig för butiksvyn.
   - Ansikten returneras.

Mer hjälp finns i [[!DNL Live Search] katalogen har inte synkroniserats](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) i kunskapsbasen med supportfrågor.

## &#x200B;5. Konfigurera data

Om du konfigurerar dina produktdata på rätt sätt får du bra sökresultat för dina kunder. I det här avsnittet aktiverar du widgetar för produktlistor och tilldelar kategorier.

### Aktivera widgetar för produktlistor

När du installerar [!DNL Live Search] 4.0.0+ aktiveras widgetar för produktlistor som standard. När widgetar är aktiverade används en annan UI-komponent för sökresultatsidan och produktlistsidan för kategoribläddring. Den här gränssnittskomponenten gör direkta anrop till [katalogtjänstens API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/), vilket ger snabbare svarstider.

Om du har en [!DNL Live Search]-version som är äldre än 4.0.0+ måste du aktivera produktlistwidgeten manuellt.

1. Gå till *>* > **[!UICONTROL Stores]** från _[!UICONTROL Settings]_&#x200B;Admin **[!UICONTROL Configuration]**.
1. Välj **[!UICONTROL Live Search]** under **[!UICONTROL Storefront Features]**.
1. Ange **[!UICONTROL Enable Product Listing Widgets]** till `Yes`.

   ![Aktivera widgetar för produktlistor](assets/ls-admin-enable-widget.png)

När du ändrar den här konfigurationen visas meddelandet `Page cache is invalidated`. Du måste tömma Magento-cachen för att spara ändringarna.

1. Gå till sidan [Cachehantering](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/tools/cache-management) genom att göra något av följande:

   - Klicka på länken **[!UICONTROL Cache Management]** i meddelandet ovanför arbetsytan.
   - Gå till _>_ > **[!UICONTROL System]** på sidofältet _[!UICONTROL Tools]_&#x200B;Admin **[!UICONTROL Cache Management]**.

1. Välj **Konfiguration** [!UICONTROL Cache Type] och klicka på **[!UICONTROL Flush Magento Cache]**.

   Ändringar i butiken görs omedelbart efter att du tömt cachen.

### Tilldela kategorier

Produkter som returneras i [!DNL Live Search] måste tilldelas en [kategori](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/categories/categories). I Luma kan till exempel produkter delas in i kategorier som &quot;Män&quot;, &quot;Kvinnor&quot; och &quot;Kugghjul&quot;. Underkategorierna är också inställda för &quot;Tops&quot;, &quot;Bottom&quot; och &quot;Watches&quot;. Dessa kategoritilldelningar förbättrar granulariteten vid filtrering.

## &#x200B;6. Testa anslutningen

Testa att se till att produktdata returneras i följande scenarier med dina katalogdata nu i SaaS:

- Rutan [!UICONTROL Search] returnerar resultat korrekt
- Kategoribläddring returnerar resultat korrekt
- Ansikten finns som filter på sökresultatsidor

Om allt fungerar som det ska installeras, ansluts och är klart att användas. [!DNL Live Search]

Om du stöter på problem i butiken kontrollerar du om det finns API-kommunikationsfel eller fel i filen `var/log/system.log` på tjänstsidan.

Om du vill tillåta [!DNL Live Search] genom en brandvägg lägger du till `commerce.adobe.io` i tillåtelselista.

## &#x200B;7. Verifiera att händelser samlar in data.

Se till att butikshändelserna som distribueras till din plats fungerar. Detta är särskilt viktigt för headless-implementationer.

- Granska de [händelser](events.md) som krävs för [!DNL Live Search].
- Kontrollera att [Live Search-kontrollpanelen](performance.md) visar data från icke-produktionsmiljö(er).
- [Verifiera händelsesamling](../product-recommendations/verify.md). Den här sidan finns i guiden för [!DNL Product Recommendations], men verifieringsstegen gäller även för [!DNL Live Search].

## &#x200B;8. Anpassa för butiken

Du har installerat tillägget [!DNL Live Search], synkroniserat, validerat och konfigurerat dina data. Nästa steg är att se till att widgetarna för [!DNL Live Search] följer din butiks utseende och känsla.

Du kan formatera widgetarna pover och PLP genom att definiera anpassade CSS-regler efter behov. Se [Formatera postarelement](storefront-popover.md#styling-popover-example) och [sidwidget för produktlista](plp-styling.md#styling-example).

Om du vill utöka widgetarnas funktioner är källkoden för varje tillgängligt i en offentlig rapport.
I det här scenariot kan du anpassa JavaScript efter dina egna behov och sedan lägga din anpassade kod på ditt CDN. Det här anpassade skriptet kommunicerar med tjänsten [!DNL Live Search] och returnerar resultatet som vanligt, vilket gör att du kan styra widgetens funktioner.

- [PLP-widgetrepo](https://github.com/adobe/storefront-product-listing-page)
- [Repo för sökfältet](https://github.com/adobe/storefront-search-as-you-type)

## Uppdaterar [!DNL Live Search]

Innan du uppdaterar Live Search kör du följande kommandorad för att kontrollera vilken version av Live Search som är installerad:

```bash
composer show magento/module-live-search | grep version
```

Om du vill uppdatera [!DNL Live Search] kör du följande från kommandoraden:

```bash
composer update magento/live-search --with-dependencies
```

Om du vill uppdatera till en huvudversion, som 3.1.1 till 4.0.0, redigerar du projektets rotfil [!DNL Composer] `.json` enligt följande:

1. Om din installerade `magento/live-search`-version är `3.1.1` eller tidigare och du uppgraderar till version `4.0.0` eller senare, kör du följande kommando före uppgraderingen:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Om du vill ha information om den installerade versionen av `magento/live-search` kör du följande kommando:

   ```bash
   composer show magento/live-search
   ```

1. Öppna rotfilen `composer.json` och sök efter `magento/live-search`.

1. I avsnittet `require` ska du uppdatera versionsnumret på följande sätt:

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. Spara `composer.json`. Kör sedan följande från kommandoraden:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Avinstallerar [!DNL Live Search]

Information om hur du avinstallerar [!DNL Live Search] finns i [Avinstallationsmoduler](https://experienceleague.adobe.com/sv/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] paket

Tillägget [!DNL Live Search] består av följande paket:

| Paket | Beskrivning |
|--- |--- |
| `module-live-search` | Gör att handlare kan konfigurera sina sökinställningar för ansikten, synonymer, frågeregler och så vidare, och ger åtkomst till en skrivskyddad GraphQL-spelningsmiljö för att testa frågor från *Admin*. |
| `module-live-search-adapter` | Slussar sökbegäranden från butiken till tjänsten [!DNL Live Search] och återger resultaten i butiken. <br /> - Kategoribläddring - dirigerar begäranden från butiken [top navigation](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/navigation/navigation-top) till söktjänsten.<br /> - Global sökning - dirigerar begäranden från rutan [snabbsökning](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search) i det övre högra hörnet av butiken till tjänsten [!DNL Live Search]. |
| `module-live-search-storefront-popover` | En sökfunktion som ersätter standardsnabbsökningen och returnerar data och miniatyrbilder av de översta sökresultaten. |

## [!DNL Live Search] beroenden

Metapaketet [!DNL Composer] som installerar tillägget [!DNL Live Search] innehåller följande modulberoenden.

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## Avancerade begrepp

Följande avsnitt innehåller mer avancerade ämnen när du använder [!DNL Live Search] och [!DNL Catalog Service].

### Slutpunkt

[!DNL Live Search] kommunicerar via slutpunkten vid `https://catalog-service.adobe.io/graphql`.

Eftersom [!DNL Live Search] inte har tillgång till den fullständiga produktdatabasen har [!DNL Live Search] GraphQL API:erna för GraphQL och Commerce inte fullständig paritet.

Adobe rekommenderar att du anropar SaaS API:er direkt - särskilt katalogtjänstslutpunkten.

- Öka prestanda och minska belastningen på processorn genom att kringgå Commerce databas-/grafikprocess
- Dra nytta av federationen [!DNL Catalog Service] för att anropa [!DNL Live Search], [!DNL Catalog Service] och [!DNL Product Recommendations] från en enda slutpunkt.

I vissa fall är det kanske bättre att ringa [!DNL Catalog Service] för produktinformation och liknande fall. Mer information finns i [refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/).

Om du har en anpassad headless-implementering kan du ta en titt på referensimplementeringarna för [!DNL Live Search]:

- [PLP-widget](https://github.com/adobe/storefront-product-listing-page)
- [Livesökningsfält](https://github.com/adobe/storefront-search-as-you-type)

Automatisk insamling av användarinteraktionsdata fungerar inte som standard när du inte använder standardkomponenter som sökadaptern, Luma-widgetar eller AEM CIF-widgetar. Adobe Sensei använder dessa insamlade data för intelligent varuexponering och prestandaspårning. För att lösa det här problemet måste ni utveckla en anpassad lösning för att implementera datainsamlingen på ett headless sätt.

Den senaste versionen av [!DNL Live Search] använder redan [!DNL Catalog Service].

### Språkstöd

[!DNL Live Search] widgetar har stöd för följande språk:

|  |  |  |  |
|--- |--- |--- |--- |
| Språk | Län | Språkkod | Magento Locale |
| Bulgariska | Bulgarien | bg_BG | bg_BG |
| Katalanska | Spanien | ca_ES | ca_ES |
| Tjeckiska | Tjeckien | cs_CZ | cs_CZ |
| Danska | Danmark | da_DK | da_DK |
| Tyska | Tyskland | de_DE | de_DE |
| Grekiska | Grekland | el_GR | el_GR |
| Engelska | Förenade kungariket | en_GB | en_GB |
| Engelska | Amerikas förenta stater | sv_SE | sv_SE |
| Spanska | Spanien | es_ES | es_ES |
| Estniska | Estland | et_EE | et_EE |
| Baskiska | Spanien | eu_ES | eu_ES |
| Persiska | Iran | fa_IR | fa_IR |
| Finska | Finland | fi_FI | fi_FI |
| Franska | Frankrike | fr_FR | fr_FR |
| Galiciska | Spanien | gl_ES | gl_ES |
| Hindi | Indien | hi_IN | hi_IN |
| Ungerska | Ungern | hu_HU | hu_HU |
| Indonesiska | Indonesien | id_ID | id_ID |
| Italienska | Italien | it_IT | it_IT |
| Koreanska | Sydkorea | ko_KR | ko_KR |
| Litauiska | Litauen | lt_LT | lt_LT |
| Lettiska | Lettland | lv_LV | lv_LV |
| Norska | Norge bokmål | nb_NO | nb_NO |
| Nederländska | Nederländerna | nl_NL | nl_NL |
| Polska | Polen | pl_PL | pl_PL |
| Portugisiska | Brasilien | pt_BR | pt_BR |
| Portugisiska | Portugal | pt_PT | pt_PT |
| Rumänska | Rumänien | ro_RO | ro_RO |
| Ryska | Ryssland | ru_RU | ru_RU |
| Svenska | Sverige | sv_SE | sv_SE |
| Thailändska | Thailand | th_TH | th_TH |
| Turkiska | Turkiet | tr_TR | tr_TR |
| Kinesiska | Kina | zh_CN | zh_Hans_CN |
| Kinesiska | Taiwan | zh_TW | zh_Hant_TW |

Om widgeten upptäcker att språkinställningen för Commerce Admin matchar ett språk som stöds används det som standard. I annat fall är widgeten standard engelska. I Admin konfigureras språkinställningen genom att gå till _[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options].

Administratörer kan också ange språket för [sökindexet](settings.md#language) för att få bättre sökresultat.

### Databas för Widget-kod

Koden för sidwidgeten för produktlistor och widgeten för Live-sökfält kan hämtas från GitHub.

Utvecklare som har tillgång till koden kan helt anpassa hur den fungerar och ser ut. De har koden på sina egna servrar men använder fortfarande tjänsten [!DNL Live Search].

- [PLP-widget](https://github.com/adobe/storefront-product-listing-page)
- [Sökfältet](https://github.com/adobe/storefront-search-as-you-type)

### Dataexporttillägg

När Live Search är aktiverat synkroniserar dataexporttillägget Commerce-data mellan Commerce-programmet och Live Search. Detta säkerställer att de senaste Commerce-uppgifterna finns tillgängliga i butiken. I Admin kan du kontrollera synkroniseringsstatus med hjälp av kontrollpanelen för datahantering. Du kan hantera och felsöka dataexportprocessen med Commerce CLI och loggar. Mer information finns i [Dataexportguiden](../data-export/overview.md).

### Inventory management

[!DNL Live Search] har stöd för [Inventory management](https://experienceleague.adobe.com/sv/docs/commerce-admin/inventory/introduction)-funktioner i Commerce (tidigare Multi-Source Inventory, eller MSI). Om du vill aktivera fullständigt stöd måste du [uppdatera](install.md#updating-live-search) beroendemodulen `commerce-data-export` till version 102.2.0+.

[!DNL Live Search] returnerar ett booleskt meddelande som anger om en produkt är tillgänglig i Inventory management, men inte innehåller information om vilken källa som har aktien.

### Prisindexerare

Live Search-kunder kan använda prisindexeraren [SaaS](../price-index/price-indexing.md) som ger snabbare prisändringar och synkroniseringstid.

### Prisstöd

Live Search-widgetar har stöd för de flesta, men inte alla, pristyper som stöds av Adobe Commerce.

För närvarande stöds baspriser. Avancerade priser som inte stöds är:

- Kostnad
- Lägsta kampanjpris

Titta på [API-nät](../catalog-service/mesh.md) för mer komplexa prisberäkningar.

Prisformatet stöder de nationella konfigurationsinställningarna i Commerce-instansen: *Lagrar* > Inställningar > *Konfiguration* > Allmänt > *Allmänt* > Lokala alternativ > Språk.

### Headless storefront support

Om du vill kan du behöva installera modulen `module-data-services-graphql` som utökar programmets befintliga GraphQL-täckning så att den innehåller fält som krävs för beteendedatainsamling i butiken.

```bash
composer require magento/module-data-services-graphql
```

Den här modulen lägger till ytterligare kontexter i GraphQL-frågor:

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### Stöd för B2B

[!DNL Live Search] har stöd för [B2B-funktioner](https://experienceleague.adobe.com/sv/docs/commerce-admin/b2b/guide-overview) med ytterligare [begränsningar](boundaries-limits.md#b2b-and-category-permissions).

### PWA support

[!DNL Live Search] fungerar med PWA Studio, men användare kan se små skillnader jämfört med andra Commerce-implementeringar. Grundläggande funktioner som sök- och produktlistsidor fungerar i Venia, men vissa permutationer av Graphql kanske inte fungerar som de ska. Det kan också finnas prestandaskillnader.

- Den aktuella PWA-implementeringen av [!DNL Live Search] kräver mer bearbetningstid för att returnera sökresultat än [!DNL Live Search] med den inbyggda Commerce-butiken.
- [!DNL Live Search] i PWA stöder inte [händelsehantering](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Därför fungerar inte sökrapporter och intelligent varuexponering i PWA butiker.
- När du använder [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) stöder GraphQL inte filtrering direkt på `description`, `name`, `short_description`, men dessa fält kan returneras med ett mer allmänt filter.

Om du vill använda [!DNL Live Search] med PWA Studio måste integratörer också:

1. Installera [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Ange `environmentId` i objektet `storeDetails`.

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookies

[!DNL Live Search] samlar in användarinteraktionsdata som en del av basfunktionen och cookies används för att lagra dessa data. När användaren samlar in användarinformation måste han eller hon godkänna att lagra cookies. [!DNL Live Search] och [!DNL Product Recommendations] delar dataströmmen och därmed samma cookie-mekanism. Läs mer om det i [Hantera cookie-begränsningar](https://experienceleague.adobe.com/sv/docs/commerce/product-recommendations/developer/setting-cookie).
