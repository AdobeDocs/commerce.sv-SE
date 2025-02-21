---
title: Installera [!DNL Data Connection]
description: Lär dig hur du installerar, uppdaterar och avinstallerar tillägget  [!DNL Data Connection] från Adobe Commerce.
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Installera [!DNL Data Connection]

[Granska förutsättningarna](overview.md#prereqs) innan du installerar tillägget.

## Installera tillägget

Tillägget [!DNL Data Connection] är tillgängligt från [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html). När du installerar det här tillägget från serverns kommandorad ansluts det till din Adobe Commerce-installation som en [tjänst](../landing/saas.md). När processen är klar visas **[!DNL Data Connection]** och **Commerce Services Connector** på menyn **System** under **Tjänster** i Commerce _Admin_.

![[!DNL Data Connection] tilläggsadministratörsvy](assets/epc-adminui.png)

>[!IMPORTANT]
>
>Tilläggets namn har ändrats från Experience Platform-anslutning till [!DNL Data Connection], men paketnamnet är fortfarande `experience-platform-connector` för att stödja bakåtkompatibilitet.

1. Om du vill hämta paketet `experience-platform-connector` kör du följande från kommandoraden:

   ```bash
   composer require magento/experience-platform-connector
   ```

   Det här metapaketet innehåller följande moduler och tillägg:

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. (Valfritt) Installera tillägget [[!DNL Live Search]](../live-search/install.md) om du vill inkludera [!DNL Live Search]-data, som omfattar [sökhändelser](events.md#search-events).

1. (Valfritt) Om du vill inkludera B2B-data, som omfattar [rekvisitionshändelser](events.md#b2b-events), installerar du [B2B-tillägget](#install-the-b2b-extension).

1. (Valfritt) Om du är vårdförsäljare installerar du tillägget [Data Services HIPAA](#install-the-data-services-hipaa-extension) så att dina [!DNL Commerce] backoffice-data är HIPAA-klara.

### Installera Adobe I/O Events och konfigurera modulen för kundkoppling

När du har installerat tillägget `experience-platform-connector` måste du installera Adobe I/O Events för Adobe Commerce och konfigurera modulen `customers-connector`.

Följande steg gäller både för Adobe Commerce i molninfrastruktur och lokala installationer.

1. Om du kör Commerce 2.4.4 eller 2.4.5 använder du följande kommando för att läsa in händelsemodulerna:

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6 och senare laddar dessa moduler automatiskt.

1. Uppdatera projektberoenden.

   ```bash
   composer update
   ```

1. Aktivera de nya modulerna:

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

Slutför installationen baserat på distributionstyp: Adobe Commerce i molninfrastrukturen eller lokalt.

#### On Cloud-infrastruktur

Aktivera den globala variabeln `ENABLE_EVENTING` i `.magento.env.yaml` i Adobe Commerce på Cloud-infrastrukturen. [Läs mer](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html#enable_eventing).

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

Implementera och skicka uppdaterade filer till molnmiljön. När distributionen är klar aktiverar du skicka händelser med följande kommando:

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### Lokalt

I lokala miljöer måste du manuellt aktivera kodgenerering och Adobe Commerce Events:

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### Installera B2B-tillägget

För B2B-handlare installerar du följande tillägg för att inkludera händelsedata för [rekvisitionslistan](events.md#b2b-events).

Hämta tillägget `magento/experience-platform-connector-b2b` genom att köra följande från kommandoraden:

```bash
composer require magento/experience-platform-connector-b2b
```

### Installera datatjänstens HIPAA-tillägg

För hälso- och sjukvårdspersonalen installerar du följande tillägg för att säkerställa att informationen om händelsen på back office är HIPAA-ready.

Hämta tillägget `magento/module-data-services-hipaa` genom att köra följande från kommandoraden:

```bash
composer require magento/module-data-services-hipaa
```

## Uppdatera tillägget [!DNL Data Connection] {#update}

Om du vill uppdatera tillägget [!DNL Data Connection] kör du följande från kommandoraden:

```bash
composer update magento/experience-platform-connector --with-dependencies
```

Eller, för B2B-handlare:

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

Om du vill uppdatera till en större version, till exempel från 2.0.0 till 3.0.0, redigerar du projektets rotfil [!DNL Composer] `.json` enligt följande:

1. Öppna rotfilen `composer.json` och sök efter `magento/experience-platform-connector`.

1. I avsnittet `require` ska du uppdatera versionsnumret på följande sätt:

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **Spara** `composer.json`. Kör sedan följande från kommandoraden:

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   Eller, för B2B-handlare:

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## Avinstallera tillägget [!DNL Data Connection] {#uninstall}

Information om hur du avinstallerar tillägget [!DNL Data Connection] finns i [avinstallationsmoduler](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html).
