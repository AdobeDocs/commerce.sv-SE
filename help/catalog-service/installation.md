---
title: Onboarding och installation
description: Lär dig hur du installerar  [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
source-git-commit: ccc484c47a7bb975a073b00c44cb9af7b5604f88
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Onboarding och installation

Installera katalogtjänsten om du vill begära och ta emot produktdata från en Commerce-instans med [katalogtjänstens GraphQL API](https://developer.adobe.com/commerce/services/graphql/catalog-service/). Katalogtjänsten levereras som ett dispositionsmetapaket från repo.magento.com.

>[!NOTE]
>
>Om din Commerce-instans använder Live Search eller produktrekommendationer installeras eller uppdateras katalogtjänsten automatiskt när du registrerar eller uppgraderar dessa tjänster. Mer information finns i installationsanvisningarna för [Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) och [Produktrekommendationer](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure).



## Systemkrav

**Programvarukrav**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3, 8.4
- Disposition: 2.x

**Plattformar som stöds**

- Adobe Commerce om molninfrastruktur: 2.4.4+
- Adobe Commerce lokalt: 2.4.4+

## Slutpunkter

[!DNL Catalog Service] har två slutpunkter tillgängliga för introduktion:

- Sandbox (`https://catalog-service-sandbox.adobe.io/graphql`) - används för testning och validering innan live-körning
- Produktion (`https://catalog-service.adobe.io/graphql`) - används för Live-trafik för Commerce handlare och webbplatser

Alla Commerce-testinstanser använder sandlådeslutpunkten.

Utför alla inläsningstester på sandlådeslutpunkten. Innan du börjar läsa in testningen skickar du en [supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) så att tjänstgruppen kan förutse den extra servertrafiken.

## Installation och konfiguration

Följande steg krävs för att komma igång med [!DNL Catalog Service] för Adobe Commerce:

- Installera katalogtjänsttillägget (`magento/catalog-service`)
- Konfigurera tjänsten och dataexporten
- Åtkomst till tjänsten

### Installera katalogtjänsttillägget

>[!BEGINSHADEBOX]

**Förutsättning**

- Åtkomst till [repo.magento.com](https://repo.magento.com) för att installera tillägget. Om du vill ha nyckelgenerering och de nödvändiga rättigheterna kan du läsa [Hämta dina autentiseringsnycklar](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Information om molninstallationer finns i [Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Åtkomst till kommandoraden på Adobe Commerce-programservern.

>[!ENDSHADEBOX]

Installera den senaste versionen av Catalog Services-tillägget (`magento/catalog-service`) på en Adobe Commerce-instans som kör Adobe Commerce version 2.4.4 eller senare. Katalogtjänsten levereras som ett dispositionsmetapaket från databasen [repo.magento.com](https://repo.magento.com).

>[!BEGINTABS]

>[!TAB Molninfrastruktur]

Använd den här metoden för att installera [!DNL Catalog Service] för en Commerce Cloud-instans.

1. På din lokala arbetsstation byter du till projektkatalogen för ditt Adobe Commerce i molninfrastrukturprojekt.

   >[!NOTE]
   >
   >Mer information om att hantera Commerce projektmiljöer lokalt finns i [Hantera grenar med CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) i _Adobe Commerce on Cloud Infrastructure User Guide_.

1. Kolla in miljögrenen för att uppdatera med hjälp av Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Lägg till katalogtjänstmodulen.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Uppdatera paketberoenden.

   ```bash
   composer update "magento/catalog-service"
   ```

1. Genomför och push-kodsändringar för filerna `composer.json` och `composer.lock`.

1. Lägg till, implementera och skicka kodändringarna för `composer.json`- och `composer.lock`-filerna till molnmiljön.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   När uppdateringarna skickas till molnmiljön initieras [Commerce molndistributionsprocess](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) för att ändringarna ska tillämpas. Kontrollera distributionsstatusen från [distributionsloggen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Lokal]

Använd den här metoden för att installera [!DNL Catalog Service] för en lokal instans.

1. Använd Composer för att lägga till katalogtjänstmodulen i ditt projekt:

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Uppdatera beroenden och installera tillägget:

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Uppgradera Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Rensa cachen:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >I vissa fall, särskilt när du distribuerar till produktion, kanske du vill undvika att rensa kompilerad kod eftersom det kan ta en stund. Se till att du säkerhetskopierar systemet innan du gör några ändringar.

>[!ENDTABS]

### Konfigurera tjänsten och dataexporten

När du har installerat [!DNL Catalog Service] utför du följande åtgärder för att integrera katalogtjänsten med din Adobe Commerce-instans. Integreringen möjliggör datasynkronisering och kommunikation mellan Commerce-instansen, katalogtjänsten och andra stödtjänster. Datasynkronisering hanteras av [SaaS-tillägget för dataexport](../data-export/overview.md).

1. Konfigurera [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) genom att ange API-nycklar och välja ett SaaS-dataminne.

   Installation av Commerce Services Connector är en engångsprocess som krävs för att använda Adobe Commerce tjänster som Catalog Service, Live Search och Product Recommendations. Om du redan har konfigurerat anslutningen för en annan tjänst hoppar du över det här steget.

1. Utför en inledande datasynkronisering från [Dashboard för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   Den inledande synkroniseringen kan ta från några minuter till timmar beroende på katalogstorleken. Du kan övervaka synkroniseringsstatusen från kontrollpanelen för datahantering. Efter den första synkroniseringen exporterar katalogen produktdata fortlöpande för att hålla tjänsterna uppdaterade.

   >[!NOTE]
   >
   >Du kan också starta den inledande synkroniseringen från kommandoraden med Commerce CLI. Se [Inledande synkronisering](../data-export/data-export-cli-commands.md#initial-sync) i _Exportguiden för SaaS-data_.

Så här ser du till att katalogexporten körs som den ska:

- [Bekräfta att seriejobben körs](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verifiera att indexerarna körs från [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) eller genom att använda Commerce CLI-kommandot `bin/magento indexer:info`.
- Kontrollera att indexerarna `Catalog Attributes Feed, Product Feed, Product Overrides Feed` och `Product Variant Feed` är inställda på `Update by Schedule`.

### Övervaka och felsöka datasynkronisering

Från Commerce Admin kan du övervaka synkroniseringsprocessen med [Dashboard för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Använd [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) och loggar för att hantera och felsöka processen.

### Åtkomst till tjänsten

GraphQL-API:t [!DNL Catalog Service] är tillgängligt från slutpunkten ` https://catalog-service.adobe.io/graphql` med hjälp av POST-kommandon via HTTPS.

I dina GraphQL-frågor måste du ange flera HTTP-huvuden, inklusive den offentliga API-nyckeln som du lade till i konfigurationen för Adobe Commerce Services Connector i Admin. Mer information finns i dokumentationen för [Storefront Services GraphQL](https://developer.adobe.com/commerce/services/graphql/).

### Brandväggskonfiguration

Om du vill tillåta [!DNL Catalog Service] genom en brandvägg lägger du till `commerce.adobe.io` i tillåtelselista.

## Katalogtjänst och API-nät

Med [API-nät för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) kan utvecklare integrera privata eller tredjeparts-API:er och andra gränssnitt med Adobe-produkter med hjälp av Adobe IO.

Avsnittet [[!DNL Catalog Service]  och API Mesh](mesh.md) innehåller information om installation och konfiguration.

## Instrumentpanel för datahantering

Mer information om [!DNL Catalog Service]-datasynkronisering finns i [Kontrollpanelen för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).
