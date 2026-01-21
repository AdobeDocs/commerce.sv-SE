---
title: Verktyg för massdatamigrering
description: Lär dig hur du använder Bulk Data Migration Tool för att migrera data från din befintliga Adobe Commerce on Cloud-instans till [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce som molntjänst och Adobe Commerce Optimizer-projekt (Adobe-hanterad SaaS-infrastruktur)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: e582ce85b58b57922a8cdd63dbe32bd0f08c64f9
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Verktyg för massöverföring av data

Verktyget för massdatamigrering följer en distribuerad arkitektur som möjliggör säker och effektiv datamigrering från PaaS till SaaS-miljöer. Detta verktyg hjälper lösningsimplementatörer att migrera data från en befintlig Adobe Commerce on Cloud-instans (PaaS) till [!DNL Adobe Commerce as a Cloud Service] (SaaS). För mer information om migrationsprocessen, se översikten[&#x200B; över &#x200B;](./overview.md)migration.

>[!NOTE]
>
>Verktyget för bulkdatamigrering stödjer migrering av kärndata från förstapartshandeln enbart. Anpassad datamigrering stöds för närvarande inte.

Följande bild visar arkitekturen och nyckelkomponenterna för användning av verktyget för massöverföring av data.

![Arkitekturdiagram för Bulk Data Migration Tool som visar PaaS till SaaS-dataflöde](../assets/bulk-data-diagram.png){zoomable="yes"}

## Migreringsarbetsflöde

Arbetsflödet för massöverföring av data består av följande steg:

1. Skapa en ny miljö för din migration.
1. Kopiera dina data från ditt gamla system.
1. Flytta din data till det nya systemet.
1. Gör din produktkatalog tillgänglig i det nya systemet.
1. Bekräfta att dina data migrerades korrekt.

Följande avsnitt beskriver dessa steg i detalj.

## Få tillgång till bulkdatamigreringsverktyget

Tillgängligheten för bulkdatamigreringsverktyget är följande:

- **Q1 2026** (ännu inte tillgängligt) - Efter den initiala lanseringen av bulkdatamigreringsverktyget kommer du att kunna komma åt det genom att skicka in ett supportärende.
- **Q1 2026** (ännu inte tillgängligt) - Efter den offentliga lanseringen av verktyget för massdatamigrering kommer det att vara tillgängligt från denna sida.

## Skapa målmiljö

Lösningsimplementatören (SI) skapar en målmiljö för migreringen. Denna miljö lagrar data som migrerats från källinstansen.

Först, [skapa en ny [!DNL Adobe Commerce as a Cloud Service]  (SaaS)-instans](../getting-started.md#create-an-instance).

### Konfigurera extraktionsverktyg

Använd extraktionsverktyget för att extrahera data från källinstansen.

1. Ladda ner extraktionsverktyget från länken som Adobe tillhandahåller.
1. Sätt följande miljövariabler i extraktionsverktyget:
   - Anslutningsdetaljer till din befintliga MySQL-databas
   - Mål-tenant-ID:t för din [!DNL Adobe Commerce as a Cloud Service] instans
   - Dina IMS-meriter, inklusive:
      - Klient-ID
      - Klienthemlighet
      - IMS-sikten
      - IMS URL – Bas-URL:en. Till exempel, `https://ims-na1.adobelogin.com/`.
      - IMS organisations-ID

   För IMS-scopes och andra värden, välj din OAuth-typ i **avsnittet Credentials** i ditt projekt i [Adobe Developer Console](https://developer.adobe.com/console/). Mer information finns i `.example.env` filen som ingår i extraktionsverktyget.

### Extrahera data

Innan extraktionsverktyget körs måste lösningsimplementatören etablera en SSH-tunnel till PaaS-databasen med hjälp av:

```bash
magento-cloud tunnel:open
```

Kör sedan extraktionsverktyget, som kommer:

1. Koppla upp dig till PaaS-databasen, analysera dess schema och jämför det med detaljerna i SaaS-hyresgästschemat.
1. Generera en extraktions- och transformationsplan baserad på de gemensamma schemaelementen mellan PaaS och SaaS.
1. Extrahera data med Catalog Data Management Service (CDMS).

### Lastdata

Kör verktyget för att ladda data som tillhandahålls av Adobe. Detta verktyg kommer:

1. Koppla upp dig mot SaaS-hyresgästdatabasen med ett migreringskonto.
1. Skapa en laddningsplan.
1. Genomför planen och flytta data i batcher till SaaS-hyresgästdatabasen.
1. Bearbeta katalogmedia och överför det till målmiljön.
1. Töm SaaS Redis-cachen och ogiltigförklara databasindex för hyresgästen.

### Katalogdatainsamling

Efter att datan laddats flödar katalogdata automatiskt från SaaS-hyresgästdatabasen till Katalogtjänsten.

Katalogtjänsten delar denna data med Live Search och Produktrekommendationer. Ingen manuell intervention krävs för denna process. Datan finns tillgänglig i alla tjänster när insamlingen är klar.

### Verifiering av dataintegritet

Efter migreringen utför CDMS följande automatiska dataintegritetskontroller för att säkerställa noggrannheten och fullständigheten hos de migrerade datan:

**API-baserad verifiering**

Under verifieringen jämför CDMS REST- och GraphQL API-svar från tidigare körda frågor med motsvarande poster från målinstansen. Eventuella avvikelser är synliga i migrationsstatusen.

**Verifiering på databasnivå**

Under verifieringen räknar CDMS antalet extraherade poster och jämför det antalet med mängden inlästa poster.

**On-demand-verifiering (valfritt)**

Du kan också manuellt utlösa omfattande verifiering av alla systemposter:

>[!NOTE]
>
>Denna process är resurskrävande och bör endast användas i sandlådemiljöer.

Den fullständiga verifieringen inkluderar:

- Fullständig API-baserad verifiering med alla förextraherade REST- och GraphQL API-svar
- Detaljerad rapport över eventuella inkonsekvenser som hittats
