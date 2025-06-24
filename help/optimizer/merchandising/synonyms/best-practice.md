---
title: Bästa praxis för synonymer
description: Lär dig de bästa sätten att implementera synonymer i din butik.
role: Admin, Developer
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 54b300ed89f830c2fe5258ec889302a59decd59f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Bästa praxis för synonymer

Nedan finns en lista med de effektivaste strategierna för att skapa synonymer.

- [!DNL Adobe Commerce Optimizer] hanterar felstavningar som standard. Du kan konfigurera synonymer så att de innehåller ord som kunderna kan använda som skiljer sig från de ord som anges i din katalog. Du vill inte förlora någon affär eftersom någon letar efter en &quot;soffa&quot;, medan din produkt listas som en &quot;soffa&quot;. Du kan fånga ett stort antal söktermer genom att ange alla möjliga ord som kunderna kan använda för att hitta dina produkter. Du kan [ange synonymer som ett eller två sätt](add.md#step-2-define-the-synonym-by-type) för att förbättra resultatet.

- Mappa märkesnamn och förkortningar till deras fullständiga namn, till exempel&quot;HP&quot; till&quot;Hewlett-Packard&quot; och vanliga smeknamn för produkter, till exempel&quot;iPhone&quot; till&quot;Apple iPhone&quot;.

- Inkludera branschspecifik jargon och termer som kunderna kan använda som synonymer, till exempel&quot;smygskor&quot; och&quot;skor för löpning&quot;.

- Uppdatera synonymlistan regelbundet baserat på nya söktrender, produkttillägg och kundbeteende.

- Testa effekten av synonymmappningar genom att analysera sökresultat och feedback från kunderna. Förfina mappningarna för att förbättra noggrannheten och relevansen.

- Undvik att använda stoppord eftersom de inte gör synonymer mer meningsfulla, utan ökar mängden data som måste behandlas. [!DNL Adobe Commerce Optimizer] filtrerar bort vanliga engelska &quot;stop words&quot; från synonymer, som:

  a, an, and, are, as, at, be, but, by, for, if, in, is, it, no, not, of, on, or, such, the, their, then, this, this, to, was, will, with,

- Det är inte nödvändigt att definiera både singular- och plural-former för ett ord som synonym. Om du har en blandning av enstaka och plurala termer i din katalog hittar du rätt uppsättning med produkter i Sök. Om du till exempel använder ordet &quot;pant&quot; i produktnamnet och en kund söker efter &quot;byxor&quot;, returneras rätt uppsättning produkter och det enstaka ordet &quot;pant&quot; erbjuds som förslag. Det enstaka ordet&quot;pant&quot; används ofta i modebranschen och ibland i detaljhandeln, även om pluralformen&quot;byxor&quot; används oftare i vissa områden. (Ordet&quot;gnagare&quot; avser tekniskt sett den del av ett plagg som täcker ett ben, vilket är orsaken till att du behöver ett &quot;byxpar&quot; för att täcka båda benen.)

- Se till att terminologin används på samma sätt i katalogen. Tänk på att det kan finnas regionala skillnader i användning och ibland skillnader inom en bransch.
