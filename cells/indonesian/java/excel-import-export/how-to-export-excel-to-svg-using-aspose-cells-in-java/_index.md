---
category: general
date: 2026-11-25
description: Ekspor Excel ke SVG dengan Aspose.Cells di Java – panduan langkah demi
  langkah untuk menyimpan Excel sebagai SVG dan membuat gambar vektor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: id
lastmod: 2026-11-25
og_description: Ekspor Excel ke SVG dengan Aspose.Cells di Java. Pelajari cara menyimpan
  Excel sebagai SVG dan menghasilkan gambar vektor berkualitas tinggi dalam beberapa
  baris kode.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Ekspor Excel ke SVG di Java – tutorial lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Cara mengekspor Excel ke SVG menggunakan Aspose.Cells di Java
url: /id/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor Excel ke SVG menggunakan Aspose.Cells di Java

Jika Anda perlu **mengekspor Excel ke SVG**, panduan ini menunjukkan cara melakukannya dengan Aspose.Cells untuk Java. Anda akan belajar cara **menyimpan Excel sebagai SVG** dan menghasilkan **gambar vektor** berkualitas tinggi hanya dengan beberapa baris kode.

Mengekspor workbook Excel ke file SVG memungkinkan Anda menyematkan lembar kerja dalam halaman web, laporan, atau lingkungan apa pun yang mengutamakan grafik yang dapat diskalakan. Format SVG mempertahankan font, warna, dan batas sel tanpa pikselasi yang terjadi pada gambar raster.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Java 17 atau yang lebih baru terpasang.
* Lisensi aktif Aspose.Cells untuk Java (atau kunci evaluasi sementara).
* Proyek Maven atau Gradle tempat Anda dapat menambahkan dependensi Aspose.Cells.

Tambahkan pustaka Aspose.Cells ke proyek Anda:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Mengekspor Excel ke SVG – langkah demi langkah

Proses ini terdiri dari tiga langkah sederhana: memuat workbook, mengonfigurasi opsi ekspor SVG, dan menyimpan hasilnya. Setiap langkah dijelaskan di bawah.

### Langkah 1: Muat workbook yang berisi data

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Mengapa ini penting:**  
`Workbook` adalah objek utama dalam Aspose.Cells. Memuat file sekali memberi Anda akses ke semua worksheet, gaya, dan objek tertanam, yang kemudian akan dirender oleh pengekspor SVG.

### Langkah 2: Atur opsi ekspor gambar untuk SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Mengapa ini penting:**  
`ImageOrPrintOptions` memungkinkan Anda mengontrol format output. Memilih `ImageFormat.SVG` memastikan hasilnya berupa **gambar vektor** bukan bitmap. Mengaktifkan `OnePagePerSheet` menghindari pemisahan halaman di dalam satu sheet, yang biasanya diinginkan ketika SVG akan ditampilkan dalam tampilan web.

### Langkah 3: Simpan workbook sebagai file SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Mengapa ini penting:**  
Metode `save` menggabungkan workbook yang telah dimuat dengan `exportOptions` yang telah dikonfigurasi. Pemanggilan ini menulis file SVG yang sepenuhnya sesuai standar dan dapat dibuka di browser, Inkscape, atau editor vektor apa pun.

## Contoh lengkap yang dapat dijalankan

Menggabungkan ketiga langkah menghasilkan program mandiri yang dapat Anda kompilasi dan jalankan segera:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Output yang diharapkan**

Menjalankan program akan mencetak:

```
Export complete: Excel saved as SVG.
```

Anda akan menemukan `WithVariationSelectors.svg` di `C:/Output`. Membuka file tersebut di browser menampilkan worksheet yang dirender sebagai grafik yang dapat diskalakan, dengan teks, batas, dan warna sel tetap terjaga.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian yang disarankan |
|-----------|------------------------|
| **Multiple worksheets** | Loop melalui `workbook.getWorksheets()` dan panggil `save` untuk setiap sheet, opsional menambahkan nama sheet ke nama file. |
| **Large workbooks** | Tingkatkan `exportOptions.setRenderThreadCount(int)` untuk menggunakan rendering paralel, mengurangi waktu konversi. |
| **Custom DPI** | Panggil `exportOptions.setHorizontalResolution(int)` dan `exportOptions.setVerticalResolution(int)` untuk mengontrol skala viewBox SVG. |
| **Embedding fonts** | Set `exportOptions.setExportFontAsSVG(true)` untuk menyematkan definisi font langsung di dalam SVG, menjamin kesetiaan visual pada mesin yang tidak memiliki font asli. |
| **Password‑protected files** | Berikan password saat memuat: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Tips profesional

* **Hindari fallback raster** – Jika worksheet berisi diagram kompleks, pastikan mereka muncul sebagai elemen vektor dalam SVG. Jika tidak, aktifkan `exportOptions.setExportChartAsSVG(true)`.
* **Kinerja** – Untuk konversi batch, gunakan satu instance `ImageOrPrintOptions` kembali alih-alih membuat yang baru untuk setiap file.
* **Pengujian** – Validasi SVG yang dihasilkan dengan validator online (misalnya, W3C SVG Validator) untuk menemukan markup yang tidak valid lebih awal.

## Verifikasi konversi

Anda dapat memverifikasi secara programatik bahwa file output memang SVG:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

Keberadaan elemen root `<svg>` menandakan operasi **convert Excel to SVG** berhasil.

## Kesimpulan

Tutorial ini menunjukkan cara **mengekspor Excel ke SVG** menggunakan Aspose.Cells untuk Java. Dengan memuat workbook, mengonfigurasi `ImageOrPrintOptions` untuk SVG, dan memanggil `save`, Anda dapat **menyimpan Excel sebagai SVG** dan memperoleh konversi **Excel ke gambar vektor** yang bersih. Selanjutnya Anda dapat menyematkan SVG dalam halaman web, menyertakannya dalam dokumentasi, atau memprosesnya lebih lanjut dengan alat grafis vektor apa pun.

### Apa yang dapat Anda jelajahi selanjutnya

* **Ekspor Excel sebagai PNG atau JPEG** – ubah menjadi `exportOptions.setImageFormat(ImageFormat.PNG)` untuk output raster.
* **Konversi Excel ke PDF** – gunakan `PdfSaveOptions` untuk dokumen yang dapat dicetak.
* **Pemrosesan batch** – gabungkan kode di atas dengan watcher sistem file untuk secara otomatis **mengonversi Excel ke SVG** untuk setiap workbook baru di sebuah folder.

Silakan bereksperimen dengan opsi-opsi tersebut, dan biarkan fleksibilitas Aspose.Cells mengubah data Excel Anda menjadi format visual apa pun yang Anda butuhkan. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengekspor Grafik Excel sebagai SVG Menggunakan Aspose.Cells Java untuk Grafik Vektor Skalabel](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai SVG menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Cara Mengekspor Excel ke SVG – Panduan Langkah‑per‑Langkah Java](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}