---
title: RAG-dokumentationstjänst
description: Lär dig använda den AI-baserade dokumentationssöktjänsten för Adobe Commerce-utveckling.
badgeSaas: label="Endast SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Tjänsten Documentation RAG (Beta)

>[!NOTE]
>
>Dokumentationen för RAG-tjänsten finns för närvarande i Beta och upplevelsen kan komma att ändras.

Tjänsten för dokumentation av RAG (Retrieval-Augmented Generation) erbjuder AI-baserade semantiska sökfunktioner i relevant dokumentation för Adobe Commerce och App Builder.

Denna RAG har ett IDE-gränssnitt där du kan ställa frågor om Adobe Commerce och kan ge råd om hur du bäst utvecklar program och andra migreringsåtgärder.

RAG-tjänsten ingår i [Commerce utökningsverktyg](./coding-tools.md) MCP-servern (Model Context Protocol), som är integrerad med Cursor och andra MCP-kompatibla AI-assistenter.

## Tillgänglig dokumentation

I följande tabell beskrivs vilken dokumentation som för närvarande är indexerad av RAG-tjänsten och vilka nyckelord du kan använda för att utlösa sökning i det associerade indexet. Dokumentationen som ingår kommer att fortsätta att utökas i takt med att vi utvecklar tjänsten för högspänningsnät.

