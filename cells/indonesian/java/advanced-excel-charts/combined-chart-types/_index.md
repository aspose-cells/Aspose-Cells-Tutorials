---
date: 2026-09-02
description: Pelajari cara mengekspor diagram ke PNG, menambahkan seri data, menggabungkan
  diagram garis dan kolom, menyimpan buku kerja sebagai XLSX, dan menambahkan legenda
  diagram menggunakan Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Ekspor diagram ke PNG dan tambahkan seri data untuk diagram gabungan
og_description: Ekspor diagram ke PNG dengan Aspose.Cells for Java, gabungkan diagram
  garis dan kolom, tambahkan seri data, dan simpan buku kerja sebagai XLSX dalam satu
  tutorial.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Ekspor diagram ke PNG dan tambahkan seri data untuk diagram gabungan
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Ekspor diagram ke PNG dan tambahkan seri data untuk diagram gabungan
url: /id/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor diagram ke PNG dan tambahkan seri data untuk diagram gabungan

Dalam tutorial ini Anda akan **menambahkan seri data** ke buku kerja Excel, **menggabungkan elemen diagram garis dan kolom**, dan mempelajari cara **mengekspor diagram ke PNG** menggunakan Aspose.Cells for Java. Kami akan membimbing Anda melalui setiap langkah—dari menyiapkan buku kerja, menambahkan diagram ke lembar kerja, menyesuaikan legenda, hingga **menyimpan buku kerja sebagai XLSX** dan menghasilkan gambar PNG dari diagram. Pada akhir tutorial, Anda akan memiliki diagram gabungan yang siap‑pakai yang dapat Anda sematkan dalam laporan atau dasbor.

## Jawaban Cepat
- **Perpustakaan mana yang membuat diagram gabungan?** Aspose.Cells for Java.  
- **Bagaimana cara menambahkan seri data?** Call `chart.getNSeries().add(...)` with the appropriate range.  
- **Bagaimana cara mengekspor diagram ke PNG?** Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Format file apa yang dapat saya simpan untuk buku kerja?** Standard `.xlsx` (save workbook as XLSX).  
- **Apakah saya memerlukan lisensi untuk produksi?** Yes – a valid Aspose.Cells license is required for production deployments.

## Apa itu ekspor diagram ke PNG di Aspose.Cells?
Mengekspor diagram ke PNG membuat gambar raster dari diagram Excel yang dapat ditampilkan di halaman web, laporan, atau email tanpa memerlukan aplikasi Excel. Metode ini menangkap tata letak visual, warna, dan penanda data secara tepat, menghasilkan file gambar yang dapat dipindahkan.

## Mengapa membuat diagram garis‑kolom gabungan?
Diagram garis‑kolom gabungan memungkinkan Anda menampilkan kumpulan data yang berbeda dengan representasi visual yang berbeda (misalnya, seri garis di atas seri kolom) dalam satu tampilan. Pendekatan ini ideal untuk membandingkan tren terhadap total, menyoroti korelasi, atau memberikan wawasan yang lebih kaya sambil menjaga jejak visual tetap kecil.

## Prasyarat
- Java Development Kit (JDK) 8 atau lebih tinggi  
- Perpustakaan Aspose.Cells for Java (unduh dari tautan di bawah)  
- Familiaritas dasar dengan sintaks Java dan konsep Excel  

## Memulai

Pertama, unduh perpustakaan Aspose.Cells for Java dari situs resmi:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Setelah JAR ditambahkan ke classpath proyek Anda, Anda dapat mulai membangun diagram.

### Langkah 1: impor kelas aspose.cells
`Workbook` adalah objek inti Aspose.Cells yang mewakili seluruh file Excel dalam memori.  
```java
import com.aspose.cells.*;
```

### Langkah 2: buat buku kerja baru
`Worksheet` mewakili satu lembar dalam sebuah `Workbook` dan menyediakan akses ke sel, baris, dan diagram.  
```java
Workbook workbook = new Workbook();
```

### Langkah 3: akses lembar kerja pertama
`Chart` adalah objek yang menyimpan semua pengaturan terkait diagram, seri, dan opsi rendering.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Langkah 4: tambahkan objek diagram gabungan ke lembar kerja  
Kami akan memulai dengan diagram garis dan kemudian menambahkan seri kolom untuk mencapai efek **diagram garis‑kolom gabungan**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Menambahkan data ke diagram

