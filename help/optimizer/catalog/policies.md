---
title: Profiler
description: Lär dig hur du använder principer för att filtrera data i en kanal för att se till att data skickas till rätt mål.
hide: true
recommendations: noCatalog
exl-id: 05bbad1a-d612-41a4-9575-543f507089c3
source-git-commit: a731d978aa180633431b0dd9dde5439c286461a2
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Profiler

>[!NOTE]
>
>I den här dokumentationen beskrivs en produkt vid utveckling av tidig åtkomst och den återspeglar inte alla funktioner som är avsedda för allmän tillgänglighet.

Profiler är dataåtkomstfilter i kanaler som ytterligare finjusterar data som skickas till varje kanal. Profiler säkerställer att rätt innehåll skickas till rätt mål. Exempel: försäljningsställe fysiska butiker, marknadsplatser, reklamledningar (Google, Facebook, Instagram).

Profilerna baseras på produktattribut, t.ex. varumärke, modell eller artikelkategori, och används för att anpassa katalogdata så att de uppfyller specifika affärskrav. &#x200B;

## Filter

Filter är den mekanism i en policy som tillämpar katalogsegmentering. Med filter kan företag skräddarsy butiker och kanaler efter specifika produktuppsättningar baserat på verksamhetens behov. Du använder kriterier som produktattribut, operatorer och värden för att definiera en regel eller ett villkor som anger vilka produkter som inkluderas eller exkluderas i en kanal eller butik.

### Delar till ett filter

Ett filter består av följande delar:

