---
category: general
date: 2026-06-18
description: Erstelle ein Java‑Tutorial zum Erzeugen einer Excel‑Datei, das zeigt,
  wie man die Zeilenhintergrundfarbe festlegt, Excel aus einer DataTable generiert
  und die Arbeitsmappe als XLSX mit wechselnder Zeilenfarbgebung speichert.
draft: false
keywords:
- create excel file java
- set row background color
- save workbook as xlsx
- alternating row shading excel
- generate excel from datatable
language: de
og_description: Excel-Datei in Java Schritt für Schritt erstellen. Lernen Sie, die
  Zeilenhintergrundfarbe festzulegen, abwechselnde Zeilenfarbgebung anzuwenden, Excel
  aus DataTable zu generieren und die Arbeitsmappe als XLSX zu speichern.
og_title: Excel-Datei in Java erstellen – Vollständiger Leitfaden für Styling und
  Export
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  headline: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  type: TechArticle
- description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  name: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  steps:
  - name: Exporting a Large DataTable
    text: 'When dealing with 100k+ rows, you may hit memory limits. Aspose.Cells supports
      **streaming** mode:'
  - name: Using Apache POI Instead of Aspose.Cells
    text: 'If licensing is a concern, you can replace the import logic with POI’s
      `CellStyle` objects. The concept stays the same: create two `CellStyle`s, loop
      over rows, and apply `setFillForegroundColor` with `IndexedColors`. The only
      downside is the code becomes a bit more verbose.'
  - name: Adding Conditional Formatting
    text: 'Suppose you want to highlight any score above 90 in green. Add this after
      the import:'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- data-export
title: Excel-Datei in Java erstellen – Vollständige Anleitung mit Zeilenformatierung
  und XLSX‑Export
url: /de/java/excel-import-export/create-excel-file-java-full-guide-with-row-styling-and-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Datei mit Java erstellen – Vollständige Anleitung mit Zeilenformatierung und XLSX‑Export

Haben Sie sich schon einmal gefragt, wie man **excel file java** erstellt, das sofort professionell aussieht? Sie sind nicht allein – Entwickler benötigen häufig eine schnelle Möglichkeit, tabellarische Daten in ein schön formatiertes Spreadsheet zu verwandeln, ohne Excel manuell zu öffnen. In diesem Tutorial führen wir Sie durch eine komplette Lösung: Daten aus einer `DataTable` übernehmen, **alternating row shading excel** anwenden und schließlich **save workbook as xlsx**. Am Ende haben Sie einen wiederverwendbaren Code‑Snippet, den Sie in jedes Java‑Projekt einbinden können.

Wir decken alles ab, was Sie benötigen: die erforderliche Bibliothek (Aspose.Cells für Java), den genauen Code zum Setzen der **row background color**, wie man **generate excel from datatable** erzeugt und ein paar praktische Tipps, um häufige Stolperfallen zu vermeiden. Kein Schnickschnack, nur ein solides, sofort ausführbares Beispiel, das Sie noch heute anpassen können.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- Java 17 oder höher (der Code funktioniert mit jeder aktuellen JDK)
- Maven oder Gradle zur Verwaltung der Abhängigkeiten
- Grundlegendes Verständnis von Java‑Collections
- Zugriff auf die Aspose.Cells für Java‑Bibliothek (Kostenlose Testversion oder lizenziert)

Falls Sie eine Open‑Source‑Alternative bevorzugen, lässt sich die Logik leicht auf Apache POI übertragen – einfach die API‑Aufrufe austauschen. Der Kürze halber bleiben wir bei Aspose.Cells, da dessen `importDataTable`‑Methode den Schritt **generate excel from datatable** zu einem Einzeiler macht.

## Schritt 1: Projekt einrichten und Aspose.Cells hinzufügen

Fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` (Maven) oder `build.gradle` (Gradle) hinzu. Damit wird die Kernbibliothek eingebunden, die das Arbeiten mit Workbooks, Styles und Farben ermöglicht.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

Nach dem Aktualisieren Ihres Projekts können Sie Java‑Code schreiben, der **create excel file java** im Stil erzeugt.

## Schritt 2: Workbook erstellen und Daten laden

Zuerst instanziieren wir ein frisches `Workbook`. Dann erhalten wir eine `DataTable` – das kann das Ergebnis einer JDBC‑Abfrage, eines CSV‑Parsers oder irgendeiner In‑Memory‑Tabelle sein, die Sie bereits besitzen.

```java
import com.aspose.cells.*;

