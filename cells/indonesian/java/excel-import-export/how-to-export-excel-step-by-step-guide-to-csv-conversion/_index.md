---
category: general
date: 2026-06-18
description: Cara mengekspor file Excel dengan cepat – pelajari cara mengonversi xlsx
  ke csv, mengekspor rentang ke csv, dan menulis csv ke file menggunakan Java. Solusi
  sederhana dan andal.
draft: false
keywords:
- how to export excel
- convert xlsx to csv
- write csv to file
- export range to csv
- export excel to csv
language: id
og_description: Cara mengekspor file Excel di Java. Mengonversi xlsx ke csv, mengekspor
  rentang ke csv, dan menulis csv ke file dengan contoh yang siap dijalankan.
og_title: Cara Mengekspor Excel – Tutorial Konversi CSV Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to export Excel files quickly – learn to convert xlsx to csv, export
    range to csv, and write csv to file using Java. Simple, reliable solution.
  headline: 'How to Export Excel: Step‑by‑Step Guide to CSV Conversion'
  type: TechArticle
tags:
- Java
- Excel
- CSV
- File I/O
title: 'Cara Mengekspor Excel: Panduan Langkah-demi-Langkah untuk Konversi CSV'
url: /id/java/excel-import-export/how-to-export-excel-step-by-step-guide-to-csv-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Excel: Tutorial Konversi CSV Lengkap

Pernah bertanya‑tanya **cara mengekspor data Excel** tanpa harus membuka spreadsheet secara manual? Anda tidak sendirian—banyak pengembang membutuhkan cara cepat dan programatik untuk mengubah workbook *.xlsx* menjadi file CSV teks biasa. Dalam panduan ini kami akan menjelaskan cara mengonversi workbook Excel ke CSV, mengekspor rentang tertentu, dan akhirnya menulis string CSV tersebut ke file. Pada akhir tutorial Anda akan memiliki potongan kode Java yang berdiri sendiri dan melakukan semua itu.

Kami juga akan menyelipkan beberapa tips berguna seperti cara **mengonversi xlsx ke csv** dengan format angka dan tanggal khusus, serta mengapa Anda mungkin lebih memilih mengekspor rentang daripada seluruh lembar. Tanpa basa‑basi, hanya solusi praktis yang dapat Anda sisipkan ke proyek apa pun.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Java 17 atau lebih baru (kode ini menggunakan API modern `Files.writeString`).
- Library Aspose.Cells for Java (atau library kompatibel lain yang menyediakan `ExportTableOptions`). Anda dapat mengunduhnya dari Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

- Sebuah file Excel sederhana (`input.xlsx`) yang ditempatkan di folder yang Anda kontrol (ganti `YOUR_DIRECTORY` dengan path sebenarnya).

Sudah siap? Baik—mari kita mulai.

## Langkah 1: Siapkan Opsi Ekspor (Export Range to CSV)

Hal pertama yang harus Anda lakukan adalah memberi tahu library **bagaimana mengekspor data Excel**. `ExportTableOptions` memungkinkan Anda mendefinisikan output string, format angka, dan format tanggal dalam satu objek yang rapi.

```java
// Configure export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);               // Export as a plain string
exportOptions.setNumberFormat("#,##0.00");           // Two‑decimal numbers
exportOptions.setDateFormat("yyyy-MM-dd");           // ISO‑style dates
```

> **Mengapa ini penting:** Dengan mengekspor sebagai string Anda menghindari penanganan aliran byte menengah, dan format khusus memastikan CSV terlihat persis seperti yang Anda harapkan—terutama ketika Anda kemudian **menulis csv ke file**.

## Langkah 2: Muat Workbook (Convert XLSX to CSV)

Selanjutnya, buka workbook sumber. Inilah titik di mana kita sebenarnya **mengonversi xlsx ke csv**—konversi terjadi nanti, tetapi memuat file adalah langkah pertama.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Grab the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Jika Anda perlu bekerja dengan lembar lain, cukup ubah indeks atau gunakan `get("SheetName")`. Library ini menangani format `.xlsx` maupun `.xls` lama, jadi Anda sudah tercakup untuk sebagian besar skenario.

## Langkah 3: Ekspor Rentang Tertentu (Export Range to CSV)

Seringkali Anda tidak memerlukan seluruh lembar—mungkin hanya tabel penjualan di sel `A1:D10`. Di sinilah **export range to csv** berperan. Metode ini mengembalikan satu `String` yang berisi data CSV.

