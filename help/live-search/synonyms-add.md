---
title: Lägg till synonymer
description: Lägg till  [!DNL Live Search] synonymer för att förbättra svar på sökbegäranden.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Lägg till synonymer

Öka kundengagemanget genom att lägga till en egen strukturerad lista med [!DNL Live Search] synonymer. [!DNL Live Search] kan hantera upp till 200 synonymer per `Data Space ID`.

![[!DNL Live Search] synonymer](assets/synonym-workspace.png)

## Steg 1: Lägg till en synonym

1. Gå till **Markering** > SEO &amp; Search > **[!DNL Live Search]** i Admin.
1. För flera arkiv anger du **Scope** till den [butiksvy](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) där synonyminställningarna gäller.
1. Klicka på fliken **Synonymer**.
1. Klicka på knappen **Lägg till synonymer**.

## Steg 2: Definiera synonymen efter typ

Följ instruktionerna för den [typ av synonym](synonyms-type.md) som du vill skapa.

### Tvåvägssynonym

1. Acceptera standardalternativet **Tvåvägs**.

   ![Lägg till tvåvägssynonym](assets/synonym-add-two-way.png)


1. Ange termen eller frasen **Nyckelord** som ska matchas.
1. Ange den/de **uttryck** som du vill lägga till som synonymer för nyckelordet. Avgränsa flera termer med komma.
I det här exemplet är nyckelordet som ska matchas&quot;byxor&quot; och uppsättningen expansionstermer är&quot;byxor, slackar&quot;.

   ![Exempel på dubbelriktad synonym](assets/synonym-add-two-way-example.png)

1. Klicka på **Spara** när du är klar.
Synonymuppsättningen visas i listan med en dubbelriktad pil mellan varje term, vilket betyder att termerna är utbytbara.

   ![Tvåvägssynonym](assets/synonym-two-way.png)

### Envägssynonym

1. Klicka på synonytypen **Envägs**.

   ![Lägg till envägssynonym](assets/synonym-add-one-way.png)

1. Ange villkoren **Nyckelord** och **Utökning**. Avgränsa flera termer med komma.

   ![Exempel på envägssynonym](assets/synonym-add-one-way-example.png)

   I det här exemplet är nyckelordet &quot;byxor&quot; och de ensidiga expansionstermerna &quot;capris, peddle-pushers&quot; är en delmängd av &quot;byxor&quot;, men med en specifik betydelse.

1. Klicka på **Spara** när du är klar.
Synonymuppsättningen visas i listan med en enkelriktad pil som pekar från expanderingsvillkoren till nyckelordet för att ange att termerna är deluppsättningar av nyckelordet. Ett plustecken avgränsar varje expansionsterm.

   ![Envägssynonym](assets/synonym-one-way.png)

## Steg 3: Publicera ändringar

1. När dina synonymer är klara klickar du på **Publicera ändringar**.
1. Vänta i upp till två timmar tills dina uppdateringar är tillgängliga i butiken.

## Fältbeskrivningar

| Fält | Beskrivning |
|--- |--- |
| [Typ](synonyms.md) | Avgör om synonymer har samma betydelse som nyckelordet eller är en delmängd av nyckelordet. Alternativ:<br />Tvåvägs (standard) - Termer som har samma betydelse som nyckelordet och returnerar samma sökresultat<br />Envägs - Termer som är en delmängd av nyckelordet. Envägssynonymer returnerar en mer smal lista över specifika produkter. |
| Nyckelord | Ett ord som vanligtvis associeras med ett urval produkter i din katalog. |
| Utbyggnad | Ytterligare termer som har samma eller liknande betydelse som nyckelordet. |
