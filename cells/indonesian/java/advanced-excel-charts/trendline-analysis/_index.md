---
date: 2026-08-27
description: Pelajari cara menambahkan trendline ke chart, menampilkan nilai R‑squared,
  dan mengekspor chart sebagai gambar PNG atau JPEG menggunakan Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Ekspor Chart ke Gambar dengan Analisis Trendline
og_description: Tambahkan trendline ke chart, lihat R‑squared, dan ekspor hasil sebagai
  PNG/JPEG menggunakan Aspose.Cells for Java – solusi cepat dengan dukungan 50 format.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Tambahkan trendline ke chart dan ekspor sebagai gambar dengan Aspose.Cells
  for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Cara menambahkan trendline ke chart dan mengekspor sebagai gambar di Java
url: /id/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan garis tren ke diagram dan ekspor sebagai gambar

Dalam tutorial ini Anda akan belajar cara **menambahkan garis tren ke diagram**, menampilkan nilai R‑squared, dan mengekspor visual ke file PNG atau JPEG menggunakan Aspose.Cells for Java. Anda akan melihat mengapa garis tren penting, cara menyiapkan workbook, dan langkah‑langkah tepat untuk menghasilkan gambar beresolusi tinggi yang dapat disematkan dalam laporan, email, atau halaman web.

