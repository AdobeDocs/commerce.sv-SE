---
title: Installera [!DNL Payment Services]
description: Installera tillägget för Payments Services.
exl-id: babaa91a-9376-4acb-b934-a89f9df52016
role: Admin
feature: Payments, Checkout, Install, Upgrade, Paas
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Installera [!DNL Payment Services]

Om du vill börja använda betalningstjänsterna för [!DNL Adobe Commerce] och [!DNL Magento Open Source] måste du slutföra några startsteg.

>[!INFO]
>
> Mer information finns i videon [Konfigurera [!DNL Payment Services] för Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services).

Hämtning och installation av tillägget [!DNL Payment Services] för [!DNL Adobe Commerce] och [!DNL Magento Open Source] är ett nödvändigt steg för att använda [!DNL Payment Services].

## Hämta tillägget

Du måste hämta tillägget från [Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html) innan du installerar det.

1. Navigera till [Betalningstjänster-tillägget i Commerce Marketplace](https://commercemarketplace.adobe.com/magento-payment-services.html).
1. Om du vill välja utgåva och version växlar du **[!UICONTROL Edition]** och **[!UICONTROL Your store version]** till de alternativ du vill använda.
1. Klicka på **[!UICONTROL Add to Cart]**.
1. Slutför utcheckningen och klicka på **[!UICONTROL Place Order]**.
1. Kontrollera e-postmeddelandet som är kopplat till din Marketplace-nedladdning för att få orderbekräftelse och information.

>[!NOTE]
>
> För Adobe Commerce version 2.4.7 eller senare finns [!DNL Payment Services] att få.

## Installera tillägget

Du kan installera tillägget [!DNL Payment Services] för både [!DNL Adobe Commerce] i molninfrastrukturen och lokala instanser, som är länkade till ditt Commerce-konto [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys) som tillhandahålls i registreringsprocessen.
[!DNL Magento Open Source]-kunder använder de lokala instruktionerna.

I dispositionen används dessa nycklar vid den första installationen av [!DNL Adobe Commerce], eller i situationer där dispositionsnycklarna inte tidigare sparats i filen `auth.json`.

Mer information om hur du hämtar Composer-nycklar finns i [Hämta dina autentiseringsnycklar](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys).

Mer information om vad du bör tänka på innan du hämtar och installerar ett tillägg finns i [Installera ett tillägg](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions).

### [!DNL Adobe Commerce] i molninfrastruktur

Den här metoden används för att installera tillägget [!DNL Payment Services] för en Commerce Cloud-instans.

1. Uppdatera din `composer.json`-fil:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Uppdatera beroenden och installera tillägget:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Använd kommandot `composer update` för att uppdatera alla rotberoenden.

1. Verkställ och push-styr ändringarna.

### Lokala konfigurationer och andra konfigurationer

Den här metoden används för att installera tillägget [!DNL Payment Services] för en lokal instans och [!DNL Magento Open Source]-kunder.

1. Kör följande kommandon för att hämta tillägget:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Uppdatera beroenden och installera tillägget:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Använd kommandot `composer update` för att uppdatera alla rotberoenden.

1. Uppgradera din instans:

   ```bash
   bin/magento setup:upgrade
   ```

1. Rensa cachen:

   ```bash
   bin/magento cache:clean
   ```

1. Verkställ ändringarna.
1. Uppdatera instansen för att vara säker på att den implementerade koden distribueras.

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1 är kompatibel med PHP-version 7.x. Vi rekommenderar dock att du uppdaterar till den senaste [!DNL Payment Services] -versionen.

## Uppgradera tillägget

När en ny version av [!DNL Payment Services] släpps kan du enkelt uppgradera ditt tillägg.

1. Så här hämtar du den senaste versionen av paketet:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Använd kommandot `composer update` för att uppdatera alla rotberoenden.

1. Efter uppdatering av dispositionen kör du:

   ```bash
   bin/magento setup:upgrade
   ```

1. Verkställ och push-styr ändringarna.

## Felsökning

Fel kan uppstå när tillägget [!DNL Payment Services] installeras. Använd följande felsökningsmetoder för att åtgärda felen.

### Lista över databaser

Kontrollera att `repo.magento.com` finns i din lista över databaser.

### Felaktiga dispositionsnycklar

Om följande fel visar att du har fel Composer-tangenter:

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Kontrollera att Composer-tangenterna är giltiga och att du har tillgång till andra Magento-paket.

Så här ser du vilka dispositionsnycklar som är konfigurerade:

1. Hitta platsen för filen `auth.json`:

   ```bash
   composer config --global home
   ```

1. Visa filen `auth.json`:

   ```bash
   cat /path/to/auth.json
   ```

1. Se [vilka nycklar som är associerade med ditt Commerce-konto `MageID`](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys).

### Inte tillräckligt med minne för PHP

Om följande felmeddelande visas har du inte tillräckligt med minne för PHP:

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[Öka minnesgränsen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit) för PHP i din miljö i `php.ini`.

Du kan också ange minnesgränsen med det här kommandot: `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`.

Exempel:

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
