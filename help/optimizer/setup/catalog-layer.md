---
title: Kataloglager
description: Lär dig hur du med kataloglager kan ändra produktdata utan att ändra originalkälldata, så att du kan anpassa och återställa ändringar när som helst.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 4a904527af172a5e35b87410135d55484d07ad84
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Kataloglager

Med kataloglager kan du ändra produktdata utan att ändra originalkälldata. Lager tillämpar ändringar på specifika produktattribut, som namn, beskrivning, bilder, länkar och metadata, genom att skapa ett lager ovanpå baskatalogen. Dina ursprungliga produktdata förblir intakta, vilket gör att du kan anpassa produkterna och återställa ändringarna när du vill.

![Kataloglager](../assets/catalog-layers.png)

## Så här fungerar kataloglager

När en kund tittar på din butik kombinerar systemet dina baskatalogdata med aktiva kataloglager för att visa den slutliga produktinformationen. Så här fungerar processen:

1. **Lagerprogram** - När en begäran görs med ett kanal-ID och ett miljö-ID hämtar lagringstjänsten den relevanta katalogvyn.

1. **Datasammanfogning** - Systemet tillämpar kataloglager på produktdata baserat på lagerprioritetsordning.

1. **Fälthantering** - Olika fälttyper behandlas på olika sätt:

   - **Åsidosätt fält** - Textfält som namn, beskrivning och metatitlar ersätts med de värden som definieras i lagret, där det högprioriterade lagret prioriteras.
   - **Sammanfoga fält** - Matrisfält som bilder, länkar och attribut kombineras från flera lager, vilket ger ett enhetligt svar.

1. **Prioritetsupplösning** - Ordningsfältet avgör vilket lager som har prioritet. När flera lager ändrar samma fält har lagret med det lägre ordningsnumret högre prioritet (till exempel är ordning 1 den högsta).

## Användningsexempel för kataloglager

Kataloglager används ofta för:

- **SEO-optimering** - Åsidosätt produktmetatitlar och beskrivningar baserat på AI-rekommendationer från [Sites Optimizer](../manage-results/opportunities.md).
- **Säsongskampanjer** - Uppdatera produktnamn, beskrivningar eller bilder tillfälligt för kampanjer utan att ändra källdata.
- **Regional anpassning** - Visa annan produktinformation baserat på geografisk plats eller språk.
- **A/B-testning** - Testa olika produktpresentationer för att optimera konverteringsgraden.
- **Hantering av flera varumärken** - Anpassa produktattribut för olika varumärkeskataloger.

## Lägga till ett kataloglager via dataöverföring

Du kan lägga till kataloglager i dina produkter under dataöverföringsprocessen. Den här metoden är idealisk för gruppåtgärder eller automatiserade arbetsflöden.

