---
category: general
date: 2026-10-07
description: Erfahren Sie, wie Sie in Java ein PNG aus einem Bereich erstellen und
  Daten als PNG exportieren. Dieser Leitfaden zeigt Ihnen, wie Sie ein Excel‑Bereichsbild
  mit Aspose.Cells speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: de
lastmod: 2026-10-07
og_description: Erstellen Sie ein PNG aus einem Bereich in Java und exportieren Sie
  Daten als PNG mit Aspose.Cells. Folgen Sie diesem vollständigen Tutorial, um das
  Excel‑Bereichsbild sofort zu speichern.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: PNG aus einem Bereich in Java erstellen – Schritt‑für‑Schritt Aspose.Cells‑Anleitung
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
title: Wie man aus einem Bereich in Java mit Aspose.Cells ein PNG erstellt
url: /de/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PNG aus einem Bereich in Java mit Aspose.Cells erstellt

Wenn Sie **PNG aus einem Bereich** in einer Excel‑Arbeitsmappe erstellen müssen, zeigt Ihnen dieses Tutorial genau, wie Sie das tun. Am Ende der Anleitung können Sie **Daten als PNG exportieren**, ein Excel‑Bereichs‑Bild speichern und die Datei in Berichten oder Webseiten wiederverwenden.

Sie sehen ein vollständiges, ausführbares Java‑Programm, das eine Arbeitsmappe lädt, die gewünschten Zellen auswählt, sie als PNG rendert und das Ergebnis auf die Festplatte speichert. Keine externen Tools sind erforderlich – Aspose.Cells erledigt alles intern.

## Was dieses Tutorial abdeckt

* Voraussetzungen und Maven‑Einrichtung für Aspose.Cells  
* Laden einer Arbeitsmappe, die eine Pivot‑Tabelle oder einen beliebigen Datenbereich enthält  
* Definieren des genauen Zellbereichs, den Sie konvertieren möchten  
* Konfigurieren von Bildoptionen für die PNG‑Ausgabe  
* Rendern des Bereichs und Speichern der PNG‑Datei  
* Häufige Stolpersteine und Tipps für hochqualitative Bilder  

Nachdem Sie diese Schritte abgeschlossen haben, können Sie **Arbeitsblatt in PNG konvertieren** für jeden Bereich, egal ob es sich um eine einfache Tabelle oder ein komplexes Pivot‑Diagramm handelt.

## Voraussetzungen

* Java 17 oder höher (der Code kompiliert mit JDK 11+)  
* Maven 3.6+ (oder Gradle, falls Sie das bevorzugen)  
* Aspose.Cells für Java 23.12 oder neuer – fügen Sie die unten gezeigte Abhängigkeit hinzu  
* Eine vorhandene Excel‑Datei (`PivotWithStyle.xlsx`), die den zu erfassenden Bereich enthält  

> **Pro‑Tipp:** Wenn Sie keine Lizenz besitzen, können Sie einen temporären Evaluierungsschlüssel von Aspose anfordern. Die Bibliothek funktioniert im Evaluierungsmodus ohne zusätzliche Konfiguration.

### Maven‑Abhängigkeit

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Schritt 1: Laden der Arbeitsmappe, die den Zielbereich enthält

Der erste Vorgang besteht darin, die Excel‑Datei zu öffnen. Aspose.Cells liest die Datei in den Speicher, ohne dass Microsoft Office erforderlich ist.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Warum das wichtig ist*: Das Laden der Arbeitsmappe gibt Ihnen Zugriff auf Arbeitsblätter, Zellen und Seiten‑Setup‑Eigenschaften, die für das Rendern benötigt werden.

## Schritt 2: Zugriff auf das Arbeitsblatt, das den Bereich enthält

Die meisten Arbeitsmappen haben ein Standardblatt mit dem Index 0, Sie können aber auch den Blattnamen verwenden.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Wenn Ihre Daten sich in einem anderen Blatt befinden, ersetzen Sie `0` durch den entsprechenden Index oder verwenden Sie `workbook.getWorksheets().get("SheetName")`.

## Schritt 3: Definieren des Zellbereichs, den Sie konvertieren möchten

Sie können jeden rechteckigen Bereich mit der A1‑Notation angeben. In diesem Beispiel erfassen wir `A1:D15`, was eine Pivot‑Tabelle oder einen regulären Datenblock sein kann.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Randfall*: Wenn der Bereich zusammengeführte Zellen enthält, erweitert Aspose.Cells das Bild automatisch, um den zusammengeführten Bereich einzuschließen.

## Schritt 4: PNG‑Bildoptionen vorbereiten

`ImageOrPrintOptions` ermöglicht die Steuerung von Format, Auflösung und anderen Render‑Details. Das Festlegen des Speicherformats auf PNG sorgt für verlustfreie Qualität.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Das Erhöhen der DPI ist nützlich, wenn die Quellzellen kleine Schriftarten oder detaillierte Diagramme enthalten.

