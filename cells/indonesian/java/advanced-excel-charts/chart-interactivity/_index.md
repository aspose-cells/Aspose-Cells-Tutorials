---
date: 2026-08-21
description: Pelajari cara menambahkan tooltip, label data, dan mengubah tipe diagram
  pada diagram Excel menggunakan Aspose.Cells for Java – panduan langkah demi langkah
  dengan contoh interaktif.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Ubah Tipe Diagram Excel
og_description: Pelajari cara menambahkan tooltip, label data, dan mengubah tipe diagram
  pada diagram Excel menggunakan Aspose.Cells for Java – panduan langkah demi langkah
  dengan contoh interaktif.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Cara menambahkan tooltip dan label data ke diagram Excel di Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Cara menambahkan tooltip dan label data ke diagram Excel di Java
url: /id/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan label data ke diagram Excel dan ubah tipe diagram – Aspose.Cells Java

Diagram interaktif memberikan laporan Excel Anda tingkat wawasan baru, dan **cara menambahkan tooltip** membuat informasi langsung dapat dibaca. Dalam tutorial ini Anda akan belajar cara **menambahkan label data ke diagram Excel**, **mengubah tipe diagram**, dan membuat solusi Java interaktif dengan Aspose.Cells. Kami juga akan menunjukkan cara menambahkan tooltip dan hyperlink drill‑down sederhana sehingga audiens Anda dapat menjelajahi data secara mendalam.

## Jawaban Cepat
- **Library apa yang digunakan?** Aspose.Cells for Java  
- **Bisakah saya mengubah tipe diagram?** Ya – cukup ubah enum `ChartType` saat Anda membuat diagram.  
- **Bagaimana cara menambahkan tooltip ke diagram?** Gunakan API data‑label (`setHasDataLabels(true)`) dan aktifkan tampilan nilai.  
- **Apakah drill‑down didukung?** Anda dapat melampirkan hyperlink ke titik data untuk perilaku drill‑down dasar.  
- **Prasyarat?** Java IDE, Aspose.Cells JAR, dan file Excel dengan data contoh.

## Apa itu cara menambahkan tooltip?
**Cara menambahkan tooltip** mengacu pada proses mengaktifkan teks hover‑over yang menampilkan nilai titik data atau informasi khusus pada diagram Excel. Di Aspose.Cells hal ini dicapai melalui pengaturan data‑label diagram. Tooltip membantu pengguna dengan cepat memahami data tanpa mengacaukan diagram, dan dapat disesuaikan untuk font, warna, dan format.

## Mengapa menggunakan diagram interaktif dengan Aspose.Cells?
Aspose.Cells mendukung **lebih dari 50 format input dan output**—termasuk XLSX, CSV, PDF, dan HTML—dan dapat memproses workbook dengan **lebih dari 1 000 lembar** tanpa memuat seluruh file ke memori, memberikan pembuatan diagram sisi server yang cepat untuk pelaporan perusahaan. Diagram interaktif juga memungkinkan penyematan hyperlink, pembaruan data dinamis, dan ekspor ke format yang ramah web, menjadikannya ideal untuk dasbor dan portal pelaporan.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal berikut:

