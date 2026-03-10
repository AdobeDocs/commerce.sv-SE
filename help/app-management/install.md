---
title: Installera och få tillgång till  [!DNL App Management]
description: Krav och åtkomstkrav för Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Installera och få åtkomst till [!DNL App Management]

[!DNL App Management] är tillgängligt i Commerce Admin för berättigande Commerce-instanser. Tillgängligheten beror på vilken distributionstyp du har.

## Tillgänglighet

När du har uppfyllt följande krav väljer du motsvarande flik för din distributionstyp nedan för att se om [!DNL App Management] kräver installation eller redan är tillgänglig på din instans.

## Förutsättningar

Innan du kopplar ett program måste du ha följande:

| Krav | Beskrivning |
|-------------|-------------|
| **Administratörsåtkomst** | Commerce Admin med [!DNL App Management] behörigheter |
| **Distribuerad app** | App Builder-program som distribuerats till din organisation och som är redo att anslutas |
| **Organisationsåtkomst** | Tillgång till den Adobe-organisation där appen är installerad |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management] är automatiskt tillgängligt på [!DNL Adobe Commerce as a Cloud Service]. Ingen installation krävs. [Aktivera det i Admin](#access-app-management) och börja associera appar.

>[!TAB Adobe Commerce i molnet (PaaS) och lokalt]

* **Adobe Commerce 2.4.8 och senare**—[!DNL App Management] inkluderas automatiskt. Ingen installation krävs.

* **Adobe Commerce 2.4.5 till 2.4.7** - Installera [!DNL Admin UI SDK] (som inkluderar [!DNL App Management]) med Composer:

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  Kör sedan:

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

Mer information finns i [Installera eller uppdatera Adobe Commerce Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"}.

>[!ENDTABS]

## Åtkomst [!DNL App Management]

1. Logga in på Commerce Admin.

1. Navigera till **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

Vyn [!DNL App Management] visas. Här kan du associera, konfigurera och hantera App Builder-program.

## Installera App Builder-program

Om du behöver installera en App Builder-app från Adobe Exchange (till exempel en färdig integrerings- eller Marketplace-app) kan du läsa [Installera App Builder-appar från Adobe Exchange](https://experienceleague.adobe.com/sv/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} för steg-instruktioner.

När ett program har installerats och distribuerats använder du [!DNL App Management] för att [associera det med din Commerce-instans](manage-app.md#associate-an-app) och konfigurera dess inställningar.
