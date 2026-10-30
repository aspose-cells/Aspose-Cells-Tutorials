---
category: general
date: 2026-08-20
description: Pelajari cara mengekspor diagram ke docx dan mengonversi buku kerja Excel
  ke docx dengan Aspose.Cells di Java. Panduan langkah demi langkah dengan kode lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: id
lastmod: 2026-08-20
og_description: Ekspor grafik ke docx dan konversi buku kerja Excel ke docx menggunakan
  Aspose.Cells untuk Java. Ikuti tutorial lengkap yang dapat dijalankan ini.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Ekspor grafik ke docx dengan Aspose.Cells – Panduan Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Cara mengekspor diagram ke docx dari Excel menggunakan Aspose.Cells untuk Java
url: /id/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengekspor diagram ke docx dari buku kerja Excel menggunakan Java

Jika Anda perlu **export chart to docx** secara langsung dari file Excel, tutorial ini menunjukkan solusi siap‑jalankan. Pada akhir panduan Anda juga akan mengetahui cara **convert Excel workbook to docx** sambil mempertahankan diagram yang dapat diedit, sehingga dokumen Word yang dihasilkan dapat dimodifikasi tanpa kehilangan keakuratan.

Mengekspor diagram umum dilakukan ketika Anda membuat laporan yang menggabungkan perhitungan spreadsheet dengan tata letak Word yang kaya. Aspose.Cells for Java membuat konversi menjadi sederhana, dan API‑nya memungkinkan Anda menjaga diagram tetap dapat diedit—tanpa memerlukan gambar statis.

## Apa yang dibahas dalam tutorial ini

* Memuat buku kerja yang sudah ada yang berisi diagram.  
* Mengonfigurasi `ImageOrPrintOptions` untuk menargetkan format DOCX.  
* Mengaktifkan flag `ExportEditableCharts` (tersedia mulai versi 25.10).  
* Menyimpan buku kerja sebagai file DOCX yang mempertahankan diagram yang dapat diedit.  

Tidak diperlukan alat eksternal selain Aspose.Cells JAR. Kode ini bekerja dengan Java 8+ dan versi terbaru Aspose.Cells mana pun.

## Prasyarat

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 atau lebih baru) | Fitur `setExportEditableCharts` diperkenalkan pada rilis ini. |
| **Java Development Kit (JDK) 8 atau lebih baru** | Menyediakan runtime untuk mengompilasi dan mengeksekusi contoh. |
| **Buku kerja Excel (`.xlsx`) yang berisi setidaknya satu diagram** | Diagram adalah objek yang akan diekspor ke DOCX. |
| **IDE Java atau alat build (mis., Maven, Gradle)** | Mempermudah manajemen dependensi dan eksekusi. |

