---
title: Onboarding
description: Läs om kraven och vilka plattformar som stöds i  [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Onboarding

Startprocessen för [!DNL Product Recommendations] kräver åtkomst till serverns kommandorad och består av följande steg. Om du inte är van vid att arbeta via kommandoraden ber du en utvecklare eller systemintegratör att hjälpa till.

- [Implementeringsarbetsflöde](implementation-workflow.md)
- [Installera och konfigurera](install-configure.md)
- [Inställningar](settings.md)
- [Verifiera](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)
- [Mellanlagringsmiljö](staging-environment.md)

## Krav

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Disposition 2

### Plattformar som stöds

- Adobe Commerce On Premise (EE): 2.4.4+
- Adobe Commerce on Cloud (ECE): 2.4.4+

## Slutpunkt

[!DNL Product Recommendations] kommunicerar via slutpunkten vid `https://catalog-service.adobe.io/graphql`.

### Stöd för Page Builder

[!DNL Product Recommendations] kan läggas till på en sida som en Page Builder-innehållstyp. Information om hur du lägger till stöd för Page Builder i produktrekommendationer finns i [Installera och konfigurera](install-configure.md).

Mer information om hur du lägger till [[!DNL Page Builder]  i ](page-builder.md)-innehåll finns i [!DNL Product Recommendations]Integrering[!DNL Page Builder].

### SaaS-prisindexering

Produktrekommendationskunder kan använda [SaaS-prisindexering](../price-index/price-indexing.md), vilket ger snabbare prisändringar och synkroniseringstid.

### Stöd för B2B {#b2bsupport}

B2B-butiker kräver ofta komplex logik som styr synlighet och pris för varje kund eller kundgrupp. [!DNL Product Recommendations] [support](release-notes.md) den här funktionen genom att använda [kategoribehörigheter](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html), [delade kataloger](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) och [kundgruppsspecifika priser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html). Om du t.ex. har dolt vissa kategorier i kundsegmentet för detaljhandeln visas inte rekommendationer för produkter i dessa kategorier för en kund i det segmentet. När du definierar en delad katalog för specifika kundgrupper och företag ser kunderna rekommendationer endast för produkter de har tillgång till. Alla rekommenderade produkter återspeglar korrekt kundgruppsspecifikt pris baserat på varje kunds kundgrupp.

>[!NOTE]
>
>Handläggarna kan anpassa och utöka widgetar eller butikselement med hjälp av [katalogtjänstens](../catalog-service/overview.md) Storefront-API, men eventuella anpassningar är inte möjliga för Adobe supportteam.
