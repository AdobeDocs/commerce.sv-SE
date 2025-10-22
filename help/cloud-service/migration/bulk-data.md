---
title: Migreringsverktyg för massdata
description: Lär dig hur du använder verktyget för datamigrering (Bulk Data Migration) för att migrera data från din befintliga Adobe Commerce på molninstansen till  [!DNL Adobe Commerce as a Cloud Service].
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/sv/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
role: Developer
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Migreringsverktyg för massdata

Migreringsverktyget för gruppdata följer en distribuerad arkitektur som möjliggör säker och effektiv datamigrering från PaaS till SaaS-miljöer. Det här verktyget är utformat för att lösningsimplementerare ska kunna migrera data från en befintlig Adobe Commerce på Cloud-instans (PaaS) till [!DNL Adobe Commerce as a Cloud Service] (SaaS). Mer information om migreringsprocessen finns i [migreringsöversikten](./overview.md).

>[!NOTE]
>
>Massdatamigreringsverktyget har bara stöd för migrering av förstahandsdata för kärnhandel. Anpassad datamigrering stöds för närvarande inte.

Följande bild visar arkitekturen och de viktigaste komponenterna för att använda verktyget för migrering av gruppdata.

![Verktygsarkitektur för massdatamigrering](../assets/bulk-data-diagram.png)

## Arbetsflöde för migrering

Arbetsflödet för massdatamigrering består av följande steg:

1. Konfigurera en ny miljö för din migrering.
1. Kopiera data från ditt gamla system.
1. Flytta era data till det nya systemet.
1. Gör produktkatalogen tillgänglig i det nya systemet.
1. Bekräfta att dina data har migrerats korrekt.

I följande avsnitt beskrivs dessa steg i detalj.

## Få åtkomst till verktyget för massdatamigrering

Följande massdatamigreringsverktyg är tillgängliga:

- **Q4 2025** (ännu inte tillgängligt) - Efter den första versionen av migreringsverktyget för gruppdata kan du komma åt det genom att skicka en supportanmälan.
- **Q4 2025** (ännu inte tillgängligt) - Efter den offentliga versionen av verktyget för migrering av gruppdata kommer det att vara tillgängligt från den här sidan.

## Skapa målmiljö

Solution Implementer (SI) skapar en målmiljö för migreringen. Den här miljön används för att lagra data som migreras från källinstansen.

Först [skapar du en ny  [!DNL Adobe Commerce as a Cloud Service] (SaaS)-instans](../getting-started.md#create-an-instance).

### Konfigurera extraheringsverktyget

Extraheringsverktyget används för att extrahera data från källinstansen.

1. Ladda ned extraheringsverktyget från den länk du får från Adobe.
1. Ange följande miljövariabler i extraheringsverktyget:
   - Anslutningsinformation till din befintliga MySQL-databas
   - Målklient-ID för din [!DNL Adobe Commerce as a Cloud Service]-instans
   - Dina IMS-autentiseringsuppgifter, inklusive:
      - Klient-ID
      - Klienthemlighet
      - IMS-scope
      - IMS URL - Bas-URL. Exempel: `https://ims-na1.adobelogin.com/`.
      - ID för IMS-organisation

   För IMS-omfång och andra värden väljer du OAuth-typen i avsnittet **Credentials** i ditt projekt i [Adobe Developer Console](https://developer.adobe.com/console/). Mer information finns i filen `.example.env` som ingår i extraheringsverktyget.

### Extrahera data

Innan extraheringsverktyget körs måste den som implementerar lösningen upprätta en SSH-tunnel till PaaS-databasen med:

```bash
magento-cloud tunnel:open
```

Kör sedan extraheringsverktyget som:

1. Anslut till PaaS-databasen, analysera dess schema och jämför det med SaaS-klientens schemainformation.
1. Generera en extraherings- och omvandlingsplan baserad på de vanliga schemaelementen mellan PaaS och SaaS.
1. Extrahera data med hjälp av katalogdatahanteringstjänsten (CDMS).

### Läs in data

Kör det inläsningsdataverktyg som tillhandahålls av Adobe. Det här verktyget kommer att:

1. Anslut till SaaS-klientdatabasen med ett migreringskonto.
1. Generera en inläsningsplan.
1. Kör planen och flytta data till SaaS-klientdatabasen gruppvis.
1. Bearbeta katalogmedia och överför dem till målmiljön.
1. Tömmer SaaS Redis-cachen och gör databasindex för klienten ogiltiga.

### Inmatning av katalogdata

När data har lästs in flödar katalogdata automatiskt från SaaS-klientdatabasen till katalogtjänsten.

Katalogtjänsten delar dessa data med Live Search och Produktrekommendationer. Ingen manuell åtgärd krävs för den här processen. Data kommer att finnas tillgängliga i alla tjänster när intaget är slutfört.

### Verifiering av dataintegritet

Efter migreringen utför CDMS följande automatiska dataintegritetskontroller för att säkerställa att migrerade data är korrekta och fullständiga:

**API-baserad verifiering**

Under verifieringen jämför CDMS REST- och GraphQL API-svar från tidigare körda frågor med motsvarande poster från målinstansen. Eventuella avvikelser visas i migreringsstatusen.

**Verifiering på databasnivå**

Under verifieringen räknar CDMS antalet extraherade poster och jämför det antalet med mängden inlästa poster.

**Verifiering på begäran (valfritt)**

Du kan också manuellt aktivera omfattande verifiering av alla systemposter:

>[!NOTE]
>
>Den här processen är resursintensiv och bör bara användas i sandlådemiljöer.

Fullständig verifiering innefattar:

- Fullständig API-baserad verifiering med alla förextraherade REST- och GraphQL API-svar
- Detaljerad rapport om eventuella inkonsekvenser som hittats
