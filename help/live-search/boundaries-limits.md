---
title: Gränser och begränsningar
description: Lär dig mer om gränserna och gränserna för  [!DNL Live Search] så att du kan vara säker på att det uppfyller behoven i din verksamhet.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 6103707941c0a5544734d3523dded19d65717890
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---

# Gränser och begränsningar

När det gäller webbplatssökningar har Adobe Commerce fler alternativ. Granska följande gränser och gränser för att säkerställa att [!DNL Live Search] och [!DNL Catalog Service] uppfyller ditt företags behov. Om du behöver avancerade sökfunktioner som innehållssökning, BYOA (Bring-your-own-algorithm) eller attributbaserad marknadsföring bör du överväga en tredjepartslösning.

## Allmänt

- Modulen [Avancerad sökning](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search) är inaktiverad när [!DNL Live Search] är installerat och länken Avancerad sökning i sidfoten i förgrunden har tagits bort.
- [Nivåpris](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/products/pricing/product-price-tier) stöds inte i fältet [!DNL Live Search] och i widgeten Produktlistsida.
- Produktpriserna inkluderar moms, men [!DNL Live Search] kan inte visa momsen som ett separat värde.
- Innehållssökning (CMS-sidor och -block) stöds inte.
- Det maximala antalet resultat som kan sidnumreras är 10 000. För att säkerställa att kunderna inte behöver använda djup sidnumrering när en kategori eller sökresultat innehåller ett stort antal produkter, kan du erbjuda användbara sätt att filtrera produkter.
- Det finns en hård gräns på 1 MB per attribut, inklusive beskrivning och anpassade attribut.
- Sökadaptern stöder inte produktattribut som har skapats med en anpassad källmodell och används som facets. Om du vill ha stöd för den här funktionen måste du använda [widgeten Produktlistsida](plp-styling.md).
- Sökadaptern används inte i Live Search 4.0.0.
- Anpassade produkttyper stöds inte.
- Anpassade attribut som skapats programmatiskt med `"is_user_defined": false` stöds inte.
- Du kan filtrera resultat med hjälp av villkoren &quot;börjar med&quot; eller &quot;innehåller&quot; med vissa begränsningar som beskrivs i [utvecklardokumentationen](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations).
- Du kan bara spåra prestandamått under det senaste året.
- Om en sökfråga innehåller flera ord behandlas de som separata söktermer om de är tomma mellan orden. Använd [synonymer](./synonyms.md) om du vill ta hänsyn till sökfrågor med flera ord.
- [!DNL Live Search] stöder inte [omdirigering av söktermer](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/catalog/search/search-terms) internt. Implementera omdirigeringar genom att använda Fast eller någon annan anpassad konfiguration.

## Indexering

- [!DNL Live Search] [index](indexing.md) upp till totalt 450 produktattribut per butiksvy. Dessa fördelas enligt följande:
   - 50 sorterbara attribut
   - 200 filterbara attribut
   - 200 sökbara attribut
- [!DNL Live Search] indexerar bara produkter från Adobe Commerce-databasen.
- CMS-sidor är inte indexerade.
- SKU-, namn- och kategoriattribut går att söka i som standard och kan inte uteslutas från sökningen. Se till att du tar bort tilldelningen av produkterna från kategorierna om de inte ska ingå i dessa kategorier.

## Fasetter

- I uppsättningen med definierade filterbara attribut kan du konfigurera upp till 100 attribut som fasets.
- Inom ett facet kan högst 100 hinkar returneras. Om du behöver returnera fler än 100 bucket [skapar du en supportbiljett](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) så att Adobe kan analysera prestandapåverkan och avgöra om det är möjligt att öka den här gränsen för din miljö.
- Dynamiska aspekter kan orsaka prestandaproblem i stora index och index med hög ordningstalsgrad. Om du har skapat dynamiska ansikten och observerar prestandaförsämringar eller sidor som inte läses in med timeoutfel, kan du försöka ändra dina facets till fäst för att avgöra om detta löser ditt prestandaproblem.
- Stock-status (`quantity_and_stock_status`) stöds inte som en fasett. Du kan använda `inStock: 'true'` för att filtrera bort från Stock-produkter. Detta stöds inte i rutan i modulen `LiveSearchAdapter` när &quot;Visa utanför stockprodukter&quot; är inställt på &quot;Sant&quot; i [!DNL Commerce] Admin.
- Datumtypsattribut stöds inte som en faktor.
- Ändringar som görs i attributets metadata efter att attributet har lagts till som en egenskap återspeglas inte i ansiktet.
- Du kan ha upp till 50 sorterbara attribut och 200 sökbara attribut.

## Fråga

