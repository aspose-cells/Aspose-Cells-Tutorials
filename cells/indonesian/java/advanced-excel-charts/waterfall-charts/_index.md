---
date: 2026-09-02
description: Pelajari cara membuat excel waterfall chart di Java dengan Aspose.Cells,
  atur chart data range, sesuaikan data labels, dan export ke XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Waterfall Charts
og_description: Buat excel waterfall chart menggunakan Aspose.Cells untuk Java – atur
  chart data range, tambahkan data labels, dan export ke XLSX dalam beberapa langkah.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Buat excel waterfall chart dengan Aspose.Cells untuk Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Buat excel waterfall chart dengan Aspose.Cells untuk Java
url: /id/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagram Air Terjun

## Pengenalan diagram air terjun menggunakan Aspose.Cells untuk Java

Dalam tutorial ini Anda akan belajar cara **membuat diagram air terjun Excel** dan **mengatur rentang data diagram** dengan Aspose.Cells untuk Java. Diagram air terjun mengubah serangkaian angka positif dan negatif menjadi cerita visual yang jelas, menjadikannya ideal untuk laporan keuangan, tinjauan kinerja penjualan, dan skenario apa pun di mana Anda perlu melihat bagaimana item individu berkontribusi pada total.

## Jawaban Cepat
- **Apa itu diagram air terjun?** Visual yang menunjukkan bagaimana nilai awal ditambah dan dikurangi oleh serangkaian nilai menengah, berakhir dengan total akhir.  
- **Perpustakaan mana yang digunakan?** Aspose.Cells untuk Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya menyimpan file sebagai XLSX?** Ya – gunakan `workbook.save("FileName.xlsx")`.  
- **Apakah cocok untuk visualisasi data Java?** Tentu saja; Aspose.Cells menyediakan fitur charting yang kaya tanpa perlu menginstal Office.

## Apa itu diagram air terjun?
Diagram air terjun menampilkan kontribusi positif dan negatif secara berurutan ke nilai awal, membantu Anda memahami bagaimana setiap komponen memengaruhi hasil keseluruhan. Dengan memvisualisasikan keuntungan dan kerugian berdampingan, diagram ini membuat aliran keuangan yang kompleks menjadi mudah dibaca.

## Mengapa menggunakan Aspose.Cells untuk Java untuk menambahkan diagram air terjun?
Aspose.Cells memungkinkan Anda menghasilkan diagram Excel di server mana pun, pipeline CI, atau desktop tanpa memerlukan Microsoft Excel. Ia mendukung **lebih dari 15 format output** (XLSX, PDF, HTML, CSV, dan lainnya), memproses workbook dengan **lebih dari 500 baris** dalam kurang dari satu detik, dan memberikan kontrol programatik atas setiap elemen diagram—dari warna hingga label data.

## Prasyarat

Sebelum kita menyelam ke kode, pastikan Anda memiliki prasyarat berikut:

- Aspose.Cells untuk Java: Anda perlu menginstal Aspose.Cells untuk Java. Anda dapat mengunduhnya dari halaman rilis Aspose.Cells untuk Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Lingkungan pengembangan Java: Pastikan Java terinstal di sistem Anda dan alat build (Maven/Gradle) siap.

Sekarang, mari kita mulai membuat diagram air terjun langkah demi langkah.

## Cara mengatur rentang data diagram air terjun di Java
Muat workbook baru, isi dengan data, tambahkan objek `Chart`, definisikan rentang seri, dan akhirnya simpan file. Proses ini sederhana: Anda membuat workbook, mengisi sel dengan kategori dan nilai, membuat diagram, mengikat rentang data, lalu mengekspor workbook. Hasilnya adalah diagram air terjun yang berfungsi penuh siap digunakan dalam laporan atau dasbor.

### Langkah 1: impor Aspose.Cells
Paket `com.aspose.cells` berisi semua kelas yang diperlukan untuk manipulasi Excel, termasuk pembuatan workbook, penanganan worksheet, dan pembuatan diagram.

### Langkah 2: inisialisasi workbook dan worksheet
**Workbook** mewakili file Excel, dan **Worksheet** adalah lembar tunggal di dalam file tersebut. Membuat objek-objek ini menyediakan kanvas untuk data mentah dan diagram.

### Langkah 3: masukkan data
Kolom A berisi label kategori, sementara kolom B berisi nilai numerik untuk diagram air terjun. Tata letak ini cocok dengan alur laba‑rugi tipikal yang digunakan dalam analisis keuangan.

