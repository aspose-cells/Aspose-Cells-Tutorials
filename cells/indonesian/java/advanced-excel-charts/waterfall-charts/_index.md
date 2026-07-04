---
date: 2026-02-16
description: Pelajari cara mengatur rentang data diagram dan membuat diagram waterfall
  di Java menggunakan Aspose.Cells. Panduan langkah demi langkah untuk menambahkan
  diagram seri data, menyesuaikannya, dan mengekspor ke XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Atur Rentang Data Diagram – Aspose.Cells untuk Diagram Air Terjun Java
url: /id/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

  
**Tested With:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

Translate labels but keep dates.

Then closing shortcodes.

Now produce final content with all translations.

Be careful to keep markdown formatting exactly.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagram Waterfall

## Pengenalan Diagram Waterfall menggunakan Aspose.Cells untuk Java

Dalam tutorial ini Anda akan belajar cara **set chart data range** dan membuat **waterfall chart** dengan Aspose.Cells untuk Java. Diagram waterfall adalah alat penting dalam visualisasi data karena memungkinkan Anda melihat efek kumulatif dari serangkaian nilai positif dan negatif. Baik Anda menyiapkan laporan keuangan, laporan kinerja penjualan, atau analisis berbasis data lainnya, diagram waterfall dapat mengubah angka mentah menjadi wawasan yang jelas dan dapat ditindaklanjuti.

## Jawaban Cepat
- **Apa itu diagram waterfall?** Visual yang menunjukkan bagaimana nilai awal ditambah dan dikurangi oleh serangkaian nilai menengah, berakhir dengan total akhir.  
- **Perpustakaan mana yang digunakan?** Aspose.Cells untuk Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya menyimpan file sebagai XLSX?** Ya – gunakan `workbook.save("FileName.xlsx")`.  
- **Apakah cocok untuk visualisasi data Java?** Tentu saja; Aspose.Cells menyediakan fitur charting yang kaya tanpa perlu menginstal Office.

## Apa itu Diagram Waterfall?
Diagram waterfall menampilkan kontribusi positif dan negatif secara berurutan terhadap nilai awal, membantu Anda memahami bagaimana setiap komponen memengaruhi hasil keseluruhan.

## Mengapa Menggunakan Aspose.Cells untuk Java untuk Menambahkan Diagram Waterfall?
- **Tidak memerlukan Microsoft Excel** – menghasilkan chart di server mana pun atau pipeline CI.  
- **Kontrol penuh atas pemformatan** – warna, label data, dan sumbu dapat disesuaikan secara programatik.  
- **Mendukung banyak format output** – XLSX, PDF, HTML, dan lainnya.  
- **Kinerja tinggi** – ideal untuk workbook besar dan pelaporan otomatis.

## Prerequisites

Sebelum kita masuk ke kode, pastikan Anda telah menyiapkan hal‑hal berikut:

