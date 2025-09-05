---
title: Hantera cookie-begränsningar
description: Läs om hur produktrekommendationer hanterar begränsningar av cookies och efterlevnad av sekretess.
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
source-git-commit: dbb36b9fa800e128f1aea795a891ffbfb751aa76
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# Hantera cookie-begränsningar

Både Adobe Commerce och Magento Open Source ber om samtycke innan data lagras i webbläsarcookies. Mer information finns i [Begränsningsläge för cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=sv-SE).

## Hur produktrekommendationer hanterar cookie-begränsningar

När du distribuerar modulen `magento/product-recommendations` till produktionen börjar den samla in interaktionshändelser för kunder på din butik. Dessa data kan lagras i webbläsarens cookies eller lokala lager för att underlätta rekommendationsalgoritmer.

>[!IMPORTANT]
>
>Produktrekommendationer respekterar nu läget för begränsning av cookies genom att inga data samlas in eller lagras i cookies eller lokal lagring när cookie-begränsningar är aktiverade. Detta inkluderar beteendedata som används för personaliserade rekommendationer.

### Data som påverkas av begränsningar för cookie

Följande produktrekommendationsdata samlas inte in när läget för begränsning av cookies är aktiverat:

- **Beteendedata**: Produktvyer, tilläggsköp, köp och andra kundinteraktioner.
- **Sessionsdata**: Shopparsessionsinformation och enhetsinteraktioner för rekommendationer.
- **Personalization-data**: Data som används för rekommendationstyper som&quot;Nyligen visade&quot; och&quot;Mest köpta&quot;.

### Påverkan på rekommendationstyper

När läget för begränsning av cookies är aktiverat och kunderna inte har accepterat cookies kanske vissa rekommendationstyper inte visas eller kan visa begränsade resultat:

- **Nyligen visade produkter**: Kräver sessionsdata lagrade i cookies/lokal lagring.
- **Rekommenderas för dig**: Kräver beteendedata för personalisering.
- **Köpte detta, köpte**: Kräver inköpshistorik.

>[!NOTE]
>
>Rekommendationstyper som inte förlitar sig på beteendedata, som&quot;Mest visade&quot; och&quot;Visuell likhet&quot;, fortsätter att fungera normalt även om cookie-begränsningar är aktiverade.

## Lösningar för cookie-medgivande från tredje part

Produktrekommendationer kan inte automatiskt integreras med cookie-lösningar från tredje part. Det är handlarens ansvar att se till att datainsamlingen följer gällande integritetslagstiftning och -bestämmelser.

Om du använder en anpassad cookie-medgivandelösning kan du implementera cookie-mekanismen som inte spåras för att styra datainsamlingen.

### Implementera icke-spårade cookies

Du kan använda cookien `mg_dnt` för att programmässigt kontrollera datainsamling:

#### Kaknamn

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### Inaktivera datainsamling

Ange Do-not-track-cookie när användare avböjer cookies:

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### Aktivera datainsamling

Rensa do-not-track-cookie när användare accepterar cookies:

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## Testa läget för begränsning av cookie

Så här testar du hur produktrekommendationer fungerar med begränsningar för cookies:

1. Aktivera läget för begränsning av cookies i din Adobe Commerce-konfiguration.
1. Besök din butik utan att ta emot cookies.
1. Verifiera att rekommendationsenheter visar lämpligt reservinnehåll.
1. Acceptera cookies och verifiera att rekommendationerna börjar samla in data.

## Integritetsefterlevnad

Datainsamling av produktrekommendationer innehåller inte personligt identifierbar information (PII). Alla användaridentifierare, som cookie-ID:n och IP-adresser, anonymiseras. Mer information finns i [Adobe sekretesspolicy](https://www.adobe.com/privacy/policy.html).

>[!TIP]
>
>För vårdkunder som använder datatjänstens HIPAA-tillägg kan ytterligare konfiguration krävas. Mer information finns i [HIPAA-beredskap](../data-connection/hipaa-readiness.md).