- Lingkungan Pengembangan Java (JDK 8+ disarankan)  
- Perpustakaan Aspose.Cells untuk Java (unduh dari [Aspose.Cells for Java download page](https://releases.aspose.com/cells/java/))  
- Workbook contoh (`data.xlsx`) yang berisi data yang ingin Anda visualisasikan  

## Langkah 1: menyiapkan proyek Java Anda

1. Buat proyek Java baru di IDE favorit Anda (IntelliJ IDEA, Eclipse, dll.).  
2. Tambahkan JAR Aspose.Cells ke jalur build proyek Anda atau dependensi Maven/Gradle.

## Langkah 2: memuat data

Untuk bekerja dengan diagram, pertama-tama Anda memerlukan workbook yang dimuat ke memori.

Kelas `Workbook` mewakili file Excel, dan `Worksheet` mewakili satu lembar dalam file tersebut.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Cara mengubah tipe diagram di Aspose.Cells?

Buat diagram baru dengan enum `ChartType` yang diinginkan; Aspose.Cells tidak mengubah tipe diagram yang ada secara langsung, sehingga Anda harus menambahkan diagram baru dengan tipe yang tepat dan secara opsional menghapus yang lama. Pendekatan ini menjamin semua seri dan sumbu dibangun kembali dengan benar untuk representasi visual baru.

## Langkah 3: membuat diagram (dan mengubah tipenya)

Anda dapat memilih tipe diagram apa pun yang sesuai dengan analisis Anda. Di bawah ini kami membuat **diagram kolom**, tetapi Anda dapat dengan mudah beralih ke diagram garis, lingkaran, atau batang dengan mengubah enum `ChartType`.

Objek `Chart` menyediakan metode untuk mengonfigurasi representasi visual data di worksheet.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Tip pro:** Untuk **mengubah tipe diagram Excel**, ganti `ChartType.COLUMN` dengan `ChartType.LINE`, `ChartType.PIE`, dll.

## Cara menambahkan tooltip ke diagram Excel?

Muat diagram Anda, aktifkan label data, dan atur flag `showValue`. Tooltip kemudian akan menampilkan nilai sel yang mendasarinya setiap kali pengguna mengarahkan kursor ke titik data dalam file Excel yang dirender atau tampilan HTML. Anda juga dapat menyesuaikan font, warna, dan latar belakang tooltip agar sesuai dengan gaya laporan Anda.

Kelas `DataLabel` mengontrol tampilan dan konten label data, yang juga berfungsi sebagai tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Langkah 4: menambahkan interaktivitas

### 4.1. Menambahkan tooltip (menambahkan tooltip ke diagram)

Tooltip muncul ketika pengguna mengarahkan kursor ke titik data. Kode berikut mengaktifkan label data dan menampilkan nilai sebagai tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Menambahkan label data – **tambahkan label data ke diagram excel**

Label data memberikan petunjuk visual permanen pada diagram itu sendiri. Anda dapat menampilkannya sebagai callout untuk meningkatkan keterbacaan.

Kelas `DataLabel` mengontrol tampilan label pada setiap seri. Dengan memanggil `setHasDataLabels(true)` dan mengonfigurasi properti seperti `setShowValue(true)`, Anda menanamkan nilai numerik langsung ke diagram, membuatnya langsung terlihat tanpa interaksi apa pun. Opsi tambahan memungkinkan Anda menampilkan nama seri, persentase, atau teks khusus untuk konteks yang lebih kaya.

> **Mengapa menambahkan label data?** Menyertakan label data langsung pada diagram menghilangkan kebutuhan pengguna untuk mengarahkan kursor atau menebak nilai, meningkatkan kejelasan laporan.

### 4.3. Menerapkan drill‑down (hyperlink pada titik data)

Cara sederhana untuk menambahkan kemampuan drill‑down adalah dengan melampirkan hyperlink pada titik tertentu. Mengklik titik tersebut membuka halaman web dengan informasi detail.

Kelas `Hyperlink` melampirkan tautan yang dapat diklik ke elemen diagram, memungkinkan navigasi drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Cara menambahkan label data ke diagram Excel?

Kelas `DataLabel` mengontrol tampilan label pada setiap seri. Dengan memanggil `setHasDataLabels(true)` dan mengonfigurasi properti seperti `setShowValue(true)`, Anda menanamkan nilai numerik langsung ke diagram, membuatnya langsung terlihat tanpa interaksi apa pun. Opsi tambahan memungkinkan Anda menampilkan nama seri, persentase, atau teks khusus untuk konteks yang lebih kaya.

## Langkah 5: menyimpan workbook

Setelah mengonfigurasi diagram, simpan workbook sehingga fitur interaktif disimpan dalam file output.

Memanggil `workbook.save` menulis workbook yang dimodifikasi ke file dalam format yang dipilih.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Masalah umum & solusi

| Masalah | Solusi |
|-------|----------|
| **Tooltip tidak muncul** | Pastikan `setHasDataLabels(true)` dipanggil sebelum mengonfigurasi `setShowValue(true)`. |
| **Hyperlink tidak dapat diklik** | Verifikasi format output mendukung hyperlink (mis., XLSX, bukan CSV). |
| **Tipe diagram tidak berubah** | Periksa kembali Anda telah memodifikasi enum `ChartType` yang tepat saat menambahkan diagram. |

## Pertanyaan yang sering diajukan

**Q: Bagaimana saya dapat mengubah tipe diagram setelah dibuat?**  
A: Anda perlu membuat diagram baru dengan `ChartType` yang diinginkan. Aspose.Cells tidak menyediakan konversi tipe secara langsung, jadi hapus diagram lama dan tambahkan yang baru.

**Q: Bisakah saya menyesuaikan tampilan tooltip?**  
A: Ya. Gunakan properti `DataLabel` seperti `setFontSize`, `setFontColor`, dan `setBackgroundColor` untuk menata teks tooltip.

**Q: Bagaimana saya menangani interaksi pengguna dalam aplikasi web?**  
A: Ekspor workbook ke file HTML atau XLSX dan gunakan JavaScript di sisi klien untuk menangkap peristiwa klik pada elemen diagram.

**Q: Di mana saya dapat menemukan contoh dan dokumentasi lebih lanjut?**  
A: Kunjungi [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) untuk daftar lengkap kelas dan metode terkait diagram.

## Kesimpulan

Anda sekarang tahu cara **menambahkan label data ke diagram Excel**, **mengubah tipe diagram Excel**, **membuat solusi diagram Java interaktif**, dan memperkaya mereka dengan tooltip, label data, serta hyperlink drill‑down menggunakan Aspose.Cells untuk Java. Peningkatan ini membuat laporan Excel Anda jauh lebih menarik dan memberikan wawasan lebih bagi pengguna akhir.

---

**Terakhir Diperbarui:** 2026-08-21  
**Diuji Dengan:** Aspose.Cells for Java 24.12  
**Penulis:** Aspose

## Tutorial Terkait

- [Cara Memodifikasi Diagram Excel dan Label Data Menggunakan Aspose.Cells untuk Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Ekstrak Label Sumbu Diagram Excel Menggunakan Aspose.Cells Java: Panduan Komprehensif](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Buat Diagram Bubble di Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑ demi‑ Langkah](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}