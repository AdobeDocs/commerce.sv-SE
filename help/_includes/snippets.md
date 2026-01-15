---
source-git-commit: a89282dde7bc6221e8fca79af19ac388e010a143
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---
# Commerce-fragment

## ACCS - tidig åtkomst {#accs-early-access}

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

<!--
## Nav hack ACCS {#nav-hack-accs}

>[!BEGINSHADEBOX]

<table style="table-layout:fixed">
  <tr>
    <td style="vertical-align: middle;"><a href="https://developer.adobe.com/commerce/webapi/"><img alt="Developers" src="../assets/icons/developers.svg" /> <strong>Developers</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
  </tr>
</table>

>[!ENDSHADEBOX]
-->

## AEM Assets instansmappning {#aem-assets-instance-mapping}

>[!NOTE]
>
>När du ansluter [!DNL Adobe Commerce as a Cloud Service] till [!DNL AEM Assets] mappas [!DNL AEM Assets]-sceninstansen till din sandbox [!DNL Adobe Commerce as a Cloud Service]-instans och andra icke-produktionsmiljöer. Produktionsinstansen [!DNL AEM Assets] mappas till produktionsinstansen [!DNL Adobe Commerce as a Cloud Service].

## IMS-identitet och information om enkel inloggning {#ims-identity-and-sso-config}

Adobe Commerce identitetshantering och autentisering hanteras av Adobe Identity Management System (IMS) via Adobe Admin Console.

Information om alternativ för identitetskonfiguration, inklusive Adobe ID, Enterprise ID och Federated ID, och instruktioner för hur du konfigurerar enkel inloggning (SSO) för säker åtkomst till Adobe-program finns i [Konfigurera identitet och enkel inloggning](https://helpx.adobe.com/enterprise/using/set-up-identity.html) i *Enterprise Admin Console* -dokumentationen.

## Versionsinformation om ACCS-tjänster och utbyggbarhet {#accs-release}

### Ytterligare versionsinformation

[!DNL Adobe Commerce as a Cloud Service] innehåller de senaste versionerna av marknadsföringstjänster, betaltjänster och utökningsmöjligheter. Använd följande länkar om du vill visa versionsinformationen för var och en:

| Tjänster | Utbyggbarhet | Storefront |
| --- | --- | --- |
| <ul><li>[Katalogtjänst](../catalog-service/release-notes.md)</li><li>[Live Search](../live-search/release-notes.md)</li><li>[Betalningstjänster](../payment-services/release-notes.md)</li><li>[Produktrekommendationer](../product-recommendations/release-notes.md)</li><li>[SaaS-dataexport](../data-export/release-notes.md)</li></ul> | <ul><li>[Administratörsgränssnitt SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API-nät](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[Händelser](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[Versionsinformation](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)</li><li>[Ändra](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/)</li></ul> |
