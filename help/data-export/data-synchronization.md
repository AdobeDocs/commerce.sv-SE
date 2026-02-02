---
title: Synkronisera data med SaaS-dataexport
description: Lär dig hur  [!DNL SaaS Data Export] samlar in och synkroniserar data mellan Adobe Commerce-instanser och anslutna SaaS-tjänster.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: ea425b56fe7afd9bdaa813d040ac9e47b7022908
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# Synkronisera data med SaaS-dataexport

När du installerar en Commerce-tjänst som kräver dataexport, t.ex. katalogtjänsten, Live Search eller Produktrekommendationer, installeras en samling Saas-moduler för dataexport för att hantera datainsamling och synkroniseringsprocessen.

SaaS-dataexport flyttar kontinuerligt produktdata från en Adobe Commerce-instans till Commerce Services-plattformen för att hålla informationen uppdaterad. Produktrekommendationer kräver till exempel aktuell kataloginformation för att korrekt kunna returnera rekommendationer med rätt namn, pris och tillgänglighet. Använd [Instrumentpanelen för datahantering](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) för att observera och hantera synkroniseringsprocessen, eller kommandoradsgränssnittet för att utlösa en synkronisering och indexera om produktdata för användning i Commerce Services.

I följande diagram visas dataexportflödet i SaaS.

