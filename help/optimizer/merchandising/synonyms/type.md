---
title: Synonymer
description: Lär dig mer om de olika synonymtyperna i  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Typer av synonymer

Envägs- och tvåvägssynonymer utökar definitionen av nyckelord. Vissa är utbytbara med nyckelordet, medan andra representerar en delmängd av nyckelordet.

## Tvåvägs

Tvåvägssynonymer har samma betydelse och returnerar samma sökresultat. I följande exempel är det första ordet som visas i fet stil det nyckelord som används i katalogen, följt av ord som har samma betydelse som det ursprungliga nyckelordet. Du kan skapa ett enkelt par tvåvägssynonymer, eller en kedja av flera tvåvägssynonymer för samma nyckelord.

**jacka** ![Tvåvägsväljare](../../assets/btn-two-way.png) jacka
**byxor** ![Tvåvägsväljare](../../assets/btn-two-way.png) slackar ![Tvåvägsväljare](../../assets/btn-two-way.png) byxor

## Envägs

En envägssynonym är en delmängd av ett nyckelord, men med en mer specifik betydelse. Till exempel är kapris och shorts byxor, men inte alla byxor är kapris eller shorts. En sökning efter byxor innefattar kapris och shorts. Men om du söker efter kortkommandon returneras inte kapris.

**tröja** ![Envägsväljare](../../assets/btn-one-way.png) hoodie
**byxor** ![Envägsväljare](../../assets/btn-one-way.png) capris ![Flera enkelriktade väljare](../../assets/btn-multiple-one-way.png) kalvbyxor ![Flera enkelriktade väljare](../../assets/btn-multiple-one-way.png) pedagogiker

## Beteende för synonym med flera ord

För synonymer med flera ord betraktas synonymen som en fras av [!DNL Adobe Commerce Optimizer]. Om du till exempel skapar en tvåvägssynonym **matrumstabell** ![Tvåvägsväljare](../../assets/btn-two-way.png) **kökstabell** ![Tvåvägsväljare](../../assets/btn-two-way.png) **matningstabell** söker [!DNL Adobe Commerce Optimizer] igenom alla fält som är inställda på sökbara för förekomsten av **matrumstabell** eller **3&rbrace;kökstabell** eller **matbord**.

Om ingen synonym skapas och en kund söker efter **kökstabell** söker [!DNL Adobe Commerce Optimizer] efter termerna var som helst i de sökbara fälten, även mellan olika fält, till exempel **tabell** i namnfältet och **kök** i meta-nyckelordet.

När du har skapat en synonym ändras sökbeteendet så att det söker efter den exakta frasen **kökstabell**. Detta kan minska antalet resultat eftersom endast produkter med den exakta frasen visas.

Om du vill att villkoren ska genomsökas separat som tidigare kan du [skapa en supportanmälan](https://experienceleague.adobe.com/sv/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Om efterfrågan är tillräcklig kommer [!DNL Adobe Commerce Optimizer] att överväga att lägga till den här funktionen i produkten i en framtida version.
