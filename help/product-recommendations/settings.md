---
title: Inställningar
description: Lär dig hur du ändrar källan för dina [!DNL Product Recommendations] -data och hur du aktiverar visuella rekommendationer.
exl-id: fe37624d-c53e-40cd-b182-10f62cba74c0
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Inställningar

När du [konfigurerar ett SaaS-datautrymme](../landing/saas.md#saas-configuration) för rekommendationer, samlar SaaS-datautrymmet in katalogdata och butiksbeteendedata. [Adobe AI](https://business.adobe.com/ai.html) analyserar data och beräknar produktassociationer som används för att uppfylla produktrekommendationer.

Icke-produktionsmiljöer för testning eller testning har vanligtvis inte den kvantitet eller kvalitet av butiksbeteendedata som behövs för realistiska produktrekommendationer. Faktiskt shoppingbeteende i stor skala kan endast fångas i en produktionsmiljö. För att lösa detta problem kan du med Adobe Commerce använda produktrekommendationer från din produktionsmiljö tillsammans med andra SaaS-datamallar som inte är i produktion. Om du använder faktiska butiksdata i en icke-produktionsmiljö kan du förhandsgranska de rekommendationer kunderna ser och experimentera med olika rekommendationstyper och placeringsplatser. Rekommendationer från en annan SaaS-datamängd kan förhandsgranskas av kunderna, men inte klickas.

Mellanlagringsorder spelas in med mellanlagring `environmentId`. Det påverkar inte produktionsdata. Produktionsdata hämtas med `alternateEnvironmentId`.

>[!NOTE]
>
>När du använder Produktrekommendationer via REST kan parametern `alternateEnvironmentId` användas för att ange andra dataspaces. Den här parametern är inte tillgänglig när produktrekommendationer används via [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/).

## Välj rekommendationskälla

Om du vill ändra källan till dina produktrekommendationer väljer du SaaS-dataområdet med de beteendedata som du vill använda. Innan du börjar bör du kontrollera att:

- Datainsamlingen i Storefront måste vara [konfigurerad och aktiverad](install-configure.md) för din produktionsmiljö och [verifierad](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) att beteendedata skickas till Adobe Commerce.
- Katalogen för icke-produktionsmiljö bör i princip vara densamma som din produktionskatalog. Genom att använda liknande kataloger ser du till att produktrekommendationsenheterna returnerar mycket liknande produktrekommendationsenheter.

1. Logga in på Admin i din icke-produktionsmiljö i Adobe Commerce.

1. Gå till _Marknadsföring_ > **Kampanjer** > _Produktrekommendationer_ på sidofältet **Admin**.

1. Klicka på **Inställningar**.

   ![inställningar för produktrekommendation](assets/settings.png)
   _Inställningar_

1. Aktivera alternativet _Hämta rekommendationer från ett annat SaaS-datautrymme_ i avsnittet **Rekommendationskälla**. Avsnittet _Rekommendationskälla_ visas bara i en icke-produktionsmiljö.

   En lista över _tillgängliga SaaS-datautrymmen_ visas.

   ![inställningar för produktrekommendation](assets/settings-select-saas.png)
   _Inställningar_

1. Välj den SaaS-dataminne som innehåller kunddata som du vill använda.

1. Klicka på **Spara ändringar**.

   Adobe Commerce hämtar nu rekommendationer från den valda datamängden.

   >[!NOTE]
   >
   > Du kan visa rekommendationer som hämtats från ett annat SaaS-datautrymme i butiken som inte är i produktion, men du kan inte klicka på rekommendationerna.

### Konfigurera ett nytt SaaS-datautrymme

1. Klicka på **Redigera konfiguration** i källavsnittet för rekommendationer.

1. Följ instruktionerna för att konfigurera en ny [[!DNL Commerce] tjänst](/help/landing/saas.md).

## Aktivera visuella rekommendationer

Om modulen [Visual Product Recommendations](install-configure.md) är installerad måste du aktivera Visual Recommendations för att kunna använda rekommendationstypen [Visual Likity](type.md#visualsim) .

I avsnittet _Visuella rekommendationer_ anger du **Aktivera visuella rekommendationer** till den aktiva positionen.
