---
category: general
date: 2026-07-03
description: Formel-Export in Java einbinden, um Excel‑Zellen mit Aspose.Cells in
  Text zu konvertieren. Erfahren Sie, wie Sie einen Excel‑Bereich ausgeben und Zellwerte
  effizient als Zeichenkette erhalten.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: de
og_description: Formeln‑Export in Java einbinden, um Excel‑Zellen in Text zu konvertieren.
  Schritt‑für‑Schritt‑Anleitung, die zeigt, wie man einen Excel‑Bereich ausgibt und
  Zellwerte als Zeichenkette abruft.
og_title: Formeln‑Export in Java einbinden – Excel‑Zellen in Text umwandeln
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Formel-Export in Java einbinden – Excel‑Zellen in Text konvertieren
url: /de/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formeln‑Export in Java einbinden – Excel‑Zellen in Text konvertieren

Haben Sie schon einmal **Formeln‑Export einbinden** müssen, wenn Sie Daten aus einer Excel‑Arbeitsmappe auslesen? Vielleicht bauen Sie einen Reporting‑Service, der die ursprünglichen Formeln erhalten muss, während er dennoch einen sauberen Text‑Blob liefert. In diesem Fall sind Sie hier genau richtig. Dieser Leitfaden führt Sie Schritt für Schritt durch die Konvertierung von Excel‑Zellen in Klartext — *einschließlich* aller eingebetteten Formeln — mit Aspose.Cells für Java.

Wir gehen außerdem darauf ein, wie man **Excel‑Bereich druckt**, **Export‑Tabellen‑Optionen** anpasst und schließlich **Zellwerte als String** erhält, die Sie protokollieren, über eine API senden oder in einer Datenbank ablegen können. Am Ende haben Sie ein vollständig ausführbares Snippet und ein solides Verständnis dafür, warum jeder Aufruf nötig ist.

## Was Sie am Ende wissen werden

- Ein komplettes, copy‑paste‑fertiges Java‑Programm, das eine `.xlsx`‑Datei liest, einen Bereich auswählt und ihn als formatierte Zeichenkette exportiert.
- Ein Verständnis der Klasse `ExportTableOptions` und warum das Umschalten von `setExportAsString` und `setIncludeFormula` wichtig ist.
- Tipps zum Umgang mit großen Arbeitsblättern, verschiedenen Datentypen und zur Anpassung des Ausgabeformats.
- Eine kurze Checkliste für häufige Stolperfallen (z. B. zusammengeführte Zellen, ausgeblendete Zeilen und länderspezifische Zahlenformate).

### Voraussetzungen

- Java 17 oder neuer (der Code kompiliert auch mit älteren Versionen, wir verwenden jedoch das aktuelle LTS).
- Aspose.Cells für Java 23.10 (oder eine neuere Version) — Sie können das Paket von Maven Central beziehen.
- Eine Beispiel‑`input.xlsx` in einem Ordner Ihrer Wahl (der Pfad ist im Beispiel aus Gründen der Übersicht fest codiert).

Wenn Sie das bereits haben, legen wir los.

## Schritt 1: Projekt einrichten und Abhängigkeiten hinzufügen

Erstellen Sie zunächst ein Maven‑Projekt (oder Gradle, falls Sie das bevorzugen). Fügen Sie die Aspose.Cells‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro‑Tipp:** Wenn Sie einen Unternehmens‑Proxy verwenden, stellen Sie sicher, dass das Repository erreichbar ist; sonst schlägt der Build mit einem „Could not resolve dependencies“-Fehler fehl.

Sobald Maven die Bibliotheken heruntergeladen hat, können Sie mit dem Schreiben von Java beginnen.

## Schritt 2: Arbeitsmappe laden und gewünschtes Arbeitsblatt holen

Die erste Zeile des Code‑Beispiels zeigt, wie man eine vorhandene Arbeitsmappe öffnet:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten oder relativen Pfad zu Ihrer Datei. Der `Workbook`‑Konstruktor erkennt das Dateiformat automatisch (XLS, XLSX, CSV usw.), sodass Sie es nicht explizit angeben müssen.

Anschließend holen wir das erste Blatt:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Warum das erste Blatt? In vielen Vorlagen befinden sich die Daten auf dem ersten Tab, Sie können jedoch jeden Index verwenden oder `get("SheetName")` nutzen, wenn Sie lieber einen benannten Ansatz bevorzugen.

## Schritt 3: Den zu exportierenden Bereich definieren

Jetzt kommt das Herzstück der **convert excel cells text**‑Operation. Sie teilen Aspose.Cells mit, welche Zellen Sie ziehen möchten, indem Sie ein `Range`‑Objekt erstellen:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

