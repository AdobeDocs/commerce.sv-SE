---
title: Jämförelse mellan Adobe Commerce SaaS och PaaS
description: Jämför Adobe Commerce SaaS- och PaaS-modeller för att fastställa den bästa implementeringsmetoden för dina affärsbehov.
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 3fe22d47b6fd6cf1077cbd4644ffad08f55826ca
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# Jämförelse av funktioner

Adobe Commerce erbjuder tre driftsättningsmodeller:

- [!BADGE Endast SaaS]{type=Positive url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE Endast PaaS]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."} [Adobe Commerce i molnet](https://experienceleague.adobe.com/sv/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/sv/docs/commerce-operations/installation-guide/overview) (lokal)

Jämförelsen fokuserar på skillnaderna mellan SaaS (software-as-a-service) och PaaS-modeller (platform-as-a-service). Dessa modeller ger olika nivåer av anpassning, utbyggbarhet och kontroll över er Commerce-implementering.

>[!NOTE]
>
>Den lokala modellen delar liknande funktioner med PaaS-modellen, så den här jämförelsen gäller också när SaaS ska jämföras med lokala implementeringar.

## Funktioner för butikshantering

[Commerce Admin-gränssnittet](https://experienceleague.adobe.com/sv/docs/commerce-admin/systems/guide-overview) är det primära gränssnittet för att komma åt funktioner för att hantera backend-butiksåtgärder, lager, priser, kampanjer och kundinteraktioner. [!DNL Adobe Commerce as a Cloud Service] erbjuder dock unika lösningar som ersätter några av de välkända funktionerna i [!DNL Adobe Commerce on Cloud] och lokala projekt.

I följande tabell beskrivs de funktioner och ersättningslösningar som finns i [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>PaaS-modellen [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."}</th>
            <th>SaaS-modellen [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast för Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (Adobe-hanterad SaaS-infrastruktur)."}</th>
            <th>Information</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Digital resurshantering</a></td>
            <td><a href="../aem-assets-integration/overview.md">Integrering med AEM Assets</a></td>
            <td>Ett robust DAM-system (Digital Asset Management) som kan integreras med Adobe Experience Manager för hantering av multimediematerial. Standardfunktionen för hantering av digitala filer och resurser innehåller också grundläggande verktyg för hantering av digitala resurser.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/guide-overview">Content Management System (CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=sv-SE">Storefront Builder</a></td>
            <td rowspan="3">En CMS som gör det möjligt för användare att enkelt skapa och hantera butiksinnehåll med hjälp av dokumentredigering eller en Visual Editor och som har inbyggda experimenteringsfunktioner.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/page-builder/guide-overview">Page Builder</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL-omskrivningar</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/staging/content-staging">Mellanlagring av innehåll</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">Katalogtjänst</a></td>
            <td rowspan="2">En tjänst för avancerad visningsmodell (skrivskyddad) som hanterar katalogdata och återger produktrelaterade butiksupplevelser.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/payments/payments">Betalningar</a></td>
            <td><a href="../payment-services/guide-overview.md">Betalningstjänster</a></td>
            <td>En integrerad betalningstjänst som underlättar säkra och effektiva transaktioner.</td>
        </tr>
    </tbody>
</table>

## Utbyggbarhet och plattformsfunktioner

I följande tabell jämförs plattformsfunktioner och utökningsfunktioner för att hjälpa dig förstå skillnaderna och avgöra vilken modell som bäst passar dina affärsbehov innan du påbörjar en implementering.

<table>
    <thead>
        <tr>
            <th>Funktion</th>
            <th>PaaS-modellen [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."}</th>
            <th>SaaS-modellen [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast för Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (Adobe-hanterad SaaS-infrastruktur)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Plattformsfunktioner</strong></td>
        </tr>
        <tr>
            <td>B2B-funktionalitet</td>
            <td>Fullständiga B2B-funktioner är tillgängliga efter installationen</td>
            <td>Förinstallerat med grundfunktioner för B2B <sup>1</sup></td>
        </tr>
        <tr>
            <td>Experimentation</td>
            <td>Tillägg för vissa lager</td>
            <td>A/B-testning för att optimera engagemang och konvertering</td>
        </tr>
        <tr>
            <td>Uppdateringar av funktioner och säkerhet</td>
            <td>Kräver manuell uppgradering och korrigering</td>
            <td>Automatiskt distribuerad</td>
        </tr>
        <tr>
            <td>Värdinfrastruktur</td>
            <td>Single-tenant</td>
            <td>Multi-tenant</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Anpassning av Commerce Admin</strong></td>
        </tr>
        <tr>
            <td>Extensible core Admin screens</td>
            <td>Komplett layout- och funktionsanpassning</td>
            <td>Förinställningsfilter, synlighetskontroller</td>
        </tr>
        <tr>
            <td>Utbyggbara nya administrationsskärmar</td>
            <td>Integrering av administratörsgränssnitt och extern programinjektion (Admin UI SDK)</td>
            <td>Injektion med externa appar (Admin UI SDK)</td>
        </tr>
        <tr>
            <td>Anpassningsbart administratörstema</td>
            <td>Utbyggbart temramverk</td>
            <td>Inget temramverk</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Utbyggbarhet</strong></td>
        </tr>
        <tr>
            <td>Utbyggbarhetsmodell</td>
            <td>In-process (PHP customization) och out-of-process (API:er, händelser, App Builder)</td>
            <td>Endast ej processinriktad (API:er, händelser, App Builder)</td>
        </tr>
        <tr>
            <td>Utbyggbara webb-API:er</td>
            <td>Utbyggbarhet för REST/GraphQL och API Mesh med anpassade lösningar</td>
            <td>API Mesh med anpassade lösningar</td>
        </tr>
        <tr>
            <td>Utbyggbarhet för datamodell</td>
            <td>Komplett anpassning av datamodellen</td>
            <td>Anpassade attribut för kärnenheter och B2B-entiteter<sup>2</sup></td>
        </tr>
        <tr>
            <td>Technologies</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Node</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Data och lagring</strong></td>
        </tr>
        <tr>
            <td>Söka efter indexanpassningar</td>
            <td>Anpassa sökningar</td>
            <td>Kräver lösningar från tredje part</td>
        </tr>
        <tr>
            <td>Anpassade e-posttyper</td>
            <td>Fullständig e-postanpassning</td>
            <td>Endast standardmallar för e-post</td>
        </tr>
        <tr>
            <td>Anpassad datalagring</td>
            <td>DB, fil, cache, kö</td>
            <td>App Builder State Library (endast fil)<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> Core <a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/b2b/guide-overview">B2B-funktioner</a>, som företagsledning och offert, finns tillgängliga i SaaS. Branschspecifika anpassningar kan dock kräva ytterligare implementeringsåtgärder.
                <br><br>
                <sup> 2</sup> Datamodellens utbyggbarhet i SaaS har stöd för <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">utökning av kärnenheter</a> utöver produkt och kund, inklusive B2B-enheter. Branschspecifika datamodeller (till exempel attribut som är specifika för återförsäljare) kan dock kräva ytterligare arkitektoniska överväganden.
                <br><br>
                <sup> 3</sup> Adobe arbetar aktivt med Document DB-integrering för att hantera beständiga lagringsbehov för SaaS. För närvarande kan implementeringar som kräver långsiktig datalagring behöva tillhandahålla och underhålla ytterligare infrastruktur.
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>När du funderar på att migrera till SaaS rekommenderar Adobe att du:
>
>- Flytta lämplig funktionalitet till icke-processrelaterad utökningsbarhet där det är möjligt.
>- Minska den yta som kräver övergång.
>- Överväg [!DNL API Mesh] om du vill utöka API-funktioner.
>- Övervaka Adobe pågående plattformsutveckling och nya funktionsreleaser.
>- Utvärdera branschspecifika datamodellskrav mot tillgängliga utökningsalternativ.
>- Överväg att anta [marknadsföringstjänster som drivs av katalogvyer och principer](../optimizer/setup/catalog-view.md).
