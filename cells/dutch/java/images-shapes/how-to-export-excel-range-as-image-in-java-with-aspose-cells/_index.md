---
category: general
date: 2026-10-10
description: Leer hoe je een Excel-bereik als afbeelding exporteert in Java met Aspose.Cells.
  De gids behandelt ook het exporteren van geselecteerde cellen als afbeelding en
  het opslaan van een Excel-werkblad als afbeelding.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: nl
lastmod: 2026-10-10
og_description: Exporteer Excel‑bereik als afbeelding in Java met een stapsgewijze
  oplossing. Inclusief het exporteren van geselecteerde cellen als afbeelding en het
  opslaan van een Excel‑werkblad als afbeelding.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Excel-bereik exporteren als afbeelding in Java – volledige Aspose.Cells‑gids
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Hoe een Excel-bereik exporteren als afbeelding in Java met Aspose.Cells
url: /nl/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel‑bereik exporteren als afbeelding in Java met Aspose.Cells

Als je een **Excel‑bereik als afbeelding wilt exporteren**, leidt deze tutorial je door een volledige Java‑oplossing met de Aspose.Cells‑bibliotheek. Je leert ook hoe je **geselecteerde cellen als afbeelding kunt exporteren** en hoe je **een Excel‑werkblad als afbeelding kunt opslaan** voor rapportage of documentatiedoeleinden.

Een deel van een werkmap naar een afbeelding exporteren elimineert de noodzaak voor externe screenshot‑tools en garandeert pixel‑perfecte resultaten. Aan het einde van deze gids heb je een herbruikbare methode die een PNG (of elk ondersteund formaat) direct naar schijf schrijft, klaar voor opname in PDF‑bestanden, e‑mails of webpagina’s.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* Java 17 of nieuwer geïnstalleerd.
* Maven 3.8+ (of een ander build‑tool dat Maven‑afhankelijkheden kan verwerken).
* Een Aspose.Cells for Java‑licentie (de gratis evaluatie werkt, maar voegt een watermerk toe).
* Een voorbeeld‑Excel‑bestand (`input.xlsx`) geplaatst in een bekende map.

De volgende secties gaan ervan uit dat je vertrouwd bent met basis‑Java‑ontwikkeling en Maven‑projectopzet.

## Stap 1: Voeg Aspose.Cells toe aan je project

Voeg de Aspose.Cells Maven‑dependency toe aan je `pom.xml`. Deze bibliotheek levert de klassen `Workbook`, `Worksheet` en `ImageOrPrintOptions` die in het code‑voorbeeld worden gebruikt.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Houd het versienummer up‑to‑date; nieuwere releases voegen ondersteuning voor extra formaten en prestatie‑verbeteringen toe.

## Stap 2: Maak een hulpfunctie om een bereik te exporteren

Het encapsuleren van de exportlogica in een methode maakt het eenvoudig om deze te hergebruiken in verschillende projecten en om randgevallen zoals samengevoegde cellen of verborgen rijen af te handelen.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Waarom deze methode belangrijk is

* **Scheiding van verantwoordelijkheden:** Laden, opties configureren en exporteren zijn duidelijk gescheiden.
* **Flexibiliteit:** Je kunt het afbeeldingsformaat of de DPI wijzigen zonder de kernlogica aan te passen.
* **Foutafhandeling:** Het gooien van `Exception` laat de aanroeper beslissen of hij wil loggen, opnieuw proberen of afbreken.

## Stap 3: Roep de methode aan met echte parameters

Hieronder staat een minimale `main`‑methode die laat zien hoe je **geselecteerde cellen als afbeelding kunt exporteren** en ook hoe je **een Excel‑werkblad als afbeelding kunt opslaan** door het volledige bladbereik te gebruiken.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Verwachte output

Het uitvoeren van het programma maakt twee PNG‑bestanden aan:

* `range.png` – een afbeelding die alleen de cellen **A1:G20** bevat.
* `full_sheet.png` – een afbeelding van het volledige gebruikte gebied van het eerste werkblad, effectief **een Excel‑werkblad als afbeelding opslaan**.

Je kunt de bestanden openen met elke afbeeldingsviewer om te verifiëren dat de visuele lay‑out overeenkomt met de weergave in Excel, inclusief celranden, kleuren en samengevoegde cellen.

## Stap 4: Veelvoorkomende randgevallen afhandelen

### 1. Samengevoegde cellen

Aspose.Cells behoudt automatisch de weergave van samengevoegde cellen, maar als je de rendering wilt controleren, stel dan `options.setOnePagePerSheet(true)` in om het volledige blad op één pagina te forceren vóór het exporteren.

### 2. Verborgen rijen of kolommen

Standaard worden verborgen rijen/kolommen niet gerenderd. Om ze wel op te nemen, schakel je het volgende in:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Grote bereiken en geheugenverbruik

Het exporteren van zeer grote bereiken kan veel geheugen verbruiken. Als je een `OutOfMemoryError` tegenkomt, overweeg dan:

* De DPI verlagen (`options.setHorizontalResolution(150)`).
* Het bereik in kleinere stukjes exporteren en de afbeeldingen vervolgens samenvoegen met een grafische bibliotheek.

## Stap 5: Het resultaat programmatisch verifiëren (optioneel)

Als je downstream‑proces moet bevestigen dat de afbeelding correct is gegenereerd, kun je de PNG laden met `javax.imageio.ImageIO` en de afmetingen controleren:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Een breedte en hoogte groter dan nul duiden op een geslaagde export.

## Conclusie

Je weet nu hoe je **een Excel‑bereik als afbeelding kunt exporteren** in Java, hoe je **geselecteerde cellen als afbeelding kunt exporteren**, en hoe je **een Excel‑werkblad als afbeelding kunt opslaan** met Aspose.Cells. De herbruikbare `exportRangeAsImage`‑methode abstraheert de complexiteit, laat je de beeldkwaliteit regelen en werkt met elke werkblad‑index of celbereik.

Vervolgstappen die je kunt onderzoeken:

* Converteer de PNG naar PDF met Aspose.PDF voor rapportage.
* Verwerk meerdere werkmappen in één map batch‑gewijs.
* Integreer de afbeeldingsexport in een Spring Boot REST‑endpoint zodat cliënten afbeeldingen op aanvraag kunnen ophalen.

Voel je vrij om te experimenteren met verschillende afbeeldingsformaten (`ImageFormat.JPEG`, `ImageFormat.BMP`) en DPI‑instellingen om te voldoen aan de visuele eisen van je project. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Export Excel Workbook als afbeelding met Aspose.Cells voor Java: Een stap‑voor‑stap gids](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Hoe maak je een Excel‑grafiek met trendlijn en exporteer je deze naar afbeelding met Aspose.Cells voor Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel‑cellen naar afbeelding met Aspose.Cells .NET: Een stap‑voor‑stap gids](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}