Der String `"A1:C3"` ist eine klassische A1‑Adressierung. Er kann auch programmgesteuert gebaut werden:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Diese Flexibilität hilft, wenn die Bereichsgröße dynamisch ist — z. B. wenn Sie die zuletzt genutzte Zeile mit `ws.getCells().getMaxDataRow()` auslesen.

## Schritt 4: Export‑Tabellen‑Optionen konfigurieren, um Formeln einzuschließen

Hier steckt die Magie des **include formulas export**. Standardmäßig liefert Aspose.Cells die *angezeigten* Werte. Enthält eine Zelle `=SUM(A1:A3)`, erhalten Sie die berechnete Zahl, nicht den Formelt‑Text. Um das zu ändern, richten Sie `ExportTableOptions` ein:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Warum beide Flags? `setExportAsString(true)` weist die API an, die Zellen mit dem Standard‑Trennzeichen zu verketten (Tab für Spalten, Zeilenumbruch für Zeilen). `setIncludeFormula(true)` schaltet die Wertequelle von „angezeigtem Wert“ auf „rohe Formel“ um. Wenn Sie nur Werte wollen, lassen Sie es auf `false`.

### Optionale Anpassungen

- `eto.setExportHiddenRows(true);` — ausgeblendete Zeilen mit exportieren.
- `eto.setExportHiddenColumns(true);` — das Gleiche für Spalten.
- `eto.setExportAsHTML(true);` — HTML statt Klartext erhalten.

Fühlen Sie sich frei zu experimentieren; die Options‑Klasse ist ein **export table options**‑Spielplatz.

## Schritt 5: Den Bereich als formatierte Zeichenkette abrufen

Jetzt ziehen wir die Daten:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Der zurückgegebene `txt` sieht etwa so aus (angenommen A1:C3 enthält eine Mischung aus Werten und Formeln):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Beachten Sie das Tab (`\t`) zwischen den Spalten und den Zeilenumbruch (`\n`) zwischen den Zeilen. Sie können die Zeichenkette später splitten, wenn Sie ein 2‑D‑Array benötigen:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Schritt 6: Ergebnis ausgeben – „Print Excel Range“ leicht gemacht

Abschließend geben wir die Zeichenkette auf der Konsole aus:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Beim Ausführen des Programms wird exakt die oben gezeigte Ausgabe gedruckt. Von hier aus könnten Sie die Zeichenkette in eine Log‑Datei schreiben, über HTTP senden oder in einem NoSQL‑Dokument speichern.

## Vollständiges, sofort ausführbares Beispiel

Alles zusammengefügt, hier das komplette Programm. Kopieren, einfügen und **Run** klicken — keine fehlenden Importe.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Erwartete Ausgabe (Beispiel)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Enthält Ihre Arbeitsmappe Zahlen, die als Datum formatiert sind, erscheinen sie im länderspezifischen Format (z. B. `2026‑07‑03`). Um ISO‑Datumsangaben zu erzwingen, können Sie `ExportTableOptions` mit einem benutzerdefinierten `NumberFormat` anpassen.

## Edge Cases und häufige Fragen

### Was, wenn der Bereich zusammengeführte Zellen enthält?

Zusammengeführte Zellen werden als Wert der oberen‑linken Zelle behandelt. Der Rest des zusammengeführten Bereichs erscheint als leere Zeichenkette. Wenn Sie die Adresse des zusammengeführten Bereichs benötigen, fragen Sie vor dem Export `Cell.getMergedRange()` ab.

### Kann ich ein riesiges Blatt (Hunderttausende Zeilen) exportieren?

Ja, aber achten Sie auf den Speicherverbrauch. Verwenden Sie `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, damit Aspose.Cells Daten auf die Festplatte streamt. Außerdem empfiehlt es sich, in Chunks zu exportieren (z. B. 10 000 Zeilen auf einmal), um die Zeichenkette handhabbar zu halten.

### Wie ändere ich das Spaltentrennzeichen?

`ExportTableOptions` stellt `setSeparator(char separator)` bereit. Für CSV‑ähnliche Ausgabe setzen Sie es auf `','`:

```java
eto.setSeparator(',');
```

### Respektieren Formeln externe Verweise?

Zeigt eine Formel auf eine andere Arbeitsmappe, behält Aspose.Cells den Referenz‑Text bei (`='[Other.xlsx]Sheet1'!A1`). Der externe Wert wird nicht ausgewertet, es sei denn, Sie laden auch die referenzierte Arbeitsmappe.

## Pro‑Tipps für produktionsreifen Code

- **Cache die Arbeitsmappe**, wenn Sie sie häufig lesen…

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Features zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}