Sekarang kontainer diagram sudah ada, kita perlu mengisinya dengan data.

### Langkah 5: definisikan rentang data dan tambahkan seri data
`NSeries` adalah koleksi yang menyimpan setiap seri data untuk sebuah diagram. Menambahkan seri menghubungkan rentang sel ke diagram.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Parameter pertama (`"A1:A5"`) adalah rentang untuk seri pertama, dan yang kedua (`"B1:B5"`) membuat seri kedua yang akan digabungkan dengan yang pertama.

### Langkah 6: atur data kategori (sumbu X)
`CategoryAxis` mewakili sumbu horizontal diagram, mengontrol label yang ditampilkan sepanjang sumbu X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Menyesuaikan diagram

Diagram yang baik menceritakan sebuah cerita. Mari beri judul, label sumbu, dan legenda yang jelas.

### Langkah 7: atur label sumbu diagram dan judul
`Title` menetapkan judul utama diagram, dan objek `Axis` mewakili sumbu X dan Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Langkah 8: tambahkan legenda diagram dan sesuaikan posisinya
`Legend` mengontrol penempatan dan tampilan legenda seri dalam diagram.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Menyimpan dan mengekspor diagram

Setelah menyesuaikan, Anda ingin **menyimpan buku kerja sebagai XLSX** dan juga menghasilkan gambar.

### Langkah 9: simpan buku kerja sebagai file Excel (XLSX)
`Workbook.save` menulis buku kerja dalam memori ke file dalam format yang ditentukan.  
```java
workbook.save("CombinedChart.xlsx");
```

### Langkah 10: ekspor diagram ke PNG
`Chart.toImage` merender diagram sebagai file gambar dalam format yang dipilih.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metode `chart.toImage` **menghasilkan gambar diagram Excel** yang dapat digunakan di halaman web, laporan, atau email.

## Masalah umum & pemecahan masalah

| Masalah | Solusi |
|-------|----------|
| **Tidak ada data muncul** | Verifikasi bahwa rentang sel (`A1:A5`, `B1:B5`, `C1:C5`) memang berisi data sebelum membuat diagram. |
| **Legenda menutupi diagram** | Setel `chart.getLegend().setOverlay(false)` atau pindahkan legenda ke posisi lain (mis., `RIGHT`). |
| **File gambar kosong** | Pastikan diagram memiliki setidaknya satu seri dan bahwa `chart.toImage` dipanggil setelah semua penyesuaian. |
| **Penyimpanan menghasilkan pengecualian** | Periksa bahwa Anda memiliki izin menulis ke direktori target dan bahwa file tidak terbuka di Excel. |

## Pertanyaan yang sering diajukan

**Q: Bagaimana cara menginstal Aspose.Cells for Java?**  
A: Unduh JAR dari situs resmi dan tambahkan ke classpath proyek Anda. Tautan unduhan adalah: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Bisakah saya membuat tipe diagram lain selain garis dan kolom?**  
A: Ya, Aspose.Cells mendukung diagram batang, pai, sebar, area, dan banyak tipe diagram lainnya. Lihat dokumentasi API untuk daftar lengkap.

**Q: Apakah lisensi diperlukan untuk penggunaan produksi?**  
A: Lisensi Aspose.Cells yang valid diperlukan untuk penyebaran produksi. Versi percobaan gratis tersedia untuk evaluasi.

**Q: Bagaimana cara mengubah warna setiap seri?**  
A: Gunakan `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (atau serupa) setelah menambahkan seri.

**Q: Di mana saya dapat menemukan contoh kode lebih banyak?**  
A: Dokumentasi lengkap dan contoh tambahan tersedia di situs referensi Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Terakhir diperbarui:** 2026-09-02  
**Diuji dengan:** Aspose.Cells for Java versi terbaru  
**Penulis:** Aspose

## Tutorial Terkait

- [Cara Menambahkan Label ke Diagram Excel Menggunakan Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Cara Membuat Diagram Excel dengan Garis Tren dan Mengekspor ke Gambar menggunakan Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Ekspor Diagram Excel ke PDF Menggunakan Aspose.Cells for Java: Panduan Ukuran Halaman Kustom](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}