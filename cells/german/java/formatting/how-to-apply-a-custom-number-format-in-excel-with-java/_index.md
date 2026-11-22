---
category: general
date: 2026-11-22
description: Erfahren Sie, wie Sie ein benutzerdefiniertes Zahlenformat verwenden,
  um eine Spalte in Excel mit Java als Währung zu formatieren. Setzen Sie das Excel‑Zahlenformat
  schnell mit einem einfachen Stil.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: de
lastmod: 2026-11-22
og_description: Wenden Sie ein benutzerdefiniertes Zahlenformat in Excel mit Java
  an. Dieses Tutorial zeigt, wie man das Excel‑Zahlenformat festlegt und die erste
  Spalte als Währung formatiert.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Benutzerdefiniertes Zahlenformat in Excel mit Java anwenden – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Wie man in Excel mit Java ein benutzerdefiniertes Zahlenformat anwendet
url: /de/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein benutzerdefiniertes Zahlenformat in Excel mit Java anwendet

Wenn Sie eine Spalte in einem Excel‑Arbeitsblatt **benutzerdefiniert formatieren** müssen, zeigt Ihnen diese Anleitung genau, wie Sie dies mit Java erledigen. Egal, ob Sie Finanzberichte erstellen oder Buchhaltungsdaten exportieren, die Formatierung der ersten Spalte als Währung macht die Ausgabe sofort lesbar.

Im folgenden Beispiel werden wir die **Spalte als Währung formatieren**, den Stil auf die erste Spalte anwenden und anschließend eine `DataTable` in das Arbeitsblatt importieren. Der gleiche Ansatz funktioniert für jedes numerische Format, das Sie anzeigen möchten.

## Was Sie lernen werden

* Wie man ein **benutzerdefiniertes Zahlenformat** mit dem `Style`‑Objekt von Apache POI erstellt.  
* Wie man **Excel-Zahlenformat** für eine bestimmte Spalte festlegt, einschließlich des Falls **set currency format**.  
* Wie man **erste Spalte stylt**, während man eine `DataTable` importiert.  
* Wie man die Arbeitsmappe speichert und überprüft, dass die Formatierung korrekt angezeigt wird.

### Voraussetzungen

* Java 17 oder neuer.  
* Apache POI 5.x (die Bibliothek, die `Workbook`, `Worksheet` und `Style` bereitstellt).  
* Eine `DataTable`‑Implementierung, die wie im Code‑Beispiel iterierbar ist.  
* Grundlegende Kenntnisse in Java und Excel.

---

## Schritt 1: Projekt einrichten und Daten importieren

Fügen Sie zunächst Apache POI zu Ihrem Projekt hinzu. Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit ein:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Als Nächstes erhalten Sie die Quelldaten als `DataTable`. In einem realen Szenario kann dies aus einer Datenbankabfrage, einer CSV‑Datei oder einer API‑Antwort stammen.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro‑Tipp:** Stellen Sie sicher, dass die `DataTable`‑Spalten die richtigen Java‑Typen (`Integer`, `Double` usw.) haben, da das Zahlenformat nur numerische Zellen beeinflusst.

---

## Schritt 2: Erstellen Sie ein **benutzerdefiniertes Zahlenformat** für die erste Spalte

Ein **benutzerdefiniertes Zahlenformat** gibt Excel an, wie numerische Werte angezeigt werden sollen. Um Werte als Währung darzustellen, verwenden wir das integrierte `CURRENCY`‑Format, Sie können jedoch auch Muster wie `"$#,##0.00"` definieren.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Warum das funktioniert:**  
* `createCellStyle()` gibt ein wiederverwendbares Stilobjekt zurück.  
* `setDataFormat()` fügt dem Stil das **set currency format** hinzu, das Excel dann auf jede Zelle anwendet, die diesen Stil verwendet.  
* Durch das Speichern des Stils in `columnStyles[0]` stellen wir sicher, dass nur die erste Spalte die Währungsformatierung erhält.

---

## Schritt 3: Importieren Sie die `DataTable` und wenden dabei die Spaltenstile an

Jetzt importieren wir die Daten in das Arbeitsblatt. Die Methode `importDataTable` akzeptiert das Stil‑Array, sodass wir die **erste Spalte stylen** können und die übrigen Spalten die Standardformatierung behalten.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Der obige Aufruf **setzt das Excel-Zahlenformat** nur für die erste Spalte. Alle anderen Spalten erben den Standardstil der Arbeitsmappe, was den Code einfach und effizient hält.

---

## Schritt 4: Arbeitsmappe speichern und Ergebnis überprüfen

Schließlich schreiben Sie die Arbeitsmappe in eine Datei und öffnen sie in Excel, um zu bestätigen, dass die erste Spalte Währungssymbole anzeigt.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Erwartete Ausgabe:**  
Wenn Sie *FormattedReport.xlsx* öffnen, erscheinen die Werte in Spalte A mit dem entsprechenden Währungssymbol (z. B. `$1,234.00`). Alle anderen Spalten behalten ihre ursprüngliche numerische Darstellung bei.

---

## Gemeinsame Variationen und Sonderfälle

| Situation | Anpassung |
|-----------|------------|
| **Andere Währung** (z. B. Euro) | Ersetzen Sie `Style.CustomNumberFormat.CURRENCY` durch ein benutzerdefiniertes Muster: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Mehr als eine formatierte Spalte** | Füllen Sie zusätzliche Einträge in `columnStyles[]` mit eigenen `CellStyle`‑Objekten. |
| **Große Datensätze** | Verwenden Sie `importDataTable` in Batches oder streamen Sie Zeilen, um `OutOfMemoryError` zu vermeiden. |
| **Lokalspezifische Trennzeichen** | Verwenden Sie `java.text.NumberFormat`, um ein lokalsensitives Muster zu erzeugen und an `setDataFormat` zu übergeben. |

> **Achtung:** Das Wiederverwenden eines einzelnen `CellStyle`‑Objekts über viele Spalten hinweg kann zu unerwarteten Formatierungen führen, da Excel die Anzahl verschiedener Stile pro Arbeitsmappe begrenzt. Erstellen Sie für jedes benötigte eindeutige Format einen separaten Stil.

---

## Vollständiges ausführbares Beispiel

Unten finden Sie ein eigenständiges Programm, das den gesamten Arbeitsablauf von der Datenerstellung bis zum Speichern der formatierten Arbeitsmappe demonstriert.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Das Ausführen des Programms erzeugt **FormattedReport.xlsx**, wobei Spalte A (die „Amount“-Spalte) mit einem **benutzerdefinierten Zahlenformat** angezeigt wird, das ein Dollarzeichen und zwei Dezimalstellen zeigt.

---

## Fazit

Sie wissen jetzt, wie Sie ein Excel‑Arbeitsblatt aus Java **benutzerdefiniert formatieren**, **Spalte als Währung formatieren** und **erste Spalte stylen**, während Sie Daten importieren. Durch das Erstellen eines wiederverwendbaren `CellStyle` und dessen Übergabe an `importDataTable` können Sie **Excel-Zahlenformat** für jede Spalte festlegen, ohne jede Zelle manuell durchlaufen zu müssen.

Als Nächstes versuchen Sie:

* Verwenden Sie `setDataFormat` mit lokalspezifischen Mustern, um **Währungsformat festzulegen**.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Set Number Format Excel in Java – Complete Guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Apply Number Format Excel in Java – Complete Aspose.Cells Guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [How to create excel workbook with currency format and bold font in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}