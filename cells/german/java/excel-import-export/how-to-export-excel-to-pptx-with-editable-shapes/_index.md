---
category: general
date: 2026-11-25
description: Erfahren Sie, wie Sie Excel nach PPTX mit editierbaren Formen exportieren.
  Dieser Leitfaden zeigt außerdem, wie Sie den Druckbereich festlegen und Excel‑Diagramme
  für Präsentationen konvertieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: de
lastmod: 2026-11-25
og_description: Wie man Excel mit Aspose.Cells nach PPTX exportiert, wobei bearbeitbare
  Formen erhalten bleiben, sowie Tipps zum Festlegen des Druckbereichs und zur Konvertierung
  von Excel‑Diagrammen für Präsentationen.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: Wie man Excel nach PPTX mit editierbaren Formen exportiert
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Wie man Excel nach PPTX mit bearbeitbaren Formen exportiert
url: /de/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Excel nach PPTX mit editierbaren Formen exportiert

Wenn Sie **how to export Excel**-Dateien nach PowerPoint exportieren müssen, während editierbare Textfelder und Formen erhalten bleiben, führt Sie diese Anleitung durch den gesamten Prozess. Sie lernen außerdem, wie Sie **set print area** für eine fokussierte Folie festlegen und wie Sie **convert Excel chart**-Objekte konvertieren, sodass sie nach dem Export vollständig editierbar bleiben.

Das Exportieren von Excel nach PPTX ist üblich, wenn Präsentationsdecks aus datengetriebenen Berichten erstellt werden. Durch die Verwendung von Aspose.Cells für Java vermeiden Sie manuelles Kopieren und Einfügen, erhalten die Formatierung unverändert und erhalten programmatische Kontrolle über die Ausgabe.

## Was Sie lernen werden

* Laden Sie eine vorhandene XLSX-Arbeitsmappe, die ein Textfeld oder Diagramm enthält.  
* Konfigurieren Sie die Exportoptionen, sodass die resultierende PPTX-Datei **editable shapes** enthält.  
* **Set the print area** festlegen, um den exportierten Bereich auf die benötigten Zellen zu beschränken.  
* Speichern Sie das Arbeitsblatt als PPTX-Datei und überprüfen Sie, dass Textfelder und Diagramme in PowerPoint bearbeitet werden können.  

**Voraussetzungen**

* Java 17 oder neuer installiert.  
* Maven oder Gradle für das Abhängigkeitsmanagement.  
* Grundlegendes Verständnis von Excel-Arbeitsmappen und Java-Programmierung.

---

## Wie man Excel nach PPTX mit editierbaren Formen exportiert

Dieser Abschnitt liefert den Kerncode, der den Export durchführt. Das Beispiel verwendet Aspose.Cells 23.9 (die zum Zeitpunkt des Schreibens aktuelle Version) und demonstriert jeden erforderlichen Schritt.

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### Warum jede Zeile wichtig ist

1. **Dependency** – Aspose.Cells stellt die Klasse `ImageOrPrintOptions` bereit, die Arbeitsblätter als PPTX‑Folien rendern kann. Durch das Hinzufügen via Maven wird sichergestellt, dass die Bibliothek im Klassenpfad ist.  
2. **Imports** – Das Importieren der richtigen Klassen hält den Code sauber und vermeidet vollqualifizierte Namen.  
3. **Loading the workbook** – Sie müssen auf die genaue Datei verweisen, die die zu exportierenden Objekte enthält. Der Pfad kann absolut oder relativ zum Projektstammverzeichnis sein.  
4. **Export options** – Das Setzen von `setEditable(true)` ist der Schlüssel zu **how to export Excel**, damit die resultierenden PowerPoint‑Formen editierbar bleiben. Ohne dieses Flag werden Textfelder zu statischen Bildern.  
5. **Print area** – Der Aufruf `setPrintArea` begrenzt den Export auf den gewünschten Bereich, wodurch die Dateigröße reduziert und unerwünschte Zeilen/Spalten entfernt werden. Dies entspricht direkt der Anforderung **set print area excel**.  
6. **Saving** – Die Konstante `SaveFormat.PPTX` weist Aspose.Cells an, eine PowerPoint‑Datei statt eines Bildes oder PDFs zu erzeugen.  

