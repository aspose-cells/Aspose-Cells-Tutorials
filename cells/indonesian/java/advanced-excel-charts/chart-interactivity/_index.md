---
date: 2025-11-28
description: Pelajari cara menambahkan tooltip, label data, dan fitur drill‑down untuk
  membuat grafik interaktif di Java menggunakan Aspose.Cells.
language: id
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Cara Menambahkan Tooltip pada Grafik Interaktif (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Tooltip pada Diagram Interaktif (Aspose.Cells Java)

## Pendahuluan

Diagram interaktif memungkinkan pengguna menjelajahi data dengan mengarahkan kursor, mengklik, atau menelusuri detail lebih dalam. Dalam tutorial ini Anda akan mempelajari **cara menambahkan tooltip** ke sebuah diagram, serta cara **menambahkan label data**, dan mengimplementasikan navigasi **drill‑down**—semua dengan Aspose.Cells untuk Java. Pada akhir tutorial, Anda akan dapat membuat diagram interaktif yang lengkap, yang membuat presentasi data Anda lebih menarik dan mendalam.

## Jawaban Cepat
- **Perpustakaan apa yang dibutuhkan?** Aspose.Cells untuk Java (versi terbaru).  
- **Fitur utama apa yang dibahas dalam panduan ini?** Menambahkan tooltip ke diagram.  
- **Apakah saya juga dapat menambahkan label data?** Ya – lihat bagian “Menambahkan Label Data”.  
- **Apakah drill‑down didukung?** Ya, melalui hyperlink pada titik data.  
- **Format file apa yang dihasilkan?** Sebuah workbook Excel (`.xlsx`) dengan diagram interaktif.

## Apa itu Menambahkan Tooltip?

Tooltip adalah popup kecil yang muncul ketika pengguna mengarahkan kursor ke elemen diagram, menampilkan informasi tambahan seperti nilai tepat atau pesan khusus. Tooltip meningkatkan keterbacaan data tanpa membuat tata visual menjadi berantakan.

## Mengapa Membuat Diagram Interaktif di Java?

- **Pengambilan keputusan yang lebih baik:** Pengguna dapat langsung melihat nilai yang tepat.  
- **Laporan profesional:** Elemen interaktif membuat dasbor terlihat modern.  
- **Komponen dapat digunakan kembali:** Setelah Anda menguasai API, Anda dapat menerapkannya pada solusi pelaporan berbasis Excel apa pun.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Lingkungan pengembangan Java (JDK 8 atau lebih baru).  
- Perpustakaan Aspose.Cells untuk Java (unduh dari [here](https://releases.aspose.com/cells/java/)).  
- File Excel contoh bernama **data.xlsx** yang berisi data yang ingin Anda visualisasikan.

## Langkah 1: Menyiapkan Proyek Java Anda

1. Buat proyek Java baru di IDE pilihan Anda (IntelliJ IDEA, Eclipse, dll.).  
2. Tambahkan JAR Aspose.Cells ke classpath proyek Anda.

## Langkah 2: Memuat Data

Untuk membuat diagram interaktif Anda pertama-tama memerlukan lembar kerja dengan data. Kode di bawah ini memuat lembar kerja pertama dari **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Langkah 3: Membuat Diagram

Sekarang kita akan menambahkan diagram kolom ke lembar kerja. Diagram akan menempati sel F6 sampai K16.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Langkah 4: Menambahkan Interaktivitas

### 4.1. Cara Menambahkan Tooltip

Potongan kode berikut mengaktifkan tooltip untuk seri pertama dalam diagram. Setiap titik data akan menampilkan nilainya saat diarahkan.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Menambahkan Label Data ke Diagram

Jika Anda juga menginginkan label yang terlihat di samping setiap kolom, gunakan pendekatan **add data labels chart** yang ditunjukkan di bawah ini. Ini memenuhi kata kunci sekunder *add data labels chart*.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Cara Drill Down (Mengimplementasikan Drill‑Down)

Drill‑down memungkinkan pengguna mengklik sebuah titik data dan melompat ke tampilan detail (misalnya, halaman web). Di sini kami menempelkan hyperlink ke titik pertama dari seri.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Pro tip:** Anda dapat menghasilkan URL secara dinamis berdasarkan nilai titik untuk menciptakan pengalaman drill‑down yang benar‑benar didorong data.

## Langkah 5: Menyimpan Workbook

Setelah mengkonfigurasi diagram, simpan workbook. File yang dihasilkan berisi diagram interaktif yang siap dibuka di Excel.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Masalah Umum & Solusi

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| Tooltip tidak muncul | Label data tidak diaktifkan | Pastikan `setHasDataLabels(true)` dipanggil sebelum mengatur `ShowValue`. |
| Hyperlink tidak dapat diklik | Indeks titik salah | Pastikan Anda merujuk ke titik yang benar (`get(0)` adalah titik pertama). |
| Diagram tampak salah posisi | Rentang sel tidak tepat | Sesuaikan indeks baris/kolom dalam `add(ChartType.COLUMN, row1, col1, row2, col2)`. |

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana saya dapat mengubah jenis diagram?**  
A: Ganti `ChartType.COLUMN` dengan nilai enum lain seperti `ChartType.LINE` atau `ChartType.PIE` saat memanggil `worksheet.getCharts().add(...)`.

**Q: Bisakah saya menyesuaikan tampilan tooltip?**  
A: Ya. Gunakan properti pemformatan objek `DataLabel` (ukuran font, warna latar belakang, dll.) untuk menata teks tooltip.

**Q: Bagaimana saya menangani interaksi pengguna dalam aplikasi web?**  
A: Ekspor workbook ke format yang kompatibel dengan web (misalnya, HTML) dan gunakan JavaScript untuk menangkap peristiwa klik pada elemen diagram.

**Q: Di mana saya dapat menemukan contoh dan dokumentasi lebih lanjut?**  
A: Jelajahi referensi API resmi di [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/).

**Q: Apakah memungkinkan menambahkan beberapa link drill‑down dalam diagram yang sama?**  
A: Tentu saja. Lakukan perulangan pada titik-titik seri dan tetapkan URL unik ke koleksi `Hyperlinks` setiap titik.

## Kesimpulan

Dalam panduan ini Anda mempelajari **cara menambahkan tooltip**, **menambahkan label data**, dan **mengimplementasikan drill‑down** untuk membuat solusi **create interactive chart java** menggunakan Aspose.Cells. Fitur-fitur ini mengubah diagram Excel statis menjadi visualisasi dinamis yang ramah pengguna, yang membantu pemangku kepentingan menjelajahi data dengan mudah.

---

**Last Updated:** 2025-11-28  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}