- Aspose.Cells untuk Java: Anda perlu menginstal Aspose.Cells untuk Java. Anda dapat mengunduhnya dari [here](https://releases.aspose.com/cells/java/).

- Lingkungan Pengembangan Java: Pastikan Java telah terinstal di sistem Anda.

Sekarang, mari kita mulai membuat diagram waterfall langkah demi langkah.

## Cara Menetapkan Rentang Data Diagram untuk Diagram Waterfall di Java

### Langkah 1: Impor Aspose.Cells

```java
import com.aspose.cells.*;
```

Pertama, Anda perlu mengimpor pustaka Aspose.Cells ke proyek Java Anda. Pustaka ini menyediakan fungsionalitas luas untuk bekerja dengan file Excel, termasuk pembuatan chart.

### Langkah 2: Inisialisasi Workbook dan Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Buat workbook baru dan tambahkan worksheet ke dalamnya. Kita akan menggunakan worksheet ini untuk memasukkan data dan **add chart to worksheet**.

### Langkah 3: Masukkan Data

Sekarang, mari isi worksheet dengan data yang ingin kita representasikan dalam diagram waterfall.

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

Dalam contoh ini, kita memiliki kategori di kolom A dan nilai yang bersesuaian di kolom B. Anda dapat mengganti data ini dengan dataset Anda sendiri.

### Langkah 4: Buat Diagram Waterfall

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Kami telah menambahkan diagram waterfall ke worksheet, menentukan seri data dan data kategori. Ini adalah langkah inti yang **adds waterfall chart** ke lembar Anda. Perhatikan bagaimana metode `add` menggunakan rentang `"B2:B6"` – inilah tempat kami **set chart data range** untuk seri. Anda dapat menyesuaikan tampilan chart lebih lanjut (warna, label data, dll.) menggunakan properti objek `Chart`.

### Langkah 5: Simpan Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Simpan workbook ke file. Contoh ini menggunakan format XLSX, tetapi Aspose.Cells juga memungkinkan Anda **export excel pdf java**‑compatible file seperti PDF, CSV, dan banyak format lainnya. Ini memenuhi persyaratan **save workbook xlsx**.

## Masalah Umum dan Solusinya

- **Chart muncul kosong** – Pastikan referensi rentang data (`B2:B6` dan `A2:A6`) cocok dengan sel yang berisi nilai dan kategori Anda.  
- **Nilai negatif tidak ditampilkan dengan benar** – Pastikan tipe seri diatur ke `ChartType.WATERFALL`; tipe chart lain memperlakukan nilai negatif secara berbeda.  
- **File tidak dapat dibuka di Excel** – Pastikan Anda menggunakan versi terbaru Aspose.Cells (rilis terbaru) dan ekstensi file sesuai dengan format (`.xlsx` untuk Excel).

## Pertanyaan yang Sering Diajukan

### Bagaimana saya dapat menyesuaikan tampilan diagram waterfall saya?

Anda dapat menyesuaikan tampilan diagram waterfall dengan memodifikasi properti seperti warna, label data, dan label sumbu. Lihat dokumentasi Aspose.Cells untuk panduan detail.

### Bisakah saya membuat beberapa diagram waterfall dalam worksheet yang sama?

Ya, Anda dapat membuat beberapa diagram waterfall dalam worksheet yang sama dengan mengikuti langkah yang sama menggunakan rentang data yang berbeda.

### Apakah Aspose.Cells kompatibel dengan berbagai lingkungan pengembangan Java?

Ya, Aspose.Cells untuk Java kompatibel dengan berbagai lingkungan pengembangan Java, termasuk Eclipse, IntelliJ IDEA, dan NetBeans.

### Bisakah saya menambahkan seri data tambahan ke diagram waterfall saya?

Tentu saja, Anda dapat menambahkan lebih banyak seri data ke diagram waterfall untuk merepresentasikan skenario data yang kompleks secara efektif. Ini adalah contoh bagaimana Anda dapat **add data series chart** secara programatik.

### Di mana saya dapat menemukan lebih banyak sumber daya dan contoh untuk Aspose.Cells untuk Java?

Anda dapat menjelajahi dokumentasi Aspose.Cells untuk Java di [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) untuk informasi mendalam dan contoh kode.

## FAQ

**Q: Bagaimana cara menetapkan rentang data chart untuk diagram waterfall keuangan?**  
A: Gunakan metode `add` pada seri chart, dengan memberikan rentang sel yang berisi nilai Anda, misalnya `"B2:B6"`.

**Q: Bisakah saya mengekspor workbook ke PDF alih-alih XLSX?**  
A: Ya, panggil `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` untuk output yang **export excel pdf java**‑compatible.

**Q: Bagaimana jika saya perlu membuat diagram waterfall keuangan dengan lebih banyak kategori?**  
A: Perluas rentang data di kolom nilai dan kolom kategori, lalu perbarui pemanggilan `add` dan `setCategoryData` sesuai.

**Q: Apakah ada cara untuk secara otomatis memformat batang positif dan negatif?**  
A: Anda dapat mengiterasi koleksi `Series` dan mengatur warna `FillFormat` berdasarkan tanda masing‑masing nilai.

**Q: Apakah Aspose.Cells mendukung pembaruan data dinamis untuk chart?**  
A: Ya, Anda dapat mengubah nilai sel setelah chart dibuat; chart akan mencerminkan perubahan tersebut saat workbook disimpan.

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells untuk Java (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}