---
title: Typer av Commerce-data
description: Lär dig vilka typer av data du kan samla in och skicka till Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Typer av Commerce-data

[Dataanslutningstillägget](overview.md) ansluter dina Commerce-data till Experience Platform. Data som är avsedda att användas i Experience Platform är grupperade i två beteendetyper: tidsseriedata, som tillhör klassen **Experience Event**, och registerdata, som tillhör klassen **Individual Profile** .

Läs mer om [databeteende](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=sv-SE#data-behaviors) och [klasser](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=sv-SE#class) i Experience Platform.

## Tidsseriedata

Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av en registrerade. När en kund t.ex. besöker en produkt på er webbplats läggs en produkt till i kundvagnen, en beställning osv. Tidsseriedata hämtas in till Experience Platform med ett schema som har klassen inställd på **Experience Event**.

### Insamlade tidsseriedata

Se [beteendehändelser](events.md) och [back office-händelser](events-backoffice.md) om du vill veta vilka data som hämtas när en tidsseriehändelse genereras.

### Schema krävs för att importera tidsseriens händelsedata

Lär dig hur du [skapar ett schema](update-xdm.md) som kan importera händelsedata för beteende- och backoffice-tidsserier.

## Registrera data

Postdata innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ. En kund på er webbplats skapar till exempel ett konto som genererar postdata. Dessa data importeras till Experience Platform med ett schema som har klassen inställd på **Individual Profile**. Du kan skicka postdata till Adobe profilhanterings- och segmenteringstjänst: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE).

### Insamlade profilpostdata

Information om vilka data som hämtas när en profilpost genereras finns i [postdata för kundprofil](events-profilerecord.md).

### Schema krävs för att importera profilpostdata

Lär dig hur du [skapar ett schema](profile-data.md) som kan importera profilpostdata.
