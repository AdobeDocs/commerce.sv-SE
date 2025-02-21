---
title: Product Stock Management
description: Konfigurera butiksmeddelanden och funktioner som är tillgängliga för kunderna.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Product Stock Management

Som handlare kan du använda lager- och källalternativen för Adobe Commerce [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction). Du kan också använda lösningen för att uppfylla kraven för butiker för att kontrollera andra alternativ för lagertillgänglighet som är relaterade till butiksverksamheten.

- Leveransalternativ i hemmet från Merchant Store

- Tillåt/Tillgängligt för butiksplockning

- UPC/SKU/andra unika produktidentifierare

- Tröskelvärdet slut

- Minska lager från specifika platser vid beställning

Konfigurera alternativ för Product Stock från administratören: **[!UICONTROL Catalog > Products > Select Product]**

## **ProduktStock-alternativ**

| **Fält** | **Beskrivning** | **Omfång** | **Krävs** |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|--------------|
| **Tillgängligt för hemleverans** | <p>Anger tillgänglighet för hemleverans (leverans från butik) för produkten. När det här alternativet är aktiverat kan alla tilldelade butiksplatser med tillgängligt lager för produkten kvalificeras för alternativet Home Delivery. När det här alternativet är inaktiverat är produkten aldrig berättigad till hemleverans.</p>Vanligtvis räcker det att ange det här alternativet på handlarnivå. Det kan dock finnas unika fall för specifika produkter, t.ex. sådana som omfattas av statliga fraktbegränsningar, som inte bör omfattas av systemet för hemleverans.</p> | Webbplats | Nej |
| **[!UICONTROL Available for Store Pickup]** | <p>Ställ in butiksupphämtning för produkten. När det här alternativet är aktiverat är alla tilldelade butiksplatser med tillgängligt lager för produkten berättigade till alternativet Butiksplockning. När produkten är inaktiverad är den aldrig berättigad till Store Pickup.</p><p>Det här alternativet kan vara användbart för att spåra handelslager i systemet som du inte vill sälja från e-handelskanalen.</p> | Webbplats | Nej |
| **[!UICONTROL UPC / SKU / Custom Scannable Identifier]** | Det här attributet ska finnas som ett produktattribut och relateras till inställningen **[!UICONTROL Barcode Source / Barcode Type]**. Det här attributet används för att spåra en skannerbar streckkod för dina produkter. Det här värdet kan skickas när en order skickas till dina butiker för plockning. Butikskollegister kan använda värdet i plocklistan för att matcha produkter på hyllan med en streckkodsskanner. | Butiksvy | Nej |

{style="table-layout:auto"}

## Källor för produktnivålager

| **Fält** | **Beskrivning** | **Omfång** | **Krävs** |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Out of Stock Threshold]** | <p>Ange lagertröskeln för artikeln inom varje källa. När lagret ligger under tröskelvärdet anses det vara utanför lagret vid källan.</p><p>Om du vill använda inställningen för global lagringskonfiguration markerar du alternativet **[!UICONTROL Use Default]**.</p> | Global | Nej |
| **[!UICONTROL Allow Store Pickup]** | <p>Ange uttryckligen om artikeln är tillgänglig för butiksupphämtning, oavsett vilken lagerplatskonfiguration som är tillgänglig eller vilken butiksplats som är tillgänglig.</p><p>Om du vill använda produktnivåinställningen avmarkerar du alternativet [!UICONTROL Use Default] och gör ditt val. I annat fall väljs den här inställningen baserat på konfigurationen för **[!UICONTROL Allow In-Store Pickup]** som är inställd på Stock-källan.</p> | Global | Nej |

{style="table-layout:auto"}