## Schritt 5: Render‑Bereich auf den ausgewählten Bereich beschränken

Durch das Zuweisen des Bereichs als Druckbereich rendert Aspose.Cells nur diese Zellen und ignoriert den Rest des Blatts.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Wenn Sie diesen Schritt überspringen, wird das gesamte Arbeitsblatt gerastert, was Speicher verschwendet und ein größeres Bild erzeugt.

## Schritt 6: Den Bereich rendern und das Bild (optional) ins Arbeitsblatt einfügen

Wenn Sie das erzeugte PNG wieder in die Arbeitsmappe einbetten möchten (zur Vorschau), können Sie es als Bild hinzufügen. Dieser Schritt ist für reine Export‑Szenarien optional.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Warum Sie das tun könnten*: Einige Workflows erfordern, dass das Bild vor der Verteilung Teil der Arbeitsmappe ist, z. B. beim Erstellen eines druckbaren Berichts, der native Zellen und Bilder kombiniert.

## Schritt 7: PNG‑Datei auf die Festplatte speichern

Schließlich schreiben Sie das Bild in eine Datei. Die `save`‑Methode beachtet das in `imageOptions` angegebene Format.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Wenn das Programm beendet ist, enthält `PivotImage.png` einen pixelgenauen Schnappschuss der Zellen `A1:D15`.

### Erwartete Ausgabe

* Eine Datei namens `PivotImage.png` im Verzeichnis `YOUR_DIRECTORY`.  
* Das Bild zeigt das genaue Layout, die Schriftarten, Farben und Rahmen des ausgewählten Bereichs.  
* Enthält der Quellbereich eine Pivot‑Tabelle, beinhaltet das gerenderte Bild dieselbe Formatierung und die berechneten Werte wie in Excel angezeigt.

## Umgang mit gängigen Szenarien

### Export eines nicht zusammenhängenden Bereichs

Aspose.Cells rendert keine getrennten Bereiche in einem einzigen Bild. Um mehrere Bereiche zu exportieren, erstellen Sie separate Bilder für jeden Bereich und kombinieren Sie sie später mit einer Bildverarbeitungs‑Bibliothek (z. B. ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Speichern eines großen Arbeitsblatts als PNG

Das Rendern eines gesamten Blatts, das tausende Zeilen umfasst, kann viel Speicher beanspruchen. Mildern Sie das Problem, indem Sie:

* Die DPI reduzieren (`imageOptions.setResolution(72)`) für eine kleinere Datei.  
* `setPageCount` verwenden, um die Anzahl der zu rendernden Seiten zu begrenzen.  
* Eine druckbare Seite nach der anderen über `worksheet.getPageSetup().setPrintArea(...)` exportieren.

### Erhalt von Zellformeln

Ein PNG‑Bild ist ein Rasterformat; Formeln werden nicht beibehalten. Wenn nachgelagerte Verbraucher die Rohdaten benötigen, exportieren Sie den Bereich zusätzlich als CSV oder JSON mittels `Range.exportDataTable()`.

## Vollständiges, ausführbares Beispiel

Unten finden Sie die komplette Java‑Klasse, die Sie in Ihre IDE kopieren‑und‑einfügen können. Ersetzen Sie `YOUR_DIRECTORY` durch einen absoluten oder relativen Pfad auf Ihrem Rechner.

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

Führen Sie das Programm mit `mvn compile exec:java` (oder Ihrem bevorzugten Build‑Tool) aus. Nach der Ausführung öffnen Sie `PivotImage.png`, um das Ergebnis zu prüfen.

## Fazit

Sie wissen jetzt, wie man **PNG aus einem Bereich** in Java mit Aspose.Cells erstellt, effektiv **Daten als PNG exportiert** und **Excel‑Bereichs‑Bild speichert** für jedes Reporting‑ oder Sharing‑Szenario. Die Schritte – Laden der Arbeitsmappe, Definieren des Bereichs, Konfigurieren der Bildoptionen, Festlegen des Druckbereichs und Speichern der Datei – decken den gesamten Workflow für **Arbeitsblatt in PNG konvertieren** und **Zellen als PNG speichern** ab.

### Nächste Schritte

* Experimentieren Sie mit verschiedenen `Resolution`‑Werten, um Qualität und Dateigröße auszubalancieren.  
* Verwenden Sie `ImageOrPrintOptions.setTransparent(true)`, wenn Sie ein PNG mit transparentem Hintergrund benötigen.  
* Kombinieren Sie mehrere Bereichsbilder zu einem einzigen PDF mittels `PdfSaveOptions` für mehrseitige Berichte.  
* Erkunden Sie den Export in andere Rasterformate (JPEG, BMP) durch Ändern von `setSaveFormat`.

Passen Sie dieses Muster gerne für Diagramme, Tabellen oder sogar ganze Arbeitsblätter an. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}