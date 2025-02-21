---
title: Förbättra prestanda vid export av SaaS-data
description: Lär dig hur du förbättrar SaaS-dataexportprestanda för Commerce Services genom att använda dataexportläge med flera trådar.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Förbättra prestanda vid export av SaaS-data

**Exportläge för flertrådsdata** snabbar upp exportprocessen genom att dela upp flödesuppgifter i grupper och bearbeta dem parallellt.

Utvecklare eller systemintegratörer kan förbättra prestanda genom att använda dataexportläget med flera trådar i stället för standardläget med en tråd. I entrådsläge finns det ingen parallellisering av feedbackprocessen. På grund av standardgränserna är dessutom alla klienter begränsade till att endast använda en tråd. I de flesta fall krävs ingen anpassning av konfigurationen.

## Att tänka på vid användning av flertrådsläge

När du arbetar med dataexporttjänster vill du optimera prestanda samtidigt som du ser till att synkroniseringen är korrekt.
Adobe rekommenderar att du använder standardkonfigurationen för datainhämtning, som vanligtvis uppfyller synkroniseringskraven för Commerce handlare. Det finns dock scenarier där anpassning kan snabba upp bearbetningstiden.

Tänk på följande när du bestämmer dig för om du vill anpassa dataexportkonfigurationen:

- **Inledande synkronisering**-Utvärdera antalet produkter och [beräkna datavolymen och överföringstiden](estimate-data-volume-sync-time.md) baserat på standardkonfigurationen. Fråga dig själv: Kan du vänta på den här initiala datasynkroniseringen när du har startat en Commerce-tjänst?

- **Lägger till nya butiksvyer eller webbplatser**-Om du planerar att lägga till butiksvyer eller webbplatser med samma produktantal efter att du publicerat, uppskattar du datavolymen och överföringstiden. Kontrollera om synkroniseringstiden är godkänd med standardkonfigurationen eller om flertrådsbearbetning är nödvändig.

- **Vanlig import** - Förutse vanlig import, t.ex. prisuppdateringar eller ändringar av lagerstatus. Utvärdera om uppdateringarna kan tillämpas inom en acceptabel tidsram eller om snabbare bearbetning behövs.

- **Produktvikt**-Fundera på om dina produkter är lätta eller tunga. Justera batchstorleken därefter om produktbeskrivningar eller attribut ökar produktstorleken.

Tänk på att noggrann planering, inklusive beräkning av datavolym och synkroniseringstid, ofta kan eliminera behovet av anpassning. Schemalägg foderintag baserat på dessa uppskattningar för att uppnå optimala resultat.

>[!NOTE]
>
>Adobe rekommenderar att du är försiktig när du använder flertrådsbearbetning. Funktionen är en funktion för tidig åtkomst som fortfarande förbättras. Om du konfigurerar flertrådning för snabbare prestanda kan du utlösa säkerhetsutkast för Adobe Commerce Services som ingår för att förhindra felanvändning av systemet vid dataöverföring. Dessa skyddsräcken hindrar även användare från att utlösa synkroniseringsändringar som kan överbelasta systemet. När skyddsräcken aktiveras blockeras förfrågningar och systemet returnerar 429 fel. Om du råkar ut för dessa fel justerar du konfigurationen och skickar in en supportanmälan för att få hjälp.

## Konfigurera multi-threading

Flertrådsläge stöds för alla [synkroniseringsmetoder](data-synchronization.md#synchronization-process): fullständig synkronisering, partiell synkronisering och objektsynkronisering med fel. Om du vill konfigurera flertrådning anger du antalet trådar och batchstorlek som ska användas under synkroniseringen.

- `thread-count` är antalet trådar som aktiveras för att bearbeta entiteter. Standardvärdet `thread-count` är `1`.
- `batch-size` är antalet entiteter som bearbetas i en iteration. Standardvärdet `batch-size` är `100` poster för alla feeds förutom prisfeeden. Standardvärdet för prisfeed är `500` poster.

Du kan konfigurera flertrådsteknik som ett tillfälligt alternativ när du kör ett omsynkroniseringskommando eller genom att lägga till flertrådskonfigurationen i Adobe Commerce-programkonfigurationen.

>[!NOTE]
>
>Se till att du justerar SaaS-dataexportens prestanda med den hastighetsgräns som har definierats för en kund på konsumentsidan.

### Konfigurera multi-threading vid körning

När du kör ett fullständigt synkroniseringskommando från kommandoraden anger du flertrådsbearbetning genom att lägga till alternativen `thread-count` och `batch-size` i CLI-kommandot.

```
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

De alternativ som anges på kommandoraden åsidosätter den dataexportkonfiguration som anges i Adobe Commerce-programfilen `config.php`.

### Lägga till flertrådning i Commerce-konfigurationen

Om du vill bearbeta alla dataexportåtgärder med hjälp av multi-threading kan systemintegratörer eller utvecklare ändra antalet trådar och batchstorleken för varje feed i Commerce-programkonfigurationen.

Dessa ändringar kan tillämpas genom att lägga till anpassade värden i [systemavsnittet](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system) i konfigurationsfilen, `app/etc/config.php`.

**Exempel: Konfigurera flertrådning för produkter och priser**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```
