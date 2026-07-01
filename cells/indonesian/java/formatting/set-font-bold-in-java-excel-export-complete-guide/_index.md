---
category: general
date: 2026-06-30
description: Atur teks menjadi tebal saat mengimpor DataTable ke Excel menggunakan
  Java. Pelajari kode pemformatan bersyarat, impor DataTable ke Excel, dan gaya tabel
  dengan mudah.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: id
og_description: Atur teks menjadi tebal di Java saat mengekspor DataTable ke Excel.
  Panduan ini mencakup kode pemformatan bersyarat, impor DataTable ke Excel, dan penataan
  tabel.
og_title: Mengatur Font Tebal pada Ekspor Excel Java – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Atur Font Tebal pada Ekspor Excel Java – Panduan Lengkap
url: /id/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Font Tebal dalam Ekspor Excel Java – Panduan Lengkap

Pernah bertanya-tanya **cara mengatur font tebal** untuk kolom tertentu saat Anda **mengimpor datatable excel**? Anda bukan satu-satunya. Banyak pengembang mengalami kebuntuan ketika mereka membutuhkan spreadsheet yang bergaya rapi tanpa harus mengatur setiap sel secara manual. Kabar baik? Dengan beberapa baris kode Java Anda dapat mengimpor `DataTable`, menerapkan font tebal, dan bahkan menambahkan beberapa **kode pemformatan bersyarat**—semuanya secara programatik.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan **cara mengimpor datatable** ke dalam workbook Excel, menerapkan **set font bold** pada setiap kolom indeks genap, dan secara opsional menambahkan format bersyarat sederhana. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan dan pemahaman yang jelas tentang **import table with styles** untuk proyek apa pun.

## Prasyarat

- Java 8 atau lebih baru (kode ini juga bekerja pada Java 17)  
- Aspose.Cells untuk Java (versi percobaan gratis sudah cukup) – tambahkan dependensi Maven atau JAR ke classpath Anda.  
- Familiaritas dasar dengan konversi `java.sql` `ResultSet` → `DataTable` (kami akan membuat tabel tiruan untuk kesederhanaan).  
- Sebuah IDE atau alat build seperti Maven/Gradle.

> **Pro tip:** Jika Anda menggunakan Maven, tambahkan ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Ikhtisar Solusi

1. **Buat `DataTable` tiruan** yang meniru data yang biasanya Anda ambil dari basis data.  
2. **Hasilkan array `CellStyle`** di mana setiap kolom genap mendapatkan font tebal – itu inti dari **set font bold**.  
3. **Ambil worksheet pertama** dari workbook.  
4. **Impor `DataTable`** dengan header kolom, mulai dari sel `A1`, dan terapkan gaya yang telah disiapkan.  
5. (Opsional) **Tambahkan aturan pemformatan bersyarat** untuk mengilustrasikan kata kunci **conditional formatting code**.

Setiap langkah dijelaskan dalam bahasa Inggris yang sederhana, dan blok kode sepenuhnya mandiri sehingga Anda dapat menyalin‑tempel dan menjalankannya secara langsung.

---

## Langkah 1: Dapatkan atau Bangun DataTable untuk Diimpor

Dalam aplikasi dunia nyata, Anda mungkin akan memanggil utilitas konversi `ResultSet` → `DataTable`. Untuk panduan ini kami akan membuat `DataTable` sederhana secara manual sehingga Anda dapat fokus pada bagian Excel.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Mengapa ini penting:** Memiliki `DataTable` yang siap memungkinkan kami fokus pada API **import datatable excel** dan logika gaya. Metode di atas dapat digunakan kembali—cukup ganti baris yang dikodekan secara keras dengan kueri basis data saat Anda masuk ke produksi.

## Langkah 2: Siapkan Gaya – Di Sinilah Kami **Set Font Bold**

Sekarang kami akan membangun array objek `CellStyle`, satu per kolom. Aturannya sederhana: **set font bold** untuk setiap kolom indeks genap (0, 2, 4,…). Kolom ganjil tetap normal.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Mengapa Menggunakan Array Gaya?

- **Performance:** Menerapkan gaya per kolom lebih cepat daripada menata setiap sel secara individual.  
- **Consistency:** Setiap sel dalam kolom mewarisi pemformatan yang sama, menjamin tampilan yang seragam.  
- **Scalability:** Menambahkan lebih banyak kolom di kemudian hari hanya memerlukan perpanjangan array—tanpa menulis ulang kode.

## Langkah 3: Akses Worksheet Pertama dalam Workbook

Aspose.Cells membuat worksheet default untuk kami, tetapi praktik yang baik adalah mengambilnya secara eksplisit. Ini juga menunjukkan **cara mengimpor datatable** ke dalam lembar tertentu.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

## Langkah 4: Impor DataTable dengan Gaya – Operasi Inti **Import Table With Styles**

Metode `importDataTable` melakukan pekerjaan berat. Ia menyalin data, menambahkan header kolom, dan menerapkan array gaya yang kami buat sebelumnya.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Saat Anda menjalankan contoh, Anda akan melihat **set font bold** diterapkan pada kolom `ID` dan `Score`, sementara `Name` tetap normal.

## Langkah 5 (Opsional): Tambahkan Pemformatan Bersyarat – Contoh Cepat **Conditional Formatting Code**

Jika Anda ingin menyorot baris di mana skor melebihi 90, beberapa baris tambahan akan menyelesaikannya. Ini menampilkan kata kunci **conditional formatting code** tanpa mengganggu alur utama.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Catatan:** Potongan kode di atas bersifat opsional tetapi menunjukkan bagaimana Anda dapat menumpuk **conditional formatting code** di atas tabel yang sudah bergaya.

## Menggabungkan Semua – Contoh Lengkap yang Dapat Dijalankan

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Otomatisasi Pemformatan Bersyarat Excel Menggunakan Aspose.Cells untuk Java: Panduan Lengkap](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Cara Menerapkan Pengaturan Font Kustom di Aspose.Cells Java untuk Pemformatan Excel](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Mengatur Ukuran Font di Excel Menggunakan Aspose.Cells Java - Panduan Komprehensif](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}