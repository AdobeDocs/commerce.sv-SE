---
title: Datasynkronisering
description: Granska katalogdata som synkroniseras från din Commerce-datakälla till  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
source-git-commit: e2c3c8a225b2c56985ba48c7efc9ae2c2d059b2e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Datasynkronisering

På sidan **Datasynkronisering** visas en översikt över synkroniseringsstatusen för produktdata som överförts från din datakälla (din befintliga Commerce-katalog, PIM-system, ERP-system (Enterprise Resource Planning) och så vidare) till [!DNL Adobe Commerce Optimizer].

Sidan **Datasynkronisering** ger värdefulla insikter om tillgängligheten av produktdata för din butik, så att den snabbt kan visas för dina kunder.

Sidan **Datasynkronisering** finns på *Inställningar* > **Datasynkronisering**.

![Datasynkronisering](../assets/data-sync.png)

Sidan **Datasynkronisering** innehåller följande fält:

| Fält | Beskrivning |
|--- |--- |
| Katalogkälla | Specifik språkinställning för synkroniserade data. |
| [!DNL Catalog Service] | Visar den senaste synkroniseringsuppdateringen, det totala antalet mottagna produkter, ett sökfält och en tabell över synkroniserade produkter för [!DNL Catalog Service]. |
| Produktidentifiering | Visar den senaste synkroniseringsuppdateringen, det totala antalet mottagna produkter, ett sökfält och en tabell över synkroniserade produkter för sökning. |
| Rekommendationer | Visar den senaste synkroniseringsuppdateringen, det totala antalet mottagna produkter, ett sökfält och en tabell över synkroniserade produkter för rekommendationer. |
| Produkter som tagits emot under de senaste tre timmarna | Visar antalet produkter som har överförts från katalogkällan till Adobe Commerce Optimizer under de senaste tre timmarna. Om du gör ovanliga uppdateringar av katalogen är det här värdet ofta noll. |
| Totalt antal produkter i katalog | Återger det totala antalet katalogprodukter som är tillgängliga för Adobe Commerce Optimizer. |
| Synkroniserade produkter | Innehåller information om de produkter som synkroniseras med Adobe Commerce Optimizer. Som standard sorteras den här tabellen efter&quot;Senast uppdaterad&quot;. Om du vill hitta en viss produkt använder du fältet **[!UICONTROL Search by Name or SKU]**. |

## Lista över synkroniserade produkter

Om du vill visa information om en synkroniserad produkt i JSON-format klickar du på kodikonen ![Kodlänken](../assets/data-sync-details.png) på produktraden i tabellen med synkroniserade produkter.

![Synkroniserad produktinformation](../assets/synced-products.png)

## Synkronisera om katalogdata

Om du inte ser specifika produkter på sidan **Datasynkronisering** måste du initiera en omsynkronisering från det överordnade systemet. Tänk dock på att en omsynkronisering kan öka belastningen på maskinvaruresurserna. Du kan dock behöva synkronisera om katalogen i följande scenarier:

- När du gör stora ändringar i produktkatalogen, till exempel lägger till nya produkter, uppdaterar produktinformation eller ändrar kategorier

- Om du märker några avvikelser eller prestandaproblem när du visar produktdata i dina butiker

>[!IMPORTANT]
>
>Den tid det tar att slutföra synkroniseringen varierar beroende på katalogstorleken och den datamängd som har uppdaterats.

## Övervaka datasynkroniseringsstatus

För projekt som använder Adobe Commerce som den överordnade datakällan kan du övervaka dataexportprocessen och initiera omsynkroniseringsåtgärder från statussidan [Synkronisering av dataflöden](../../data-export/data-synchronization.md) i Commerce Admin.

