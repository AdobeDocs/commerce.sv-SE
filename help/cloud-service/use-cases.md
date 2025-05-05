---
title: Användningsexempel
description: Lär dig hur du kan uppnå praktiska användningsfall och affärsscenarier som stöds med  [!DNL Adobe Commerce as a Cloud Service].
role: User, Leader
exl-id: fe961c6d-8bd2-4144-b73b-a3d216a46670
source-git-commit: d5935f4d080c3be1f51bf8916575a3b2f357ee22
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Användningsexempel

{{accs-early-access}}

I följande användningsexempel demonstreras kärnfunktioner och affärsscenarier som stöds av [!DNL Adobe Commerce as a Cloud Service], vilket gör att du kan snabba upp utvecklingen och lansera slagkraftiga upplevelser.

Om du råkar ut för några problem kan du få hjälp i avsnittet [Felsökning](#troubleshooting).

## Förutsättningar

Innan du provar något av dessa användningsfall måste du uppfylla följande krav:

1. [Skapa din Cloud Service-instans](./getting-started.md#create-an-instance) med följande alternativ:
   1. Välj [!UICONTROL **Sandbox**] i listrutan [!UICONTROL **Miljö**].
   1. Välj [!UICONTROL **Adobe Store**] i listrutan [!UICONTROL **Testa data**].
1. [Logga in på ditt Adobe Experience Cloud-konto](https://experience.adobe.com)
1. [Konfigurera din Cloud Service-butik](./storefront.md) med följande alternativ:
   1. Välj [!UICONTROL `adobe-commerce/adobe-demo-store`] som mall.
   1. Välj [!UICONTROL **Välj en tillgänglig instans (Nät -> SaaS)**] som anslutningsmetod.

## Arbetsflöde för kassor

I det här arbetsflödet visas utcheckningsprocessen för en kund som köper en produkt från din butik och hur du som administratör kan bekräfta ordern.

### Aktivera betaltjänster

1. Gå till [!UICONTROL **Inställningar**] > [!UICONTROL **Betalningsmetoder**] i Commerce Admin.

1. Ange `Payment Services Sandbox ID` och `Payment Services Sandbox Key` i avsnittet [!UICONTROL **Allmän konfiguration**]. Du kan få dessa ID:n genom att följa stegen som beskrivs i [Sandbox-introduktion](../payment-services/sandbox.md#sandbox-onboarding)

1. Ställ in listrutan [!UICONTROL **Aktivera**] på [!UICONTROL **Ja**].

1. Klicka på [!UICONTROL **Spara konfiguration**].

### Köpa en produkt

1. Gå till [storefront](./storefront.md) som du skapade i förutsättningarna.

1. Hitta och välj en produkt. Gör de anpassningar som behövs. Klicka sedan på [!UICONTROL **Lägg till i kundvagnen**].

   ![butikssökning](./assets/store-search.png){width="600" zoomable="yes"}

1. Välj kundvagnsikonen för att visa kundvagnen.

   ![lägg till i kundvagn och utcheckning](./assets/add-to-cart-and-checkout.png){width="600" zoomable="yes"}

1. Klicka på [!UICONTROL **Utcheckning**].

   ![klicka på utcheckning](./assets/click-checkout.png){width="600" zoomable="yes"}

1. Ange kontaktuppgifter och leveransinformation. Du kan använda fiktiv information för den här beställningen.

1. Om du vill checka ut väljer du [!UICONTROL **Kontrollera/Pengar-beställning**]. Om du vill använda ett kreditkort använder du ett av [testkorten från Paypal](https://developer.paypal.com/tools/sandbox/card-testing/#link-teststaticcardnumbers). Du kan använda dessa med alla framtida förfallodatum och CVC.

   ![ange information](./assets/enter-details.png){width="600" zoomable="yes"}

   ![kreditkort](./assets/credit-card.png){width="600" zoomable="yes"}

1. Klicka på [!UICONTROL **Montera order**].

### Bekräfta ordern

1. Öppna Commerce Admin: `<your store URL>/admin`.

1. Logga in med din Adobe ID.

1. Navigera till [!UICONTROL **Försäljning**] > [!UICONTROL **Beställningar**].

   ![bekräfta beställning](./assets/confirm-order.png){width="600" zoomable="yes"}

1. Leta efter den ordning du har angett och bekräfta informationen.

   ![beställningsinformation](./assets/order-details.png){width="600" zoomable="yes"}

## Uppdatera butikens innehåll

Skapa, redigera och publicera material direkt i butiken.

1. Öppna [storefront](./storefront.md) som du skapade i förutsättningarna.

1. Öppna Storefront Builder. Genom att navigera till `https://da.live/#/<GitHub User Name>/<Repository Name>/main/da/index.md`.

1. Öppna sidan [!UICONTROL **Index**].

1. Under Carousel-blocket anger du en ny titel genom att redigera raden&quot;Välkommen till Adobe Store-demo&quot;.

1. Klicka på ikonen Skicka och klicka på [!UICONTROL **Förhandsgranska**].

1. Granska förhandsgranskningssidan och klicka på [!UICONTROL **Publicera**].

1. Uppdatera butikssidan och bekräfta att dina ändringar nu är aktiva.

## Sammanhangsbaserad expertis

Med Adobe Commerce kontextuella experimenteringsfunktion kan du skapa och hantera experiment i butiken för att testa olika innehåll och konfigurationer.

### Förutsättningar

* Installera [AEM Sidekick-tillägget](https://www.aem.live/docs/sidekick)

1. Markera indexsidan i Storefront Builder och klicka på [!UICONTROL **Kopiera**].

1. Skapa en [!UICONTROL **experimentmapp**] under huvudmappen genom att klicka på knappen [!UICONTROL **Nytt**] och välja [!UICONTROL **Mapp**].

1. Skapa en mapp med namnet **1234** i mappen [!UICONTROL **experiment**] .

1. Klistra in de två kopiorna av indexsidan i mappen **1234** .

1. Öppna varje sida och döp om dem till&quot;homev1&quot; och&quot;homev2&quot;. Detta är dina [utmanare](https://www.aem.live/docs/experimentation#create-your-challenger-page).

1. Ändra varje sida så att den innehåller olika innehåll. Ändra till exempel hjältebilden eller texten. Du måste kunna identifiera skillnaderna mellan sidorna.

1. Publicera alla dina utmanande sidor.

1. Öppna kontrollsidan, den ursprungliga indexsidan.

1. Lägg till ett nytt block med titeln [!UICONTROL **metadata**].

1. Lägg till följande information i metadatablockets rader

   * Title - Adobe Commerce
   * Beskrivning - en webbutik
   * Experimentera - 1234
   * Experimentera varianter
      * `https://<your-site>.aem.live/experiments/1234/indexv1`
      * `https://<your-site>.aem.live/experiments/1234/indexv2`

   ![metadata-block](./assets/metadata-block.png){width="600" zoomable="yes"}

1. Öppna ett inkodat eller privat surffönster och navigera till huvudsidan.

1. Stäng det privata surffönstret och upprepa föregående steg. Varje gång du öppnar sidan visas en slumpmässig variant som du har skapat.

## Förbättra innehållet i butiken

Med AEM Assets, Adobe Express och Firefly kan du nu snabbt ändra bilderna som visas i butiken i ett enkelt, självstyrt arbetsflöde.

### Förutsättningar

* Kräver åtkomst till AEM Assets, Adobe Express och Adobe Firefly.

### Anpassa bakgrunden i en bild

Tänk dig ett scenario där du snabbt vill ändra bakgrunden i en produktbild. Med kombinationen Adobe Commerce, AEM Assets och Adobe Express kan du göra den här ändringen i några enkla steg.

1. Öppna [storefront](./storefront.md) som du skapade i förutsättningarna och navigera till ett objekt som du vill ändra. Observera artikelns SKU eller produktkod.

1. Öppna [!UICONTROL AEM Assets] genom att markera den i [Adobe Experience Cloud](https://experience.adobe.com/#/home).

   ![aem assets](./assets/select-aem-assets.png){width="600" zoomable="yes"}

1. Klicka på [!UICONTROL Assets].

   ![klicka på resurser](./assets/click-assets.png){width="600" zoomable="yes"}

1. Sök efter objektet med **SKU** eller **produktkod**.

1. Markera det objekt som du vill redigera och klicka på [!UICONTROL **Öppna i Adobe Express**].

   ![öppna i Adobe express](./assets/open-in-adobe-express.png){width="600" zoomable="yes"}

1. Välj [!UICONTROL **Infoga objekt**] på panelen [!UICONTROL **Bild**].

   ![Infoga objekt](./assets/insert-object.png){width="600" zoomable="yes"}

1. Beskriv den bild som du vill lägga till i textrutan. Till exempel &quot;snöpine-träd&quot;.

   ![redigera infogningsobjekt](./assets/insert-object-edit.png){width="600" zoomable="yes"}

1. Justera [!UICONTROL Brush size] och rita där du vill lägga till den genererade bilden. I det här exemplet ritar du runt det befintliga objektet för att markera bakgrunden.

1. Klicka på [!UICONTROL **Generera**] för att visa resultatet.

1. Välj mellan olika resultat genom att markera önskat alternativ och klicka på [!UICONTROL **Behåll**].

1. Klicka på [!UICONTROL **Dina grejer**] för att återgå till bildredigeraren.

1. Klicka på [!UICONTROL **Spara**] för att ange bildtyp.

1. Klicka på [!UICONTROL **Spara**] igen för att spara ändringarna.

1. I dialogrutan [!UICONTROL **Spara resurs**] väljer du Commerce [!UICONTROL **målmapp**].

   ![spara som ny resurs](./assets/save-as-new-asset.png){width="600" zoomable="yes"}

1. Klicka på [!UICONTROL **Spara som ny resurs**] för att spara bilden.

#### Lägg till bilden i Commerce AEM Assets

1. På [navigeringspanelen](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/sites/authoring/basic-handling#navigation-panel) i AEM as a Cloud Service väljer du **Assets** > **Filer** > **Commerce** och klickar på resursen som du skapade i föregående avsnitt.

   ![e-handelsmapp](./assets/commerce-folder.png){width="600" zoomable="yes"}

1. Klicka på [!UICONTROL **Egenskaper**].

   ![egenskaper](./assets/properties.png){width="600" zoomable="yes"}

1. Klicka på fliken [!UICONTROL **Commerce**].

   ![fliken E-handel](./assets/commerce-tab.png){width="600" zoomable="yes"}

1. Kontrollera att [!UICONTROL **Finns den i Adobe Commerce?Fältet**] är inställt på [!UICONTROL **Ja**].

1. Klicka på [!UICONTROL **Lägg till**] och ange den produkt-SKU som du vill lägga till resursen i.

   ![lägg till i sku](./assets/add-to-sku.png){width="600" zoomable="yes"}

1. Välj positionen för resursen och resurstypen.

1. Välj fliken [!UICONTROL **Grundläggande**] och ändra fliken [!UICONTROL **Granskningsstatus**] till [!UICONTROL **Godkänd**].

   ![Godkänn resurs](./assets/approve-asset.png){width="600" zoomable="yes"}

1. Klicka på [!UICONTROL **Spara och stäng**].

#### Bekräfta bilden i Commerce

1. Gå till [!UICONTROL **Katalog**] > [!UICONTROL **Produkter**] i Adobe Commerce [!UICONTROL **Admin**].

1. Välj den produkt du lade till bilden i föregående avsnitt.

1. Expandera avsnittet [!UICONTROL **Bilder och video**].

   ![bilder och videoklipp](./assets/images-and-videos.png){width="600" zoomable="yes"}

1. Bekräfta att bilden nu finns i listan med bilder.

1. Gå tillbaka till butiken och navigera till sidan för den ändrade produkten.

1. Bekräfta att den nya bilden visas.

   ![bildbekräftelse](./assets/image-confirm.png){width="600" zoomable="yes"}

## Generera variationer

Adobe Commerce Generate Variations använder generativ AI för att automatisera generering av högkvalitativt innehåll, finjustera meddelanden och smidigt publicera material i butiken.

### Generera text

1. Öppna din butiksplats med [Universal Editor](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction).

1. Markera det textblock som du vill redigera.

1. Klicka på [!UICONTROL **Generera variationer**] på panelen [!UICONTROL **Egenskaper**].

1. Klicka på knappen [!UICONTROL **Generera**] .

1. Markera eller anpassa den genererade texten.

1. Klicka på [!UICONTROL **Publicera**] för att uppdatera butiken.

### Generera innehåll och bilder

1. Öppna [Generera variationer](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

1. Välj mallen [!UICONTROL **Hero Banner**].

1. I textrutan [!UICONTROL **Förklara användarinteraktion**] anger du:&quot;Upplevelse för Adobe-anställda och -partners att köpa Adobe-märkta utrustning!&quot;.

1. Ange **www.adobestore.com** i [!UICONTROL **URL:en för domänkunskap**].

1. Klicka på [!UICONTROL **Generera**].

1. Välj en innehållsvariant och klicka på [!UICONTROL **Generera bild**].

1. Välj [!UICONTROL **Bredbild (16:9)**] i listrutan [!UICONTROL **Bildstorlek**].

1. Välj [!UICONTROL **Foto**] i listrutan [!UICONTROL **Innehållstyp**].

1. För referensbilden [!UICONTROL **Style**] väljer du den befintliga bannern för Adobe-butiken.

1. Markera den genererade bild som du vill använda och klicka på [!UICONTROL **Spara**].

1. Upprepa den här processen med andra referensbilder för att generera fler variationer.


## Felsökning

Använd följande förslag för att lösa eventuella problem du stöter på när du provar dessa självstudiekurser.

* Om du behöver hjälp med kommandon eller flaggor:
   1. Kör `aio --help` om du vill visa alla tillgängliga kommandon och flaggor.
   1. Använd flaggan `--help` för specifika kommandon. Exempel:
      * `aio console --help`
      * `aio commerce –help`

* Om du stöter på ogiltiga inloggningsproblem:
   1. Kör `aio config clear `.
   1. Kör `aio auth login –-force `.
   1. Logga in i webbläsaren.
   1. Välj din profil.
   1. Växla tillbaka till terminalen för att fortsätta.

* Om ditt `init`-kommando misslyckas:
   1. Kör `aio api-mesh delete`.
   1. Kör `aio commerce init` igen.

* Om du valde fel organisation, projekt eller arbetsyta innan du kör kommandot `init`:
   1. Kör `aio console org select`.
   1. Kör `aio console project select`.
   1. Kör `aio console workspace select`.

* Om du har en ogiltig klientorganisation:
   1. Avbryt den aktuella CLI-körningen genom att trycka på **Ctrl-C**.
   1. Kör `aio commerce init`.

* Om en ogiltig API Mesh-installation påträffas:
   * Kör `aio api-mesh update mesh-config.json`.
