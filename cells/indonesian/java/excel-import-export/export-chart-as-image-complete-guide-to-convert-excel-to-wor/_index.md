---
category: general
date: 2026-06-30
description: Ekspor diagram sebagai gambar dan pelajari cara mengekspor diagram, menyimpan
  Excel sebagai Word, mengonversi Excel ke Word, serta mengonversi XLSX ke DOCX dalam
  beberapa langkah mudah.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: id
og_description: Ekspor diagram sebagai gambar dan konversi Excel ke Word dengan cepat.
  Ikuti panduan ini untuk menyimpan Excel sebagai Word, mengekspor diagram, dan mengonversi
  XLSX ke DOCX.
og_title: Ekspor Grafik sebagai Gambar – Konversi Excel ke Word Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Ekspor Grafik sebagai Gambar – Panduan Lengkap Mengonversi Excel ke Word
url: /id/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Diagram sebagai Gambar – Panduan Lengkap Mengonversi Excel ke Word

Pernah bertanya-tanya bagaimana cara mengekspor diagram sebagai gambar dari buku kerja Excel dan langsung menempelkannya ke dokumen Word? Anda bukan satu‑satunya—para pengembang terus menanyakan, “Bagaimana cara mengekspor diagram dari XLSX dan menyematkannya ke DOCX tanpa kehilangan kualitas?”  

Kabar baiknya, dengan beberapa baris kode Java Anda dapat **mengekspor diagram sebagai gambar**, lalu **menyimpan Excel sebagai Word** dalam satu alur yang mulus. Dalam tutorial ini kami akan membahas seluruh proses, mulai dari memuat buku kerja hingga mengonfigurasi opsi penyimpanan yang mengubah diagram Anda menjadi PNG tajam di dalam file DOCX.

Kami juga akan menyentuh tugas terkait seperti **mengonversi Excel ke Word**, **menyimpan Excel sebagai Word**, dan **mengonversi XLSX ke DOCX**—semua sambil menjaga kode tetap jelas dan dapat dijalankan. Tanpa basa‑basi, hanya solusi praktis yang dapat Anda salin‑tempel hari ini.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

- **Java Development Kit (JDK) 8+** – kode ini berjalan pada JDK modern apa pun.
- **Aspose.Cells for Java** versi 23.10 atau lebih baru. Anda dapat mengunduhnya dari Maven Central atau mengunduh JAR secara langsung.
- Sebuah **file Excel** (`charts.xlsx`) yang berisi setidaknya satu diagram yang ingin Anda ekspor.
- Sebuah **IDE Java** (IntelliJ IDEA, Eclipse, atau VS Code) – pilih yang Anda suka.
- Pengetahuan dasar tentang Java dan Maven/Gradle (opsional tetapi membantu).

Itu saja. Tanpa plugin tambahan, tanpa interop COM, hanya Java murni.

---

## Langkah 1: Muat Buku Kerja Excel dan Temukan Diagramnya

Hal pertama yang harus kita lakukan adalah membuka buku kerja yang berisi diagram. Aspose.Cells membuatnya sangat mudah—cukup arahkan ke jalur file.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Mengapa ini penting:** Memuat buku kerja memberi kita akses ke objek diagram, yang nantinya akan kami perintahkan kepada Aspose untuk dirender sebagai gambar. Jika buku kerja berisi beberapa lembar atau diagram, Anda dapat menyesuaikan indeks atau melakukan iterasi melalui mereka.

---

## Langkah 2: Konfigurasikan Opsi Penyimpanan DOCX untuk Mengekspor Diagram sebagai Gambar

Aspose.Cells menyediakan kelas `DocxSaveOptions` yang memungkinkan Anda mengontrol cara konversi bekerja. Menetapkan `setExportChartAsImage(true)` memberi tahu perpustakaan untuk meraster setiap diagram menjadi gambar sebelum disematkan ke dalam file Word.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Tips profesional:** Jika Anda lebih suka grafik vektor (EMF/WMF) Anda dapat membiarkan flag ini mati, tetapi gambar raster biasanya ditampilkan lebih konsisten di semua versi Word.

---

## Langkah 3: Simpan Buku Kerja sebagai File DOCX

Setelah opsi‑opsi tersebut diatur, kita cukup menyimpan buku kerja. Perpustakaan akan menangani konversi semua lembar kerja, tabel, dan—berkat flag yang kami setel—diagram sebagai gambar.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **Apa yang Anda dapatkan:** Sebuah file `charts.docx` di mana diagram Excel asli muncul sebagai PNG beresolusi tinggi (atau JPEG, tergantung pengaturan) di dalam dokumen Word. Buka file tersebut di Microsoft Word untuk melihat hasilnya.

