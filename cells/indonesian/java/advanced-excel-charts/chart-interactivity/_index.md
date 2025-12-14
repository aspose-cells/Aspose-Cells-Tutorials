---
date: 2025-12-06
description: Pelajari cara mengubah jenis grafik Excel dan membuat grafik interaktif
  dengan Java menggunakan Aspose.Cells. Tambahkan tooltip ke grafik, label data, dan
  drill‑down untuk visualisasi data yang lebih kaya.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Ubah Tipe Grafik Excel dengan Aspose.Cells Java
url: /id/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Tipe Diagram Excel dan Tambahkan Interaktivitas

## Pendahuluan

Diagram interaktif memberi laporan Excel Anda tingkat wawasan baru, memungkinkan pengguna mengarahkan kursor, mengklik, dan menjelajahi titik data secara langsung. Pada tutorial ini Anda akan **mengubah tipe diagram Excel** dan **membuat solusi diagram interaktif Java** dengan Aspose.Cells for Java. Kami akan membimbing Anda menambahkan tooltip ke diagram, label data, dan hyperlink drill‑down sederhana sehingga audiens dapat menyelami angka‑angka lebih dalam.

## Jawaban Cepat
- **Perpustakaan apa yang digunakan?** Aspose.Cells for Java  
- **Apakah saya dapat mengubah tipe diagram?** Ya – cukup ubah enum `ChartType` saat membuat diagram.  
- **Bagaimana cara menambahkan tooltip ke diagram?** Gunakan API label‑data (`setHasDataLabels(true)`) dan aktifkan tampilan nilai.  
- **Apakah drill‑down didukung?** Anda dapat melampirkan hyperlink ke titik data untuk perilaku drill‑down dasar.  
- **Prasyarat?** IDE Java, Aspose.Cells JAR, dan file Excel dengan data contoh.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki hal‑hal berikut:

- Lingkungan Pengembangan Java (JDK 8+ disarankan)  
- Perpustakaan Aspose.Cells for Java (unduh dari [here](https://releases.aspose.com/cells/java/))  
- Sebuah workbook contoh (`data.xlsx`) yang berisi data yang ingin Anda visualisasikan  

## Langkah 1: Menyiapkan Proyek Java Anda

1. Buat proyek Java baru di IDE favorit Anda (IntelliJ IDEA, Eclipse, dll.).  
2. Tambahkan Aspose.Cells JAR ke jalur build proyek atau ke dependensi Maven/Gradle.

## Langkah 2: Memuat Data

Untuk bekerja dengan diagram, pertama‑tama Anda perlu memuat workbook ke memori.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Langkah 3: Membuat Diagram (dan Mengubah Tipe‑nya)

Anda dapat memilih tipe diagram apa pun yang sesuai dengan analisis Anda. Di bawah ini kami membuat **diagram kolom**, tetapi Anda dapat dengan mudah beralih ke diagram garis, pai, atau batang dengan mengubah enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Tip profesional:** Untuk **mengubah tipe diagram Excel**, ganti `ChartType.COLUMN` dengan `ChartType.LINE`, `ChartType.PIE`, dll.

## Langkah 4: Menambahkan Interaktivitas

### 4.1. Menambahkan Tooltip (Add Tooltips to Chart)

Tooltip muncul ketika pengguna mengarahkan kursor ke titik data. Kode berikut mengaktifkan label data dan menampilkan nilai sebagai tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Menambahkan Label Data

Label data memberikan petunjuk visual permanen pada diagram itu sendiri. Anda dapat menampilkannya sebagai callout untuk meningkatkan keterbacaan.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Menerapkan Drill‑Down (Hyperlink pada Titik Data)

Cara sederhana menambahkan kemampuan drill‑down adalah dengan melampirkan hyperlink ke titik tertentu. Mengklik titik tersebut membuka halaman web dengan informasi detail.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Langkah 5: Menyimpan Workbook

Setelah mengonfigurasi diagram, simpan workbook sehingga fitur interaktif tersimpan dalam file output.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Masalah Umum & Solusi

| Masalah | Solusi |
|-------|----------|
| **Tooltip tidak muncul** | Pastikan `setHasDataLabels(true)` dipanggil sebelum mengonfigurasi `setShowValue(true)`. |
| **Hyperlink tidak dapat diklik** | Verifikasi format output mendukung hyperlink (misalnya, XLSX, bukan CSV). |
| **Tipe diagram tidak berubah** | Periksa kembali bahwa Anda telah mengubah enum `ChartType` yang tepat saat menambahkan diagram. |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara mengubah tipe diagram setelah dibuat?**  
J: Anda harus membuat diagram baru dengan `ChartType` yang diinginkan. Aspose.Cells tidak menyediakan konversi tipe secara langsung, jadi hapus diagram lama dan tambahkan yang baru.

**T: Bisakah saya menyesuaikan tampilan tooltip?**  
J: Ya. Gunakan properti `DataLabel` seperti `setFontSize`, `setFontColor`, dan `setBackgroundColor` untuk menata teks tooltip.

**T: Bagaimana cara menangani interaksi pengguna dalam aplikasi web?**  
J: Ekspor workbook ke file HTML atau XLSX dan gunakan JavaScript di sisi klien untuk menangkap peristiwa klik pada elemen diagram.

**T: Di mana saya dapat menemukan contoh dan dokumentasi lebih lanjut?**  
J: Kunjungi [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) untuk daftar lengkap kelas dan metode terkait diagram.

## Kesimpulan

Anda kini tahu cara **mengubah tipe diagram Excel**, **membuat solusi diagram interaktif Java**, dan memperkaya mereka dengan tooltip, label data, serta hyperlink drill‑down menggunakan Aspose.Cells for Java. Peningkatan ini membuat laporan Excel Anda jauh lebih menarik dan memberikan wawasan lebih bagi pengguna akhir.

---

**Terakhir Diperbarui:** 2025-12-06  
**Diuji Dengan:** Aspose.Cells for Java 24.12  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}