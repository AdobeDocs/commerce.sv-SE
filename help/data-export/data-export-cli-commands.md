---
title: Synkronisera feeds med Commerce CLI
description: Lär dig hur du använder kommandoradskommandon för att hantera feeds och processer för  [!DNL data export extension] for Adobe Commerce SaaS-tjänster.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 0f1d55f81cb030d218f0aa8dfa2af4dfd8f640c1
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Synkronisera feeds med Commerce CLI

Med kommandot `saas:resync` i paketet `magento/saas-export` kan du hantera datasynkronisering för Adobe Commerce SaaS-tjänster.

Adobe rekommenderar inte att du använder kommandot `saas:resync` regelbundet. Vanliga scenarier för kommandot är:

- Inledande synkronisering
- Synkronisera data till ett nytt datautrymme efter ändring av [SaaS-dataområdes-ID](https://experienceleague.adobe.com/sv/docs/commerce-admin/config/services/saas)
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

Delvis synkronisera om specifika enheter med deras ID:n. Stöder feeds för `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` och `categoryPermissions`.

När du använder alternativet `--by-ids` anger du som standard värden med SKU-värden för produkten. Lägg till alternativet `--id-type=ProductID` om du vill använda produkt-ID i stället.

**Exempel:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

Rensa flödesindexerartabellen innan du indexerar om och skickar data till SaaS. Stöds endast för `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` och `categoryPermissions`.

Om den används med alternativet `--dry-run` utför åtgärden en omsynkroniseringsåtgärd med torr körning för alla objekt.

>[!IMPORTANT]
>
>Använd endast efter miljörensning eller med alternativet `--dry-run`. Om den används i andra fall kan rensningsåtgärden orsaka dataförlust och problem med datasynkronisering.

**Exempel:**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

Återupptar en avbruten omsynkronisering. Stöds endast för feeds av typen `products`, `productAttributes` och `productOverrides`.

**Exempel:**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

Kör omindexeringsprocessen för feeds utan att skicka feeden till SaaS och utan att spara i flödestabellen. Det här alternativet är användbart när du vill identifiera eventuella problem med datauppsättningen.

Lägg till miljövariabeln `EXPORTER_EXTENDED_LOG=1` för att spara nyttolast i `var/log/saas-export.log`.

**Exempel:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### Testa specifika feed-objekt

Testa specifika feed-objekt genom att lägga till alternativet `--by-ids` med den utökade loggsamlingen för att se den genererade nyttolasten i filen `var/log/saas-export.log`.

**Exempel:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### Testa alla feed-objekt

Som standard innehåller den feed som skickas under en `resync --dry-run`-åtgärd bara nya objekt, eller objekt som inte har exporterats tidigare. Om du vill ta med alla objekt i den feed som ska bearbetas använder du alternativet `--cleanup-feed`.

**Exempel**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

Obligatoriskt. Anger den feed-entitet som ska synkroniseras igen.

Tillgängliga feeds:

- `categories`
- `categoryPermissions`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

>[!NOTE]
>
>Vilka flöden som är tillgängliga i din miljö kan vara olika beroende på vilka moduler som är installerade i din Adobe Commerce-miljö.

**Exempel:**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

Skickar befintliga katalogdata till [!DNL Commerce Services] igen utan omindexering. Stöds inte för produktrelaterade feeds.

Beteendet varierar beroende på [exportläge](data-synchronization.md#synchronization-modes):

- Äldre läge: Skickar alla data igen utan att trunkeras.
- Omedelbart läge: Alternativet ignoreras, endast synkroniserar uppdateringar/fel.

**Exempel:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

Som standard anges de enheter som anges när du använder kommandot `saas:resync feed` med alternativet `--by-ids` av produkt-SKU:n. Använd alternativet `--id-type=ProductId` för att ange enheter efter produkt-ID.

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**Exempel:**

## Felsökning

Om du inte ser förväntade data i anslutna Commerce-tjänster felsöker du problemen genom att kontrollera felloggar för dataexport och använda kommandot `saas:resync` med miljövariabler för att granska nyttolaster och profileringsdata. Se [Granska loggar och felsöka](troubleshooting-logging.md).
