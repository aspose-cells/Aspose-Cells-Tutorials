---
date: '2026-06-12'
description: Pelajari cara mengekspor grafik ke PNG dengan Aspose.Cells Java, menghasilkan
  gambar grafik, merender grafik Excel sebagai PNG, dan menyesuaikan visualisasi secara
  efisien.
keywords:
- export chart to png
- java generate chart image
- render excel chart image
- java chart visualization library
- Aspose.Cells Java
schemas:
- author: Aspose
  dateModified: '2026-06-12'
  description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  headline: Export chart to PNG using Aspose.Cells Java
  type: TechArticle
- description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  name: Export chart to PNG using Aspose.Cells Java
  steps:
  - name: Verify that **JDK 8** or newer is on your `PATH`.
    text: Verify that **JDK 8** or newer is on your `PATH`.
  - name: Open your preferred IDE and create a new Maven/Gradle Java project.
    text: Open your preferred IDE and create a new Maven/Gradle Java project.
  - name: Add the Aspose.Cells dependency using the snippets above.
    text: Add the Aspose.Cells dependency using the snippets above.
  - name: Add the Maven or Gradle dependency as shown earlier.
    text: Add the Maven or Gradle dependency as shown earlier.
  - name: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
    text: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
  - name: 'Load the license at runtime:'
    text: 'Load the license at runtime:'
  type: HowTo
