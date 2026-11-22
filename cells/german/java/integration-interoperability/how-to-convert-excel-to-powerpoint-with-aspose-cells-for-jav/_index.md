---
category: general
date: 2026-11-22
description: Erfahren Sie, wie Sie Excel mit Aspose.Cells für Java in PowerPoint konvertieren,
  einschließlich der Schritte zum Exportieren von Excel‑Diagrammen nach PowerPoint
  in einem einzigen Workflow.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- export excel chart to powerpoint
- Aspose.Cells Java
- Excel to PPTX conversion
- Java file format conversion
language: de
lastmod: 2026-11-22
og_description: Konvertieren Sie Excel mit Aspose.Cells für Java in PowerPoint. Folgen
  Sie diesem vollständigen Schritt‑für‑Schritt‑Tutorial, um auch Excel‑Diagramme nach
  PowerPoint zu exportieren.
og_image_alt: Diagram showing conversion of Excel to PowerPoint using Aspose.Cells
og_title: Excel in PowerPoint konvertieren mit Aspose.Cells – Java‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  headline: How to convert Excel to PowerPoint with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  name: How to convert Excel to PowerPoint with Aspose.Cells for Java
  steps:
  - name: Open `withShapes.pptx` in PowerPoint.
    text: Open `withShapes.pptx` in PowerPoint.
  - name: Confirm that each Excel sheet appears as a separate slide.
    text: Confirm that each Excel sheet appears as a separate slide.
  - name: Check that charts retain their colors, legends, and data labels.
    text: Check that charts retain their colors, legends, and data labels.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: Wie man Excel mit Aspose.Cells für Java nach PowerPoint konvertiert
url: /de/java/integration-interoperability/how-to-convert-excel-to-powerpoint-with-aspose-cells-for-jav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Excel in PowerPoint mit Aspose.Cells für Java konvertiert

Wenn Sie **Excel in PowerPoint konvertieren** müssen, zeigt Ihnen diese Anleitung einen einfachen Weg mit Aspose.Cells für Java. Sie sehen außerdem, wie Sie **Excel‑Diagramm nach PowerPoint exportieren** können, sodass Sie Diagramme direkt in eine Präsentation einbetten, ohne manuelles Kopieren‑Einfügen.

Das Konvertieren von Tabellenkalkulationen in Folien ist üblich, wenn Sie datenbasierte Erkenntnisse einem nicht‑technischen Publikum präsentieren wollen. Anstatt Diagramme in PowerPoint neu zu erstellen, können Sie die gesamte Pipeline automatisieren, das Format beibehalten und Stunden an Arbeit sparen.

In diesem Tutorial lernen Sie:

* Aspose.Cells in einem Maven‑ oder Gradle‑Projekt einrichten.  
* Eine vorhandene Arbeitsmappe laden, die Daten und Diagramme enthält.  
* `ImageOrPrintOptions` konfigurieren, um das PPTX‑Format zu verwenden.  
* Die Arbeitsmappe als PowerPoint‑Präsentation speichern.  
* Das Ergebnis prüfen und typische Randfälle behandeln.

> **Voraussetzung** – Sie benötigen eine gültige Aspose.Cells‑Lizenz für Java (oder Sie können die Evaluierungs‑Version verwenden). Der Code funktioniert mit Java 8+ und jeder IDE, die Maven/Gradle unterstützt.

![Diagram showing conversion of Excel to PowerPoint using Aspose.Cells](convert_excel_to_powerpoint.png)

## Was Sie benötigen

| Element | Grund |
|------|--------|
| **Java Development Kit (JDK) 8 oder neuer** | Erforderlich zum Kompilieren und Ausführen des Beispiels. |
| **Maven oder Gradle** | Vereinfacht das Dependency‑Management für Aspose.Cells. |
| **Aspose.Cells für Java** | Stellt die APIs `Workbook` und `ImageOrPrintOptions` bereit, die für die Konvertierung verwendet werden. |
| **Eine Excel‑Datei (`shapes.xlsx`) mit mindestens einem Diagramm** | Demonstriert das Szenario *Excel‑Diagramm nach PowerPoint exportieren*. |

