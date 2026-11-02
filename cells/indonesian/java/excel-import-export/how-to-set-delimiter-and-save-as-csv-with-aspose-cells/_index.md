---
category: general
date: 2026-08-14
description: Cara mengatur pemisah dan menyimpan sebagai CSV menggunakan Aspose.Cells,
  membatasi digit, mengekspor string CSV, dan menghitung ulang formula di Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: id
lastmod: 2026-08-14
og_description: Cara mengatur delimiter dan menyimpan sebagai CSV dengan Aspose.Cells,
  membatasi digit, mengekspor string CSV, serta menghitung ulang rumus di Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Cara mengatur delimiter dan menyimpan sebagai CSV – Panduan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Cara mengatur delimiter dan menyimpan sebagai CSV dengan Aspose.Cells
url: /id/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengatur delimiter dan menyimpan sebagai CSV dengan Aspose.Cells

Jika Anda perlu **cara mengatur delimiter** saat mengekspor data dari workbook Excel, panduan ini menunjukkan solusi lengkap end‑to‑end menggunakan Aspose.Cells untuk Java. Anda akan belajar cara mengonfigurasi delimiter CSV, membatasi jumlah digit signifikan, mengekspor string CSV, dan menyegarkan formula dynamic‑array setelah memuat workbook.

Tutorial ini mencakup semua yang Anda perlukan untuk menjalankan kode di mesin Anda, termasuk penanganan kalender khusus seperti masa pemerintahan Kaisar Jepang. Pada akhir tutorial, Anda akan dapat menghasilkan file CSV yang akurat, mengontrol presisi numerik, dan memastikan formula selalu up‑to‑date.

## Prasyarat

- Java 17 atau lebih baru (kode juga dapat dikompilasi dengan JDK 11+)
- Aspose.Cells untuk Java 23.9 atau yang lebih baru – unduh dari [situs Aspose](https://products.aspose.com/cells/java/)
- Familiaritas dasar dengan Maven atau Gradle untuk manajemen dependensi
- IDE (IntelliJ IDEA, Eclipse, VS Code) atau editor teks sederhana dan command line

> **Tips pro:** Gunakan folder `libs` khusus atau Maven Central untuk menempatkan JAR Aspose.Cells pada classpath Anda. Contoh di bawah mengasumsikan proyek Maven.

## Langkah 1: Siapkan proyek Maven

Buat file `pom.xml` dengan dependensi Aspose.Cells:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Jalankan `mvn clean compile` untuk mengunduh pustaka dan memastikan build berhasil.

## Langkah 2: Cara mengatur delimiter dan menyimpan sebagai CSV

Tujuan utama adalah mengubah delimiter koma default menjadi karakter khusus (misalnya titik koma) saat menyimpan workbook Excel sebagai CSV. Aspose.Cells menyediakan `CsvSaveOptions` untuk tujuan ini.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Mengapa ini berhasil

- `CsvSaveOptions.setDelimiter(char)` memberi tahu Aspose.Cells karakter apa yang memisahkan bidang. Secara default adalah koma, tetapi karakter apa pun (tab `'\t'`, pipa `'|'`, dll.) dapat digunakan.
- `setSignificantDigits(int)` membatasi presisi numerik, memenuhi kebutuhan **cara membatasi digit** tanpa harus memformat setiap sel secara manual.

#### Output yang diharapkan

File `output.csv` akan berisi baris seperti:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Perhatikan bahwa angka dibulatkan menjadi lima digit signifikan (misalnya, `123.45678` → `123.46`).

## Langkah 3: Cara membatasi digit saat menyimpan CSV

Jika Anda memerlukan kontrol yang lebih ketat atas format numerik, Anda juga dapat menggunakan instance `CsvSaveOptions` untuk menentukan string format angka khusus.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` mengikuti pola gaya .NET, yang dipatuhi oleh Aspose.Cells.
- Menggabungkan `setNumberFormat` dan `setSignificantDigits` memberikan pembulatan yang dapat diprediksi di berbagai locale.

## Langkah 4: Cara mengekspor CSV sebagai string dengan delimiter khusus

Terkadang Anda tidak menginginkan file fisik; Anda memerlukan data CSV di memori (misalnya, untuk dikirim sebagai respons HTTP). Kelas `ExportTableOptions` memungkinkan Anda mengekspor rentang sebagai string.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Kapan menggunakan ini

- Mengembalikan CSV dari endpoint REST (`@RestController` di Spring)
- Menyematkan data CSV ke lampiran email tanpa menulis ke disk
- Melakukan pemeriksaan cepat selama unit test

## Langkah 5: Cara menghitung ulang formula setelah memuat workbook

Jika workbook Anda berisi formula—terutama **formula dynamic‑array** yang diperkenalkan pada versi Excel terbaru—Anda harus menghitung ulang mereka setelah memuat file. Aspose.Cells secara otomatis menyegarkan hasil dynamic‑array, tetapi Anda tetap perlu memanggil `calculateFormula()` untuk formula biasa.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Mengapa harus menghitung ulang?

- Formula dapat merujuk data eksternal atau fungsi volatile (`NOW()`, `RAND()`) yang memerlukan nilai terbaru.
- Formula dynamic‑array (misalnya, `=SORT(A1:A10)`) dievaluasi secara otomatis, tetapi memanggil `calculateFormula()` menjamin konsistensi di semua sheet.

## Langkah 6: Contoh lengkap end‑to‑end

Berikut adalah satu kelas yang mendemonstrasikan **cara mengatur delimiter**, **menyimpan sebagai CSV**, **membatasi digit**, **mengekspor string CSV**, **memuat workbook dengan kalender khusus**, dan **menghitung ulang formula**. Kode ini siap disalin‑tempel ke proyek Anda.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Memverifikasi hasil

1. Buka `output.csv` dengan editor teks – Anda harus melihat titik koma (`;`) memisahkan setiap kolom.
2. Pastikan kolom numerik menampilkan paling banyak lima digit signifikan.
3. Output konsol akan mencetak string CSV yang dihasilkan pada langkah 4.
4. Buka `japan_updated.xlsx` di Excel – formula yang sebelumnya menampilkan `#REF!` atau nilai usang kini akan menunjukkan hasil yang benar.

## Kesalahan umum dan cara menghindarinya

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| CSV menampilkan kutipan berlebih | Sel berisi koma sementara delimiter juga koma | Gunakan delimiter lain (`;` atau `\t`) melalui `setDelimiter` |
| Angka dibulatkan tidak tepat | `setSignificantDigits` diterapkan setelah format angka khusus | Terapkan `setNumberFormat` **sebelum** `setSignificantDigits` |

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Load and Save Excel as CSV Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Load a CSV File Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [How to Load CSV Files Using Custom Parsers in Java with Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}