---

## Langkah 4: Verifikasi Output (Opsional tetapi Disarankan)

Selalu merupakan ide yang baik untuk memverifikasi secara programatik bahwa konversi berhasil, terutama saat mengotomatisasi proses batch.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Jika Anda menjalankan potongan kode ini dan melihat pesan sukses, Anda telah berhasil **mengonversi XLSX ke DOCX** sambil mempertahankan visual diagram sebagai gambar.

---

## Contoh Lengkap yang Siap Dijalan

Berikut adalah program Java lengkap yang siap dijalankan dan menggabungkan semua langkah. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya di mesin Anda.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Output yang diharapkan saat Anda menjalankan program:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

Buka `charts.docx` di Microsoft Word, dan Anda akan melihat diagram ditampilkan sebagai gambar bersih, tepat pada posisi di mana diagram Excel asli berada.

---

## Pertanyaan Umum & Kasus Khusus

### Bagaimana jika buku kerja saya memiliki banyak diagram?

Anda tidak perlu mengubah apa‑apa—menetapkan `setExportChartAsImage(true)` berlaku untuk **semua** diagram dalam buku kerja. Jika Anda hanya menginginkan diagram tertentu sebagai gambar, Anda harus mengekspornya secara manual menggunakan `chart.toImage()` dan kemudian menyisipkannya ke file Word sendiri.

### Bisakah saya mengontrol format gambar (PNG vs JPEG)?

Aspose.Cells menggunakan PNG secara default untuk ekspor diagram‑sebagai‑gambar. Untuk beralih ke JPEG, Anda dapat menyesuaikan `ImageOrPrintOptions` sebelum menyimpan:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Apakah ini bekerja dengan file Excel lama (.xls)?

Tentu saja. Kode yang sama bekerja untuk `.xls` maupun `.xlsx`. Aspose.Cells secara otomatis mendeteksi format, sehingga Anda dapat **menyimpan Excel sebagai Word** terlepas dari versi sumbernya.

### Bagaimana perbedaannya dengan “mengonversi Excel ke Word” menggunakan interop Office native?

Interop native biasanya memerlukan mesin Windows dengan Office terpasang, dan diagram dapat kehilangan ketajaman. Menggunakan Aspose.Cells bersifat platform‑agnostik, bekerja di Linux/macOS, dan mempertahankan kualitas diagram dengan merasternya.

---

## Tips untuk Implementasi Siap Produksi

- **Pemrosesan batch:** Loop melalui direktori berisi file XLSX, terapkan `DocxSaveOptions` yang sama. Bungkus konversi dalam blok try‑catch untuk menangani file korup secara elegan.
- **Manajemen memori:** Untuk buku kerja yang sangat besar, panggil `workbook.dispose()` setelah menyimpan untuk membebaskan sumber daya native.
- **Kustomisasi:** Anda juga dapat menetapkan `saveOptions.setPreserveCellFormatting(true)` jika perlu mempertahankan gaya sel saat mengonversi.
- **Logging:** Integrasikan kerangka kerja logging (SLF4J, Log4j) untuk merekam statistik konversi—berguna untuk jejak audit.

---

## Kesimpulan

Anda kini memiliki solusi end‑to‑end yang **mengekspor diagram sebagai gambar**, **menyimpan Excel sebagai Word**, dan **mengonversi XLSX ke DOCX** dengan hanya beberapa pernyataan Java. Inti utama adalah bahwa `DocxSaveOptions` dari Aspose.Cells membuat penanganan diagram menjadi sangat mudah—tanpa ekstraksi gambar manual, tanpa interop COM, dan dukungan lintas platform penuh.

Silakan bereksperimen: coba mengekspor beberapa lembar kerja, sesuaikan resolusi gambar, atau gabungkan pendekatan ini dengan perpustakaan Aspose lainnya (seperti Aspose.Words) untuk dokumen Word yang lebih kaya. Langit adalah batasnya ketika Anda sudah tahu cara mengekspor diagram dengan benar.

Punya pertanyaan lebih lanjut tentang mengonversi file Excel, menyematkan gambar, atau mengoptimalkan performa? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut membahas topik terkait yang erat kaitannya dengan teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Convert Excel Chart to Image with Aspose.Cells .NET](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET: A Step‑by‑Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}