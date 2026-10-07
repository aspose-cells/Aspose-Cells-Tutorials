---
category: general
date: 2026-10-07
description: Leer hoe je een PNG maakt van een bereik en gegevens exporteert als PNG
  in Java. Deze gids laat zien hoe je een Excel‑bereikafbeelding opslaat met Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: nl
lastmod: 2026-10-07
og_description: Maak een PNG van een bereik in Java en exporteer gegevens als PNG
  met Aspose.Cells. Volg deze volledige tutorial om direct een afbeelding van een
  Excel-bereik op te slaan.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: PNG maken vanuit bereik in Java – stapsgewijze Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hoe PNG te maken van een bereik in Java met Aspose.Cells
url: /nl/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PNG te maken van een bereik in Java met Aspose.Cells

Als u **PNG van een bereik wilt maken** in een Excel-werkmap, laat deze tutorial u precies zien hoe u dit doet. Aan het einde van de gids kunt u **gegevens exporteren als PNG**, een Excel‑bereikafbeelding opslaan en het bestand hergebruiken in rapporten of webpagina's.

U ziet een volledige, uitvoerbare Java‑programma dat een werkmap laadt, de gewenste cellen selecteert, ze rendert als een PNG en het resultaat opslaat op schijf. Er zijn geen externe tools nodig—Aspose.Cells behandelt alles intern.

## Wat deze tutorial behandelt

* Voorwaarden en Maven‑configuratie voor Aspose.Cells
* Een werkmap laden die een draaitabel of een willekeurig gegevensbereik bevat
* Het exacte celbereik definiëren dat u wilt converteren
* Afbeeldingsopties configureren voor PNG‑output
* Het bereik renderen en het PNG‑bestand opslaan
* Veelvoorkomende valkuilen en tips voor afbeeldingen van hoge kwaliteit

Na het voltooien van deze stappen kunt u **werkblad naar PNG converteren** voor elk bereik, of het nu een eenvoudige tabel of een complexe draaitabelgrafiek is.

## Voorwaarden

* Java 17 of later (de code compileert met JDK 11+)
* Maven 3.6+ (of Gradle als u dat verkiest)
* Aspose.Cells for Java 23.12 of nieuwer – voeg de hieronder getoonde afhankelijkheid toe
* Een bestaande Excel‑bestand (`PivotWithStyle.xlsx`) dat het bereik bevat dat u wilt vastleggen

> **Pro tip:** Als u geen licentie heeft, kunt u een tijdelijke evaluatiesleutel aanvragen bij Aspose. De bibliotheek werkt in evaluatiemodus zonder extra configuratie.

### Maven‑afhankelijkheid

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Stap 1: Laad de werkmap die het doelbereik bevat

De eerste handeling is het openen van het Excel‑bestand. Aspose.Cells leest het bestand in het geheugen zonder Microsoft Office te vereisen.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Waarom dit belangrijk is*: Het laden van de werkmap geeft u toegang tot werkbladen, cellen en paginainstellings‑eigenschappen die nodig zijn voor het renderen.

## Stap 2: Toegang tot het werkblad dat het bereik bevat

De meeste werkmappen hebben een standaardblad op index 0, maar u kunt ook de bladnaam gebruiken.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Als uw gegevens zich op een ander blad bevinden, vervang dan `0` door de juiste index of gebruik `workbook.getWorksheets().get("SheetName")`.

## Stap 3: Definieer het celbereik dat u wilt converteren

U kunt elk rechthoekig gebied specificeren met A1-notatie. In dit voorbeeld leggen we `A1:D15` vast, wat een draaitabel of een regulier gegevensblok kan zijn.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Randgeval*: Wanneer het bereik samengevoegde cellen bevat, breidt Aspose.Cells de afbeelding automatisch uit om het samengevoegde gebied op te nemen.

## Stap 4: Bereid PNG‑afbeeldingsopties voor

`ImageOrPrintOptions` stelt u in staat het formaat, de resolutie en andere renderdetails te regelen. Het instellen van het opslagformaat op PNG zorgt voor verliesvrije kwaliteit.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Het verhogen van de DPI is nuttig wanneer de broncellen kleine lettertypen of gedetailleerde grafieken bevatten.

## Stap 5: Beperk het rendergebied tot het geselecteerde bereik

