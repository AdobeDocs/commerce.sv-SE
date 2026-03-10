---
title: Konfigurera AEM Assets för Commerce Optimizer
description: Lär dig konfigurera AEM Assets-integrering för  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 7f0970648663331fea2af19b981c4fd3b3aedcaa
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---


# Konfigurera AEM Assets för [!DNL Adobe Commerce Optimizer]

[!BADGE Endast SaaS]{type=Positive tooltip="Gäller endast Adobe Commerce Optimizer-projekt."}

AEM Assets-integrering för [!DNL Adobe Commerce Optimizer] gör det möjligt för handlare att använda AEM Assets som centraliserad lösning för hantering av digitala resurser för produktbilder. Den här guiden beskriver konfigurationen som är specifik för [!DNL Commerce Optimizer].

Till skillnad från Adobe Commerce (PaaS) eller Adobe Commerce as a Cloud Service (ACCS) har [!DNL Commerce Optimizer] inget gränssnitt för administratörskonfiguration. Om du vill aktivera integreringen skapar du en supportanmälan med dina [!DNL Adobe Commerce Optimizer]- och AEM Assets-uppgifter. Adobe Support konfigurerar integreringen och registrerar din klient hos Assets Integration Service.

Följande diagram är en översikt över produktsynkroniseringen mellan [!DNL Adobe Commerce Optimizer] och AEM Assets-integreringen.

![AEM Assets till [!DNL Commerce Optimizer] flow](../assets/aco-asset-sync-architecture.png){width="700"}

Den här integreringen har två huvudflöden:

* **Från AEM Assets**: När en resurs har godkänts, avvisats eller tagits bort flödar händelsen genom Adobe Pipeline till Assets integreringstjänst. Tjänsten matchar resurser till produkter med `match-by-SKU` (metadatadriven) eller en [anpassad matchning (App Builder)](../synchronize/custom-match.md){target=_blank}, och skickar sedan `product-asset`-mappningarna till Commerce Optimizer, där de lagras som produktlager.

* **Från[!DNL Adobe Commerce Optimizer]**: När en produkt uppdateras i [!DNL Commerce Optimizer] flödar händelsen genom Adobe Pipeline till Assets integreringstjänst. Tjänsten synkroniserar alla matchande resursmappningar tillbaka till [!DNL Adobe Commerce Optimizer].

## Förutsättningar

Innan du konfigurerar integreringen bör du kontrollera att du har:

* En aktiv [!DNL Adobe Commerce Optimizer]-instans med berättigande för produktvisuella effekter, eller en AEM Assets-licens med Dynamic Media.
* Tillgång till AEM Assets as a Cloud Service.
* Både [!DNL Commerce Optimizer] och AEM Assets i samma Adobe IMS-organisation.
* Dynamiska media med OpenAPI aktiverat i din AEM Assets-miljö.

## Onboarding

