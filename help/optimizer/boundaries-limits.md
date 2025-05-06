---
title: Gränser och begränsningar
description: Lär dig mer om gränserna och gränserna för  [!DNL Adobe Commerce Optimizer] så att du kan vara säker på att det uppfyller behoven i din verksamhet.
role: Admin, Developer
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Gränser och begränsningar

>[!NOTE]
>
>Denna dokumentation beskriver gränserna och gränserna för utveckling av tidig åtkomst och återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

Följande innehåller gränser och begränsningar för Adobe Commerce Optimizer.

## Katalog

- Den garanterade andelen för katalogintaget är: 1 000 produkter/minut och 5 000 priser/minut
- Basantalet produktuppdateringar per dag är 1 000 000.
- Det totala antalet SKU:er som tillåts i en instans är 250 000. 
- Det högsta antalet scope är 50.
- Antalet varianter per produkt är 10 000.
- Produktstorleken får inte överstiga 200 kB.

## Priser

- Det högsta antalet prislistor är 1 000.

## Sökning och butik

- Antalet produkter som en enskild sökbegäran kan returnera är 100.
- Det högsta antalet filterbara attribut är 200
- Det högsta antalet sökbara attribut är 200
- Det maximala antalet sorterbara attribut är 50
- Det högsta antalet facets är 100. Alla facets måste vara filterbara attribut.
- Det högsta antalet alternativ som en enskild facet-katt returnerar är 100, vilket kan ökas per supportbegäran.

## Kanaler och policyer

- Det högsta antalet kanaler per klientorganisation är 1 000.
- Det högsta antalet profiler som tilldelats en kanal är 10.
- Det högsta antalet attributvärden som används i en princip är 100. 

## Produktupptäckt och rekommendationer

- För produktupptäckt stöds inte attributbaserad marknadsföring och prisinställningar.
- Rekommendationer:

   - [!DNL Adobe Commerce Optimizer] stöder rekommendationstypen _Senast visade_ för tidig åtkomst.
   - Det finns inget stöd för inkludering eller uteslutning av kategorier eller attribut.
   - Du kan inte förhandsgranska rekommendationer i [!DNL Adobe Commerce Optimizer].
