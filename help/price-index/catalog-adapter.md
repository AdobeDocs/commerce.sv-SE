---
title: Katalogkortstillägg
description: Återge priser från Commerce Services med hjälp av katalogadaptern
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
exl-id: e42101fa-9c30-482c-a649-44dc35376abb
source-git-commit: 74f6cb64724194651c4eeb538c0c69142b01ac5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Katalogadapter

Tillägget `[!DNL Catalog Adapter]` inaktiverar standardproduktprisindexeraren som ingår i Commerce-programmet och använder priser som tillhandahålls av [katalogtjänsten](../catalog-service/overview.md) i stället.

Kortet är utformat för att fungera med [SaaS-dataexporten](../data-export/overview.md) och Adobe Commerce-tjänsten. SaaS-dataexport ansvarar för att skicka priserna och [!DNL Catalog Adapter] hämtar alla priser från Adobe Commerce-tjänsten.

När du aktiverar [!DNL Catalog Adapter] påverkas prisindexering och åtgärder på följande sätt:

- Prisindexeraren som ingår i Adobe Commerce-programmet är inaktiverad.
- Priserna hanteras med SaaS-dataexporten och prisindexeraren [SaaS](price-indexing.md).
- När en kund öppnar en produkt, kategori eller annan sida som visar produktpriser hämtas priserna från Adobe Commerce-tjänsten.
- Priserna skickas till Adobe Commerce-tjänsten genom att data synkroniseras från [SaaS-dataexporten](../data-export/overview.md).
- Utcheckningen beräknar om priserna dynamiskt.

Du kan aktivera prisindexering på nytt i Commerce genom att ta bort eller inaktivera tillägget Katalogkort.

## Krav

- Adobe Commerce 2.4.4+
- Adobe Commerce-miljön måste ha någon av följande Commerce-tjänster aktiverade och konfigurerade:

   - [Live Search](../live-search/install.md)
   - [Produktrekommendationer](../product-recommendations/install-configure.md)
   - [Katalogtjänst](../catalog-service/installation.md)

## Installation

Tillägget Catalog Adapter är ett Composer-metapaket som installerar följande moduler:

- **Inaktivering av prisindexerare**-Den här modulen inaktiverar prisindexet i Commerce-programmet så att priserna levereras via prisindexering för SaaS. Produktprisindexeraren i Commerce kan inte aktiveras när prisindexeringstillägget SaaS är installerat.
- **Prisleverantör** - Den här modulen tillhandahåller priser för produkter från Adobe Commerce-tjänsten. Den utgör sökfrågan och hämtar priserna för produkterna i klientdelen.
- **Sökadapter för katalogtjänst** - Den här modulen överför priser från Adobe Commerce till en Adobe Commerce-tjänst som svar på en produktsökningsbegäran.

## Installationssteg

>[!BEGINTABS]

>[!TAB Molninfrastruktur]

Använd den här metoden för att installera [!DNL Catalog Adapter] för en Commerce Cloud-instans.

1. På din lokala arbetsstation byter du till projektkatalogen för ditt Adobe Commerce i molninfrastrukturprojekt.

   >[!NOTE]
   >
   >Mer information om att hantera Commerce projektmiljöer lokalt finns i [Hantera grenar med CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) i _Adobe Commerce on Cloud Infrastructure User Guide_.

1. Kolla in miljögrenen för att uppdatera med hjälp av Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Lägg till katalogadaptermodulen.

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Uppdatera paketberoenden.

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. Genomför och push-kodsändringar för filerna `composer.json` och `composer.lock`.

1. Lägg till, implementera och skicka kodändringarna för `composer.json`- och `composer.lock`-filerna till molnmiljön.

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   När uppdateringarna skickas till molnmiljön initieras [Commerce molndistributionsprocess](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) för att ändringarna ska tillämpas. Kontrollera distributionsstatusen från [distributionsloggen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Lokal]

Använd den här metoden för att installera [!DNL Catalog Adapter] för en lokal instans.

1. Lägg till katalogadaptern i projektet med Composer:

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Uppdatera beroenden och installera tillägget:

   ```bash
   composer update  "magento/catalog-adapter"
   ```

1. Uppgradera Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Rensa cachen:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >I vissa fall, särskilt när du distribuerar till produktion, kanske du vill undvika att rensa kompilerad kod eftersom det kan ta en stund. Se till att du säkerhetskopierar systemet innan du gör några ändringar.

>[!ENDTABS]


## Återaktivera Adobe Commerce produktprisindexerare

Om du har program från tredje part som är beroende av Adobe Commerce standardproduktprisindexerare kan du aktivera det igen med följande kommandon:

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## Inaktivera produktprisindexeraren för scenariot Headless Storefront

Om du har en headless Commerce-instans kan du behöva inaktivera Adobe Commerce produktprisindexerare för att minska belastningen på din Adobe Commerce-instans. Du kan slutföra den här uppgiften genom att installera modulen `magento/module-price-indexer-disabler`:

```bash
composer require magento/module-price-indexer-disabler
```

## Användningsscenarier

Nedan följer några vanliga `[!DNL Catalog Adapter]`-scenarier.

### Inga beroenden till Adobe Commerce produktprisindexerare

- Du är återförsäljare av Luma- eller Adobe Commerce Core GraphQL som har en obligatorisk tjänst installerad (Live Search, Product Recommendations, Catalog Service)
- Inga integreringar med tillägg från tredje part som kräver Adobe Commerce produktprisindexerare

1. Installera [!DNL Catalog Adapter].

### Med beroenden till Adobe Commerce produktprisindexerare

- Du är återförsäljare av Luma- eller Adobe Commerce Core GraphQL-produkter och har en tjänst som stöds installerad (Live Search, Product Recommendations, Catalog Service)
- Du använder ett tillägg från en annan leverantör som är beroende av Adobe Commerce produktprisindexerare

1. Installera [!DNL Catalog Adapter].
1. Aktivera Adobe Commerce standardprisindexerare.

### Headless Commerce-instanser

- En handlare med en headless Commerce-instans med de nödvändiga tjänsterna installerade (Live Search, Product Recommendations, Catalog Service)
- Ingen användning av Adobe Commerce standardproduktprisindexerare

1. Installera modulen `magento/module-price-indexer-disabler` från paketet [!DNL Catalog Adapter].
