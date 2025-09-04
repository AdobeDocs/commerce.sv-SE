---
title: Versionsinformation för [!DNL SaaS Data Export Extension]
description: Den senaste versionsinformationen för  [!DNL Data Export Extension]  för Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: 6abfeca68ab67fb11493f78440e09408479e1535
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# Versionsinformation om [!DNL SaaS Data Export] tillägg

De här versionsinformationen beskriver de senaste versionerna av tillägget [!DNL SaaS data export]. Support ges för den aktuella större versionen. Versionsinformation för äldre versioner finns som referens.

Bland uppdateringarna finns:

![Nya](../assets/new.svg) nya funktioner
![Korrigera ](../assets/fix.svg) Korrigeringar och förbättringar
![Fel](../assets/bug.svg) Kända fel


>[!NOTE]
>
>SaaS-tillägget för dataexport är en samling moduler som installeras automatiskt med Live Search, Produktrekommendationer och katalogtjänsten. Du kan kontrollera vilken version som är installerad på datorn med Composer. I vissa fall kanske du vill uppgradera dataexporttillägget på datorn för att kunna hämta korrigeringar eller nya funktioner utan att uppdatera Commerce tjänstversion.

## Aktuell huvudversion

## 103.4.11 Utgåva

![Nytt](../assets/new.svg) [!BADGE Endast PaaS]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."}
Ytterligare stöd för ytterligare produktattribut som inkluderar momsklass, attributuppsättning och lagerdata från Commerce produktkonfigurationer i produktflödet. Kunder som vill inkludera dessa attribut i produktexportflöden måste lägga till modulen Extra produktattribut i sina Adobe Commerce-projekt. Se [Lägg till momsklass, attributuppsättning och lagerattribut](add-tax-attribute-set-inventory-attributes.md).<!--MDEE-1135-->
![ Åtgärda ](../assets/fix.svg) Ett problem som orsakade felaktig synkronisering av borttagna produktuppdateringar har åtgärdats om ett fel uppstod under ett fullständigt produktindex. Nu synkroniseras alla produktborttagningar korrekt även om ett fel inträffar under indexeringsprocessen. <!--MDEE-1144-->

## 103.4.10 Utgåva

![Korrigera](../assets/fix.svg) Ett problem där fel typ (`text` i stället för `OBJECT`) returnerades för vissa dynamiskt skapade attribut har korrigerats. Nu returneras alltid rätt typinformation, vilket eliminerar behovet av manuell omsynkronisering eller tillfälliga lösningar.<!--MDEE-1131-->
![ Korrigera ](../assets/fix.svg) Ett problem där insamling av produktdata under partiell synkronisering kunde misslyckas på grund av fel i LowStock-lagerprovidern har åtgärdats. Med den här korrigeringen exporteras produktdata på ett tillförlitligt sätt och inga produkt-ID:n hoppas över på grund av fel relaterade till LowStock.<!--MDEE-1132-->

## 103.4.9 Utgåva

![Korrigera](../assets/fix.svg) Ett problem där produktprisfeeds inte genererades om när en produkt togs bort eller när produktens SKU ändrades har korrigerats.<!--MDEE-1125-->
![ Korrigera ](../assets/fix.svg) Förbättrad bearbetning av produktuppdateringar för att säkerställa att ändringarna återspeglas korrekt när du uppdaterar en nyskapad produkt med samma SKU som en tidigare borttagen produkt. Produktsynkroniseringen använder nu uppdaterade produkt-ID:n korrekt, vilket ger korrekt och tillförlitlig dataexport.<!--MDEE-1126-->
![ Åtgärda ](../assets/fix.svg) Ett problem där katalogtjänsten kunde returnera inaktuella variantdata för konfigurerbara produkter genom att säkerställa att produktuppdateringshändelser publiceras efter attributborttagningar har åtgärdats.<!--MDEE-1127-->

## 103.4.8 Utgåva

![Ny](../assets/new.svg) har lagt till information om nivåpris i prisflödet. <!--MDEE-1070-->
![ Korrigera ](../assets/fix.svg) Tillägget för dataexport exporterar nu korrekt webbplatsomfattande paketpriser, vilket säkerställer att butikspriserna återspeglar korrekta värden baserade på konfigurationen &quot;Katalogens prisomfång&quot;.<!--MDEE-1115-->
![ Korrigera ](../assets/fix.svg) Tidigare synkroniserades produkter med felaktig `lowStock=true` status när Inventory management (Inventory management med flera källor) med tröskelkonfiguration användes. Det här problemet har åtgärdats för att säkerställa korrekt rapportering av låga lagernivåer.<!--MDEE-1113-->

