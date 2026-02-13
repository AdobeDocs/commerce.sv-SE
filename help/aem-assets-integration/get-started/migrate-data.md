---
title: Migrera mediefiler till AEM
description: Migrera mediefilerna från Adobe Commerce eller en extern källa till AEM Assets DAM.
feature: CMS, Media, Integration
exl-id: ccb13e90-8b18-4f1e-94ce-f0dacea2f617
source-git-commit: ac880333814d9d9a45e658e2a637cd9634dbfb1f
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Migrera mediefiler till AEM Assets DAM

Både Adobe Commerce och Adobe Experience Manager (AEM) har inbyggda funktioner för att effektivisera migreringen av mediefiler från Commerce till AEM Assets **digitala resurshanteringssystem (DAM)**. Du kan också migrera mediefiler från andra källor.

## Förutsättningar

| Kategori | Krav |
|----------|-------------|
| **Systemkrav** | <ul><li>AEM as a Cloud Service-miljö etablerad med AEM Assets</li><li>Tillräcklig lagringskapacitet</li><li>Nätverksbandbredd för stora filöverföringar</li></ul> |
| **Nödvändig åtkomst och behörigheter** | <ul><li>Administratörsåtkomst till AEM Assets as a Cloud Service</li><li>Tillgång till källsystemet där mediefiler lagras (Adobe Commerce eller externt system)</li><li>Lämpliga behörigheter för åtkomst till molnlagringstjänster</li></ul> |
| **Molnlagringskonto** | <ul><li>AWS S3 eller Azure Blob Storage-konto</li><li>Privat behållare/bucket-konfiguration</li><li>Autentiseringsuppgifter</li></ul> |
| **Source Content** | <ul><li>Organiserade mediefiler klara för migrering</li><li>Bild- och videofiler i <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">format som stöds av AEM Assets</a>.</li><li>Rena, duplicerade resurser</li></li> |
| **Förberedelse av metadata** | <ul><li><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">AEM Assets metadataprofil har konfigurerats för Commerce-resurser</a></li><li>Mappade metadatavärden för varje resurs</li><li>CSV-filredigerare (t.ex. Microsoft Excel)</li></ul> |

## Bästa praxis för migrering

1. Kuratera resurser före migrering genom att ta bort oanvänt och duplicerat innehåll.

1. Ordna materialet logiskt efter storlek, format eller skiftläge.

1. Överväg att dela upp stora migreringar i mindre grupper.

1. Schemalägg resurskrävande import under tider med låg belastning.

1. Validera metadatamappning före fullständig import.

## Arbetsflöde för migrering

Följ migreringsarbetsflödet för att exportera mediefiler från Adobe Commerce eller något annat externt system och importera dem till AEM Assets DAM.

### Steg 1: Exportera innehåll från den befintliga datakällan

[!BADGE Endast PaaS]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."}

För Adobe Commerce-handlare kan modulen **Fjärrlagring** underlätta import och export av mediefiler. Med den här modulen kan företag lagra och hantera mediefiler med hjälp av fjärrlagringstjänster som AWS S3. Mer information om hur du konfigurerar fjärrlagring för din Commerce-instans finns i [Konfigurera fjärrlagring](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3) i **Konfigurationshandboken för Commerce**.

Om du har mediefiler lagrade utanför Adobe Commerce kan du överföra dem direkt till någon av de [datakällor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites) som stöds av AEM as a Cloud Service.

### Steg 2: Skapa en CSV-fil för metadatamappning

Skapa en CSV-fil som mappar alla mediefiler till Commerce produktdata. Välj någon av följande metoder:

* **Adobe Commerce (PaaS)**: Använd CLI-kommandot för att automatiskt generera CSV-filen från katalogen
* Skapa CSV-filen manuellt

#### Exportera metadata med CLI

[!BADGE Endast PaaS]{type=Informative tooltip="Gäller endast Adobe Commerce i molnprojekt (Adobe-hanterad PaaS-infrastruktur)."}

