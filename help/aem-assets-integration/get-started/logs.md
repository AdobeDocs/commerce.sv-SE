---
title: Visa och hantera loggar
description: Lär dig var du hittar och hanterar loggar för AEM Assets Integration for Commerce.
feature: CMS, Media, Integration
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
source-git-commit: 202eca18c71a211cbbf1d210be00543049170c3f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Visa och hantera loggar

AEM Assets-integreringen innehåller följande loggfiler i din Commerce-instans:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Be systemadministratören att kontrollera loggfilens rotationsschema för dessa loggar för att förhindra att de blir för stora. I vissa miljöer roteras loggarna automatiskt, i andra fall måste du konfigurera loggrotation manuellt.  Mer information finns i följande avsnitt:

- Be systemadministratören att konfigurera [loggrotation](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings) för lokala Adobe Commerce-installationer.
- Information om projekt för molninfrastruktur finns i [Visa och hantera loggar](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html).
