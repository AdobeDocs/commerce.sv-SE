---
title: Anslut instansen
description: Koppla din Commerce-instans med en API-nyckel och en privat nyckel och ange datautrymmet i konfigurationen.
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
feature: Payments, Checkout, Configuration, Paas
badgePaas: label="Endast PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur) och lokala projekt."
source-git-commit: 0f2e9c3a7d990a46bafc5f3b8a083436d42643b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Anslut instansen

Du ansluter din Commerce-instans med en API-nyckel och en privat nyckel, och anger datautrymmet i konfigurationen med [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html). **Du konfigurerar den här anslutningen endast en gång.**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> Mer information finns i videon [[!DNL Adobe Commerce] Services Connector](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en).

* Om du redan har *anslutit din instans* kan du fortsätta med att [konfigurera din testsandlåda](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html) genom att hämta och använda dina API-autentiseringsuppgifter och konfigurera Commerce Services.
* Om du fortfarande *behöver ansluta din instans* läser du informationen i det här avsnittet om hur du [hämtar API-autentiseringsuppgifter](#obtain-api-credentials) och [konfigurerar Commerce Services](#configure-commerce-services).
* Om du är *osäker på om din instans är ansluten* navigerar du till **System** > Tjänster > **Commerce Services Connector** och visar offentliga och privata API-nyckelvärden i avsnitten [!UICONTROL Sandbox Keys] och [!UICONTROL Production Keys] samt fälten *Projekt* och *Data Space* i avsnittet [!UICONTROL SaaS Identifier] . Om dessa värden finns är instansen ansluten.

>[!NOTE]
>
>Alla handlare som är berättigade till betaltjänster kan använda ett produktionsdatautrymme och två testdatamallar.

## Hämta API-autentiseringsuppgifter

Om du vill använda en Commerce SaaS-tjänst måste du använda instansens API-nycklar (Commerce publika API-nyckel och en privat nyckel) för både sandlådan och produktionen, som skapas och hanteras i [Min kontoinstrumentpanel](https://account.magento.com/customer/account/login). [Nyckelparet](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) kan skapas för ett Commerce-konto - ett för sandlådan och ett för produktion - men bara ett par kan användas aktivt åt gången.

>[!NOTE]
>
>Behöver du hjälp med att komma åt din [!UICONTROL My Account]-instrumentpanel? Se [Skapa ett Commerce-konto](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create).

När en offentlig API-nyckel har skapats är den alltid tillgänglig på instrumentpanelen för Mitt konto. Den kan kopieras eller tas bort efter behov. Den privata API-nyckeln blir synlig när du skapar en offentlig API-nyckel för antingen sandlåda eller produktion. Den är bara tillgänglig för kopiering eller sparande från den efterföljande dialogrutan och kan inte nås senare.

Ett givet API-nyckelpar är giltigt för alla Commerce-tjänster i en miljö, så om du redan har konfigurerat Commerce Services för din instans finns API-nyckelparet redan i Commerce Services Connector.

Om API-nyckeln förloras måste ett nytt API-nyckelpar [genereras](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#generate-an-api-key-and-private-key) och [tillämpas](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#configure-saas-project) på Commerce Services Connector-konfigurationen i Admin. Om fel nycklar är konfigurerade eller om det inte finns några i konfigurationen visas en dialogruta med kontoverifieringsfel i Betalningstjänster som meddelar dig om att kontot inte har verifierats.

Visa en [lista över tillgängliga Commerce-tjänster som använder API:t ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas#availableservices).

Mer information om hur du genererar en API-nyckel för antingen sandbox- eller produktionsmiljöer finns i [Referenser](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#apikey).

>[!IMPORTANT]
>
>Vi rekommenderar att du inte genererar om API-nyckelparet *och* ändrar SaaS-identifieraren och/eller datautrymmet för en aktiv produktionsinstans. Du förlorar data för instansen om de ändras.

## Konfigurera Commerce Services

Samma API-nyckel kan användas för alla instanser, men varje instans måste ha sin egen [SaaS-datamängd](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#saasenv).

>[!NOTE]
>
>Handläggarna måste använda samma nycklar som genererats för MageID för sina stödrättigheter.

Nu när du har fått dina inloggningsuppgifter kan du konfigurera ditt SaaS-projekt och Saas Data Space.

1. Gå till **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** på sidofältet _Admin_.
1. Klicka på **[!UICONTROL Configure Commerce Services]**.

   Det här alternativet är synligt om du ännu inte har konfigurerat Commerce Services för ditt konto.

   Du dirigeras till konfigurationsområdet i Admin, **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**, för att konfigurera Commerce Services Connector.

1. Följ stegen som beskrivs i [SaaS-konfigurationen](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html#saasenv) för att konfigurera dina Commerce-tjänster.

   >[!INFO]
   >
   > Mer information finns i videon [[!DNL Adobe Commerce] Services Connector](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en#configuration-faqs).

## Slutpunkt

[!DNL Payment Services] använder [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html) för att ansluta till Commerce Services och distribuera som SaaS. [!DNL Commerce Services Connector] kommunicerar via slutpunkten på:

* `commerce-beta.adobe.io` för sandlådemiljöer.
* `commerce.adobe.io for` för live-miljöer.