## 103.4.7 Utgåva

![Korrigera](../assets/fix.svg) Tar bort föråldrade tabeller som lagrade kategoribehörigheter för produkter. <!--MDEE-1065-->

## 103.4.6 Utgåva

![Korrigera](../assets/fix.svg) Exportera Adobe Commerce nedladdningsbara produktdata med attributet `ac_downloadable` för användning med Adobe Commerce Optimizer. <!--MDEE-1043-->
![ Åtgärda ](../assets/fix.svg) Allvarliga installationsfel för Adobe Commerce version 2.4.4. <!--MDEE-1074-->

## 103.4.5 Utgåva

![Ny](../assets/new.svg) SaaS-dataexport har nu stöd för produkttypen Adobe Commerce `giftcard`. I dataflödet exporteras presentkortsprodukter som enkla produkter med produktattributtypen `ac_giftcard`. <!--MDEE-1042-->
![ Korrigera ](../assets/fix.svg) Förbättrad felrapportering vid dataexport. Loggarna innehåller nu mer detaljerade felmeddelanden, inklusive den ursprungliga tekniska informationen som gör det enklare att felsöka och spåra fel. <!--MDEE-1064-->

## 103.4.4 Utgåva

![Nytt](../assets/new.svg) har lagt till ett varningsmeddelande som visas när argumentet `cleanup-feed` läggs till i CLI-kommandot `saas:resync`. Alternativet `--cleanup-feed` bör användas med försiktighet och endast i specifika scenarier som efter miljörensning eller med alternativet `--dry-run`. Om du använder den i andra fall kan det leda till dataförlust och synkroniseringsproblem. <!--MDEE-1047-->
![ Korrigera ](../assets/fix.svg) `x-request-id` har lagts till från serversvaret för förbättrad spårbarhet. <!--MDEE-1041-->
![ Korrigera ](../assets/fix.svg) Ett problem där synkroniseringsstatusen inte sparades för hela feed-batchen har korrigerats, vilket ledde till onödig omsynkronisering. <!--MDEE-1049-->
![ Korrigera ](../assets/fix.svg) Ett fel har korrigerats där alla feeds i feed-batchen hoppades över under synkroniseringen om en feed innehöll ett fel. <!--MDEE-976-->
![ Korrigera ](../assets/fix.svg) Stöd för dimensioner har lagts till i kategoribehörighetsindexeraren. <!--MDEE-654-->

## 103.4.3 Utgåva

![Korrigera](../assets/fix.svg) Ett problem där produkter hoppades över under dataexportprocessen på grund av saknade EAV-attribut har åtgärdats. <!--MDEE-970-->

## 103.4.2 Utgåva

![Korrigera](../assets/fix.svg) Lagt till möjligheten att samla in enhetsnyttolaster i `saas-export.log` när du kör testomsynkroniseringen med kommandot `saas:resync --dry-run` med miljövariabeln `EXPORTER_EXTENDED_LOG=1` . <!--MDEE-1023-->

## 103.4.1 Utgåva

![Korrigera](../assets/fix.svg) har lagt till ett prefix i QueryXml-cachenycklar för att förhindra namnkonflikter med andra moduler. <!--MDEE-1019-->

## 103.4.0-utgåvan

![Korrigera](../assets/fix.svg) Produkten åsidosätter feed och skickar inte längre behörigheter om produkten inte har tilldelats en kategori.<!--MDEE-449-->

## 103.3.21 Utgåva

![Korrigera](../assets/new.svg) Funktioner som delvis synkroniserar `products`, `productOverrides` och `productAttributes` feeds baserat på en angiven lista med produkt-SKU:er. Använd den nya funktionen genom att lägga till alternativet `--by-ids` i det omsynkroniserade CLI-kommandot: <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![Åtgärda](../assets/fix.svg) Minskade potentiella kompatibilitetsproblem med PHP 8.4 genom borttagning av inaktuella funktioner. <!--MDEE-1002-->

## 103.3.20 Utgåva

![Åtgärda](../assets/fix.svg) ej spårbara `BulkException` fel i `cron.log` genom att förbättra meddelanden för fel relaterade till kronijobbsfel för export av katalogdata.<!--MDEE-966-->
![ Korrigera ](../assets/fix.svg) Förbättrade prestanda för produktsynkroniseringsprocessen på instanser med ett stort antal butiksvyer. <!--MDEE-974-->

