---
category: general
date: 2026-10-01
description: Erfahren Sie, wie Sie Formen mit ShapeExportOptions in Java exportieren
  und die Form beim Konvertieren in PPTX mit Aspose.Cells editierbar halten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: de
lastmod: 2026-10-01
og_description: Exportieren Sie Formen mit ShapeExportOptions in Java, um bearbeitbare
  PPTX‑Dateien zu erstellen. Dieses Tutorial führt Sie durch den gesamten Prozess
  mit Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Form exportieren mit ShapeExportOptions in Java – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Wie man ein Shape mit ShapeExportOptions in Java exportiert
url: /de/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Formen mit ShapeExportOptions in Java exportiert

Wenn Sie **eine Form mit ShapeExportOptions** aus einer Excel‑Arbeitsmappe exportieren müssen, zeigt Ihnen diese Anleitung die genauen Schritte. Sie sehen, wie Sie die Form beim Konvertieren in eine PPTX‑Datei editierbar halten, was für nachträgliche Bearbeitungen in PowerPoint unerlässlich ist.

Das Exportieren von Formen ist eine gängige Aufgabe, wenn Sie Präsentationen aus Tabellenkalkulationen erzeugen – sei es für Vertriebs‑Decks, Reporting‑Dashboards oder automatisierte Präsentationen. Dieses Tutorial deckt alles ab, was Sie benötigen, von der Projekt‑Einrichtung bis zur Überprüfung der exportierten Datei, und verwendet die **Aspose.Cells for Java**‑Bibliothek.

## Was Sie benötigen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Java 17 oder neuer (der Code kompiliert mit jedem aktuellen JDK)
- Maven oder Gradle für das Abhängigkeits‑Management
- Eine Excel‑Datei (`Shapes.xlsx`), die mindestens ein Textfeld oder eine andere Form enthält
- Grundlegende Kenntnisse der Aspose.Cells‑APIs

## Schritt 1: Aspose.Cells zu Ihrem Projekt hinzufügen (Aspose Cells export shape)

Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Für Gradle platzieren Sie dies in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro‑Tipp:** Registrieren Sie Ihre Lizenz frühzeitig, um Evaluations‑Wasserzeichen zu vermeiden.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Schritt 2: Laden Sie die Arbeitsmappe, die die Form enthält

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

Das `Workbook`‑Objekt repräsentiert die gesamte Excel‑Datei. Das Laden ist die erste Voraussetzung für jede Form‑Manipulation.

## Schritt 3: Greifen Sie auf das Arbeitsblatt zu und holen Sie die gewünschte Form (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Warum das wichtig ist:** Formen werden pro Arbeitsblatt gespeichert, daher müssen Sie zum richtigen Blatt navigieren, bevor Sie eine bestimmte Form exportieren können.

## Schritt 4: Konfigurieren Sie **ShapeExportOptions**, um die Form editierbar zu halten (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

Durch Setzen von `ExportAsEditable` auf `true` weist Aspose.Cells an, die Vektordaten der Form zu erhalten, sodass PowerPoint‑Benutzer die Form nach dem Import bearbeiten können.

## Schritt 5: Exportieren Sie die Form direkt in eine PPTX‑Datei (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

Die Methode `exportToImage` funktioniert für mehrere Bildformate; endet der Ziel‑Dateiname mit `.pptx`, schreibt Aspose.Cells eine PowerPoint‑Folien‑Datei, die die Form enthält.

### Erwartetes Ergebnis

- `textbox.pptx` erscheint im angegebenen Verzeichnis.
- Öffnet man die Datei in PowerPoint, wird eine einzelne Folie mit dem ursprünglichen Textfeld angezeigt.
- Das Textfeld ist vollständig editierbar (Text, Schriftart, Größe usw. können geändert werden).

## Schritt 6: Überprüfen Sie die Ausgabe und behandeln Sie gängige Sonderfälle

### Programmgesteuert prüfen

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

Wenn `slideCount` gleich `1` ist, war der Export erfolgreich.

### Sonderfall: Mehrere Formen

Enthält das Arbeitsblatt mehrere Formen und Sie möchten nur eine bestimmte, finden Sie sie über den Namen:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Sonderfall: Form nicht gefunden

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Sonderfall: Export in andere Formate

`ShapeExportOptions` unterstützt außerdem PNG, JPEG, SVG und EMF. Ändern Sie die Dateierweiterung und setzen Sie optional `exportOptions.setImageFormat(ImageFormat.PNG)`.

## Vollständiges, ausführbares Beispiel

Alle Teile zusammen ergeben ein eigenständiges Programm, das Sie in Ihre IDE kopieren‑und‑einfügen können:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

Beim Ausführen des Programms wird `textbox.pptx` erstellt. Öffnen Sie es in PowerPoint, klicken Sie mit der rechten Maustaste auf das Textfeld, und Sie sehen die üblichen Bearbeitungshandgriffe – das bestätigt, dass **export shape with ShapeExportOptions** die Editierbarkeit erhalten hat.

## Häufig gestellte Fragen

| Frage | Antwort |
|----------|--------|
| *Kann ich eine Diagramm‑Form exportieren?* | Ja. Der gleiche Aufruf `exportToImage` funktioniert für Diagramme, Bilder und SmartArt. |
| *Was, wenn ich ein PNG mit höherer Auflösung benötige?* | Setzen Sie `options.setImageFormat(ImageFormat.PNG)` und passen Sie `options.setResolution(300)` vor dem Export an. |
| *Ist die exportierte PPTX mit älteren PowerPoint‑Versionen kompatibel?* | Die Bibliothek schreibt Office Open XML (PPTX), das von PowerPoint 2007 und neuer unterstützt wird. |
| *Benötige ich eine Lizenz, damit das funktioniert?* | Eine kostenlose Evaluation funktioniert, fügt jedoch ein Wasserzeichen hinzu. Registrieren Sie eine Lizenz, um es zu entfernen. |

## Nächste Schritte

- Erkunden Sie **Aspose.Slides for Java**, wenn Sie mehrere exportierte Formen zu einem einzigen Präsentationsdeck kombinieren möchten.
- Verwenden Sie **ShapeExportOptions.setExportAsEditable(false)**, wenn Sie ein Rasterbild (PNG/JPEG) für schnellere Darstellung bevorzugen.
- Automatisieren Sie die Stapelverarbeitung: Durchlaufen Sie alle Arbeitsblätter und exportieren Sie jede Form in separate PPTX‑Dateien.

---

### Fazit

Sie wissen jetzt, wie man **eine Form mit ShapeExportOptions in Java exportiert** und dabei die Editierbarkeit beim Konvertieren eines Textfelds (oder einer anderen Form) in eine PPTX‑Datei bewahrt. Indem Sie die oben beschriebenen Schritte befolgen – Bibliothek einbinden, Arbeitsmappe laden, `ShapeExportOptions` konfigurieren und `exportToImage` aufrufen – können Sie den Form‑Export in jede automatisierte Reporting‑Pipeline integrieren.

Experimentieren Sie gern mit verschiedenen Formen, Ausgabeformaten und Auflösungseinstellungen. Wenn Ihnen diese Anleitung geholfen hat, teilen Sie sie mit Kolleg*innen oder setzen Sie ein Lesezeichen für die Zukunft. Viel Spaß beim Coden!

## Was Sie als Nächstes lernen sollten

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [How to Adjust Shape Margins in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [How to Apply 3D Shape Formatting in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java Workbook Shape Copying Guide](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}