## Schritt 1: Aspose.Cells zu Ihrem Projekt hinzufügen

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-cells:24.10' // latest version as of 2026
```

> **Warum dieser Schritt wichtig ist** – Das Hinzufügen der Bibliothek stellt die Klassen `Workbook`, `ImageOrPrintOptions` und `SaveFormat` bereit. Ohne die korrekte Dependency lässt sich der Code nicht kompilieren.

## Schritt 2: Die Arbeitsmappe laden, die das/die Diagramm(e) enthält

```java
import com.aspose.cells.Workbook;

// Load the Excel file. Replace the path with your actual location.
Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
```

**Erklärung:**  
`Workbook` ist der Einstiegspunkt für alle Excel‑Operationen. Durch das Laden von `shapes.xlsx` bringen Sie sowohl die Datentabellen als auch eingebettete Diagramme in den Speicher, was die nachfolgende Konvertierung ermöglicht.

## Schritt 3: Konvertierungsoptionen erstellen und das Zielformat auf PPTX setzen

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

// Configure options for image/print conversion.
ImageOrPrintOptions options = new ImageOrPrintOptions();
// The SaveFormat.PPTX constant tells Aspose.Cells to generate a PowerPoint file.
options.setSaveFormat(SaveFormat.PPTX);
```

**Warum `ImageOrPrintOptions` verwenden?**  
Diese Optionen steuern, wie jedes Arbeitsblatt oder Diagramm gerendert wird. Das Setzen von `SaveFormat.PPTX` weist die Bibliothek an, jedes Blatt (oder Diagramm) auf einer eigenen Folie abzulegen und dabei die visuelle Treue zu bewahren.

## Schritt 4: Die Arbeitsmappe als PowerPoint‑Präsentation speichern

```java
// The second argument is the options object we just configured.
workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);
```

**Was hier passiert:**  
Aspose.Cells iteriert über die Arbeitsblätter und Diagramme der Arbeitsmappe, rastert sie in folienkompatible Grafiken und schreibt ein `.pptx`‑Paket an den angegebenen Ort. Die resultierende Datei kann in Microsoft PowerPoint, Google Slides oder jedem PPTX‑kompatiblen Viewer geöffnet werden.

## Schritt 5: Die Konvertierung überprüfen

1. Öffnen Sie `withShapes.pptx` in PowerPoint.  
2. Stellen Sie sicher, dass jedes Excel‑Blatt als separate Folie erscheint.  
3. Prüfen Sie, dass Diagramme ihre Farben, Legenden und Datenbeschriftungen beibehalten.  

Wenn ein Diagramm verzerrt wirkt, müssen Sie eventuell die DPI‑Einstellung von `ImageOrPrintOptions` anpassen:

```java
options.setResolution(300); // 300 DPI gives higher quality for complex charts
```

## Excel‑Diagramm nach PowerPoint exportieren – eine fokussierte Variante

Manchmal möchten Sie nur ein einzelnes Diagramm statt der gesamten Arbeitsmappe verschieben. Das lässt sich erreichen, indem Sie das Diagramm zuerst in ein Bild konvertieren und dann manuell in eine PowerPoint‑Folie einfügen, aber Aspose.Cells vereinfacht den Prozess:

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;
import com.aspose.cells.SaveOptions;

// Assume the chart is on the first worksheet, first chart object.
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

// Create options for converting the chart to an image.
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
chartOptions.setImageFormat(ImageFormat.PNG);
chartOptions.setSaveFormat(SaveFormat.PPTX);

