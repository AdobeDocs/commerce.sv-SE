---
title: Kommandoradsgränssnitt för SaaS-dataexport
description: Lär dig hur du använder kommandoradskommandon för att hantera feeds och processer för  [!DNL data export extension] for Adobe Commerce SaaS-tjänster.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Kommandoradsgränssnittsreferens för SaaS-dataexport

Utvecklare och systemadministratörer kan hantera synkroniseringsåtgärder för SaaS-dataexport med [Adobe Commerce kommandoradsverktyg](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI). Kommandot `saas:resync` ingår i paketet `magento/saas-export`.

Adobe rekommenderar inte att du använder kommandot `saas:resync` regelbundet. Vanliga scenarier för kommandot är:

- Den inledande synkroniseringen
- [SaaS-dataområdes-ID ](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) ändrades och du måste synkronisera data till det nya dataområdet.
- Felsökning

## Inledande synkronisering

>[!NOTE]
>Om du använder Live Search eller Produktrekommendationer behöver du inte köra den inledande synkroniseringen. Processen startas automatiskt när du har anslutit tjänsten till din Commerce-instans.

När du utlöser en `saas:resync` från kommandoraden, beroende på katalogstorleken, kan det ta från några minuter till några timmar innan data uppdateras.

För den första synkroniseringen rekommenderar Adobe att du kör kommandona i följande ordning:

```bash
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

## Exempel på kommandon

Granska [alternativbeskrivningarna](#command-options) innan du använder `saas:resync`-kommandon.

- Utför en fullständig omsynkronisering för en entitetsfeed.

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  Feeds som redan har exporterats synkroniseras inte om.

- Synkronisera om den angivna feeden och rensningsdata fullständigt

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  Använd endast efter att ha utfört en [!DNL Data Space ID Cleanup]-åtgärd.

- Om du vill exportera feeds skickar du om alla data till anslutna Commerce-tjänster utan att trunkera indexdata i flödestabellen

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- Visa tillgängliga kommandon och alternativ med beskrivningar.

  ```
  bin/magento saas:resync --help
  ```

## Kommandoalternativ

Följande alternativ är tillgängliga för att hantera `saas:resync`-åtgärder.

>[!NOTE]
>
>Kommandot `saas:resync` stöder även avancerade alternativ för att förbättra dataexportkommandon genom att öka gruppstorleken och lägga till flertrådsbearbetning. Se [Anpassa exportbearbetning](customize-export-processing.md).

### `feed`

Det här obligatoriska alternativet anger vilken feed-entitet som ska synkroniseras igen, till exempel `products`.

Alternativvärdet `feed` kan innehålla någon av de tillgängliga entitetsflödena:

- `products`: produktdatafeed
- `productAttributes`: datafeed för produktattribut
- `categories`: kategoridatafeed
- `variants`: Datafeed för konfigurerbara produktvarianter
- `prices`: produktprisdatafeed
- `categoryPermissions`: datafeed för kategoribehörigheter
- `productOverrides`: datafeed för produktbehörigheter
- `inventoryStockStatus`: Dataflöde för lagerstatus
- `scopesWebsite`: webbplatser med butiker och lagring visar dataflöde
- `scopesCustomerGroup`: kundgruppdatafeed
- `orders`: Datafeed för försäljningsorder

Beroende på vilka [Commerce Services](../landing/saas.md) som är installerade kan det finnas en annan uppsättning feeds tillgängliga för kommandot `saas:resync`.

### `no-reindex`

Det här alternativet skickar om befintliga katalogdata till [!DNL Commerce Services] utan omindexering. Om det här alternativet inte anges kör kommandot en fullständig omindexering innan data synkroniseras.

Beteendet för det här alternativet beror på om feeden exporteras i [äldre eller direkt exportläge](data-synchronization.md#synchronization-modes)

- För tidigare exportflöden trunkeras inte indexerade data i flödestabellen i synkroniseringsprocessen. I stället skickas alla data vidare till Adobe Commerce-tjänsten.
- För flöden med omedelbar export ignoreras det här alternativet om det anges. För dessa flöden trunkeras inte indexet av den omsynkroniserade processen och endast uppdateringar eller objekt som tidigare misslyckades synkroniseras igen.

### `cleanup`

Med det här alternativet rensas tabellen för flödesindexerare före en synkronisering. När SaaS-dataexporten anges körs en fullständig omsynkronisering för den angivna feeden och alla befintliga data i flödestabellen rensas.

Adobe rekommenderar att du bara använder det här kommandot när du har utfört åtgärden [!DNL Data Space ID Cleanup].

>[!WARNING]
>
>**Använd inte det här alternativet regelbundet**. Det kan orsaka problem med datasynkronisering i Adobe Commerce Services. `delete product event` kanske inte sprids till Adobe Commerce-tjänsten om alternativet `cleanup` används.

## Felsökning

Om du inte ser förväntade data i anslutna Commerce-tjänster felsöker du problemen genom att kontrollera felloggar för dataexport och använda kommandot `saas:resync` med miljövariabler för att granska nyttolaster och profileringsdata. Se [Granska loggar och felsöka](troubleshooting-logging.md).
