---
category: general
date: 2026-09-27
description: Utwórz skoroszyt Excel w Javie, zaimportuj dane SQL, ustaw format liczbowy
  kolumny i zapisz skoroszyt jako XLSX przy użyciu Aspose.Cells w Javie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: pl
lastmod: 2026-09-27
og_description: Utwórz skoroszyt Excel w Javie, zaimportuj dane SQL, ustaw format
  liczbowy kolumny i zapisz skoroszyt jako XLSX z w pełni działającym przykładem w
  Javie.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Tworzenie skoroszytu Excel w Javie – import danych SQL i ustawianie formatów
  liczb w kolumnach
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
title: Utwórz skoroszyt Excel w Javie i zastosuj formaty liczb w kolumnach
url: /pl/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel w Javie i zastosuj formaty liczb w kolumnach

If you need to **create Excel workbook java** and style numeric columns, this guide shows you exactly how. You’ll learn to import SQL data into Excel, set a number format for each column, and **save workbook as XLSX** using the Aspose.Cells library.

Working with spreadsheets from Java often feels fragmented—developers copy‑paste snippets, forget to format numbers, or end up with CSV files instead of true Excel files. This tutorial removes that friction by providing a single, end‑to‑end solution that you can drop into any Java project.

By the end of the article you will be able to:

* Connect to a database and retrieve a `DataTable` (or `ResultSet`)  
* Create a new workbook with Aspose.Cells  
* Apply a consistent **add number format excel** style to every column  
* **Save workbook as XLSX** to a location of your choice  

The only prerequisite is a Java development environment (JDK 8+ recommended) and the Aspose.Cells for Java JAR on your classpath.

---

## Wymagania wstępne

| Wymaganie | Dlaczego ma znaczenie |
|-------------|----------------|
| JDK 8 lub nowszy | Dostarcza funkcje językowe użyte w przykładzie. |
| Aspose.Cells for Java (najnowsza wersja) | Obsługuje tworzenie, stylizowanie i zapisywanie Excela bez zainstalowanego Office. |
| Baza danych zgodna z JDBC (np. MySQL, PostgreSQL) | Dostarcza dane SQL, które zaimportujemy. |
| Maven lub Gradle (opcjonalnie) | Uproszcza zarządzanie zależnościami. |

Add Aspose.Cells to your Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Or download the JAR directly from the Aspose website and add it to your project’s classpath.

---

## Krok 1: Utwórz skoroszyt Excel w Javie

The first logical block is to instantiate a new `Workbook`. This object represents the entire Excel file in memory and gives you access to worksheets, cells, and styles.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Creating the workbook up front also gives us a `Style` factory that we’ll need later when we **set number format column**.

## Krok 2: Pobierz dane z SQL (import sql data excel)

Below we open a JDBC connection, execute a simple `SELECT` statement, and load the result set into an Aspose `DataTable`. The `DataTable` class mimics the .NET `DataTable` and works seamlessly with the `importDataTable` method.

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

> **Wskazówka:** If you already have a `DataTable` from another source (e.g., CSV parsing), you can skip the JDBC code and return that table directly.

---

## Krok 3: Przygotuj wielokrotnego użytku styl (add number format excel)

We want every numeric column to display numbers with two decimal places and a thousands separator. Instead of styling each cell individually, we create a `Style` object once per column and reuse it during import. This is the most efficient way to **add number format excel**.

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

You can adapt the format string (`"#,##0.00"`) to any Excel number format you need. For dates, use `styles[i].setCustom("mm-dd-yyyy")`, etc.

---

## Krok 4: Importuj DataTable i zastosuj style kolumn

Now we bring everything together. The `importDataTable` overload lets us pass the `DataTable`, specify whether the first row should be treated as column headers, and supply the style array. This automatically **set number format column** for each cell in the corresponding column.

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

Because we passed `true` for the `importColumnNames` flag, the first row of the worksheet contains the column names from the `DataTable`. Each subsequent row receives the data, already formatted according to the style we defined.

---

## Krok 5: Zapisz skoroszyt jako xlsx

The final step is to persist the in‑memory workbook to a physical file. Aspose.Cells supports many formats; we’ll use the modern XLSX format, which is what most applications expect today.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

You can change `filePath` to any valid location on your system. The method throws `IOException` if the directory does not exist or you lack write permission.

---

## Pełny, gotowy do uruchomienia przykład

Putting all the pieces together yields a self‑contained program you can compile and run immediately.

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

### Oczekiwany wynik

Running the program creates a file named **DataTableWithNumberFormat.xlsx** in the working directory. Open it with Microsoft Excel, LibreOffice Calc, or any XLSX‑compatible viewer and you will see:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*Kolumna **Amount** wyświetla liczby z dwoma miejscami po przecinku i separatorem tysięcy, dzięki zastosowanemu stylowi **add number format excel**.*

---

## Często zadawane pytania i obsługa przypadków brzegowych

| Pytanie | Odpowiedź |
|----------|--------|
| **Co jeśli moje zapytanie nie zwróci żadnych wierszy?** | The `DataTable` will be empty but still contain column definitions. The workbook will contain only the header row, which is often sufficient for downstream processes. |
| **Jak zastosować różne formaty dla poszczególnych kolumn?** | Modify `buildColumnStyles` to inspect the column name or data type and assign a custom format (e.g., dates, percentages). |
| **Czy mogę zapisać bezpośrednio do `ByteArrayOutputStream`?** | Yes. Replace `workbook.save(filePath, SaveFormat.XLSX);` with

## Co powinieneś nauczyć się dalej?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}