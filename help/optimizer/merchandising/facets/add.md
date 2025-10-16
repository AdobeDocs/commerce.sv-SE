---
title: Skapa och hantera ansikten
description: Lär dig hur du lägger till och hanterar ansikten i  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: d6b7ff1f-a9b8-4fb8-8bd3-b3596695045c
source-git-commit: dc751a54c654980a29606c85cdd1cd3324973aab
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Skapa och hantera ansikten

Alla filterbara produktattribut kan användas som en fasett. Med ansikten kan kunderna filtrera och hitta produkter enklare i butiken. I den här artikeln beskrivs hur du lägger till, hanterar och konfigurerar aspekter i din butik.

![Skapa en Fasett](../../assets/create-facet.png)

## Skapa en fasett

1. Välj _Marknadsföring_ > **Ansikten** i den vänstra listen och klicka sedan på **Skapa ansikten**.
1. I listan *Skapa ansikten* har varje tillgängligt attribut en separat ![Lägg till-knapp](../../assets/btn-add.png). Fyll i något av följande:

   - I listan *Fasettattribut* väljer du det produktattribut som du vill använda som en fasett och klickar på **Lägg till**.
   - Om du vill hitta ett visst produktattribut anger du de första tecknen i attributnamnet i rutan *Sök*. Klicka sedan på **Lägg till**.

   Fasetten läggs till längst ned i listan *Dynamiska aspekter* och knappen *Publiceringsändringar* blir tillgänglig.

1. Om det inte går att hitta den aspekt du vill lägga till använder du [Metadata API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata) för att ange parametern `filterable`:

   `"filterable": true`

   Fasetten blir tillgänglig i butiken nästa gång katalogen synkroniseras med [!DNL Adobe Commerce Optimizer]. Om ansiktet inte är tillgängligt efter två timmar kan du läsa [datasynkronisering](../../setup/data-sync.md).

## Redigera fasettegenskaper (valfritt)

1. Hitta den fasett du vill redigera.
1. Klicka på ytterligare väljare (![Mer väljare](../../assets/btn-more.png)).
1. Klicka på **Redigera** på menyn. Justera sedan följande egenskaper efter behov:

   - Etikett - Ange den ansiktsetikett som du vill använda.
   - Sorteringstyp - Välj något av följande:
      - Alfabetiskt - Sorterar ansikten alfabetiskt
      - Antal - Sorterar ansikten baserat på antalet träffar som hittas
   - Maxvärde - Ange det maximala antalet fasettvärden som visas i butiken. Giltiga poster: 0 - 100; Standard: 8.

1. Klicka på **Spara** när du är klar.

## Fäst/ta bort ansikten

Fäststiftets färg ändras när användaren klickar på det och används för att flytta ansiktet till antingen *Fästa ansikten* eller *Dynamiska ansikten* .

1. Om du vill fästa en fasett högst upp i listan *Filter* ska du leta reda på aspekten i listan *Dynamiska ansikten* och klicka på det grå stiftet (![Fästväljaren](../../assets/btn-pin-gray.png)).

   Fäststiftet blir blått och ansiktet flyttas till avsnittet *Fastnålade ansikten*.

1. Om du vill ta bort en fasett hittar du den i listan *Fastnålade ansikten* och klickar på det blå stiftet (![Fästväljaren](../../assets/btn-pin-blue.png)).

   Fäststiftet blir grått och ansiktet flyttas till avsnittet *Dynamiska ansikten*.

>[!NOTE]
>
>Fäst ansiktsordning kan vara inkonsekvent om det finns två etiketter med samma namn.

## Ta bort ansikten

1. Leta reda på aspekten i listan och klicka på (![Mer väljare](../../assets/btn-more.png)) mer väljare.
1. Klicka på **Ta bort**.
1. När du uppmanas att bekräfta klickar du på **Ta bort facet**.
Fasetten tas bort från butiken när ändringarna har publicerats.

## Publicera ändringar

1. Klicka på **[!UICONTROL Publish]** om du vill uppdatera butiken med dina ändringar.
1. Vänta i ungefär 15 minuter tills uppdateringarna visas i din butik.

## Ytterligare information

- Mer information om hur du konfigurerar prisfaktureringsintervall och grupperingar finns i [Inställningar](../../settings.md).
- Läs mer om [typer](type.md) av ansikten.
