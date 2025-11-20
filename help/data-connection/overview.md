---
title: Översikt över användarhandbok
description: Lär dig hur du integrerar Adobe Commerce-data med Adobe Experience Platform med  [!DNL Data Connection] tillägget.
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# [!DNL Data Connection] - introduktion

>[!IMPORTANT]
>
>Namnet på Experience Platform-anslutningen har ändrats till [!DNL Data Connection].

Tillägget [!DNL Data Connection] ansluter din Adobe Commerce-webbinstans till Adobe Experience Platform och Edge Network. För mobilappsutvecklare använder du Adobe Experience Platform Mobile SDK med Commerce för att hämta in och skicka Commerce-data till Experience Platform. [Läs mer](./mobile-sdk-epc.md).

Din Commerce-butik innehåller massor av data. Information om hur era kunder surfar, ser och till slut köper produkterna på er webbplats kan ge möjligheter att skapa en mer personaliserad shoppingupplevelse. Även om dessa data kan vara till hjälp för inbyggda Commerce-funktioner som kundvagnsprisregler och dynamiska block, förblir data isolerade i din Commerce-instans.

Adobe Experience Platform har en serie teknologier som, när de lagras tillsammans med data från din Commerce-butik, kan distribuera dessa data via Edge Network till andra Adobe DX-produkter för att få insikter om kundernas köpbeteende. Med dessa djupgående insikter kan ni skapa en mer personaliserad shoppingupplevelse i alla kanaler.

Följande bild visar hur dina Commerce-data flödar från din butik till andra Adobe DX-produkter när tillägget [!DNL Data Connection] installeras och konfigureras.

![Hur data flödar till Experience Platform kant](assets/commerce-edge.png)

I bilden ovan skickas data om beteenden, bakgrunder och kundprofiler till Experience Platform-kanten med hjälp av en SDK, API och en källanslutning. Du behöver inte förstå hur dessa delar fungerar när tillägget hanterar komplexiteten i datadelningen för dig. När händelsedata ligger i framkanten kan du hämta dessa data till andra Experience Platform-program. Exempel:

