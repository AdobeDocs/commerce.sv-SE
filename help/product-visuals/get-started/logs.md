---
title: Visa och hantera loggar
description: Lär dig var du kan hitta och hantera loggar för produktvisuella effekter.
feature: CMS, Media, Integration
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Visa och hantera loggar

Produktvisualer innehåller följande loggfiler i din Commerce-instans:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Be systemadministratören att kontrollera loggfilens rotationsschema för dessa loggar för att förhindra att de blir för stora. I vissa miljöer roteras loggarna automatiskt, i andra fall måste du konfigurera loggrotation manuellt.  Mer information finns i följande avsnitt:

- Be systemadministratören att konfigurera [loggrotation](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings) för lokala Adobe Commerce-installationer.
- Information om projekt för molninfrastruktur finns i [Visa och hantera loggar](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html).
