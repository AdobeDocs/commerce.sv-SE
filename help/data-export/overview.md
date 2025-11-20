---
title: '[!DNL SaaS Data Export Guide]'
description: Lär dig hur du använder tillägget  [!DNL data export] för Adobe Commerce SaaS-tjänster som synkroniserar data mellan Adobe Commerce och anslutna Commerce-tjänster.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# [!DNL SaaS Data Export] Användarhandbok

[!DNL SaaS data export] synkroniserar data mellan en Adobe Commerce-instans och anslutna Commerce Services. När du lägger till Live Search, produktrekommendationer eller katalogtjänsten i en Adobe Commerce-installation installeras tillägget [!DNL Data export] automatiskt.

SaaS-dataexport samlar in och exporterar olika typer av data, som kallas _feeds_, som samlar in specifika typer av information. Beroende på vilka Commerce-tjänster som är installerade inkluderar dataexportflödena för SaaS:

- **Katalogentiteten skickar** sammanställda produktdata. Data omfattar produkter, produktattribut, produktpriser, produktvariationer, kategorier, kategoribehörigheter och produktbehörigheter.
- **Omfångsfeed** samlar in data för kundgrupper, webbplatser, butiker och butiksvyer.
- **Försäljningsorderfeeden** samlar in orderdata inklusive relaterade entiteter som fakturor, leveranser, kreditnotor och så vidare.
- **Multi-Source Inventory feed** samlar in data om lagerlagerlagerstatusartiklar.

SaaS-dataexport levereras som ett PHP-tillägg. Det har stöd för flera metoder för att initiera och hantera datasynkroniseringsprocessen.

- **Manuell synkronisering från administratören eller kommandoraden**

   - Kontrollpanelen [Datahantering](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) i Commerce Admin innehåller en grafisk vy över synkroniseringsstatusen. Du kan använda kontrollpanelen för att utföra en fullständig omsynkronisering (_fullständig synkronisering_) av alla feeds. Adobe rekommenderar dock att du bara utför en fullständig synkronisering första gången du ansluter Adobe Commerce till en Commerce-tjänst. Se [Synkroniseringsprocess](data-synchronization.md).

   - [Adobe Commerce kommandoradsverktyg](https://experienceleague.adobe.com/sv/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) innehåller kommandon för att synkronisera specifika flöden och ytterligare alternativ för att anpassa flödeshantering.

- **Automatisk synkronisering med cron-jobb**

   - [Partiell datasynkronisering](data-synchronization.md#partial-synchronization-with-cron-jobs) - Kroniska jobb utlöser en partiell datasynkronisering när en Commerce Admin-användare uppdaterar en entitet. Dataexportprocessen skickar endast dessa uppdateringar till anslutna Commerce-tjänster. Den partiella synkroniseringsprocessen baseras på MView-mekanismen och kräver inga åtgärder från Admin-användaren eller systemintegratorn.

   - [Automatiskt återförsök för synkroniseringsfel](data-synchronization.md#failed-items-sync-for-error-recovery) - Kroniska jobb utlöser automatiskt återförsök av synkroniseringsprocessen när fel uppstår under datasynkroniseringsprocessen.

- **Exportera schemaläggning och prestanda**

   - Utvecklare och systemintegratörer kan uppskatta hur lång tid SaaS-dataexporten tar att synkronisera data mellan Adobe Commerce och anslutna tjänster. Den här uppskattningen kan hjälpa till att schemalägga dataexportbearbetning för att förhindra platsavbrott. Se [Beräkna datavolym och överföringstid](estimate-data-volume-sync-time.md).

   - I de fall där synkroniseringen behöver ske snabbare, erbjuder SaaS-dataexport anpassade alternativ för att förbättra exportbearbetningens prestanda. Se [Förbättra dataexportprestanda](customize-export-processing.md).

- **Spåra och felsöka dataexportaktiviteter** - Använd data- och saas-export-loggar för att granska synkroniseringsstatus och feed-nyttolaster under synkroniserings- och indexeringsprocessen. Se [Loggning och felsökning](troubleshooting-logging.md).