| Part | Beskrivning | Exempel |
|---|---|---|
| **Attribut** | Det produktattribut som används för filtrering. | `part_category` |
| **Operator** | Villkoret som används i attributet. | `IN`, `EQUALS`, `CONTAINS` |
| **Värdekälla** | Anger om värdena är `STATIC` eller `TRIGGER`. | `STATIC` [Läs mer](#value-source-types) |
| **Värde** | De specifika värden som uppfyller villkoret. | `brakes, suspension` |

### Exempel

Ett filter med attributet `part_category`, operatorn `IN` och värdena `brakes, suspension` säkerställer att endast produkter med attributet `part_category` som har värdet `brake` eller `suspension` filtreras och visas av principen.

### Värdekälltyper

Det finns två typer av värdekällor: **STATIC** och **TRIGGER**.

Principer med en **värdekälla** av **STATIC** betraktas som universella principer. De allmänna riktlinjerna definierar upplevelsen av en webbplats som helhet. Det innebär att kanalen alltid kommer att köra den principen. Med andra ord baseras inte körningen av den principen på någon användarinteraktion i butiken.

Principer med en **värdekälla** av **TRIGGER** kallas exklusiva principer. Detta innebär att kanalen bara kör den principen när utlösaren anges i API-anropets huvud. I butiken innebär detta att information visas baserat på vad kunden väljer. I följande bild finns till exempel två listrutor: **Varumärke** och **Modell**.

![Utlös värdekälla på butiken](../assets/policy-trigger.png)

**Varumärke** och **Modell** är definierade utlösare:

- `AC-Policy-Brand`
- `AC-Policy-Model`

Om användaren klickar på listrutan **Varumärke** innehåller rubriken för API-anropet `AC-Policy-Brand`, som är konfigurerad att endast visa produkter som är specifika för principen `AC-Policy-Brand`.

## Skapa princip

I det här avsnittet skapar du en ny profil. Principen kan vara **STATIC** eller **TRIGGER**.

### Skapa en STATISK princip

1. Öppna avsnittet **[!UICONTROL Catalog]** på den vänstra menyn och klicka på **[!UICONTROL Policies]**.

1. Klicka på knappen **[!UICONTROL Add Policy]**.

   En ny sida öppnas där du kan fylla i profilinformationen. &#x200B;

1. Ange namnet på profilen, t.ex. &quot;Cigport Part Categories&quot;.

1. Klicka på knappen **[!UICONTROL Add Filter]**.

   En dialogruta öppnas där du kan lägga till filterinformation.

1. Lägg till filterinformationen. Exempel:

   1. **Attribut** - Ange ett attribut från katalogen. Exempel: &quot;part_category&quot;. Namnet måste exakt matcha namnet på attributet i katalogen.
   1. **Operator** - Välj operatorn. Till exempel **IN**. &#x200B;
   1. **Värde Source** - Välj **STATIC**. &#x200B;
   1. **Värde** - Ange värdena i det attribut du tidigare angav. Exempel: &quot;bromsar, fjädring&quot;. &#x200B;Dessa namn måste exakt matcha namnen på värdena för attributet som du angav tidigare.

1. Klicka på knappen **[!UICONTROL Save]** i dialogrutan med filterinformation. &#x200B;

1. Klicka på åtgärdspunkterna (..) bredvid det filter du skapade och välj **Aktivera**. Här kan du även **redigera**, **inaktivera** eller **ta bort** filtret.

   Kolumnen **Status** visar en grön ikon och ordet&quot;Aktiverad&quot;.

1. Klicka på knappen **[!UICONTROL Save]** om du vill spara den nya profilen. &#x200B; Om knappen inte är aktiv kontrollerar du att profilnamnet har lagts till genom att klicka på pennikonen bredvid **Ny profil**.

1. Om du vill verifiera din nya profil går du tillbaka till listan med profiler genom att klicka på bakåtpilen. &#x200B;Din nya profil visas.

### Skapa en utlösarprincip

1. Öppna avsnittet **[!UICONTROL Catalog]** på den vänstra menyn och klicka på **[!UICONTROL Policies]**.

1. Klicka på knappen **[!UICONTROL Add Policy]**.

   En ny sida öppnas där du kan fylla i profilinformationen. &#x200B;

1. Ange namnet på profilen, t.ex. &quot;Cigport Part Categories&quot;.

1. Klicka på knappen **[!UICONTROL Add Trigger]**.

   Dialogrutan **Utlösarinformation** visas.

1. Ange ett namn för utlösaren, till exempel **AC-Policy-Brand**.

1. Välj **Transporttyp**. **HTTP_HEADER** är för närvarande den enda typ som stöds.

1. Klicka på knappen **[!UICONTROL Save]** för att spara utlösaren.

1. Klicka på knappen **[!UICONTROL Add Filter]**.

   En dialogruta öppnas där du kan lägga till filterinformation.

1. Lägg till filterinformationen. Exempel:

   1. **Attribut** - Ange ett attribut från katalogen. Exempel: &quot;part_category&quot;. Namnet måste exakt matcha namnet på attributet i katalogen.
   1. **Operator** - Välj operatorn. Till exempel **IN**. &#x200B;
   1. **Värde Source** - Välj **UTLÖSARE**. &#x200B;
   1. **Värde** - Ange utlösarnamnet som du skapade tidigare (**AC-Policy-Brand**).

1. Klicka på knappen **[!UICONTROL Save]** i dialogrutan med filterinformation. &#x200B;

1. Klicka på åtgärdspunkterna (..) bredvid det filter du skapade och välj **Aktivera**. Här kan du även **redigera**, **inaktivera** eller **ta bort** filtret.

   Kolumnen **Status** visar en grön ikon och ordet&quot;Aktiverad&quot;.

1. Klicka på knappen **[!UICONTROL Save]** om du vill spara den nya profilen. &#x200B; Om knappen inte är aktiv kontrollerar du att profilnamnet har lagts till genom att klicka på pennikonen bredvid **Ny profil**.

1. Om du vill verifiera din nya profil går du tillbaka till listan med profiler genom att klicka på bakåtpilen. &#x200B;Din nya profil visas.

Om du följer dessa steg skapas profilen och kan länkas till en kanal för att styra synligheten.
