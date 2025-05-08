---
title: Kommandoradskonfiguration
description: Efter installationen kan du konfigurera  [!DNL Payment Services] med kommandoradsgränssnittet (CLI).
role: Admin, Developer
level: Intermediate
exl-id: 265ab1be-fe52-41f3-85cb-addbc2ddfb17
feature: Payments, Checkout, Configuration, Integration, Paas
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Kommandoradskonfiguration

När du har installerat [!DNL Payment Services] kan du enkelt konfigurera det från [ i hemmet ](payments-home.md) eller via kommandoradsgränssnittet (CLI).

## Konfigurera dataexport

[!DNL Payment Services] kombinerar orderdata som exporterats från [!DNL Magento Open Source] och [!DNL Adobe Commerce] med aggregerade betalningsdata från betalningsleverantörer för att skapa användbara rapporter. Tillägget [!DNL Payment Services] använder indexerare för att effektivt samla in alla nödvändiga data för rapporterna.

Mer information om data som används i [!DNL Payment Services]-rapportering finns i [Statusrapport för orderbetalning](order-payment-status.md#data-used-in-the-report).

### Konfigurera kron på [!DNL Magento Open Source]

Om du vill använda ett `BY SCHEDULE`-indexläge på [!DNL Magento Open Source] måste du konfigurera cron. Se [Konfigurera och kör cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs).

### Ange indexerare

Beställningsdata exporteras och sparas i betalningstjänsten med något av två indexlägen: `ON SAVE` (standard) eller `BY SCHEDULE` (rekommenderas).

Följande index gäller [!DNL Payment Services]:

| Code | Namn | Beskrivning |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | Försäljningsorderfeed | Skapar index för orderdata |
| `sales_order_status_data_exporter` | Feed för försäljningsorderstatus | Skapar index för försäljningsorderstatusdata |
| `store_data_exporter` | Lagrar feed | Skapar index för butiksdata |

Om du vill ändra indexläge för alla tre indexerarna kör du:

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>Om du inte anger några indexerare i kommandot uppdateras alla indexerare till samma värde. Om du vill ändra en specifik indexerare måste du ange den i kommandot.

Mer information om hur du ändrar läget för en indexerare manuellt finns i [Konfigurera indexerare](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"} i utvecklardokumentationen. Mer information om hur du ändrar det i Admin finns i [Indexhantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"} i användarhandboken.

### Indexera om data manuellt

Du kan indexera om data manuellt i stället för att vänta på att det ska hända automatiskt. Mer information finns i [Indexera om](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"} i [Hantera index](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"}.

När läget `BY SCHEDULE` är inställt spåras ändrade entiteter och cron-jobbet uppdaterar indexvärdet för dem baserat på ett angivet schema. Se [Kör cron från kommandoraden](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run) i [Konfigurera och kör cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)) om du vill veta hur du manuellt aktiverar indexering med hjälp av cron-jobb.

### Skicka omindexerade data till betalningstjänsten

När data har indexerats skickas de automatiskt till [!DNL Payment Services]. Med det här kommandot kan du även manuellt utlösa processen att skicka indexerade data:

```bash
bin/magento saas:resync --feed [feedName]
```

Använd följande kommandoalternativ:

| Kommando | Beskrivning |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | Utför en omindexering av den angivna feeden och skickar den till motsvarande tjänst |
| `bin/magento saas:resync --no-reindex` | Hoppar över indexering och skickar osynkroniserade data från indexen |

Med parametern `--feed` kan du ange vilken feed du vill skicka:

| Feed | Beskrivning |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | Beställer feed i produktionsläge |
| `paymentServicesOrdersSandbox` | Beställningsfeed i sandlådeläge |
| `paymentServicesOrderStatusesProduction` | Orderstatus i produktionsläge |
| `paymentServicesOrderStatusesSandbox` | Ordna statusvärden i sandlådeläge |
| `paymentServicesStoresProduction` | Lagrar i produktionsläge |
| `paymentServicesStoresSandbox` | Lagrar i sandlådeläge |

Alla data som behövs för rapporterna skickas automatiskt till [!DNL Payment Services] om cron har konfigurerats och installerats. Du kan också manuellt utlösa processen att skicka kunddata till [!DNL Payment Services].

```bash
bin/magento cron:run --group payment_services_data_export
```

Mer information om omindexering och indexering finns i avsnittet [Hantera indexerare](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) i utvecklardokumentationen.

## Konfigurera scope via CLI

[!DNL Payment Services] tillåter handlare att använda [flera PayPal-konton](settings.md#use-multiple-paypal-accounts). Nu kan ni ändra omfång för dessa konton via CLI.

Om du vill ange omfånget till nivån `website` kör du:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

Om du vill ange omfånget till nivån `store` använder du:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> Om du vill ändra omfånget till butiksnivå kontaktar du din [!DNL Payment Services]-säljare.

När omfånget ändras rensas cachen så att ändringarna visas:

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## Konfigurera L2/L3-bearbetning

[!DNL Payment Services] kan bearbeta data på nivå 2 och nivå 3 från kortbetalningstransaktioner för att tillhandahålla ytterligare information för handlare.

>[!WARNING]
>
> Integrering med nivå 2 och nivå 3-bearbetning med PayPal är endast tillgängligt för handlare i USA. Mer information finns i [betalningshantering](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} i dokumentationen för PayPal-utvecklare.

Om du vill använda L2/L3-bearbetningsdata för [!DNL Payment Services], eller om du har några frågor, kan du kontakta din [!DNL Payment Services]-kontoansvarige.

Mer information om L2- och L3-bearbetning som används i [!DNL Payment Services] finns i [Nivå 2- och Nivå 3-bearbetning](levels-card-payment-transactions.md).
