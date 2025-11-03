---
title: '[!DNL Storefront Popover]'
description: ' [!DNL Live Search storefront popover] Returnerar dynamiskt föreslagna produkter och miniatyrbilder.'
exl-id: 240a5333-15e9-4178-ba3c-ae6c62c2238c
source-git-commit: f96e7d8d2a31d5e0f49bd3ac2da320313908a868
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# [!DNL Storefront Popover]

När [!DNL Live Search] är [installerat](install.md) visas en [!DNL popover] i butiken när shoppare skriver i rutan [Sök](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html?lang=sv-SE#quick-search). För varje tecken som skrivs uppdateras [!DNL popover] med förslag på produkter och miniatyrbilder av det översta sökresultatet.

[!DNL Live Search] returnerar resultat för en fråga med minst två tecken. För en partiell matchning är det maximala antalet tecken per ord 20. Det går inte att konfigurera antalet tecken i en sökfråga.

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

>[!TIP]
>
>Lär dig hur du anger produktattribut som sökbara i artikeln [Konfigurera Live Search](workspace.md).

## Sidstorlek [!DNL Popover]

Sidstorleken för [!DNL popover] avgör hur många rader med automatiskt slutförda produkter som kan returneras. Under Live Search-installationen ändras värdet `page_size` till det aktuella värdet för inställningen [&#x200B; Katalogsökning &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html?lang=sv-SE) - `Autocomplete Limit` .

Som standard är värdet för Katalogsökning - Gräns för automatisk komplettering satt till åtta rader (eller rader). Så här ändrar du sidstorleken för [!DNL popover]:

1. Gå till *Store* > Inställningar > **Konfiguration** på sidofältet **Admin**.
1. Expandera **Katalog** i den vänstra panelen och välj **Katalog** i listan med inställningar.
1. Expandera avsnittet *Katalogsökning*.
1. Ange **Gräns för automatisk slutförande** till det antal rader som du vill tillåta i [!DNL popover].
1. Klicka på **Spara konfiguration** när du är klar.

## Exempel på formatering [!DNL Popover]

Du kan anpassa utseendet och känslan för widgeten [!DNL Popover] så att den matchar företagets riktlinjer för varumärkesprofilering.

[!DNL storefront popover] visar alltid produkten `name` och `price` och valet av fält är inte konfigurerbart. [!DNL popover]-element kan emellertid formateras med [&#x200B; CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/)-klasser. Följande deklarationer ändrar till exempel bakgrundsfärgen för behållaren [!DNL popover] och sidfoten.

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## Synlighet för behållare

Den överordnade komponenten för `.livesearch.popover-container` är `.search-autocomplete`.  Klassen `.active` anger behållarens synlighet. Klassen `.active` läggs till villkorligt när [!DNL popover] är öppen.

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

Mer information om formatering av butikselement finns i [CSS (Cascading Style Sheets)](https://developer.adobe.com/commerce/frontend-core/guide/css/) i [Utvecklarhandbok för Fornend](https://developer.adobe.com/commerce/frontend-core/guide/).

## Klassväljare

Du kan använda följande klassväljare för att formatera behållar- och produktelementen i [!DNL popover].

- `.livesearch.popover-container`
- `.livesearch.view-all-footer`
- `.livesearch.products-container`
- `.livesearch.product-result`
- `.livesearch.product-name`
- `.livesearch.product-price`

### Väljare för behållarklass

#### .livesearch.popover-container

![[!DNL Popover] container](assets/livesearch-popover-container.png)

#### .livesearch.view-all-footer

![Visa alla sidfötter](assets/livesearch-view-all-footer.png)

### Produktklassväljare

#### .livesearch.products-container

![Produktbehållare](assets/livesearch-product-container.png)

#### .livesearch.product-result

![Produktresultat](assets/livesearch-product-result.png)

#### .livesearch.product-name

![Produktnamn](assets/livesearch-product-name.png)

#### .livesearch.product-price

![Produktpris](assets/livesearch-product-price.png)

#### .livesearch-produktlänk

![Produktresultat](assets/livesearch-product-link.png)

## Arbeta med ett ändrat tema {#working-with-modified-theme}

Du kan använda [!DNL storefront popover] med ett anpassat [tema](https://developer.adobe.com/commerce/frontend-core/guide/themes/) som ärver de nödvändiga filerna från *Luma*. `top.search`-blocket i `header-wrapper` i modulen `Magento_Search` får inte ändras.

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## Inaktiverar [!DNL popover]

Om du vill inaktivera [!DNL popover] och återställa [snabbsökningsfunktionen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html?lang=sv-SE#quick-search) anger du följande kommando:

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```

## Headless-implementationer

För dem med headless-implementeringar kan du installera [!DNL Live Search popover] med ett [npm-paket](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
