---
category: general
date: 2026-09-27
description: Buat workbook Excel dengan Java, impor data SQL, atur format angka pada
  kolom, dan simpan workbook sebagai XLSX menggunakan Aspose.Cells di Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: id
lastmod: 2026-09-27
og_description: Buat workbook Excel dengan Java, impor data SQL, atur format angka
  pada kolom, dan simpan workbook sebagai XLSX dengan contoh Java yang berfungsi penuh.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Buat workbook Excel dengan Java – impor data SQL dan atur format angka kolom
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
title: Buat workbook Excel dengan Java dan terapkan format angka pada kolom
url: /id/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook Excel java dan terapkan format nomor kolom

Jika Anda perlu **create Excel workbook java** dan menata kolom numerik, panduan ini menunjukkan cara tepatnya. Anda akan belajar mengimpor data SQL ke Excel, mengatur format nomor untuk setiap kolom, dan **save workbook as XLSX** menggunakan library Aspose.Cells.

Bekerja dengan spreadsheet dari Java sering terasa terfragmentasi—pengembang menyalin‑tempel potongan kode, lupa memformat angka, atau berakhir dengan file CSV alih‑alih file Excel yang sebenarnya. Tutorial ini menghilangkan gesekan tersebut dengan menyediakan solusi tunggal, end‑to‑end yang dapat Anda masukkan ke dalam proyek Java mana pun.

Dengan menyelesaikan artikel ini Anda akan dapat:

* Terhubung ke basis data dan mengambil `DataTable` (atau `ResultSet`)  
* Membuat workbook baru dengan Aspose.Cells  
* Menerapkan gaya **add number format excel** yang konsisten ke setiap kolom  
* **Save workbook as XLSX** ke lokasi pilihan Anda  

Satu‑satunya prasyarat adalah lingkungan pengembangan Java (JDK 8+ disarankan) dan JAR Aspose.Cells untuk Java di classpath Anda.

---

## Prerequisites

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| JDK 8 atau lebih baru | Menyediakan fitur bahasa yang digunakan dalam contoh. |
| Aspose.Cells untuk Java (versi terbaru) | Menangani pembuatan, penataan, dan penyimpanan Excel tanpa perlu Office terinstal. |
| Database yang kompatibel dengan JDBC (mis., MySQL, PostgreSQL) | Menyediakan data SQL yang akan kami impor. |
| Maven atau Gradle (opsional) | Menyederhanakan manajemen dependensi. |

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

## Step 1: Create Excel workbook java

The first logical block is to instantiate a new `Workbook`. This object represents the entire Excel file in memory and gives you access to worksheets, cells, and styles.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Creating the workbook up front also gives us a `Style` factory that we’ll need later when we **set number format column**.

---

## Step 2: Retrieve data from SQL (import sql data excel)

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

> **Tip:** Jika Anda sudah memiliki `DataTable` dari sumber lain (mis., parsing CSV), Anda dapat melewatkan kode JDBC dan mengembalikan tabel tersebut secara langsung.

---

## Step 3: Prepare a reusable style (add number format excel)

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

## Step 4: Import the DataTable and apply the column styles

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

## Step 5: Save workbook as xlsx

The final step is to persist the in‑memory workbook to a physical file. Aspose.Cells supports many formats; we’ll use the modern XLSX format, which is what most applications expect today.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

You can change `filePath` to any valid location on your system. The method throws `IOException` if the directory does not exist or you lack write permission.

---

## Full, runnable example

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

### Expected result

Running the program creates a file named **DataTableWithNumberFormat.xlsx** in the working directory. Open it with Microsoft Excel, LibreOffice Calc, or any XLSX‑compatible viewer and you will see:

| Id | Jumlah | TanggalDibuat |
|----|--------|---------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*Kolom **Jumlah** menampilkan angka dengan dua tempat desimal dan pemisah ribuan, berkat gaya **add number format excel** yang kami terapkan.*

---

## Common questions and edge‑case handling

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika kueri saya tidak mengembalikan baris?** | `DataTable` akan kosong tetapi tetap berisi definisi kolom. Workbook akan berisi hanya baris header, yang sering cukup untuk proses selanjutnya. |
| **Bagaimana saya menerapkan format berbeda per kolom?** | Modifikasi `buildColumnStyles` untuk memeriksa nama kolom atau tipe data dan menetapkan format khusus (mis., tanggal, persentase). |
| **Bisakah saya menulis langsung ke `ByteArrayOutputStream`?** | Ya. Ganti `workbook.save(filePath, SaveFormat.XLSX);` dengan

## What Should You Learn Next?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat dan Menyimpan Workbook Excel sebagai SVG menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Buat Simpan Workbook Excel Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Buat Simpan Workbook Excel Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}