---
category: general
date: 2026-09-11
description: Buat lembar kerja baru dan salin rentang Excel menggunakan Aspose.Cells.
  Pelajari cara menyalin rentang antar lembar sambil mempertahankan tabel pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: id
lastmod: 2026-09-11
og_description: Buat lembar kerja baru dan salin rentang Excel dengan Aspose.Cells.
  Tutorial ini menunjukkan langkah-langkah tepat untuk menyalin rentang antar lembar
  dan menjaga tabel pivot tetap utuh.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Buat lembar kerja baru dan salin rentang Excel – Panduan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Buat lembar kerja baru dan salin rentang Excel dengan Aspose.Cells
url: /id/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat lembar kerja baru dan salin rentang Excel dengan Aspose.Cells

Jika Anda perlu **create new worksheet** dan memindahkan data dalam file Excel, Aspose.Cells membuatnya mudah. Panduan ini menunjukkan secara tepat cara menyalin rentang Excel dari satu lembar ke lembar lain sambil mempertahankan semua tabel pivot di dalam rentang.

Anda akan belajar cara **copy excel range**, cara **copy range between sheets**, dan mengapa metode `copy` Aspose.Cells mempertahankan definisi tabel pivot. Tidak diperlukan alat eksternal—hanya proyek Java dengan pustaka Aspose.Cells.

## Prasyarat

- Java 17 atau yang lebih baru terpasang
- Aspose.Cells untuk Java (versi 23.12 atau lebih baru) ditambahkan ke classpath proyek Anda
- Sebuah workbook sumber (`input.xlsx`) yang berisi tabel pivot dalam rentang yang ingin Anda salin
- Familiaritas dasar dengan sintaks Java dan manajemen dependensi Maven/Gradle

## Langkah 1: Siapkan proyek dan impor Aspose.Cells

Buat proyek Maven sederhana (atau Gradle, jika Anda lebih suka) dan tambahkan dependensi Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Kemudian impor kelas yang diperlukan dalam file sumber Java Anda:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Mengapa langkah ini penting*: Mengimpor kelas yang tepat memberi Anda akses ke `Workbook`, `Worksheet`, `Range`, dan metode `copy` yang akan menangani transfer rentang.

## Langkah 2: Muat workbook sumber

Buka workbook yang berisi data yang ingin Anda salin. Kode berikut memuat `input.xlsx` dari direktori yang Anda tentukan:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Penjelasan*: `Workbook` mewakili seluruh file Excel. Memuatnya sekali memberi Anda akses baca/tulis ke setiap lembar dan koleksi sel.

## Langkah 3: Identifikasi rentang sumber yang mencakup tabel pivot

Pilih worksheet yang berisi tabel pivot dan tentukan blok sel tepat yang ingin Anda salin. Dalam contoh ini kami menyalin sel A1 hingga D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Mengapa ini penting*: Dengan membuat objek `Range`, Anda memberi tahu Aspose.Cells sel mana (termasuk objek tersemat seperti tabel pivot) yang harus diduplikasi.

## Langkah 4: **Create new worksheet** yang akan menerima data yang disalin

Sekarang kami menambahkan lembar baru ke workbook yang sama. Inilah titik di mana kata kunci utama muncul:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Penjelasan*: Menambahkan lembar baru mengisolasi data yang disalin, memudahkan verifikasi bahwa operasi **copy excel range** berhasil tanpa memengaruhi lembar asli.

## Langkah 5: Salin rentang – tabel pivot dipertahankan secara otomatis

Gunakan metode `copy` untuk memindahkan rentang dari lembar sumber ke lembar tujuan. Aspose.Cells menyalin formula, format, dan definisi tabel pivot:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Mengapa ini berhasil*: Metode `copy` melakukan deep copy pada sel sumber. Ia tidak hanya menyalin nilai; ia mereplikasi seluruh struktur sel, termasuk cache pivot. Inilah mengapa Anda dapat **copy range aspose.cells** dan masih melihat tabel pivot yang berfungsi pada lembar baru.

## Langkah 6: Simpan workbook dengan lembar kerja baru

Akhirnya, tulis workbook yang telah dimodifikasi ke disk:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Hasil*: `output.xlsx` kini berisi lembar asli plus lembar baru bernama **Copy** yang memuat rentang yang sama persis, termasuk tabel pivot.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut program lengkap yang dapat dijalankan:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Output yang diharapkan**: Buka `output.xlsx` di Excel. Anda akan melihat lembar bernama **Copy** yang sel A1:D20‑nya berisi data, format, dan tabel pivot aktif yang identik dengan yang asli.

## Pertanyaan umum dan kasus tepi

- **Bagaimana jika rentang sumber berisi sel yang digabung?**  
  Metode `copy` juga menyalin informasi penggabungan, sehingga sel yang digabung tetap tidak berubah pada lembar tujuan.

- **Apakah saya dapat menyalin ke workbook yang berbeda?**  
  Ya. Muat instance `Workbook` kedua, buat rentang tujuan di workbook tersebut, dan panggil `sourceRange.copy(destinationRange)`. Metode ini menangani penyalinan lintas‑workbook secara otomatis.

- **Bagaimana jika lembar tujuan sudah memiliki data?**  
  Operasi penyalinan akan menimpa sel yang ada yang berpotongan dengan rentang tujuan. Untuk menghindari kehilangan data, pastikan area tujuan kosong atau gunakan sel mulai yang berbeda (mis., `"B2"`).

- **Apakah cache pivot diduplikasi?**  
  Aspose.Cells menggunakan kembali cache pivot asli, yang berarti tabel pivot baru tetap terhubung ke data sumber yang sama. Jika Anda memerlukan cache yang independen, Anda harus membuat ulang tabel pivot setelah menyalin.

## Tips dan praktik terbaik

- **Tip pro**: Gunakan `Workbook.setForceFormulaRecalculation(true)` sebelum menyimpan jika rentang Anda berisi formula yang bergantung pada data di luar blok yang disalin.
- **Waspadai** rentang besar: menyalin lembar yang sangat besar dapat mengonsumsi memori yang signifikan. Pertimbangkan menyalin dalam potongan lebih kecil jika Anda mengalami `OutOfMemoryError`.
- **Tip kinerja**: Nonaktifkan pembaruan layar (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) saat bekerja dengan file yang sangat besar untuk mempercepat proses penyalinan.

## Kesimpulan

Anda kini tahu cara **create new worksheet** dan **copy excel range** antar lembar menggunakan Aspose.Cells, mempertahankan tabel pivot dan semua atribut sel. Teknik ini memungkinkan Anda menduplikasi blok data secara programatik, membuat templat laporan, atau merestrukturisasi workbook tanpa menyalin‑tempel manual.

Selanjutnya, jelajahi topik terkait seperti **copy range aspose.cells** untuk operasi lintas‑workbook, mengotomatisasi penyegaran tabel pivot, atau mengekspor lembar yang disalin ke PDF. Bereksperimenlah dengan rentang sumber dan nama lembar yang berbeda untuk menyesuaikan skenario otomatisasi Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Salin Bentuk Antara Lembar Excel Menggunakan Aspose.Cells untuk .NET&#58; Panduan Lengkap](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Salin Gambar Antara Lembar di Excel Menggunakan Aspose.Cells untuk Java&#58; Panduan Komprehensif](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Salin Data Rentang](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}