## 103.3.19 Utgåva

![Korrigera](../assets/fix.svg) Uppdaterade tillägget för dataexport för att förbättra utbyggbarheten för feeds. <!--MDEE-936-->
![ Korrigera ](../assets/fix.svg) Dataexportprocessorn verifierar nu indexerarens status före en fullständig omsynkronisering för att undvika oavsiktlig dataförlust i flödestabellen.

## 103.3.18 Utgåva

![Korrigera](../assets/fix.svg) Mellanlagringsuppdateringar för produkt- och kategorientiteter aktiveras nu korrekt vid dataexportuppdateringar.<!--MDEE-963-->

## 103.3.17 Utgåva

![Korrigera](../assets/fix.svg) Kompatibilitet för PHP 8.4 har lagts till. <!--MDEE-941-->

## 103.3.16 Utgåva

![Åtgärda](../assets/fix.svg) Alternativvärden kan vara tomma för konfigurerbara produkter för flera butiksvyer. <!--MDEE-926-->

## 103.3.15 Utgåva

![Korrigera](../assets/fix.svg) Säkerställde stabil funktion för integreringstester på äldre konfigurationer. <!--MDEE-869-->
![ Korrigera ](../assets/fix.svg) Sluta sprida alternativ för onödiga attribut. <!--MDEE-882-->
![ Korrigera ](../assets/fix.svg) Felmeddelandet som skickades till dataexportloggen när serialisering av data misslyckades har åtgärdats. <!--MDEE-913-->
![ Korrigera ](../assets/fix.svg) Förbättrade tillförlitligheten för enkla produktuppdateringar med extra testtäckning. <!--MDEE-886-->

## 103.3.14 Utgåva

![Korrigera](../assets/fix.svg) Exportindexeraren behåller nu rätt status för beroende indexerare. Tidigare ogiltigförklarades dessa index felaktigt och ytterligare kontroller och validering krävdes som bromsade indexeringsprestanda. <!--MDEE-866-->

## 103.3.13 Utgåva

![Korrigera](../assets/fix.svg) Förbättrade prestanda för datasynkroniseringsprocessen genom att lägga till ett lokalt cacheminne för attributalternativdata.<!--MDEE-864-->

## 103.3.12 Utgåva

![Korrigering](../assets/fix.svg) Ett problem som ökade synkroniseringstiden för enkla och virtuella produkter har åtgärdats. <!--MDEE-861-->

## 103.3.11 Utgåva

![Korrigera](../assets/fix.svg) Dataexporttjänsten skickar nu specialprisdata för paketprodukter som en procentandel, vilket korrigerar en tidigare utgåva där den skickades som ett slutligt pris. <!--MDEE-854-->
![ Korrigera ](../assets/fix.svg) Monolog-implementeringen har uppdaterats för kompatibilitet med Monolog 3. <!--MDEE-858-->

## 103.3.10 Utgåva

![Korrigera](../assets/fix.svg) Flera lagringsgranskningsfiltreringar har korrigerats för den anpassade produktalternativfeeden. <!--MDEE-842-->
![ Korrigera ](../assets/fix.svg) Ogiltiga feeds skickas inte om förrän flödets hash-värde har ändrats.<!--MDEE-848-->

## 103.3.9 Utgåva

![Korrigera](../assets/fix.svg) När en entitet tas bort sprids nu flaggan `deleted` för omfångstjänstfeeds för webbplatsen (`scopesWebsite`) och kundgruppen (`scopesCustomerGroup`).<!--MDEE-839-->

## 103.3.8 Release

![Åtgärda](../assets/fix.svg) Inaktiverade konfigurationsalternativ exporteras inte längre som aktiva alternativ.<!--MDEE-812-->
![ Korrigera ](../assets/fix.svg) Alternativ och värden uppdateras nu för en konfigurerbar produkt när ändringar görs i en underordnad produkt. <!--MDEE-835-->
![ Nytt ](../assets/new.svg) Förbättrade möjligheten att inkludera ytterligare systemattributdata i produktattributsflödet.

## 103.3.7 Utgåva

![Korrigera](../assets/fix.svg) Onödiga beroenden har tagits bort från modulen InventoryDataExporter.
![Åtgärda](../assets/fix.svg) Ändrade obligatoriska versioner för lagermoduler som ingår i modulen CatalogInventoryDataExporter så att de stöder Adobe Commerce version 2.4.4.

## 103.3.6 Utgåva

