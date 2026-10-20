---
category: general
date: 2026-10-07
description: Lär dig hur du skapar PNG från ett område och exporterar data som PNG
  i Java. Denna guide visar hur du sparar en Excel‑områdesbild med Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: sv
lastmod: 2026-10-07
og_description: Skapa PNG från ett område i Java och exportera data som PNG med Aspose.Cells.
  Följ den här kompletta handledningen för att spara Excel‑områdesbilden omedelbart.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Skapa PNG från område i Java – steg‑för‑steg Aspose.Cells‑guide
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
title: Hur man skapar PNG från ett område i Java med Aspose.Cells
url: /sv/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur du skapar PNG från ett område i Java med Aspose.Cells

Om du behöver **create PNG from range** i en Excel‑arbetsbok visar den här handledningen exakt hur du gör det. I slutet av guiden kommer du att kunna **export data as PNG**, spara en Excel‑område‑bild och återanvända filen i rapporter eller webbsidor.

Du kommer att se ett komplett, körbart Java‑program som laddar en arbetsbok, väljer önskade celler, renderar dem som en PNG och sparar resultatet till disk. Inga externa verktyg krävs—Aspose.Cells hanterar allt internt.

## Vad den här handledningen täcker

* Förutsättningar och Maven‑konfiguration för Aspose.Cells
* Ladda en arbetsbok som innehåller en pivottabell eller vilket dataintervall som helst
* Definiera det exakta cellområdet du vill konvertera
* Konfigurera bildalternativ för PNG‑utmatning
* Rendera området och spara PNG‑filen
* Vanliga fallgropar och tips för högkvalitativa bilder

Efter att ha slutfört dessa steg kommer du att kunna **convert worksheet to PNG** för vilket område som helst, oavsett om det är ett enkelt bord eller ett komplext pivottabell‑diagram.

## Förutsättningar

* Java 17 eller senare (koden kompileras med JDK 11+)
* Maven 3.6+ (eller Gradle om du föredrar)
* Aspose.Cells för Java 23.12 eller nyare – lägg till beroendet som visas nedan
* En befintlig Excel‑fil (`PivotWithStyle.xlsx`) som innehåller området du vill fånga

> **Pro tip:** Om du inte har en licens kan du begära en tillfällig utvärderingsnyckel från Aspose. Biblioteket fungerar i utvärderingsläge utan ytterligare konfiguration.

### Maven‑beroende

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Steg 1: Ladda arbetsboken som innehåller målområdet

Den första operationen är att öppna Excel‑filen. Aspose.Cells läser filen till minnet utan att kräva Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Varför detta är viktigt*: Att ladda arbetsboken ger dig åtkomst till kalkylblad, celler och sidinställnings‑egenskaper som behövs för rendering.

## Steg 2: Åtkomst till kalkylbladet som innehåller området

De flesta arbetsböcker har ett standardblad på index 0, men du kan också använda bladnamnet.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Om dina data finns på ett annat blad, ersätt `0` med rätt index eller använd `workbook.getWorksheets().get("SheetName")`.

## Steg 3: Definiera cellområdet du vill konvertera

Du kan ange vilket rektangulärt område som helst med A1‑notation. I det här exemplet fångar vi `A1:D15`, vilket kan vara en pivottabell eller ett vanligt datablok.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Edge case*: När området innehåller sammanslagna celler expanderar Aspose.Cells automatiskt bilden för att inkludera det sammanslagna området.

## Steg 4: Förbered PNG‑bildalternativ

`ImageOrPrintOptions` låter dig kontrollera format, upplösning och andra renderingsdetaljer. Att sätta sparformatet till PNG säkerställer förlustfri kvalitet.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Att öka DPI är användbart när källcellerna innehåller små teckensnitt eller detaljerade diagram.

## Steg 5: Begränsa renderingsområdet till det valda området

Genom att tilldela området som utskriftsområde renderar Aspose.Cells endast de cellerna och ignorerar resten av bladet.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Om du hoppar över detta steg kommer hela kalkylbladet att rasteriseras, vilket kan slösa minne och producera en större bild.

## Steg 6: Rendera området och lägg till bilden i kalkylbladet (valfritt)

Om du vill bädda in den genererade PNG‑filen tillbaka i arbetsboken (för förhandsgranskningsändamål) kan du lägga till den som en bild. Detta steg är valfritt för rena export‑scenarier.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Varför du kan göra detta*: Vissa arbetsflöden kräver att bilden är en del av arbetsboken innan distribution, till exempel att skapa en utskrivbar rapport som blandar inbyggda celler och bilder.

## Steg 7: Spara PNG‑filen till disk

Slutligen skriver du bilden till en fil. `save`‑metoden respekterar formatet som specificerats i `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

När programmet är klart kommer `PivotImage.png` att innehålla en pixel‑perfekt ögonblicksbild av cellerna `A1:D15`.

### Förväntat resultat

* En fil med namnet `PivotImage.png` placerad i `YOUR_DIRECTORY`.
* Bilden visar exakt layout, teckensnitt, färger och kantlinjer från det valda området.
* Om källområdet innehåller en pivottabell inkluderar den renderade bilden samma stil och beräknade värden som visas i Excel.

## Hantera vanliga scenarier

### Exportera ett icke‑sammanhängande område

Aspose.Cells renderar inte separata områden i en enda bild. För att exportera flera områden, skapa separata bilder för varje område och kombinera dem senare med ett bildbehandlingsbibliotek (t.ex. ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Spara ett stort kalkylblad som PNG

Att rendera ett helt blad som sträcker sig över tusentals rader kan förbruka mycket minne. Minska detta genom att:

* Minska DPI (`imageOptions.setResolution(72)`) för en mindre fil.
* Använda `setPageCount` för att begränsa antalet renderade sidor.
* Exportera en utskrivningsbar sida åt gången via `worksheet.getPageSetup().setPrintArea(...)`.

### Bevara cellformler

En PNG‑bild är ett rasterformat; formler bevaras inte. Om efterföljande konsumenter behöver rådata, exportera också området som CSV eller JSON med `Range.exportDataTable()`.

## Fullt, körbart exempel

Nedan är den kompletta Java‑klassen som du kan kopiera‑och‑klistra in i din IDE. Ersätt `YOUR_DIRECTORY` med en absolut eller relativ sökväg på din maskin.

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

Kör programmet med `mvn compile exec:java` (eller ditt föredragna byggverktyg). Efter körning, öppna `PivotImage.png` för att verifiera resultatet.

## Slutsats

Du vet nu hur du **create PNG from range** i Java med Aspose.Cells, effektivt **export data as PNG** och **save excel range image** för vilket rapport‑ eller delningsscenario som helst. Stegen—ladda arbetsboken, definiera området, konfigurera bildalternativ, sätta utskriftsområdet och spara filen—täcker hela arbetsflödet för **convert worksheet to PNG** och **save cells as PNG**.

### Nästa steg

* Experimentera med olika `Resolution`‑värden för att balansera kvalitet och filstorlek.
* Använd `ImageOrPrintOptions.setTransparent(true)` om du behöver en PNG med transparent bakgrund.
* Kombinera flera område‑bilder till en enda PDF med `PdfSaveOptions` för flersidiga rapporter.
* Utforska export till andra rasterformat (JPEG, BMP) genom att ändra `setSaveFormat`.

Känn dig fri att anpassa detta mönster till diagram, tabeller eller till och med hela kalkylblad. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}