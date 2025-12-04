---
date: 2025-12-04
description: Pelajari cara membuat diagram interaktif Java menggunakan Aspose.Cells,
  menambahkan tooltip ke diagram, dan menambahkan diagram drill down untuk visualisasi
  data yang lebih kaya.
language: id
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Buat Grafik Interaktif Java dengan Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Buat Diagram Interaktif Java

## Introduction

Diagram interaktif memberi pengguna Anda kemampuan untuk menjelajahi titik data, melihat detail saat mengarahkan kursor, dan bahkan menelusuri dataset yang lebih dalam—semua tanpa meninggalkan spreadsheet. Dalam tutorial ini Anda akan belajar **how to create interactive chart Java** aplikasi menggunakan Aspose.Cells. Kami akan membahas cara menambahkan tooltip, label data, dan mengimplementasikan pengalaman drill‑down, sehingga diagram Anda menjadi lebih menarik dan informatif.

## Quick Answers
- **Apa perpustakaan yang digunakan?** Aspose.Cells for Java  
- **Bisakah saya menambahkan tooltip ke diagram?** Ya, menggunakan API data‑label NSeries  
- **Apakah drill‑down didukung?** Ya, dengan melampirkan hyperlink ke titik data  
- **Format file apa yang dihasilkan?** Workbook XLSX standar dengan diagram tersemat  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi  

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki:

- Lingkungan pengembangan Java (JDK 8+ disarankan)  
- Aspose.Cells for Java library (unduh dari [Aspose release page](https://releases.aspose.com/cells/java/))  
- File Excel contoh bernama **data.xlsx** yang berisi data yang ingin Anda visualisasikan  

## Step 1: Setting Up Your Java Project

1. Buat proyek Java baru di IDE pilihan Anda (IntelliJ IDEA, Eclipse, VS Code, dll.).  
2. Tambahkan JAR Aspose.Cells ke classpath proyek Anda—baik dengan menempatkan JAR di folder `libs` atau dengan menambahkan dependensi Maven/Gradle.  

## Step 2: Loading Data

Untuk membuat diagram interaktif, Anda pertama-tama memerlukan worksheet dengan data. Potongan kode di bawah ini membuka workbook yang ada dan mengambil worksheet pertama.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tip:** Pastikan rentang data yang ingin Anda diagramkan bersebelahan; Aspose.Cells akan secara otomatis mendeteksi rentang saat Anda mengikat seri.

## Step 3: Creating a Chart

Sekarang kita membuat diagram kolom dan menempatkannya di worksheet. Anda dapat mengubah `ChartType.COLUMN` ke tipe lain (mis., `ChartType.LINE`) jika menginginkan gaya visual yang berbeda.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Why this matters:** Menambahkan diagram secara programatik memberi Anda kontrol penuh atas ukuran, posisi, dan sumber data, yang penting untuk membangun pengalaman interaktif.

## Step 4: Adding Interactivity

### Cara menambahkan tooltip ke diagram

Tooltip (atau label data yang menampilkan nilai) membantu pengguna langsung melihat angka tepat di balik setiap batang. Kode berikut mengaktifkan label data dan mengkonfigurasinya untuk menampilkan nilai.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Cara menambahkan label data (callouts)

Jika Anda ingin label muncul sebagai callout bukan teks biasa, ubah properti `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Cara menambahkan diagram drill down

Drill‑down memungkinkan pengguna mengklik titik data dan melompat ke tampilan detail terkait—biasanya diimplementasikan dengan hyperlink. Di bawah ini kami melampirkan URL ke titik pertama dalam seri.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Common pitfall:** Ingat untuk mengatur target hyperlink ke halaman yang dapat menampilkan data detail (mis., laporan web atau lembar Excel lain). Jika tidak, klik akan mengarah ke tautan mati.

## Step 5: Saving the Workbook

Setelah mengkonfigurasi diagram, simpan workbook. File yang dihasilkan berisi diagram interaktif yang siap dibuka di Excel atau penampil kompatibel lainnya.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Conclusion

Dalam panduan ini Anda belajar **how to create interactive chart Java** solusi dengan Aspose.Cells, mencakup:

- Memuat data dari workbook yang ada  
- Membuat diagram kolom secara programatik  
- Menambahkan tooltip dan label data callout  
- Mengimplementasikan fungsi drill‑down melalui hyperlink  
- Menyimpan workbook akhir  

Teknik ini mengubah spreadsheet statis menjadi dasbor dinamis yang ramah pengguna, meningkatkan pemahaman data dan pengambilan keputusan.

## Frequently Asked Questions

**Q: Bagaimana saya dapat mengubah tipe diagram?**  
A: Ubah enum `ChartType` dalam metode `add` (mis., `ChartType.LINE` untuk diagram garis).

**Q: Bisakah saya menyesuaikan tampilan tooltip?**  
A: Ya, Anda dapat mengatur ukuran font, warna, latar belakang, dan properti gaya lainnya melalui objek `DataLabels`.

**Q: Bagaimana saya menangani interaktivitas diagram dalam aplikasi web?**  
A: Ekspor workbook ke XLSX, kemudian gunakan perpustakaan chart JavaScript (mis., Highcharts) untuk merender data di sisi klien, atau sematkan file Excel dalam Office Web Viewer yang menghormati hyperlink.

**Q: Di mana saya dapat menemukan contoh lebih lanjut?**  
A: Kunjungi [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) resmi untuk daftar lengkap kelas dan metode terkait diagram.

**Q: Apakah saya memerlukan lisensi untuk penggunaan produksi?**  
A: Ya, lisensi komersial diperlukan untuk penerapan; lisensi evaluasi gratis tersedia untuk pengujian.

---

**Last Updated:** 2025-12-04  
**Tested With:** Aspose.Cells for Java 24.12 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}