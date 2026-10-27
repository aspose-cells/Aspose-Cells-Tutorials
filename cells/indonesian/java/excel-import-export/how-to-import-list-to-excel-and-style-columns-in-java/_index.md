---
category: general
date: 2026-08-17
description: Impor daftar ke Excel dalam Java menggunakan Aspose.Cells, pelajari cara
  menata kolom, mengekspor data ke xlsx, dan membuat workbook Excel secara programatik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import list to excel
- how to style column
- export data to xlsx
- import data with header
- create excel workbook java
language: id
lastmod: 2026-08-17
og_description: Impor daftar ke Excel dalam Java dengan Aspose.Cells, beri gaya pada
  header kolom, ekspor data ke xlsx, dan buat workbook Excel secara efisien.
og_image_alt: Screenshot of a Java‑generated Excel file showing bold column headers
og_title: Impor daftar ke Excel dalam Java – panduan lengkap dengan penataan kolom
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  headline: How to import list to Excel and style columns in Java
  type: TechArticle
- description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  name: How to import list to Excel and style columns in Java
  steps:
  - name: Why this works
    text: '* **`importDataTable`** reads the keys of each map (`"Name"` and `"Score"`)
      as column headers when the `true` flag is set. This satisfies the **import data
      with header** requirement. * The **style array** aligns with the column order.
      By setting `columnStyles[1].getFont().setBold(true)`, we answer t'
  - name: Null values and type safety
    text: 'If a map contains `null` or mixed‑type values, Aspose.Cells automatically
      writes an empty cell. To guarantee consistent typing, you can pre‑process the
      list:'
  - name: Mismatched column counts
    text: '`importDataTable` expects the style array length to match the number of
      columns. If you add a new column later, remember to expand `columnStyles` accordingly,
      otherwise Aspose.Cells throws `IndexOutOfBoundsException`.'
  - name: Large data sets
    text: For more than 10 000 rows, consider using the **`importArray`** overload,
      which streams data directly to the worksheet and reduces memory consumption.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Data export
title: Cara mengimpor daftar ke Excel dan menata kolom di Java
url: /id/java/excel-import-export/how-to-import-list-to-excel-and-style-columns-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengimpor list ke Excel dan menata kolom di Java

Jika Anda perlu **mengimpor list ke Excel** dari aplikasi Java, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan melihat cara membuat workbook Excel, mengimpor list of maps sebagai tabel data, menerapkan gaya tebal pada kolom tertentu, dan menyimpan hasilnya sebagai file **xlsx**.

Bekerja dengan spreadsheet adalah kebutuhan umum untuk pelaporan, pertukaran data, atau otomatisasi. Pada akhir tutorial ini Anda akan dapat **mengekspor data ke xlsx** dengan pemformatan kolom khusus tanpa meninggalkan kode Java Anda.

## Apa yang Anda perlukan

* Java 17 atau lebih baru (kode juga berfungsi dengan Java 8+)
* Perpustakaan Aspose.Cells for Java – versi 23.10 (atau rilis terbaru)
* Lingkungan pengembangan seperti IntelliJ IDEA atau Eclipse
* Familiaritas dasar dengan koleksi Java (`List`, `Map`)

> **Tips pro:** Tambahkan dependensi Maven Aspose.Cells untuk menjaga perpustakaan tetap terbaru:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Mengimpor list ke Excel dengan Aspose.Cells

