---
category: general
date: 2026-09-18
description: Erfahren Sie, wie Sie Excel mit Aspose.Cells nach PowerPoint exportieren.
  Konvertieren Sie Excel in PPTX, erstellen Sie PowerPoint aus Excel und speichern
  Sie Excel in wenigen Minuten als PowerPoint.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- create powerpoint from excel
- save excel as powerpoint
- export excel to powerpoint
language: de
lastmod: 2026-09-18
og_description: Wie man Excel mit Aspose.Cells nach PowerPoint exportiert. Folgen
  Sie dieser Anleitung, um Excel in PPTX zu konvertieren, PowerPoint aus Excel zu
  erstellen und Excel effizient als PowerPoint zu speichern.
og_image_alt: Screenshot showing how to export Excel to PowerPoint with Aspose.Cells
og_title: Wie man Excel nach PowerPoint exportiert – vollständiges Aspose.Cells‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  headline: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  name: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that contains the shapes
    text: '```java import com.aspose.cells.*;'
  - name: Configure export options for PowerPoint conversion
    text: '```java /** * Creates ImageOrPrintOptions that control how Excel content
      is rendered * in the resulting PowerPoint file. * * @return a fully configured
      ImageOrPrintOptions object */ private static ImageOrPrintOptions createExportOptions()
      { ImageOrPrintOptions options = new ImageOrPrintOptions(); //'
  - name: Mark pictures (or charts) as editable
    text: '```java /** * Marks the first picture on the first worksheet as editable.
      * You can extend this loop to mark all pictures if needed. * * @param workbook
      the workbook that was loaded earlier */ private static void makeFirstPictureEditable(Workbook
      workbook) { // Navigate to the first worksheet (index'
  - name: Save the workbook as an editable PowerPoint presentation
    text: '```java /** * Performs the actual conversion and writes the PPTX file.
      * * @param workbook the workbook prepared in previous steps * @param exportOptions
      the options created in step 2 * @param outputPath full path for the resulting
      .pptx file * @throws Exception if saving fails */ private static voi'
  - name: Full runnable example
    text: '```java import com.aspose.cells.*;'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel‑to‑PowerPoint
- Document conversion
title: Wie man Excel mit Aspose.Cells nach PowerPoint exportiert – Schritt‑für‑Schritt‑Anleitung
url: /de/java/excel-import-export/how-to-export-excel-to-powerpoint-with-aspose-cells-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel mit Aspose.Cells nach PowerPoint exportieren – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **Excel exportieren** möchten, um es in einer PowerPoint‑Präsentation zu verwenden, zeigt dieses Tutorial eine vollständige, sofort einsatzbereite Lösung. Nach den ersten beiden Sätzen wissen Sie genau, welche API‑Aufrufe eine `.xlsx`‑Datei in eine editierbare `.pptx` umwandeln. Der Ansatz funktioniert für jede Arbeitsmappe, die Diagramme, Bilder oder andere Formen enthält, und er erfordert nur wenige Zeilen Java‑Code.

In diesem Leitfaden lernen Sie, wie Sie **Excel nach PPTX konvertieren**, **PowerPoint aus Excel erstellen** und **Excel als PowerPoint speichern**, wobei die Editierbarkeit von Diagrammen und Bildern erhalten bleibt. Es wird kein zusätzliches Werkzeug über Aspose.Cells hinaus benötigt, und der Code läuft auf Java 8+ und jedem aktuellen JDK.

* Java Development Kit (JDK) 8 oder neuer installiert  
* Maven oder Gradle für die Abhängigkeitsverwaltung (oder die Aspose.Cells‑JAR im Klassenpfad)  
* Eine Arbeitsmappe (`WithShapes.xlsx`), die mindestens ein Bild oder Diagramm enthält  

---

![Diagramm, das zeigt, wie Excel nach PowerPoint exportiert wird](https://example.com/diagram.png "Wie man Excel nach PowerPoint exportiert – Illustration")

## Excel mit Aspose.Cells nach PowerPoint exportieren

Der Kern der Konvertierung besteht aus vier prägnanten Schritten. Jeder Schritt ist in einer Methode gekapselt, sodass Sie die Logik in größeren Anwendungen wiederverwenden können.

### Schritt 1: Laden der Arbeitsmappe, die die Formen enthält

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    /**
     * Loads the source Excel workbook.
     *
     * @param path full path to the .xlsx file
     * @return a Workbook instance ready for manipulation
     * @throws Exception if the file cannot be read
     */
    private static Workbook loadWorkbook(String path) throws Exception {
        // The Workbook constructor reads the entire file into memory.
        return new Workbook(path);
    }
}
```

**Warum das wichtig ist:**  
Das Laden der Arbeitsmappe gibt Ihnen Zugriff auf Arbeitsblätter, Bilder und Diagramme. Aspose.Cells liest die Datei, ohne Microsoft Office aufzurufen, sodass die Operation auf headless Servern funktioniert.

### Schritt 2: Exportoptionen für die PowerPoint‑Konvertierung konfigurieren

```java
    /**
     * Creates ImageOrPrintOptions that control how Excel content is rendered
     * in the resulting PowerPoint file.
     *
     * @return a fully configured ImageOrPrintOptions object
     */
    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        // Do not include hidden worksheets – they usually contain metadata only.
        options.setExportHiddenWorksheet(false);
        // Export charts as editable shapes so the end‑user can modify them in PowerPoint.
        options.setExportChartAsEditable(true);
        return options;
    }
```

**Warum das wichtig ist:**  
`setExportChartAsEditable(true)` weist Aspose.Cells an, Vektorformen anstelle von Rasterbildern zu erzeugen. Dadurch wird die PowerPoint‑Ausgabe **PowerPoint aus Excel erstellen** mit vollständig editierbaren Diagrammen, was die meisten Präsentations‑Workflows erfüllt.

### Schritt 3: Bilder (oder Diagramme) als editierbar markieren

```java
    /**
     * Marks the first picture on the first worksheet as editable.
     * You can extend this loop to mark all pictures if needed.
     *
     * @param workbook the workbook that was loaded earlier
     */
    private static void makeFirstPictureEditable(Workbook workbook) {
        // Navigate to the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
        // Retrieve the first picture on that sheet
        Picture pic = sheet.getPictures().get(0);
        // Set the picture to be editable in the PowerPoint output
        pic.setEditable(true);
    }
```

**Warum das wichtig ist:**  
Wenn ein Bild als editierbar markiert ist, gibt Aspose.Cells es als EMF/WMF‑Form im PPTX‑Datei aus. Dies ist für den Anwendungsfall **Excel nach PowerPoint exportieren** entscheidend, bei dem der Empfänger das Bild später anpassen muss.

### Schritt 4: Die Arbeitsmappe als editierbare PowerPoint‑Präsentation speichern

```java
    /**
     * Performs the actual conversion and writes the PPTX file.
     *
     * @param workbook      the workbook prepared in previous steps
     * @param exportOptions the options created in step 2
     * @param outputPath    full path for the resulting .pptx file
     * @throws Exception if saving fails
     */
    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // The SaveFormat.PPTX enum tells Aspose.Cells to generate a PowerPoint file.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
```

**Warum das wichtig ist:**  
Der Aufruf `save` fasst alle vorherigen Änderungen (editierbare Bilder, Diagrammeinstellungen) zu einem einzigen `.pptx`‑Archiv zusammen. Die resultierende Datei kann in Microsoft PowerPoint, Google Slides oder jedem PPTX‑kompatiblen Viewer geöffnet werden.

### Vollständiges ausführbares Beispiel

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    public static void main(String[] args) {
        try {
            // Adjust these paths to match your environment.
            String sourcePath = "YOUR_DIRECTORY/WithShapes.xlsx";
            String destinationPath = "YOUR_DIRECTORY/Result.pptx";

            // Step 1 – load workbook
            Workbook workbook = loadWorkbook(sourcePath);

            // Step 2 – configure export options
            ImageOrPrintOptions exportOptions = createExportOptions();

            // Step 3 – make the first picture editable
            makeFirstPictureEditable(workbook);

            // Step 4 – save as PPTX
            saveAsPowerPoint(workbook, exportOptions, destinationPath);

            System.out.println("Conversion successful! File saved at: " + destinationPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---- Helper methods from earlier steps ----

    private static Workbook loadWorkbook(String path) throws Exception {
        return new Workbook(path);
    }

    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setExportHiddenWorksheet(false);
        options.setExportChartAsEditable(true);
        return options;
    }

    private static void makeFirstPictureEditable(Workbook workbook) {
        Worksheet sheet = workbook.getWorksheets().get(0);
        if (!sheet.getPictures().isEmpty()) {
            sheet.getPictures().get(0).setEditable(true);
        }
    }

    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // Export options are automatically applied when saving to PPTX.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
}
```

**Erwartetes Ergebnis:**  
Das Öffnen von `Result.pptx` in PowerPoint zeigt eine Folie, die das erste Arbeitsblatt von `WithShapes.xlsx` widerspiegelt. Diagramme erscheinen als Vektorformen, die Sie doppelklicken können, um Daten zu bearbeiten, und das erste Bild ist ein editierbares Objekt (Sie können es direkt in PowerPoint skalieren, neu einfärben oder ersetzen).

---

## Excel nach PPTX konvertieren – erweiterte Anpassungen

Obwohl der grundlegende Ablauf für die meisten Szenarien ausreicht, können Sie Folgendes benötigen:

* **Mehrere Arbeitsblätter exportieren** – iterieren Sie über `workbook.getWorksheets()` und rufen Sie `workbook.save` für jedes auf, wobei Sie über `ImageOrPrintOptions.setSlideNumber(int)` einen anderen Folienindex übergeben.  
* **Folienabmessungen steuern** – verwenden Sie `exportOptions.setImageHeight(int)` und `setImageWidth(int)`, um eine bestimmte PowerPoint‑Foliengröße (z. B. 1024 × 768) anzupassen.  
* **Formeln erhalten** – setzen Sie `exportOptions.setExportFormulasAsValues(false)`, wenn Sie die ursprünglichen Excel‑Formeln als versteckte Daten einbetten möchten.  

Diese Anpassungen ermöglichen es Ihnen, **PowerPoint aus Excel zu erstellen**, das mit dem Corporate‑Branding oder den Präsentationsstandards übereinstimmt.

---

## Excel als PowerPoint speichern – häufige Fallstricke und wie man sie vermeidet

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Diagramme erscheinen als Rasterbilder | `setExportChartAsEditable(false)` (Standard) | Editierbare Diagramme aktivieren mit `setExportChartAsEditable(true)` |
| Kein Bild erscheint auf der Folie | Bild nicht als editierbar markiert oder Bildindex außerhalb des Bereichs | Überprüfen Sie `sheet.getPictures().size() > 0` bevor Sie `setEditable(true)` aufrufen |
| Versteckte Arbeitsblätter erscheinen in der PPTX | `setExportHiddenWorksheet(true)` | Behalten Sie den Standardwert `false` bei oder setzen Sie ihn explizit auf `false` |
| Ausgabedatei ist beschädigt | Verwendung einer veralteten Aspose.Cells‑Version (vor 20.10) | Aktualisieren Sie auf die neueste Aspose.Cells‑Version für Java (z. B. 23.12) |

---

## Excel nach PowerPoint exportieren: Leistungstipps

* **Verwenden Sie dasselbe `ImageOrPrintOptions`‑Objekt** für mehrere Saves – es vermeidet wiederholte Allokationen.  
* **Streamen Sie die Quellarbeitsmappe** (`new Workbook(InputStream)`) bei der Arbeit mit großen Dateien auf speicherbeschränkten Servern.  
* **Parallelisieren Sie die Konvertierung pro Arbeitsblatt**, wenn Sie ein Deck mit Hunderten von Folien erzeugen müssen; jedes Arbeitsblatt kann in einem eigenen Thread verarbeitet werden, da Aspose.Cells‑Objekte nach der Erstellung thread‑sicher sind.

---

## Nächste Schritte

Sie wissen jetzt, **wie man Excel** in ein PowerPoint‑Deck exportiert, **Excel nach PPTX konvertiert** und **Excel als PowerPoint speichert** mit editierbarem Inhalt. Um dieses Wissen zu erweitern, könnten Sie:

* **Aspose.Slides** erkunden, um nach der Konvertierung Animationen oder Master‑Folien‑Layouts hinzuzufügen.  
* Den Workflow in einer CI/CD‑Pipeline automatisieren, sodass jeder neue Excel‑Report automatisch zu einem PPTX‑Folien‑Deck wird.  
* Dieser Ansatz mit **Apache POI** kombinieren, um Excel‑Dateien vorzuverarbeiten, bevor sie an Aspose.Cells übergeben werden.

---

## Fazit

Dieses Tutorial zeigte **wie man Excel** mit Aspose.Cells nach PowerPoint exportiert und deckte jeden Schritt vom Laden der Arbeitsmappe bis zum Speichern einer editierbaren `.pptx` ab. Sie können nun **Excel nach PPTX konvertieren**, **PowerPoint aus Excel erstellen** und **Excel als PowerPoint speichern** in Ihren Java‑Anwendungen mit Zuversicht. Experimentieren Sie mit den optionalen Einstellungen, um die Ausgabe exakt an Ihre Präsentationsanforderungen anzupassen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Excel mit Aspose.Cells für .NET in PowerPoint konvertiert: Ein vollständiger Leitfaden](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Wie man Excel nach PowerPoint exportiert – Schritt‑für‑Schritt‑Leitfaden](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Wie man Excel mit C# nach PowerPoint exportiert – Vollständiger Leitfaden](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}