#### Erwartete Ausgabe

Nach dem Ausführen des Programms öffnen Sie `EditableShapes.pptx` in PowerPoint. Sie sollten eine Folie sehen, die den ausgewählten Excel‑Bereich widerspiegelt, und alle Textfelder oder Diagrammlegenden können durch Doppelklick bearbeitet werden, genau wie native PowerPoint‑Objekte.

---

## Festlegen des Druckbereichs in Excel

Wenn Sie nur einen Teil des Arbeitsblatts benötigen, verbessert das Definieren eines **print area** sowohl die Leistung als auch die visuelle Klarheit.

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Tip:* Wenn Sie später den Datenbereich ändern, rufen Sie vor dem Export erneut `setPrintArea` auf. Der Export berücksichtigt die zuletzt eingestellte Einstellung.

---

## Konvertieren eines XLSX‑Diagramms in ein editierbares PowerPoint‑Diagramm

Aspose.Cells behandelt Diagramme als Zeichenobjekte. Durch Aktivieren von `setEditable(true)` wird das Diagramm in ein natives PowerPoint‑Diagramm konvertiert, das bearbeitet werden kann (z. B. Serien oder Achsentitel ändern).

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

Wenn Sie **how to convert xlsx**-Dateien mit mehreren Diagrammen benötigen, wiederholen Sie den Export für jedes Arbeitsblatt oder verwenden Sie `Workbook.save` mit `SaveFormat.PPTX`, nachdem Sie das aktive Blatt angepasst haben.

---

## Wie man XLSX programmgesteuert konvertiert (Bonus)

Neben PPTX möchten Sie die Arbeitsmappe möglicherweise auch in ein anderes Format wie PDF oder PNG konvertieren. Die gleiche Klasse `ImageOrPrintOptions` funktioniert für diese Ziele:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

Dies demonstriert die breitere **how to convert xlsx**-Fähigkeit von Aspose.Cells.

---

## Häufige Fallstricke und bewährte Tipps

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Formen werden zu Bildern | `setEditable(false)` (Standard) | Rufen Sie `exportOptions.setEditable(true)` auf |
| Exportierte Folie ist leer | Druckbereich enthält keine Daten | Überprüfen Sie den an `setPrintArea` übergebenen Bereichs‑String |
| Diagramm verliert Formatierung | Verwendung einer veralteten Aspose.Cells‑Version | Aktualisieren Sie auf die neueste Bibliothek (≥ 23.9) |
| Große Dateigröße | Export des gesamten Arbeitsblatts | Begrenzen Sie den Druckbereich oder blenden Sie ungenutzte Zeilen/Spalten aus |

---

## Fazit

Sie wissen jetzt, wie man **how to export Excel**-Arbeitsmappen nach PPTX mit vollständig editierbaren Formen und Diagrammen exportiert, wie man **set print area** festlegt, um die Ausgabe zu fokussieren, und wie man **convert Excel chart**‑Objekte für nahtlose Präsentationsbearbeitung konvertiert. Das vollständige, ausführbare Java‑Beispiel oben kann in jedes Projekt eingefügt werden, das bereits Aspose.Cells verwendet.

**Nächste Schritte**

* Erkunden Sie die **convert excel chart**‑Optionen in PowerPoint (z. B. Änderung des Diagrammtyps).  
* Kombinieren Sie diesen Export mit der **set print area excel**‑Automatisierung, um mehrere Folien aus einer einzigen Arbeitsmappe zu erzeugen.  
* Versuchen Sie, mit dem gleichen `ImageOrPrintOptions`‑Muster in andere Formate (PDF, PNG) zu exportieren.

Fühlen Sie sich frei, mit verschiedenen Bereichen, mehreren Arbeitsblättern oder benutzerdefinierten Folienlayouts zu experimentieren. Viel Spaß beim Programmieren!

## Was Sie als Nächstes lernen sollten

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to set print area excel and export to PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Convert Excel to PowerPoint and set print area](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}