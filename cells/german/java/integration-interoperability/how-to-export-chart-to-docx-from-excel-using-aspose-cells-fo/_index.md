---
category: general
date: 2026-08-20
description: Erfahren Sie, wie Sie ein Diagramm in ein DOCX exportieren und eine Excel‑Arbeitsmappe
  mit Aspose.Cells in Java in ein DOCX konvertieren. Schritt‑für‑Schritt‑Anleitung
  mit vollständigem Code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: de
lastmod: 2026-08-20
og_description: Exportieren Sie das Diagramm nach DOCX und konvertieren Sie die Excel‑Arbeitsmappe
  in DOCX mit Aspose.Cells für Java. Folgen Sie diesem vollständigen, ausführbaren
  Tutorial.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Diagramm in docx exportieren mit Aspose.Cells – Java‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Wie man ein Diagramm aus Excel in ein DOCX exportiert mit Aspose.Cells für
  Java
url: /de/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm aus einer Excel-Arbeitsmappe mit Java in DOCX exportieren

Wenn Sie **export chart to docx** direkt aus einer Excel-Datei benötigen, zeigt Ihnen dieses Tutorial eine sofort einsatzbereite Lösung. Am Ende der Anleitung wissen Sie außerdem, wie Sie **convert Excel workbook to docx** durchführen können, wobei ein editierbares Diagramm erhalten bleibt, sodass das resultierende Word-Dokument ohne Qualitätsverlust bearbeitet werden kann.

Das Exportieren von Diagrammen ist üblich, wenn Sie Berichte erstellen, die Tabellenkalkulationsberechnungen mit umfangreichen Word-Layouts kombinieren. Aspose.Cells for Java macht die Konvertierung unkompliziert, und die API ermöglicht es, das Diagramm editierbar zu behalten – kein statisches Bild erforderlich.

## Was dieses Tutorial abdeckt

* Laden einer vorhandenen Arbeitsmappe, die ein Diagramm enthält.  
* Konfigurieren von `ImageOrPrintOptions`, um das DOCX-Format anzusteuern.  
* Aktivieren des `ExportEditableCharts`-Flags (verfügbar ab Version 25.10).  
* Speichern der Arbeitsmappe als DOCX-Datei, die ein editierbares Diagramm beibehält.  

Keine externen Werkzeuge sind über die Aspose.Cells JAR hinaus erforderlich. Der Code funktioniert mit Java 8+ und jeder aktuellen Version von Aspose.Cells.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| **Aspose.Cells for Java** (v25.10 oder neuer) | Die `setExportEditableCharts`-Funktion wurde in diesem Release eingeführt. |
| **Java Development Kit (JDK) 8 oder neuer** | Stellt die Laufzeit zum Kompilieren und Ausführen des Beispiels bereit. |
| **Eine Excel-Arbeitsmappe (`.xlsx`), die mindestens ein Diagramm enthält** | Das Diagramm ist das Objekt, das nach DOCX exportiert wird. |
| **Eine Java-IDE oder ein Build-Tool (z. B. Maven, Gradle)** | Vereinfacht das Verwalten von Abhängigkeiten und die Ausführung. |