>[!NOTE]
>
>Du importerar kataloglager med hjälp av API:t för inmatning, men [inställningen av ordningen](#manage-layer-priorities) för lagren görs med användargränssnittet.

**Förutsättningar:**

- API-autentiseringsuppgifter med behörighet att komma åt datainmatningstjänsten
- SKU:er som redan finns i baskatalogen

**Steg:**

1. Förbered lagerdata i rätt format med de produktattribut du vill ändra.

1. Använd API-slutpunkten för produktlager för att importera lagerdata.

1. Kontrollera att lagret har importerats genom att kontrollera katalogvykonfigurationen.

Detaljerade API-specifikationer och exempel på nyttolast finns i [Produktlager](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) i utvecklardokumentationen.

## Lägga till ett kataloglager manuellt i användargränssnittet

>[!NOTE]
>
>Den här funktionen är inte tillgänglig än.

Med katalogvygränssnittet kan du skapa och hantera lager manuellt, vilket är särskilt användbart för integreringar som Sites Optimizer som genererar AI-baserade rekommendationer.

>[!NOTE]
>
>Om ett Sites Optimizer-lager inte finns i katalogvyn skapas ett lager automatiskt och tilldelas ordning 1 (högsta prioritet) av funktionen för automatisk korrigering i Sites Optimizer. Om du tar bort det här lagret återskapas det nästa gång funktionen för automatisk korrigering i Sites Optimizer körs och befintliga lager flyttas till lägre ordningsnummer. Om Sites Optimizer-lagret redan finns i ett annat ordningsnummer ändras inte prioriteten för autokorrigeringsfunktionen.

>[!TIP]
>
>Använd API-metoden [som beskrivs ovan](#add-a-catalog-layer-via-data-ingestion) för grupplageråtgärder.

**Så här skapar du ett manuellt lager:**

1. Navigera till **Store-konfiguration** > **Katalogvyer**.

1. Markera katalogvyn där du vill använda lagret.

1. Klicka på **Lägg till kataloglager** i kataloglageravsnittet.

1. Konfigurera lageregenskaperna:

   - **Lagernamn** - Ange ett beskrivande namn som identifierar syftet med lagret.
   - **Produkter** - Välj de produkter som det här lagret gäller för.
   - **Attribut** - Välj vilka produktattribut du vill ändra (namn, beskrivning, bilder, metataggar och så vidare).
   - **Värden** - Ange de nya värdena för varje markerat attribut.

1. Klicka på **Spara** för att skapa lagret.

Det nya lagret läggs till i katalogvyn och tilldelas automatiskt nästa tillgängliga ordernummer.

## Förhandsgranska lagereffekter

>[!NOTE]
>
>Den här funktionen är inte tillgänglig än.

Innan du aktiverar lager eller ändrar prioriteringar kan du förhandsvisa hur de påverkar produktdata.

**Så här förhandsgranskar du lagerändringar:**

1. Navigera till **Store-konfiguration** > **Katalogvyer**.

1. Markera katalogvyn med de lager som du vill förhandsgranska.

1. Välj en specifik produkt eller använd förhandsvisningsfunktionen i avsnittet Katalollager.

1. Granska den kombinerade produktinformationen och visa hur lager ändrar baskatalogvärdena.

1. Justera lagerinnehåll eller prioritetsordning efter behov.

## Aktivera, inaktivera eller ta bort lager

Du kan aktivera eller inaktivera kataloglager utan att ta bort dem, så att du kan styra när specifika anpassningar ska användas.

**Så här aktiverar eller inaktiverar du ett lager:**

1. Navigera till **Store-konfiguration** > **Katalogvyer**.

1. Markera katalogvyn som innehåller lagret.

1. Leta reda på det lager som du vill växla i avsnittet Kataloglager.

1. Klicka på aktiveringsalternativet för att aktivera eller inaktivera lagret.

   - **Aktiv** - Lagret används på produktdata.
   - **Inaktiv** - Lagret bevaras men tillämpas inte på produktdata.

1. Ändringen träder i kraft direkt i butiken.

**Så här tar du bort ett lager:**

Använd API:t för datainmatning för att [ta bort ett kataloglager](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers).

## Hantera lagerprioriteringar

Den ordning som lager tillämpas i avgör vilka värden som visas i butiken när flera lager ändrar samma produktattribut. Genom att hantera prioriteter ser du till att rätt data visas.

**Förstå prioritetsordning:**

- Varje lager tilldelas ett ordernummer (1, 2, 3 och så vidare)
- Ordning 1 har högst prioritet och åsidosätter alla andra lager
- När flera lager ändrar samma fält har det lägre ordningsnumret företräde
- Prioriteten gäller endast för åsidosättningsfält (namn, beskrivning, meta-taggar)
- Sammanfoga fält (bilder, länkar, attribut) kombinerar data från alla lager

**Så här ändrar du ordning på lagerprioriteter:**

1. Navigera till **Store-konfiguration** > **Katalogvyer**.

1. Markera katalogvyn som innehåller de lager som du vill ändra ordning på.

1. Leta reda på det lager som du vill flytta i avsnittet Kataloglager.

1. Dra och släpp lagret om du vill ändra dess position, eller använd reglagen för ordningsändring.

1. Systemet uppdaterar automatiskt ordernummer baserat på den nya sekvensen.

1. Klicka på **Spara** för att använda den nya prioritetsordningen.

>[!IMPORTANT]
>
>Förändringar av lagrets prioritet träder i kraft omedelbart och kan påverka det som kunderna ser i butiken. Granska förhandsgranskningen innan du sparar för att kontrollera att rätt värden används (**förhandsgranskningen är inte tillgänglig än**).

## God praxis

Följ de här rekommendationerna när du arbetar med kataloglager:

- **Använd beskrivande namn** - Namnge lager tydligt för att indikera deras syfte (till exempel&quot;Semesterkampanj 2025&quot; eller&quot;SEO-optimering - produktsidor&quot;).

- **Begränsa lager** - Systemet har stöd för flera lager, men för många kan påverka prestanda. Konsolidera lager när det är möjligt.

<!--- **Test before activating**—Always preview layer effects before activating them on your live storefront. !!!REMOVE IF PREVIEW NOT AVAILABLE FOR GA!!!-->

- **Logik för dokumentprioritet** - Håll reda på vilka lager som ska prioriteras för att undvika oavsiktliga åsidosättningar.

- **Granska Sites Optimizer-lager** - När du använder autokorrigering från Sites Optimizer skapas lager med högsta prioritet. Tänk på detta när du lägger till manuella lager som kan åsidosätta AI-rekommendationerna. Läs mer om hur du använder [Sites Optimizer](../manage-results/opportunities.md).

- **Bildskärmsprestanda** - Om produktsidan läses in långsamt kan du granska lagerkonfigurationen och överväga att konsolidera lager.

## Mer som detta

- [Katalogvyer](catalog-view.md) - Konfigurera katalogvyer för olika butiker
- [Möjligheter](../manage-results/opportunities.md) - Lär dig mer om AI-baserad optimering med kataloglager
