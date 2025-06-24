---
title: Merchandising Rules Workspace
description: Lär dig mer om arbetsytan för marknadsföringsregler.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 33a0903986cf581ece48616dad877db9516d9350
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Merchandising Rules Workspace

Arbetsytan *Regler för marknadsföring* visar det aktuella urvalet av regler och deras status, och ger tillgång till verktyg som du behöver för att skapa och hantera regler. Från arbetsytan kan du:

- Sök efter regler
- Visa regelinformation
- Aktivera/inaktivera regler
- Ta bort regler
- Åtkomst till regelredigeraren

![Merchandising Rules Workspace](../../assets/rules-workspace.png)

## Visa/dölj kolumner

1. Klicka på **Visa/dölj** ![Kolumnväljaren](../../assets/btn-show-hide-columns.png) i det övre högra hörnet.

1. Gör något av följande på menyn:

   - Om du vill visa en dold kolumn klickar du på ett kolumnnamn utan bockmarkering.
   - Om du vill dölja en synlig kolumn klickar du på ett kolumnnamn med en bock.

## Filtrera regler efter status

1. Om din butik har många regler kan du filtrera reglerna efter status för att förkorta listan. Som standard visas alla regler i listan Regler.

1. Om du bara vill visa regler med en viss statusinställning anger du **Status** till något av följande:

   - Alla
   - Aktiv
   - Inaktiv
   - Schemalagd
   - Utkast

   Du kan också filtrera efter **Villkor**, **Startdatum**, **Slutdatum** och **Senast uppdaterad**.

## Visa detaljer

På informationspanelen visas regelnamn, status, villkor och händelser, start- och slutdatum, beskrivning och datum för senaste redigering. Regler kan aktiveras, redigeras och tas bort från informationspanelen.

1. Leta reda på regeln i rutnätet som du vill visa på arbetsytan för *marknadsföringsregler* och klicka på ikonen (![Mer väljare](../../assets/btn-more.png)).

   Du kan göra något av följande på menyn:

   - Redigera regel
   - Ta bort regel
   - Aktivera/inaktivera regel

## Kolumnbeskrivningar

| Kolumn | Beskrivning |
|--- |--- |
| Namn | Regelns namn. |
| Senast uppdaterad | Det datum då regeln senast uppdaterades. |
| Startdatum | Startdatumet för en schemalagd regel. |
| Slutdatum | Slutdatumet för en schemalagd regel. |
| Status | Den färgkodade statusen anger regelns aktuella läge. Använd statuskontrollen ovanför rutnätet för att filtrera regler efter status. Värden:<br />All status - Visar alla regler oavsett status.<br />Aktiv (blå) - Visar endast aktiva regler.<br />Schemalagd (Orange) - visar endast schemalagda regler.<br />Inaktiv (grå) - visar endast inaktiva regler. |

## Kontroller

| Kontroll | Beskrivning |
|--- |--- |
| Lägg till regel | Öppnar [regelredigeraren](add.md). |
| Status | Filtrerar listan med regler efter status. Alternativ: Alla, Aktiva, Inaktiva, Schemalagda |
| ![Kolumnväljare](../../assets/btn-show-hide-columns.png) | Anger vilka kolumner som visas i rutnätet. Alternativ: Senast uppdaterad, Startdatum, Slutdatum, Status |
| Sök | Söker efter en regel efter fullständigt namn eller partiell matchning. |
| ![Fler väljare](../../assets/btn-more.png) | Visar en meny med fler åtgärder som kan tillämpas på den valda regeln. Alternativ: Redigera, Visa information, Ta bort |

## Regelinformation

| Fält | Beskrivning |
|--- |--- |
| Status | Regelns aktuella status. |
| Villkor | Sökfrågan som beskriver villkoren som är kopplade till regeln. |
| Startdatum | Det datum då regeln träder i kraft, om den är schemalagd. |
| Slutdatum | Det datum då regeln förfaller, om den är schemalagd. |
| Beskrivning | En kort beskrivning av regeln. |
| Senast uppdaterad | Datum och tid då regeln senast uppdaterades. |
| Aktiverad | En kontroll som ändrar regelns status. Alternativ: Aktiverad/Inaktiverad |