Anda dapat mengunduh Aspose.Cells JAR terbaru dari [situs Aspose](https://products.aspose.com/cells/java/).

## Langkah 1: Siapkan proyek dan tambahkan dependensi Aspose.Cells

Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Untuk Gradle, tambahkan:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** Gunakan versi tepat yang memperkenalkan `ExportEditableCharts` (25.10) atau rilis yang lebih baru. Versi lama akan mengabaikan flag tersebut dan menghasilkan gambar statis sebagai gantinya.

## Langkah 2: Muat buku kerja yang berisi diagram

Kelas `Workbook` mewakili seluruh file Excel. Memuatnya hanya memerlukan satu baris kode:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Why this matters:** Buku kerja harus dimuat sepenuhnya sebelum Anda dapat menerapkan opsi ekspor apa pun. Jika jalur file tidak tepat, Aspose.Cells akan melempar `FileNotFoundException`.

## Langkah 3: Konfigurasikan opsi gambar/print untuk output DOCX

`ImageOrPrintOptions` mengontrol bagaimana buku kerja dirender. Menetapkan format penyimpanan ke `DOCX` memberi tahu Aspose.Cells untuk menghasilkan dokumen Word alih‑alih gambar.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Anda juga dapat menyesuaikan ukuran halaman, DPI, atau kualitas gambar di sini, tetapi hal‑hal tersebut bersifat opsional untuk ekspor diagram.

## Langkah 4: Aktifkan ekspor diagram yang dapat diedit

Mulai versi 25.10, Aspose.Cells dapat menyematkan diagram sebagai objek diagram Word native. Ini membuatnya sepenuhnya dapat diedit di Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Edge case:** Jika Anda mengatur flag ini ke `false` (atau mengabaikannya), diagram akan dirender sebagai gambar statis. Gunakan `true` hanya ketika audiens target perlu mengedit diagram setelah konversi.

## Langkah 5: Simpan buku kerja sebagai file DOCX

Akhirnya, panggil `Workbook.save` dengan opsi yang telah dikonfigurasi:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Setelah program selesai, buka `ChartEditable.docx` di Microsoft Word. Anda akan melihat diagram asli, dan jika Anda meng‑klik‑kan kanan diagram tersebut, opsi **Edit Data** akan tersedia—menegaskan bahwa diagram benar‑benar dapat diedit.

## Contoh lengkap yang dapat dijalankan

Berikut adalah file sumber lengkap. Salin ke IDE Anda, ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif, dan jalankan.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Output yang diharapkan**

* File bernama `ChartEditable.docx` di direktori yang ditentukan.  
* Membuka file di Word menampilkan diagram persis seperti yang muncul di Excel, dan Anda dapat meng‑klik‑ganda diagram untuk mengedit seri data.

## Kesalahan umum dan cara menghindarinya

| Symptom | Cause | Fix |
|---------|-------|-----|
| Word menampilkan **gambar statis** alih‑alih diagram yang dapat diedit | `setExportEditableCharts` tidak dipanggil atau menggunakan versi < 25.10 | Pastikan flag diatur ke `true` dan Anda menggunakan Aspose.Cells 25.10 atau lebih baru. |
| DOCX yang dihasilkan **kosong** | Jalur file sumber workbook tidak tepat atau izin tidak cukup | Verifikasi jalur workbook dan pastikan aplikasi memiliki akses baca/tulis. |
| Tata letak diagram terlihat **terdistorsi** | Pengaturan halaman di Excel (mis., baris/kolom tersembunyi) berbeda dengan default Word | Sesuaikan `ImageOrPrintOptions` (mis., `setOnePagePerSheet(true)`) untuk mengontrol skala. |
| **Kinerja** menurun pada workbook besar | Mengekspor banyak diagram atau set data besar | Ekspor hanya lembar yang diperlukan atau gunakan `setSheetIndex` untuk membatasi pemrosesan. |

## Memperluas solusi

* **Multiple charts:** Iterasi semua worksheet dan panggil `worksheet.getCharts()` untuk mengekspor setiap diagram secara terpisah.  
* **Custom DOCX styling:** Setelah menyimpan, gunakan Aspose.Words untuk menambahkan header, footer, atau gaya ke dokumen yang dihasilkan.  
* **Batch conversion:** Bungkus kode dalam loop yang memproses direktori berkas `.xlsx`, menghasilkan DOCX untuk masing‑masing.

## Kesimpulan

Anda kini memiliki metode andal untuk **export chart to docx** dan **convert Excel workbook to docx** sambil mempertahankan kemampuan edit penuh pada diagram. Langkah‑langkah kunci adalah memuat workbook, mengonfigurasi `ImageOrPrintOptions` untuk DOCX, mengaktifkan `ExportEditableCharts`, dan menyimpan hasilnya.

Bereksperimenlah dengan opsi tambahan—seperti mengatur margin halaman atau menyematkan rumus workbook—untuk menyesuaikan output dengan alur kerja pelaporan Anda. Ketika Anda perlu menghasilkan laporan Word dari data Excel secara programatik, pendekatan ini memberikan solusi yang bersih dan mudah dipelihara.

--- 

*Siap mencobanya? Kloning contoh, perbarui jalur berkas, dan jalankan program. Jika Anda menemui masalah, lihat dokumentasi Aspose.Cells for Java atau jelajahi topik terkait di bawah ini.*  

### Topik terkait yang mungkin ingin Anda jelajahi selanjutnya

* **convert excel workbook to pdf** – menghasilkan laporan PDF dari workbook yang sama.  
* **Aspose.Cells chart formatting** – menyesuaikan warna, penanda, dan sumbu sebelum ekspor.  
* **Embedding images in DOCX with Aspose.Words** – menggabungkan diagram dengan konten Word lainnya.  

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automate Excel Chart Access Using Aspose.Cells Java: A Step‑by‑Step Guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}