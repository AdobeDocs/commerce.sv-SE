---
title: '[!DNL Manage the Data Export extension]'
description: Lär dig hur du uppgraderar  [!DNL Data Export] tillägget och tar bort eller inaktiverar dataexporttjänster som inte behövs.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Hantera SaaS-dataexporttillägget

Tillägget [!DNL data export] för SaaS-tjänster är en samling moduler som möjliggör datainsamling och synkronisering mellan Adobe Commerce och anslutna Commerce-tjänster.

Specifika moduler ingår i metapaketen för Adobe Commerce Services-tillägg, som
som [Live Search](/help/live-search/overview.md), [Produktrekommendationer](/help/product-recommendations/overview.md) och [katalogtjänst](/help/catalog-service/overview.md). Om du använder de här tjänsterna krävs ingen separat installation för att aktivera tillägget för dataexport.

## Ta bort eller inaktivera Commerce dataexportfunktioner

Om du inte behöver någon av de installerade exportmodulerna för handelsdata kan du inaktivera det med kommandot `magento:module:disable` CLI.

Det finns till exempel ett [Kategorier-API](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) som använder kategorierna för behörighet att skicka data internt. Om du inte använder detta API kan du inaktivera dataexporten för kategoribehörighetsflödet.

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Uppdatera en modul till en viss version

Du kan uppdatera alla installerade exportmoduler för handelsdata med Composer. Du kan till exempel uppdatera en modul till en viss version och även uppdatera eventuella beroenden som krävs.

1. Logga in på Commerce programserver.

1. Uppdatera modulen med Composer från kommandoraden:

   ```bash
   composer require magento/module-saas-price:103.3.1 --with-all-dependencies
   ```

Om Commerce-instansen distribueras i molninfrastrukturen ska du uppdatera tillägget från din molnprojektkatalog. Se [Uppgradera ett tillägg](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) i _Adobe Commerce on Cloud Infrastructure Guide_.
