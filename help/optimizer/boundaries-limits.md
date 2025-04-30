---
title: Gränser och begränsningar
description: Lär dig mer om gränserna och gränserna för  [!DNL Adobe Commerce Optimizer] så att du kan vara säker på att det uppfyller behoven i din verksamhet.
role: Admin, Developer
source-git-commit: 45a43fe2ada206515c512a04aa6e9072e08844cc
workflow-type: tm+mt
source-wordcount: '335'
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

- Det högsta antalet prislistor är 30 000. Basskiktets antal prisböcker får inte överstiga 100 och bör följa regeln där (antalet prisböcker) x (antalet kanaler) måste vara mindre än eller lika med 100.
- Det garanterade priset för foderintag är 5000 poster per minut.
- En prispost får inte ha fler än 10 rabatter.
- Basantalet prisuppdateringar per dag är 5 000 000.

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

   - ACO har stöd för rekommendationstypen _Senast visade_ för EA
   - Det finns inget stöd för inkludering eller uteslutning av kategorier eller attribut.
   - Du kan inte förhandsgranska rekommendationer i [!DNL Adobe Commerce Optimizer].