```java
// Export the range A1:D10 as a CSV string using the options defined above
String csvData = worksheet.getCells()
                          .exportTableAsString("A1:D10", exportOptions);
```

> **Tips pro:** String rentang mengikuti notasi A1 Excel, jadi Anda dapat dengan mudah menyesuaikannya menjadi `"B2:F20"` atau rentang dinamis apa pun yang Anda hitung pada waktu runtime.

## Langkah 4: Tulis String CSV ke File (Write CSV to File)

Setelah kita memiliki teks CSV di memori, langkah terakhir adalah menyimpannya. Java 11+ membuat ini menjadi satu baris dengan `Files.writeString`.

```java
// Write the CSV string to an output text file
Files.writeString(Paths.get("YOUR_DIRECTORY/output.txt"), csvData);
```

File akan dibuat jika belum ada, dan ditimpa jika sudah ada—sempurna untuk pekerjaan batch yang menghasilkan laporan setiap hari.

## Langkah 5: Verifikasi Output (Export Excel to CSV)

Pemeriksaan cepat dapat menghemat jam debugging. Buka `output.txt` di editor teks apa pun atau impor kembali ke Excel untuk memastikan konversi berhasil.

```text
Product,Quantity,Price,Total
Widget A,10,12.50,125.00
Widget B,5,8.75,43.75
...
```

Jika angka muncul dengan dua desimal dan tanggal mengikuti `yyyy‑MM‑dd`, Anda telah berhasil **mengekspor excel ke csv** dengan format yang diinginkan.

## Kasus Khusus & Kesalahan Umum

- **Worksheet besar:** Mengekspor seluruh lembar dapat mengonsumsi banyak memori. Gunakan rentang spesifik bila memungkinkan.
- **Karakter khusus:** CSV menggunakan koma sebagai pemisah; jika data Anda mengandung koma, bungkus nilai dengan tanda kutip (`"value, with comma"`). Sebagian besar library menangani ini secara otomatis, tetapi periksa kembali jika Anda melihat baris yang rusak.
- **Encoding:** `Files.writeString` secara default menggunakan UTF‑8. Jika Anda memerlukan charset lain (misalnya Windows‑1252), berikan argumen `Charset`.
- **Sel kosong:** Mereka menjadi string kosong di output CSV—tidak masalah kecuali Anda mengandalkan jumlah kolom tetap.

## Contoh Lengkap yang Siap Dijalan

Berikut adalah kelas Java lengkap yang dapat Anda salin, tempel, dan jalankan. Ganti `YOUR_DIRECTORY` dengan path folder yang sebenarnya di mesin Anda.

```java
import com.aspose.cells.*;
import java.nio.file.*;

public class ExcelToCsvExporter {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("#,##0.00");
        exportOptions.setDateFormat("yyyy-MM-dd");

        // 2️⃣ Load the workbook (convert xlsx to csv later)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Export the desired range (export range to csv)
        String csvData = worksheet.getCells()
                                  .exportTableAsString("A1:D10", exportOptions);

        // 4️⃣ Write the CSV string to a file (write csv to file)
        Path outputPath = Paths.get("YOUR_DIRECTORY/output.txt");
        Files.writeString(outputPath, csvData);

        // 5️⃣ Simple verification message
        System.out.println("✅ CSV export complete! File saved to: " + outputPath);
    }
}
```

**Output konsol yang diharapkan**

```
✅ CSV export complete! File saved to: /path/to/YOUR_DIRECTORY/output.txt
```

Buka `output.txt` yang dihasilkan dan Anda akan melihat tampilan bersih, dipisahkan koma, dari rentang yang dipilih.

## Kesimpulan

Kami telah membahas **cara mengekspor data Excel** ke CSV dengan cara yang bersih dan dapat diulang: mengonfigurasi opsi ekspor, memuat workbook, mengekspor rentang tertentu, dan akhirnya **menulis csv ke file**. Pendekatan ini memberi Anda kontrol penuh atas format angka dan tanggal, sehingga file **export excel to csv** yang dihasilkan siap untuk sistem downstream.

Selanjutnya, Anda dapat mengeksplorasi:

- Mengekspor beberapa rentang dalam satu run (loop melalui named ranges).
- Menggunakan pemisah lain (titik koma) untuk locale yang memerlukannya.
- Men-stream CSV langsung ke respons HTTP untuk unduhan berbasis web.

Cobalah, sesuaikan rentangnya, dan biarkan generasi CSV menjadi bagian mudah dari toolbox Java Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Export Excel to CSV with Blank Rows Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/german/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/french/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}