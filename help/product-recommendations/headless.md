---
title: Headless
description: Lär dig hur du integrerar  [!DNL Product Recommendations]  i en headlessbutik.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Headless

Du kan integrera [!DNL Product Recommendations] i ett headless-lager med antingen [ PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) eller en anpassad klientteknik, som React eller Vue JS.

Anpassade och headless-integratörer bör referera till dessa Luma- och PWA-instruktioner som en föreslagen implementering. Det finns många sätt att implementera produktrekommendationer i headless-lösningar och den här dokumentationen täcker inte alla scenarier. Integratörerna måste omfatta händelser, design och testning för sina implementeringar.

[!DNL Product Recommendations] kräver [beteendedata och katalogdata](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html?lang=sv-SE) för att fungera. Synkroniseringsprocessen för katalogdata förblir oförändrad i en headless-implementering, men ändringar krävs för att samla in beteendedata.

>[!NOTE]
>
>Headless-instanser måste implementera händelser för att kunna styra kontrollpanelen för produktrekommendationer.

Om du vill integrera [!DNL Product Recommendations] i ett headless-lager måste du:

1. Skicka beteendedata till Adobe Sensei för att analysera och beräkna produktrekommendationsresultat. Du kan också skicka ytterligare data för att aktivera [måttrapportering](workspace.md) för produktrekommendationer.

1. Hämta produktrekommendationsresultat och återge dessa resultat på sidan.

Du kan utföra båda dessa åtgärder med de tillgängliga SDK:erna enligt följande arbetsflöde.

1. [Installera](install-configure.md) modulen [!DNL Product Recommendations].

1. Installera och använd [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) för att utlösa [beteendehändelserna](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html?lang=sv-SE).

   Det minsta antal händelser som krävs för att returnera [!DNL Product Recommendations] resultat:

   | Händelse | Kategori |
   |--- | ---|
   | `view` | produkt |
   | `add-to-cart` | produkt |
   | `place-order` | utcheckning |

   Om du vill aktivera [måttrapportering](workspace.md) krävs följande ytterligare händelser:

   | Händelse | Kategori |
   |--- | ---|
   | `impression-render` | rekommendationsenhet |
   | `view` | rekommendationsenhet |
   | `rec-click` | rekommendationsenhet |
   | `rec-add-to-cart-click` | recommendation-unit (om knappen &quot;Lägg till i kundvagn&quot; finns i rekommendationsmallen) |

1. När händelserna utlöses använder du [Adobe Commerce Storefront Event Collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) för att hantera händelserna och skicka dem till Adobe Sensei.

1. När beteendedata har samlats in kan du [skapa](create.md) [!DNL Product Recommendations] i Admin.

1. Använd [Recommendations SDK](https://developer.adobe.com/commerce/services/product-recommendations/) för att hämta rekommendationsenheterna på butiken. SDK returnerar nödvändiga produktdata för att kunna återge rekommendationsenheter på en sida.
