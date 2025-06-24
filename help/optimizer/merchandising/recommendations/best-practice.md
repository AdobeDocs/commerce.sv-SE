---
title: Rekommendationer bästa praxis
description: Lär dig var du kan placera rekommendationer på olika sidor på din webbplats och förslag på etiketter som används ofta för varje rekommendationstyp.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Rekommendationer bästa praxis

Adobe rekommenderar följande riktlinjer när du använder rekommendationer:

- Diversifiera dina rekommendationstyper. Kunderna börjar ignorera rekommendationer om de föreslår samma produkter om och om igen.

- Distribuera inte samma rekommendationer till kundvagnssidan och orderbekräftelsesidan. Använd `Most Added to Cart` som kundvagnssida och `Bought This, Bought That` som orderbekräftelsesida.

- Håll sajten aktuell. Distribuera inte fler än tre rekommendationsenheter på samma sida.

- Om din butik säljer kläder kan `More like this`-rekommendationen föreslå könsspecifika produkter som inte matchar kön för den produkt som visas. Använd endast den här rekommendationstypen för kategorier som inte är kläder.

## Placement

Med så många rekommendationstyper att välja mellan, vilka ska du använda på varje sida? Om du är osäker på var du ska börja kan du prova följande:

| Sida | Rekommendationstyp |
|---|---|
| Startsida | `Recommended for you` |
| Produktsida | `Viewed this, viewed that` |
| Kundvagn | `Bought this, bought that` |

Du kan spåra [måtten](../../manage-results/recommendation-performance.md) och justera om det behövs. Kom ihåg att experimenterande är avgörande.

## Rekommendationsetiketter

Etiketten som tilldelas en rekommendation i butiken påverkar hur kunderna tolkar dess relevans för dem. Följande etiketter används ofta för varje typ av rekommendation.

| Rekommendationstyp | Rekommenderade etiketter |
|---|---|
| Mest visade<br> Mest tillagda i kundvagn<br>Mest köpta<br>Konvertering (visa i kundvagn)<br>Konvertering (visa för köp) | Mest populära<br>Populära objekt<br>Trending<br>Populära just nu<br>Nyligen populära<br>Populära objekt inspirerade av det här objektet (PDP)<br>Populära säljare<br>Du kanske är intresserad av |
| Rekommenderas för dig | Bara för dig<br>Rekommenderas för dig<br>Inspirerad av dina shoppingtrender |
| Visade det här | Kunder som visade det här objektet visade även<br>Kunder visade<br>Relaterade artiklar |
| Visad den här, köpt den där | Kunder som tittade på det här köpet till slut <br>Kunder som till slut köpte<br>Vad köper andra efter att ha tittat på det här objektet? |
| Köpte den här, köpte den där | Få allt du behöver<br>Glöm inte dessa<br>Köps ofta tillsammans |
| Mer som detta | Fler objekt som denna<br>Liknar detta |
| Allmän | Du kanske också gillar <br>Shoppare som också gillar<br>Liknande alternativ<br>Relaterade artiklar |
| Trender | Trending<br>Trending now<br>Recent trending<br>Hot items<br>Trending related products (PDP) |
| Nyligen visade | Nyligen visade<br>Ta en annan titt |
