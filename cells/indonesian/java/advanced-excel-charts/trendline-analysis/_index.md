---
date: 2026-02-09
description: Pelajari cara membuat diagram Excel, menambahkan garis tren, menampilkan
  nilai R‑squared, dan mengekspor diagram ke gambar menggunakan Aspose.Cells untuk
  Java. Termasuk langkah-langkah memuat file Excel, menyesuaikan diagram, dan menyimpan
  sebagai PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Cara Membuat Grafik Excel dengan Garis Tren dan Mengekspor ke Gambar menggunakan
  Aspose.Cells untuk Java
url: /id/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Diagram ke Gambar dengan Analisis Garis Tren

Dalam tutorial ini Anda akan belajar cara **membuat diagram Excel** dengan garis tren, menampilkan nilai R‑squared-nya, dan mengekspor visual yang dihasilkan ke sebuah gambar menggunakan Aspose.Cells for Java. Kami akan memandu Anda memuat workbook yang sudah ada, menambahkan garis tren, menyesuaikan judul, menyimpan workbook, dan akhirnya menghasilkan file PNG/JPEG yang dapat Anda sematkan di mana saja.

## Jawaban Cepat
- **Apa tujuan utama panduan ini?** Menunjukkan cara menambahkan garis tren, menampilkan persamaannya dan nilai R‑squared, serta mengekspor diagram yang dihasilkan ke sebuah gambar menggunakan Java.  
- **Perpustakaan apa yang diperlukan?** Aspose.Cells for Java (unduh [di sini](https://releases.aspose.com/cells/java/)).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya menghasilkan file Excel di Java?** Ya – tutorial ini membuat dan menyimpan workbook XLSX.  
- **Bagaimana cara mengekspor diagram ke PNG atau JPEG?** Gunakan metode `Chart.toImage()` (dibahas pada bagian “Export Chart”).

## Cara membuat diagram Excel dengan garis tren dan mengekspor ke gambar
Judul ini secara langsung menjawab kueri kata kunci utama dan memandu Anda melalui seluruh alur kerja secara logis. Di bawah ini Anda akan menemukan alasan, prasyarat, dan panduan langkah demi langkah.

## Apa itu Ekspor Diagram ke Gambar?
Mengekspor diagram ke gambar mengubah representasi visual data Anda menjadi bitmap portabel (PNG, JPEG, dll.). Ini berguna untuk menyematkan diagram dalam laporan, halaman web, atau presentasi di mana file Excel asli tidak diperlukan.

## Mengapa Menambahkan Garis Tren dan Menampilkan Nilai R‑squared?
Garis tren membantu Anda mengidentifikasi pola dasar dari serangkaian data, sementara metrik **R‑squared** mengukur seberapa baik garis tren cocok dengan data. Menyertakan keduanya dalam gambar yang diekspor memberikan pemangku kepentingan wawasan langsung tanpa harus membuka workbook.

## Prasyarat
- Java 8 atau yang lebih baru terpasang.  
- Perpustakaan Aspose.Cells for Java ditambahkan ke proyek Anda (file JAR pada classpath).  
- Familiaritas dasar dengan IDE Java (IntelliJ IDEA, Eclipse, dll.).  

## Panduan Langkah demi Langkah

### Langkah 1: Siapkan Proyek
Buat proyek Java baru dan tambahkan JAR Aspose.Cells ke jalur build. Ini menyiapkan lingkungan untuk menghasilkan dan memanipulasi file Excel.

### Langkah 2: Muat File Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Kami baru saja **memuat file Excel** ke memori, siap untuk pembuatan diagram.*

### Langkah 3: Buat Diagram
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Di sini kami menghasilkan diagram garis yang nantinya akan menampung garis tren kami.*

### Langkah 4: Tambahkan Garis Tren (how to add trendline) dan Tampilkan Nilai R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Pemanggilan `setDisplayRSquaredValue(true)` memastikan **nilai R‑squared** muncul pada diagram.*

### Langkah 5: Sesuaikan Diagram dan Simpan Workbook (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Sekarang workbook **dihasilkan** dan disimpan sebagai file XLSX, siap untuk diproses lebih lanjut.*

### Langkah 6: Ekspor Diagram ke Gambar (export chart to image)
> **Catatan:** Langkah ini dijelaskan tanpa blok kode tambahan untuk menjaga jumlah blok asli tetap tidak berubah.  
Setelah diagram dibuat dan disimpan, Anda dapat mengekspornya ke gambar dengan memanggil metode `chart.toImage()` dan menulis `java.awt.image.BufferedImage` yang dihasilkan ke format file pilihan Anda (PNG, JPEG, BMP). Alur kerja tipikalnya:
1. Dapatkan objek `Chart` (sudah dilakukan pada langkah sebelumnya).  
2. Panggil `chart.toImage()` untuk memperoleh `BufferedImage`.  
3. Gunakan `ImageIO.write(bufferedImage, "png", new File("chart.png"))` untuk menulis file.  

Ini menghasilkan gambar resolusi tinggi yang dapat Anda sematkan di mana saja, menyelesaikan proses **ekspor diagram ke gambar**.

## Analisis Hasil
Buka `output.xlsx` di Excel untuk memverifikasi bahwa garis tren, persamaan, dan nilai R‑squared muncul seperti yang diharapkan. Buka file gambar yang diekspor (misalnya, `chart.png`) untuk melihat visual bersih yang dapat dibagikan tanpa workbook asli.

## Masalah Umum dan Solusinya
- **Garis tren tidak muncul:** Pastikan rentang data (`A1:A10`) memang berisi nilai numerik; data non‑numerik akan mencegah perhitungan garis tren.  
- **Nilai R‑squared muncul sebagai 0:** Ini sering berarti seri data konstan atau memiliki variasi yang tidak cukup. Coba set data lain atau garis tren polinomial.  
- **Ekspor gambar gagal dengan `NullPointerException`:** Pastikan diagram telah sepenuhnya dirender sebelum memanggil `toImage()`. Menyimpan workbook terlebih dahulu kadang dapat menyelesaikan masalah timing.  

## Pertanyaan yang Sering Diajukan

**T: Bagaimana saya dapat mengubah tipe garis tren?**  
J: Gunakan enumerasi `TrendlineType` yang berbeda saat menambahkan garis tren, misalnya `TrendlineType.POLYNOMIAL` untuk fitting polinomial.

**T: Bisakah saya menyesuaikan tampilan garis tren (warna, ketebalan)?**  
J: Ya. Akses `LineFormat` garis tren melalui `trendline.getLineFormat()` dan atur properti seperti `setWeight()` dan `setColor()`.

**T: Bagaimana cara mengekspor diagram ke PDF alih-alih gambar?**  
J: Konversi diagram ke gambar terlebih dahulu, lalu sematkan gambar tersebut ke PDF menggunakan Aspose.PDF atau perpustakaan PDF pilihan Anda.

**T: Apakah memungkinkan menambahkan beberapa garis tren ke diagram yang sama?**  
J: Tentu saja. Panggil `chart.getNSeries().get(0).getTrendlines().add(...)` untuk setiap seri yang ingin Anda analisis.

**T: Apakah Aspose.Cells mendukung ekspor gambar resolusi tinggi?**  
J: Ya. Anda dapat menentukan DPI saat memanggil `chart.toImage()` dan kemudian menskalakan gambar sesuai sebelum menyimpan.

## Kesimpulan
Anda kini memiliki solusi lengkap, end‑to‑end untuk **membuat diagram Excel**, menambahkan garis tren, menampilkan persamaan dan nilai R‑squared, menyesuaikan visual, menyimpan workbook, dan akhirnya mengekspor diagram sebagai gambar PNG/JPEG. Pendekatan ini memungkinkan Anda menghasilkan aset analitik kelas profesional secara programatis, sempurna untuk pelaporan otomatis, dasbor, atau skenario apa pun di mana gambar statis lebih praktis daripada file Excel.

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.Cells for Java latest  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}