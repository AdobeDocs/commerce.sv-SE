---
title: Fasetttyper
description: Lär dig mer om de olika typerna av faktorer i  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Typer av ansikten

[!DNL Adobe Commerce Optimizer] använder en mängd olika ansiktstyper och de visas bara i listan *Filter* när det är relevant. Listan över tillgängliga facets ändras beroende på vilka produkter som returneras. Följande egenskaper påverkar deras presentation och beteende:

- Fastnålade ansikten - De vanligaste ansiktena kan fästas överst i listan. De återstående ansiktena visas i ordningen *Sorteringstyp* efter de fästa ansiktena.
- Dynamiska aspekter - Produktattribut som [Adobe Sensei](https://www.adobe.com/sensei.html) anser vara mest relevanta för en produktuppsättning och fråga. Beräkningen tar hänsyn till attributmetadata för hela katalogen och fastställer vid frågans tidpunkt de mest relevanta aspekterna.
- Prisfaktorer - Returprodukter efter prisintervall. Du kan ange antalet markeringar och prisintervallet på arbetsytan [*Inställningar*](../../settings.md).

## Fasettetiketter

Du kan redigera ansiktsetiketter från [facetingarbetsytan](workspace.md).

## Sorteringstyp

Alla ansikten som återges för butiken sorteras i alfabetisk ordning eller efter antal.

| Sorteringstyp | Beskrivning |
|--- |--- |
| Alfabetiskt | I listan *Filter* i butiken sorteras ansiktena i bokstavsordning. |
| Antal | Fasetter kan också sorteras efter antalet värden som hittas per faktor i den aktuella uppsättningen returnerade produkter. |
