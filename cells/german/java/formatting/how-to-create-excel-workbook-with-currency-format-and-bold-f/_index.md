---
category: general
date: 2026-08-20
description: Erstelle eine Excel-Arbeitsmappe in Java mit Aspose.Cells, setze das
  Währungsformat, füge fette Schrift hinzu und importiere ein Stil-Array für formatierte
  Zellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: de
lastmod: 2026-08-20
og_description: Erstellen Sie eine Excel‑Arbeitsmappe in Java, setzen Sie das Währungsformat,
  fügen Sie fette Schrift hinzu und lernen Sie, wie Sie den Stil mit Aspose.Cells
  importieren.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Erstelle Excel-Arbeitsmappe mit formatierten Währungszellen in Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Wie man in Java eine Excel-Arbeitsmappe mit Währungsformat und fetter Schrift
  erstellt
url: /de/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine Excel-Arbeitsmappe mit Währungsformat und fetter Schrift in Java erstellt

Wenn Sie programmgesteuert **eine Excel-Arbeitsmappe erstellen** müssen, zeigt Ihnen diese Anleitung genau, wie es geht. Wir gehen Schritt für Schritt durch das Erstellen einer Arbeitsmappe, das Anwenden eines Währungsformats, das Hinzufügen einer fetten Schrift und die Nutzung der **how to import style**‑Funktion von Aspose.Cells, sodass jede importierte Zelle konsistent aussieht.

Am Ende haben Sie eine einsatzbereite `DataTableWithStyleArray.xlsx`‑Datei, die Zahlen als Dollar anzeigt und sie fett hervorhebt. Keine manuelle Formatierung in Excel ist nötig.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Java 17 oder höher installiert.
- Eine Aspose.Cells for Java‑Lizenz (oder einen kostenlosen Evaluierungsschlüssel).
- Maven oder Gradle zur Verwaltung der `aspose-cells`‑Abhängigkeit.
- Grundlegende Kenntnisse von Java‑Collections und `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro‑Tipp:** Wenn Sie auf eine `LicenseException` stoßen, legen Sie Ihre Lizenzdatei in den Klassenpfad und rufen Sie `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` auf, bevor Sie die Arbeitsmappe erstellen.

## Wie man eine Excel-Arbeitsmappe mit formatierten Währungszellen erstellt

Dieser Abschnitt enthält die Kernschritte. Jeder Schritt erklärt **warum** er wichtig ist, nicht nur **was** Sie tippen sollen.

### Schritt 1: Initialisieren der Arbeitsmappe und des Arbeitsblatts

Das Erstellen einer frischen Arbeitsmappe gibt Ihnen einen sauberen Container für alle nachfolgenden Formatierungen.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Warum:** Das `Workbook`‑Objekt repräsentiert die gesamte Excel‑Datei. Der Zugriff auf das erste `Worksheet` ermöglicht es Ihnen, sofort Daten zu befüllen.

### Schritt 2: Erstellen einer DataTable mit numerischen Daten

Eine `DataTable` ahmt eine Datenbanktabelle nach und erleichtert das massenhafte Importieren von Zeilen.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Warum:** Die Verwendung von `DOUBLE` stellt sicher, dass die Werte ihre Dezimalpräzision behalten, was entscheidend ist, wenn Sie später **format cells currency** anwenden.

### Schritt 3: Definieren eines Stils – Währungsformat und fette Schrift

Hier **setzen wir das Währungsformat** und **fügen fette Schrift** zu einem `Style`‑Objekt hinzu.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Warum:** Der `Number`‑Format‑String `$#,##0.00` weist Excel an, die Zelle als Geldwert zu behandeln, während `setBold(true)` die Zahlen hervorhebt. Das Ablegen des Stils in einem Array bereitet uns auf den **how to import style**‑Schritt vor.

### Schritt 4: Konfigurieren der Importoptionen zur Verwendung des Stil‑Arrays

Aspose.Cells lässt Sie ein `Style[]` über `ImportTableOptions` übergeben. Das ist die offizielle **how to import style**‑Methode.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Warum:** Ohne `ImportTableOptions` würden importierte Zellen den Standardstil erben und das von uns definierte Währungsformat sowie die Fettschrift verlieren.

### Schritt 5: Importieren der DataTable in das Arbeitsblatt