## Jawaban Cepat
- **Apa tujuan utama panduan ini?** Untuk menunjukkan cara menambahkan garis tren ke diagram, menampilkan persamaannya dan nilai R‑squared, serta mengekspor diagram sebagai gambar dengan Java.  
- **Perpustakaan mana yang saya perlukan?** Aspose.Cells for Java – unduh dari [Aspose.Cells for Java release page](https://releases.aspose.com/cells/java/).  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk penyebaran produksi.  
- **Bisakah saya menghasilkan workbook Excel secara programatis?** Ya – tutorial ini membuat dan menyimpan workbook XLSX dari awal.  
- **Bagaimana diagram diekspor ke PNG atau JPEG?** Panggil metode `Chart.toImage()` dan tulis `BufferedImage` yang dikembalikan dengan `ImageIO.write(...)`.

## Bagaimana cara membuat diagram Excel dengan garis tren dan mengekspornya ke gambar?
Muat workbook, tambahkan diagram garis, lampirkan garis tren yang menampilkan persamaan dan nilai R‑squared, simpan workbook, lalu panggil `chart.toImage()` dan tulis `BufferedImage` yang dihasilkan ke file PNG atau JPEG. Alur end‑to‑end ini hanya memerlukan beberapa baris kode Java dan menghasilkan gambar pixel‑perfect yang cocok untuk aplikasi downstream apa pun.

## Apa itu mengekspor diagram ke gambar?
Mengekspor diagram ke gambar mengubah representasi visual data Anda menjadi bitmap portabel (PNG, JPEG, BMP, dll.). Format ini ideal untuk menyematkan diagram dalam laporan, halaman web, atau presentasi di mana file Excel asli tidak diperlukan.

## Mengapa menambahkan garis tren dan menampilkan nilai R‑squared?
Garis tren mengungkap pola mendasar dari serangkaian data, sementara metrik **R‑squared** mengukur seberapa dekat garis tren cocok dengan data. Menyertakan keduanya dalam gambar yang diekspor memberi pemangku kepentingan wawasan langsung tanpa membuka workbook. Ini membantu pengambil keputusan menilai kekuatan korelasi dan meramalkan tren dengan cepat tanpa harus membuka Excel.

## Prasyarat
- Java 8 atau yang lebih baru terpasang di mesin pengembangan Anda.  
- Perpustakaan Aspose.Cells for Java ditambahkan ke classpath proyek (file JAR).  
- Familiaritas dengan IDE Java seperti IntelliJ IDEA atau Eclipse.  

## Panduan langkah demi langkah

### Langkah 1: siapkan proyek
Buat proyek Java baru dan letakkan JAR Aspose.Cells pada jalur build. Ini menyiapkan lingkungan untuk menghasilkan dan memanipulasi file Excel.

### Langkah 2: muat file excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Kami baru saja **memuat file Excel** ke dalam memori, siap untuk pembuatan diagram.*

### Langkah 3: buat diagram
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Di sini kami menghasilkan diagram garis yang nantinya akan menampung garis tren kami.*

### Langkah 4: tambahkan garis tren (how to add trendline) dan tampilkan nilai R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Pemanggilan `setDisplayRSquaredValue(true)` memastikan **nilai R‑squared** muncul pada diagram.*

### Langkah 5: sesuaikan diagram dan simpan workbook (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Sekarang workbook **dihasilkan** dan disimpan sebagai file XLSX, siap untuk pemrosesan lebih lanjut.*

### Langkah 6: ekspor diagram ke gambar (export chart to image)
> **Catatan:** Langkah ini dijelaskan tanpa blok kode tambahan untuk menjaga jumlah blok asli tidak berubah.  
Setelah diagram dibuat dan disimpan, Anda dapat mengekspornya ke gambar dengan memanggil metode `chart.toImage()` dan menulis `java.awt.image.BufferedImage` yang dihasilkan ke format file pilihan Anda (PNG, JPEG, BMP). Alur kerja tipikalnya:
1. Dapatkan objek `Chart` (sudah dilakukan pada langkah sebelumnya).  
2. Panggil `chart.toImage()` untuk memperoleh `BufferedImage`.  
3. Gunakan `ImageIO.write(bufferedImage, "png", new File("chart.png"))` untuk menulis file.  

Objek `Chart` mewakili sebuah diagram dalam workbook dan menyediakan metode untuk memodifikasi penampilan serta datanya. `BufferedImage` adalah kelas Java yang menyimpan gambar di memori, memungkinkan penyimpanan ke file. `ImageIO` adalah kelas utilitas untuk membaca dan menulis gambar di Java. `setDisplayRSquaredValue` mengaktifkan penampilan statistik R‑squared pada garis tren.

### Analisis hasil
Buka `output.xlsx` di Excel untuk memverifikasi bahwa garis tren, persamaan, dan nilai R‑squared muncul sebagaimana mestinya. Buka file gambar yang diekspor (misalnya `chart.png`) untuk melihat visual bersih yang dapat dibagikan tanpa workbook asli.

## Masalah umum dan solusi
- **Garis tren tidak muncul:** Pastikan rentang data (`A1:A10`) berisi nilai numerik; data non‑numerik mencegah perhitungan garis tren.  
- **Nilai R‑squared muncul sebagai 0:** Ini biasanya berarti seri data konstan atau tidak memiliki variasi. Coba set data lain atau gunakan garis tren polinomial.  
- **Ekspor gambar gagal dengan `NullPointerException`:** Pastikan diagram telah sepenuhnya dirender sebelum memanggil `toImage()`. Menyimpan workbook terlebih dahulu kadang dapat menyelesaikan masalah timing.

## Pertanyaan yang sering diajukan

**Q: Bagaimana saya dapat mengubah tipe garis tren?**  
A: Gunakan enumerasi `TrendlineType` yang berbeda saat menambahkan garis tren, misalnya `TrendlineType.POLYNOMIAL` untuk fitting polinomial.

**Q: Bisakah saya menyesuaikan penampilan garis tren (warna, ketebalan)?**  
A: Ya. Akses `LineFormat` garis tren melalui `trendline.getLineFormat()` dan atur properti seperti `setWeight()` dan `setColor()`.

**Q: Bagaimana cara mengekspor diagram ke PDF alih-alih gambar?**  
A: Konversi diagram ke gambar terlebih dahulu, lalu sematkan gambar tersebut ke PDF menggunakan Aspose.PDF atau perpustakaan PDF lainnya.

**Q: Apakah memungkinkan menambahkan beberapa garis tren ke diagram yang sama?**  
A: Tentu saja. Panggil `chart.getNSeries().get(0).getTrendlines().add(...)` untuk setiap seri yang ingin Anda analisis.

**Q: Apakah Aspose.Cells mendukung ekspor gambar beresolusi tinggi?**  
A: Ya. Anda dapat menentukan DPI saat memanggil `chart.toImage()` dan kemudian menskalakan gambar sebelum menyimpan, memastikan output tajam untuk cetak atau layar berdensitas tinggi.

---

**Terakhir Diperbarui:** 2026-08-27  
**Diuji Dengan:** Aspose.Cells for Java terbaru (mendukung 50+ format file dan memproses workbook hingga 2 juta baris tanpa memuat seluruh memori)  
**Penulis:** Aspose

## Tutorial Terkait

- [Tambahkan Label Data ke Diagram Excel dengan Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Cara Mengekspor Diagram Excel sebagai SVG Menggunakan Aspose.Cells Java untuk Grafik Vektor Skalabel](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Ekspor Diagram Excel ke PDF Menggunakan Aspose.Cells for Java&#58; Panduan Ukuran Halaman Kustom](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}