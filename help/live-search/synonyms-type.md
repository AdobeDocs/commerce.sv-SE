---
title: Typer av synonymer
description: Envägs- och tvåvägs [!DNL Live Search] synonymer utökar definitionen av nyckelord.
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Typer av synonymer

Envägs- och tvåvägssynonymer utökar definitionen av nyckelord. Vissa är utbytbara med nyckelordet, medan andra representerar en delmängd av nyckelordet.

## Tvåvägs

Tvåvägssynonymer har samma betydelse och returnerar samma sökresultat. I följande exempel är det första ordet som visas i fet stil det nyckelord som används i katalogen, följt av ord som har samma betydelse som det ursprungliga nyckelordet. Du kan skapa ett enkelt par tvåvägssynonymer, eller en kedja av flera tvåvägssynonymer för samma nyckelord.

**jacka** ![Tvåvägsväljare](assets/btn-two-way.png) jacka
**byxor** ![Tvåvägsväljare](assets/btn-two-way.png) slackar ![Tvåvägsväljare](assets/btn-two-way.png) byxor

## Envägs

En envägssynonym är en delmängd av ett nyckelord, men med en mer specifik betydelse. Till exempel är kapris och shorts byxor, men inte alla byxor är kapris eller shorts. En sökning efter byxor innefattar kapris och shorts. Men om du söker efter kortkommandon returneras inte kapris.

**tröja** ![Envägsväljare](assets/btn-one-way.png) hoodie
**byxor** ![Envägsväljare](assets/btn-one-way.png) capris ![Flera enkelriktade väljare](assets/btn-multiple-one-way.png) kalvbyxor ![Flera enkelriktade väljare](assets/btn-multiple-one-way.png) pedagogiker

## God praxis

Tänk på följande metodtips för att få ut det mesta av [!DNL Live Search]-synonymer.

### Undvik stoppord

[!DNL Live Search] filtrerar bort vanliga engelska &quot;stop words&quot; från synonymer, som:

a, an, and, are, as, at, be, but, by, for, if, in, is, it, no, not, of, on, or, such, the, their, then, this, this, to, was, will, with,

Stoppord gör inte synonymer mer mer meningsfulla, utan ökar mängden data som måste bearbetas.

### Användning av singular och plural

Det är inte nödvändigt att definiera både singular- och plural-former för ett ord som synonym. Om du har en blandning av enstaka och plurala termer i din katalog hittar du rätt uppsättning med produkter i Sök. Om du till exempel använder ordet &quot;pant&quot; i produktnamnet och en kund söker efter &quot;byxor&quot;, returneras rätt uppsättning produkter och det enstaka ordet &quot;pant&quot; erbjuds som förslag. Det enstaka ordet&quot;pant&quot; används ofta i modebranschen och ibland i detaljhandeln, även om pluralformen&quot;byxor&quot; används oftare i vissa områden. (Ordet&quot;gnagare&quot; avser tekniskt sett den del av ett plagg som täcker ett ben, vilket är orsaken till att du behöver ett &quot;byxpar&quot; för att täcka båda benen.)

### Konsekvens

Se till att terminologin används på samma sätt i katalogen. Tänk på att det kan finnas regionala skillnader i användning och ibland skillnader inom en bransch.

## Beteende för synonym med flera ord

För synonymer med flera ord ser Commerce synonymen som en fras. Om du till exempel skapar en tvåvägssynonym **matrumstabell** ![Tvåvägsväljare](assets/btn-two-way.png) **kökstabell** ![Tvåvägsväljare](assets/btn-two-way.png) **mattabell** söker Commerce igenom alla fält som är inställda på sökbara för förekomsten av **matrumstabell** eller **kök tabell** eller **mattabell**.

Om ingen synonym skapas och en kund söker efter **kökstabell** söker Commerce efter termerna var som helst i de sökbara fälten, även mellan olika fält, till exempel **tabell** i namnfältet och **kök** i meta-nyckelordet.

När du har skapat en synonym ändras sökbeteendet så att det söker efter den exakta frasen **kökstabell**. Detta kan minska antalet resultat eftersom endast produkter med den exakta frasen visas.

Om du vill att villkoren ska genomsökas separat som tidigare kan du [skapa en supportanmälan](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Om efterfrågan är tillräcklig kommer Commerce att överväga att lägga till den här funktionaliteten i produkten i en kommande release.