public class ExcelExporter {

    // Simulated method that returns a DataTable with dummy data
    private static DataTable getData() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("Name", DataType.STRING);
        dt.getColumns().add("Score", DataType.DOUBLE);

        // Add some rows
        dt.getRows().add(new Object[]{1, "Alice", 92.5});
        dt.getRows().add(new Object[]{2, "Bob", 85.0});
        dt.getRows().add(new Object[]{3, "Charlie", 78.3});
        dt.getRows().add(new Object[]{4, "Diana", 88.9});
        return dt;
    }

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (or load an existing one)
        Workbook workbook = new Workbook();

        // Step 2: Obtain the data to be written as a DataTable
        DataTable dataTable = getData(); // assume this returns the source data
```

Jetzt haben wir ein leeres Workbook und eine befüllte `DataTable`. Der nächste Schritt ist, wo die visuelle Magie einsetzt.

## Schritt 3: Zeilen‑Styles definieren – Hintergrundfarbe der Zeile setzen

Wir möchten jeder Zeile einen eigenen Hintergrund zuweisen, abwechselnd hellblau und hellgrau. Das verbessert die Lesbarkeit, besonders bei großen Berichten. Der nachfolgende Code erstellt ein `Style`‑Array – einen Eintrag pro Datenzeile – und weist basierend auf dem Zeilenindex eine **set row background color** zu.

```java
        // Step 3: Prepare an array of row styles – one style per data row
        Style[] rowStyles = new Style[dataTable.getRows().size()];
        for (int i = 0; i < rowStyles.length; i++) {
            rowStyles[i] = workbook.createStyle();

            // Step 4: Alternate background colors for better readability
            if (i % 2 == 0) {
                // Even rows – light blue
                rowStyles[i].setForegroundColor(Color.getLightBlue());
            } else {
                // Odd rows – light gray
                rowStyles[i].setForegroundColor(Color.getLightGray());
            }
            // Apply solid fill pattern
            rowStyles[i].setPattern(BackgroundType.SOLID);
        }
```

Beachten Sie, dass wir `Color.getLightBlue()` und `Color.getLightGray()` verwenden. Aspose.Cells bietet eine umfangreiche Palette, Sie können diese Aufrufe jedoch durch jede beliebige `Color` ersetzen – etwa Ihre Unternehmensfarben.

## Schritt 4: DataTable mit Styling importieren

Jetzt bringen wir die Daten und das Style‑Array zusammen. Die Methode `importDataTable` übernimmt das Kopieren der Zeilen, das Anwenden des entsprechenden Styles und fügt sogar Spaltenüberschriften hinzu, wenn Sie `true` für das Flag `importColumnNames` übergeben.

```java
        // Step 5: Import the DataTable into the first worksheet using the styles
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.getCells().importDataTable(dataTable, true, "A1", rowStyles);
```

Der Anker `"A1"` sagt Aspose, wo das Schreiben beginnen soll – obere linke Ecke des Sheets. Da wir das `rowStyles`‑Array übergeben haben, erbt jede Zeile die zuvor festgelegte Hintergrundfarbe und wir erhalten **alternating row shading excel**, ohne nach dem Import noch eine Schleife ausführen zu müssen.

## Schritt 5: Das formatierte Workbook als XLSX speichern

Abschließend speichern wir das Workbook auf dem Datenträger. Die Methode `save` ermittelt das Format automatisch anhand der Dateierweiterung, sodass die Verwendung von `.xlsx` ein modernes Office Open XML‑Workbook erzeugt, das in Excel, Google Sheets oder LibreOffice geöffnet werden kann.

```java
        // Step 6: Save the styled workbook to a file
        workbook.save("styledTable.xlsx"); // save workbook as xlsx
        System.out.println("Excel file created successfully!");
    }
}
```

Wenn Sie die `main`‑Methode ausführen, entsteht eine Datei namens `styledTable.xlsx` im Stammverzeichnis Ihres Projekts. Öffnen Sie sie, und Sie sehen eine sauber formatierte Tabelle mit abwechselnden Zeilenfarben – genau das, was ein Business‑Stakeholder von einem Bericht erwartet.

![Screenshot einer mit Java erstellten, formatierten Excel‑Datei](images/styled_excel_java.png "Beispiel für create excel file java")

*Bild‑Alt‑Text:* **create excel file java** Screenshot, der abwechselnde Zeilenfarbgebung zeigt

## Warum dieser Ansatz besser funktioniert als manuelles Styling Zelle für Zelle

Sie fragen sich vielleicht, warum wir ein Style‑Array verwenden, anstatt nach dem Import jede Zeile zu durchlaufen. Die Antwort ist zweifach:

1. **Performance** – Das Anwenden eines Styles während des Imports vermeidet einen zusätzlichen Durchlauf über das Arbeitsblatt, was bei tausenden Zeilen kostspielig sein kann.
2. **Wartbarkeit** – Die Style‑Logik befindet sich an einer einzigen Stelle (`rowStyles`), sodass Sie Farben, Rahmen oder das Muster leicht ändern können, ohne den Importcode zu berühren.

Falls Sie später weitere visuelle Hinweise hinzufügen möchten (z. B. Zeilen mit einem Score unter einem Schwellenwert hervorheben), erweitern Sie einfach den `if`‑Block innerhalb der Schleife – keine weiteren Änderungen nötig.

## Häufige Varianten und Sonderfälle

### Export einer großen DataTable

Bei 100 k+ Zeilen können Speichergrenzen erreicht werden. Aspose.Cells unterstützt den **streaming**‑Modus:

```java
Workbook wb = new Workbook(FileFormatType.XLSX);
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