Sie können die neueste Aspose.Cells JAR von der [Aspose-Website](https://products.aspose.com/cells/java/) herunterladen.

## Schritt 1: Projekt einrichten und die Aspose.Cells-Abhängigkeit hinzufügen

Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Für Gradle fügen Sie hinzu:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Profi‑Tipp:** Verwenden Sie die genaue Version, die `ExportEditableCharts` (25.10) eingeführt hat, oder eine neuere Version. Ältere Versionen ignorieren das Flag und erzeugen stattdessen ein statisches Bild.

## Schritt 2: Arbeitsmappe laden, die das Diagramm enthält

Die Klasse `Workbook` repräsentiert die gesamte Excel-Datei. Das Laden erfolgt in einer einzigen Zeile:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Warum das wichtig ist:** Die Arbeitsmappe muss vollständig geladen sein, bevor Sie Exportoptionen anwenden können. Wenn der Dateipfad falsch ist, wirft Aspose.Cells eine `FileNotFoundException`.

## Schritt 3: Bild‑/Druckoptionen für DOCX-Ausgabe konfigurieren

`ImageOrPrintOptions` steuert, wie die Arbeitsmappe gerendert wird. Durch das Setzen des Speicherformats auf `DOCX` wird Aspose.Cells angewiesen, ein Word‑Dokument anstelle eines Bildes zu erzeugen.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Sie können hier auch die Seitengröße, DPI oder Bildqualität anpassen, aber das ist für den Diagramm‑Export optional.

## Schritt 4: Export editierbarer Diagramme aktivieren

Ab Version 25.10 kann Aspose.Cells Diagramme als native Word‑Diagrammobjekte einbetten. Dadurch sind sie in Microsoft Word vollständig editierbar.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Sonderfall:** Wenn Sie dieses Flag auf `false` setzen (oder weglassen), wird das Diagramm als statisches Bild gerendert. Verwenden Sie `true` nur, wenn die Zielgruppe das Diagramm nach der Konvertierung bearbeiten muss.

## Schritt 5: Arbeitsmappe als DOCX-Datei speichern

Rufen Sie schließlich `Workbook.save` mit den konfigurierten Optionen auf:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Wenn das Programm beendet ist, öffnen Sie `ChartEditable.docx` in Microsoft Word. Sie sollten das ursprüngliche Diagramm sehen, und wenn Sie mit der rechten Maustaste darauf klicken, ist die Option **Edit Data** verfügbar – was bestätigt, dass das Diagramm wirklich editierbar ist.

## Vollständiges, ausführbares Beispiel

Unten finden Sie die vollständige Quelldatei. Kopieren Sie sie in Ihre IDE, ersetzen Sie `YOUR_DIRECTORY` durch einen absoluten oder relativen Pfad und führen Sie sie aus.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Erwartete Ausgabe**

* Eine Datei namens `ChartEditable.docx` im angegebenen Verzeichnis.  
* Beim Öffnen der Datei in Word wird das Diagramm exakt so angezeigt, wie es in Excel erschien, und Sie können das Diagramm doppelklicken, um seine Datenreihen zu bearbeiten.

## Häufige Fallstricke und wie man sie vermeidet

| Symptom | Ursache | Lösung |
|---------|---------|--------|
| Word zeigt ein **static image** statt eines editierbaren Diagramms | `setExportEditableCharts` nicht aufgerufen oder Version < 25.10 verwendet | Stellen Sie sicher, dass das Flag auf `true` gesetzt ist und Sie Aspose.Cells 25.10 oder neuer verwenden. |
| Das erzeugte DOCX ist **blank** | Falscher Dateipfad für die Quellarbeitsmappe oder unzureichende Berechtigungen | Überprüfen Sie den Pfad der Arbeitsmappe und dass die Anwendung Lese‑/Schreibzugriff hat. |
| Diagrammlayout sieht **distorted** aus | Seiteneinrichtung in Excel (z. B. ausgeblendete Zeilen/Spalten) unterscheidet sich von den Word‑Standardwerten | Passen Sie `ImageOrPrintOptions` an (z. B. `setOnePagePerSheet(true)`), um die Skalierung zu steuern. |
| **Performance** verschlechtert sich bei großen Arbeitsmappen | Exportieren vieler Diagramme oder großer Datensätze | Exportieren Sie nur die benötigten Arbeitsblätter oder verwenden Sie `setSheetIndex`, um die Verarbeitung zu begrenzen. |

## Erweiterung der Lösung

* **Mehrere Diagramme:** Durchlaufen Sie alle Arbeitsblätter und rufen Sie `worksheet.getCharts()` auf, um jedes Diagramm einzeln zu exportieren.  
* **Benutzerdefiniertes DOCX‑Styling:** Nach dem Speichern verwenden Sie Aspose.Words, um Kopf‑ und Fußzeilen oder Stile auf das erzeugte Dokument anzuwenden.  
* **Batch‑Konvertierung:** Verpacken Sie den Code in einer Schleife, die ein Verzeichnis von `.xlsx`‑Dateien verarbeitet und für jede ein DOCX erzeugt.

## Fazit

Sie haben nun eine zuverlässige Methode, um **export chart to docx** und **convert Excel workbook to docx** durchzuführen, wobei die vollständige Editierbarkeit des Diagramms erhalten bleibt. Die wichtigsten Schritte sind das Laden der Arbeitsmappe, das Konfigurieren von `ImageOrPrintOptions` für DOCX, das Aktivieren von `ExportEditableCharts` und das Speichern des Ergebnisses.

Experimentieren Sie mit zusätzlichen Optionen – z. B. dem Festlegen von Seitenrändern oder dem Einbetten der Formeln der Arbeitsmappe – um die Ausgabe an Ihren Reporting‑Workflow anzupassen. Wenn Sie programmgesteuert Word‑Berichte aus Excel‑Daten erzeugen müssen, bietet dieser Ansatz eine saubere, wartbare Lösung.

--- 

*Bereit, es auszuprobieren? Klonen Sie das Beispiel, aktualisieren Sie die Dateipfade und führen Sie das Programm aus. Wenn Sie auf Probleme stoßen, konsultieren Sie die Aspose.Cells for Java‑Dokumentation oder erkunden Sie die nachstehenden verwandten Themen.*

### Verwandte Themen, die Sie als Nächstes erkunden könnten

* **convert excel workbook to pdf** – PDF‑Berichte aus derselben Arbeitsmappe erzeugen.  
* **Aspose.Cells chart formatting** – Farben, Markierungen und Achsen vor dem Export anpassen.  
* **Embedding images in DOCX with Aspose.Words** – Diagramme mit anderem Word‑Inhalt kombinieren.  

Happy coding!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automate Excel Chart Access Using Aspose.Cells Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}