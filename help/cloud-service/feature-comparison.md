---
title: Jämförelse mellan Adobe Commerce SaaS och PaaS
description: Jämför Adobe Commerce SaaS- och PaaS-modeller för att fastställa den bästa implementeringsmetoden för dina affärsbehov.
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: e8e0c9f6a14232abc1332b48df7ae8bc3b955900
workflow-type: tm+mt
source-wordcount: '861'
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
            <th>Funktion</th>
            <th>PaaS-modellen [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."}</th>
            <th>SaaS-modellen [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast för Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (Adobe-hanterad SaaS-infrastruktur)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Digital resurshantering</td>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Mediegalleri</a></td>
            <td><a href="../aem-assets-integration/overview.md">Produktbilder</a></td>
        </tr>
        <tr>
            <td>Innehållshantering</td>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/guide-overview">Content Management System (CMS)</a>, <a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/page-builder/guide-overview">Page Builder</a>, <a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL-omskrivningar</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=sv-SE">Storefront Builder</a></td>
        </tr>
        <tr>
            <td>Kataloghantering</td>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/staging/content-staging">Mellanlagring av innehåll</a>, <a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
            <td><a href="../catalog-service/overview.md">Katalogtjänst</a></td>
        </tr>
        <tr>
            <td>Betalningar</td>
            <td><a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/payments/payments">Betalningslösningar</a></td>
            <td><a href="../payment-services/guide-overview.md">Betalningstjänster</a></td>
        </tr>
        <tr>
            <td>B2B-funktionalitet</td>
            <td>Fullständiga B2B-funktioner är tillgängliga efter installationen</td>
            <td>Förinstallerat med grundfunktioner för B2B <sup>1</sup></td>
        </tr>
        <tr>
            <td>Experimentation</td>
            <td>Tillägg för vissa lager</td>
            <td>Inbyggd A/B-testning för att optimera engagemang och konvertering</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> Core <a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/b2b/guide-overview">B2B-funktioner</a>, som företagsledning och offert, finns tillgängliga i SaaS. Branschspecifika anpassningar kan dock kräva ytterligare implementeringsåtgärder.
            </td>
        </tr>
    </tfoot>
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
            <td>Uppdateringar av funktioner och säkerhet</td>
            <td>Kräver manuell uppgradering och korrigering. Sex depotplåster och en mindre release per år.</td>
            <td>Automatiskt uppgraderad av Adobe via en versionslös SaaS-modell</td>
        </tr>
        <tr>
            <td>Värdinfrastruktur</td>
            <td>Single-tenant</td>
            <td>Multi-tenant</td>
        </tr>
        <tr>
            <td>Prestanda och skalbarhet</td>
            <td>Vågrät automatisk skalning för skalad arkitektur. Lodrät autoskalning för webbnivå introduceras i tidig åtkomst för alla handlare inklusive icke-skalad arkitektur.</td>
            <td>Multi-tenant cloud-native application med fullständig autoskalning över stacken</td>
        </tr>
        <tr>
            <td>Observationer</td>
            <td>[!DNL New Relic] åtkomst för kunderna att övervaka och hantera miljön</td>
            <td>Hanteras av Adobe. Kunder kan använda [!DNL OpenTelemetry] för [!DNL App Builder] appar och RUM-instrumentpaneler för butiker. [!DNL New Relic]-licensen ingår inte. Kunder kan konfigurera [!DNL API Mesh] och [!DNL App Builder] att skicka data till sina egna [!DNL New Relic]-konton.</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] ingår</td>
            <td>Fullt hanterad Edge CDN i nära samarbete med Commerce Storefront. BYO-CDN stöds också.</td>
        </tr>
        <tr>
            <td>Säkerhet och efterlevnad</td>
            <td>SOC2, PCI, ISO-certifieringar per värdtjänstleverantör, HIPAA</td>
            <td>SOC2, PCI, ISO, GDPR. HIPAA är för närvarande inte tillgängligt.</td>
        </tr>
        <tr>
            <td>Disaster Recovery och SLA</td>
            <td>99,99 % infrastruktur, 99,9 % program (Managed Services)</td>
            <td>99,9 % (infrastruktur och tillämpning), snabbare RPO/RTO</td>
        </tr>
        <tr>
            <td>Mottagande regioner</td>
            <td>Azure (24 platser), AWS (22 platser), GCP (8 platser, inte standard)</td>
            <td>Global. Kontakta din kundtjänstrepresentant om du vill ha information om produktionsmiljöer i ditt område. Ytterligare platser introducerades baserat på efterfrågan.</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Anpassning av Commerce Admin</strong></td>
        </tr>
        <tr>
            <td>Admin Console-utökningsmöjligheter</td>
            <td>Anpassning och tema för PHP, utbyggbarhet för App Builder (rekommenderas)</td>
            <td>App Builder extensibility</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Utbyggbarhet</strong></td>
        </tr>
        <tr>
            <td>Utbyggbarhetsmodell</td>
            <td>In-process (PHP-anpassning) och out-of-process (Recommended:APIs, events, App Builder)</td>
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
            <td>Anpassade attribut för kärnenheter och B2B-entiteter<sup>1</sup></td>
        </tr>
        <tr>
            <td>Technologies</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Node</td>
        </tr>
        <tr>
            <td>App Marketplace</td>
            <td>[Magento Marketplace](https://marketplace.magento.com/) (PHP-tillägg) och [Exchange Marketplace](https://commercemarketplace.adobe.com) för [!DNL App Builder] appar (rekommenderas)</td>
            <td>[!DNL App Builder] appar från [[!DNL Exchange Marketplace]](https://commercemarketplace.adobe.com)</td>
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
            <td>App Builder State Library (file only)<sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">Database Storage for App Builder</a> är för närvarande i Tidig åtkomst.</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> Datamodellens utbyggbarhet i SaaS stöder <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">utökning av kärnenheter</a> utöver produkt och kund, inklusive B2B-enheter. Branschspecifika datamodeller (till exempel attribut som är specifika för återförsäljare) kan dock kräva ytterligare arkitektoniska överväganden.
                <br><br>
                <sup> 2</sup> Adobe arbetar aktivt med Document DB-integrering för att hantera beständiga lagringsbehov för SaaS. För närvarande kan implementeringar som kräver långsiktig datalagring behöva tillhandahålla och underhålla ytterligare infrastruktur.
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