Setzen Sie die Memory‑Preference, bevor Sie Styles erstellen, und die Bibliothek schreibt Daten in temporäre Dateien statt alles im RAM zu halten.

### Verwendung von Apache POI statt Aspose.Cells

Wenn Lizenzkosten ein Thema sind, können Sie die Import‑Logik durch POIs `CellStyle`‑Objekte ersetzen. Das Konzept bleibt gleich: zwei `CellStyle`s erstellen, über die Zeilen iterieren und `setFillForegroundColor` mit `IndexedColors` anwenden. Der Nachteil ist, dass der Code etwas ausführlicher wird.

### Bedingte Formatierung hinzufügen

Angenommen, Sie möchten jeden Score über 90 grün hervorheben. Fügen Sie nach dem Import Folgendes hinzu:

```java
FormatConditionCollection fcc = sheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
Style conditionStyle = workbook.createStyle();
conditionStyle.setForegroundColor(Color.getLightGreen());
conditionStyle.setPattern(BackgroundType.SOLID);
fc.setStyle(conditionStyle);
```

Jetzt besitzt das Arbeitsblatt nicht nur abwechselnde Schattierungen, sondern auch dynamische Hervorhebungen.

## Zusammenfassung: Was wir erreicht haben

- **Create excel file java** aus einer `DataTable` mit Aspose.Cells.
- **Set row background color** programmgesteuert, wodurch **alternating row shading excel** entsteht.
- **Save workbook as xlsx**, sodass die Datei mit modernen Tabellenkalkulations‑Tools kompatibel ist.
- Demonstriert, wie man **generate excel from datatable** effizient und erweiterbar umsetzt.

All das passt in eine kompakte, leicht lesbare Java‑Klasse, die Sie einfach in Ihr eigenes Projekt kopieren können.

## Nächste Schritte und verwandte Themen

Wenn Ihnen dieser Durchgang gefallen hat, könnten Sie auch folgende Themen erkunden:

- **Exportieren von Diagrammen** aus Java nach Excel (Aspose.Cells Chart API).
- **Passwortschutz** für das erzeugte Workbook (`workbook.protect(...)`).
- **Große Datensätze schreiben** mit Streaming, um den Speicherverbrauch gering zu halten.
- **Integration mit Spring Boot**, um die erzeugte Datei als herunterladbare Antwort bereitzustellen.

All diese Themen bauen auf dem hier dargelegten Fundament auf – also experimentieren Sie gern und erweitern Sie die Lösung.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen oder Ideen für weitere Verbesserungen haben, hinterlassen Sie einen Kommentar unten. Lassen Sie uns die Diskussion am Laufen halten.*

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungs‑Ansätze in Ihren eigenen Projekten erkunden können.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Set Excel Row Heights Using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/mastering-excel-row-heights-aspose-cells-java/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}