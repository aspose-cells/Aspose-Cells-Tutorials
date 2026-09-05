---
category: general
date: 2026-09-05
description: Lernen Sie, wie Sie einen Bereich in Excel kopieren, Excel nach PowerPoint
  exportieren und Excel in pptx konvertieren, mit einem vollständigen Java‑Beispiel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: de
lastmod: 2026-09-05
og_description: Wie man einen Bereich kopiert und Excel mit Java nach PowerPoint exportiert.
  Folgen Sie dieser Schritt‑für‑Schritt‑Anleitung, um Excel effizient in PPTX zu konvertieren.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Wie man einen Bereich aus Excel kopiert und in Java nach PowerPoint exportiert
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Wie man einen Bereich aus Excel kopiert und ihn mit Java nach PowerPoint exportiert
url: /de/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man einen Bereich aus Excel kopiert und nach PowerPoint exportiert mit Java

Wenn Sie **how to copy range** aus einer Excel-Arbeitsmappe benötigen und dann **export excel to PowerPoint**, bietet Ihnen dieser Leitfaden eine vollständige, sofort einsatzbereite Lösung. Sie sehen genau, wie man einen Bereich mit Pivot‑Tabelle kopiert, ein neues Arbeitsblatt für die Kopie erstellt und schließlich **convert Excel to PPTX** mit einem einzigen Methodenaufruf.

Das Kopieren von Bereichen und das Exportieren von Arbeitsmappen ist ein häufiges Bedürfnis, wenn Sie Berichte, Präsentationen oder Dashboards programmgesteuert erstellen. Am Ende dieses Tutorials haben Sie ein Java‑Programm, das:

* Lädt eine vorhandene `.xlsx`‑Datei.
* Kopiert den Bereich `A1:H20` (einschließlich einer Pivot‑Tabelle) in ein neues Blatt.
* Speichert die Arbeitsmappe als editierbare `.pptx`‑Präsentation.

Sie benötigen nur die Aspose.Cells for Java‑Bibliothek; weitere Abhängigkeiten sind nicht erforderlich.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* Java 17 (oder neuer) installiert.
* Maven oder Gradle zur Verwaltung von Abhängigkeiten.
* Aspose.Cells for Java 23.9 (oder die neueste Version) – fügen Sie sie Ihrem Projekt hinzu, wie im Maven‑Snippet unten gezeigt.
* Eine Excel‑Datei (`input.xlsx`), die die Daten und die Pivot‑Tabelle enthält, die Sie kopieren möchten.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Schritt 1: Arbeitsmappe aus einer Datei laden

Der erste Vorgang in **how to copy range** besteht darin, die Quellarbeitsmappe zu öffnen. Dadurch erhalten Sie Zugriff auf Arbeitsblätter, Zellen und Pivot‑Tabellen.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Warum dieser Schritt?*  
Das Laden der Datei erstellt eine In‑Memory‑Repräsentation des Excel‑Dokuments, sodass Sie dessen Inhalt manipulieren können, ohne die Originaldatei zu berühren.

## Schritt 2: Das Quellarbeitsblatt ermitteln, das die Daten enthält

Typischerweise enthält das erste Blatt die Daten, die Sie kopieren möchten. Sie können es über den Index abrufen.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

Falls Ihre Arbeitsmappe die Pivot‑Tabelle auf einem anderen Blatt speichert, ersetzen Sie `0` durch den entsprechenden Index oder verwenden Sie `get("SheetName")`.

## Schritt 3: Ein neues Arbeitsblatt für den kopierten Bereich hinzufügen

Das Erstellen eines Zielblatts isoliert die kopierten Daten und erleichtert den späteren Export.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

Sie können das Blatt beliebig benennen; der Name „Copy“ signalisiert deutlich, dass es den duplizierten Bereich enthält.

## Schritt 4: Bereich kopieren (how to copy range) inklusive der Pivot‑Tabelle

Jetzt führen wir die Kernoperation **how to copy range** aus. Die Methode `copyRange` kopiert sowohl Werte als auch Formatierungen und bewahrt die Definition der Pivot‑Tabelle.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*Warum `CopyOptions` verwenden?*  
Durch die Bereitstellung einer `CopyOptions`‑Instanz können Sie feinabstimmen, was kopiert wird (z. B. Formeln, Spaltenbreiten). Der Standard‑Konstruktor kopiert alles, was ideal ist, wenn Sie eine exakte Kopie eines **copy pivot table sheet** möchten.

## Schritt 5: Optionen vorbereiten, um die Arbeitsmappe als editierbare PowerPoint‑Präsentation zu exportieren

Der Export nach PowerPoint erfolgt über `ImageOrPrintOptions`. Das Festlegen des Speicherformats auf `SaveFormat.PPTX` weist Aspose.Cells an, eine PowerPoint‑Datei anstelle eines Bildes zu erzeugen.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

