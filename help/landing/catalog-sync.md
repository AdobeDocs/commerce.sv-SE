---
title: Katalogsynkronisering
description: Lär dig hur du exporterar produktdata från  [!DNL Commerce] servern till [!DNL Commerce Services].
feature: Catalog Management, Data Import/Export, Catalog Service
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Katalogsynkronisering

>[!NOTE]
>
> Kontrollpanelen för katalogsynkronisering är nu Dashboard för datahantering. Den nya instrumentpanelen har nu stöd för [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+, [[!DNL Live Search]](../live-search/overview.md) v4.1.0+ och [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+. Kunderna kan hämta Dashboard för datahantering genom att uppdatera till den senaste versionen av någon av dessa tjänster. Läs mer om det i dokumentationen för [Dashboard för datahantering](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=sv-SE). Det här avsnittet gäller även för användare som ännu inte har uppgraderat och fortfarande har kontrollpanelen för katalogsynkronisering.

Adobe Commerce använder indexerare för att kompilera katalogdata till tabeller. Processen aktiveras automatiskt av [händelser](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html?lang=sv-SE#events-that-trigger-full-reindexing), till exempel en ändring av ett produktpris eller lagernivå.

Katalogsynkroniseringstjänsten flyttar fortlöpande produktdata från en [!DNL Adobe Commerce]-instans till [!DNL Commerce Services]-plattformen för att hålla informationen uppdaterad. [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) kräver till exempel aktuell kataloginformation för att kunna returnera rekommendationer med korrekta namn, priser och tillgänglighet. Använd kontrollpanelen _Katalogsynkronisering_ för att observera och hantera synkroniseringsprocessen eller kommandoradsgränssnittet för att utlösa en katalogsynkronisering och för att indexera om produktdata för användning av [!DNL Commerce Services]. Se [Referens för kommandoradsgränssnitt](../data-export/data-export-cli-commands.md) i _Exporthandboken för SaaS-data_.

## Åtkomst till kontrollpanelen för katalogsynkronisering

Om du vill komma åt kontrollpanelen Katalogsynkronisering väljer du **System** > _Dataöverföring_ > **Katalogsynkronisering**.

Med kontrollpanelen **Katalogsynkronisering** kan du:

- Visa synkroniseringsstatus (**Pågår**, **Slutfört**, **Misslyckades**)
- Visa det totala antalet synkroniserade produkter
- Sök efter synkroniserade produkter för att visa deras aktuella tillstånd
- Sök i butikskatalog efter namn, SKU, osv.
- Visa synkroniserad produktinformation i JSON för att hjälpa till att diagnostisera en synkroniseringsdiskrepans
- Starta om synkroniseringsprocessen

### Senaste synkronisering

Rapporterar synkroniseringsstatus för:

- **Slutfört** - Visar datum och tid då synkroniseringen slutfördes och antalet produkter som uppdaterades
- **Misslyckades** - Visar datum och tid då synkroniseringsförsöket gjordes
- **Pågår** - Visar datum och tid för den senaste lyckade synkroniseringen

Katalogsynkroniseringsprocessen körs automatiskt varje timme. Om du inte ser förväntade produkter i butiken, eller om produkterna inte återspeglar de senaste ändringarna du gjort, kan du lösa [katalogsynkroniseringsproblem](#resolvesync).

### Synkroniserade produkter

Visar det totala antalet produkter som synkroniseras från din [!DNL Commerce]-katalog. Efter den första synkroniseringen bör endast ändrade produkter synkroniseras.

## Synkronisera igen {#resync}

Om du måste initiera en omsynkronisering av katalogen innan den schemalagda timsynkroniseringen inträffar, kan du tvinga fram en omsynkronisering.

>[!NOTE]
>
> Om du tvingar en omsynkronisering utlöses en omsynkronisering av hela produktkatalogen, vilket kan öka belastningen på maskinvaruresurserna.

1. Välj **Inställningar** på kontrollpanelen _Katalogsynkronisering_.

   Sidan _Katalogsynkroniseringsinställningar_ visas.

1. Klicka på [!UICONTROL Resync] i avsnittet _Synkronisera om data_.

   [!DNL Commerce] synkroniserar katalogen under nästa schemalagda synkroniseringsfönster. Beroende på storleken på katalogen kan den här åtgärden ta lång tid.

## Synkroniserade katalogprodukter

Följande information visas i tabellen **Synkroniserade katalogprodukter**.

| Fält | Beskrivning |
|---|---|
| ID | Unik identifierare för produkten |
| Namn | Produktens butiksnamn |
| Typ | Identifierar produkttypen, till exempel enkel, konfigurerbar eller nedladdningsbar |
| Senast exporterad | Datum när produkten senast exporterades från katalogen |
| Senast ändrad | Datum när produkten senast ändrades i katalogen |
| SKU | Visar produktens lagerställeenhet |
| Pris | Produktpris |
| Synlighet | En produkts synlighetsinställning enligt definitionen i katalogen [!DNL Commerce] |

## Lös problem med katalogsynkronisering {#resolvesync}

Se [Loggar och felsökning](../data-export/troubleshooting-logging.md#troubleshooting) i _Exportguiden för SaaS-data_.
