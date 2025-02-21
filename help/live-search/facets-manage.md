---
title: Hantera ansikten
description: Lär dig hur du hanterar befintliga  [!DNL Live Search] facets.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Hantera ansikten

Följ de här instruktionerna för att uppdatera egenskaperna för befintliga aspekter eller ändra deras presentation i butiken.

## Konfigurera grupperingar av prisfaktorer

Se [Inställningar](settings.md) för att konfigurera prisfaktablad och grupperingar.

## Redigera fasett

1. Hitta den fasett du vill redigera.
1. Om det finns många aspekter i listan anger du *Filtrera efter* till något av följande:

   * Fastnålade
   * Dynamisk

   Gå till [Fasetttyper](facets-type.md) om du vill veta mer.

   ![Filteransikten](assets/facets-filter-by-cropped.png)

1. Klicka på **Fler** (..) alternativ om du vill redigera ansiktsegenskaperna.
1. Klicka på **Redigera**

   ![Redigera alternativ](assets/facet-edit-menu.png)

1. Gör något av följande om du vill redigera ansiktsetiketten:

   * Redigera [attributetiketten](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) för en [!DNL Commerce]-butik.
   * För en headless-implementering klickar du på värdet i den första kolumnen och redigerar texten efter behov.

   ![Redigera etikett](assets/facet-edit-label.png)

1. (Endast Headless) Om du vill ändra metoden som används för att sortera fasettvärden klickar du på värdet i kolumnen *Sorteringstyp* och väljer något av följande:

   * Alfabetiskt
   * Antal

   ![Redigera antal](assets/facets-edit-count.png)

1. I kolumnen **Max. värde** anger du det maximala antalet (från 0 till 10) av ansiktsfiltervärden som ska visas i butiken.
1. Klicka på **Spara** när du är klar.

   Ändringarna visas inte i butiken förrän de har publicerats.

## Fäst/ta bort fasett

Fäststiftets färg ändras när användaren klickar på det och används för att flytta ansiktet till antingen *Fästa ansikten* eller *Dynamiska ansikten* .

1. Om du vill fästa en fasett högst upp i listan *Filter* ska du leta reda på aspekten i listan *Dynamiska ansikten* och klicka på det grå stiftet (![Fästväljaren](assets/btn-pin-gray.png)).

   Fäststiftet blir blått och ansiktet flyttas till avsnittet *Fastnålade ansikten*.

1. Om du vill ta bort en fasett hittar du den i listan *Fastnålade ansikten* och klickar på det blå stiftet (![Fästväljaren](assets/btn-pin-blue.png)).

   Fäststiftet blir grått och ansiktet flyttas till avsnittet *Dynamiska ansikten*.

   ![Fastnålade och dynamiska aspekter](assets/facets-pinned-unpinned.png)

>[!NOTE]
>
>Fäst ansiktsordning kan vara inkonsekvent om det finns två etiketter med samma namn.

## Flytta fäst fasett

>[!NOTE]
>
>Ordning av fästa ansikten stöds endast i headless-implementeringar. Om ordnade fasetteringar behövs använder du [!DNL Live Search] PLP-widgeten.

Du kan ändra ordningen på fästa ansikten genom att flytta raden till en annan position. Fästade ytor har en *Flytta*-ikon (![Flytta väljare](assets/btn-move.png)) i början av raden. Till skillnad från fästa ansikten kan dynamiska ansikten inte flyttas.

1. Hitta aspekten i avsnittet *Fastnålade ansikten* i listan.
1. Använd ikonen **Flytta** (![Flytta väljaren](assets/btn-move.png)) om du vill dra raden till en ny plats i avsnittet *Fastnålade ansikten*.

   När ändringarna har publicerats visas de omordnade ansiktena i listan *Filter* i butiken.

## Ta bort fasett

1. Hitta aspekten i listan och klicka på **Fler** (...) alternativ.
1. Klicka på **Ta bort**.
1. När du uppmanas att bekräfta klickar du på **Ta bort facet**.
Fasetten tas bort från butiken när ändringarna har publicerats.

## Publicera ändringar

1. Om du vill uppdatera butiken med dina ändringar klickar du på **Publicera ändringar**.
1. Vänta i ungefär 15 minuter tills uppdateringarna visas i din butik.
