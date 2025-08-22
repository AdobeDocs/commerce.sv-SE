---
title: '[!DNL Adobe Commerce as a Cloud Service] - översikt'
description: Läs om de viktigaste funktionerna och fördelarna med  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
source-git-commit: 8fc46b0b93ac5102477f33bf2a8ae70a7acaf85d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---


# [!DNL Adobe Commerce as a Cloud Service] - översikt

[!DNL Adobe Commerce as a Cloud Service] erbjuder flexibilitet, skalbarhet och effektivitet genom att göra det möjligt för företag att leverera och snabbt skala digitala operationer och snabba upp innovationer. Adobe molnbaserade infrastruktur anpassar automatiskt resurser för att möta de höga kraven på trafik, beställningar och kataloghantering.

I följande tabell visas vilka produkter som fungerar som [!DNL Adobe Commerce as a Cloud Service]:

<table style="table-layout:auto">
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;"> ✓ </span>
      </span>
      <strong>Commerce Storefront</strong>
    </td>
    <td>
      Kundgränssnitt där kunderna surfar och köper produkter
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;"> ✓ </span>
      </span>
      <strong>Merchandising Services</strong>
    </td>
    <td>
      Backend-tjänster som hanterar produktkataloger, priser och lager
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;"> ✓ </span>
      </span>
      <strong>Produktbilder</strong>
    </td>
    <td>
      Digital resurshantering för produktbilder och media
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;"> ✓ </span>
      </span>
      <strong>Developer Platform</strong>
    </td>
    <td>
      Grundläggande utvecklingsverktyg och API:er för att bygga anpassade funktioner
    </td>
  </tr>
</table>

## Arkitektur

I följande video visas en kort introduktion till arkitekturen [!DNL Adobe Commerce as a Cloud Service]. Bilder som illustrerar arkitekturen visas nedanför videon.

