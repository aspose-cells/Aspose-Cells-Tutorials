---
date: 2025-12-01
description: Pelajari cara mengubah jenis grafik Excel dan menambahkan fitur interaktif
  seperti tooltip, label data, dan drill‑down menggunakan Aspose.Cells untuk Java.
language: id
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Ubah jenis diagram Excel dan tambahkan interaktivitas – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Tipe Diagram Excel dan Tambahkan Interaktivitas

## Introduction

Diagram interaktif memungkinkan audiens Anda menjelajahi data secara langsung, sementara kemampuan untuk **change Excel chart type** memberi Anda fleksibilitas untuk menyajikan informasi dalam format visual yang paling efektif. Dalam tutorial ini Anda akan belajar cara menggunakan Aspose.Cells for Java untuk mengubah tipe diagram, menambahkan tooltip, menyematkan label data, dan bahkan membuat tautan drill‑down — semua tanpa meninggalkan kode Java Anda. Pada akhir tutorial, Anda akan memiliki workbook Excel interaktif yang lengkap, yang dapat Anda sematkan dalam laporan, dasbor, atau aplikasi web.

## Quick Answers
- **Bisakah saya mengubah tipe diagram secara programatis?** Ya – gunakan enum `ChartType` saat membuat atau memperbarui diagram.  
- **Bagaimana cara menambahkan tooltip ke diagram?** Aktifkan label data dan setel `ShowValue` ke true.  
- **Apa cara termudah untuk menambahkan tautan drill‑down?** Lampirkan hyperlink ke titik data melalui `getHyperlinks().add(url)`.  
- **Apakah saya memerlukan lisensi untuk Aspose.Cells?** Versi percobaan gratis cukup untuk pengembangan; lisensi diperlukan untuk produksi.  
- **Versi Java mana yang didukung?** Java 8 ke atas didukung sepenuhnya.

## What is “change Excel chart type”?

Mengubah tipe diagram berarti mengganti representasi visual (misalnya, dari diagram kolom ke diagram garis) sambil mempertahankan data dasar tetap utuh. Ini berguna ketika Anda menemukan bahwa diagram lain lebih baik dalam menyampaikan tren, perbandingan, atau distribusi.

## Why add interactivity to Excel charts?

- **Insight data yang lebih baik:** Tooltip dan label data memungkinkan pengguna melihat nilai tepat tanpa menggulir.  
- **Presentasi yang menarik:** Elemen interaktif membuat penonton tetap tertarik.  
- **Kemampuan drill‑down:** Hyperlink memungkinkan pengguna melompat ke lembar kerja terperinci atau sumber eksternal.  
- **Aset yang dapat digunakan kembali:** Satu workbook dapat melayani berbagai skenario pelaporan hanya dengan mengganti tipe diagram.

## Prerequisites

- Lingkungan Pengembangan Java (JDK 8+)  
- Aspose.Cells for Java library (download from [here](https://releases.aspose.com/cells/java/))  
- File Excel contoh (`data.xlsx`) yang berisi data yang ingin Anda visualisasikan

## Step‑by‑step guide

### Step 1: Set up your Java project

1. Buat proyek Java baru di IDE favorit Anda (IntelliJ IDEA, Eclipse, VS Code, dll.).  
2. Tambahkan JAR Aspose.Cells ke classpath proyek Anda.

### Step 2: Load the source workbook

Kita mulai dengan memuat workbook yang sudah ada yang berisi data untuk diagram kita.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Step 3: Create a chart and **change its type**

Di bawah ini kami membuat diagram kolom, kemudian langsung menunjukkan cara Anda dapat mengubahnya menjadi diagram garis jika diperlukan.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro tip:** Mengubah tipe diagram setelah dibuat sesederhana memanggil `setChartType(...)`. Ini memenuhi kata kunci utama **change Excel chart type** tanpa memerlukan objek diagram baru.

### Step 4: Add interactivity

#### 4.1 Add tooltips to the chart

Tooltip ditampilkan ketika pengguna mengarahkan kursor ke titik data. Di Aspose.Cells, tooltip diimplementasikan melalui label data.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Add data labels ( **add data labels chart** )

Label data dapat menampilkan nilai tepat, nama kategori, atau keduanya. Di sini kami menggunakan gaya callout.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implement drill‑down ( **add drill down excel** )

Tautan drill‑down memungkinkan pengguna mengklik sebuah titik dan melompat ke tampilan terperinci, baik di dalam workbook maupun di halaman web.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Step 5: Save the workbook

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Common issues and solutions

| Masalah | Alasan | Solusi |
|-------|--------|-----|
| Tooltip tidak muncul | `HasDataLabels` tidak diaktifkan | Pastikan `setHasDataLabels(true)` dipanggil sebelum mengonfigurasi `ShowValue`. |
| Tautan drill‑down tidak berfungsi | URL hyperlink tidak terbentuk dengan benar | Pastikan URL dimulai dengan `http://` atau `https://`. |
| Tipe diagram tidak berubah | Menggunakan versi Aspose.Cells yang lebih lama | Upgrade ke versi terbaru (dicoba dengan 24.12). |

## Frequently Asked Questions

**Q: Bagaimana saya dapat mengubah tipe diagram setelah dibuat?**  
A: Panggil `chart.setChartType(ChartType.YOUR_CHOICE)` pada objek `Chart` yang sudah ada. Ini secara langsung memenuhi kebutuhan **change Excel chart type**.

**Q: Bisakah saya menyesuaikan tampilan tooltip?**  
A: Ya. Gunakan `chart.getNSeries().get(0).getPoints().getDataLabels()` untuk mengatur ukuran font, warna, dan latar belakang.

**Q: Apakah memungkinkan menambahkan beberapa tautan drill‑down dalam satu diagram?**  
A: Tentu saja. Loop melalui titik-titik dan panggil `getHyperlinks().add(url)` untuk setiap titik yang ingin Anda tautkan.

**Q: Apakah Aspose.Cells mendukung tipe diagram lain seperti pie atau radar?**  
A: Semua tipe diagram yang didefinisikan dalam enum `ChartType` didukung, termasuk `PIE`, `RADAR`, `AREA`, dll.

**Q: Di mana saya dapat menemukan contoh lebih lanjut?**  
A: Kunjungi [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) resmi untuk daftar lengkap metode terkait diagram.

## Conclusion

Anda sekarang tahu cara **change Excel chart type**, menyematkan **tooltip**, menambahkan **label data**, dan membuat tautan **drill‑down** menggunakan Aspose.Cells untuk Java. Fitur interaktif ini mengubah spreadsheet statis menjadi alat eksplorasi data dinamis, sempurna untuk dasbor, laporan, dan analitik berbasis web.

---

**Terakhir Diperbarui:** 2025-12-01  
**Diuji Dengan:** Aspose.Cells 24.12 untuk Java  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}