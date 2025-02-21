---
title: Konfiguration av lagringsplats och mappningssystem
description: Konfigurera en distansleverantör som har stöd för mappning av lagringsplats i butikens gränssnitt. Butiksuppfyllelselösningarna kräver en distansleverantör för att möjliggöra butikssökning och andra mappnings- och schemaläggningsfunktioner för hela arbetsflödet.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# Lagringsplats och mappningsinställningar

Aktivera butikens plats och mappningsfunktioner för arkivuppfyllelse genom att konfigurera en [distansleverantör](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm) för att söka efter butiksplatser.

**Krav**

Under konfigurationsprocessen anger du en Google API-nyckel för Google Maps-plattformen. Om du inte har någon [genererar du en från Google Maps-plattformen](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps).

Så här konfigurerar du distansprovidern:

1. Lägg till Google Maps-integreringen för innehållstypen Karta från konfigurationen **[!UICONTROL Stores > General]** i Admin.

   - Gå till **[!UICONTROL Stores > Configuration  > General > Content Management]**.

   - Lägg till din Google API-nyckel i fältet **[!UICONTROL Google Maps API Key]**.

1. I konfigurationen **[!UICONTROL Stores > Inventory]** i Admin väljer du distansprovidern för arkivuppfyllelse.

   - Gå till **[!UICONTROL Stores > Configuration > Catalog > Inventory]**.

   - Expandera avsnittet **[!UICONTROL Distance Provider for Distance Based SSA]**.

   - Ange **Provider** till **Google Map**.

1. Konfigurera inställningar för **[!UICONTROL Google Distance Provider]**.

   - Lägg till din **Google API-nyckel**.

   - Ange **[!UICONTROL Computation Mode]** till `Driving` och **[!UICONTROL Value]** till `Distance`