// Save only the chart as a PPTX slide.
chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOptions);
```

**Warum das wichtig ist:**  
Der Code‑Abschnitt isoliert ein einzelnes Diagramm, reduziert die Dateigröße und gibt Ihnen feinere Kontrolle darüber, welche Visualisierungen zu Folien werden. Es ist der direkteste Weg, um **Excel‑Diagramm nach PowerPoint zu exportieren**, wenn Sie nicht die komplette Arbeitsmappe benötigen.

## Häufige Stolperfallen und wie man sie vermeidet

| Problem | Ursache | Lösung |
|-------|-------|-----|
| **Leere Folien** | Das Arbeitsblatt enthält keine sichtbaren Daten oder das Diagramm ist ausgeblendet. | Stellen Sie sicher, dass das Diagramm sichtbar ist und das Arbeitsblatt Daten enthält, bevor Sie speichern. |
| **Niedrigauflösende Bilder** | Standard‑DPI ist 96, was für gedruckte Folien unzureichend sein kann. | Rufen Sie `options.setResolution(200‑300)` vor `workbook.save` auf. |
| **Nicht unterstützte Diagrammtypen** | Sehr neue oder benutzerdefinierte Diagrammtypen werden möglicherweise nicht perfekt gerendert. | Exportieren Sie das Diagramm als Bild (`ImageFormat.PNG`) und fügen Sie es manuell ein. |
| **Dateipfad‑Fehler** | Falscher relativer Pfad auf unterschiedlichen Betriebssystemen. | Verwenden Sie `Paths.get("YOUR_DIRECTORY", "file.xlsx").toString()` für plattformunabhängige Pfade. |

## Profi‑Tipps für produktionsreife Konvertierungen

* **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis mit Excel‑Dateien und rufen Sie dieselbe Konvertierungslogik auf.  
* **Speichermanagement:** Für große Arbeitsmappen `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` aufrufen, um den Heap‑Verbrauch zu reduzieren.  
* **Lizenzaktivierung:** Legen Sie Ihre Lizenzdatei (`Aspose.Cells.lic`) im Klassenpfad ab und rufen Sie `License license = new License(); license.setLicense("Aspose.Cells.lic");` vor jeglicher Nutzung der Aspose‑API auf.  
* **Thread‑Sicherheit:** Jeder Thread sollte mit seiner eigenen `Workbook`‑Instanz arbeiten; Aspose.Cells‑Objekte sind nicht thread‑sicher.

## Vollständiges funktionierendes Beispiel

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) throws Exception {
        // 1. Optional: activate your Aspose.Cells license.
        // License license = new License();
        // license.setLicense("Aspose.Cells.lic");

        // 2. Load the workbook that contains charts.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // 3. Set conversion options – target PPTX format.
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
        // Increase resolution for sharper charts (optional).
        options.setResolution(300);

        // 4. Save the workbook as a PowerPoint presentation.
        workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);

        // 5. (Optional) Export only the first chart to its own PPTX.
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        ImageOrPrintOptions chartOpts = new ImageOrPrintOptions();
        chartOpts.setSaveFormat(SaveFormat.PPTX);
        chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOpts);

        System.out.println("Conversion completed successfully.");
    }
}
```

**Erwartete Ausgabe:**  

Beim Ausführen des Programms wird `Conversion completed successfully.` ausgegeben und es werden zwei Dateien erstellt:

* `withShapes.pptx` – ein Foliendeck, bei dem jedes Arbeitsblatt (und seine Diagramme) auf einer separaten Folie erscheint.  
* `singleChart.pptx` – eine Ein‑Folie‑Präsentation, die nur das erste Diagramm aus der Arbeitsmappe enthält.

Öffnen Sie diese Dateien in PowerPoint, um zu prüfen, dass die Diagramme ihr ursprüngliches Styling und ihre Datenbeschriftungen beibehalten.

## Fazit

Sie wissen jetzt, wie Sie **Excel in PowerPoint** mit Aspose.Cells für Java konvertieren und haben zudem den effizientesten Weg gesehen, **Excel‑Diagramm nach PowerPoint zu exportieren**, wenn nur ein bestimmtes Visual benötigt wird. Durch das Konfigurieren von `ImageOrPrintOptions` und das Setzen von `SaveFormat` auf `PPTX` übernimmt die Bibliothek das aufwändige Rendern von Arbeitsblättern und Diagrammen in folienkompatible Grafiken.

Ab hier können Sie:

* Batch‑Konvertierungen für Reporting‑Pipelines automatisieren.  
* Das erzeugte PPTX mit anderen Folien‑Assets über die Apache POI `XSLF`‑API kombinieren.  
* Weitere Export‑Formate wie PDF oder HTML für Multi‑Channel‑Distribution erkunden.

Experimentieren Sie gern mit DPI‑Einstellungen, benutzerdefinierten Folien‑Layouts oder der Einbettung des erzeugten PPTX in E‑Mail‑Workflows. Viel Spaß beim Coden!


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [How to export Excel sheet to PowerPoint with Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step‑by‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to export chart to docx from Excel using Aspose.Cells for Java](/cells/english/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}