---
category: general
date: 2026-08-08
description: Cara menyalin pivot di Aspose.Cells dan menyalin rentang ke workbook
  menggunakan Java. Pelajari langkah‑langkah tepat untuk menduplikasi tabel pivot
  dengan CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: id
lastmod: 2026-08-08
og_description: Cara menyalin pivot di Aspose.Cells dan menyalin rentang ke workbook
  dengan Java. Ikuti panduan lengkap ini untuk menggandakan tabel pivot menggunakan
  CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Cara menyalin pivot di Aspose.Cells – menyalin rentang ke buku kerja
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Cara menyalin pivot di Aspose.Cells – menyalin rentang ke buku kerja
url: /id/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin pivot di Aspose.Cells – menyalin rentang ke workbook

Jika Anda perlu **cara menyalin pivot** dalam file Excel menggunakan Aspose.Cells, panduan ini menunjukkan proses yang tepat. Pada akhir tutorial Anda akan dapat **menyalin rentang ke workbook** sambil mempertahankan definisi tabel pivot.

Contoh ini menggunakan Java, tetapi konsep yang sama berlaku untuk bahasa .NET apa pun yang bekerja dengan Aspose.Cells. Tidak diperlukan alat eksternal—hanya pustaka Aspose.Cells untuk Java dan lingkungan pengembangan dasar.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Java Development Kit (JDK) 8 atau yang lebih baru.
* Maven atau Gradle untuk mengelola dependensi (contoh menggunakan Maven).
* Aspose.Cells untuk Java 23.9 (atau versi terbaru) yang ditambahkan ke proyek Anda.
* Sebuah workbook input (`input.xlsx`) yang berisi setidaknya satu tabel pivot pada lembar kerja pertama.

Menyiapkan hal‑hal ini mencegah kesalahan runtime ketika kode mengakses workbook.

## Cara menyalin pivot dengan Aspose.Cells

Bagian ini menjelaskan setiap langkah yang diperlukan untuk **cara menyalin pivot** dari satu bagian lembar ke bagian lain, menggunakan kelas `CopyOptions`.

### Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Mengapa langkah ini penting*: Pustaka menyediakan kelas `Workbook`, `CopyOptions`, dan kelas lain yang diperlukan untuk operasi **aspose.cells copy range**. Tanpa dependensi, kompiler tidak dapat menemukan tipe‑tipe tersebut.

### Langkah 2: Muat workbook sumber

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Memuat file membuat representasi spreadsheet di memori. Objek `Workbook` memberi Anda akses ke lembar kerja, sel, dan tabel pivot.

### Langkah 3: Konfigurasikan opsi penyalinan untuk menyertakan tabel pivot

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` memberi tahu Aspose.Cells bahwa operasi harus mempertahankan metadata tabel pivot. Jika Anda menghilangkan flag ini, tabel pivot akan menjadi data statis, kehilangan interaktivitasnya.

### Langkah 4: Salin rentang yang diinginkan beserta tabel pivot

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Metode `copyRange` menyalin sel, format, dan—karena opsi yang diatur pada langkah sebelumnya—setiap tabel pivot yang berpotongan dengan rentang. Inilah inti dari fungsionalitas **copy range to workbook**.

### Langkah 5: Simpan workbook yang telah dimodifikasi

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Menyimpan menuliskan perubahan ke file baru (`output.xlsx`). Sekarang Anda dapat membuka file ini di Excel dan melihat bahwa tabel pivot telah digandakan persis di tempat rentang disalin.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua potongan kode, berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Hasil yang diharapkan

* `output.xlsx` berisi data yang sama dengan `input.xlsx`.
* Tabel pivot yang semula berada di rentang sumber muncul di sel tujuan, berfungsi penuh (filter, kemampuan refresh, dll.).
* Semua format sel, rumus, dan lebar kolom dipertahankan karena `copyRange` menyalin seluruh blok sel.

## Pertanyaan umum dan kasus tepi

**Bagaimana jika rentang tujuan tumpang tindih dengan tabel pivot yang sudah ada?**  
Aspose.Cells akan menimpa sel target. Untuk menghindari kehilangan data, pastikan area tujuan kosong atau pindahkan tabel pivot yang ada terlebih dahulu.

**Apakah saya dapat menyalin tabel pivot antar lembar kerja?**  
Ya. Gunakan `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` dimana `targetSheetIndex` menunjuk ke lembar kerja tujuan.

**Apakah `setCopyPivotTable(true)` menyalin sumber data yang mendasarinya?**  
Metode ini hanya menyalin referensi cache pivot. Jika data sumber berada di workbook yang sama, pivot tujuan akan menunjuk ke cache yang sama. Untuk menggandakan cache, Anda harus membuat cache pivot baru secara manual.

**Bagaimana menyalin rentang besar secara efisien?**  
Saat menyalin rentang sangat besar, pertimbangkan hanya menggunakan `CopyOptions.setCopyFormula(true)` dan `setCopyDataValidation(true)` bila diperlukan. Mengurangi jumlah opsi dapat meningkatkan kinerja.

## Tips untuk penggunaan **aspose.cells copy range** yang andal

* **Pro tip:** Selalu panggil `workbook.calculateFormula()` setelah menyalin jika rentang berisi rumus yang bergantung pada cache pivot.
* **Waspadai:** Lembar kerja tersembunyi. `copyRange` hanya bekerja pada lembar kerja yang terlihat kecuali Anda secara eksplisit merujuk ke lembar tersembunyi dengan indeksnya.
* **Pemeriksaan versi:** Flag `setCopyPivotTable` tersedia mulai Aspose.Cells 20.9. Pastikan versi pustaka Anda mendukungnya.

## Kesimpulan

Anda kini mengetahui **cara menyalin pivot** di Aspose.Cells dan **cara menyalin rentang ke workbook** sambil mempertahankan fungsionalitas pivot secara penuh. Langkah‑langkah—menambahkan pustaka, memuat workbook, mengonfigurasi `CopyOptions`, melakukan penyalinan, dan menyimpan—membentuk pola berulang yang dapat Anda adaptasi ke skenario salin‑tempel lainnya.

Selanjutnya, jelajahi topik terkait seperti **aspose.cells copy range** untuk diagram, pemformatan bersyarat, dan validasi data. Bereksperimenlah dengan menyalin antar format file yang berbeda (XLSX → XLS) untuk memperluas kemampuan otomatisasi Anda. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}