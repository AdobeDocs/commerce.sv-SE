---
title: Introduktion till  [!DNL Product Recommendations]
description: '[!DNL Product Recommendations] är ett kraftfullt marknadsföringsverktyg som du kan använda för att öka konverteringarna, öka intäkterna och stimulera kundernas engagemang.'
recommendations: noCatalog
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Introduktion till [!DNL Product Recommendations]

Produktrekommendationer är ett kraftfullt marknadsföringsverktyg som ni kan använda för att öka konverteringarna, öka intäkterna och stimulera kundernas engagemang. Adobe Commerce produktrekommendationer drivs av [Adobe AI](https://business.adobe.com/se/ai.html) som använder artificiell intelligens och maskininlärningsalgoritmer för att utföra en djupanalys av aggregerade besöksdata. Dessa data kombineras med din Adobe Commerce-katalog och ger en engagerande, relevant och personaliserad upplevelse.

Produktrekommendationer visas i butiken som enheter med etiketter, t.ex.&quot;Kunder som tittade på den här produkten också&quot;. Du kan skapa, hantera och distribuera rekommendationer i olika butiksvyer direkt från Adobe Commerce Admin.

Om din storefront implementeras med PWA Studio finns mer information i [PWA-dokumentationen](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Om du använder en anpassad klientteknik som React eller Vue JS, ska du lära dig hur du [integrerar](headless.md) [!DNL Product Recommendations] i den headless-butiken.

>[!NOTE]
>
>Det finns många sätt att utveckla en headless-implementering eller anpassad implementering. I den här guiden beskrivs ett sätt att göra detta med PWA Studio. Det omfattar inte alla scenarier eller eventuella händelser.

## Integritet

Datainsamlingen för syftet med [!DNL Product Recommendations] innehåller ingen personligt identifierbar information (PII). Alla användaridentifierare som cookie-ID:n och IP-adresser är dessutom strikt anonymiserade. Mer information finns i [Adobe integritetspolicy](https://www.adobe.com/privacy/policy.html).

[!DNL Product Recommendations]-användare kan referera till [Instrumentpanelen för datahantering](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=sv-SE) för mer information om datasynkronisering.

## Produktrekommendationer jämfört med produktrelationer

Med tanke på de ständigt föränderliga detaljerna i onlineförsäljningen är det som fungerar bäst för er butik ofta en kombination av flera nyckeltekniker. Genom att använda både [!DNL Product Recommendations] och [&#x200B; produktrelationer &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=sv-SE) får du större flexibilitet när du marknadsför produkter. Du kan utnyttja [!DNL Product Recommendations] som drivs av Adobe AI för att automatisera dina rekommendationer i stor skala. Sedan kan du utnyttja [relaterade produktregler](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=sv-SE) när du måste ingripa manuellt och se till att en specifik rekommendation görs till ett målkundsegment, eller när vissa affärsmål måste uppfyllas.

Med produktrekommendationer kan du:

- Välj bland nio distinkta intelligenta rekommendationstyper baserade på följande områden: kundbaserade, objektbaserade, popularitetsbaserade, trendbaserade och likhetsbaserade
- Använd beteendedata för att personalisera rekommendationer under hela kundresan
- Mät viktiga mätvärden som är relevanta för varje rekommendation för att hjälpa er att förstå effekten av era rekommendationer

## [!DNL Product Recommendations] demo

Titta på den här videon om du vill veta mer om [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/3449962?captions=swe&quality=12)

## Lagringspolicy för katalogdata

Om du inte skickar en fråga för katalogdata i testmiljön under 90 dagar i följd, ställs katalogdata in på viloläge och inga data returneras för någon fråga. Katalogdata i produktionsmiljön påverkas inte av den här principen.

Om du vill återaktivera katalogdata i din testmiljö skickar [du en supportförfrågan](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) med titeln:&quot;Återaktivera [!DNL Product Recommendations]&quot; och inkluderar miljö-ID:n. Katalogdata i testmiljön bör återställas inom några timmar.
