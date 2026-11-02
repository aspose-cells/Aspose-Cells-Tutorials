---
category: general
date: 2026-09-08
description: Cara menyalin rentang di Java menggunakan Aspose.Cells – pelajari cara
  menyalin tabel pivot, menduplikasi tabel pivot, dan mengekspor tabel pivot sambil
  mempertahankan format.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: id
lastmod: 2026-09-08
og_description: Cara menyalin rentang di Java dengan Aspose.Cells. Tutorial ini menunjukkan
  cara menyalin tabel pivot, menduplikasi tabel pivot, dan mengekspor tabel pivot
  sambil mempertahankan format.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Cara menyalin rentang di Java – panduan lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara menyalin rentang di Java dengan Aspose.Cells
url: /id/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin rentang di Java dengan Aspose.Cells

Jika Anda perlu **menyalin rentang** di Java, Aspose.Cells membuat tugas ini menjadi sederhana. Baik Anda memindahkan blok sel biasa atau tabel pivot lengkap, perpustakaan ini menangani operasi penyalinan sambil mempertahankan formula, gaya, dan cache pivot. Dalam panduan ini Anda akan belajar untuk **menyalin tabel pivot**, **menggandakan tabel pivot**, dan bahkan **mengekspor tabel pivot** ke workbook baru dengan format lengkap.

Tutorial ini mencakup semua hal mulai dari penyiapan proyek hingga langkah verifikasi akhir, sehingga Anda dapat menjalankan kode segera setelah membacanya. Tidak ada alat eksternal yang diperlukan selain JAR Aspose.Cells untuk Java.

## Prasyarat

- Java 17 (atau JDK yang didukung) terpasang dan dikonfigurasi di IDE Anda.
- Maven atau Gradle untuk manajemen dependensi (contoh menggunakan Maven).
- File Excel sumber (`source.xlsx`) yang berisi tabel pivot dalam rentang `A1:H20`.
- Familiaritas dasar dengan pemrograman Java.

## Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Aspose.Cells adalah perpustakaan komersial, tetapi versi evaluasi gratis tersedia. Tambahkan dependensi ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Jika Anda lebih suka Gradle, entri yang setara adalah:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Menambahkan JAR memberi Anda akses ke kelas `Workbook`, `Worksheet`, `Range`, dan `CopyOptions` yang digunakan sepanjang panduan ini.

## Langkah 2: Muat workbook sumber dan pilih lembar kerja pertama

Bagian pertama dari **menyalin rentang** adalah membuka workbook yang berisi data yang ingin Anda pindahkan.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Mengapa ini penting:** Membuka workbook membuat representasi dalam memori yang dapat dimanipulasi oleh API tanpa menyentuh file asli di disk.

## Langkah 3: Tentukan rentang yang berisi tabel pivot

Tabel pivot berada di dalam blok persegi panjang. Anda harus menentukan blok tersebut agar Aspose.Cells mengetahui apa yang harus disalin.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Catatan:** Metode `createRange` **tidak** menyalin apa pun saat ini; ia hanya membuat objek `Range` yang menunjuk ke sel-sel yang ingin Anda gandakan.

## Langkah 4: Buat workbook baru dan dapatkan lembar kerja pertamanya

Sekarang buat workbook tujuan di mana rentang yang disalin akan ditempatkan.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Mengapa workbook baru?** Menggunakan file baru menjamin tidak ada gaya tersembunyi atau rentang bernama yang mengganggu operasi penyalinan, yang terutama penting ketika Anda **mengekspor tabel pivot** ke file terpisah.

## Langkah 5: Salin rentang (termasuk tabel pivot) ke lembar tujuan

Ini adalah inti dari **menyalin rentang dengan format**. Objek `CopyOptions` memberi tahu Aspose.Cells untuk mempertahankan semuanya: nilai, formula, gaya, dan cache pivot.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Salin tabel pivot:** Karena rentang sumber mencakup tabel pivot, API secara otomatis menggandakan cache pivot, sehingga lembar kerja baru berisi tabel pivot yang berfungsi penuh dan berperilaku persis seperti yang asli.

