---
title: Sidwidget för produktlista
description: Aktivera och formatera  [!DNL Live Search Product Listing Page Widget]
exl-id: 50ba8046-869a-4071-b3a3-a6392544c07b
source-git-commit: 7684d5cded63f2b0805ee307dff77932607c47eb
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Sidwidget för produktlista

[!DNL Live Search Product Listing Page Widget] (PLP) använder Commerce Services-plattformen för att tillhandahålla en utförlig, sökbar och faktablad produktlistsida. I det här avsnittet beskrivs hur du aktiverar och formaterar PLP-widgeten.

## Aktivera PLP-widgeten

När tjänsten [!DNL Live Search] är installerad konverteras standardsökfunktionen automatiskt till [!DNL Live Search].

PLP-widgeten [!DNL Live Search] är aktiverad som standard för nya installationer.

Om du uppgraderar [!DNL Live Search] och PLP-widgeten redan har inaktiverats, förblir det så. Så här aktiverar du den:
1. Gå till Lager → Inställningar → Konfiguration i Adobe Commerce Admin.
1. Klicka på **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]** i den vänstra navigeringen.
1. Klicka på avsnittet [!UICONTROL Storefront Features].
1. Ange [!UICONTROL Enable Product Listing Widget] = Ja
1. Spara konfiguration
1. Om du uppmanas till det tömmer du cachen (gå till System > Verktyg > Cachehantering > [!UICONTROL Flush Magento Cache]).

>[!IMPORTANT]
>
>När [!DNL Live Search Product Listing Page Widget] är aktiverat går det inte att ändra sorteringsordningen på en produktlistsida.

## Widgetfunktioner

PLP-widgeten har följande färdiga funktioner:

- Knapparna Lägg till i kundvagnen - endast för enkla produkter.
- Flera bilder per produkt - Bilden kan ändras när en annan färg väljs för en konfigurerbar produkt.
- Stöd för färgrutor - Observera att färgattributet måste vara stavat `color` för att koden ska kunna valideras korrekt.

### Anpassa widgeten

Utöver de färdiga funktionerna i PLP-widgeten kan du anpassa widgeten ytterligare och inkludera följande funktioner:

- Filtrera efter attribut
- Stöd för flera språk
- Prisreglage

Information om hur du anpassar PLP-widgeten för att hantera ovanstående funktioner finns i `storefront-product-listing-page` Viktigt i följande [databas](https://github.com/adobe/storefront-product-listing-page/). Viktigt i den här databasen innehåller ett exempel på hur du anpassar PLP-widgeten och distribuerar anpassningarna till din plats.

>[!WARNING]
>
>Om du anpassar PLP-widgeten med koden som finns i rapporten ansvarar du för underhållet och de uppdateringar som behövs. Alla nya PLP-widgetfunktioner som Adobe-releaser kan vara inkompatibla med din anpassade implementering.

## Exempel på format

Du kan anpassa utseendet och känslan för PLP-widgeten så att den matchar webbplatsen med [CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/).

>[!NOTE]
>
>Element med anpassade klasser inom ett Adobe Commerce-tema ärvs inte. Dessa element måste ha en specifik klass som mål för att matcha de anpassade klasserna. De primära åtgärdsklasserna fungerar inte med en widgetknapp. Allmänna målelement i CSS ärvs; `button` gäller för widgetknappar.

De markerade diven innehåller målklassen `ds-sdk-product-item__product-name`.

![Sidnumrering](assets/plp-css-example.png)

Anpassa produktnamnet genom att lägga till en regel som gör dem till stora bokstäver.

```css
.ds-sdk-product-item__product-name {
 text-transform: uppercase;
}
```

![Sidnumrering](assets/plp-css-example-after.png)

## CSS-klasser

### Produktlista

- `.ds-sdk-product-list`: Yttre div
- `.ds-sdk-product-list__grid`: Inre div

![Sidnumrering](assets/plp-css-product-list.png)

#### Sidnumrering av produktlista

- `.ds-plp-pagination`

![Sidnumrering](assets/plp-css-pagination.png)

- `.ds-plp-pagination_item`

![Sidnumreringsobjekt](assets/plp-css-pagination-item.png)

- `.ds-plp-pagination_item--current`

![Sidnumrering av aktuellt objekt](assets/plp-css-pagination-item-current.png)

### Widgetar

- `.ds-widgets`: Yttre div
- `.ds-widgets__actions`: inre div på vänster sida
- `.ds-widgets__results`: Inre div på höger sida

![Widget-resultat](assets/plp-css-widgets.png)

### Sortera-listrutan

- `.ds-sdk-sort-dropdown`

![Sorteringslistrutan](assets/plp-css-dropdown.png)

- `.ds-sdk-sort-dropdown__button`

![Nedrullningsknapp](assets/plp-css-dropdown-button.png)

- `.ds-sdk-sort-dropdown__items`

![Listruteobjekt](assets/plp-css-dropdown-items.png)

- `.ds-sdk-sort-dropdown__items--item`

![Listruteobjekt](assets/plp-css-dropdown-item.png)

- `.ds-sdk-sort-dropdown__items--item-selected`

![Listruta för markerat objekt](assets/plp-css-dropdown-selected.png)

- `.ds-sdk-sort-dropdown__items--item-active`

![Aktiv markering i listruta](assets/plp-css-dropdown-active.png)

### Fasetter

- `.ds-plp-facets`
- `.ds-plp-facets__header`
- `.ds-plp-facets__header_title`
- `.ds-plp-facets__header__clear-all`

![Rubrik för ansikten](assets/plp-css-facets-title-clear.png){width="350"}

- `.ds-plp-facets__pills`
- `.ds-sdk-pill`

![Faktablad](assets/plp-css-facets-pill.png){width="350"}

- `.ds-sdk-pill__label`
- `.ds-sdk-pill__cta`

![Fasettetikett](assets/plp-css-pill-label-cta.png){width="350"}

- `.ds-plp-facets__list`

![Fasettlista](assets/plp-css-facets-list.png){width="350"}

- `.ds-sdk-input`
- `.ds-sdk-input__label`
- `.ds-sdk-product-item__product-swatch-group`
- `ds-sdk-product-item__product-swatch-item`
- `.ds-sdk-input_fieldset_show-more`

![Indata](assets/plp-css-sdk-input.png)

- `.ds-sdk-labelled-input`

![Etiketterade indata](assets/plp-css-labelled-input.png)

- `.ds-sdk-labelled-input__input`
- `.ds-sdk-labelled-input__label`

![Indataetikett](assets/plp-css-labelled-input-label.png)

### Produktartikel

- `.ds-sdk-product-item`
- `.ds-sdk-product-item__image`
- `.ds-sdk-product-item__product-name`
- `.ds-sdk-product-item__product-options`
- `.ds-sdk-product-price`
   - `.ds-sdk-product-price--no-discount`
   - `.ds-sdk-product-price--grouped`
   - `.ds-sdk-product-price--bundle`
   - `.ds-sdk-product-price--discount`

![Produkt](assets/plp-css-product.png)

### Läser in

- `.ds-sdk-loading`
- `.ds-sdk-loading__spinner`
- `.ds-sdk-loading__spinner-label`

![Läser in indikator](assets/plp-css-loading.png)

## Inaktivera PLP-widgeten

Så här inaktiverar du PLP-widgeten:

1. Gå till **Store** > Inställningar > **Konfiguration** > **[!DNL Live Search]** > **StoreFront Features** och ställ in **Aktivera produktlistwidgetar** på Nej.
1. Välj **Spara konfiguration** om du vill spara inställningen.
