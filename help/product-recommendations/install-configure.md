---
title: Installera och konfigurera
description: Lär dig hur du installerar, uppdaterar och avinstallerar  [!DNL Product Recommendations].
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Installera och konfigurera

För att distribuera [!DNL Product Recommendations] till din butik och administratör måste du installera modulen och konfigurera [Commerce Services Connector](../landing/saas.md). När uppdateringarna släpps kan du enkelt uppdatera installationen med den senaste versionen.

- [Installera](#install)
- [Konfigurera](#configure)
- [Uppdatera](#update)
- [Avinstallera](#uninstall)

## Installera [!DNL Product Recommendations] {#install}

Eftersom modulen [!DNL Product Recommendations] är ett fristående metapaket, kommer uppdateringar att släppas oftare än Adobe Commerce. Information om hur du kontrollerar att du är uppdaterad med de senaste felkorrigeringarna och funktionerna finns i [versionsinformationen](release-notes.md).

>[!IMPORTANT]
>
>Kontrollera att du har rätt [berättiganden](../landing/saas.md#credentials) för att använda produktrekommendationer.

Installera modulen `magento/product-recommendations` med Composer:

```bash
composer require magento/product-recommendations
```

### Stöd för Page Builder {#pbsupport}

[!DNL Product Recommendations] för Page Builder är en valfri modul som installeras separat. Installera modulen genom att köra följande kommando om du vill använda [!DNL Product Recommendations] med Page Builder:

```bash
composer require magento/module-page-builder-product-recommendations
```

Genom att aktivera [!DNL Product Recommendations] i Page Builder kan du lägga till en befintlig, aktiv [rekommendationsenhet](https://experienceleague.adobe.com/sv/docs/commerce-admin/page-builder/add-content/recommendations) i allt innehåll som skapas i Page Builder, till exempel sidor, block och dynamiska block.

Mer information finns i [Använda [!DNL Product Recommendations] med Page Builder-innehåll](page-builder.md).

### Lägg till rekommendationstyp för visuell likhet {#vissimsupport}

Rekommendationstypen _Visuell likhet_ gör att du kan distribuera en rekommendationsenhet till produktinformationssidan som visar produkter som [visuellt liknar &#x200B;](type.md#visualsim) den produkt som visas. Rekommendationstypen är mest användbar när bilder och visuella aspekter av produkterna är viktiga delar av shoppingupplevelsen. Installera rekommendationstypen _Visuell likhet_ genom att köra följande kommando:

```bash
composer require magento/module-visual-product-recommendations
```

## Konfigurera [!DNL Product Recommendations] {#configure}

1. När du har installerat modulen `magento/product-recommendations` konfigurerar du [Commerce Services Connector](../landing/saas.md) genom att ange API-nycklar och välja ett SaaS-datautrymme.

   Om du konfigurerar den här anslutningen aktiveras datasynkronisering och kommunikation mellan Commerce-instansen, katalogtjänsten och andra stödtjänster. Datasynkronisering hanteras av [SaaS-tillägget för dataexport](../data-export/overview.md).

1. Om du vill vara säker på att katalogexporten kan köras korrekt kontrollerar du att [cron](https://experienceleague.adobe.com/sv/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) -jobben och [indexers](https://experienceleague.adobe.com/sv/docs/commerce-operations/configuration-guide/cli/manage-indexers) körs och att `Product Feed`-indexeraren är inställd på `Update by Schedule`.

När du har länkat Commerce-programmet till Commerce Services och angett [SaaS-datautrymmet](../landing/saas.md#saas-configuration) påbörjas katalogsynkroniseringen. Du kan sedan [verifiera](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) att beteendedata skickas till din butik.

## Övervaka och felsöka datasynkronisering

Från Commerce Admin kan du övervaka synkroniseringsprocessen med [Dashboard för datahantering](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/data-transfer/data-dashboard). Använd [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) och loggar för att hantera och felsöka processen.

Du kan sedan [verifiera](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) att beteendedata skickas till din butik.

## Uppdatera din [!DNL Product Recommendations]-installation {#update}

Precis som alla Adobe Commerce använder [!DNL Product Recommendations] Composer för installation och uppdateringar. Kör följande om du vill uppdatera modulen `magento/product-recommendations`:

```bash
composer update magento/product-recommendations --with-dependencies
```

Om du vill uppdatera till en huvudversion, till exempel från 5.0 till 6.0, måste du redigera rotfilen `composer.json` för ditt projekt. (Mer information om den senaste versionen finns i [versionsinformationen](release-notes.md).) Låt oss till exempel öppna huvudfilen `composer.json` och söka efter modulen `magento/product-recommendations` :

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Låt oss bump the major version from `5.0` to `6.0`:

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

Spara filen `composer.json` och kör:

```bash
composer update magento/product-recommendations --with-dependencies
```

Eller om du har installerat modulerna `magento/module-visual-product-recommendations` och `magento/module-page-builder-product-recommendations`:

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> I version 3.x.x av produktrekommendationer behövde du bara en API-nyckel. I version 4.x.x och senare måste du ange offentliga och privata API-nycklar för både sandbox- och produktionsmiljöer. Om du inte anger båda paren med API-nycklar kan du inte komma åt funktionen Produktrekommendationer i Admin. Men datainsamlingen fortsätter i er butik och befintliga rekommendationer visas fortfarande för era kunder.

## Brandväggar

Om du vill tillåta produktrekommendationer via en brandvägg lägger du till `commerce.adobe.io` i tillåtelselista.

## Avinstallera [!DNL Product Recommendations] {#uninstall}

Om det behövs kan du [avinstallera](https://experienceleague.adobe.com/sv/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) produktrekommendationsmodulen.