>[!VIDEO](https://video.tv.adobe.com/v/3443271?learn=on&captions=swe)

I det här diagrammet visas dataflödet mellan [!DNL Adobe Commerce as a Cloud Service] och alla Adobe Experience Cloud-lösningar.

![[!DNL Adobe Commerce as a Cloud Service]-arkitekturdiagram ](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Använd Adobe [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront?lang=sv-SE) från Edge Delivery Services för att skapa avancerade upplevelser på några minuter med enkel dokumentbaserad redigering eller visuell redigering med Storefront Builder.

Commerce Storefront är helt headless med en frikopplad arkitektur som ger alla marknadsföringstjänster och data via ett GraphQL API-lager. Med denna arkitektur kan teamen utveckla sina gränser oberoende av Commerce Foundation, vilket gör det enkelt att skapa och testa nya kontaktytor med ny teknik.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] har inte stöd för Luma-butiker. Om du migrerar från Adobe Commerce i molnet eller lokalt läser du [Befintliga butiker](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/?lang=sv-SE#existing-storefronts) för mer information om övergångar.

## Marknadsföringstjänster och betaltjänster

Adobe erbjuder en mängd intelligenta, sammanställningsbara marknadsföringstjänster som hjälper er att uppnå era affärsmål. Dessa tjänster tillhandahåller även API:er som är viktiga för att optimera prestanda i stor skala.

- [Livesökning](../live-search/overview.md) - Få smartare, snabbare och relevanta resultat för kunderna med det här AI-baserade sökverktyget.
- [Produktrekommendationer](../product-recommendations/overview.md) - Lägg till AI-baserade rekommendationer baserat på kundbeteende, populära trender, produktlikhet med mera.
- [Marknadsföringstjänster som drivs av katalogvyer och principer](../optimizer/setup/catalog-view.md) - Hantera stora och komplexa produktkataloger med flexibel datamodellering för att leverera högpresterande, flexibla e-handelskataloger som är anpassade efter affärsstruktur och go-to-market-strategier. Använd med [Commerce Optimizer](../optimizer/overview.md) för att optimera katalogens prestanda och förbättra konverteringsgraden.
- [Betalningstjänster](../payment-services/guide-overview.md) - Öka kundnöjdheten genom att erbjuda olika betalningsmetoder, inklusive räntefria betalningar, och en enda vy över betalningshantering, order och fakturor.

## Produktvisualiseringar från AEM Assets

Produktvisuellt material förenklar resurshanteringen med hjälp av ett DAM-system (Digital Asset Management) som är integrerat med Adobe Experience Manager för hantering av multimediematerial.

Integreringen säkerställer att digitala resurser, som produktbilder eller marknadsföringsmaterial, dynamiskt länkas till lämpliga försäljningsenheter, inklusive produkter och kategorier i Adobe Commerce, baserat på SKU eller andra nyckelattribut.

Produktvisualer är tillgängliga direkt med [!DNL Adobe Commerce as a Cloud Service], vilket ger några av funktionerna från AEM Assets.

Alternativt innehåller de inbyggda funktionerna i [!DNL Adobe Commerce as a Cloud Service] grundläggande verktyg för resurshantering som du kan använda för att lagra och hantera digitala resurser.

### Produktvisualiseringar eller AEM Assets

Följande jämförelse hjälper dig att välja det bästa alternativet för dina behov i innehållsförsörjningskedjan:

<table style="width: 100%; border-collapse: collapse; margin: 20px 0;">
  <tr style="border: none;">
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">Produktvisualiseringar från AEM Assets</h3>
      <ul style="margin: 0; padding-left: 20px;">
        <li>Integrerad, automatiserad produktbild och video Digital Asset Manager (DAM)</li>
        <li>Ändra storlek på, beskära och konvertera bilder</li>
        <li>Snabb leverans av bilder och video</li>
        <li>Optimera bildformat, storlek och kvalitet baserat på webbläsarens funktioner</li>
        <li>Tillgång till Adobe Express och Adobe Firefly</li>
        <li>Användningsbegränsningar för leveranskapacitet för bild/video och användaråtkomst</li>
        <li>Integrerad resursväljare</li>
      </ul>
    </td>
    <td style="width: 10%; text-align: center; vertical-align: middle; font-size: 98px; color: #d32f2f; font-weight: bold;">
      ›
    </td>
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">AEM Assets</h3>
      <ul style="margin: 0; padding-left: 20px;">
        <li>Alla funktioner från produktvisuella</li>
        <li>Digital Asset Manager (DAM) för fullständig marknadsföring</li>
        <li>Obegränsat antal användare (betala per användare)</li>
        <li>Obegränsad bild- och videoutgång</li>
        <li>Avancerade funktioner för resurshantering:</li>
        <ul>
          <li>360-graders snurra och interaktiva visningsprogram</li>
          <li>Stöd för 3D-modeller och engagerande innehåll</li>
          <li>PDF support</li>
          <li>AI-baserad smart beskärning</li>
         <li>Dynamiska bildmallar</li>
        <li>Smart taggning</li>
        <li>Spåra och analysera tillgångsprestanda</li>
        </ul>
      </ul>
    </td>
  </tr>
</table>

<table style="width: 100%; margin: 20px 0;">
  <tr>
    <td style="background: #f5f5f5; padding: 15px; text-align: center; font-weight: bold;">
      Integrering med Adobe är tillgängligt för enkel migrering mellan olika erbjudanden.
    </td>
  </tr>
</table>

Läs [Integreringsguiden för AEM Assets](../aem-assets-integration/overview.md) om du vill veta mer om hur du integrerar produktvisualer som drivs av AEM Assets med [!DNL Adobe Commerce as a Cloud Service].

## Developer Platform

Adobe erbjuder utvecklare omfattande tilläggspunkter och verktyg för att bygga applikationer som utökar funktionerna i Commerce Foundation och kan integreras med tredjepartssystem (som CRM, ERPS och PIMS). Med dessa verktyg minskar du den totala ägandekostnaden för plattformen på följande sätt:

- **Skalbarhet** - Program kan skalas separat från kärnprogramvaran, vilket ger ökad effektivitet och förenklar uppgraderingar.
- **Isolering** - En isolerad miljö innebär att utvecklare kan uppgradera eller ändra sina tillägg efter eget gottfinnande utan att förlita sig på en kärnversion.
- **Tekniskt oberoende**-Utvecklare kan välja vilket teknikläge och vilka kodningsspråk som passar deras behov.

>[!TIP]
>
>Leverantörsbyggda appar är också tillgängliga för installation på [Adobe Exchange](https://exchange.adobe.com/).

Adobe tillhandahåller följande utvecklingsverktyg för att bygga integreringar och anpassningar:

- [**API-nät för Adobe Developer App Builder**](https://developer.adobe.com/graphql-mesh-gateway/) - Koordinera och kombinera flera API:er, GraphQL, REST och andra källor till en enda frågningsbar slutpunkt för GraphQL.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/) - Bygg och distribuera säkra och skalbara webbprogram som utökar Commerce funktionalitet och integreras med tredjepartslösningar.
- [**Händelser**](https://developer.adobe.com/commerce/extensibility/events/) - Använd anpassade händelseutlösare för att interagera med andra utökningsbara utvecklingsverktyg.
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/) - Använd webhooks för att automatiskt aktivera interaktion mellan Commerce och tredjepartssystem.
- [**Administratörsgränssnitt SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/) - Anpassa och förbättra Commerce Admin med nya sidor och funktioner för era handlare.
- [**Integration Starter Kit**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) - Snabba upp integreringen med referensintegreringar, introduktionsskript och en standardiserad arkitektur.

## Commerce Foundation

Commerce Foundation är en säker automatiserad värdplattform och självbetjäningsfunktioner för hantering av dina Commerce-program i en molnbaserad miljö.

Viktiga funktioner:

- Förenklad introduktion
- Smidiga uppgraderingar
- Tredjepartsintegreringar

### Förenklad introduktion

Starta sandlådan och produktionsinstanser på några minuter med självbetjäningsportalen [!UICONTROL Commerce Cloud Manager]. Allt ni behöver, inklusive Merchandising Services, en headless Commerce-instans och App Builder, konfigureras och integreras automatiskt med era instanser.

Se [Komma igång](getting-started.md) om du vill veta mer om hur du skapar och hanterar Commerce-instanser.

### Smidiga uppgraderingar

Få tillgång till de senaste funktionerna och förbättringarna utan att behöva uppgradera manuellt. Den kontinuerliga leveransen av nya funktioner och uppdateringar eliminerar behovet av manuell korrigering, vilket säkerställer att du alltid har tillgång till de senaste funktionerna med en låg total ägandekostnad.

Den typiska uppgraderingsprocessen för Adobe Commerce i Cloud innefattar att skapa säkerhetskopior, klona instanser, köra kompatibilitetsverktyg och åtgärda kodkonflikter. Det behövs inte längre med [!DNL Adobe Commerce as a Cloud Service]. Adobe skickar meddelanden i appen när nya funktioner och säkerhetsuppdateringar har släppts. Du har en 30-dagars period på dig att utvärdera de nya funktionerna i dina sandlådeinstanser innan uppdateringarna automatiskt tillämpas i dina produktionsmiljöer.

>[!NOTE]
>
>Adobe garanterar bakåtkompatibilitet för alla uppdateringar. Det innebär att när uppdateringar tillämpas bryts inte befintliga funktioner eller anpassningar som följer [API-första utökningsmodellen](https://developer.adobe.com/commerce/extensibility/).

### Tredjepartsintegreringar

Utvecklare kan använda omfattande [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) - och [REST API:er](https://developer.adobe.com/commerce/webapi/rest/) för att integrera Commerce Foundation med tredjepartssystem och utöka Commerce funktioner.

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/sv/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

## Fördelar

Följande avsnitt innehåller information om de fördelar som [!DNL Adobe Commerce as a Cloud Service] ger företag och IT-chefer.

### Företagsledare

- **Öka intäkterna**: Kör organisk trafik med en högpresterande butik som ökar SEO. Skapa personaliserade upplevelser som genererar konverteringar med hjälp av omfattande data.
- **Skalningsåtgärder**: Tjänster för automatisk skalförändring uppfyller verksamhetens höga krav med 99,9 % tillgänglighet. Utnyttja flera varumärken och regioner och ha stöd för B2B och B2C från en enda instans. Stöd för stora och komplexa produktkataloger med flexibel datamodellering.
- **Öka säljarens produktivitet**: Använd AI-baserade marknadsföringstjänster för att förbättra konverteringen. Experimentera direkt i butiken. Hantera butiksupplevelsen och skapa multimedieupplevelser på några minuter med enkel dokumentbaserad redigering eller en visuell redigerare.
- **Lägre total ägandekostnad (TCO) och snabbare innovation**: Alltid uppdaterade tjänster ger dig direkt tillgång till nya funktioner. Aktivera nya funktioner genom att enkelt installera appar från marknadsplatsen. Frigör resurser från tidsödande underhåll och fokusera på att bygga nya funktioner.

### IT-ledare

- **Snabb etablering**: Kom igång snabbt med självbetjäning på några minuter. Alla tjänster är förkonfigurerade för att fungera smidigt tillsammans för att komma igång snabbare. Tillhandahåll sandlådor för utvecklingsexperiment efter behov.
- **Låg ägandekostnad**: Inga fler uppgraderingar med alltid uppdaterade tjänster. Håll dig trygg och följ de senaste säkerhetspatcharna som automatiskt tillämpas åt dig. Skala automatiskt för de mest krävande arbetsbelastningarna.
- **Högpresterande butiker**: Skapa rika upplevelser på några minuter med enkel dokumentbaserad redigering eller en visuell redigerare. Använd AI-baserade marknadsföringstjänster för att öka konverteringsgraden. Inbyggda experiment i butiken.
- **Snabbare innovation**: Frigör resurser från tidsödande underhåll och fokusera på att bygga nya funktioner som ger affärsvärde. Använd omfattande utbyggbarhet och standardbaserade tekniker (JavaScript, HTML, CSS och lågkodsverktyg) för att skapa differentierade upplevelser. Installera appar från tredje part med ett klick för att lägga till nya funktioner på handelsplattformen.