Door het bereik als afdrukgebied toe te wijzen, rendert Aspose.Cells alleen die cellen en negeert de rest van het blad.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Als u deze stap overslaat, wordt het volledige werkblad gerasterd, wat geheugen kan verspillen en een grotere afbeelding oplevert.

## Stap 6: Render het bereik en voeg de afbeelding toe aan het werkblad (optioneel)

Als u de gegenereerde PNG terug in de werkmap wilt insluiten (voor preview‑doeleinden), kunt u deze als afbeelding toevoegen. Deze stap is optioneel voor zuivere exportscenario's.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Waarom u dit zou doen*: Sommige workflows vereisen dat de afbeelding deel uitmaakt van de werkmap vóór distributie, bijvoorbeeld het maken van een afdrukbaar rapport dat native cellen en afbeeldingen combineert.

## Stap 7: Sla het PNG‑bestand op schijf op

Schrijf tenslotte de afbeelding naar een bestand. De `save`‑methode respecteert het formaat dat is opgegeven in `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Wanneer het programma eindigt, zal `PivotImage.png` een pixel‑perfecte momentopname van cellen `A1:D15` bevatten.

### Verwachte output

* Een bestand met de naam `PivotImage.png` in `YOUR_DIRECTORY`.
* De afbeelding toont de exacte lay-out, lettertypen, kleuren en randen van het geselecteerde bereik.
* Als het bronbereik een draaitabel bevat, omvat de gerenderde afbeelding dezelfde opmaak en berekende waarden zoals weergegeven in Excel.

## Veelvoorkomende scenario's behandelen

### Een niet‑aaneengesloten bereik exporteren

Aspose.Cells rendert geen niet‑aaneengesloten bereiken in één afbeelding. Om meerdere gebieden te exporteren, maakt u afzonderlijke afbeeldingen voor elk bereik en combineert u ze later met een beeldverwerkingsbibliotheek (bijv. ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Een groot werkblad opslaan als PNG

Het renderen van een volledig blad met duizenden rijen kan veel geheugen verbruiken. Verminder dit door:

* De DPI verlagen (`imageOptions.setResolution(72)`) voor een kleiner bestand.
* `setPageCount` gebruiken om het aantal gerenderde pagina's te beperken.
* Een afdrukbare pagina per keer exporteren via `worksheet.getPageSetup().setPrintArea(...)`.

### Cel‑formules behouden

Een PNG‑afbeelding is een rasterformaat; formules worden niet bewaard. Als downstream‑gebruikers de ruwe gegevens nodig hebben, exporteer dan het bereik ook als CSV of JSON met `Range.exportDataTable()`.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat de volledige Java‑klasse die u kunt kopiëren‑en‑plakken in uw IDE. Vervang `YOUR_DIRECTORY` door een absoluut of relatief pad op uw machine.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Voer het programma uit met `mvn compile exec:java` (of uw favoriete build‑tool). Na uitvoering, open `PivotImage.png` om het resultaat te verifiëren.

## Conclusie

U weet nu hoe u **PNG van een bereik kunt maken** in Java met Aspose.Cells, effectief **gegevens kunt exporteren als PNG** en **een Excel‑bereikafbeelding kunt opslaan** voor elk rapportage‑ of delingsscenario. De stappen—het laden van de werkmap, het definiëren van het bereik, het configureren van afbeeldingsopties, het instellen van het afdrukgebied en het opslaan van het bestand—dekken de volledige workflow voor **werkblad naar PNG converteren** en **cellen opslaan als PNG**.

### Volgende stappen

* Experimenteer met verschillende `Resolution`‑waarden om kwaliteit en bestandsgrootte in balans te brengen.
* Gebruik `ImageOrPrintOptions.setTransparent(true)` als u een PNG met een transparante achtergrond nodig heeft.
* Combineer meerdere bereikafbeeldingen tot één PDF met `PdfSaveOptions` voor meer‑pagina‑rapporten.
* Verken export naar andere rasterformaten (JPEG, BMP) door `setSaveFormat` te wijzigen.

Voel u vrij dit patroon aan te passen voor grafieken, tabellen of zelfs volledige werkbladen. Veel programmeerplezier!

## Wat moet u hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om u te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in uw eigen projecten te verkennen.

- [Hoe een Excel-werkblad exporteren naar PNG met Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Excel naar PNG converteren met Aspose.Cells voor Java: Een stapsgewijze gids](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Een Union‑bereik maken in Excel met Aspose.Cells Java: Een uitgebreide gids](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}