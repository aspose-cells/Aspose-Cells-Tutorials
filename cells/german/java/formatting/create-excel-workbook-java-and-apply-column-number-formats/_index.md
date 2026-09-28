---
category: general
date: 2026-09-27
description: Erstelle ein Excel-Arbeitsbuch in Java, importiere SQL-Daten, setze das
  Zahlenformat einer Spalte und speichere das Arbeitsbuch als XLSX mit Aspose.Cells
  in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: de
lastmod: 2026-09-27
og_description: Excel-Arbeitsmappe in Java erstellen, SQL‑Daten importieren, das Zahlenformat
  einer Spalte festlegen und die Arbeitsmappe als XLSX speichern – mit einem vollständig
  funktionierenden Java‑Beispiel.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Excel-Arbeitsmappe in Java erstellen – SQL-Daten importieren und Spaltenzahlenformate
  festlegen
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Excel-Arbeitsmappe in Java erstellen und Spaltenzahlformate anwenden
url: /de/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel‑Arbeitsmappe in Java erstellen und Spaltenzahlformate anwenden

Wenn Sie **create Excel workbook java** und numerische Spalten formatieren müssen, zeigt Ihnen dieser Leitfaden genau, wie es geht. Sie lernen, SQL‑Daten in Excel zu importieren, für jede Spalte ein Zahlenformat festzulegen und **save workbook as XLSX** mit der Aspose.Cells‑Bibliothek.

Die Arbeit mit Tabellenkalkulationen aus Java heraus fühlt sich oft fragmentiert an – Entwickler kopieren und fügen Code‑Snippets ein, vergessen Zahlen zu formatieren oder enden mit CSV‑Dateien anstelle echter Excel‑Dateien. Dieses Tutorial beseitigt diese Reibung, indem es eine einzige, durchgängige Lösung bereitstellt, die Sie in jedes Java‑Projekt einbinden können.

Am Ende des Artikels können Sie:

* Eine Verbindung zu einer Datenbank herstellen und ein `DataTable` (oder `ResultSet`) abrufen  
* Eine neue Arbeitsmappe mit Aspose.Cells erstellen  
* Einen konsistenten **add number format excel**‑Stil auf jede Spalte anwenden  
* **Save workbook as XLSX** an einem Ort Ihrer Wahl speichern  

Die einzige Voraussetzung ist eine Java‑Entwicklungsumgebung (empfohlen JDK 8+) und das Aspose.Cells for Java‑JAR in Ihrem Klassenpfad.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| JDK 8 or newer | Stellt die im Beispiel verwendeten Sprachfeatures bereit. |
| Aspose.Cells for Java (latest version) | Ermöglicht das Erstellen, Stylen und Speichern von Excel ohne installierte Office‑Software. |
| A JDBC‑compatible database (e.g., MySQL, PostgreSQL) | Stellt die SQL‑Daten bereit, die wir importieren werden. |
| Maven or Gradle (optional) | Vereinfacht die Verwaltung von Abhängigkeiten. |

Fügen Sie Aspose.Cells zu Ihrem Maven `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Oder laden Sie das JAR direkt von der Aspose-Website herunter und fügen es dem Klassenpfad Ihres Projekts hinzu.

## Schritt 1: Excel‑Arbeitsmappe in Java erstellen

Der erste logische Block besteht darin, ein neues `Workbook` zu instanziieren. Dieses Objekt repräsentiert die gesamte Excel‑Datei im Speicher und gibt Ihnen Zugriff auf Arbeitsblätter, Zellen und Stile.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Das vorzeitige Erstellen der Arbeitsmappe liefert uns außerdem eine `Style`‑Factory, die wir später benötigen, wenn wir **set number format column** festlegen.

## Schritt 2: Daten aus SQL abrufen (import sql data excel)

Im Folgenden öffnen wir eine JDBC‑Verbindung, führen ein einfaches `SELECT`‑Statement aus und laden das Result‑Set in ein Aspose `DataTable`. Die Klasse `DataTable` ahmt das .NET‑`DataTable` nach und funktioniert nahtlos mit der Methode `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Tipp:** Wenn Sie bereits ein `DataTable` aus einer anderen Quelle haben (z. B. CSV‑Parsing), können Sie den JDBC‑Code überspringen und diese Tabelle direkt zurückgeben.

