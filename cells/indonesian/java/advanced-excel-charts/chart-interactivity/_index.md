---
date: 2026-02-09
description: Pelajari cara menambahkan label data ke grafik Excel dan mengubah jenis
  grafik menggunakan Aspose.Cells untuk Java, serta tooltip dan interaktivitas drill‑down.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Tambahkan Label Data ke Diagram Excel dengan Aspose.Cells Java
url: /id/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

We need to translate "Add Data Labels to Excel Chart and Change Chart Type – Aspose.Cells Java" heading.

Also "Interactive charts give your Excel reports a new level of insight..." etc.

Make sure to keep bold formatting.

Translate "Quick Answers" etc.

Translate table content.

Translate FAQs.

Make sure to keep markdown formatting.

Let's craft translation.

We'll keep URLs unchanged.

Let's produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Label Data ke Diagram Excel dan Ubah Jenis Diagram – Aspose.Cells Java

Diagram interaktif memberikan laporan Excel Anda tingkat wawasan baru, dan **menambahkan label data ke diagram Excel** membuat informasi langsung dapat dibaca. Pada tutorial ini Anda akan belajar cara **menambahkan label data ke diagram Excel**, mengubah jenis diagram, dan membuat solusi Java interaktif dengan Aspose.Cells. Kami juga akan menunjukkan cara menambahkan tooltip dan hyperlink drill‑down sederhana sehingga audiens dapat menjelajahi data secara mendalam.

## Jawaban Cepat
- **Perpustakaan apa yang digunakan?** Aspose.Cells untuk Java  
- **Apakah saya dapat mengubah jenis diagram?** Ya – cukup ubah enum `ChartType` saat membuat diagram.  
- **Bagaimana cara menambahkan tooltip ke diagram?** Gunakan API label‑data (`setHasDataLabels(true)`) dan aktifkan tampilan nilai.  
- **Apakah drill‑down didukung?** Anda dapat melampirkan hyperlink ke titik data untuk perilaku drill‑down dasar.  
- **Prasyarat?** IDE Java, Aspose.Cells JAR, dan file Excel dengan data contoh.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki hal‑hal berikut:

- Lingkungan Pengembangan Java (JDK 8+ disarankan)  
- Perpustakaan Aspose.Cells untuk Java (unduh dari [here](https://releases.aspose.com/cells/java/))  
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

## Langkah 3: Membuat Diagram (dan Mengubah Jenisnya)

Anda dapat memilih jenis diagram apa pun yang sesuai dengan analisis Anda. Di bawah ini kami membuat **diagram kolom**, tetapi Anda dapat dengan mudah beralih ke diagram garis, pai, atau batang dengan mengubah enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Tips pro:** Untuk **mengubah jenis diagram Excel**, ganti `ChartType.COLUMN` dengan `ChartType.LINE`, `ChartType.PIE`, dll.

## Langkah 4: Menambahkan Interaktivitas

### 4.1. Menambahkan Tooltip (Add Tooltips to Chart)

Tooltip muncul ketika pengguna mengarahkan kursor ke titik data. Kode berikut mengaktifkan label data dan menampilkan nilai sebagai tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Menambahkan Label Data – **add data labels to excel chart**

Label data memberikan petunjuk visual permanen pada diagram itu sendiri. Anda dapat menampilkannya sebagai callout untuk meningkatkan keterbacaan.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Mengapa menambahkan label data?** Menyertakan label data langsung pada diagram menghilangkan kebutuhan pengguna untuk mengarahkan kursor atau menebak nilai, sehingga meningkatkan kejelasan laporan.

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
| **Jenis diagram tidak berubah** | Periksa kembali apakah Anda telah mengubah enum `ChartType` yang tepat saat menambahkan diagram. |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara mengubah jenis diagram setelah dibuat?**  
J: Anda harus membuat diagram baru dengan `ChartType` yang diinginkan. Aspose.Cells tidak menyediakan konversi jenis secara langsung, jadi hapus diagram lama dan tambahkan yang baru.

**T: Bisakah saya menyesuaikan tampilan tooltip?**  
J: Ya. Gunakan properti `DataLabel` seperti `setFontSize`, `setFontColor`, dan `setBackgroundColor` untuk menata teks tooltip.

**T: Bagaimana cara menangani interaksi pengguna dalam aplikasi web?**  
J: Ekspor workbook ke file HTML atau XLSX dan gunakan JavaScript di sisi klien untuk menangkap peristiwa klik pada elemen diagram.

**T: Di mana saya dapat menemukan contoh dan dokumentasi lebih lanjut?**  
J: Kunjungi [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) untuk daftar lengkap kelas dan metode terkait diagram.

## Kesimpulan

Anda kini tahu cara **menambahkan label data ke diagram Excel**, **mengubah jenis diagram Excel**, **membuat solusi diagram Java** yang interaktif, serta memperkaya mereka dengan tooltip, label data, dan hyperlink drill‑down menggunakan Aspose.Cells untuk Java. Peningkatan ini membuat laporan Excel Anda jauh lebih menarik dan memberikan wawasan lebih bagi pengguna akhir.

---

**Terakhir Diperbarui:** 2026-02-09  
**Diuji Dengan:** Aspose.Cells untuk Java 24.12  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}