Jetzt bringen wir die Daten in das Blatt bei Zelle `A1`, wobei das Stil‑Array automatisch angewendet wird.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` bedeutet, dass die erste Zeile der `DataTable` Spaltenüberschriften enthält.
- `"A1"` ist die obere linke Ecke, an der der Import beginnt.

> **Warum:** Der Import mit dem Stil‑Array garantiert, dass jede importierte Zelle den zuvor vorbereiteten **format cells currency**‑Stil erhält.

### Schritt 6: Speichern der Arbeitsmappe auf dem Datenträger

Abschließend schreiben wir die im Speicher befindliche Arbeitsmappe in eine physische Datei.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Warum:** Das Speichern bewahrt die Formatierung, sodass Sie oder nachgelagerte Prozesse die Datei in Excel mit dem gewünschten Aussehen öffnen können.

## Vollständiger Quellcode

Unten finden Sie die komplette, sofort ausführbare Java‑Klasse. Kopieren Sie sie in Ihre IDE, ersetzen Sie `YOUR_DIRECTORY` durch einen existierenden Ordner und führen Sie sie aus.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Erwartete Ausgabe

Wenn Sie `DataTableWithStyleArray.xlsx` in Microsoft Excel öffnen, sollten Sie folgendes sehen:

| Amount |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Die Zahlen werden mit einem **currency format** (`$`‑Zeichen, zwei Dezimalstellen) angezeigt.
- Die Schrift für beide Zellen ist **bold**, sodass sie hervorgehoben werden.

## Häufige Variationen und Sonderfälle

| Szenario | Was zu ändern ist | Grund |
|----------|-------------------|-------|
| **Andere Währung** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Verwenden Sie das Euro‑Symbol oder ein länderspezifisches Format. |
| **Mehrere Spalten mit unterschiedlichen Stilen** | Erstellen Sie mehrere `Style`‑Objekte, füllen Sie `styleArray` in derselben Reihenfolge wie die Spalten. | Jede Spalte kann ihr eigenes Zahlenformat, Schrift, Hintergrund usw. haben. |
| **Große Datensätze** | Verwenden Sie `cells.importDataTable(dataTable, false, "A1", importOptions);` und setzen Sie `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Verbessert die Leistung, indem Header‑Zeilen oder unnötige Metadaten übersprungen werden. |
| **Stil nach dem Import anwenden** | Rufen Sie `cells.get("A2").setStyle(currencyStyle);` für einzelne Zellen auf. | Nützlich, wenn nur ein Teil der Zeilen eine spezielle Formatierung benötigt. |

## Tipps für den Produktionseinsatz

- **Lizenz frühzeitig**: Registrieren Sie Ihre Aspose.Cells‑Lizenz, bevor Sie die Arbeitsmappe erstellen, um das Evaluations‑Wasserzeichen zu vermeiden.
- **Thread‑Sicherheit**: `Workbook`‑Instanzen sind **nicht** thread‑sicher. Erzeugen Sie pro Thread eine separate Instanz, wenn Sie viele Dateien gleichzeitig generieren.
- **Speichermanagement**: Bei sehr großen Blättern sollten Sie die Streaming‑API von `Workbook` (`Workbook` → `WorkbookDesigner`) nutzen, um den Speicherverbrauch gering zu halten.
- **Testing**: Schreiben Sie einen Unit‑Test, der die gespeicherte Datei mit Apache POI öffnet und prüft, ob das Zellen‑Stil‑Zahlenformat `"$#,##0.00"` entspricht.

## Fazit

Sie wissen jetzt, wie man **eine Excel-Arbeitsmappe** in Java **erstellt**, **ein Währungsformat setzt**, **fette Schrift hinzufügt** und korrekt **how to import style** mit Aspose.Cells’ `ImportTableOptions` verwendet. Diese End‑to‑End‑Lösung eliminiert manuelle Excel‑Schritte und stellt sicher, dass jede importierte Zelle dieselbe **format cells currency**‑Gestaltung hat.

Bereit für die nächste Herausforderung? Versuchen Sie, bedingte Formatierung hinzuzufügen, Diagramme einzubetten oder die Arbeitsmappe nach PDF zu exportieren – alles unter Wiederverwendung der gleichen Stil‑Array‑Technik. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}