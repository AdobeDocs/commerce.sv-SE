---
source-git-commit: e761e54e7bd7997f3f40b1dfc1293012931111b0
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 5%

---
# Adobe Commerce tekniska dokumentation

Vi välkomnar bidrag från såväl communityn som från Adobe-anställda utanför dokumentationsteamen.

## Adobe Open Source - uppförandekod

Detta projekt har antagit [Adobe Open Source Code of Conduct](code-of-conduct.md) eller [.NET Foundation Code of Conduct](https://dotnetfoundation.org/code-of-conduct). Mer information finns i artikeln [Contributing](contributing.md).

## Om dina bidrag till Adobe-innehåll

Se [Adobe Docs Contributor Guide](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=sv-SE).

Hur du bidrar beror på vem du är och vilken typ av ändringar du vill bidra med:

### Mindre ändringar

Om du bidrar med mindre uppdateringar kan du besöka artikeln och klicka på feedbackområdet som visas längst ned i artikeln, klicka på **Detaljerade feedbackalternativ** och sedan på **Föreslå en redigering** för att gå till markeringskällfilen på GitHub. Använd GitHub-gränssnittet för att göra uppdateringar. Mer information finns i den allmänna [Adobe Docs Contributor-guiden](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=sv-SE).

Mindre korrigeringar och förtydliganden som du lämnar in för dokumentation och kodexempel i den här rapporten omfattas av Adobe användarvillkor.

### Större ändringar eller nya artiklar från communitymedlemmar

Om du är en del av Adobe-communityn och vill skapa en ny artikel eller skicka större ändringar använder du fliken Problem i Git-databasen för att skicka in ett problem för att starta en konversation med dokumentationsteamet. När du har gått med på en plan måste du arbeta med en anställd för att få in det nya innehållet genom en kombination av arbete i det offentliga och privata arkivet.

### Större förändringar för Adobe medarbetare

Om du är teknikskribent, programchef eller utvecklare för en Adobe Experience Cloud-lösning och det är ditt jobb att bidra till eller skapa tekniska artiklar, bör du använda den privata databasen på `https://git.corp.adobe.com/AdobeDocs`.

## Verktyg och inställningar

Deltagare i communityn kan använda GitHub-gränssnittet för grundläggande redigering eller förgrena rapporten för att göra större insatser.

Mer information finns i [Adobe Docs Contributor Guide](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=sv-SE).

## Så här använder du Markdown för att formatera avsnittet

Alla artiklar i den här databasen använder den smaksatta koden GitHub. Om du inte känner till Markdown kan du läsa:

- [Grunderna för markeringar](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [Utskrivbart kalkylblad för markering](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## Förimplementera kopplingar för bildoptimering

Den här databasen innehåller automatiska förimplementeringskopplingar som optimerar bilder innan implementering. **Alla medverkande bör aktivera dessa kopplingar** för att säkerställa konsekvent bildoptimering och minskad databasstorlek.

### Snabbinställningar

När du har klonat databasen kör du:

```bash
.githooks/setup-hooks.sh
```

### Vad krokarna gör

- Identifiera automatiskt mellanlagrade bildfiler (PNG, JPG, JPEG, GIF, SVG)
- Kör `image_optim` för att komprimera och optimera bilder
- Scenoptimerade bilder på nytt automatiskt
- Säkerställ att alla dedikerade bilder optimeras korrekt

### Fördelar

- Minskad databasstorlek
- Snabbare sidinläsning för dokumentation
- Enhetlig bildkvalitet för alla deltagare
- Ingen manuell optimering krävs

Detaljerade installationsanvisningar, felsökning och konfiguration finns i [`.githooks/README.md`](.githooks/README.md).

## Tillgängliga uppspelningsuppgifter

I den här databasen används streckuppgifter som tillhandahålls av `adobe-comdox-exl-rake-tasks` Gem. Om du vill se alla tillgängliga uppgifter kör du:

```bash
cd _jekyll
bundle exec rake --tasks
```
