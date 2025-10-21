---
title: Versionsinformation om AEM Assets Integration
description: Läs versionsinformationen för information om alla AEM Assets Integration-utgåvor.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 141f2291d1ead324a159053145e92ee7d4237a7d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Versionsinformation om AEM Assets Integration

Denna versionsinformation beskriver den första versionen av AEM Assets Integration och innehåller:

![Nya](../assets/new.svg) nya funktioner
![&#x200B; Åtgärdat problem &#x200B;](../assets/fix.svg) Korrigeringar och förbättringar
![Kända fel](../assets/bug.svg)

Om du vill se funktionsändringar och korrigeringar som släppts utanför den vanliga versionen av funktionen går du igenom avsnitten _Uppdateringar för värdtjänsten_.

Läs mer om kommande releaser, produktsupport och vilka Adobe Commerce-versioner som stöder tillägget AEM Assets Integration i Adobe Commerce [Releasedatum](https://experienceleague.adobe.com/sv/docs/commerce-operations/release/planning/schedule) och [Produkttillgänglighet](https://experienceleague.adobe.com/sv/docs/commerce-operations/release/product-availability) .

## Uppdateringar av värdtjänster

I versionsinformationen beskrivs funktionsändringar och korrigeringar som har gjorts och släppts utanför de vanliga funktionsreleaserna för värdtjänsten.

+++Uppdateringar av värdtjänster

_11 september 2025_

![Nytt problem](../assets/new.svg) Uppdaterade [anpassade automatiska matchningsslutpunkter](https://experienceleague.adobe.com/sv/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} med ett nytt `asset_matches`-attribut.

_11 februari 2025_

![Nytt problem](../assets/new.svg) Nu kan handlare synkronisera bilder för produkter och kategorier.

+++

## v1.2.4

_17 oktober 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Korrigerat problem](../assets/fix.svg)<!-- Issue ACAP-1155 --> Förbättrad övergripande stabilitet för anpassade attribut. Anpassade attribut uppdateras nu korrekt när asynkrona API:er används.

## v1.2.3

_2 oktober 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Korrigerat problem](../assets/fix.svg)<!-- Issue ACAP-1135 --> Ett problem med att uppdatera produktattribut har korrigerats. Produktattributen uppdateras nu som förväntat och ett lämpligt fel returneras i stället för ett 200-svar när uppdateringarna misslyckas.

## v1.2.2

_18 september 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Korrigerat problem](../assets/fix.svg)<!-- Issue ACAP-1110 --> Förbättrad allmän bildstabilitet på mini-cart-, kundvagns- och utcheckningssidor. Bilderna på dessa sidor läses nu in korrekt.

## v1.2.0

_7 augusti 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Nytt problem](../assets/new.svg)<!-- Issue ACAP-1018 --> Nu kan handlare välja källa för bild- och medieresurser genom att välja en [visualiseringsägare](https://experienceleague.adobe.com/sv/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} när de konfigurerar Assets-integreringen från administratören.

![Nytt problem](../assets/new.svg)<!-- Issue ACAP-1078 --> Uppdaterade [anpassade automatiska matchningsslutpunkter](https://experienceleague.adobe.com/sv/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} med ett nytt `asset_matches`-attribut. Med den här ändringen kan du implementera din egen matchande logik för att returnera alla resurser som är associerade med en specifik `productSku`.

## v1.1.2

_11 juni 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Nytt problem](../assets/new.svg)<!-- Issue ACAP-1041 --> Stöd för Adobe Commerce 2.4.8 och PHP 8.4 har lagts till.

## v1.1.0

_23 april 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Nytt problem](../assets/new.svg)<!-- Issue ACAP-955 --> Nu kan en [anpassad domän-URL](https://experienceleague.adobe.com/sv/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) användas i stället för AEM-leverans-URL. Om en handlare anger ett **anpassat domännamn** på sin AEM-kontrollpanel måste du lägga till den här **anpassade domän-URL:en** i Commerce.

![Korrigerat problem](../assets/fix.svg)<!-- Issue ACAP-987 --> Förbättrade övergripande loggar för AEM Assets-synkroniseringsprocesser.

## v1.0.22

_12 mars 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Nytt problem](../assets/new.svg)<!-- Issue ACAP-xx --> Nu krävs [Assets-väljarens IMS-klient-ID](https://experienceleague.adobe.com/sv/docs/commerce/aem-assets-integration/get-started/setup-synchronization) av Assets-väljaren för att aktivera mappning av AEM Assets-bilder med produktkategorier och Page Builder-genererat innehåll.

## v1.0.20

_11 februari 2025_

[!BADGE Stöds]{type=Informative tooltip="Stöds"} Adobe Commerce version 2.4.5 och senare.

![Ny](../assets/new.svg)<!-- Issue ACAP-xx --> allmän tillgänglighetsrelease.
