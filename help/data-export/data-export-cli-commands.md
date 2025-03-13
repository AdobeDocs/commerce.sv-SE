---
title: Synkronisera feeds med Commerce CLI
description: Lär dig hur du använder kommandoradskommandon för att hantera feeds och processer för  [!DNL data export extension] for Adobe Commerce SaaS-tjänster.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Synkronisera feeds med Commerce CLI

Med kommandot `saas:resync` i paketet `magento/saas-export` kan du hantera datasynkronisering för Adobe Commerce SaaS-tjänster.

Adobe rekommenderar inte att du använder kommandot `saas:resync` regelbundet. Vanliga scenarier för kommandot är:

- Inledande synkronisering
- Synkronisera data till det nya dataområdet efter ändring av [SaaS-dataområdes-ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Felsökning

Övervaka synkroniseringsåtgärder i filen `var/log/saas-export.log`.

## Inledande synkronisering

>[!NOTE]
>
>Initial synkronisering körs automatiskt när Live Search eller Produktrekommendationer är aktiverade. Manuella kommandon behövs inte.

När du utlöser en `saas:resync` från kommandoraden, beroende på katalogstorleken, kan det ta från några minuter till några timmar innan data uppdateras.

För den första synkroniseringen rekommenderar Adobe att du kör kommandona i följande ordning:

```shell
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

## Synkronisera med CLI-kommandon

Kommandot `saas:resync` stöder olika synkroniseringsåtgärder:

- Delvis synkronisering via SKU
- Återuppta avbrutna synkroniseringar
- Validera data utan synkronisering

Visa alla tillgängliga alternativ:

```shell
bin/magento saas:resync --help
```

I följande avsnitt finns exempel på alternativbeskrivningar.


>[!NOTE]
>
>Avancerade alternativ för att hantera exportbearbetning finns i [Anpassa exportbearbetning](customize-export-processing.md).

## `--by-ids`

Delvis synkronisera om specifika enheter med deras ID:n. Stöder feeds av typen `products`, `productAttributes` och `productOverrides`.

Enheter anges som standard av produkt-SKU. Använd `--id-type=ProductID` om du vill använda produkt-ID:n i stället.

**Exempel:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

Rensar tabellen för flödesindexering innan den indexeras om och skickar data till SaaS. Stöds endast för feeds av typen `products`, `productOverrides` och `prices`.

>[!IMPORTANT]
>
>Använd endast efter miljörensning. Kan orsaka problem med datasynkronisering i Commerce Services.

**Exempel:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

Återupptar en avbruten omsynkronisering. Stöds endast för feeds av typen `products`, `productAttributes` och `productOverrides`.

**Exempel:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

Kör omindexeringsprocessen för feeds utan att skicka till SaaS eller spara till flödestabellen. Validera data.

Lägg till miljövariabeln `EXPORTER_EXTENDED_LOG=1` för att spara nyttolast i `var/log/saas-export.log`.

**Exempel:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

Obligatoriskt. Anger den feed-entitet som ska synkroniseras igen.

Tillgängliga feeds:

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**Exempel:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

Skickar befintliga katalogdata till [!DNL Commerce Services] igen utan omindexering. Stöds inte för produktrelaterade feeds.

Beteendet varierar beroende på [exportläge](data-synchronization.md#synchronization-modes):

- Äldre läge: Skickar alla data igen utan att trunkeras.
- Omedelbart läge: Alternativet ignoreras, endast synkroniserar uppdateringar/fel.

**Exempel:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## Felsökning

Om du inte ser förväntade data i anslutna Commerce-tjänster felsöker du problemen genom att kontrollera felloggar för dataexport och använda kommandot `saas:resync` med miljövariabler för att granska nyttolaster och profileringsdata. Se [Granska loggar och felsöka](troubleshooting-logging.md).