- questions:
  - answer: Place the `Aspose.Cells.lic` file in the resources folder and load it
      with `License license = new License(); license.setLicense("Aspose.Cells.lic");`.
    question: How do I resolve license activation issues?
  - answer: Yes, it integrates seamlessly with Spring Boot, Jakarta EE, or any servlet
      container.
    question: Can I use Aspose.Cells for Java in a web application?
  - answer: Forgetting to update the source data before calling `calculate()` leads
      to stale visuals.
    question: What are common pitfalls when refreshing charts?
  - answer: Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` and process
      worksheets in streams.
    question: How do I handle large Excel files efficiently?
  - answer: PNG, JPEG, BMP, and TIFF are fully supported; choose PNG for loss‑less
      quality.
    question: What image formats are supported for rendering charts?
  type: FAQPage
title: Ekspor grafik ke PNG menggunakan Aspose.Cells Java
url: /id/java/charts-graphs/aspose-cells-java-load-customize-excel-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor diagram ke PNG menggunakan Aspose.Cells Java

## Pendahuluan

Mengekspor diagram ke PNG adalah kebutuhan umum ketika Anda perlu menyisipkan data visual dalam laporan, presentasi, atau halaman web. Dengan **Aspose.Cells for Java**, Anda dapat memuat workbook Excel yang ada, memperbarui data diagram, menerapkan pengaturan globalisasi, dan merender diagram langsung sebagai gambar PNG berkualitas tinggi—semua tanpa harus menginstal Microsoft Excel. Dalam tutorial ini Anda akan mempelajari cara **mengekspor diagram ke PNG**, menghasilkan gambar diagram secara programatik, dan menyesuaikan output untuk audiens global.

## Jawaban Cepat
- **Bagaimana cara mengekspor diagram ke PNG?** Muat workbook, akses diagram, dan panggil `chart.toImage()` dengan `ImageOrPrintOptions` yang disetel ke PNG.  
- **Perpustakaan mana yang mendukung pembuatan gambar diagram di Java?** Aspose.Cells for Java menyediakan API lengkap untuk merender diagram Excel sebagai gambar.  
- **Apakah saya memerlukan lisensi untuk ekspor PNG?** Versi percobaan gratis berfungsi, tetapi lisensi komersial menghapus batas evaluasi.  
- **Bisakah saya menyesuaikan format angka secara global?** Ya, gunakan `Workbook.getSettings().setGlobalizationSettings()` sebelum merender.  
- **Apakah PNG satu‑satunya format?** Tidak, Anda juga dapat merender ke JPEG, BMP, atau TIFF dengan mengubah opsi format gambar.

## Apa itu Aspose.Cells for Java?
`Aspose.Cells for Java` adalah **perpustakaan pemrosesan spreadsheet berbasis Java** yang memungkinkan pengembang membuat, memodifikasi, mengonversi, dan merender file Excel tanpa Microsoft Office. Ia mendukung lebih dari 50 format file, menangani workbook dengan ribuan baris, dan dapat merender diagram ke gambar dalam waktu kurang dari satu detik pada perangkat keras server tipikal.

## Mengapa mengekspor diagram ke PNG dengan Aspose.Cells?
Mengekspor diagram ke PNG dengan Aspose.Cells memberikan kinerja tinggi, penggunaan memori rendah, dan fleksibilitas format sambil menghilangkan kebutuhan akan Microsoft Excel. Perpustakaan ini merender diagram dalam kurang dari satu detik, menjaga penggunaan heap tetap wajar, dan mendukung PNG, JPEG, BMP, serta TIFF, menjadikannya ideal untuk web, cetak, dan penyebaran lintas platform.

## Prasyarat

- **Aspose.Cells for Java** v25.3 (atau lebih baru).  
- **JDK 8+** terpasang pada mesin pengembangan Anda.  
- **IDE** seperti IntelliJ IDEA atau Eclipse.  
- **Maven atau Gradle** untuk manajemen dependensi.  

### Perpustakaan dan Dependensi yang Diperlukan

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Penyiapan Lingkungan

1. Pastikan **JDK 8** atau yang lebih baru ada di `PATH` Anda.  
2. Buka IDE pilihan Anda dan buat proyek Java Maven/Gradle baru.  
3. Tambahkan dependensi Aspose.Cells menggunakan cuplikan di atas.  

### Akuisisi Lisensi

Aspose.Cells menawarkan percobaan gratis untuk mengevaluasi fiturnya:

- [Download Free Trial](https://releases.aspose.com/cells/java/)  
- Untuk penggunaan produksi, beli lisensi di [Purchase Aspose.Cells](https://purchase.aspose.com/buy).  
- Lisensi sementara dapat diminta untuk pengujian yang diperpanjang.

## Menyiapkan Aspose.Cells for Java

Setelah lingkungan Anda siap, inisialisasi Aspose.Cells dalam proyek Anda:

1. Tambahkan dependensi Maven atau Gradle seperti yang ditunjukkan sebelumnya.  
2. Letakkan file lisensi Anda (`Aspose.Cells.lic`) di folder resources proyek.  
3. Muat lisensi pada runtime:

```java
   License license = new License();
   license.setLicense("path/to/Aspose.Total.Java.lic");
   ```  

## Panduan Implementasi

Kami akan membahas tiga skenario inti: memuat & memperbarui diagram, menyesuaikan pengaturan globalisasi, dan merender diagram ke PNG.

### Cara mengekspor diagram ke PNG dengan Aspose.Cells Java?

Untuk mengekspor diagram ke PNG dengan Aspose.Cells for Java, pertama muat workbook menggunakan kelas `Workbook`, kemudian ambil objek `Chart` yang diinginkan dari lembar kerja yang sesuai. Konfigurasikan `ImageOrPrintOptions` untuk menetapkan format gambar ke PNG, dan akhirnya panggil `chart.toImage(outputStream, options)`. Stream yang dihasilkan berisi PNG berkualitas tinggi yang dapat disimpan atau dikirim langsung ke klien.

### Memuat dan Menyegarkan Diagram dari File Excel

**Ikhtisar**: Muat workbook yang ada, pastikan diagram mencerminkan data terbaru, dan siapkan untuk merender.

#### 1. Muat Workbook  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  
*Definition anchor*: Kelas `Workbook` mewakili seluruh file Excel dalam memori, menyediakan akses ke lembar kerja, diagram, dan sel.

#### 2. Akses Worksheet dan Diagram  
```java
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
```  
*Definition anchor*: Objek `Worksheet` memberi Anda akses baris/kolom, sementara objek `Chart` mengenkapsulasi semua properti khusus diagram.

#### 3. Segarkan Diagram  
```java
chart.calculate();
```  
Pemanggilan `calculate()` memaksa diagram menghitung ulang serinya berdasarkan data sumber yang berubah, menjamin akurasi visual.

### Menyesuaikan Pengaturan Globalisasi untuk Diagram

**Ikhtisar**: Sesuaikan format tanggal, waktu, dan angka agar sesuai dengan konvensi regional sebelum merender.

#### 1. Muat Workbook  
```java
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  