### Langkah 4: buat diagram air terjun
Objek **Chart** membuat representasi visual; mengatur tipenya ke `ChartType.WATERFALL` mengkonfigurasikannya sebagai diagram air terjun. Gunakan metode `add` untuk mengatur rentang data diagram untuk seri (`"B2:B6"`), dan hubungkan sumbu kategori ke `"A2:A6"`.

### Langkah 5: simpan workbook
Menyimpan workbook menuliskan diagram dan data ke format file yang ditentukan. Panggil `workbook.save("WaterfallChart.xlsx")` untuk menghasilkan file XLSX, atau ubah parameter format untuk mengekspor ke PDF, CSV, atau HTML.

## Masalah umum dan solusi

- **Diagram muncul kosong** – Pastikan referensi rentang data (`B2:B6` dan `A2:A6`) sesuai dengan sel yang berisi nilai dan kategori Anda.  
- **Nilai negatif tidak ditampilkan dengan benar** – Pastikan tipe seri diatur ke `ChartType.WATERFALL`; tipe diagram lain memperlakukan nilai negatif secara berbeda.  
- **File tidak dapat dibuka di Excel** – Gunakan rilis Aspose.Cells terbaru dan pastikan ekstensi file cocok dengan format (`.xlsx` untuk Excel).

## Pertanyaan yang Sering Diajukan

### Bagaimana saya dapat menyesuaikan tampilan diagram air terjun saya?
Anda dapat memodifikasi properti seperti `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` untuk mengubah warna batang, mengaktifkan label data dengan `setShowDataLabels(true)`, dan menyesuaikan judul sumbu melalui `getCategoryAxis().setTitle("Stage")`. Referensi API Aspose.Cells menyediakan daftar lengkap opsi yang dapat disesuaikan.

### Bisakah saya membuat beberapa diagram air terjun dalam worksheet yang sama?
Ya. Setelah menambahkan diagram pertama, ulangi langkah pembuatan diagram dengan rentang data berbeda dan objek `Chart` baru. Setiap diagram bersifat independen dan dapat diposisikan di mana saja pada lembar.

### Apakah Aspose.Cells kompatibel dengan berbagai lingkungan pengembangan Java?
Tentu saja. Perpustakaan ini bekerja dengan Eclipse, IntelliJ IDEA, NetBeans, dan sistem build apa pun yang mendukung Maven atau Gradle. Tidak diperlukan plugin tambahan.

### Bisakah saya menambahkan seri data tambahan ke diagram air terjun saya?
Anda dapat menambahkan lebih banyak seri dengan memanggil `chart.getNSeries().add("C2:C6", true)` dan mengkonfigurasi setiap seri secara terpisah. Ini memungkinkan Anda membandingkan beberapa skenario berdampingan.

### Di mana saya dapat menemukan lebih banyak sumber daya dan contoh untuk Aspose.Cells untuk Java?
Jelajahi dokumentasi lengkap di referensi API Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q: Bagaimana cara mengatur rentang data diagram air terjun keuangan?**  
A: Gunakan metode `add` pada seri diagram, dengan memberikan rentang sel yang berisi nilai Anda, misalnya `"B2:B6"`.

**Q: Bisakah saya mengekspor workbook ke PDF alih-alih XLSX?**  
A: Ya, panggil `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` untuk menghasilkan versi PDF.

**Q: Bagaimana jika saya perlu membuat diagram air terjun dengan lebih banyak kategori?**  
A: Perluas rentang data di kedua kolom nilai dan kategori, lalu perbarui pemanggilan `add` dan `setCategoryData` sesuai.

**Q: Apakah ada cara untuk secara otomatis memformat batang positif dan negatif?**  
A: Iterasi melalui koleksi `Series` dan atur warna `FillFormat` berdasarkan tanda masing‑masing nilai; Aspose.Cells memungkinkan Anda menerapkan pemformatan bersyarat secara programatik.

**Q: Apakah Aspose.Cells mendukung pembaruan data dinamis untuk diagram?**  
A: Ya. Setelah memodifikasi nilai sel, cukup simpan kembali workbook—diagram akan secara otomatis mencerminkan data baru.

---

**Terakhir Diperbarui:** 2026-09-02  
**Diuji dengan:** Aspose.Cells untuk Java (terbaru)  
**Penulis:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Tutorial Terkait

- [Sesuaikan Label Data Diagram Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Tambahkan Label Data ke Diagram Excel dengan Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Cara Membuat dan Mengekspor Diagram di Java Menggunakan Aspose.Cells: Panduan Lengkap](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}