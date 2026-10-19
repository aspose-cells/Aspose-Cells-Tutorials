---
category: general
date: 2026-06-27
description: Simpan Excel sebagai TSV dengan cepat menggunakan Java. Pelajari cara
  mengekspor lembar kerja ke teks, mengekspor lembar kerja sebagai teks biasa, dan
  mengekspor string data Excel dengan Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: id
og_description: Simpan Excel sebagai TSV menggunakan Java. Tutorial ini menunjukkan
  cara mengekspor lembar kerja ke teks, mengekspor lembar kerja sebagai teks biasa,
  dan mengekspor string data Excel secara efisien.
og_title: Simpan Excel sebagai TSV – Panduan Ekspor Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Simpan Excel sebagai TSV – Panduan Lengkap Mengekspor Lembar Kerja ke Teks
url: /id/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan Excel sebagai TSV – Panduan Lengkap Mengekspor Worksheet ke Teks

Pernah membutuhkan untuk **save Excel as TSV** tetapi tidak yakin panggilan API mana yang harus digunakan? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika mereka mencoba mengubah spreadsheet menjadi file ber‑delimiter tab untuk pemrosesan lanjutan. Kabar baiknya? Dengan beberapa baris Java dan Aspose.Cells Anda dapat mengekspor worksheet ke teks, mengekspor sheet plain text, dan bahkan mengekspor Excel data string tanpa kesulitan.

Dalam tutorial ini kami akan membahas seluruh alur kerja—mulai dari memuat workbook hingga mengonfigurasi opsi ekspor dan akhirnya menulis file TSV ke disk. Pada akhir tutorial Anda akan dapat **save Excel as TSV** dalam proyek Java apa pun, baik Anda menangani satu lembar atau memproses puluhan file sekaligus.

## Apa yang Dibahas dalam Panduan Ini

* Memuat workbook Excel dari disk  
* Memilih worksheet yang tepat (atau melakukan iterasi pada banyak worksheet)  
* Mengonfigurasi `ExportTableOptions` untuk menghasilkan output plain‑text  
* Menulis data sebagai file nilai dipisahkan tab (TSV)  
* Tips untuk menangani rentang besar, delimiter berbeda, dan karakter Unicode  

Tidak memerlukan alat eksternal—hanya Aspose.Cells untuk Java dan runtime Java 8+.

---

## Langkah 1: Siapkan Proyek Anda dan Muat Workbook

Sebelum kita masuk ke kode, pastikan Anda telah menambahkan JAR Aspose.Cells ke classpath proyek Anda. Jika Anda menggunakan Maven, dependensinya terlihat seperti ini:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Sekarang kita dapat memuat workbook:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Mengapa ini penting:** Memuat file adalah langkah pertama dalam alur kerja **export Excel data string** apa pun. Jika file tidak dapat dibuka, tidak ada yang lain yang akan berhasil.

### Pro tip
Jika Anda menangani file yang dilindungi password, panggil `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## Langkah 2: Pilih Worksheet yang Ingin Anda Ekspor

Anda dapat mengambil sheet pertama, sheet berdasarkan nama, atau iterasi semua sheet. Berikut kasus paling sederhana—mengekspor worksheet pertama:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Jika Anda perlu **export worksheet to text** untuk setiap sheet, bungkus kode di atas dalam loop `for`:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## Langkah 3: Buat dan Konfigurasikan Opsi Ekspor

Inti dari **export sheet plain text** terletak pada `ExportTableOptions`. Dengan mengubah beberapa properti, kita mengubah rentang menjadi string plain‑text dengan delimiter tab:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Mengapa menggunakan `setExportAsString(true)`?**  
> Itu memberi tahu Aspose.Cells untuk memperlakukan output sebagai teks mentah, yang persis apa yang Anda butuhkan ketika ingin **save Excel as TSV**. Alternatifnya adalah ekspor CSV atau HTML, yang keduanya tidak memberikan pemisahan tab yang bersih.

### Kasus Tepi: Delimiter Kustom
Jika sistem downstream Anda mengharapkan pipe (`|`) alih‑alih tab, cukup ubah delimiter:

```java
exportOptions.setDelimiter('|');
```

---

## Langkah 4: Ekspor Rentang yang Diinginkan ke File Teks

Sekarang kita benar‑benar menulis file TSV. Metode `exportTable` menerima tiga argumen: rentang sel, path output, dan `ExportTableOptions` yang baru saja kita konfigurasikan.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Jika Anda ingin mengekspor *seluruh* rentang yang digunakan, ganti `"A1:D20"` dengan `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Pro tip
Setelah mengekspor, Anda juga dapat menangkap string secara langsung:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Itu memberi Anda **export Excel data string** mentah tanpa menyentuh sistem file.

---

## Langkah 5: Menangani File Besar dan Tips Kinerja

Saat menangani spreadsheet besar (ratusan ribu baris), pertimbangkan optimasi berikut:

| Masalah | Solusi |
|-------|----------|
| Tekanan memori | Gunakan `WorkbookFactory.create(InputStream)` untuk streaming file alih‑alih memuatnya sepenuhnya. |
| I/O lambat | Tulis ke `BufferedWriter` atau gunakan NIO `Files.newBufferedWriter`. |
| Karakter Unicode | Pastikan file output ditulis dengan UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Berikut adalah cuplikan yang menggabungkan streaming dan enkoding UTF‑8:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## Kesalahan Umum dan Cara Menghindarinya

1. **Lupa mengatur `setExportAsString(true)`.**  
   Tanpa flag ini Aspose akan menghasilkan file Excel biner, yang merusak tujuan **export worksheet to text** Anda.

2. **Menggunakan delimiter yang salah.**  
   Koma alih‑alih tab akan menghasilkan CSV, bukan TSV. Periksa kembali `setDelimiter('\t')`.

3. **Sintaks rentang tidak tepat.**  
   `"A1:D20"` baik‑baik saja, tetapi `"A1:D20:"` (titik dua ekstra) akan menyebabkan `IllegalArgumentException`.

4. **Izin file.**  
   Pastikan direktori target dapat ditulisi. Di Linux, `chmod 755` sering menyelesaikan masalah.

---

## Menyimpulkan Semua – Contoh Lengkap yang Berfungsi

Berikut program lengkap yang siap dijalankan yang mendemonstrasikan **save Excel as TSV** dari awal hingga akhir:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Menjalankan program ini menghasilkan file ber‑pemisah tab (`out.tsv`) yang dapat dikonsumsi oleh sistem downstream mana pun—baik itu pemuat basis data, skrip Unix `awk`, atau penampil spreadsheet sederhana.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **save Excel as TSV** menggunakan Java dan Aspose.Cells. Mulai dari memuat workbook, memilih sheet yang tepat, mengonfigurasi `ExportTableOptions`, dan akhirnya menulis file, Anda kini memiliki pola yang solid dan siap produksi untuk skenario **export worksheet to text**, **export sheet plain text**, dan **export Excel data string**.

Apa selanjutnya? Cobalah mengekspor beberapa rentang, mengganti delimiter secara dinamis, atau streaming output langsung ke respons HTTP untuk unduhan berbasis web. Prinsip yang sama berlaku, dan Anda akan menemukan bahwa menangani data Excel dalam teks biasa menjadi sangat mudah setelah dasar‑dasarnya dipahami.

Ada pertanyaan atau menemukan kasus tepi yang aneh? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekspor Data Excel ke HTML5 Menggunakan Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Ekspor Data Excel Tanpa Usaha menggunakan Aspose.Cells untuk Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [Cara Mengekspor Worksheet Excel ke PNG Menggunakan Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}