| Kategori | Index | Innehåll ingår | Nyckelord |
|-------|---------|---------|------------------------|
| [Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) | commerce-storefront-docs | Edge Delivery Services, insticksprogram, butikskomponenter | storefront, drop-in, EDS, produktlista, utcheckning |
| [Utbyggbarhet](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhooks, event, extensions, integreringar | webkrok, event, extension, API mesh, GraphQL |
| [Commerce](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview) | commerce-core-docs | Commerce (katalog, kunder, beställningar) | katalog, produkt, kund, order, lager |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, körningsåtgärder, UI-tillägg | app builder, runtime action, React Spectrum |

Mer information om indexmarkering finns i [Automatisk indexmarkering](#automatic-index-selection-recommended) och [Explicit indexmarkering](#explicit-index-selection).

Mer information om dokumentationen som ingår i varje index finns i [listan över inkapslade källor](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md).

## Säkerhet och integritet

* **IMS-autentisering** - Alla API-anrop använder Adobe IMS OAuth2-token.
* **Ingen datalagring** - MCP-servern lagrar inga autentiseringsuppgifter eller data.
* **Lokal körning** - Alla verktyg körs lokalt på datorn.
* **Säker kommunikation** - Dokumentationssökningen använder HTTPS med tokenvalidering.

Produktionsslutpunkten skyddas av [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview), som innehåller följande skydd:

* Brandvägg för webbaserade program (WAF) med Microsoft Default RuleSet 2.1 och Bot Manager RuleSet 1.0
* Geografisk blockering för USA:s regioner som är underkastade handelsembargo (Kuba, Iran, Nordkorea, Syrien, Krim, Luhansk, Donetsk)
* DDoS-skydd vid kanten
* API-hantering, backend låst för att endast acceptera trafik från frontdörren

För olika säkerhetskrav kan du använda en anpassad slutpunkt. Mer information finns i [Anpassad frontdörrslutpunkt](#custom-front-door-endpoint).

## Förutsättningar

Kontrollera att du har:

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ (LTS rekommenderas)
* [Markör-IDE](https://cursor.com/download){target="_blank"} (rekommenderas) eller en annan MCP-kompatibel IDE

  >[!NOTE]
  >
  >Även om andra MCP-kompatibla IDE:er stöds rekommenderas Cursor som IDE för att få bästa möjliga upplevelse. Om du använder en annan utvecklingsmiljö måste du ändra anvisningarna och andra steg i dokumentationen för att den ska fungera med den valda utvecklingsmiljön.

## Installation

1. Installera [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) globalt:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Autentisera med Adobe IMS:

   ```bash
   aio auth login
   ```

1. Klona Commerce verktygskatalog för utbyggbarhet och navigera till katalogen:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. Installera beroenden:

   ```bash
   npm install
   ```

1. Skapa eller uppdatera `.cursor/mcp.json` i din Commerce-projektkatalog (inte globalt) så att den inkluderar `commerce-extensibility-tools` MCP-servern:

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   Se till att du ersätter `<your-project-directory>` med den faktiska sökvägen där du klonade databasen.

   >[!NOTE]
   >
   >Om du har problem med att ange sökvägen till din projektkatalog i Windows läser du [Felsökning av sökvägsproblem](#path-issues-windows).

1. Starta om Cursor IDE för att läsa in MCP-servern.

1. Kontrollera installationen genom att fråga AI-assistenten:

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## Användning

När du har installerat kan du anropa indexen [automatiskt](#automatic-index-selection-recommended) eller [explicit](#explicit-index-selection). Du kan också använda kommandot [`/search-commerce-docs`](#command-based-search).

>[!NOTE]
>
>RAG-tjänsten returnerar de fem mest relevanta resultaten.

### Automatiskt indexval (rekommenderas)

Genom att ställa frågor om ditt Commerce-projekt på naturens språk söker verktyget automatiskt i rätt dokumentationsindex och tillhandahåller relevant information:

>[!BEGINSHADEBOX]

Följande uppmaning väljer automatiskt indexvärdet `commerce-storefront-docs`:

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

Följande uppmaning väljer automatiskt indexvärdet `commerce-extensibility-docs`:

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

Följande uppmaning väljer automatiskt indexvärdet `commerce-core-docs`:

```shell-session
"How to configure product catalog settings?"
```

Följande uppmaning väljer automatiskt indexvärdet `app-builder-docs`:

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### Explicit indexmarkering

Du kan också ange det index som du vill använda i uppmaningen.

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### Kommandobaserad sökning

Om du vill vara säker på att RAG-tjänsten används kan du manuellt anropa kommandot `/search-commerce-docs` Cursor för att söka efter dokumentation när du uppmanas till detta:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Anpassad slutpunkt för främre dörr

Som standard används slutpunkten [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) för produktionen med WAF-skydd. För test- och utvecklingssyften kan du åsidosätta detta med miljövariabeln `FRONT_DOOR_URL`.

Om du vill använda en anpassad slutpunkt lägger du till den i MCP-konfigurationen för pekaren:

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>De flesta utvecklare bör använda standardslutpunkten för produktion och behöver inte ange variabeln `FRONT_DOOR_URL`.

## Felsökning

I följande avsnitt finns felsökningstips för vanliga problem som du kan stöta på när du använder dokumentationsverktyget för högdagrar.

### Autentiseringsfel

Dokumentationssökverktyget kräver Adobe IMS-autentisering. Om du råkar ut för autentiseringsfel använder du följande steg för att felsöka och lösa problemet.

1. Kontrollera att du är inloggad:

   ```bash
   aio where
   ```

1. Kontrollera att du kan se din IMS-token:

   ```bash
   aio auth login --bare
   ```

1. Om det fortfarande finns autentiseringsfel provar du att logga ut och sedan in igen:

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP-servern läses inte in

Om MCP-servern inte ansluter, eller om agenten säger att den inte kan ansluta till RAG-nätverket, ska du göra följande för att felsöka och lösa problemet.

1. Öppna markörinställningar med **Cmd,** (macOS) eller **Ctrl,** (Windows och Linux).

1. Sök efter MCP och verifiera att `commerce-extensibility-tools` är listad och aktiverad.

1. Sök efter felmeddelanden på panelen MCP-inställningar.

1. Kontrollera att filen `mcp.json` finns i ditt projekt:

   ```bash
   cat .cursor/mcp.json
   ```

1. Kontrollera att sökvägen är korrekt och absolut:

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### Verktyget hittades inte

1. Avsluta markören och öppna den igen.

1. Kontrollera MCP-serverloggarna i Markörens utvecklarkonsol genom att använda **Cmd+Shift+P** (macOS) eller **Ctrl+Skift+P** (Windows/Linux) och söka efter &quot;Utvecklare: Öppna loggmapp&quot;.

1. Verifiera installationen:

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   Servern ska starta utan fel.

### Problem med sökvägar (Windows)

Använd snedstreck `/` eller omvända snedstreck `\\` i Windows:

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## Ytterligare resurser

* [Adobe Commerce-dokumentation för utvecklare](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [App Builder-dokumentation](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [Modellkontextprotokoll](https://modelcontextprotocol.io/){target="_blank"}
* [Markör-IDE](https://cursor.sh/docs){target="_blank"}
