---
title: Beräkna datavolym och överföringstid
description: Lär dig att uppskatta datavolymen och överföringstiden som krävs för verktyget  [!DNL data export] för att synkronisera feed-data mellan Adobe Commerce och anslutna tjänster.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Beräkna datavolym och överföringstid för datasynkronisering

Adobe rekommenderar att du beräknar datavolym och synkroniseringstid innan du startar synkroniseringen av dataflöden, så att du får en smidig schemaläggning och slipper avbrott i webbplatsdriften. Denna uppskattning är viktig när du planerar för inledande synkroniseringar eller storskaliga kataloguppdateringar, till exempel massprisförändringar.

Som standard bearbetar dataexportverktyget data i entrådsläge med en standardbatchstorlek. Med standardkonfigurationen finns det ingen parallellisering av feedbackprocessen. Dessutom accepterar den här komponenten begäranden per sekund (RPS) som innebär följande:

- Upp till 10 000 produkter per minut där en produkt är en SKU med attribut i en viss affisch
- Upp till 50 000 priser per minut

Följande faktorer påverkar dataöverföringstiden under synkroniseringen.

- Antal trådar är 1 (som standard)
- Batchstorleken är inställd på _100_ för alla feeds utom för `prices`-feeden, där den är inställd på _500_.
- Mottagningsfrekvensen för feed är 2 begäranden per sekund.
- Alla produkter tilldelas alla befintliga webbplatser
- För prisberäkningsscenarierna har alla produkter tilldelats särskilda och grupperade priser


## Beräkna dataöverföring per feed

Använd värdena och formlerna i följande tabell för att beräkna datavolymen och synkroniseringstiden för varje datafeed.

>[!NOTE]
>
>Dessa beräkningar baseras på en överföringshastighet på 2 begäranden per sekund. Hastigheten baseras på den tid som krävs för datainsamling och datainlämning. Den faktiska överföringshastigheten varierar beroende på nyttolastens storlek och den aktuella belastningen på Commerce programserver.

| Feed | Exempel på data | Formel att beräkna poster | Antal förväntade begäranden | Förväntad omsynkroniseringstid |
| --- | --- | --- | --- | --- |
| Produkter | Produkter (P): 10000, Store Views (SV): 4 | P * SV = 40000 | 40000 / Batchstorlek (100) = 400 begäranden | (400 begäranden * 0,5 sekunder per begäran) / 60 = 3,3 minuter |
| Kategorier | Kategorier (C): 500, Store Views (SV): 4 | C * SV = 2000 | 2000 / Batchstorlek (100) = 20 begäranden | (20 begäranden * 0,5 sekunder per begäran) / 60 = 0,1 minuter (4 sekunder) |
| Priser | Produkter (P): 10000, kundgrupper (CG): 6 (t.ex. unikt pris i delad katalog), webbplatser (WS): 2 | P \* WS * CG = 120000 | 120000 / Batchstorlek (500) = 240 begäranden | (240 begäranden * 0,5 sekunder per begäran) / 60 = 2 minuter |
| Produktåsidosättningar | Produkter med behörigheter eller i delad katalog (P): 10000, Berörda kundgrupper: 5, Tilldelade webbplatser WS: 2 | P \* WS * CG = 100000 | 100000 / Gruppstorlek (100) = 1000 begäranden | (1000 begäranden * 0,5 sekunder per begäran) / 60 = 8,3 minuter |
| Produktvarianter | Varianter (underordnade produkter) som tilldelas konfigurerbara produkter (PV): 100000 | PV = 100000 | 100000 / Gruppstorlek (100) = 1000 begäranden | (1000 begäranden * 0,5 sekunder per begäran) / 60 = 8,3 minuter |
| Kategoribehörigheter | Antal alla kategoribehörigheter + 4 reservposter (CP): 10000 | CP = 10000 | 10000 / Gruppstorlek (100) = 100 begäranden | (100 begäranden * 0,5 sekunder per begäran) / 60 = 0,8 minuter (50 sekunder) |
| Lagerstatus | Produkter (P): 10000, Stock-produkter tilldelade till (S): 5 (förutsatt att varje produkt tilldelas varje lager) | P * S = 50000 | 50000 / Gruppstorlek (100) = 500 begäranden | (500 begäranden * 0,5 sekunder per begäran) / 60 = 4,2 minuter |
| Försäljningsorder | Alla orderposter (inklusive fakturor, leveranser och så vidare) (SO): 10000 | SO = 10000 | 10000 / Gruppstorlek (100) = 100 begäranden | (100 begäranden * 0,5 sekunder per begäran) / 60 = 0,8 minuter (50 sekunder) |
