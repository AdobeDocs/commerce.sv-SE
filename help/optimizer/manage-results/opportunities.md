---
title: Möjligheter
description: Identifiera möjligheter att öka trafik, engagemang och konverteringar genom integrering med Adobe Sites Optimizer för smarta, datadrivna webbplatsförbättringar.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 7f7b4a3c866c453d9722b708a0ed4e1b601c8e8e
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# Möjligheter

Sidan **Affärsmöjligheter** hjälper dig att identifiera och implementera optimeringar för att förbättra webbplatstrafiken, användarengagemanget och konverteringsgraden genom integrering med Adobe Sites Optimizer.

![Affärsmöjligheter](../assets/opportunities.png)

## Vad är möjligheter?

[Affärsmöjligheter](https://experienceleague.adobe.com/sv/docs/experience-manager-sites-optimizer/content/documentation/opportunities/overview) är AI-baserade rekommendationer som hjälper handlare att identifiera och åtgärda problem som påverkar deras handelsplatsers prestanda. Dessa rekommendationer drivs av [Adobe Experience Manager Sites Optimizer](https://experienceleague.adobe.com/sv/docs/experience-manager-sites-optimizer/content/home), en molnbaserad tjänst som analyserar och förbättrar webbplatsens prestanda.

## Viktiga funktioner

- **Automatisk problemidentifiering** - Sites Optimizer söker kontinuerligt igenom produktkataloger, sökloggar och rekommendationsdata för att identifiera problem som påverkar identifieringen.
- **AI-drivna rekommendationer** - Ta emot intelligenta förslag för att lösa identifierade problem.
- **Konsekvenskategorisering** - Problemen kategoriseras efter affärsmässiga konsekvenser (sökning, rekommendationer, bläddring/navigering, produktdatakvalitet).
- **Instrumentpanelsrapportering** - Visa problemtrender, produkter eller frågor som påverkas mest samt förbättringar över tid.

## Kom igång

Om du vill aktivera säljprojekt i Commerce Optimizer kontaktar du din Customer Success Manager (CSM). Det finns säljprojekt med Adobe Sites Optimizer-licensen **Ultima**.

## Snabbdemo

Sidan Affärsmöjligheter är indelad i tre flikar som hjälper dig att hantera optimeringsrekommendationer:

- **Aktuell (aktiv)** - Visar nyligen identifierade möjligheter som kräver granskning och åtgärd. Detta är aktiva problem som kan påverka webbplatsens prestanda.
- **Överhoppad** - Innehåller möjligheter som du har valt att stänga av eller skjuta upp. Du kan flytta affärsmöjligheter här om de inte är relevanta för dina aktuella affärsmål.
- **Optimerad (klar)** - Visar möjligheter som har åtgärdats genom automatisk korrigering av distribution. Eventuella möjligheter som hanteras manuellt visas inte på den här fliken. På den här fliken kan du spåra dina automatiskt korrigerade möjligheter över tid.

![Aktuella affärsmöjligheter](../assets/current-opportunities.png)

## Automatisk identifiering av arbetsflöde

Arbetsflödet för automatisk identifiering använder AI-baserad analys för att automatiskt identifiera optimeringsmöjligheter i hela produktkatalogen. Denna automatiska skanningsprocess övervakar kontinuerligt era produktdata, sökloggar och rekommendationsprestanda för att upptäcka problem som kan påverka webbplatsens prestanda, SEO och kundengagemang.

### Så här fungerar det

Automatisk identifiering utnyttjar Adobe Experience Manager Sites Optimizer för att:

- **Analysera produktsidor** - Systemet undersöker de 200 översta sidorna och filtrerar produktinformationssidor för att identifiera optimeringsmål.
- **Extrahera metadata** - Meta-taggar (titlar, beskrivningar, H1-huvuden) extraheras från varje sida för analys.
- **Generera AI-rekommendationer** - Extraherade data bearbetas via Adobe AI-arbetsflöde för att skapa åtgärdbara optimeringsförslag.
- **Fyll i affärsmöjligheter** - Automatiskt identifierade förslag visas på fliken **Aktuell (aktiv)** för din granskning.

### Förutsättning

Innan automatisk identifiering kan generera rekommendationer måste katalogdata vara synkroniserade och uppdaterade för att du ska få korrekta rekommendationer.

### Vad händer härnäst

När automatisk identifiering identifierar optimeringsmöjligheter kan du:

- Granska föreslagna optimeringar på fliken **Aktuell (aktiv)**.
- Distribuera korrigeringar automatiskt med hjälp av [autokorrigeringsarbetsflödet](#auto-fix-workflow) (för [typer av affärsmöjligheter](#supported-opportunity-types) som stöds).
- Implementera ändringarna manuellt i Commerce Admin.
- Ignorera möjligheter som inte är anpassade till era affärsmål.

## Automatiskt fixerat arbetsflöde

Med hjälp av arbetsflödet för automatisk korrigering kan du snabbt driftsätta AI-genererade optimeringar med ett enda klick. När du använder en automatisk korrigering skapas ett katalogoptimeringslager som åsidosätter specifika produktattribut utan att de ursprungliga produktinformationen ändras. Dina ursprungliga produktdata förblir intakta, vilket gör att du säkert kan optimera och återställa ändringarna när du vill. Mer information finns i [Så här fungerar kataloglager med automatisk korrigering](#how-catalog-layers-work-with-auto-fix).

### Affärsmöjlighetstyper som stöds

I följande lista visas vilka typer av affärsmöjligheter som stöds:

- Titeln är för lång
- Titeln är för kort
- Duplicera titel
- Titel saknas
- Tom titel
- För lång beskrivning
- Beskrivning för kort
- Beskrivning saknas
- Tom beskrivning
- Duplicera beskrivning
- H1 saknas
- Duplicera H1
- H1 är för lång

>[!NOTE]
>
>Flera H1:er på sidan stöds för närvarande inte.

### Förutsättningar

Kontrollera följande innan du använder automatisk korrigering:

- Din produktkatalog är helt inkapslad i Commerce Optimizer.
- Affärsmöjlighetstypen stöder automatisk korrigering (vissa optimeringstyper kräver manuell implementering).
- Du har tillräcklig behörighet för att skapa och hantera kataloglager.

>[!IMPORTANT]
>
>Funktionen för automatisk korrigering kräver en fullständigt inkapslad produktkatalog. Om din katalog ännu inte har importerats kan du fortfarande visa möjligheter och implementera korrigeringar manuellt med hjälp av den angivna CSV-filen. Observera att manuella implementeringar inte spåras på fliken **Optimerad (klar)**.

### Distribuera en automatisk korrigeringsoptimering

Följ de här stegen för att implementera en AI-föreslagen optimering:

1. Navigera till **Hantera resultat** > **Affärsmöjligheter**.

1. Granska tillgängliga optimeringsförslag på fliken **Aktuell (aktiv)**.

1. Välj en affärsmöjlighet.

   ![Välj affärsmöjlighet](../assets/autofix-opportunity.png)

   >[!NOTE]
   >
   >Knappen **Distribuera optimering** är bara tillgänglig för [förslagstyper som stöds](#supported-opportunity-types). För typer som inte stöds är kryssrutan inaktiverad och du måste korrigera manuellt i katalogen.

1. Klicka på **Distribuera optimering** och sedan på **Distribuera** för att utlösa den automatiska korrigeringsprocessen.

   ![Distribuera optimering](../assets/deploy-autofix.png)

   Systemet utför följande åtgärder i bakgrunden:

   - Skapar ett nytt kataloglager för produkten (om det inte redan finns ett).
   - Uppdaterar det relevanta attributet (t.ex. metatecknet, beskrivningen eller H1) baserat på AI-rekommendationen.
   - Tilldelar det nya lagret högsta prioritet (ordning 1) i katalogvyn.
   - Validerar ändringen via katalogtjänsten.

1. Övervaka distributionsstatus. Systemet uppdaterar automatiskt förslagsstatus när valideringen är klar.

1. När optimeringen är klar flyttas förslaget till fliken **Optimerad (klar)** med en statusindikator:

   - **Grön bock** - Optimeringslagret är inställt som första prioritet och används aktivt i butiken.
   - **Varningsikon** - Lagret finns men är inte den översta prioriteten, vilket innebär att det kan åsidosättas av ett annat lager.

   ![Slutförda affärsmöjligheter](../assets/done-opportunities.png)

>[!NOTE]
>
>Autokorrigering har stöd för metadataoptimering för webbplatser på alla språk. Sites Optimizer analyserar produktinformationssidor på sitt ursprungliga språk, genererar lokaliserade AI-rekommendationer och skapar kataloglager baserat på det källspråk som är konfigurerat i katalogvyn.

### Så här fungerar kataloglager med automatisk korrigering

Om ett Adobe Sites Optimizer-lager inte finns i katalogvyn skapas ett lager automatiskt och tilldelas ordning 1 (högsta prioritet). Om du tar bort det här lagret återskapas det nästa gång automatisk korrigering körs och befintliga lager flyttas till lägre ordningsnummer. Om Adobe Sites Optimizer-lagret redan finns med ett annat ordernummer ändras inte prioriteten för automatisk korrigering. Om du vill behålla ett automatiskt korrigeringslager, men inte använda det direkt, kan du inaktivera lagret. Läs mer om hur du hanterar [kataloglager](../setup/catalog-layer.md#activate-or-deactivate-layers).

![Kataloglager](../assets/catalog-layers.png)

Diagrammet visar en rad med namnet **ASO-optimering**. Den här posten representerar alla möjligheter som du väljer att åtgärda automatiskt. Oavsett om du korrigerar en enskild affärsmöjlighet automatiskt eller flera affärsmöjligheter visas de alla på den här **ASO-optimeringsraden**. Lagren är specifika för varje katalogvy, så katalogvyn **Los Angeles** som visas här tillämpar bara lagret **ASO-optimering** när den vyn är aktiv.

### Viktiga överväganden

Tänk på följande när du använder automatisk korrigering:

- Statusen som visas för varje förslag återspeglar läget när den automatiska korrigeringsarbetaren kördes. Statusen uppdateras inte dynamiskt om du ändrar ordning på kataloglagren manuellt i efterhand.

- För att optimeringarna ska förbli aktiva bör du undvika att ändra prioriteten för kataloglager manuellt efter att du har distribuerat rekommendationer för automatisk korrigering.

### Felsökning

Om en optimering inte verkar användas i din butik:

1. Kontrollera statusindikatorn på fliken **Optimerad (klar)**.
1. Om en varningsikon visas kontrollerar du prioritetsinställningarna för kataloglagret.
1. Se till att optimeringslagret är inställt på ordning 1 (högsta prioritet) i katalogvyn.
1. Bekräfta att synkroniseringen av katalogdata är aktiv och aktuell.
1. Låt ändringarna spridas. Även med ett korrekt konfigurerat lager på order 1 kan det ta lång tid innan ändringarna visas i butiken, ungefär som när nya produkter publiceras.

## Hur Sites Optimizer och framgångsstatistik fungerar tillsammans

Framgångsmått övervakar viktiga resultatindikatorer, som produktupptäckt och katalogens affärseffektivitet, samtidigt som ni inom Sites Optimizer vet hur ni kan förbättra SEO, lasthastigheten, tillgängligheten och engagemanget. Tillsammans kan marknadsförare och marknadsförare förbättra driftseffektiviteten, vilket ger snabbare slutresultat och konverteringar med minimal IT-support. Om du vill lära dig hur du kan utnyttja dessa två tekniker för att förbättra prestanda och upplevelse i ditt butiksområde kan du läsa [Använda Success Metrics och Sites Optimizer tillsammans](./success-metrics.md#using-success-metrics-and-sites-optimizer-together).

## Läs mer om Sites Optimizer

Mer information om Sites Optimizer funktioner finns i [Adobe Experience Manager Sites Optimizer-dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-manager-sites-optimizer/content/home).

Ytterligare resurser:

- [Möjlighetstyper](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/opportunities) - Läs om tillgängliga optimeringsmöjligheter.
- [Sites Optimizer-funktioner](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/capabilities) - Upptäck vad Sites Optimizer kan göra.

## Mer som detta

- [Resultatmått](success-metrics.md) - Övervaka nyckeltal.
- [Sökprestanda](search-performance.md) - Analysera söktermer och optimera relevansen.
- [Rekommendationsprestanda](recommendation-performance.md) - Övervaka rekommendationseffektivitet.
