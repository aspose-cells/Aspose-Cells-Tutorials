---
category: general
date: 2026-10-23
description: Pelajari cara menggandakan lembar Excel di Java sambil mempertahankan
  tabel pivot. Panduan ini juga menunjukkan cara menyalin tabel pivot, menyalin rentang
  Excel, dan menyalin lembar dengan data pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: id
lastmod: 2026-10-23
og_description: Duplikat lembar Excel di Java sambil mempertahankan tabel pivot. Ikuti
  tutorial lengkap ini untuk menyalin tabel pivot, menyalin rentang Excel, dan menyalin
  lembar dengan data pivot.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplikat lembar Excel dengan tabel pivot di Java – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Cara menyalin lembar Excel dan menjaga pivot table tetap utuh di Java
url: /id/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menduplikasi lembar Excel dan mempertahankan tabel pivot tetap utuh di Java

Jika Anda perlu **duplicate Excel sheet** sambil mempertahankan setiap tabel pivot tetap aktif, panduan ini menunjukkan cara tepatnya. Anda akan melihat solusi singkat yang menyalin sebuah lembar, menyalin rentang tertentu, dan bahkan menyalin tabel pivot ke workbook lain—semua dalam Java murni menggunakan Aspose.Cells.

Menduplikasi lembar Excel adalah tugas umum ketika Anda menghasilkan laporan bulanan dari templat atau ketika Anda membutuhkan salinan sandbox untuk pengujian. Kode di bawah ini bekerja dengan Aspose.Cells 25.11 atau yang lebih baru, yang memperkenalkan opsi `setCopyPivotTable(true)`.

## Apa yang Anda perlukan

- Java 17 (atau JDK terbaru lainnya) terpasang
- Aspose.Cells for Java 25.11 atau yang lebih baru dalam proyek Anda (koordinat Maven `com.aspose:aspose-cells:25.11`)
- Workbook sumber (`SourceWithPivot.xlsx`) yang sudah berisi tabel pivot
- IDE atau alat build pilihan Anda (IntelliJ IDEA, Eclipse, Maven, Gradle, dll.)

## Langkah 1: Muat workbook sumber yang berisi tabel pivot

Operasi pertama adalah membuka workbook yang berisi pivot yang ingin Anda pertahankan.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Mengapa langkah ini penting:** Memuat workbook sumber memberi Anda akses ke objek worksheet, sel, dan tabel pivot yang tertanam. Tanpa ini, Anda tidak dapat merujuk data pivot yang ingin Anda salin.

## Langkah 2: Buat workbook tujuan kosong (atau muat yang sudah ada)

Anda dapat memulai dari workbook kosong atau membuka file yang sudah ada yang akan menerima lembar yang diduplikasi.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Tip:** Jika Anda sudah memiliki workbook pelaporan, ganti baris di atas dengan `new Workbook("ExistingReport.xlsx")` untuk menambahkan lembar yang diduplikasi ke dalamnya.

## Langkah 3: Salin seluruh worksheet – tabel pivot dipertahankan secara otomatis

Menyalin seluruh worksheet adalah cara paling sederhana untuk **copy sheet with pivot**. Aspose.Cells menyalin definisi pivot dan cache-nya secara otomatis.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Mengapa ini berhasil:** `addCopy` menggandakan struktur lembar, nilai sel, gaya, dan semua tabel pivot yang tertanam. Worksheet baru di `dstWb` akan terlihat identik dengan yang asli, termasuk cache pivot.

## Langkah 4: (Opsional) Salin hanya rentang tertentu yang mencakup tabel pivot

Terkadang Anda tidak menginginkan seluruh lembar—mungkin Anda hanya membutuhkan bagian yang berisi pivot. Di sinilah Anda **copy Excel range** dan secara eksplisit meminta pivot untuk disalin.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Bagaimana ini membantu:** `setCopyPivotTable(true)` memaksa engine untuk menggandakan definisi pivot bahkan ketika Anda menyalin rentang terbatas. Tanpa flag ini, hanya data mentah yang akan disalin, dan pivot akan hilang.

## Langkah 5: Simpan workbook tujuan

Akhirnya, tulis konten yang diduplikasi ke file baru.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Output yang diharapkan

Menjalankan program akan membuat `DuplicatedWithPivot.xlsx` di direktori target. Buka file tersebut di Excel dan Anda akan melihat:

- Worksheet baru bernama `Sheet1 (Copy)` (atau nama asli dengan tambahan “Copy”)
- Tabel pivot muncul persis seperti di lembar sumber, berfungsi penuh
- Jika Anda menggunakan penyalinan rentang opsional, hanya sel A1:G30 yang ada, tetapi pivot tetap berfungsi karena cache-nya telah disalin

## Pertanyaan umum dan kasus tepi

### Bagaimana menyalin pivot ke workbook lain tanpa menyalin seluruh lembar?

Jika Anda hanya membutuhkan pivot dan data dasarnya, salin rentang yang berisi data sumber dan pivot, lalu gunakan `setCopyPivotTable(true)`. Kode yang sama dari **Langkah 4** berlaku; pastikan rentang mencakup sumber data.

### Bagaimana jika workbook sumber memiliki beberapa worksheet dengan pivot?

Ulangi **Langkah 3** untuk setiap worksheet yang ingin Anda duplikasi:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Apakah ini bekerja dengan worksheet yang dilindungi?

Aspose.Cells dapat menyalin sheet yang dilindungi, tetapi Anda harus membuka proteksinya terlebih dahulu jika perlu memodifikasi pivot setelah penyalinan:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Bisakah saya menyalin tabel pivot ke workbook yang sudah ada dan sudah berisi sheet dengan nama yang sama?

Ya. Gunakan `addCopy` dengan nama unik:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Pro tip: verifikasi cache pivot

Setelah menyalin, Anda dapat secara programatis memastikan bahwa cache pivot ada:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Jika ID cache mencetak angka non‑negatif, pivot berhasil diduplikasi.

## Kesimpulan

Anda kini tahu cara **duplicate Excel sheet** di Java sambil mempertahankan setiap tabel pivot, cara **copy pivot** tabel secara langsung, cara **copy Excel range** yang mencakup pivot, dan cara **copy sheet with pivot** atau **copy pivot to workbook** menggunakan Aspose.Cells 25.11+. Terapkan pola ini untuk mengotomatiskan pembuatan laporan, membuat klon templat, atau membangun lingkungan pengujian yang memerlukan analitik berbasis pivot yang identik.

Siap menjelajah lebih jauh? Cobalah mengekspor workbook yang diduplikasi ke PDF, atau secara programatis menyegarkan cache pivot setelah penyalinan untuk memastikan data terbaru tercermin. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara menduplikasi worksheet dan mempertahankan tabel pivot di Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Cara Menyalin Tabel Pivot di Java – Panduan Lengkap Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Cara menyalin rentang dan mempertahankan tabel pivot di Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}