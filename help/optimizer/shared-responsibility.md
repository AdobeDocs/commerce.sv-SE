---
title: Delat ansvar
description: Lär dig mer om säkerhetsansvarsområdena för alla parter som deltar i ditt [!DNL Adobe Commerce Optimizer] projekt.
role: Admin, Architect, Leader
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 7c407bfc2becfb0ba6babe5958bcb790c178f406
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Delat ansvar, säkerhet och operativ modell

>[!BEGINSHADEBOX]

I följande sammanfattande tabeller används RACI-modellen för att visa säkerhetsansvarsområden som delas mellan Adobe och kunder.

**R** - Ansvarig
**A** - Redovisningsbar
**C** - konsulterat
**I** - Informad

>[!ENDSHADEBOX]

| Uppgift | Adobe | Kund |
| --- | --- | --- |
| Tillämpar Adobe Commerce infrastrukturkorrigeringar | RA | |
| Tillämpa korrigeringsfiler på stödtjänster | RA | |
| Definiera WAF-regler för serverdelsens ursprung | RA | |
| Definiera CDN WAF-regler för serverdel | RA | |
| Distribuera WAF-regler för serverdelsplattform | RA | |
| Distribuera CDN WAF-regler för serverdel | RA | |
| Åtgärdar fel i [!DNL Adobe Commerce Optimizer] | RA | I |
| Frigör [!DNL Adobe Commerce Optimizer]infrastrukturkorrigeringar | RA | |
| Skalning (infrastruktur) | RA | I |
| Integrera externa program | | RA |
| Installera App Builder-program | | RA |
| Testa prestanda i alla App Builder-program | | RA |
| Theming and design of custom App Builder apps | | RA |
| Konfigurerar backend-DNS | RA |  |
| On-boarding backend CDN | RA |  |
| Stöd för backend CDN | RA |  |
| Hämta en DNS-provider för serverdel | RA | |
| Etablera produktions- och sandlådemiljöer | A | R |
| Åtkomst till Dynamics för Adobe Commerce Optimizer | R | C |
| Lösning av kundsäkerhetsproblem | RA | I |
| Lösning av CDN-säkerhetsproblem i serverdelen | RA | |
| Hjälp Adobe med säkerhetsforskning (inskannade dokument/revisioner) | RA | |
| Utföra PCI ASV-skanningar | RA | I |
| Reparera Adobe Commerce Optimizer infrastruktur PCI-skanningar | R | |
| Hantera operativsystems- och plattformshemligheter | RA | |
| Övervaka säkerhetsloggar för serverdel | RA | |
| Kontrollera kundsupport och -åtkomst | A | R |
| Årstestning och dokumentation av Adobe DR-plan samt säkerhetskopiering och återställning | RA | |
| Årlig testning och dokumentation av katastrofåterställningsplanen | RA | |
| Felsökning och isolering av problem | R | R |
| Stöd för felsökning i rätt tid och isoleringsprocess för problem | R | R |
| Installera uppdateringar och patchar till Adobe Commerce Optimizer | RA | I |
| Adobe Commerce Optimizer programkvalitet | RA | |