![Korrigera](../assets/fix.svg) Dödlägen som inträffade under feed-omindexering i flertrådsläge har korrigerats. Frågorna delas nu upp i åtgärderna Infoga och Uppdatera.
![Korrigera](../assets/fix.svg) Optimerade prisfrågan för stora kataloger med många webbplatser.
![Ny](../assets/new.svg) Återförsökslogik har lagts till för att köra misslyckade transaktioner på nytt när tidsgränsen nås.

## 103.3.5 Utgåva

![Korrigera](../assets/fix.svg) Ange beroende för den senaste kompatibla dataexportversionen för SaaS gemensamma modul.

![Åtgärda](../assets/fix.svg) `ScopeConfig`-instansen med `ServiceConfigInterface` om du vill ha stöd för olika tjänstkonfigurationer.

## 103.3.4 Utgåva

![Åtgärda](../assets/fix.svg) Stöd för loggning av dataöverföringsgranskning har lagts till genom att en mekanism läggs till för att skicka en `data_sent_outside` -händelse varje gång data överförs från Commerce-instansen till en Commerce-tjänst <!--MDEE-785-->

## 103.3.3 Release

![Ny](../assets/new.svg) SaaS-dataexport cachelagrar nu EAV-attribut (Entity-Attribute-Value) för attributmetadatafrågan.

![Korrigera](../assets/fix.svg) Ett fel har korrigerats där `InventoryStockStatus`-feeden inte sparades vid återförsök om produkten togs bort.

## 103.3.2 Utgåva

![Korrigera](../assets/fix.svg) Ett problem där fältet `modifiedAt` saknades i borttagna entitetsfeeds har korrigerats.

## 103.3.1 Utgåva

![Åtgärda](../assets/fix.svg) Ett problem som orsakade att ett `Invalid Template File`-meddelande visades under omindexering av produktflöden när Page Builder installerades har åtgärdats.

## 103.3.0-utgåvan

![Nytt](../assets/new.svg) Migrerade tabeller för omedelbar export av feed till den enhetliga strukturen:
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![Ny](../assets/new.svg) Migrerade katalog- och lagerfeeds till lösningen för omedelbar export.

![Nytt](../assets/new.svg) har bytt namn på direktexport av cron-jobb för feed till `*_feed_resend_failed_items`.

![Nytt](../assets/new.svg) har bytt namn på flöden för omedelbar export, ID:n för indexerarvy och ändringsloggtabeller.
- flödestabeller (och ID för indexerarvy):
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- ändra namn på loggtabeller - Använder samma namnmönster som matningstabellerna, men om du ändrar namn på loggtabeller läggs ett `_cl`-suffix till.  Till exempel `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
Om du har egen kod som refererar till någon av dessa enheter måste du uppdatera referenserna med de nya namnen för att se till att koden fortsätter att fungera korrekt.

![Åtgärda](../assets/fix.svg) Ange `modified_at`-fält i feed-data endast för feeds som kräver det.

![Åtgärda](../assets/fix.svg) Ändra `productAttributes`-frågan om du bara vill hämta produktattribut.

## 103.2.6 Utgåva

![Korrigera](../assets/fix.svg) Ett problem som gjorde att feeds inte kunde indexeras om när tabeller har ett prefix har åtgärdats.

## 103.2.5 Utgåva

![Korrigera](../assets/fix.svg) Optimerade prisfrågan.

## 103.2.4 Utgåva

![Åtgärda](../assets/fix.svg) Korrigerade felaktig Stock-status som visades för en produkt när Commerce Inventory management är aktiverat.

## 103.2.3 Version

![Korrigera](../assets/fix.svg) Specialpriser på webbplatsnivå har korrigerats.
![Korrigera](../assets/fix.svg) har lagts till för alla feeds som bearbetas.


## 103.2.2 Utgåva

![Korrigera](../assets/fix.svg) Förbättrad batchstrategi för stora kataloger. Batchtabellen är nu ifylld med ett begränsat antal ID:n för att minska minnesanvändningen.

![Korrigera](../assets/fix.svg) Det hårda beroendet för CommerceInventoryDataExporter till MSI-moduler har tagits bort.

![Åtgärda](../assets/fix.svg) Förbättrade `commerce-data-exporter` loggar för att samla in mer information och ordna efter olika exportsteg.

## 103.2.1 Utgåva

- Frisläppt uppdaterad version.

## 103.2.0-utgåvan

- Datasynkronisering med flera trådar har lagts till för produkter och priser.
