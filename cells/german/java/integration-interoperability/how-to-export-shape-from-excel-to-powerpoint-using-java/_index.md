---
category: general
date: 2026-11-16
description: Erfahren Sie, wie Sie Formen von Excel nach PowerPoint in Java exportieren,
  Excel‑Diagramme in eine PPTX‑Datei konvertieren und Formen‑PPTX mit Aspose.Cells
  speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: de
lastmod: 2026-11-16
og_description: Wie man Formen von Excel nach PowerPoint in Java exportiert. Folgen
  Sie diesem vollständigen Tutorial, um ein Excel‑Diagramm zu konvertieren, Formen
  als PPTX zu speichern und eine Form in eine PowerPoint‑Datei einzubetten.
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: Wie man Formen von Excel nach PowerPoint in Java exportiert – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: Wie man ein Shape von Excel nach PowerPoint mit Java exportiert
url: /de/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to export shape from Excel to PowerPoint using Java

If you need to **how to export shape** from an Excel workbook into a PowerPoint slide, this guide shows you the exact steps. You’ll see how to **convert Excel chart** objects, turn them into a **shape to PowerPoint**, and finally **save shape PPTX** with the correct export options.

Exporting a shape is a common requirement when you generate reports programmatically. By the end of this tutorial you will have a self‑contained Java program that creates a `shape.pptx` file ready for presentation. No external scripts are required, and the code works with Aspose.Cells 2024‑R2 or later.

## Voraussetzungen

* Java 17 oder neuer (der Code kompiliert mit jedem JDK 8+)
* Aspose.Cells für Java Bibliothek (von der Aspose-Website herunterladen oder die Maven‑Abhängigkeit hinzufügen)
* Eine Excel‑Datei (`chart.xls`), die mindestens ein Shape enthält (ein Diagramm, Textfeld oder SmartArt)
* Grundlegende Kenntnisse der Java‑Fehlerbehandlung

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## Wie man Shape aus Excel nach PowerPoint exportiert (Gesamtablauf)

Der Prozess besteht aus vier logischen Abschnitten:

1. **Load the workbook** that contains the shape.  
2. **Locate the shape** on the first worksheet.  
3. **Configure export options** so the shape becomes an editable PowerPoint object.  
4. **Save the shape as a PPTX file**.

Each section is explained in detail below, and the complete runnable program follows the explanations.

## Schritt 1: Laden Sie die Arbeitsmappe, die das Shape enthält

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*Warum dieser Schritt?*  
`Workbook` is the entry point for all Aspose.Cells operations. Loading the file gives you access to worksheets, cells, and the shape collection. If the file cannot be found, Aspose.Cells throws a `FileNotFoundException`, which we catch later.

## Schritt 2: Zugriff auf das erste Arbeitsblatt und das Ziel‑Shape abrufen

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*Warum dieser Schritt?*  
Worksheets are stored in a zero‑based collection, so `get(0)` returns the first sheet. Shapes are also indexed; `get(0)` fetches the first shape, which is typically the chart you want to export. If your workbook contains multiple shapes, you can iterate the collection or use `shape.getName()` to pick a specific one.

## Schritt 3: Exportoptionen vorbereiten – wir wollen das Shape als editierbares PPTX‑Objekt

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*Warum dieser Schritt?*  
`ImageOrPrintOptions` controls how the shape is rendered. By choosing `SaveFormat.PPTX`, the library converts the Excel graphic into a vector‑based PowerPoint shape that remains editable after import. This is essential for a true **shape to PowerPoint** conversion; using PNG or JPEG would lock the graphic.

## Schritt 4: Das Shape in eine PowerPoint‑Datei exportieren

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*Warum dieser Schritt?*  
The `save` method writes the shape using the options defined earlier. The resulting `shape.pptx` contains a single slide where the shape appears exactly as it did in Excel, but now you can edit it in PowerPoint (change colors, resize, add animations, etc.). This satisfies the **save shape PPTX** requirement.

## Vollständiges, ausführbares Beispiel

Copy the entire class into a file named `ExportShapeDemo.java`, replace `YOUR_DIRECTORY` with an absolute or relative path, and run `javac ExportShapeDemo.java && java ExportShapeDemo`. After execution you will find `shape.pptx` in the target folder.

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### Erwartete Ausgabe

```
Export completed. File saved as shape.pptx
```

Open `shape.pptx` in Microsoft PowerPoint. You will see a single slide containing the original Excel chart (or textbox) as a fully editable PowerPoint shape.

## Häufige Variationen und Sonderfälle

| Situation | Empfohlene Anpassung |
|-----------|----------------------|
| **Mehrere Shapes** | Loop through `worksheet.getShapes()` and call `save` for each shape, or select by `shape.getName()`. |
| **Shape ist ein Diagramm mit Datenreihen** | Use `exportOptions.setExportChartAsEditable(true)` to keep series editable. |
| **Ein bestimmtes Folienlayout benötigt** | After saving, open the PPTX with Aspose.Slides and insert the shape into a custom layout. |
| **Große Arbeitsmappe** | Load only the required worksheet using `Workbook(String, LoadOptions)` to reduce memory consumption. |
| **Anderes Ausgabeformat (PDF, PNG)** | Change `exportOptions.setSaveFormat(SaveFormat.PDF)` or `SaveFormat.PNG`. This is useful when you **convert Excel chart** to a static image instead of a PowerPoint shape. |

**Profi‑Tipp:** Always verify that the shape index (`get(0)`) matches the visual element you intend to export. The shape collection order mirrors the order of insertion in Excel, which may differ from the visual stacking order.

## Wie man Shape aus Excel nach PowerPoint exportiert – Prüfliste zur Fehlerbehebung

* **Datei nicht gefunden** – Stellen Sie sicher, dass der Pfad in `new Workbook()` auf eine vorhandene `.xls`‑ oder `.xlsx`‑Datei zeigt.  
* **Keine Shapes zurückgegeben** – Vergewissern Sie sich, dass das Arbeitsblatt tatsächlich ein Shape enthält; Sie können `worksheet.getShapes().getCount()` aufrufen, um zu debuggen.  
* **Exportierte Datei ist leer** – Prüfen Sie, ob `exportOptions.setSaveFormat(SaveFormat.PPTX)` gesetzt ist; die Verwendung eines Bildformats erzeugt ein Bild statt eines Shapes.  
* **Kompatibilitätsprobleme** – Aspose.Cells 24.9+ unterstützt den PPTX‑Export auf allen gängigen Plattformen. Aktualisieren Sie, falls Sie `UnsupportedOperationException` erhalten.

## Fazit

You now know **how to export shape** from an Excel workbook and embed it into a PowerPoint presentation using Java. The tutorial covered loading the workbook, locating the shape, configuring the **export shape from Excel** options, and finally **save shape PPTX**. With this foundation you can automate report generation, build dashboards, or integrate Excel visuals into slide decks without manual copy‑paste.

### Nächste Schritte

* Explore **convert Excel chart** to other Office formats such as PDF or DOCX.  
* Combine this technique with Aspose.Slides to place multiple shapes on a single slide.  
* Experiment with `ImageOrPrintOptions` properties (e.g., `setResolution`, `setTransparent`) to fine‑tune the visual quality of the exported shape.

Feel free to adapt the code for batch processing or to integrate it into a larger reporting service. Happy coding!


## Was sollten Sie als Nächstes lernen?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to export shape with ShapeExportOptions in Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [How to export Excel sheet to PowerPoint with Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [How to Export Charts from Excel to PowerPoint – Full Java Guide](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}