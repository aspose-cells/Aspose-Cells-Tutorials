---
category: general
date: 2026-10-07
description: Pelajari cara membuat PNG dari rentang dan mengekspor data sebagai PNG
  di Java. Panduan ini menunjukkan cara menyimpan gambar rentang Excel menggunakan
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: id
lastmod: 2026-10-07
og_description: Buat PNG dari rentang di Java dan ekspor data sebagai PNG dengan Aspose.Cells.
  Ikuti tutorial lengkap ini untuk menyimpan gambar rentang Excel secara instan.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Buat PNG dari rentang di Java – panduan Aspose.Cells langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara membuat PNG dari rentang di Java dengan Aspose.Cells
url: /id/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat PNG dari rentang di Java dengan Aspose.Cells

Jika Anda perlu **create PNG from range** dalam sebuah workbook Excel, tutorial ini menunjukkan secara tepat cara melakukannya. Pada akhir panduan Anda akan dapat **export data as PNG**, menyimpan gambar rentang Excel, dan menggunakan kembali file tersebut dalam laporan atau halaman web.

Anda akan melihat program Java lengkap yang dapat dijalankan yang memuat workbook, memilih sel yang diinginkan, merendernya sebagai PNG, dan menyimpan hasilnya ke disk. Tidak diperlukan alat eksternal—Aspose.Cells menangani semuanya secara internal.

## Apa yang dibahas dalam tutorial ini

* Prasyarat dan pengaturan Maven untuk Aspose.Cells
* Memuat workbook yang berisi pivot table atau rentang data apa pun
* Mendefinisikan rentang sel yang tepat yang ingin Anda konversi
* Mengonfigurasi opsi gambar untuk output PNG
* Merender rentang dan menyimpan file PNG
* Jebakan umum dan tip untuk gambar berkualitas tinggi

Setelah menyelesaikan langkah-langkah ini Anda akan dapat **convert worksheet to PNG** untuk rentang apa pun, baik itu tabel sederhana atau diagram pivot yang kompleks.

## Prasyarat

* Java 17 atau lebih baru (kode ini dikompilasi dengan JDK 11+)
* Maven 3.6+ (atau Gradle jika Anda lebih suka)
* Aspose.Cells for Java 23.12 atau lebih baru – tambahkan dependensi yang ditunjukkan di bawah
* File Excel yang sudah ada (`PivotWithStyle.xlsx`) yang berisi rentang yang ingin Anda tangkap

> **Pro tip:** Jika Anda tidak memiliki lisensi, Anda dapat meminta kunci evaluasi sementara dari Aspose. Library ini berfungsi dalam mode evaluasi tanpa konfigurasi tambahan.

### Dependensi Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Langkah 1: Muat workbook yang berisi rentang target

Operasi pertama adalah membuka file Excel. Aspose.Cells membaca file ke memori tanpa memerlukan Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Why this matters*: Memuat workbook memberi Anda akses ke lembar kerja, sel, dan properti pengaturan halaman yang diperlukan untuk rendering.

## Langkah 2: Akses lembar kerja yang berisi rentang

Sebagian besar workbook memiliki lembar default pada indeks 0, tetapi Anda juga dapat menggunakan nama lembar.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Jika data Anda berada di lembar lain, ganti `0` dengan indeks yang sesuai atau gunakan `workbook.getWorksheets().get("SheetName")`.

## Langkah 3: Tentukan rentang sel yang ingin Anda konversi

Anda dapat menentukan area persegi panjang apa pun menggunakan notasi A1. Dalam contoh ini kami menangkap `A1:D15`, yang mungkin merupakan pivot table atau blok data biasa.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Edge case*: Ketika rentang mencakup sel yang digabungkan, Aspose.Cells secara otomatis memperluas gambar untuk menyertakan area yang digabungkan.

## Langkah 4: Siapkan opsi gambar PNG

`ImageOrPrintOptions` memungkinkan Anda mengontrol format, resolusi, dan detail rendering lainnya. Menetapkan format penyimpanan ke PNG memastikan kualitas lossless.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Meningkatkan DPI berguna ketika sel sumber berisi font kecil atau diagram detail.

## Langkah 5: Batasi area render ke rentang yang dipilih

