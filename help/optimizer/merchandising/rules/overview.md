---
title: Marknadsföringsregler
description: '[!DNL Adobe Commerce Optimizer] försäljningsregler kombinerar logik med åtgärder för att forma shoppingupplevelsen.'
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: f2a9b5e8-d23d-4855-b424-ca6b40e057df
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Marknadsföringsregler

Marknadsföringsregler avser en uppsättning regler som kombinerar logik med åtgärder för att forma en kunds sökupplevelse i din butik. Ni kan använda försäljningsregler för att lyfta, begrava, fästa eller dölja produkter och kalibrera sökresultaten i realtid för att uppnå era affärsmål.

Varje regel har tre huvudkomponenter:

- Villkor - De villkor som utlöser en åtgärd.
- Händelser - De åtgärder som utförs när villkoren uppfylls.
- Detaljer - Namnet på regeln samt valfri tidsram och beskrivning.

Du kan kombinera flera villkor och åtgärder och schemalägga en regel som aktiv under en period. Du kan också ange en standardregel som används även när ingen sökterm har angetts.

## Krav

En enkel sökregel kan ha ett enda villkor och en enda händelse, medan en komplex regel kan ha upp till tio villkor som utlöser upp till 25 händelser.
Regler kan ha:

- Upp till tio villkor
- Upp till 25 händelser

Frågetext kan innehålla:

- Alfanumeriska tecken (bokstäver och siffror)
- Versaler eller gemener. Versaler ignoreras.

## Logiska operatorer

De logiska operatorerna `AND` och `OR` förenar två villkor och returnerar olika resultat. Alla logiska operatorer som används i en regel med flera villkor är desamma. Det går inte att använda både `AND` och `OR` i samma regel.

### Matcha operatorer

Matchningsoperatorerna `All` och `Any` avgör den logiska operatorn som används för att koppla flera villkor i regeln, och kan användas för att ändra den befintliga operatorn.

- `All` - Använder den logiska operatorn `AND` för att koppla flera villkor. En regel som använder operatorn `All` Matcha kan bara ha ett `Search query is`-villkor.
- `Any` - Använder den logiska operatorn `OR` för att koppla flera villkor.

När du komponerar en komplex regel kan det hjälpa till att skriva ut den med indrag för att beskriva de villkor, associerade händelser och produktnamn eller SKU:er som behövs för att returnera de resultat du vill uppnå. Bygg sedan regeln och testa resultatet.

## Standardregel

Du kan ange en standardregel som ska användas när ingen sökterm har angetts, eller när ingen annan sökregel kan användas. Om du anger standardregeln till&quot;Mest köpta&quot; används den rankningstypen som standard för alla frågor, såvida inte superkodade med en mer specifik sökterm. Det går inte att ange någon sökterm för standardregeln.

## Prioritetsordning med flera regler

Endast en sökregel tillämpas på en sökterm åt gången.
Om flera regler är tillämpliga på en sökfras, tillämpas alla dessa regler. Om det finns en kollision mellan två regler - `rule 1` som startar sku1 men `rule 2` döljer samma SKU - har den senast använda regeln (`rule 2`) företräde.

- Regler ordnas med tidsstämpeln&quot;Senast ändrad&quot;. Den senast ändrade regeln tillämpas först och sedan äldre regler i tidsstämpelordning.
- Villkoret `query is` har företräde framför andra villkor. Om en nyare regel innehåller villkoret `query contains`, men en äldre regel har villkoret `query is`, används regeln `query is`.

### Förfrågningar från Storefront

Om en aktiv regel som innehåller ett `query is`-villkor matchar sökfrasen används den. Om det finns flera matchande regler med ett `query is`-villkor används den senast uppdaterade aktiva regeln.
I annat fall används den senast uppdaterade aktiva regeln.

### Förhandsgranska begäranden

Begäran som gjorts i [!DNL Adobe Commerce Optimizer] fungerar något annorlunda. När [!DNL Adobe Commerce Optimizer] förhandsgranskas tillämpas alla regler, inklusive de som har upphört att gälla och schemalagts.

- Om regeln som förhandsgranskas har villkoret `query is` används det.
- Om regeln som förhandsgranskas inte har villkoret `query is` och en efterföljande aktiv matchande regel med villkoret `query is` hittas, tillämpas regeln `query is`.
- Om regeln som förhandsgranskas inte har villkoret `query is`, och ingen annan regel med villkoret `query is` hittas, tillämpas regeln som förhandsgranskas.