| Program | Syfte | Användningsexempel |
|---|---|---|
| [Adobe [!DNL Real-Time CDP]](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE) | Profilhantering och segmenteringstjänst | **Segmentering av inköpshistorik**: Marknadsförare kan identifiera kunder som köper en artikel baserat på en viss tidsperiod (månads-, kvartalsvis-, års- och så vidare). Marknadsförare kan sedan skapa segment för dessa kunder och inrikta dem på kampanjer, kampanjer och som _toppdata för funnel_ för leads för prenumerationstjänster.<br> **Kategoribaserad segmentering**: Marknadsförare kan se vilken produktkategori som köptes.<br> **Erbjudandebaserad segmentering**: Marknadsförare kan identifiera kunder som konsekvent returnerar produkter. De erbjudanden och rabatter som ges till dem kan nu vara mer intelligenta. Fri frakt kan t.ex. tas bort för en kund som hela tiden returnerar produkter.<br> **Lookalike-målgruppsanpassning**: En _Lookalike-målgrupp_ är en metod som en handlare använder för att nå nya personer som troligtvis är intresserade av sin verksamhet eftersom de har liknande egenskaper som dina befintliga kunder. Lookalike-segment kan skapas baserat på beteendedata och transaktionsdata.<br> **Kundens benägenhet**: Ändringar i kundbeteendet kan identifieras som ett resultat av de djupare kundprofiler som kan skapas från transaktionsdata. Förtroendet för benägenhetspoängen ökar eftersom fler data flödar i beräkningarna, till exempel produktreturer och produktkonfigurationer.<br> **Korsförsäljning**: En handlare kan identifiera starka möjligheter till korsförsäljning och merförsäljning med hjälp av detaljinformation som hämtats i Commerce. |
| [Kund [!DNL Journey Analytics]](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=sv-SE) | Djupanalys av hela Commerce resa | **Säsongstrender**: En handlare kan identifiera säsongstrender, som hjälper dem att förbereda sig för den periodiska förändringen av efterfrågan på vissa produkter. Handlare kan också identifiera förändringar i den totala populariteten för en produkt över flera år.<br> **Konverteringsanalys**: Genom att veta när en produkt köptes tillsammans med åtkomst till butiksintryckshändelser kan handlarna generera en omfattande profil för kunden för att utföra konverteringsanalys. |
| [Adobe [!DNL Analytics]](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html?lang=sv-SE) | Detaljerad analys av kundbeteende och kampanjresultat | **Orderreturer**: Handlare kan identifiera kunder och större kundsegment som har ett mönster för att returnera produkter. Detta hjälper handlarna att förbättra sin affärsstrategi när de förstår hur kundbasbeteendet ser ut.<br> **Beställningsadress**: Baserat på leveransadressen kan en handlare förstå om beställningarna görs av kunderna själva eller om det är för en annan person eller enhet.<br> **Säsongstrender**: En handlare kan identifiera säsongstrender, som hjälper dem att förbereda sig för den periodiska förändringen av efterfrågan på vissa produkter. Handlare kan också identifiera förändringar i den totala populariteten för en produkt över flera år.<br> **Konverteringsanalys**: Genom att veta när en produkt köptes tillsammans med åtkomst till butiksintryckshändelser kan handlarna generera en omfattande profil för kunden för att utföra konverteringsanalys. **Obs!** Adobe Analytics stöder bara beteendehändelsedata (storefront). Adobe Analytics stöder inte transaktionsdata (backoffice). |
| [Adobe [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=sv-SE) | Kampanjsamordning över flera kanaler | **Beteendebaserade resor**: Merchants kan inrikta sig på en kund som köpte en mobiltelefon för två år sedan genom att föreslå att de köper den nya modellen. Marknadsförare kan skapa personaliserade kampanjer och kampanjer för dessa kunder och använda e-post- och SMS-funktioner för att nå ut. Handlare kan också använda historiska orderdata och beteendedata för att identifiera trender. En kund som till exempel har köpt en artikel med en viss konfiguration tidigare och nu vill köpa samma produkt igen, kan få sin inköpsresa förbättrad genom att ge dem synlighet och åtkomst till samma produktkonfigurationer.<br> **Personalization**: Med tillgång till kundprofilinformation kan [!DNL Journey Optimizer] låsa upp mycket personaliserade resor så att handlare kan nå ut till kunderna via flera olika kanaler.<br> **Ny profil har skapats**: Välkomstmeddelanden och kampanjaktiviteter kan uppmuntra och påverka nya kunder på deras kundresor.<br> **Profilen har tagits bort**: Marknadsförare kan välja att sluta skicka e-postreklam till kunder som har avslutat sitt konto. Alternativt kan handlarna också skapa kampanjer för att få tillbaka förlorade kunder. |

## Hämta tillbaka Experience Platform-data till Commerce

Att skicka dina Commerce-data till Experience Platform med tillägget [!DNL Data Connection] är en del av Commerce datadelningsfunktioner. Den andra sidan, som är ett valfritt tillägg, kallas [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=sv-SE). Med det här tillägget kan ni bygga målgrupper i Real-Time CDP och driftsätta dessa målgrupper i er Commerce-butik för att informera om kundprisregler, relaterade produktregler och dynamiska block.

På en hög nivå ser dataflödet från din Commerce-butik till Experience Platform och tillbaka genom Audience Activation-tillägget ut så här:

![[!DNL Data Connection] flöde](assets/data-connection.png)

När du har konfigurerat anslutningen mellan Commerce till Experience Platform och Experience Platform till Commerce fortsätter data att flöda. Du behöver inte återansluta, såvida du inte måste göra det genom en uppgradering.

## Concepts

Att dela data mellan dessa två system kräver att du förstår flera koncept.

- **Data** - Data som delas med Experience Platform samlas in från webbläsarhändelser på din lagringsplats, back office-händelser på servern och profilpostdata. Händelser i Store hämtas från kundernas interaktioner på webbplatsen och innehåller händelser som `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut` och så vidare. Se [storefront-händelser](events.md#storefront-events) för en fullständig lista över butikshändelser. Händelser på serversidan, eller på baksidan av kontoret, innehåller [orderstatus](events-backoffice.md#order-status), information som [`orderPlaced`](events-backoffice.md#orderplaced), [`orderReturned`](events-backoffice.md#orderitemreturncompleted), [`orderShipped`](events-backoffice.md#ordershipmentcompleted), [`orderCancelled`](events-backoffice.md#ordercancelled) och så vidare. Se [back office-händelser](events-backoffice.md) för en fullständig lista över back office-händelser. Profilpostdata innehåller information när en ny profil skapas, uppdateras eller tas bort. Mer information finns i [profilpostdata](events-profilerecord.md).

- **Experience Platform och Edge Network** - Datalagret för de flesta Adobe DX-produkter. Data som skickas till Experience Platform sprids till Adobe DX-produkter via Experience Platform Edge Network. Du kan t.ex. starta Journey Optimizer, hämta specifika data för Commerce-händelser från kanten och skapa en övergiven kundvagn i Journey Optimizer. Journey Optimizer kan sedan skicka e-postmeddelandet om det finns övergivna varukorgar i din Commerce-butik. Läs mer om [Experience Platform och Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html?lang=sv-SE).

- **Schema** - Schemat beskriver strukturen för de data som skickas. Innan Experience Platform kan importera dina Commerce-data måste du skapa ett schema som beskriver datastrukturen och anger begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper. Schemat använder XDM-strukturen, som alla Adobe DX-produkter kan läsa. Schemat ser till att data som skickas till Experience Platform är begripliga för alla DX-produkter. Läs mer om [scheman](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv-SE).

- **Datauppsättning** - En lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras. Alla data som har importerats till Adobe Experience Platform finns i datauppsättningarna. Läs mer om [datauppsättningar](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=sv-SE).

- **Datastream** - ID som gör att data kan flöda från Adobe Experience Platform till andra Adobe DX-produkter. Detta ID måste kopplas till en specifik webbplats i din specifika Adobe Commerce-instans. När du skapar den här dataströmmen anger du XDM-schemat som du skapade ovan. Läs mer om [datastreams](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=sv-SE).

## Stödd arkitektur

Tillägget [!DNL Data Connection] är tillgängligt på följande arkitekturer:

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html?lang=sv-SE)

>[!BEGINSHADEBOX]

## Förutsättningar

Om du vill använda tillägget [!DNL Data Connection] måste du ha följande:

- Adobe Commerce 2.4.4 eller senare
- Adobe ID och organisations-ID
- [Adobe Client Data Layer (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=sv-SE), som krävs för att samla in data för butikshändelser
- Tillstånd till andra Adobe DX-produkter.

>[!ENDSHADEBOX]

## Onboarding-steg

På en hög nivå innebär aktivering av tillägget [!DNL Data Connection] följande steg:

1. [Installera](install.md) tillägget [!DNL Data Connection].
1. [Logga in](https://helpx.adobe.com/se/manage-account/using/access-adobe-id-account.html) på ditt Adobe-konto och [visa](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=sv-SE#concept_EA8AEE5B02CF46ACBDAD6A8508646255) för att bekräfta ditt företags-ID. Organisations-ID är det ID som är kopplat till ditt tilldelade Experience Cloud-företag. Detta ID är en alfanumerisk sträng med 24 tecken, följt av (och måste innehålla) `@AdobeOrg`.
1. Kontrollera att du har [behörighet för datainsamling i Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=sv-SE).
1. Granska de [typer av data](data-ingestion.md) som du kan samla in och skicka.
1. Skapa eller uppdatera ditt [händelseschema för tidsserie](update-xdm.md) eller [profilpostdataschema](profile-data.md) med Commerce-specifika fältgrupper.
1. [Skapa en datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=sv-SE#create-a-dataset) baserat på schemat som du skapade eller uppdaterade. Den här datauppsättningen innehåller de Commerce-data som skickas till Experience Platform Edge.
1. [Skapa en datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=sv-SE) och välj det XDM-schema som innehåller de Commerce-specifika fältgrupperna.
1. [Anslut till Commerce Services](../landing/saas.md).
1. [Anslut till Adobe Experience Platform](connect-data.md).

I resten av guiden får du hjälp att gå igenom alla dessa steg i detalj så att du kan komma igång och börja använda kraften i Adobe DX-produkterna i din Commerce Store.

>[!NOTE]
>
>Lär dig hur du [integrerar](./mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK med Commerce för mobilutvecklare.

## HIPAA-beredskap

Tillägget [!DNL Data Connection] gör att du kan dela [!DNL Commerce] backoffice-data med Experience Platform och behålla kompatibiliteten med HIPAA. [Läs mer](hipaa-readiness.md).

## Målgrupp

Den här guiden är avsedd för Adobe Commerce handlare som vill berika och personalisera sin Commerce-butik för att förbättra shoppingupplevelsen för sina kunder.

## Support

Om du behöver information eller har frågor som inte ingår i den här handboken använder du följande resurser:

- [Hjälpcenter](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html?lang=sv-SE){target="_blank"}
- [Supportärenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=sv-SE#submit-ticket){target="_blank"} - Skicka in en biljett för att få ytterligare hjälp.