Om du vill integrera AEM Assets-integrering med [!DNL Commerce Optimizer] måste du [skapa en supportanmälan](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

Adobe Support använder informationen i din biljett för att registrera din klient hos Assets Integration Service och konfigurera integreringen.

Inkludera följande information i din supportanmälan:

* **[!DNL Adobe Commerce Optimizer]Klient-ID** (instans-ID) hittades i din [!DNL Commerce Optimizer] URL eller Commerce Cloud Manager-användargränssnitt.
* **AEM program-ID**.
* **AEM miljö-ID**.
* **Matchande regel**: Matcha med SKU eller [extern matchning (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Lager**: Kataloglagernamnet som klienten ska registreras med. Ange ett anpassat namn om det behövs. I annat fall används `AEM-Assets` som standard.
* **Språk**: Katalogkällans språkområde som klientorganisationen ska registreras med (till exempel `en-US`).

>[!IMPORTANT]
>
> Integreringen har stöd för en källa per tenant, vilket är en kombination av en språkinställning och ett lager.

När Adobe Support har bearbetat din biljett konfigureras integreringen och din klientorganisation registreras hos Assets integreringstjänst.

När introduktionen är klar:

1. **Registrering med Assets Integration Service**: Din [!DNL Commerce Optimizer]-klientorganisation har registrerats med Assets Integration Service via [!DNL Adobe Commerce Optimizer] klient-ID, AEM program-ID, AEM miljö-ID och klientorganisation.

1. **Evenemangsprenumeration**: Assets Integration Service prenumererar på:

   * AEM Assets-händelser (resurs godkänd, uppdaterad, borttagen)
   * [!DNL Commerce Optimizer] kataloghändelser (produkten har skapats, uppdaterats)

### Begränsningar

Integrationen [!DNL Commerce Optimizer] har följande begränsningar:

* **Ett lager per handlare** - AEM Assets-integreringen har stöd för ett AEM-Assets-lager per handlare (en källa per innehavare). Det finns för närvarande inget stöd för att konfigurera flera lager per handlare.
* **Endast bilder** - Integreringen stöder inte video eller andra medietyper.
* **Inga kategoribilder** - Kategoribildssynkronisering är inte tillgänglig. Kategoribilder från AEM Assets för Assets Selector (infogning av användargränssnitt) stöds inte.
* **Ingen skillnad mellan flera platser** - Integreringen hanterar inte flera platser. En bild som är kopplad till en produkt visas på samma sätt i alla kanaler och profiler.
* **Bildposition/bildordning** - Bildplacering och bildordning stöds inte.
* **Produkten måste finnas** - Om produkten inte finns i [!DNL Commerce Optimizer] skapas inte lagret för produktresursmappningen.
* **Lagerfält skriver över** - värden i ett lager skriver över baskatalogen. Om ett fält inte skickas i lagernyttolasten kan det skrivas över med ett tomt värde. Använd ett dedikerat lager för AEM Assets-innehåll. Om du återanvänder ett befintligt lager för andra syften kan data gå förlorade.

### Konfigurera din AEM Assets

Installations- och konfigurationsprocessen för [!DNL Commerce Optimizer] är densamma som för Adobe Commerce as a Cloud Service. Se [Konfigurera AEM Assets-projektet med stöd för Commerce-metadata](configure-aem.md) för de fullständiga stegen.

Kontrollera att AEM Assets är klart:

1. **AEM Assets-konfiguration**: Konfigurera Commerce metadataprofil. Se [Konfigurera en metadataprofil](configure-aem.md#configure-a-metadata-profile).

1. **Aktivera dynamiska media**: Verifiera att dynamiska media med OpenAPI-funktioner är aktiverade i din AEM Assets-miljö.

## Konfigurera AEM Assets

Konfigurera din AEM Assets-miljö om du vill aktivera synkronisering av produktresurser.

### Steg 1: Aktivera dynamiska media med OpenAPI

Dynamiska media med OpenAPI måste vara aktiverat i din AEM Assets-miljö. Produktvisningar och nya AEM Assets-licenser gör att du kan aktivera dem via Cloud Manager. Äldre AEM Assets-licenser kräver Adobe Support för att aktiveras. Se [Konfigurera AEM Assets-projektet](configure-aem.md#prerequisites) för mer information om aktiveringssteg.

### Steg 2: Valfritt. Konfigurera Commerce metadataprofil

Ställ in metadataprofilen i AEM Assets för att lagra Commerce-specifika metadata.

Mer information finns i [Konfigurera en metadataprofil](configure-aem.md#step-2-optional-configure-a-metadata-profile).

### Steg 3: Använd metadata på resurser

Lägg till Commerce-metadata i produktbilderna i AEM Assets.

Se [paketinnehållet i AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents) för fältdefinitioner och [Konfigurera en metadataprofil](configure-aem.md#step-2-optional-configure-a-metadata-profile) för konfigurationsstegen.

Resursen måste ha statusen **Approved** för att datasynkroniseringen ska kunna utlösas. Händelsen utlöses inte när enbart metadata sparas.

>[!CAUTION]
>
> Tilldela lagret `AEM-Assets` till din [katalogvy](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view). Om lagret inte är tilldelat kan produktbilddata skrivas över oväntat.

## Synkronisering

När integreringen har konfigurerats synkroniseras `product-asset` mappningar automatiskt.

Mer information finns i [Anpassad automatisk matchning](../synchronize/custom-match.md).

### Exempel på arbetsflöde för Matcha efter SKU

Ett typiskt flöde när du lägger till en befintlig resurs till en ny produkt:

1. Skapa produkten i [!DNL Commerce Optimizer] (via API eller dataöverföring). Produkten kan till en början finnas utan bilder.

1. Öppna den resurs du vill mappa till produkten i AEM Assets.

1. Lägg till produkt-SKU:n i **commerce:skus** -metadata och tilldela bildroller (till exempel `thumbnail`, `image`).

1. Godkänn tillgången för leverans. Detta utlöser händelsen som Assets integreringstjänst bearbetar.

1. Assets Integration Service skickar produktavbildningsmappningen till [!DNL Commerce Optimizer]. Produkten i [!DNL Commerce Optimizer] uppdateras med bilderna från resursen.

1. Kontrollera att bilden visas. Tillåt tid för synkroniseringen att slutföras (vanligtvis inom några minuter), kontrollera produkten i användargränssnittet för [!DNL Commerce Optimizer] (till exempel Datasynkronisering eller katalogvy) eller fråga butiks-API:erna (Katalogtjänst, Live Search, Storefront GraphQL API) för att bekräfta att bilden returneras.

## Hantering av bildroger

När en produkt har flera resurser som använder samma bildroll (till exempel två resurser med rollen `thumbnail`), säkerställer integreringen att endast en resurs behåller den rollen för att undvika dubblettroller i lagret [!DNL Commerce Optimizer] och oväntat butiksbeteende.

**Beteende:** När en uppdatering skickas från AEM Assets tar den senast uppdaterade resursen emot bildrollen (till exempel `thumbnail`) och rollen tas bort från den tidigare resursen som hade den. Detta förhindrar att duplicerade bildroller visas i butiken.

## Mer som detta

* [Produktbilder](../../optimizer/setup/product-visuals.md)
* [Konfigurera AEM Assets-projektet](configure-aem.md)
* [Anpassad automatisk matchning](../synchronize/custom-match.md)
* [AEM Assets Integration - översikt](../overview.md)