Använd kommandot AEM Assets Integration CLI för att automatiskt generera en CSV-metadatafil som innehåller bild-URL:er, positioner och roller från de produktmediefiler som lagras i ditt Commerce-projekt.

1. Visa en lista över tillgängliga kommandon för att verifiera att modulen AEM Assets Integration är installerad:

   ```bash
   bin/magento list aem
   ```

   De anpassade tilläggskommandona visas under `aem` i början av kommandolistan.

1. Kör metadataexportkommandot med ditt AEM-sökvägsprefix:

   ```bash
   bin/magento aem:assets:export:csv <AEM-path-prefix>
   ```

   `<AEM-path-prefix>` är den grundläggande mappsökvägen där dina resurser lagras i AEM Assets DAM (till exempel `/content/dam/commerce/`).

   ```bash
   bin/magento aem:assets:export:csv /content/dam/commerce/
   ```

   Detta skapar en `metadata.csv`-fil i katalogen `var/export` som innehåller bild-URL:er, positioner och roller för varje produktresurs i din Commerce-katalog.

#### Skapa CSV-filen manuellt

För mediefiler som lagras utanför Adobe Commerce skapar du CSV-filen manuellt. Kolumnrubrikerna **måste matcha** fältnamnen som konfigurerats i [AEM Assets-metadataprofilen](configure-aem.md). När du har skapat filen fyller du i raderna med metadatavärden för varje mediefil.

| Metadata | Beskrivning | Värde |
|-------|-------------|--------|
| assetPath | Den fullständiga sökvägen där resursen ska lagras i AEM Assets-databasen.<br><br>Använd sökvägen för att skapa undermappar för att ordna Commerce-resurser, till exempel `content/dam/commerce/<brand>/<type>`. | `/content/dam/commerce/<sub-folder>/..<filename>` |
| commerce:positions | Placering/ordning för resursen i produktgallerier | Flera numeriska värden avgränsade med pipe (&quot;Number: multi&quot;) |
| commerce:isCommerce | Flagga som anger om resursen används i e-handeln | `Yes` |
| commerce:skus | SKU:er för den här resursen | Flera strängvärden avgränsade med pipe (String: multi) |
| commerce:roles | Roller eller typer av bilder för resursen (till exempel `thumbnail`, `main image`, `swatch`) | Flera värden avgränsade med semikolon (t.ex.&quot;miniatyrbild; bild; färgrutebild; liten_bild&quot;) |

+++CSV-kod

Använd det här exemplet på CSV-kod för att skapa filen i en kodredigerare eller ett kalkylbladsprogram som Microsoft Excel.

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### Steg 3: Importera Assets satsvis till AEM Assets

När du har skapat metadatamappningsfilen kan du använda verktyget för massimport i AEM Assets för att importera dina resurser.

Här följer en översikt på hög nivå över hur du använder verktyget.

1. [Logga in i AEM Assets as a Cloud Service-redigeringsmiljö](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem).

1. I Experience Manager-verktygsvyn väljer du **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**.

   ![AEM Assets-redigering](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. Välj **[!UICONTROL Create]** i konfigurationerna för massimport för att öppna konfigurationsformuläret.

   ![AEM Assets-redigering](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. Konfigurera och spara konfigurationen.

   Du behöver:

   * Autentiseringsuppgifter för datakällan
   * Målmappen i AEM Assets där importerade filer lagras
   * Valfritt. Information om MIME-typer, filstorlek och andra parametrar för att anpassa importkonfigurationen
   * Sökvägen till CSV-filen för metadatamappning som du överförde till molnlagringsinstansen.

   Mer information finns i [Konfigurera verktyget Massimport](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool) i *AEM Assets as a Cloud Service-användarhandboken*.

1. När du har sparat konfigurationen använder du verktygen för massimport för att testa och köra importåtgärden.

>[!MORELIKETHIS]
>
> [Videodemo om verktyget Importera satsvis](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> [Tips, bästa praxis och begränsningar](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> [Överför eller importera resurser med API:er &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)