#### 2. Tetapkan Pengaturan Globalisasi Kustom  
```java
CustomSettings customGlobalizationSettings = new CustomSettings();
customGlobalizationSettings.setChartSettings(new CustomChartGlobalizationSettings());
book.getSettings().setGlobalizationSettings(customGlobalizationSettings);
```  
Anda dapat menentukan pola khusus locale seperti `"dd-MMM-yyyy"` untuk tanggal atau `"#,##0.00"` untuk angka, memastikan PNG yang diekspor menghormati standar lokal.

### Merender Diagram ke Gambar

**Ikhtisar**: Konversi diagram yang telah disegarkan menjadi file PNG yang dapat digunakan dalam presentasi, PDF, atau halaman web.

#### 1. Muat Workbook dan Akses Diagram  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
chart.calculate();
```  

#### 2. Merender ke Gambar  
```java
ImageOrPrintOptions options = new ImageOrPrintOptions();
chart.toImage(outDir + "CustomTextforOtherLabelofPieChart_out.png", options);
```  
Metode `toImage()` menulis diagram ke `java.io.OutputStream`. Dengan mengatur `ImageOrPrintOptions.setImageFormat(ImageFormat.png)`, Anda memperoleh file PNG yang tajam.

## Aplikasi Praktis

- **Laporan Bisnis** – Sisipkan diagram PNG dalam dokumen PDF atau Word untuk distribusi kepada pemangku kepentingan.  
- **Dasbor Data** – Segarkan diagram secara dinamis saat data baru tiba, lalu render ke PNG untuk pengiriman web yang cepat.  
- **Kepatuhan Global** – Terapkan format angka dan tanggal spesifik locale untuk memenuhi persyaratan regulasi regional.

## Pertimbangan Kinerja

- **Manajemen Memori**: Gunakan `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` untuk file besar.  
- **Segarkan Selektif**: Panggil `chart.calculate()` hanya pada diagram yang data sumbernya berubah.  
- **Keamanan Thread**: Buat instance `Workbook` terpisah per thread untuk menghindari masalah konkruensi.

## Masalah Umum dan Solusinya

| Masalah | Solusi |
|-------|----------|
| Lisensi tidak ditemukan | Verifikasi jalur `Aspose.Cells.lic` dan pastikan berada di classpath. |
| Output PNG kosong | Pastikan diagram tidak disembunyikan dan `calculate()` telah dipanggil sebelum merender. |
| Rendering lambat pada file besar | Aktifkan `MemorySetting.MEMORY_PREFERENCE` dan render hanya lembar kerja yang diperlukan. |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara mengatasi masalah aktivasi lisensi?**  
J: Letakkan file `Aspose.Cells.lic` di folder resources dan muat dengan `License license = new License(); license.setLicense("Aspose.Cells.lic");`.

**T: Bisakah saya menggunakan Aspose.Cells for Java dalam aplikasi web?**  
J: Ya, ia terintegrasi mulus dengan Spring Boot, Jakarta EE, atau kontainer servlet apa pun.

**T: Apa jebakan umum saat menyegarkan diagram?**  
J: Lupa memperbarui data sumber sebelum memanggil `calculate()` menghasilkan visual yang usang.

**T: Bagaimana cara menangani file Excel besar secara efisien?**  
J: Gunakan `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` dan proses lembar kerja dalam aliran.

**T: Format gambar apa yang didukung untuk merender diagram?**  
J: PNG, JPEG, BMP, dan TIFF semuanya didukung penuh; pilih PNG untuk kualitas tanpa kehilangan.

## Sumber Daya

- **Dokumentasi**: [Aspose.Cells Java API](https://reference.aspose.com/cells/java/)  
- **Unduhan**: [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
- **Pembelian dan Lisensi**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Percobaan Gratis**: [Get a Free Trial of Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **Lisensi Sementara**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Dukungan dan Forum**: [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

Dengan menguasai langkah‑langkah ini, Anda dapat dengan andal **mengekspor diagram ke PNG** dan mengintegrasikan visualisasi berkualitas tinggi ke dalam solusi berbasis Java apa pun.

---

**Terakhir Diperbarui:** 2026-06-12  
**Diuji Dengan:** Aspose.Cells 25.3 untuk Java  
**Penulis:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial Terkait

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java: Custom Page Sizes Guide](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [How to Customize Excel Charts with Theme Colors Using Aspose.Cells Java](/cells/java/charts-graphs/customize-excel-charts-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```text
// Direct answer (no code block needed here as per preservation rules)
```