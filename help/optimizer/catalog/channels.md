---
title: Kanaler
description: Lär dig hur du använder kanaler för att definiera din detaljhandelsstruktur i meningsfulla affärsgrupper.
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Kanaler

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

Med kanaler kan ni definiera er detaljhandelsstruktur i meningsfulla affärsgrupper. En kanal påverkar produktsynligheten genom att tillämpa specifika regler och filter som avgör vilka produkter som visas i en butik. Dessa policyer kan omfatta attribut som varumärke, modell eller artikelkategori, vilket säkerställer att endast relevanta produkter är synliga för kunderna baserat på kanalkonfigurationen. Dessutom kan kanalerna använda prisböcker för att visa kundspecifika priser och ytterligare anpassa shoppingupplevelsen.

## Lägg till kanal

I det här avsnittet skapar du en kanal. Kontrollera att du redan [har skapat en princip](./policies.md) innan du fortsätter skapa en kanal.

1. Öppna avsnittet **[!UICONTROL Catalog]** på den vänstra menyn och klicka på **[!UICONTROL Channels]**.

![Kanaler](../assets/channels.png)

1. Klicka på **[!UICONTROL Add Channel]**. &#x200B;

1. Fyll i kanalinformationen i formuläret Lägg till kanal i listan:

   * **Namn** - Ange kanalens namn. Exempel: &quot;Celport&quot;. &#x200B;
   * **Omfång** - Lägg till omfång (nationella inställningar). Exempel: &quot;en-US&quot;. Tryck på tangenten **enter**.
   * **Profiler** - Använd listrutan för att välja relevanta profiler. Exempel: &quot;Varumärke&quot;, &quot;Modell&quot;. &#x200B;Kontrollera att du redan [har skapat en princip](./policies.md).

1. Klicka på **[!UICONTROL Add]** för att skapa kanalen. &#x200B;

   Om knappen **[!UICONTROL Add]** inte är aktiv kontrollerar du att omfånget har lagts till korrekt genom att placera markören i omfångsfältet och trycka på **enter** &#x200B;.

Sidan Kanaler uppdateras för att visa den nya kanalen. &#x200B;

![Uppdaterad sida för kanaler](../assets/updated-channels-list.png)

När du har utfört de här stegen konfigureras den nya kanalen så att produkter och priser visas baserat på de omfattningar och profiler du har valt.
