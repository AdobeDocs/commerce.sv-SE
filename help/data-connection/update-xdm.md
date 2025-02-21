---
title: Uppdatera händelsescheman för tidsserie för Commerce-datainmatning
description: Lär dig hur du skapar ett schema, en datauppsättning och en datastream för att samla in och skicka händelsedata från tidsserier för dataöverföring från Commerce.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Uppdatera händelsescheman för tidsserie för Commerce-datainmatning

Ett av [startstegen](overview.md#onboarding-steps) för att använda tillägget [!DNL Data Connection] är att få åtkomst till arbetsytan för datastream och [skapa ett datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) som är specifikt för Adobe Commerce. När du skapar den dataströmmen måste du också välja ett schema som beskriver de data som du planerar att importera. Schemat måste innehålla handelsspecifika fältgrupper.

I den här artikeln finns de fältgrupper som schemat måste innehålla för att följande tidsseriedata från Adobe Commerce-händelserna ska kunna samlas in:

- [Beteende](events.md) - Innehåller händelser för butiker, profiler, sökning och B2B.
- [Back office](events-backoffice.md) - Inkluderar orderstatus och profilevenemang.

Läs mer om [tidsseriedata](data-ingestion.md).

Läs mer om [grunderna för schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html).

## Uppdatera schema med tidsseriens beteendedata och händelsedata för back office

I det här avsnittet får du lära dig hur du uppdaterar ditt befintliga schema eller skapar ett schema som innehåller beteendedata och händelsedata för back office.

>[!NOTE]
>
>Information om hur du lägger till profilspecifika fält finns i [händelsedata för tidsserieprofiler](#time-series-profile-event-data).

1. Om du inte redan har ett schema [skapar](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) med klassen inställd på **Experience Event**.

1. [Lägg till](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) följande Commerce-specifika fältgrupper (eller redigera ditt befintliga schema och lägg till dessa fältgrupper):

   - Webbplatssökning
   - Besök webbsidan
   - Användarinloggningsprocess
   - Referensnycklar
   - Kontaktinformation, privat
   - Kanalinformation
   - Information om Commerce
   - Adobe Analytics ExperienceEvent Commerce (om du vill skicka data till Adobe Analytics)

   >[!NOTE]
   >
   > Ange inte några Commerce-specifika fältgrupper som `Primary identity`. När du gör det identifieras fältet som obligatoriskt och Experience Platform förväntar sig det fältet i varje händelse. Om det fältet saknas misslyckas dataimporten.

   Schemat innehåller nu Commerce-specifika fältgrupper så att tidsseriedata som samlats in från Commerce-händelserna [behavior](events.md) och [back office](events-backoffice.md) visas i schemat.

1. [Aktivera](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#profile) schemat för profilen.

   När ett schema är aktiverat för profilen, deltar alla datauppsättningar som skapats från det här schemat i Real-Time CDP, som sammanfogar data från olika källor för att skapa en fullständig bild av varje kund.

1. [Skapa en datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) baserat på schemat som du skapade eller uppdaterade.

   En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

1. [Skapa en datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) och markera schemat som innehåller de Commerce-specifika fältgrupperna och motsvarande datamängd.

   Datastream skickar insamlade data till datauppsättningen. Data representeras i datauppsättningen baserat på det valda schemat.

Med scheman, datauppsättningar och datastreams konfigurerade för beteendes- och back office-data kan du [konfigurera](connect-data.md#data-collection) din Commerce-instans för att samla in och skicka data till Experience Platform.

Om du vill inkludera din kunders profilinformation läser du [händelsedata för tidsserieprofiler](#time-series-profile-event-data).

## Händelsedata för tidsserieprofil

Händelsedata för tidsserieprofil genereras från följande händelser:

- [&quot;accountCreated&quot;](events-backoffice.md#accountcreated)
- [&quot;accountUpdated&quot;](events-backoffice.md#accountupdated)
- [&quot;accountDeleted&quot;](events-backoffice.md#accountdeleted)

Om du vill importera dina kunders profilhändelsedata till Experience Platform kan du uppdatera ditt befintliga Commerce-schema och använda samma dataström som redan konfigurerats, eller skapa ett profilspecifikt dataström och schema. Det beslutet baseras på företagets datastyrning. De följande två avsnitten leder dig genom båda fallen.

### Skicka händelsedata för tidsserieprofiler till Experience Platform med ditt befintliga datastream

Om du vill lägga till tidsseriens [händelsedata för serverprofil](events-backoffice.md#customer-profile-events-server-side) i ditt befintliga Commerce-datastam lägger du till fältgruppen `Demographic Details` i ditt schema. Schemat innehåller nu följande Commerce-specifika fältgrupper:

- Webbplatssökning
- Besök webbsidan
- Användarinloggningsprocess
- Referensnycklar
- Kontaktinformation, privat
- Kanalinformation
- Information om Commerce
- Adobe Analytics ExperienceEvent Commerce (om du vill skicka data till Adobe Analytics)
- Nytt: **Demografisk information**

När fältgruppen `Demographic Details` har lagts till i ditt befintliga Commerce-schema används den datamängd och datastream som redan är associerad med ditt Commerce-schema för den här tidsseriens profildata.

### Skicka händelsedata för tidsserieprofiler till Experience Platform i ett separat datastream

Om du vill lägga till [data för profilevenemang på serversidan](events-backoffice.md#customer-profile-events-server-side) i ett nytt profilspecifikt datastream och schema utför du följande steg.

1. [Skapa](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) ett schema och ställ in klassen på **Experience Event**.

1. [Lägg till](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) följande profilspecifika fältgrupper:

   - Demografiska detaljer
   - Kontaktinformation, privat
   - Kanalinformation
   - Information om Commerce

1. [Aktivera](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#profile) schemat för profilen.

   När ett schema är aktiverat för profilen, deltar alla datauppsättningar som skapats från det här schemat i Real-Time CDP, som sammanfogar data från olika källor för att skapa en fullständig bild av varje kund.

1. [Skapa en datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) baserat på det schema du skapade.

   En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

1. [Skapa en datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) och välj det XDM-schema som innehåller de Commerce-specifika fältgrupperna och motsvarande datamängd.

   Datastream skickar insamlade data till datauppsättningen. Data representeras i datauppsättningen baserat på det valda schemat.

Med scheman, datauppsättningar och datastreams konfigurerade för kundprofildata kan du [konfigurera](connect-data.md#data-collection) din Commerce-instans för att samla in och skicka data till Experience Platform.

Mer information om hur du skapar ett schema, en datauppsättning och ett dataflöde för profilpostdata finns i [skicka profilpostdata till Experience Platform](profile-data.md).
