---
title: Implementeringsarbetsflöde
description: Lär dig hur du implementerar  [!DNL Product Recommendations]  på din butik.
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Implementeringsarbetsflöde

[!DNL Product Recommendations] använder både beteendedata och katalogdata:

- Beteende - Data från en kunds engagemang på er webbplats, till exempel produktvisningar, artiklar som lagts till i en kundvagn och inköp. Adobe Commerce och Adobe Sensei samlar inte in personligt identifierbar information.

- Katalog - Produktmetadata som namn, pris och tillgänglighet.

När du installerar `magento/product-recommendations module` aggregerar Adobe Sensei beteendedata och katalogdata och skapar [!DNL Product Recommendations] för varje rekommendationstyp. Tjänsten [!DNL Product Recommendations] distribuerar sedan dessa rekommendationer till din butik. Använd följande arbetsflöde för att implementera produktrekommendationer i butiken:

>[!NOTE]
>
> Om din storefront implementeras med PWA Studio finns mer information i [PWA-dokumentationen](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Om du använder en anpassad klientteknik som React eller Vue JS, ska du lära dig hur du [integrerar](headless.md) [!DNL Product Recommendations] i den headless-butiken.

## Arbetsflöde

1. **Distribuera datainsamling till produktion**

   Distribuering av [!DNL Product Recommendations] kräver två huvudsakliga [datakällor](type.md): katalog och beteende. Eftersom produktion är den enda miljön där era kunders handlande fångas in och analyseras ska ni börja samla in data i produktionen så tidigt som möjligt. [Lär dig](events.md) hur Adobe Sensei utbildar maskininlärningsmodeller som ger rekommendationer av högre kvalitet. När du börjar samla in beteendedata i produktionen kan du dessutom [hämta rekommendationer](staging-environment.md#fetch-recommendations-from-production-environment-recommended) baserat på dessa produktionsdata när du arbetar i icke-produktionsmiljöer. Sedan kan ni testa och experimentera med olika rekommendationer som beräknas utifrån verkliga kunddata som samlats in i produktionen.

   Om du vill distribuera datainsamling till produktion måste du [installera och konfigurera](install-configure.md) modulen [!DNL Product Recommendations] genom att ange en [API-nyckel](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html).

   >[!TIP]
   >
   > Att datainsamlingen distribueras förändrar inte butikens utseende eller kundernas upplevelse. Det är bara när rekommendationsenheter skapas och distribueras som kundupplevelsen i er butik ändras. Testa din icke-produktionsmiljö innan du distribuerar till produktionen. Skapa inte rekommendationsenheter förrän du anpassar mallen. Se nästa steg.

1. **Anpassa mallen så att den matchar din stil**

   Din storefront representerar ditt varumärke, så se till att du ändrar mallen för produktrekommendationer så att den matchar ditt webbplatstema.

   >[!TIP]
   >
   > Genom att anpassa mallen kan du ange din formatmall, skriva över var en rekommendationsenhet visas på en sida och så vidare.

   Läs [Anpassa](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html) i utvecklardokumentationen om du vill veta hur du slutför det här steget.

1. **Testa rekommendationer i din icke-produktionsmiljö**

   Det är alltid en god praxis att testa ny teknik i icke-produktionsmiljön innan du driftsätter till produktionen. Genom att testa rekommendationer i din icke-produktionsmiljö kan du leka med olika typer av rekommendationsenheter, positionering och sidor. Ni kan dra slutsatser baserade på beteendedata som redan samlats in i produktionen när ni testar i er icke-produktionsmiljö, så att rekommendationsresultaten baseras på de faktiska kundernas shoppingbeteende.

   >[!TIP]
   >
   > Se till att din icke-produktionsmiljökatalog i stort sett är densamma som den du har i produktionen. Genom att använda liknande kataloger ser du till att de produkter som returneras i rekommendationsenheterna liknar produkterna i produktionen.

   Mer information om hur du slutför det här steget finns i [Hämta](staging-environment.md) beteendedata från din produktionsmiljö.

1. **Skapa och distribuera rekommendationer till din produktionsbutik**

   Nu när du har distribuerat beteendedatainsamlingen i produktionen, ändrat mallen för produktrekommendationer och testat rekommendationer med hjälp av beteendet hos kunderna är du redo att marknadsföra all kod till produktion och [skapa](create.md) rekommendationer för direktprodukter.
