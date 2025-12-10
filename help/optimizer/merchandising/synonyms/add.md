---
title: Skapa och hantera synonymer
description: Lär dig hur du skapar och hanterar synonymer till  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: d2982a0b-e7df-44e6-b3c9-9b4328635d38
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Skapa synonymer

Öka kundengagemanget genom att lägga till en egen strukturerad lista med [!DNL Adobe Commerce Optimizer] synonymer. Du kan lägga till upp till 200 synonymer per butik.

![Synonym Workspace](../../assets/synonym-workspace.png)

## Steg 1: Lägg till en synonym

1. Gå till _Merchandising_ > **Synonymer** från den vänstra listen.
1. Klicka på knappen **[!UICONTROL Add synonyms]**.

## Steg 2: Definiera synonymen efter typ

Följ instruktionerna för den [typ av synonym](type.md) som du vill skapa.

### Tvåvägssynonym

1. Acceptera standardalternativet **Tvåvägs**.

   ![Lägg till tvåvägssynonym](../../assets/synonym-add-two-way.png)

1. Ange termen eller frasen **Nyckelord** som ska matchas.
1. Ange den/de **uttryck** som du vill lägga till som synonymer för nyckelordet. Avgränsa flera termer med komma.
I det här exemplet är nyckelordet som ska matchas&quot;byxor&quot; och uppsättningen expansionstermer är&quot;byxor, slackar&quot;.

   ![Exempel på dubbelriktad synonym](../../assets/synonym-add-two-way-example.png)

1. Klicka på **Spara** när du är klar.

   Synonymuppsättningen visas i listan med en dubbelriktad pil mellan varje term, vilket betyder att termerna är utbytbara.

   ![Tvåvägssynonym](../../assets/synonym-two-way.png)

### Envägssynonym

1. Klicka på synonytypen **Envägs**.

   ![Lägg till envägssynonym](../../assets/synonym-add-one-way.png)

1. Ange villkoren **Nyckelord** och **Utökning**. Avgränsa flera termer med komma.

   ![Exempel på envägssynonym](../../assets/synonym-add-one-way-example.png)

   I det här exemplet är nyckelordet &quot;byxor&quot; och de ensidiga expansionstermerna &quot;capris, peddle-pushers&quot; är en delmängd av &quot;byxor&quot;, men med en specifik betydelse.

1. Klicka på **Spara** när du är klar.

   Synonymuppsättningen visas i listan med en enkelriktad pil som pekar från expanderingsvillkoren till nyckelordet för att ange att termerna är deluppsättningar av nyckelordet. Ett plustecken avgränsar varje expansionsterm.

   ![Envägssynonym](../../assets/synonym-one-way.png)

## Steg 3: Publicera ändringar

1. När dina synonymer är klara klickar du på **Publicera**.
1. Vänta i upp till två timmar tills dina uppdateringar är tillgängliga i butiken.

## Fältbeskrivningar

| Fält | Beskrivning |
|--- |--- |
| [Typ](type.md) | Avgör om synonymer har samma betydelse som nyckelordet eller är en delmängd av nyckelordet. Alternativ:<br />Tvåvägs (standard) - Termer som har samma betydelse som nyckelordet och returnerar samma sökresultat<br />Envägs - Termer som är en delmängd av nyckelordet. Envägssynonymer returnerar en mer smal lista över specifika produkter. |
| Nyckelord | Ett ord som vanligtvis associeras med ett urval produkter i din katalog. |
| Utbyggnad | Ytterligare termer som har samma eller liknande betydelse som nyckelordet. |

## Hantera synonymer

Följ de här instruktionerna för att hantera befintliga [!DNL Adobe Commerce Optimizer] [synonymer](overview.md).

## Sök synonym

För att göra det enkelt att hitta en synonym kan du filtrera listan efter typ och söka efter nyckelord eller expansionsterm. Dessa metoder kan användas var för sig eller tillsammans.

1. Om du vill filtrera listan anger du **typ** till något av följande:

   - Alla
   - Envägs
   - Tvåvägs

1. Om du vill söka efter ett nyckelord eller en utökningsterm anger du minst tre tecken i rutan **[!UICONTROL Search]**.

## Redigera synonym

1. Hitta den synonym som du vill redigera och klicka på **Fler** (..) alternativ.

1. Klicka på **Redigera**.
Nyckelordet är den första termen i listan, och varje term avgränsas med kommatecken. Nyckelord och expanderingsvillkor kan uppdateras, men synonymens typ kan inte ändras.
1. Klicka på det objekt som du vill redigera. Uppdatera sedan texten efter behov.

1. Klicka på **Spara** när du är klar.

## Ta bort synonym

1. Leta reda på den synonym som du vill ta bort i listan och klicka på **Fler** (..) alternativ.
1. Klicka på **Ta bort**.
1. Klicka på **Ta bort synonym** när du uppmanas till detta.

## Publicera ändringar

För att slutföra processen måste de sparade ändringarna publiceras i butiken. Det kan ta upp till två timmar innan uppdateringarna är klara.

1. Klicka på **Publicera**.
1. Leta efter meddelandet högst upp på sidan som bekräftar att dina ändringar har publicerats.
