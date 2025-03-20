---
title: Delat ansvar
description: Lär dig mer om säkerhetsansvarsområdena för alla parter som deltar i ditt [!DNL Adobe Commerce as a Cloud Service] projekt.
role: Admin, Architect, Leader
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
source-git-commit: d38066b6db7da5bb029391716063ed098be1f519
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Delat ansvar, säkerhet och operativ modell

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] är en on demand-tjänst som är beroende av en säkerhetsmodell för delat ansvar och en driftsmodell. Dessa ansvarsområden delas mellan Adobe och kunderna. Varje part har ett tydligt ansvar för att skydda och köra Adobe Commerce-programmet.

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
| Tillämpa korrigeringar på stödtjänster (till exempel Nginx eller MySQL) | RA | |
| Definiera WAF-regler för serverdelsens ursprung | RA | |
| Definiera CDN WAF-regler för serverdel | RA | |
| Distribuera WAF-regler för serverdelsplattform | RA | |
| Distribuera CDN WAF-regler för serverdel | RA | |
| Åtgärdar kärnfel i [!DNL Adobe Commerce as a Cloud Service] | RA | I |
| Släpper infrastrukturkorrigeringar för [!DNL Adobe Commerce as a Cloud Service] | RA | |
| Skalning (infrastruktur) | RA | |
| Skalning (core application) | RA | |
| Integrera externa program | | RA |
| Installera App Builder-program | | RA |
| Testa prestanda i alla App Builder-program | | RA |
| Theming and design of custom App Builder apps | | RA |
| Konfigurerar backend-DNS | RA | I |
| On-boarding backend CDN | RA | I |
| Stöd för backend CDN | RA | I |
| Hämta en DNS-provider för serverdel | RA | |
| Etablera produktions- och sandlådemiljöer | A | R |
| Åtkomst till Dynamics för Adobe Commerce i molninfrastruktur | R | C |
| Lösning av kundsäkerhetsproblem | RA | I |
| Lösning av CDN-säkerhetsproblem i serverdelen | RA | |
| Hjälp Adobe med säkerhetsforskning (inskannade dokument/revisioner) | RA | |
| Utföra PCI ASV-skanningar | RA | I |
| Reparera Adobe Commerce infrastruktur PCI-skanningar | R | |
| Hantera operativsystems- och plattformshemligheter | RA | |
| Övervaka säkerhetsloggar för serverdel | RA | |
| Kontrollera kundsupport och -åtkomst | A | R |
| Årstestning och dokumentation av Adobe DR-plan samt säkerhetskopiering och återställning | RA | |
| Årlig testning och dokumentation av katastrofåterställningsplanen | RA | |
| Felsökning och isolering av problem | R | R |
| Stöd för felsökning i rätt tid och isoleringsprocess för problem | R | R |
| Publicera uppdateringar och patchar till Adobe Commerce Core | RA | I |
| Installera uppdateringar och patchar i Adobe Commerce Core | RA | I |
| Adobe Commerce programkvalitet | RA | |