Langkah utama pertama adalah mengubah `List<Map<String,Object>>` Java menjadi lembar kerja Excel. Aspose.Cells menyediakan metode `importDataTable`, yang menerima koleksi, flag header, baris/kolom mulai, dan array gaya opsional.

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcel {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Prepare the source data (simulating a DataTable)
        List<Map<String, Object>> dataRows = new ArrayList<>();
        dataRows.add(Map.of("Name", "Alice", "Score", 95));
        dataRows.add(Map.of("Name", "Bob",   "Score", 82));
        dataRows.add(Map.of("Name", "Charlie", "Score", 78));

        // 2️⃣ Create style objects – make the "Score" column bold
        Style[] columnStyles = new Style[2];               // two columns: Name, Score
        Workbook styleWorkbook = new Workbook();           // temporary workbook for style creation
        columnStyles[0] = styleWorkbook.createStyle();    // default style for "Name"
        columnStyles[1] = styleWorkbook.createStyle();    // custom style for "Score"
        columnStyles[1].getFont().setBold(true);          // **how to style column** – bold font

        // 3️⃣ Import the list into a worksheet using the style array
        Workbook workbook = new Workbook();                // **create excel workbook java**
        Worksheet sheet = workbook.getWorksheets().get(0);
        // true → include column headers from the map keys
        sheet.getCells().importDataTable(dataRows, true, 0, 0, columnStyles);

        // 4️⃣ Save the workbook to an .xlsx file
        String outputPath = "output/datatable_with_style.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved to: " + outputPath);
    }
}
```

### Mengapa ini berhasil

* **`importDataTable`** membaca kunci setiap map (`"Name"` dan `"Score"`) sebagai header kolom ketika flag `true` diatur. Ini memenuhi kebutuhan **import data with header**.
* **Array gaya** diselaraskan dengan urutan kolom. Dengan mengatur `columnStyles[1].getFont().setBold(true)`, kita menjawab pertanyaan **how to style column** tanpa memengaruhi kolom lain.
* Menggunakan `Workbook` sementara semata‑mata untuk pembuatan gaya menghindari pencemaran workbook akhir dengan sel yang tidak diperlukan.

## Mengekspor data ke xlsx – menangani kasus tepi umum

### Nilai null dan keamanan tipe
Jika sebuah map berisi `null` atau nilai dengan tipe campuran, Aspose.Cells secara otomatis menulis sel kosong. Untuk menjamin konsistensi tipe, Anda dapat memproses list terlebih dahulu:

```java
for (Map<String, Object> row : dataRows) {
    row.replaceAll((k, v) -> v == null ? "" : v);
}
```

### Jumlah kolom yang tidak cocok
`importDataTable` mengharapkan panjang array gaya sama dengan jumlah kolom. Jika Anda menambahkan kolom baru nanti, ingat untuk memperluas `columnStyles` sesuai, bila tidak Aspose.Cells akan melempar `IndexOutOfBoundsException`.

### Set data besar
Untuk lebih dari 10 000 baris, pertimbangkan menggunakan overload **`importArray`**, yang menyalurkan data langsung ke lembar kerja dan mengurangi konsumsi memori.

## Cara menata kolom tambahan

Anda dapat menata kolom apa pun dengan memperluas array `columnStyles`. Berikut contoh yang membuat baik “Name” maupun “Score” tebal dan menambahkan warna latar belakang pada kolom “Score”.

```java
// Extend to three columns (Name, Score, Date)
Style[] extendedStyles = new Style[3];
Workbook tmp = new Workbook();
extendedStyles[0] = tmp.createStyle(); // Name – bold
extendedStyles[0].getFont().setBold(true);

extendedStyles[1] = tmp.createStyle(); // Score – bold + yellow background
extendedStyles[1].getFont().setBold(true);
extendedStyles[1].getPattern().setBackgroundColor(Color.getYellow());

extendedStyles[2] = tmp.createStyle(); // Date – default
```

Ganti `columnStyles` yang asli dengan `extendedStyles` dan sesuaikan sumber data secara bersamaan. Ini memperlihatkan **how to style column** untuk berbagai skenario.

## Verifikasi hasilnya

Buka `output/datatable_with_style.xlsx` di Microsoft Excel, Google Sheets, atau LibreOffice Calc. Anda akan melihat:

| **Name**   | **Score** |
|------------|----------|
| Alice      | **95**   |
| Bob        | **82**   |
| Charlie    | **78**   |

Header **Score** dan sel‑selnya muncul dalam huruf tebal, mengonfirmasi bahwa gaya telah diterapkan dengan benar.

## Contoh lengkap end‑to‑end (siap salin‑tempel)

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcelFull {
    public static void main(String[] args) throws Exception {
        // ----- Prepare sample data -----
        List<Map<String, Object>> rows = new ArrayList<>();
        rows.add(Map.of("Name", "Alice",   "Score", 95));
        rows.add(Map.of("Name", "Bob",     "Score", 82));
        rows.add(Map.of("Name", "Charlie", "Score", 78));

        // ----- Create column styles (Score column bold) -----
        Style[] styles = new Style[2];
        Workbook styleWB = new Workbook();                // temporary workbook for style objects
        styles[0] = styleWB.createStyle();                // Name – default
        styles[1] = styleWB.createStyle();                // Score – custom
        styles[1].getFont().setBold(true);                // apply bold font

        // ----- Build the workbook and import the list -----
        Workbook wb = new Workbook();                     // **create excel workbook java**
        Worksheet ws = wb.getWorksheets().get(0);
        ws.getCells().importDataTable(rows, true, 0, 0, styles); // true = import header row

        // ----- Save as XLSX -----
        String outFile = "output/datatable_with_style.xlsx";
        wb.save(outFile, SaveFormat.XLSX);

        System.out.println("Excel file created at: " + outFile);
    }
}
```

Menjalankan program ini menghasilkan workbook persis seperti yang ditunjukkan sebelumnya.

## Kesimpulan

Anda kini tahu cara **mengimpor list ke Excel**, menerapkan pemformatan khusus pada kolom tertentu, dan **mengekspor data ke xlsx** menggunakan Aspose.Cells for Java. Tutorial ini mencakup:

* Membuat workbook Excel di Java (`create excel workbook java`)
* Mengimpor list of maps dengan header kolom (`import data with header`)
* Menata kolom (`how to style column`) melalui array gaya
* Menyimpan hasil sebagai file XLSX

Dari sini Anda dapat menjelajahi penataan lanjutan (batas, format angka), menambahkan diagram, atau membuat beberapa lembar kerja dalam satu workbook. Bereksperimenlah dengan sumber data lain—file CSV, basis data, atau respons API REST—untuk memperluas pola yang ditunjukkan dalam panduan ini.

Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)
- [Excel Data Import and Export Tutorials for Aspose.Cells Java](/cells/english/java/import-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}