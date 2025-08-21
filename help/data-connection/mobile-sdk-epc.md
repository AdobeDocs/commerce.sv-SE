---
title: Integrera Adobe Experience Platform Mobile SDK med Commerce
description: Lär dig hur du använder Adobe Experience Platform Mobile SDK tillsammans med en headless eller anpassad Commerce-butik.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 02d07abb-8d7f-4f0a-9f96-f42654cd79d3
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Integrera Adobe Experience Platform Mobile SDK med Commerce

>[!IMPORTANT]
>
>Adobe Experience Platform Mobile SDK för iOS har stöd för iOS 11 eller senare.

Genom att integrera [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) med Commerce mobilapp kan handlare skicka Commerce [händelsedata](events.md) till Experience Platform.

När händelsedata från Commerce finns tillgängliga i kanten kan de nås av andra Adobe Experience Cloud-program. Du kan till exempel använda data för att skapa målgrupper i Real-Time CDP och sedan [använda dessa målgrupper](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=sv-SE) för att anpassa din Commerce-mobilapp.

## Konfiguration

Installera och konfigurera SDK i Experience Platform för att komma igång med Adobe Experience Platform Mobile SDK med Commerce. Slutför sedan konfigurationen i Commerce.

### Experience Platform

1. Läs mer om mobilappsfunktioner i självstudiekursen [Adobe Experience Cloud i mobilappar](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=sv-SE).

1. [Installera och konfigurera](https://developer.adobe.com/client-sdks/documentation/getting-started/) SDK i Experience Platform.

   >[!NOTE]
   >
   >Schemat som du skapar och konfigurerar i Experience Platform är samma schema som du använder i programkoden i din Commerce-mobilapp.

### Commerce

När du har slutfört SDK-konfigurationen för Experience-plattformen lägger du till SDK-konfigurationen i Commerce.

1. Om du vill skicka händelsedata från Commerce till Experience Platform via SDK måste du ange ett XDM-schema i programkoden. Det här schemat måste matcha schemat [konfigurerat](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) för SDK i Experience Platform.

   I följande exempel visas hur du spårar händelsen `web.webpagedetails.pageViews` och anger `identityMap` med hjälp av e-postfältet.

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. Anslut till Commerce Cloud-miljön.

   Lägg till URL:en till slutpunkten för Commerce GraphQL i projektets bygginställningar. Till exempel:

   - Felsök: http://_debug_.commercialSite.cloud/graphql/
   - Version: http://_release_.commercialSite.cloud/graphql/

1. Om du vill hämta data från slutpunkterna för Commerce GraphQL måste du först generera de filer och kataloger som behövs i ditt projekt med [Apollo Code Generator](https://www.apollographql.com/docs/ios/).

   1. [Installera](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS från projektkatalogen.

   1. [Initiera](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) Apollo Codegen CLI.

      Detta skapar en `apollo-codegen-configuration.json`-fil.

   1. Generera nödvändiga GraphQL-filer och -kataloger i ditt projekt genom att ersätta innehållet i filen `apollo-codegen-configuration.json` med följande:

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [Hämta](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) Commerce GraphQL-schemat.

      Kontrollera att sökvägen är till filen `./apollo-codegen-config.json` som innehåller referensen till Commerce GraphQL-schemat.

   1. [Generera](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate) källkoden.

      Kontrollera att sökvägen är till filen `./apollo-codegen-config.json`, som innehåller konfigurationsinformationen för att generera de filer och kataloger som krävs.

   1. Lägg till eller redigera GraphQL-typer i den nyligen skapade **GraphQLGenerated** -mappen. Du kan till exempel lägga till en `DynamicBlocks.graphql`-typ med följande innehåll:

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   Du har nu integrerat Adobe Experience Platform Mobile SDK med din Commerce-mobilapp. Händelsedata flödar från appen till Experience Platform.

## Hur man särskiljer Commerce-händelser som genereras från mobilprogram

Alla [händelser](events.md) innehåller fältet `channel`. Fältet `channel` innehåller `channel._id` och `channel._type` som för en Luma storefront har namnutrymmesvärdena `"https://ns.adobe.com/xdm/channels/web"` respektive `"https://ns.adobe.com/xdm/channel-types/web"`. I en mobilbutik är namnutrymmesvärdena `"https://ns.adobe.com/xdm/channels/mobile-app"` respektive `"https://ns.adobe.com/xdm/channel-types/mobile"`.

## Nästa steg

Mer information om hur du hämtar Real-Time CDP-målgrupper från din Commerce-mobilapp för att informera om kundvagnsregler, dynamiska block och relaterade produktregler finns i [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=sv-SE#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk).