![Samling och synkronisering av SaaS-dataexport för Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

De viktigaste komponenterna i SaaS dataexportflöde är:

- SaaS-moduler för dataexport som samlar in data för flöden från Adobe Commerce, samlar ihop flödesobjekt, lyssnar efter uppdateringar och behåller feedstatus.
- SaaS exporterar moduler som exporterar data, konfigurerar routning och publicerar flöden till anslutna tjänster.
- Adobe Commerce-tjänsten hanterar dataöverföringsprocessen för att validera inkommande flöden och bevarar uppdateringar av anslutna tjänster.

>[!NOTE]
>
>För att säkerställa smidig schemaläggning och undvika avbrott i webbplatsåtgärder rekommenderar Adobe att du beräknar datavolym och synkroniseringstid innan du startar synkroniseringen av dataflöden. Denna uppskattning är viktig när du planerar för inledande synkroniseringar eller storskaliga kataloguppdateringar, till exempel massprisförändringar. Mer information finns i [Beräkna datavolym och överföringstid för datasynkronisering](estimate-data-volume-sync-time.md)

## Synkroniseringslägen

SaaS-dataexport har två lägen för att bearbeta enhetsflöden:

- **Omedelbart exportläge** - I det här läget samlas data in och skickas direkt till Commerce-tjänsten i en enda iteration. Det här läget snabbar upp leveransen av entitetsuppdateringar till Commerce-tjänsten och minskar lagringsstorleken för flödestabellerna.

- **Äldre exportläge** - I det här läget samlas data in i en enda process. Sedan skickar ett cron-jobb insamlade data till de anslutna handelstjänsterna. I loggposter för dataexport får feeds som använder det äldre läget etiketten `(legacy)`.

## Synkroniseringstyper

SaaS-dataexport har stöd för tre synkroniseringstyper: fullständig synkronisering, partiell synkronisering och återförsök med objektsynkronisering.

### Fullständig synkronisering

När du har anslutit en Adobe Commerce-instans till Commerce Service utför du en fullständig synkronisering för att skicka entitetsmatningsdata från Adobe Commerce till den anslutna tjänsten.

>[!NOTE]
>
>Fullständig synkronisering gäller främst för introduktionsfasen. Undvik regelbunden användning för att förhindra databasöverbelastning. Efter den inledande synkroniseringen synkroniseras pågående ändringar automatiskt med partiell synkronisering.

### Delvis synkronisering

Med partiell synkronisering skickar SaaS-dataexport automatiskt uppdateringar från Commerce-programmet, till exempel produktnamnsändringar eller prisuppdateringar, till anslutna handelstjänster.

I dataexportprocessen används följande cron-jobb för att automatisera den partiella synkroniseringsåtgärden.

- &quot;index&quot; cron group-jobb:
   - Jobbet `indexer_reindex_all_invalid` indexerar om alla ogiltiga feeds. Det är ett vanligt Adobe Commerce cron-jobb.
   - Jobbet `saas_data_exporter` gäller för tidigare exportfeeds.
   - Jobbet `sales_data_exporter` är specifikt för exportflödet med försäljningsdata.

Dessa jobb utförs varje minut.

För att partiell synkronisering ska fungera krävs följande konfiguration för Commerce-programmet:

- [Schemaläggning av aktivitet har aktiverats via cron-jobb](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- Alla SaaS-dataexportindexerare har konfigurerats i `Update by Schedule`-läge.

  I SaaS-dataexportversion 103.1.0 och senare är läget `Update by Schedule` aktiverat som standard. Du kan verifiera indexkonfigurationen på servern med Commerce CLI-kommandot `bin/magento indexer:show-mode | grep -i feed`

### Försök synkronisera misslyckade objekt igen

Synkroniseringen av objekt som misslyckats med försök använder en separat process för att skicka om objekt som inte kunde synkroniseras på grund av fel under synkroniseringsprocessen, till exempel ett programfel, nätverksavbrott eller ett SaaS-tjänstfel. Implementeringen för den här synkroniseringen baseras också på cron-jobb.

- `resync_failed_feeds_data_exporter` cron-gruppjobb:
   - Jobbet `<feed name>_feed_resend_failed_feeds_items` skickar om objekt som inte kunde synkroniseras, till exempel `products_feed_resend_failed_items`.

### Visa och hantera synkroniseringsprocessen

De flesta synkroniseringsaktiviteter bearbetas automatiskt baserat på programkonfigurationen. SaaS-dataexport innehåller dock även verktyg för att övervaka och hantera processen.

- [!BADGE PIAs only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."} **[Kontrollpanel för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** - Administratörsanvändare kan visa och spåra data som synkroniserats med Commerce Services och som är tillgängliga för butikstjänster.

- [!BADGE Endast SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller för Adobe Commerce-projekt som är integrerade med Adobe Commerce Optimizer (SaaS-infrastruktur som hanteras av Adobe)."} **[Datasynkroniseringssida](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)** - För Commerce-projekt som använder [!DNL Adobe Commerce Optimizer] kontrollerar du tillgängligheten för katalogdata för butiken från datasynkroniseringssidan i Adobe Commerce Optimizer.

### Verifiera Commerce programkonfiguration

Delvis synkronisering och Försök igen misslyckades. Objekten synkroniseras bara om Commerce-instansen har konfigurerats korrekt. Konfigurationen slutförs vanligtvis när du konfigurerar Commerce-tjänsten. Kontrollera följande konfiguration om dataexporten inte fungerar som den ska.

- [Bekräfta att seriejobben körs](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Verifiera att indexerarna körs från [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) eller genom att använda Commerce CLI-kommandot `bin/magento indexer:info`.

- Kontrollera att indexerarna för följande feeds är inställda på `Update by Schedule`: Katalogattribut, Produkt, Produktåsidosättningar och Produktvariant. Du kan kontrollera indexerare från [Indexhantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) i Admin eller med CLI (`bin/magento indexer:show-mode | grep -i feed`).

### Meddelanden från händelsehanteraren om dataöverföringsloggning

I version 103.3.4 och senare skickar SaaS-dataexport händelsen `data_sent_outside` när data skickas från Commerce-instansen till Adobe Commerce-tjänster.

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>Mer information om händelser och hur du prenumererar på dem finns i [Händelser och observatörer](https://developer.adobe.com/commerce/php/development/components/events-and-observers) i dokumentationen för Adobe Commerce Developer.