- [!DNL Live Search] använder en unik [GraphQL-slutpunkt](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) för frågor för att stödja funktioner som dynamisk Faceeting och sökning-som-du-typ. Även om det liknar [GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/) finns det vissa skillnader och vissa fält är kanske inte helt kompatibla.
- Det maximala antalet resultat som kan returneras i en sökfråga är 10 000.
- Det högsta antalet resultat per sida är 500.
- Det går inte att filtrera resultat med ett datumtypsattribut.

>[!NOTE]
>
>Sortering efter position kräver att ett giltigt `categoryPath`- eller `categoryIds`-filter är aktivt. [Läs mer](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#error-handling-for-categorypath-and-categoryids).

## Söka efter marknadsföring

- Det högsta antalet [regler](rules.md) för sökmarknadsföring per butiksvy är 50.
- Det högsta antalet villkor per regel är 10.
- Det högsta antalet händelser per regel är 25.
- Regler och manuellt rankade produkter tillämpas på sökresultaten när standardsorteringsordningen, &quot;Sortera efter: mest relevant&quot; har valts. Om en kund ändrar sorteringsordningen till något som att sortera efter namn eller pris gäller inte längre regler och manuella rankningar.
- För att undvika oförutsägbara resultat i sidnumrerade svar bör antalet fästa produkter inte överskrida den begärda sidstorleken.

## Synonymer

- [!DNL Live Search] kan hantera upp till 200 [synonymer](synonyms.md) per butiksvy.

## Kategoriförsäljning

- Du kan skapa en regel per kategori för varje butiksvy.
- Det högsta antalet villkor per regel är 10.
- Det högsta antalet händelser per regel är 25.
- Regler tillämpas när en viss kategori öppnas i butiken och det finns en regel för den kategorin. För regler för kategorimarknadsföring är standardsorteringsordningen&quot;Sortera efter: Position&quot;. Om en kund ändrar sorteringsordningen sorteras inte längre alla dolda, fasta och dolda produkter.

## B2B- och kategoribehörigheter

- Produkter visas inte om de inte har lagts till i en delad standardkatalog.
- Så här begränsar du kundgrupper med [kategoribehörigheter](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/categories/category-permissions):
   - Produkter måste tilldelas till rotkategorin. (**Obs!** Du kan ta bort den här begränsningen genom att uppdatera tillägget SaaS-dataexport till version 103.4.0+. Se [Hantera dataexporttillägget](../data-export/manage-extension.md).
   - Kundgruppen &quot;Inte inloggad&quot; måste ha behörigheten &quot;Tillåt&quot; för bläddring.
   - Om du vill begränsa produkter till kundgruppen Inte inloggad går du till varje kategori och anger behörigheter för varje [kundgrupp](https://experienceleague.adobe.com/sv/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- Det finns för närvarande inget stöd för B2B med PLP-widgeten i PWA Studio. Du kan [använda API](install.md#pwa-support) för att implementera den här funktionen.
- Kategorifacet i [!DNL Live Search] kan visa kategorier som inte kan visas för en specifik [kundgrupp](https://experienceleague.adobe.com/sv/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- [!DNL Live Search] har stöd för upp till 1 000 kundgrupper.

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md) är bara tillgängligt för butiker som använder *Luma*-temat, eller ett anpassat tema som baseras på *Luma*. Sidan med vägbeskrivningar på sökresultatsidan kommer inte att ha formatet *Luma*.
- [!DNL popover] stöder inte temat *Tom*.
- [!DNL popover] stöds inte i snabbbeställningsformuläret.
- Önsklistorna och produktjämförelserna stöds inte.
- Valutasymbolen för den peruanska solen (PEN) stöds inte.

## Felsökning

Hjälp om hur du felsöker vanliga problem i [!DNL Live Search] finns i följande artiklar i kunskapsbasen:

- [[!DNL Live Search] katalogen är inte synkroniserad](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) - Tillhandahåller lösningar för när produktkatalogdata inte synkroniseras korrekt mellan din Adobe Commerce-butik och Live Search-tjänsten. I den här artikeln beskrivs hur du verifierar synkroniseringsstatus, identifierar synkroniseringsfel och löser problem med datasynkronisering.
- [[!DNL Live Search] Instrumentpanelen och rankningen av sökresultat är felaktig](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect) - Åtgärdar problem där sökresultat eller prestandamått som visas på kontrollpanelen för Live-sökning inte visas som förväntat. I den här artikeln beskrivs hur du felsöker rankningsavvikelser och inkonsekvenser mellan instrumentpanelsdata.
- [[!DNL Live Search] facets sorteras inte i bokstavsordning](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted) - Korrigerar problemet där ansiktsvärden visas i oväntad ordning i stället för i bokstavsordning. I den här artikeln beskrivs hur du konfigurerar och korrigerar beteendet för facet-sortering i butiken.

Om du behöver mer hjälp kontaktar du [support](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
