---
category: general
date: 2026-09-27
description: Ekspor lembar kerja ke CSV di Java menggunakan Aspose.Cells dan atur
  presisi menjadi 5 digit signifikan – panduan lengkap langkah demi langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export worksheet to csv
- save workbook as csv
- how to set precision
- save excel as csv
- export excel to csv
language: id
lastmod: 2026-09-27
og_description: Ekspor lembar kerja ke CSV di Java dengan Aspose.Cells, pelajari cara
  mengatur presisi dan menyimpan buku kerja sebagai CSV dalam beberapa langkah saja.
og_image_alt: Screenshot showing Java code that exports worksheet to CSV with precision
og_title: Ekspor lembar kerja ke CSV dengan presisi di Java – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Export worksheet to CSV in Java using Aspose.Cells and set precision
    to 5 significant digits – a complete step‑by‑step guide.
  headline: How to export worksheet to CSV with precision in Java
  type: TechArticle
- description: Export worksheet to CSV in Java using Aspose.Cells and set precision
    to 5 significant digits – a complete step‑by‑step guide.
  name: How to export worksheet to CSV with precision in Java
  steps:
  - name: Exporting a specific worksheet
    text: 'If your workbook has multiple sheets and you only want to export one, use
      the `Worksheet` object directly:'
  - name: Exporting without losing leading zeros
    text: 'CSV treats all fields as text, but some parsers may strip leading zeros.
      To preserve them, wrap the value in double quotes:'
  - name: Using a different delimiter
    text: 'If you prefer semicolons instead of commas (common in European locales),
      set the delimiter:'
  - name: Handling large files
    text: 'For workbooks exceeding several hundred megabytes, consider streaming the
      export:'
  - name: Next steps
    text: '* Explore additional `ExportTableOptions` properties such as `setEncoding`,
      `setQuoteAllFields`, and `setSeparator` to fine‑tune your CSV output. * Combine
      the export with Java’s `java.nio.file` APIs to automate batch processing of
      multiple Excel files. * Dive into Aspose.Cells’ **export excel to CS'
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Cara mengekspor lembar kerja ke CSV dengan presisi di Java
url: /id/java/excel-import-export/how-to-export-worksheet-to-csv-with-precision-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor worksheet ke CSV dengan presisi di Java

Jika Anda perlu **export worksheet to CSV** sambil mengontrol jumlah digit signifikan, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells for Java. Anda akan belajar cara memuat file Excel, mengatur presisi yang diinginkan, dan **save workbook as CSV** dalam beberapa langkah sederhana.

Mengekspor data ke CSV adalah kebutuhan umum saat mengintegrasikan laporan berbasis Excel dengan sistem lain, dan mempertahankan presisi numerik dapat mencegah kesalahan perhitungan di hilir. Pada akhir tutorial ini Anda akan dapat **save Excel as CSV** dengan presisi khusus, dan Anda juga akan melihat bagaimana pendekatan yang sama bekerja untuk skenario umum **export excel to CSV**.

## Prasyarat

* Java Development Kit (JDK) 8 atau yang lebih baru terpasang.
* Maven atau Gradle untuk mengelola dependensi (kami akan menggunakan Maven dalam contoh).
* Lisensi Aspose.Cells for Java (evaluasi gratis dapat digunakan untuk pengujian).
* File Excel contoh (`Numbers.xlsx`) yang berisi angka-angka yang ingin Anda ekspor.

## Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Tambahkan dependensi Maven Aspose.Cells ke `pom.xml` Anda. Ini memberi Anda akses ke kelas `Workbook`, `ExportTableOptions`, dan `SaveFormat` yang diperlukan untuk ekspor.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

*Mengapa langkah ini penting*: Tanpa perpustakaan tersebut Anda tidak dapat memanipulasi file Excel secara programatik. Menggunakan Maven memastikan JAR yang tepat diunduh dan tetap terbarui.

## Langkah 2: Muat workbook yang berisi angka-angka

Buat instance `Workbook` yang menunjuk ke file Excel sumber Anda. Langkah ini menyiapkan worksheet untuk diekspor.

```java
import com.aspose.cells.*;

public class SignificantDigitsExport {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the numbers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Numbers.xlsx");
```

*Penjelasan*: Kelas `Workbook` mewakili seluruh file Excel. Memuatnya sekali memungkinkan Anda menggunakan kembali objek yang sama untuk beberapa operasi ekspor, seperti **save workbook as CSV** dengan pengaturan yang berbeda.

## Langkah 3: Konfigurasikan opsi ekspor untuk mengatur presisi

Aspose.Cells memungkinkan Anda membatasi jumlah digit signifikan melalui `ExportTableOptions`. Menyetelnya dengan benar menerapkan persyaratan **how to set precision**.

```java
        // Create export options and limit the output to 5 significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(5); // keep only 5 significant digits
```

*Mengapa ini penting*: File CSV menyimpan angka sebagai teks biasa. Jika sel Excel asli berisi banyak tempat desimal, CSV dapat menjadi tidak terkelola. Dengan memanggil `setSignificantDigits`, Anda memastikan setiap nilai numerik dibulatkan ke presisi yang ditentukan sebelum ditulis ke file.

## Langkah 4: Ekspor data worksheet ke CSV menggunakan opsi yang telah dikonfigurasi

