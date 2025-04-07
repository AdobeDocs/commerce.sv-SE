---
title: Gränser och begränsningar
description: Lär dig mer om gränserna och gränserna för  [!DNL Live Search] så att du kan vara säker på att det uppfyller behoven i din verksamhet.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 7dd7ebfae07351f32e781c61b3019b75b421287f
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# Gränser och begränsningar

När det gäller webbplatssökningar har Adobe Commerce fler alternativ. Granska följande gränser och gränser för att säkerställa att [!DNL Live Search] och [!DNL Catalog Service] uppfyller ditt företags behov. Om du behöver avancerade sökfunktioner som innehållssökning, BYOA (Bring-your-own-algorithm) eller attributbaserad marknadsföring bör du överväga en tredjepartslösning.

## Allmänt

- Modulen [Avancerad sökning](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) är inaktiverad när [!DNL Live Search] är installerat och länken Avancerad sökning i sidfoten i förgrunden har tagits bort.
- [Nivåpris](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier) stöds inte i fältet [!DNL Live Search] och i widgeten Produktlistsida.
- Priserna inkluderar inte moms.
- Innehållssökning (CMS-sidor och -block) stöds inte.
- Det finns en gräns på 10 000 produkter som kan sidnumreras. Även om den här gränsen kan höjas kan den påverka prestandan. Se till att ni kan filtrera produkter på meningsfulla sätt om en kategori eller ett sökresultat har ett stort antal produkter så att kunderna inte behöver använda djup sidnumrering.
- Det finns en hård gräns på 1 MB per attribut, inklusive beskrivning och anpassade attribut.
- Sökadaptern stöder inte produktattribut som har skapats med en anpassad källmodell och används som facets. Om du vill ha stöd för den här funktionen måste du använda [widgeten Produktlistsida](plp-styling.md).
- Anpassade produkttyper stöds inte.
- Anpassade attribut som skapats programmatiskt med `"is_user_defined": false` stöds inte.
- Du kan filtrera resultat med hjälp av villkoren &quot;börjar med&quot; eller &quot;innehåller&quot; med vissa begränsningar som beskrivs [här](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#limitations).
- Du kan bara spåra prestandamått under det senaste året.

## Indexering

- [!DNL Live Search] [index](indexing.md) upp till totalt 450 produktattribut per butiksvy. Dessa fördelas enligt följande:
   - 50 sorterbara attribut
   - 200 filterbara attribut
   - 200 sökbara attribut
- [!DNL Live Search] indexerar bara produkter från Adobe Commerce-databasen.
- CMS-sidor är inte indexerade.
- SKU-, namn- och kategoriattribut går att söka i som standard och kan inte uteslutas från sökningen. Se till att du tar bort tilldelningen av produkterna från kategorierna om de inte ska ingå i dessa kategorier.

## Fasetter

- Högst 100 attribut kan konfigureras som facets från de 200 filterbara attribut som kan indexeras.
- Inom ett facet kan högst 100 hinkar returneras. Om du behöver returnera fler än 100 bucket [skapar du en supportbiljett](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) så att Adobe kan analysera prestandapåverkan och avgöra om det är möjligt att öka den här gränsen för din miljö.
- Dynamiska aspekter kan orsaka prestandaproblem i stora index och index med hög ordningstalsgrad. Om du har skapat dynamiska ansikten och observerar prestandaförsämringar eller sidor som inte läses in med timeoutfel, kan du försöka ändra dina facets till fäst för att avgöra om detta löser ditt prestandaproblem.
- Stock-status (`quantity_and_stock_status`) stöds inte som en fasett. Du kan använda `inStock: 'true'` för att filtrera bort från Stock-produkter. Detta stöds inte i rutan i modulen `LiveSearchAdapter` när &quot;Visa utanför stockprodukter&quot; är inställt på &quot;Sant&quot; i [!DNL Commerce] Admin.
- Datumtypsattribut stöds inte som en faktor.
- Ändringar som görs i attributets metadata efter att attributet har lagts till som en egenskap återspeglas inte i ansiktet.

## Fråga

- [!DNL Live Search] använder en unik [GraphQL-slutpunkt](https://developer.adobe.com/commerce/services/graphql/live-search/) för frågor för att stödja funktioner som dynamisk Faceeting och sökning-som-du-typ. Även om det liknar [GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/) finns det vissa skillnader och vissa fält är kanske inte helt kompatibla.
- Det maximala antalet resultat som kan returneras i en sökfråga är 10 000.
- Det högsta antalet resultat per sida är 500.
- Det går inte att filtrera resultat med ett datumtypsattribut.

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
- Så här begränsar du kundgrupper med [kategoribehörigheter](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions):
   - Produkter måste tilldelas till rotkategorin. (**Obs!** Du kan ta bort den här begränsningen genom att uppdatera tillägget SaaS-dataexport till version 103.4.0+. Se [Hantera dataexporttillägget](../data-export/manage-extension.md).
   - Kundgruppen &quot;Inte inloggad&quot; måste ha behörigheten &quot;Tillåt&quot; för bläddring.
   - Om du vill begränsa produkter till kundgruppen Inte inloggad går du till varje kategori och anger behörigheter för varje [kundgrupp](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- Det finns för närvarande inget stöd för B2B med PLP-widgeten i PWA Studio. Du kan [använda API](install.md#pwa-support) för att implementera den här funktionen.
- Kategorifacet i [!DNL Live Search] kan visa kategorier som inte kan visas för en specifik [kundgrupp](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- [!DNL Live Search] har stöd för upp till 1 000 kundgrupper.

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md) är bara tillgängligt för butiker som använder *Luma*-temat, eller ett anpassat tema som baseras på *Luma*. Sidan med vägbeskrivningar på sökresultatsidan kommer inte att ha formatet *Luma*.
- [!DNL popover] stöder inte temat *Tom*.
- [!DNL popover] stöds inte i snabbbeställningsformuläret.
- Önsklistorna och produktjämförelserna stöds inte.
- Valutasymbolen för den peruanska solen (PEN) stöds inte.

## Felsökning

Hjälp om hur du felsöker några vanliga problem i [!DNL Live Search] finns i följande artiklar i kunskapsbasen:

- [[!DNL Live Search] katalogen är inte synkroniserad](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)
- [[!DNL Live Search] instrumentpanelen och rankningen av sökresultat är felaktig](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect)
- [[!DNL Live Search] visar färdiga produkter oavsett vilka inställningar för Stock-status som gäller i Admin](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-displays-out-of-stock-products)
- [[!DNL Live Search] facets sorteras inte i bokstavsordning](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted)

Om du behöver mer hjälp kontaktar du [support](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