Sie können über `pptOptions` auch die Folienabmessungen, DPI und andere Präsentationseinstellungen anpassen, falls Sie ein benutzerdefiniertes Layout benötigen.

## Schritt 6: Arbeitsmappe als PPTX‑Datei speichern (convert excel to pptx)

Zum Schluss rufen Sie `workbook.save` mit den PPTX‑Optionen auf. Dieser Schritt **how to export excel** in ein Foliendeck.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

Nach Abschluss des Programms enthält `output.pptx` eine einzelne Folie, auf der der kopierte Bereich exakt so angezeigt wird wie in Excel, einschließlich der Pivot‑Tabellen‑Steuerelemente.

### Erwartete Ausgabe

Öffnen Sie `output.pptx` in Microsoft PowerPoint oder einem kompatiblen Viewer. Sie sollten eine Folie mit dem Bereich `A1:H20` sehen, wobei Zellfarben, Rahmen und das Layout der Pivot‑Tabelle erhalten bleiben. Die Folie ist vollständig editierbar – Sie können die Tabelle verschieben, die Größe ändern oder formatieren, genau wie jedes native PowerPoint‑Element.

## Vollständiges ausführbares Beispiel

Wenn Sie alle Schritte zusammenführen, erhalten Sie eine eigenständige Java‑Klasse:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

Führen Sie die Klasse aus Ihrer IDE oder über die Befehlszeile aus:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

Sie sehen die Bestätigungsnachricht, sobald die Datei geschrieben wurde.

## Häufige Fragen und Sonderfälle

| Frage | Antwort |
|----------|--------|
| **Kann ich einen nicht zusammenhängenden Bereich kopieren?** | Verwenden Sie `copyRange` mit einem benannten Bereich, der mehrere Bereiche umfasst, oder rufen Sie `copyRange` mehrmals für jeden Block auf. |
| **Was ist, wenn das Quellblatt mehrere Pivot‑Tabellen enthält?** | Jede Pivot‑Tabelle innerhalb des kopierten Rechtecks wird übertragen. Tabellen außerhalb des Rechtecks müssen separat kopiert werden. |
| **Wie exportiere ich mehrere Blätter als separate Folien?** | Iterieren Sie über die Arbeitsblätter, kopieren Sie jedes in ein temporäres Blatt und rufen Sie `workbook.save` mit `pptOptions` für jede Iteration auf, wobei Sie über die `Presentation`‑API an dieselbe PPTX anhängen. |
| **Ist die erzeugte PPTX editierbar?** | Ja. Der Export erzeugt native PowerPoint‑Objekte, sodass Sie Text ändern, Tabellen neu anordnen oder nachträglich Animationen hinzufügen können. |
| **Wie sieht es mit großen Arbeitsmappen aus?** | Erhöhen Sie `pptOptions.setDpi(300)` für höhere Detailgenauigkeit, achten Sie jedoch auf den Speicherverbrauch; verarbeiten Sie bei Bedarf Blätter stapelweise. |

## Pro‑Tipps

* **Spaltenbreiten erhalten** – setzen Sie `CopyOptions.setColumnWidth(true)` vor dem Kopieren, wenn Sie eine exakte Breitenübereinstimmung benötigen.
* **Benutzerdefinierte Foliengröße verwenden** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` um eine 16:9‑Präsentation zu entsprechen.
* **Titelfolie hinzufügen** – nach dem Export öffnen Sie die PPTX mit Aspose.Slides und fügen vorne eine Folie mit Titel und Datum ein.

## Fazit

Sie wissen jetzt, **how to copy range** aus einer Excel‑Arbeitsmappe zu kopieren, **export excel to PowerPoint** durchzuführen und **convert excel to pptx** mit Java zu erledigen. Wenn Sie die oben genannten sechs Schritte befolgen, können Sie die Berichtserstellung automatisieren, Folien aus Live‑Daten erzeugen und die Pivot‑Tabellen‑Funktionalität intakt halten.

### Was kommt als Nächstes?

* Erkunden Sie Varianten von **copy pivot table sheet**, z. B. das Kopieren nur des Pivot‑Caches.
* Kombinieren Sie diesen Workflow mit **Aspose.Slides**, um benutzerdefinierte Animationen oder Branding hinzuzufügen.
* Automatisieren Sie die Stapelverarbeitung für Dutzende von Arbeitsmappen in einem geplanten Job.

Probieren Sie die Optionen gern aus und passen Sie den Code an Ihre eigene Reporting‑Pipeline an. Wenn Sie auf Probleme stoßen, bietet die Aspose.Cells for Java‑Dokumentation tiefere Einblicke in `CopyOptions` und `ImageOrPrintOptions`. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}