Sekarang panggil `Workbook.save` dengan enum `SaveFormat.CSV` dan berikan `exportOptions`. Ini melakukan operasi **export excel to CSV** yang sesungguhnya.

```java
        // Export the worksheet data to CSV using the configured options
        workbook.save("YOUR_DIRECTORY/Numbers_SigDigits.csv",
                      SaveFormat.CSV,
                      exportOptions);
    }
}
```

*Apa yang terjadi di balik layar*: Aspose.Cells mengiterasi setiap sel, menerapkan aturan presisi, dan menulis teks hasil ke aliran CSV. File output (`Numbers_SigDigits.csv`) berada di direktori yang sama yang Anda tentukan.

## Output yang Diharapkan

Anggap `Numbers.xlsx` berisi nilai-nilai berikut di kolom **A**:

| A          |
|------------|
| 123.456789 |
| 0.00123456 |
| 98765.4321 |

Setelah menjalankan kode dengan `setSignificantDigits(5)`, `Numbers_SigDigits.csv` akan berisi:

```
123.46
0.0012346
98765
```

Perhatikan bagaimana setiap angka dibulatkan menjadi lima digit signifikan, sesuai dengan presisi yang Anda tentukan.

## Langkah 5: Verifikasi file CSV

Buka CSV yang dihasilkan dengan editor teks atau impor ke aplikasi lain (mis., basis data atau alat analisis data) untuk memastikan bahwa:

1. File tersebut diformat dengan benar (nilai dipisahkan koma).
2. Nilai numerik menghormati presisi 5 digit.
3. Tidak ada kutipan tambahan atau karakter escape yang muncul kecuali data asli memerlukannya.

Jika Anda memerlukan presisi yang berbeda, cukup ubah argumen yang diberikan ke `setSignificantDigits`.

## Variasi umum dan kasus tepi

### Mengekspor worksheet tertentu

Jika workbook Anda memiliki beberapa sheet dan Anda hanya ingin mengekspor satu, gunakan objek `Worksheet` secara langsung:

```java
Worksheet sheet = workbook.getWorksheets().get(0); // first sheet
sheet.getCells().exportTableOptions(exportOptions);
sheet.getCells().exportCsv("YOUR_DIRECTORY/Sheet1_SigDigits.csv", exportOptions);
```

### Mengekspor tanpa kehilangan nol di depan

CSV memperlakukan semua bidang sebagai teks, tetapi beberapa parser dapat menghapus nol di depan. Untuk mempertahankannya, bungkus nilai dengan tanda kutip ganda:

```java
exportOptions.setQuoteAllFields(true);
```

### Menggunakan delimiter yang berbeda

Jika Anda lebih suka titik koma daripada koma (umum di wilayah Eropa), atur delimiter:

```java
exportOptions.setSeparator(';');
```

### Menangani file besar

Untuk workbook yang melebihi beberapa ratus megabyte, pertimbangkan streaming ekspor:

```java
Workbook workbook = new Workbook("largeFile.xlsx", new LoadOptions(LoadFormat.XLSX));
workbook.save("largeFile.csv", SaveFormat.CSV, exportOptions);
```

Aspose.Cells memproses file dalam potongan, mengurangi konsumsi memori.

## Tips Pro

* **License early** – Daftarkan lisensi Aspose.Cells Anda sebelum pembuatan `Workbook` pertama untuk menghindari watermark evaluasi.
* **Reuse ExportTableOptions** – Jika Anda perlu mengekspor banyak worksheet dengan presisi yang sama, buat satu instance `ExportTableOptions` dan gunakan kembali.
* **Validate numeric columns** – Setelah ekspor, jalankan skrip singkat untuk memastikan bahwa jumlah digit sesuai dengan harapan Anda, terutama saat menangani notasi ilmiah.

## Kesimpulan

Anda kini memiliki solusi lengkap yang dapat dijalankan untuk **export worksheet to CSV** di Java, dengan kontrol penuh atas presisi numerik. Dengan memuat workbook, mengonfigurasi `ExportTableOptions`, dan memanggil `save` dengan `SaveFormat.CSV`, Anda dapat **save workbook as CSV** sambil menerapkan aturan **how to set precision** yang Anda perlukan. Pendekatan ini bekerja untuk tugas **save excel as CSV** apa pun dan dapat diperluas ke kebutuhan format CSV lainnya.

### Langkah Selanjutnya

* Jelajahi properti tambahan `ExportTableOptions` seperti `setEncoding`, `setQuoteAllFields`, dan `setSeparator` untuk menyempurnakan output CSV Anda.
* Gabungkan ekspor dengan API `java.nio.file` Java untuk mengotomatisasi pemrosesan batch banyak file Excel.
* Selami dokumentasi **export excel to CSV** Aspose.Cells untuk skenario lanjutan seperti agregasi multi‑sheet atau pelestarian format bersyarat.

Selamat coding, dan nikmati ekspor CSV dengan kontrol presisi!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Export CSV with Java – Set Significant Digits & Export Range to CSV](/cells/english/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/)
- [Trim & Save Excel Files as CSV Using Aspose.Cells in Java](/cells/english/java/workbook-operations/excel-aspose-cells-java-trim-save-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}