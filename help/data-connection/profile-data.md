---
title: Uppdatera profilpostschema för Commerce datainmatning
description: Lär dig hur du skapar ett schema, en datauppsättning och en datastream för att samla in och skicka data från Commerce profilposter till Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Uppdatera profilpostschema för Commerce datainmatning

När era kunder skapar en profil på er Commerce-webbplats skapas en profilpost och data hämtas. Du måste skapa ett schema och en datauppsättning som är specifik för den profilposten innan du kan strömma profildata till Experience Platform.

1. [Skapa](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/ui/resources/schemas) ett schema och ställ in klassen på **Individual Profile**.

1. [Lägg till](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/ui/resources/schemas) följande profilspecifika fältgrupper:

   - identityMap
   - Demografiska detaljer
   - Kontaktinformation, privat
   - Information om användarkonto

1. [Aktivera](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/ui/resources/schemas) schemat för profilen.

   När ett schema är aktiverat för profilen, deltar alla datauppsättningar som skapats från det här schemat i Real-Time CDP, som sammanfogar data från olika källor för att skapa en fullständig bild av varje kund.

1. [Skapa en datauppsättning](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform) baserat på det schema du skapade eller uppdaterade.

   En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

1. Skapa ett [anpassat namnutrymme](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/namespaces#create-namespaces) i Experience Platform med följande värden:

   - **Visningsnamn**: _Commerce kund-ID_
   - **Identitetssymbol**: _CustomerId_
   - **Typ**: _Individuellt ID för olika enheter_

   ![Skapa anpassat namnområde](assets/custom-namespace.png){width="700" zoomable="yes"}

   Klicka på **[!UICONTROL Create]**. Ett anpassat namnutrymme används av tjänsten för enhetlig profil för sammanfogning av profilfragment.

Med schemat, datauppsättningen och det anpassade namnutrymmet konfigurerat för postdata för kundprofiler kan du [konfigurera](connect-data.md#data-collection) din Commerce-instans för att samla in och skicka data till Experience Platform.

Information om hur du skapar ett schema, en datauppsättning och en datastam för beteendedata och data för kontohändelser på baksidan finns i [Uppdatera händelsescheman för tidsserier för Commerce-datainhämtning](update-xdm.md).
