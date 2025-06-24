---
title: Metodtips för ansikten
description: Lär dig de bästa sätten att implementera faktorer i din butik.
role: Admin, Developer
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Metodtips för ansikten

Filter- och ansiktsfunktioner är en viktig komponent på din [!DNL Adobe Commerce Optimizer]-webbplats, som är utformad för att förbättra shoppingupplevelsen genom att låta kunderna begränsa sökresultaten och hitta produkterna effektivare. Den här funktionen hjälper kunderna att sortera genom enorma kataloger med artiklar genom att tillämpa specifika kriterier, vilket gör köpprocessen snabbare, enklare och mer tillfredsställande. Genom att implementera effektiva, kundvänliga filter och ansikten kan ni hjälpa kunderna att snabbt och effektivt hitta exakt det de behöver, vilket i slutänden ökar kundnöjdheten och konverteringsgraden.

## Tips för att optimera ansikten

- Identifiera de mest relevanta och användbara attributen för dina produkter, till exempel titel, kategori, varumärke, prisintervall, färg och storlek, och ange dem som [dynamiska aspekter](type.md). 
- Ange och sortera produktattribut som är enhetliga i hela katalogen och mycket relevanta för produkterna för att förbättra relevansen och filtreringsmöjligheterna för era kunder.
- Se till att det är enkelt att förstå och namnge fasettetiketter på hela webbplatsen. Använd till exempel&quot;Prisintervall&quot; i stället för&quot;Kostnad&quot;.
- Undvik överväldigande kunder genom att begränsa antalet aspekter till de viktigaste. Alltför många alternativ kan orsaka besluttrötthet. Som standard är [!DNL Adobe Commerce Optimizer] begränsad till högst 100 attribut konfigurerade som facets och 30 bucket returnerade inom varje facet. Läs mer om [ansiktsbegränsningar](../../boundaries-limits.md#catalog-views-and-policies). 
- Låt kunderna välja flera filtervillkor samtidigt för att förfina resultatet. Om du till exempel låter kunderna välja både&quot;röd&quot; och&quot;blå&quot; färg.
- Visa antalet tillgängliga produkter bredvid varje facettalternativ för att ge kunderna en uppfattning om de sökresultat de kan förvänta sig.
- Implementera komprimerbara ansiktssektioner för att hålla gränssnittet rent och hanterbart, särskilt på mobila enheter.
- Låt kunderna enkelt återställa enskilda aspekter eller alla valda filter för att starta en ny sökning.
- Om du har ett stort antal attribut att innesluta bör du överväga att kombinera attribut i ett enda meta-attribut. Exempel: skor har i allmänhet numeriska storlekar, medan skjortor vanligtvis har formatet&quot;S/M/L/XL&quot;. Dessa två typer av storlekar kan kombineras till ett enda sökbart attribut.