Dengan menetapkan rentang sebagai area cetak, Aspose.Cells merender hanya sel tersebut dan mengabaikan sisanya pada lembar.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Jika Anda melewatkan langkah ini, seluruh lembar kerja akan dirasterisasi, yang dapat membuang memori dan menghasilkan gambar yang lebih besar.

## Langkah 6: Render rentang dan tambahkan gambar ke lembar kerja (opsional)

Jika Anda ingin menyematkan PNG yang dihasilkan kembali ke dalam workbook (untuk tujuan pratinjau), Anda dapat menambahkannya sebagai gambar. Langkah ini opsional untuk skenario ekspor murni.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Why you might do this*: Beberapa alur kerja memerlukan gambar menjadi bagian dari workbook sebelum distribusi, seperti membuat laporan cetak yang mencampur sel asli dan gambar.

## Langkah 7: Simpan file PNG ke disk

Akhirnya, tulis gambar ke file. Metode `save` menghormati format yang ditentukan dalam `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Saat program selesai, `PivotImage.png` akan berisi snapshot pixel‑perfect dari sel `A1:D15`.

### Output yang diharapkan

* Sebuah file bernama `PivotImage.png` yang terletak di `YOUR_DIRECTORY`.
* Gambar menunjukkan tata letak, font, warna, dan batas yang tepat dari rentang yang dipilih.
* Jika rentang sumber berisi pivot table, gambar yang dirender mencakup gaya yang sama dan nilai yang dihitung seperti yang ditampilkan di Excel.

## Menangani skenario umum

### Mengekspor rentang tidak berurutan

Aspose.Cells tidak merender rentang terpisah dalam satu gambar. Untuk mengekspor beberapa area, buat gambar terpisah untuk setiap rentang dan gabungkan nanti dengan pustaka pemrosesan gambar (mis., ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Menyimpan lembar kerja besar sebagai PNG

Merender seluruh lembar yang mencakup ribuan baris dapat mengonsumsi memori yang signifikan. Kurangi hal ini dengan:

* Mengurangi DPI (`imageOptions.setResolution(72)`) untuk file yang lebih kecil.
* Menggunakan `setPageCount` untuk membatasi jumlah halaman yang dirender.
* Mengekspor satu halaman cetak pada satu waktu melalui `worksheet.getPageSetup().setPrintArea(...)`.

### Mempertahankan formula sel

Gambar PNG adalah format raster; formula tidak dipertahankan. Jika konsumen hilir memerlukan data mentah, juga ekspor rentang sebagai CSV atau JSON menggunakan `Range.exportDataTable()`.

## Contoh lengkap yang dapat dijalankan

Berikut adalah kelas Java lengkap yang dapat Anda salin‑tempel ke IDE Anda. Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif di mesin Anda.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Jalankan program dengan `mvn compile exec:java` (atau alat build pilihan Anda). Setelah eksekusi, buka `PivotImage.png` untuk memverifikasi hasilnya.

## Kesimpulan

Anda sekarang tahu cara **create PNG from range** di Java menggunakan Aspose.Cells, secara efektif **export data as PNG** dan **save excel range image** untuk skenario pelaporan atau berbagi apa pun. Langkah-langkah—memuat workbook, mendefinisikan rentang, mengonfigurasi opsi gambar, menetapkan area cetak, dan menyimpan file—mencakup seluruh alur kerja untuk **convert worksheet to PNG** dan **save cells as PNG**.

### Langkah selanjutnya

* Bereksperimen dengan nilai `Resolution` yang berbeda untuk menyeimbangkan kualitas dan ukuran file.
* Gunakan `ImageOrPrintOptions.setTransparent(true)` jika Anda memerlukan PNG dengan latar belakang transparan.
* Gabungkan beberapa gambar rentang menjadi satu PDF menggunakan `PdfSaveOptions` untuk laporan multi‑halaman.
* Jelajahi mengekspor ke format raster lain (JPEG, BMP) dengan mengubah `setSaveFormat`.

Silakan sesuaikan pola ini untuk diagram, tabel, atau bahkan seluruh lembar kerja. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekspor Worksheet Excel ke PNG Menggunakan Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Konversi Excel ke PNG Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑per‑Langkah](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Buat Union Range di Excel menggunakan Aspose.Cells Java: Panduan Komprehensif](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}