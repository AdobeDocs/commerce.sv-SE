---
title: Prestanda
description: ' [!DNL Live Search] Prestandaarbetsytan ger insikt i de söktermer som kunderna använder.'
exl-id: 07a63df8-b981-4913-841a-7e81ec634281
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Prestanda

Arbetsytan *Prestanda* ger insikt i de söktermer som kunderna använder. Informationen kan användas för att identifiera trender, öka klickfrekvensen och förbättra konverteringsgraden. Arbetsytan Prestanda innehåller en ögonblicksbild av sökstatistik för ett visst datumintervall och följande rapporter:

* Unika sökningar
* Nollresultat
* Populära resultat

![Prestanda](assets/performance-unique-searches.png)

Du kan även gå till [Dashboard för datahantering](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=sv-SE) om du vill ha mer information om datasynkronisering.

>[!NOTE]
>
>Prestandaarbetsytan uppdateras var 12:e timme.

## Visa en rapport

1. Om du vill ange **datumintervallet** klickar du på kalendern (![Kalender](assets/btn-calendar.png)) och gör något av följande:

   * Om du vill ange ett enstaka datum dubbelklickar du på datumet i kalendern.
   * Om du vill ange ett datumintervall klickar du på det första och det sista datumet i kalendern.

>[!NOTE]
>
>Datumintervallet får inte vara längre än ett år.

## Fältbeskrivningar

| Ögonblicksbildsdata | Beskrivning |
|--- |--- |
| Unika sökningar | Det totala antalet unika sökningar för det angivna datumintervallet. Flera sökningar av samma kund, även om de avser samma fråga, anses unika om de skickas med mer än en timmes mellanrum. |
| Genomklickningsfrekvens | Hur många procent av sökningarna som avslutas när kunden klickar på en produkt. Klickfrekvensen är till exempel 50 % om kunden söker efter &quot;byxor&quot; och &quot;skjorta&quot; och sedan klickar på ett resultat i &quot;skjortsökningen&quot;. |
| Konverteringsgrad | Procentandelen produkter som kunden köper jämfört med antalet produkter som kunden klickar på för det angivna datumintervallet. Konverteringsgraden för interaktionen är till exempel 100 % om kunden tittar på sex produkter i povern, klickar på en och gör ett köp. <br /><br />Konverteringsgraden påverkas inte av antalet vyer för en viss produkt. Konverteringsgraden är till exempel densamma om kunden använder sökfunktionen, men klickar inte på några produkter. |
| Nollresultatfrekvens | Procentandelen unika sökningar som inte returnerar några resultat för det angivna datumintervallet. Exempelvis är nollresultatfrekvensen 66,67 % om användaren söker efter &quot;fjajfjjfjf&quot; två gånger (utan resultat) och efter &quot;byxor&quot; en gång (med resultat). |
| Medel. klickningsposition | Den relativa positionen för den genomsnittliga klickfrekvensen baserat på unika sökningar för det angivna datumintervallet. |

| Rapporter | Beskrivning |
|--- |--- |
| Unika sökningar | Visar en lista med unika sökfrågor som används under det angivna datumintervallet. Rapportdata beräknas på samma sätt som unika data för ögonblicksbilder av sökningar. Om en kund skriver samma sökfråga två gånger, men med mer än en timmes mellanrum, betraktas sökningen som två unika sökningar. Rapportgräns: De 500 vanligaste villkoren |
| Nollresultat | Visar en lista över sökfrågor som inte returnerar några resultat och det antal gånger som används under det angivna datumintervallet. Rapportgräns: De 500 vanligaste villkoren |
| Populära resultat | Visar namnen på de produkter som har fått flest vyer under det angivna datumintervallet. Populära resultat beräknas endast utifrån visningar och påverkas inte av antalet klick eller genererade intäkter. Rapportgräns: De 500 vanligaste villkoren |
