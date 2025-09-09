---
title: Inställningar
description: Konfigurera inställningar för  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
source-git-commit: 652681cc9aef416040ccd470d04bf2540fe97262
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Inställningar

Använd arbetsytan *Inställningar* för att konfigurera intervall och intervall för prisaspekter och standardspråk för produktidentifiering.

Prisfakteting anger antalet prisintervallgrupper och hur prisvärden fördelas mellan dem.

Inställningen **Språk** anger [!DNL Adobe Commerce Optimizer] vilket språk som ska förväntas när indexet skrivs.

## Prisfakturor

Du kan ange antalet prisintervallgrupper och hur prisvärden fördelas mellan dem. Varje prisintervall överlappar den föregående gruppen med ett. Fem grupper med intervallet 20 skapar till exempel följande prisintervall: 0-20, 20-40, 40-60, 60-80 och >80. Om det inte finns tillräckligt många produkter i katalogen för att fylla alla definierade intervall justeras visningen av tillgängliga grupper därefter. Exempel: 0-20, 60-80, >80.

1. Välj **på arbetsytan** Inställningar **[!UICONTROL Search]** och gör sedan följande under **Prisjustering**:
   - Ange **antalet markeringar** eller prisgrupperingar som ska vara tillgängliga. Upp till 100 prisgrupperingar kan definieras.
   - Ange värdet **Intervall** eller prisintervallet för varje grupp. Maxvärdet är 40 000 000.
1. Klicka på **Spara**.

   Det tar ca 15 minuter innan de uppdaterade inställningarna är tillgängliga i butiken.

### Fältbeskrivningar

| Fält | Beskrivning |
|--- |--- |
| Antal markeringar | Anger antalet prisintervallgrupperingar som kan användas som sökfilter i butiken. Standardvärde: 8, maximalt värde: 100 |
| Intervallvärde | Anger prisintervallen för varje grupp. Fem markeringar med ett intervallvärde på 20 skapar till exempel fem grupperingar av 0-20, 20-40, 40-60, 60-80 och >80. Standardvärde: 5, maximalt värde: 40 000 000 |

## Språk

Språkinställningen talar om för [!DNL Adobe Commerce Optimizer] vilket språk som ska förväntas när katalogen läses och indexet skrivs.

Språk har olika uppsättningar regler för grammatik: hur ord avgränsas, verbtoner och ordformer till exempel.
Inställningen Språk säkerställer att rätt uppsättning regler tillämpas på indexeringsmekanismen.

Ställ in språkinställningen på katalogens primära språk. När du ändrar språket för indexet kan det ta mellan 5 och 60 minuter att återspegla ändringen på butiken, beroende på storleken och komplexiteten hos katalogen.

| Språk | Code |
|----|----|
| Arabiska | ar |
| Armeniska | hy |
| Baskiska | eu |
| Bengali | bn |
| Brasilianska | pt-br |
| Bulgariska | bg |
| Katalanska | ca |
| Kinesiska (förenklad) | zh-cn |
| Kinesiska (traditionell) | zh-tw |
| Tjeckiska | cs |
| Danska | da |
| Nederländska | nl |
| Engelska | en |
| Estniska | et |
| Finska | fi |
| Franska | fr |
| Galiciska | gl |
| Tyska | de |
| Grekiska | el |
| Hindi | hi |
| Ungerska | hu |
| Indonesiska | id |
| Irländska | ga |
| Italienska | it |
| Japanska (Katakana) | ja |
| Koreanska | ko |
| Lettiska | lv |
| Litauiska | lt |
| Norska | no |
| Persiska | fa |
| Portugisiska | pt |
| Rumänska | ro |
| Ryska | ru |
| Sorani | ku |
| Spanska | es |
| Svenska | sv |
| Turkiska | tr |
| Thailändska | th |
