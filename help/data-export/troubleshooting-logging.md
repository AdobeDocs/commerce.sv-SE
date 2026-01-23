---
title: Granska loggar och felsök
description: Lär dig hur du felsöker [!DNL data export] fel med hjälp av loggarna för dataexport och saas-export.
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
source-git-commit: a1afed7b635a2b05c5c0e0d1c9bf4a07fc5eef31
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# Granska loggar och felsök

Tillägget [!DNL data export] innehåller loggar för att spåra datainsamling och synkroniseringsprocesser.

## Loggar

Loggar är tillgängliga i katalogen `var/log` på Commerce programserver.

| loggnamn | filnamn | description |
|-----------------| ----------| -------------|
| SaaS dataexportlogg | `commerce-data-export.log` | Tillhandahåller information om dataexportaktiviteter, som entitetshändelser och fullständiga omsynkroniseringsutlösare.  Varje loggpost har en särskild struktur och innehåller information om feed, operation, status, förfluten tid, process-id och anroparen. |
| fellogg för SaaS-dataexport | `data-export-errors.log` | Visar felmeddelanden och stackspårningar för fel som inträffar under datasynkroniseringsprocessen. |
| SaaS-exportlogg | `saas-export.log` | Tillhandahåller information om data som skickas till Commerce SaaS-tjänster. |
| SaaS-exportfellogg | `saas-export-errors.log` | Innehåller information om fel som inträffar när data skickas till Commerce SaaS-tjänster. |

