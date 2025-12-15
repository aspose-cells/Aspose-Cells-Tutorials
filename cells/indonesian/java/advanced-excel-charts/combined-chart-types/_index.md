---
date: 2025-12-06
description: Pelajari cara menambahkan seri data, membuat jenis grafik gabungan, menyimpan
  buku kerja Excel, dan mengekspor grafik ke PNG dengan Aspose.Cells untuk Java.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Tambahkan seri data untuk membuat diagram gabungan menggunakan Aspose.Cells
url: /id/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan seri data untuk membuat diagram gabungan menggunakan Aspose.Cells

Dalam tutorial ini Anda akan **menambahkan seri data** ke sebuah workbook Excel dan mempelajari cara **membuat diagram gabungan** dengan Aspose.Cells untuk Java. Kami akan memandu Anda melalui setiap langkah—mulai dari menyiapkan workbook, menambahkan seri, menyesuaikan legenda, hingga **menyimpan workbook Excel** dan mengekspor **diagram ke PNG**. Pada akhir tutorial, Anda akan memiliki diagram gabungan siap pakai yang dapat Anda sematkan dalam laporan atau dasbor.

## Jawaban Cepat
- **Perpustakaan mana yang membuat diagram gabungan?** Aspose.Cells for Java  
- **Bagaimana cara menambahkan seri data?** Gunakan `chart.getNSeries().add(...)`  
- **Bisakah saya mengekspor diagram sebagai gambar?** Ya, dengan `chart.toImage(...)` (PNG)  
- **Format file apa yang dapat saya gunakan untuk menyimpan workbook?** `.xlsx` standar (Excel)  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi Aspose.Cells yang valid diperlukan  

## Apa itu **menambahkan seri data** di Aspose.Cells?
Menambahkan seri data memberi tahu diagram sel mana yang berisi nilai yang ingin Anda plot. Setiap seri dapat mewakili garis, kolom, atau jenis diagram lainnya, dan Anda dapat menggabungkannya untuk membuat **diagram gabungan**.

## Mengapa membuat **diagram gabungan**?
Diagram gabungan memungkinkan Anda menampilkan kumpulan data yang berbeda dengan representasi visual yang berbeda (misalnya, seri garis di atas seri kolom) dalam satu tampilan. Ini sangat cocok untuk membandingkan tren dengan total, menyoroti korelasi, atau menyajikan wawasan yang lebih kaya dalam format yang ringkas.

## Prasyarat
- Java Development Kit (JDK) 8 atau lebih tinggi  
- Perpustakaan Aspose.Cells untuk Java (unduh dari tautan di bawah)  
- Pemahaman dasar tentang sintaks Java dan konsep Excel  

## Memulai

Pertama, unduh perpustakaan Aspose.Cells untuk Java dari situs resmi:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Setelah JAR ditambahkan ke classpath proyek Anda, Anda dapat mulai membangun diagram.

### Langkah 1: Impor kelas Aspose.Cells
```java
import com.aspose.cells.*;
```

### Langkah 2: Buat workbook baru
```java
Workbook workbook = new Workbook();
```

### Langkah 3: Akses lembar kerja pertama
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Langkah 4: Tambahkan objek diagram gabungan  
Kami akan memulai dengan diagram garis dan kemudian menambahkan seri lain untuk mencapai efek **diagram gabungan**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Menambahkan Data ke Diagram

Sekarang kontainer diagram sudah ada, kita perlu mengisinya dengan data.

### Langkah 5: Tentukan rentang data dan **menambahkan seri data**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Tips pro:** Parameter pertama (`"A1:A5"`) adalah rentang untuk seri pertama, dan yang kedua (`"B1:B5"`) membuat seri kedua yang akan digabungkan dengan yang pertama.

### Langkah 6: Atur data kategori (sumbu X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Menyesuaikan Diagram

Diagram yang baik menceritakan sebuah kisah. Mari beri judul, label sumbu, dan legenda yang jelas.

### Langkah 7: Atur judul diagram dan label sumbu
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Langkah 8: **Menambahkan legenda diagram** dan sesuaikan posisinya
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Menyimpan dan Mengekspor Diagram

Setelah penyesuaian, Anda akan ingin **menyimpan workbook Excel** dan juga menghasilkan gambar.

### Langkah 9: Simpan workbook sebagai file Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Langkah 10: Ekspor **diagram ke PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metode `chart.toImage` **menghasilkan gambar diagram excel** yang dapat digunakan di halaman web, laporan, atau email.

## Masalah Umum & Pemecahan Masalah

| Masalah | Solusi |
|-------|----------|
| **Tidak ada data muncul** | Verifikasi bahwa rentang sel (`A1:A5`, `B1:B5`, `C1:C5`) memang berisi data sebelum membuat diagram. |
| **Legenda menutupi diagram** | Setel `chart.getLegend().setOverlay(false)` atau pindahkan legenda ke posisi lain (mis., `RIGHT`). |
| **File gambar kosong** | Pastikan diagram memiliki setidaknya satu seri dan `chart.toImage` dipanggil setelah semua penyesuaian. |
| **Penyimpanan menghasilkan pengecualian** | Periksa bahwa Anda memiliki izin menulis ke direktori target dan file tidak terbuka di Excel. |

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana cara menginstal Aspose.Cells untuk Java?**  
A: Unduh JAR dari situs resmi dan tambahkan ke classpath proyek Anda. Tautan unduhan adalah: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Bisakah saya membuat jenis diagram lain selain garis dan kolom?**  
A: Ya, Aspose.Cells mendukung bar, pie, scatter, area, dan banyak jenis diagram lainnya. Lihat dokumentasi API untuk daftar lengkap.

**Q: Apakah lisensi diperlukan untuk penggunaan produksi?**  
A: Lisensi Aspose.Cells yang valid diperlukan untuk penerapan produksi. Versi percobaan gratis tersedia untuk evaluasi.

**Q: Bagaimana cara mengubah warna setiap seri?**  
A: Gunakan `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (atau serupa) setelah menambahkan seri.

**Q: Di mana saya dapat menemukan contoh kode lebih banyak?**  
A: Dokumentasi komprehensif dan contoh tambahan tersedia di situs referensi Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
