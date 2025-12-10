---
date: 2025-12-10
description: Pelajari cara membuat diagram waterfall di Java menggunakan Aspose.Cells.
  Panduan langkah demi langkah untuk menambahkan diagram ke lembar kerja, menyesuaikannya,
  dan menyimpan buku kerja sebagai XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Cara Membuat Diagram Waterfall dengan Aspose.Cells untuk Java
url: /id/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagram Waterfall

## Pendahuluan Diagram Waterfall menggunakan Aspose.Cells untuk Java

Dalam tutorial ini Anda akan belajar cara **membuat diagram waterfall** dengan Aspose.Cells untuk Java. Diagram waterfall adalah alat penting dalam visualisasi data karena memungkinkan Anda melihat efek kumulatif dari serangkaian nilai positif dan negatif. Baik Anda sedang menyiapkan laporan keuangan, laporan kinerja penjualan, atau analisis berbasis data lainnya, diagram waterfall dapat mengubah angka mentah menjadi wawasan yang jelas dan dapat ditindaklanjuti.

## Jawaban Cepat
- **Apa itu diagram waterfall?** Visual yang menunjukkan bagaimana nilai awal ditambah dan dikurangi oleh serangkaian nilai menengah, berakhir dengan total akhir.  
- **Perpustakaan mana yang digunakan?** Aspose.Cells untuk Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya menyimpan file sebagai XLSX?** Ya – gunakan `workbook.save("FileName.xlsx")`.  
- **Apakah cocok untuk visualisasi data Java?** Tentu; Aspose.Cells menyediakan fitur charting lengkap tanpa perlu menginstal Office.

## Apa itu Diagram Waterfall?
Diagram waterfall menampilkan kontribusi positif dan negatif secara berurutan terhadap nilai awal, membantu Anda memahami bagaimana setiap komponen memengaruhi hasil keseluruhan.

## Mengapa Menggunakan Aspose.Cells untuk Java untuk Menambahkan Diagram Waterfall?
- **Tidak memerlukan Microsoft Excel** – menghasilkan diagram di server mana pun atau pipeline CI.  
- **Kontrol penuh atas format** – warna, label data, dan sumbu dapat disesuaikan secara programatik.  
- **Mendukung banyak format output** – XLSX, PDF, HTML, dan lainnya.  
- **Kinerja tinggi** – ideal untuk workbook besar dan pelaporan otomatis.

## Prasyarat

Sebelum kita masuk ke kode, pastikan Anda telah menyiapkan prasyarat berikut:

- Aspose.Cells untuk Java: Anda perlu menginstal Aspose.Cells untuk Java. Unduh dari [here](https://releases.aspose.com/cells/java/).

- Lingkungan Pengembangan Java: Pastikan Java telah terpasang di sistem Anda.

Sekarang, mari kita mulai membuat diagram waterfall langkah demi langkah.

## Cara Membuat Diagram Waterfall di Java

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

Buat workbook baru dan tambahkan worksheet ke dalamnya. Kita akan menggunakan worksheet ini untuk memasukkan data dan **menambahkan chart ke worksheet**.

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

Dalam contoh ini, kami memiliki kategori di kolom A dan nilai yang bersesuaian di kolom B. Anda dapat mengganti data ini dengan dataset Anda sendiri.

### Langkah 4: Buat Diagram Waterfall

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Kami telah menambahkan diagram waterfall ke worksheet, menentukan seri data dan data kategori. Ini adalah langkah inti yang **menambahkan diagram waterfall** ke lembar Anda. Anda dapat menyesuaikan tampilan chart lebih lanjut (warna, label data, dll.) menggunakan properti objek `Chart`.

### Langkah 5: Simpan Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Simpan workbook ke file. Contoh ini menggunakan format XLSX, tetapi Aspose.Cells juga memungkinkan Anda mengekspor ke PDF, CSV, dan banyak format lainnya. Ini memenuhi persyaratan **save workbook xlsx**.

## Masalah Umum dan Solusinya

- **Chart muncul kosong** – Pastikan referensi rentang data (`B2:B6` dan `A2:A6`) sesuai dengan sel yang berisi nilai dan kategori Anda.  
- **Nilai negatif tidak ditampilkan dengan benar** – Pastikan tipe seri diatur ke `ChartType.WATERFALL`; tipe chart lain memperlakukan nilai negatif secara berbeda.  
- **File tidak dapat dibuka di Excel** – Pastikan Anda menggunakan versi terbaru Aspose.Cells (rilis terbaru) dan ekstensi file cocok dengan format (`.xlsx` untuk Excel).

## Pertanyaan yang Sering Diajukan

### Bagaimana saya dapat menyesuaikan tampilan diagram waterfall saya?

Anda dapat menyesuaikan tampilan diagram waterfall dengan memodifikasi properti seperti warna, label data, dan label sumbu. Lihat dokumentasi Aspose.Cells untuk panduan detail.

### Bisakah saya membuat beberapa diagram waterfall dalam worksheet yang sama?

Ya, Anda dapat membuat beberapa diagram waterfall dalam worksheet yang sama dengan mengikuti langkah yang sama menggunakan rentang data yang berbeda.

### Apakah Aspose.Cells kompatibel dengan berbagai lingkungan pengembangan Java?

Ya, Aspose.Cells untuk Java kompatibel dengan berbagai lingkungan pengembangan Java, termasuk Eclipse, IntelliJ IDEA, dan NetBeans.

### Bisakah saya menambahkan seri data tambahan ke diagram waterfall saya?

Tentu, Anda dapat menambahkan lebih banyak seri data ke diagram waterfall untuk merepresentasikan skenario data yang kompleks secara efektif.

### Di mana saya dapat menemukan lebih banyak sumber daya dan contoh untuk Aspose.Cells untuk Java?

Anda dapat menjelajahi dokumentasi Aspose.Cells untuk Java di [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) untuk informasi mendalam dan contoh kode.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.Cells untuk Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}