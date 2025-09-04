---
title: Lägg till momsklass, attributuppsättning och lagerattribut
description: Lär dig hur du utökar produktflödesdata så att de innehåller attribut för skatteklassificering, attributuppsättning och avancerade lagerinställningar
role: Admin, Developer
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: 6abfeca68ab67fb11493f78440e09408479e1535
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Lägg till momsklass, attributuppsättning och lagerattribut

Modulen Extra produktattribut i Adobe Commerce utökar produktdatautflöden. Den innehåller ytterligare produktattribut från Adobe Commerce produktkonfigurationer:

* [Skatteklassificering](https://experienceleague.adobe.com/sv/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [Attributuppsättning](https://experienceleague.adobe.com/sv/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [Lager](https://experienceleague.adobe.com/sv/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

När modulen har installerats fungerar den automatiskt. Det hämtar och exporterar ytterligare attribut under produktsynkroniseringen. Ingen ytterligare konfiguration krävs.

## Viktiga fördelar

* **Automatisk förbättring**: Förbättrar produktflöden med attribut för momsklass, attributuppsättning och lager
* **Smidig integrering**: Tillhandahåller viktig kontext för externa system och tjänster
* **Nollkonfiguration**: Fungerar omedelbart efter installation
* **Realtidsuppdateringar**: Synkroniserar automatiskt med produktändringar

## Funktioner och exporterade attribut

Modulen lägger till ytterligare tre attribut till dina befintliga produktdataflöden:

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### &#x200B;1. Information om momsklass (`ac_tax_class`)

**Syfte**: Tillhandahåller information om skatteklassificering för varje produkt

**Dataformat**: Strängvärde som innehåller momsklassnamnet

**Exempelutdata**:

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**Användningsexempel**:

När du exporterar momsklassdata till Commerce katalogtjänster blir dessa data tillgängliga för program som stöder:

* Rapportering om skatteefterlevnad
* Integrering med externa momsberäkningstjänster
* Produktkategorisering för redovisningssystem

### &#x200B;2. Information om attributuppsättning (`ac_attribute_set`)

**Syfte**: Identifierar vilken attributuppsättning som tilldelas varje produkt

**Dataformat**: Strängvärde som innehåller attributuppsättningsnamnet

**Exempelutdata**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**Användningsexempel**:

När du exporterar attributuppsättningsdata till Commerce katalogtjänster aktiveras avancerade funktioner för produkthantering i externa system. Bland dessa funktioner finns:

* Identifiering av produktmall
* Kataloghantering och katalogorganisation
* Systemintegrering från tredje part som kräver kontext för attributuppsättning

### &#x200B;3. Avancerade lagerdata (`ac_inventory`)

**Syfte**: Tillhandahåller lagerhanteringsinställningar för varje produkt

**Dataformat**: JSON-kodad sträng som innehåller lagerkonfiguration

**Inkluderade fält**:

* `manageStock` (boolesk): Anger om arkivhantering är aktiverat
* `cartMinQty` (flyttal): Minsta tillåtna kvantitet i kundvagn
* `cartMaxQty` (flyttal): Högsta tillåtna kvantitet i kundvagnen
* `backorders` (sträng): Bakgrundsprincip. Värdet är något av följande:
   * `"no"`: Inga backorder tillåts
   * `"allow"`: Tillåt kvantitet under 0
   * `"allow_notify"`: Tillåt kvantitet under 0 och meddela kunden
* `enableQtyIncrements` (booleskt): Anger om kvantitetsökningar är aktiverade
* `qtyIncrements` (flytande): Ökningsvärde för obligatorisk kvantitet

**Exempelutdata**:

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**Användningsexempel**:

När du exporterar lagerdata till Commerce katalogtjänster aktiveras avancerade funktioner för lagerhantering i externa system. Bland dessa funktioner finns:

* Integrering med Inventory management
* Valideringsregler för kundvagn
* Optimering av orderprocess
* Anpassning av kundupplevelser

## Förbättrad dataexport

Modulen Extra produktattribut förbättrar befintliga produktflöden. Den integrerar de nya attributdata automatiskt.

* **Produktfeed** (`products`): Förbättrat med tre ytterligare attribut

   * Lägger till attributen `ac_tax_class`, `ac_attribute_set` och `ac_inventory` i varje produktpost
   * Behåller ursprungliga produktdata oförändrade
   * Bevarar bakåtkompatibilitet med befintliga foderkonsumenter

* **Produktattributfeed** (`productAttributes`): Förbättrat med attributmetadata för de nya attributen

   * Registrerar automatiskt metadata för de tre nya attributen i feeden `productAttributes`
   * Tillhandahåller information om attributkonfiguration (datatyper, synlighetsinställningar och så vidare)
   * Hjälper externa system att förstå det nya attributschemat

## Installera tillägget

**Krav**

* PHP 8.1, 8.2, 8.3 eller 8.4
* Adobe Commerce 2.4.4+
* [Adobe Commerce-tillägg för dataexport](manage-extension.md#update-a-module-to-a-specific-version), version 103.4.11 eller senare
* Åtkomst till [repo.magento.com](https://repo.magento.com)

  Mer information om hur du skapar nycklar och får de nödvändiga rättigheterna finns i [Hämta dina autentiseringsnycklar](https://experienceleague.adobe.com/sv/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Information om molninstallationer finns i [Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/sv/docs/commerce-on-cloud/user-guide/develop/authentication-keys).
* Åtkomst till kommandoraden på Adobe Commerce-programservern.

### Installationssteg

Lägg till modulen `adobe-commerce/module-extra-product-attributes` med Composer:

```shell
composer require adobe-commerce/module-extra-product-attributes
```

Detaljerade installationssteg finns i följande handböcker:

* [Installera tillägg på Adobe Commerce i molninfrastrukturen](https://experienceleague.adobe.com/sv/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [Installera tillägget Adobe Commerce lokalt](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extension)

## Synkronisera produktdata

Efter omdistributionen exporterar Adobe Commerce-instansen automatiskt ytterligare data under produktsynkroniseringen. Du kan också använda CLI-kommandona `resync` för att synkronisera omedelbart.

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## Felsökning

**Produkter saknar ytterligare attribut:**

* Kontrollera att modulen är korrekt installerad och aktiverad
* Kör omsynkroniseringskommandona för att uppdatera produktdata
* Kontrollera att produkter har giltiga tilldelningar för momsklass och attributuppsättning

**Lagerdata verkar vara felaktiga:**

* Kontrollera att lagerinställningarna är korrekt konfigurerade i administratören
* Kontrollera om det finns webbplatsspecifika lageråsidosättningar
* Kontrollera att modulen [Inventory management](https://experienceleague.adobe.com/sv/docs/commerce-admin/inventory/guide-overview) fungerar som den ska

Mer information finns i [Inventory management Guide](https://experienceleague.adobe.com/sv/docs/commerce-admin/inventory/guide-overview) i *Adobe Commerce Merchant Documentation*.

**Prestandaproblem:**

* Övervaka prestanda för exportprocess efter installation
* Överväg att schemalägga omsynkronisering under lågtrafikperioder

### Loggning och felsökning

Modulen loggar exportfel och varningar till Commerce standardloggningssystem. Om du råkar ut för problem under produktsynkroniseringen kontrollerar du dataexportloggarna.

Mer information finns i [Granska loggar och felsöka](troubleshooting-logging.md).

