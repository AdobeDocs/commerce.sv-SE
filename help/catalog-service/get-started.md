---
title: Kom igång med  [!DNL Catalog Service]
description: Lär dig hur du får åtkomst till  [!DNL Catalog Service] och kan integrera med klientprogram och tredjepartstjänster.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Kom igång med [!DNL Catalog Service]

När [!DNL Catalog Service] har aktiverats kan du komma åt tjänsten och använda den för att hämta katalogdata, till exempel produkt- och kategoriinformation, från din Adobe Commerce-instans. Tjänsten är tillgänglig som ett GraphQL API som du kan få åtkomst till från Commerce Admin eller från ett klientprogram som stöder GraphQL-frågor.

## Åtkomst till tjänsten

[!DNL Catalog Service] är tillgängligt som ett GraphQL API som du kan få åtkomst till från Commerce Admin eller från ett klientprogram som stöder GraphQL-frågor. Tjänsten är tillgänglig i både SaaS- och PaaS-miljöer.

[!BADGE Endast PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."}

| Miljö | Slutpunkt |
| ------------ | ----------: |
| **Testar** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Produktion** | `https://catalog-service.adobe.io/graphql` |

[!BADGE Endast SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce as a Cloud Service- och Adobe Commerce Optimizer-projekt (SaaS-infrastruktur som hanteras av Adobe)."}

| Miljö | Slutpunkt |
| ----------- | --------:|
| Testning | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| Produktion (ej tillgängligt ännu) | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**URL-struktur för SaaS-slutpunkter**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>` är molnregionen där din instans distribueras.
- `<environment>` är miljötypen, till exempel `sandbox`. Om miljön är produktion utelämnas det här värdet.
- `<tenantId>` är den unika identifieraren för din organisations specifika instans inom Adobe Experience Cloud.

Mer information om hur du använder API:t för katalogtjänsten GraphQL finns i [katalogtjänsten för Adobe Commerce Guide](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) i dokumentationen för *Adobe Commerce Developer*.

## Integrera med en headlessbutik eller tredjepartstjänster

Om du vill integrera med ett headless-lager måste du uppdatera butikskonfigurationen för att kunna kommunicera mellan butiken och [!DNL Catalog Service] för att hämta produkt- och kategoridata.

Om du använder Adobe Commerce storefront i Edge Delivery Services lägger du till katalogtjänstslutpunkten i butikskonfigurationen. Mer information finns i [Edge Delivery Services-dokumentationen](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration).

Om du vill ha mer information om hur du konfigurerar integreringar mellan tjänsten och backend-datakällor läser du i dokumentationen för projektkonfigurationen.

### Brandväggskonfiguration

Om du vill tillåta [!DNL Catalog Service] genom en brandvägg lägger du till `commerce.adobe.io` i tillåtelselista.

## Katalogtjänst och API-nät

Med [API-nät för Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) kan utvecklare integrera privata eller tredjeparts-API:er och andra gränssnitt med Adobe-produkter med hjälp av Adobe IO.

Avsnittet [[!DNL Catalog Service]  och API Mesh](mesh.md) innehåller information om installation och konfiguration.

## Använda Dashboard för datahantering

Använd [Dashboard för datahantering](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) för att övervaka datasynkronisering mellan [!DNL Catalog Service] och din Adobe Commerce-instans. Kontrollpanelen ger insikter i dataöverföringsprocessen, inklusive status för dataexport och en lista över synkroniserade produkter.