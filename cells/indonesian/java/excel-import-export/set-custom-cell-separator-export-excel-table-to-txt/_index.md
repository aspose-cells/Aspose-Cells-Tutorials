---
category: general
date: 2026-07-16
description: Tetapkan pemisah sel khusus saat mengekspor tabel Excel ke TXT menggunakan
  Aspose.Cells. Pelajari cara mengekspor formula Excel ke teks dan menyimpan lembar
  kerja sebagai file txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: id
lastmod: 2026-07-16
og_description: Atur pemisah sel khusus di Aspose.Cells memungkinkan Anda mengekspor
  tabel Excel ke TXT dengan format yang tepat. Ekspor rumus Excel ke teks dan simpan
  lembar kerja sebagai file txt dengan mudah.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Atur Pemisah Sel Kustom – Ekspor Tabel Excel ke TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Atur Pemisah Sel Kustom – Ekspor Tabel Excel ke TXT
url: /id/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur Pemisah Sel Kustom – Ekspor Tabel Excel ke TXT

Set custom cell separator adalah rahasia yang Anda butuhkan ketika ingin menghasilkan dump teks yang rapi dari lembar Excel. Pernah bertanya-tanya bagaimana cara **export excel table to txt** tanpa berakhir dengan kekacauan koma dan jeda baris? Dalam tutorial ini kita akan melewati seluruh proses menggunakan Aspose.Cells for Java, mulai dari memuat workbook hingga **save worksheet as txt file** dengan pemisah yang Anda pilih.

## Apa yang Akan Anda Pelajari

- Cara **set custom cell separator** untuk ekspor teks.
- Langkah‑langkah tepat untuk **export excel formulas to text** sehingga nilai yang telah dievaluasi ikut terbawa.
- Cara **export excel data as plain text** sambil mempertahankan tata letak.
- Contoh kode lengkap yang siap‑jalankan dan dapat Anda salin‑tempel ke proyek Anda.

Pada akhir panduan ini Anda akan dapat mengambil workbook Excel apa pun, memilih pipa (`|`), tab (`\t`), atau karakter apa saja yang Anda suka, dan menghasilkan file teks terdelimitasi yang disukai sistem hilir.

### Prasyarat

- Java 8 atau yang lebih baru terpasang.
- Maven (atau alat build lain) untuk mengambil pustaka Aspose.Cells for Java.
- Sebuah workbook contoh (`TableDemo.xlsx`) yang berisi tabel dengan rumus.

Jika Anda sudah memiliki semua itu, mari kita mulai—tanpa embel‑embel, hanya langkah praktis.

## Langkah 1: Tambahkan Aspose.Cells ke Proyek Anda

Sebelum Anda dapat **set custom cell separator**, Anda memerlukan JAR Aspose.Cells di classpath. Cara termudah adalah lewat Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Jika Anda lebih suka Gradle, ganti XML dengan yang setara `implementation 'com.aspose:aspose-cells:24.10'`. Setelah dependensi terpasang, Anda siap menulis kode Java yang berinteraksi dengan file Excel.

## Langkah 2: Muat Workbook – Menyiapkan Ekspor Tabel Excel ke TXT

Baris kode pertama yang sesungguhnya selalu sama: buka workbook yang berisi tabel yang ingin Anda ekspor.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Di sini kita mengambil worksheet pertama (`get(0)`). Jika data Anda berada di sheet lain, cukup ubah indeks atau gunakan `get("SheetName")`. Bagian ini penting untuk **export excel table to txt** karena exporter bekerja pada level worksheet.

## Langkah 3: Atur Pemisah Sel Kustom – Inti dari Proses Ekspor

Sekarang tiba saatnya bintang utama: mengonfigurasi `ExportTableOptions`. Objek ini memungkinkan Anda menentukan secara tepat bagaimana setiap sel muncul di file teks akhir.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Mengapa kita **set custom cell separator**? Karena pemisah default adalah tab, yang dapat berbenturan dengan data yang sudah mengandung tab. Dengan memilih pipa (`|`) atau titik koma, Anda menjamin setiap kolom tetap terpisah ketika parser hilir membaca file.

### Export Excel Formulas to Text

Baris `setFormulaValueInCell(true)` memberi tahu Aspose.Cells untuk menulis **export excel formulas to text** sebagai *hasil* rumus, bukan string rumus itu sendiri. Jika Anda melewatkannya, sel yang berisi `=SUM(A1:A5)` akan muncul sebagai `=SUM(A1:A5)` di TXT, yang jarang diinginkan.

## Langkah 4: Lampirkan Opsi Ekspor ke TxtSaveOptions

Sekarang kita mengaitkan opsi tabel tersebut ke konfigurasi ekspor TXT secara keseluruhan.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` adalah objek payung yang mengontrol bagaimana seluruh worksheet ditulis. Dengan memasukkan `exportTableOptions` ke dalamnya, Anda memastikan setiap tabel di sheet mematuhi aturan **set custom cell separator**.

## Langkah 5: Simpan Worksheet sebagai File TXT – Menyelesaikan Ekspor

Akhirnya, kita menulis file ke disk.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Menjalankan program ini akan menghasilkan `TableExported.txt`. Setiap baris tabel Excel asli kini akan muncul sebagai baris nilai yang dipisahkan pipa, misalnya:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Perhatikan bagaimana rumus di kolom **Total** telah dievaluasi sebelum ditulis—berkat `setFormulaValueInCell(true)`. Itulah esensi **export excel data as plain text** sambil mempertahankan hasil perhitungan.

## Langkah 6: Verifikasi Output – Apakah Sudah Sesuai?

Buka `TableExported.txt` yang dihasilkan di editor teks apa pun. Anda harus melihat:

- Satu baris per baris Excel.
- Kolom dipisahkan oleh karakter pipa yang Anda tetapkan dengan `setCellValueSeparator`.
- Tidak ada koma atau tab yang tidak diinginkan kecuali memang ada dalam nilai sel asli.
- Hasil rumus, bukan rumusnya sendiri.

Jika Anda menemukan karakter tak terduga, periksa kembali pemisah yang Anda pilih. Beberapa karakter (seperti pipa) aman untuk kebanyakan parser gaya CSV, namun bila data Anda sudah mengandung pipa, pertimbangkan pemisah lain seperti `~` atau tab (`\t`).

## Tips, Kasus Pinggir, dan Praktik Terbaik – Export Excel Data as Plain Text

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Data sudah mengandung pemisah yang Anda pilih** | Beralih ke karakter yang kurang umum (`^`, `~`, atau karakter Unicode non‑printing). |
| **Anda memerlukan enkoding UTF‑8** |  |

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}