Om du inte ser förväntade data för en Adobe Commerce-tjänst använder du felloggarna för dataexporttillägget för att avgöra var problemet uppstod. Du kan också utöka loggar med ytterligare data för spårning och felsökning. Se [Utökad loggning](#extended-logging).

### Loggformat

Varje loggpost har följande struktur.

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elapsed from script run>",
   "pid": "<process id that executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>Den JSON-baserade strängen är vacker för bättre läsbarhet.

I följande tabell beskrivs de åtgärdstyper som kan registreras i loggarna.

| Åtgärd | Beskrivning | Exempel på anropare |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| fullständig synkronisering | Samlar in och skickar alla data till SaaS för en given feed. | `bin/magento saas:resync --feed=products` |
| partiell omindexering | Samlar in och skickar data till SaaS endast för uppdaterade enheter i en given feed. Den här loggen finns bara om det finns uppdaterade entiteter. | `bin/magento cron:run --group=index` |
| försök igen med misslyckade objekt | Skicka om objekt för en viss feed till SaaS om den tidigare synkroniseringsåtgärden misslyckades på grund av ett Commerce-program eller serverfel. Den här loggen finns bara om det finns misslyckade objekt. | `bin/magento cron:run --group=saas_data_exporter` (alla cron-grupper av typen &quot;*_data_exporter&quot;) |
| fullständig synkronisering (äldre) | Samlar in och skickar alla data till SaaS för en given feed i äldre exportläge. | `bin/magento saas:resync --feed=categories` |
| partiell omindexering (äldre) | Skickar uppdaterade entiteter till SaaS för en given feed i äldre exportläge. Den här loggen finns bara om det finns uppdaterade entiteter. | `bin/magento cron:run --group=index` |
| partiell synkronisering (äldre) | Skickar uppdaterade entiteter till SaaS för en given feed i äldre exportläge. Den här loggen finns bara om det finns uppdaterade entiteter. | `bin/magento cron:run --group=saas_data_exporter` (alla cron-grupper av typen &quot;*_data_exporter&quot;) |


### Exempel på loggning

Under en fullständig omsynkronisering spåras förloppet och loggas var 30:e sekund som standard. Här är ett exempel på en loggpost.

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

I det här exemplet innehåller värdena `status` information om synkroniseringsåtgärden:

- **`"Progress 2/5"`** anger att 2 av 5 iterationer har slutförts. Antalet iterationer beror på antalet exporterade enheter.
- **`"processed: 200"`** anger att 200 objekt har bearbetats.
- **`"synced: 100"`** anger att 100 objekt skickades till SaaS. `"synced"` förväntas inte vara lika med `"processed"`. Här är ett exempel:
   - **`"synced" < "processed"`** betyder att flödestabellen inte upptäckte några ändringar i objektet jämfört med den tidigare synkroniserade versionen. Sådana objekt ignoreras under synkroniseringsåtgärden.
   - **`"synced" > "processed"`** samma enhets-ID (till exempel `Product ID`) kan ha flera värden i olika omfång. En produkt kan till exempel tilldelas fem webbplatser. I det här fallet kan du ha&quot;1 bearbetat&quot; objekt och&quot;5 synkroniserade&quot; objekt.

+++ **Exempel: Fullständig omsynkroniseringslogg för prisfeed**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## Visa och felsöka loggar med New Relic

Om du lagrar Adobe Commerce-loggar i New Relic kan du lägga till tolkningsregler för att förbättra läsbarheten och frågeupplevelsen.

1. Logga in på New Relic.

1. Gå till `Logs => Parsing`.

1. Klicka på `Create parsing rule`.

1. Konfigurera tolkningsregeln genom att lägga till följande värden.

   - **Filterloggar baserade på NRQL**

     `filePath LIKE '%commerce-data-export%.log'`

   - **Analysregel**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel}: %{GREEDYDATA:feed:json}`

I det här exemplet läggs en regel till som gör att du kan söka efter New Relic-loggar efter en viss flödestyp, åtgärd o.s.v.

**Exempelfrågesträng**—`feed.feed:"products" and feed.status:"Complete"`

## Felsökning

Om data saknas eller är felaktiga i Commerce Services bör du kontrollera om loggarna innehåller meddelanden om fel som uppstod under synkroniseringen från Adobe Commerce till Commerce Services-plattformen. Använd vid behov utökad loggning för att lägga till ytterligare information i loggarna för felsökning.

- Felloggen för dataexport (`commerce-data-export-errors.log`) fångar upp fel som inträffar under insamlingsfasen.
- SaaS-exportfelloggen (`saas-export-errors.log`) fångar upp fel som inträffar under överföringsfasen.

Om du ser fel som inte är relaterade till konfiguration eller tillägg från tredje part skickar du en [supportanmälan](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) med så mycket information som möjligt.

### Lös problem med katalogsynkronisering {#resolvesync}

När du utlöser en omsynkronisering av data kan det ta upp till en timme innan data uppdateras och återspeglas i gränssnittskomponenter som livesökning och rekommendationsenheter. Om du fortfarande ser avvikelser mellan din katalog och data i Commerce Store, eller om katalogsynkroniseringen misslyckades, se följande:

#### Datamatchningsavvikelse

1. Visa detaljerad vy för produkten i fråga i sökresultaten.
1. Kopiera JSON-utdata och verifiera att innehållet matchar det du har i [!DNL Commerce]-katalogen.
1. Om innehållet inte stämmer överens gör du en mindre ändring i produkten i katalogen, till exempel lägger till ett mellanslag eller en punkt.
1. Vänta på en omsynkronisering eller [utlöser en manuell omsynkronisering](#resync).

#### Synkronisering körs inte

Om synkroniseringen inte körs enligt ett schema eller inget synkroniseras, se den här [KnowledgeBase](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce)-artikeln.

#### Synkroniseringen misslyckades

Om katalogsynkroniseringen har statusen **Misslyckades** skickar du en [supportanmälan](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

## Utökad loggning

Använd miljövariabler för att utöka loggar med ytterligare data för spårning och felsökning. Lägg till miljövariabeln på kommandoraden när du kör CLI-kommandon för dataexport enligt följande exempel.

### Kontrollera flödets nyttolast

Inkludera flödets nyttolast i SaaS-exportloggen genom att lägga till miljövariabeln `EXPORTER_EXTENDED_LOG=1` när du synkroniserar om flödet.

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

När åtgärden har slutförts är flödets nyttolast tillgänglig för granskning i SaaS-exportloggen (`var/.log/saas-export.log`).

### Bevara nyttolast i feed-indexregistret

För dataexporttillägget Commerce SaaS (`magento/module-data-exporter`) 103.3.0 och senare behåller direktexportflöden endast de data som krävs i indextabellen. I flödena ingår alla katalog- och lagerstatusflöden.

Att bevara nyttolastdata i indextabellen rekommenderas inte i produktionsmiljöer, men det kan vara användbart i en utvecklarmiljö. Inkludera flödets nyttolast i indexet genom att lägga till miljövariabeln `PERSIST_EXPORTED_FEED=1` när du synkroniserar om flödet.

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### Kör profileraren för att felsöka långsamma prestanda

Om omindexeringsprocessen för ett specifikt flöde tar en orimlig tid, kör du profileraren för att samla in ytterligare data som kan vara användbara för supportteamet.

Kör profileraren genom att lägga till miljövariabeln `EXPORTER_PROFILER=1` när du kör kommandot reindex.

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

Profileringsdata lagras i dataexportloggen (`var/log/commerce-data-export.log`) i följande format:

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
