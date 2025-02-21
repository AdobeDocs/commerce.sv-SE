---
title: Testa i mellanlagringsmiljön
description: Lär dig hur du använder  [!DNL Product Recommendations]  från din produktionsmiljö i din staging-miljö i testningssyfte.
feature: Services, Recommendations, Staging
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Testa i mellanlagringsmiljön

Innan du distribuerar rekommendationer till produktionsmiljön bör du testa tjänsten i en icke-produktionsmiljö för att kontrollera att allt fungerar som det ska.

[!DNL Product Recommendations] returnerar produkter som baseras på [beteendedata från din butik](events.md). I en icke-produktionsmiljö har ni förmodligen inga beteendedata från kunderna. Den enda rekommendationstypen som du kan testa utan beteendedata är `More like this`. Den här rekommendationstypen kräver inga indata eftersom den använder en likhetsmatchning för direkt innehåll.

Följande rekommendationstyper kräver beteendedata:

- Mest visade
- Visade det här, såg du att
- Köpte den här, köpte den där

Hur kan du testa dina rekommendationer i en icke-produktionsmiljö med beteendedata? Det finns ett par alternativ.

## Hämta rekommendationer från produktionsmiljön (rekommenderas)

Med Adobe Commerce kan du hämta rekommendationer från din produktionsmiljö och förhandsgranska dem i din icke-produktionsmiljö genom att [växla](settings.md) till SaaS-datautrymmet.

Om du vill hämta rekommendationer från produktionsmiljön måste du se till att:

- Datainsamlingen för Storefront är [konfigurerad och aktiverad](install-configure.md) i produktionsmiljön.
- Katalogen i din icke-produktionsmiljö är i stort sett densamma som den i produktionsmiljön. Genom att använda liknande kataloger ser du till att de produkter som returneras i rekommendationsenheterna liknar dem i produktionsmiljön.

## Generera beteendedata i icke-produktionsmiljö

1. Distribuera modulen `magento/product-recommendations` till en icke-produktionsmiljö där katalogdata liknar din produktionskatalog.

1. Använd ett av de icke-produktionsdatamrådets ID:n för [konfiguration](../landing/saas.md#saas-configuration) i Admin.

1. Generera data själv genom att klicka runt butiken för att efterlikna de verkliga kundernas beteende (eller skapa ett automatiseringsskript). Genom testningen kan ni generera beteendehändelser i er icke-produktionsmiljö. Dessa händelser används för att skapa de produkttillhörigheter som ger rekommendationer. För testning föreslår [!DNL Commerce] att du interagerar med följande rekommendationstyper:

   - Mest visade - kräver minimala indata. Användarna måste visa produkterna.
   - En titt på det här: Flera användare måste visa flera produkter.
   - Köpta den här produkten - Kräver att flera användare köper flera produkter.

### Caveats

- Beteenings- och katalogdata från det icke-producerade [SaaS-datautrymmet](../landing/saas.md#saas-configuration) identifierar en isolerad miljö där de resulterande produktrekommendationerna helt och hållet baseras på beteendedata som genereras på den associerade butiken.

- Eftersom du inte har stora mängder beteendedata är indata för produktassociationer begränsade. Dessa data skickas dock fortfarande till Sensei för att beräkna maskininlärningsmodellerna och lämna rekommendationer baserade på data som genereras i den här miljön.