## Schritt 3: Wiederverwendbaren Stil vorbereiten (add number format excel)

Wir möchten, dass jede numerische Spalte Zahlen mit zwei Dezimalstellen und einem Tausendertrennzeichen anzeigt. Anstatt jede Zelle einzeln zu formatieren, erstellen wir ein `Style`‑Objekt einmal pro Spalte und verwenden es beim Import erneut. Dies ist der effizienteste Weg, um **add number format excel** anzuwenden.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

Sie können die Formatzeichenfolge (`"#,##0.00"`) an jedes gewünschte Excel‑Zahlenformat anpassen. Für Datumsangaben verwenden Sie `styles[i].setCustom("mm-dd-yyyy")` usw.

## Schritt 4: DataTable importieren und Spaltenstile anwenden

Jetzt fügen wir alles zusammen. Die überladene Methode `importDataTable` ermöglicht es, das `DataTable` zu übergeben, anzugeben, ob die erste Zeile als Spaltenüberschriften behandelt werden soll, und das Stil‑Array bereitzustellen. Dadurch wird automatisch **set number format column** für jede Zelle in der jeweiligen Spalte gesetzt.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Da wir `true` für das Flag `importColumnNames` übergeben haben, enthält die erste Zeile des Arbeitsblatts die Spaltennamen aus dem `DataTable`. Jede nachfolgende Zeile erhält die Daten, bereits formatiert gemäß dem von uns definierten Stil.

## Schritt 5: Arbeitsmappe als XLSX speichern

Der letzte Schritt besteht darin, die im Speicher befindliche Arbeitsmappe in eine physische Datei zu schreiben. Aspose.Cells unterstützt viele Formate; wir verwenden das moderne XLSX‑Format, das heute von den meisten Anwendungen erwartet wird.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Sie können `filePath` zu einem beliebigen gültigen Speicherort auf Ihrem System ändern. Die Methode wirft eine `IOException`, wenn das Verzeichnis nicht existiert oder Sie keine Schreibberechtigung haben.

## Vollständiges, ausführbares Beispiel

Wenn man alle Teile zusammenfügt, entsteht ein eigenständiges Programm, das Sie sofort kompilieren und ausführen können.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Erwartetes Ergebnis

Das Ausführen des Programms erzeugt eine Datei namens **DataTableWithNumberFormat.xlsx** im Arbeitsverzeichnis. Öffnen Sie sie mit Microsoft Excel, LibreOffice Calc oder einem beliebigen XLSX‑kompatiblen Viewer und Sie sehen:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*Die **Amount**‑Spalte zeigt Zahlen mit zwei Dezimalstellen und einem Tausendertrennzeichen an, dank des **add number format excel**‑Stils, den wir angewendet haben.*

## Häufige Fragen und Sonderfall‑Behandlung

| Frage | Antwort |
|----------|--------|
| **Was passiert, wenn meine Abfrage keine Zeilen zurückgibt?** | Das `DataTable` wird leer sein, enthält aber weiterhin die Spaltendefinitionen. Die Arbeitsmappe enthält nur die Kopfzeile, was für nachgelagerte Prozesse oft ausreichend ist. |
| **Wie wende ich unterschiedliche Formate pro Spalte an?** | Passen Sie `buildColumnStyles` an, um den Spaltennamen oder den Datentyp zu prüfen und ein benutzerdefiniertes Format zuzuweisen (z. B. Datumsangaben, Prozentsätze). |
| **Kann ich direkt in einen `ByteArrayOutputStream` schreiben?** | Ja. Ersetzen Sie `workbook.save(filePath, SaveFormat.XLSX);` durch |

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man eine Excel‑Arbeitsmappe als SVG erstellt und speichert mit Aspose.Cells für Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel‑Arbeitsmappe erstellen und speichern Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel‑Arbeitsmappe erstellen und speichern Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}