## Langkah 6: Simpan workbook tujuan

Akhirnya, tulis hasilnya ke disk.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Saat Anda membuka `dest.xlsx`, Anda akan melihat replika persis dari tabel pivot asli, lengkap dengan formatnya, slicer, dan bidang terhitung.

## Output yang Diharapkan

- `dest.xlsx` berisi lembar kerja bernama **Sheet1**.
- Sel `A1:H20` memuat data dan tabel pivot yang sama dengan sumber.
- Semua gaya sel (font, warna, batas) dipertahankan.
- Tabel pivot sepenuhnya interaktif; menyegarkannya mencerminkan data dasar di rentang yang disalin.

## Cara menyalin rentang dengan format – penjelasan mendalam

Contoh sebelumnya menunjukkan skenario paling sederhana, tetapi Anda mungkin menemukan variasi yang memerlukan pendekatan sedikit berbeda.

### Salin tabel pivot ke workbook yang sudah ada

Jika Anda perlu **menggandakan tabel pivot** di dalam workbook yang sudah memiliki data, gunakan panggilan `copyRange` yang sama tetapi arahkan ke alamat tujuan yang berbeda:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Ekspor hanya tabel pivot (tanpa data di sekitarnya)

Terkadang Anda hanya menginginkan tabel pivot, bukan data sumber. Identifikasi rentang tampilan tabel pivot melalui metode `getPivotTable`-nya:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Pertahankan pemformatan bersyarat

Aturan pemformatan bersyarat adalah bagian dari koleksi gaya. Flag `PasteType.ALL` sudah menyalinnya, tetapi Anda dapat menyatakannya secara eksplisit:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Kasus tepi dan pemecahan masalah

| Situation | What to watch for | Recommended fix |
|-----------|-------------------|-----------------|
| Workbook sumber dan tujuan menggunakan versi Excel yang berbeda | Beberapa fitur pivot terbaru (misalnya, data model) mungkin tidak ditampilkan dengan benar | Gunakan versi Aspose.Cells terbaru dan setel `Workbook.setFileFormatType(FileFormatType.XLSX)` untuk kedua workbook |
| Tabel pivot sangat besar ( > 10 000 baris) menyebabkan tekanan memori | Kesalahan out‑of‑memory selama penyalinan | Aktifkan `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` sebelum memuat |
| Lembar tujuan sudah berisi rentang bernama dengan nama yang sama dengan sumber | Tabrakan nama menyebabkan kegagalan `CopyOptions` | Panggil `copyOptions.setIgnoreNameConflicts(true)` |

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke dalam kelas Java. Program ini mencakup semua impor, penanganan error, dan komentar.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Jalankan program, lalu buka `dest.xlsx` untuk memverifikasi bahwa tabel pivot berfungsi persis seperti yang asli.

## Kesimpulan

Anda kini mengetahui **cara menyalin rentang** di Java menggunakan Aspose.Cells, termasuk cara **menyalin tabel pivot**, **menggandakan tabel pivot**, dan **mengekspor tabel pivot** sambil mempertahankan semua format. Perpustakaan ini menyembunyikan detail tingkat rendah dari struktur XML Excel, memungkinkan Anda fokus pada logika bisnis.

### Langkah selanjutnya

- Jelajahi **menyalin rentang dengan format** untuk grafik dan gambar (gunakan `PasteType.PICTURES`).
- Otomatiskan pemrosesan batch: lakukan loop pada beberapa file sumber dan konsolidasikan tabel pivot mereka ke dalam workbook ringkasan.
- Gabungkan teknik ini dengan Aspose.Slides untuk menghasilkan laporan PowerPoint yang menyematkan pivot yang disalin

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Memperbarui Sumber Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimalkan Pemuatan Tabel Pivot di Java menggunakan Aspose.Cells – Panduan Komprehensif](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Cara Menyalin Tabel Pivot di C# – Konversi Excel ke PPTX, Salin Rentang & Buat Kotak Teks](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}