---
title: Installera och konfigurera
description: Läs mer om hur du installerar, uppdaterar och avinstallerar [!DNL Product Recommendations].
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce on Cloud-projekt (PaaS-infrastruktur som hanteras av Adobe) och lokala projekt."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '582'
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

### Lägg till stöd för Page Builder {#pbsupport}

[!DNL Product Recommendations] för Page Builder är en valfri modul som installeras separat. Om du vill använda [!DNL Product Recommendations] Page Builder installerar du modulen genom att köra följande kommando:

```bash
composer require magento/module-page-builder-product-recommendations
```

Genom att aktivera [!DNL Product Recommendations] i Page Builder kan du lägga till en befintlig, aktiv [rekommendationsenhet](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) i allt innehåll som skapas i Page Builder, till exempel sidor, block och dynamiska block.

Mer information finns [i Använda [!DNL Product Recommendations] med Page Builder-innehåll](page-builder.md) .

### Lägga till rekommendationstyp för visuell likhet {#vissimsupport}

Med rekommendationstypen _Visuell likhet_ kan du distribuera en rekommendationsenhet till din produktinformationssida som visar produkter som visuellt liknar[&#128279;](type.md#visualsim) den produkt som visas. Den här rekommendationstypen är mest användbar där bilder och visuella aspekter av produkterna är viktiga delar av shoppingupplevelsen. Installera rekommendationstypen _Visuell likhet_ genom att köra följande kommando:

```bash
composer require magento/module-visual-product-recommendations
```

## Konfigurera [!DNL Product Recommendations] {#configure}

1. När du har installerat `magento/product-recommendations` modulen konfigurerar [du Commerce Services Connector](../landing/saas.md) genom att ange API-nycklar och välja ett SaaS-datautrymme.

   Genom att konfigurera den här anslutningen kan du synkronisera data och kommunicera mellan Commerce-instansen, katalogtjänsten och andra stödtjänster. Datasynkronisering hanteras av [SaaS-tillägget](../data-export/overview.md) för dataexport.

1. Om du vill vara säker på att katalogexporten kan köras korrekt kontrollerar du att [cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) -jobben och [indexers](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) körs och att `Product Feed`-indexeraren är inställd på `Update by Schedule`.

När du har länkat Commerce-programmet till Commerce Services och angett [SaaS-datautrymmet](../landing/saas.md#saas-configuration) påbörjas katalogsynkroniseringen. Du kan sedan [verifiera](verify.md) att beteendedata skickas till din butik.

## Övervaka och felsöka datasynkronisering

Från Commerce Admin kan du övervaka synkroniseringsprocessen med [Dashboard för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Använd [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) och loggar för att hantera och felsöka processen.

Du kan sedan [verifiera](verify.md) att beteendedata skickas till din butik.

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

`composer.json` Spara filen och kör:

```bash
composer update magento/product-recommendations --with-dependencies
```

Eller om du har installerat `magento/module-visual-product-recommendations` modulerna och `magento/module-page-builder-product-recommendations` :

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> I version 3.x.x av Product Recommendations behövde du bara en enda API-nyckel. I version 4.x.x och senare måste du ange offentliga och privata API-nycklar för både sandbox- och produktionsmiljöerna. Om du inte anger båda paren med API-nycklar kan du inte komma åt funktionen Product Recommendations i Admin. Datainsamlingen fortsätter dock i ditt skyltfönster och befintliga rekommendationer fortsätter att visas för dina kunder.

## Brandväggar

Om du vill släppa igenom Product Recommendations genom en brandvägg lägger du till `commerce.adobe.io` i listan över tillåtna.

## Avinstallera [!DNL Product Recommendations] {#uninstall}

Om det behövs kan du [avinstallera](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) produktrekommendationsmodulen.
