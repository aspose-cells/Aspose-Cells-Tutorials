---
date: 2026-02-14
description: Pelajari cara mengekspor grafik ke png, menambahkan seri data, menggabungkan
  grafik garis dan kolom, menyimpan buku kerja sebagai xlsx, dan menambahkan legenda
  grafik menggunakan Aspose.Cells untuk Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Ekspor grafik ke PNG dan tambahkan seri data untuk grafik gabungan
url: /id/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor diagram ke PNG dan tambahkan seri data untuk diagram gabungan

Dalam tutorial ini Anda akan **menambahkan seri data** ke workbook Excel, **menggabungkan elemen diagram garis dan kolom**, dan mempelajari cara **mengekspor diagram ke PNG** menggunakan Aspose.Cells for Java. Kami akan membahas setiap langkah—mulai dari menyiapkan workbook, menambahkan diagram ke lembar kerja, menyesuaikan legenda, hingga **menyimpan workbook sebagai xlsx** dan menghasilkan gambar PNG dari diagram. Pada akhir tutorial, Anda akan memiliki diagram gabungan siap pakai yang dapat disematkan dalam laporan atau dasbor.

## Jawaban Cepat
- **Perpustakaan mana yang membuat diagram gabungan?** Aspose.Cells for Java  
- **Bagaimana cara menambahkan seri data?** Gunakan `chart.getNSeries().add(...)`  
- **Bagaimana cara mengekspor diagram ke png?** Panggil `chart.toImage("file.png", ImageFormat.getPng())`  
- **Format file apa yang dapat saya simpan untuk workbook?** Standar `.xlsx` (save workbook as xlsx)  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi Aspose.Cells yang valid diperlukan  

## Apa itu **export chart to PNG** di Aspose.Cells?
Mengekspor diagram ke PNG menghasilkan gambar raster dari diagram Excel yang dapat ditampilkan di halaman web, laporan, atau email tanpa memerlukan aplikasi Excel.

## Mengapa membuat **combined line column chart**?
Diagram gabungan memungkinkan Anda menampilkan kumpulan data yang berbeda dengan representasi visual yang berbeda (misalnya, seri garis di atas seri kolom) dalam satu tampilan. Ini sangat cocok untuk membandingkan tren dengan total, menyoroti korelasi, atau menyajikan wawasan yang lebih kaya dalam format yang kompak.

## Prasyarat
- Java Development Kit (JDK) 8 atau lebih tinggi  
- Perpustakaan Aspose.Cells for Java (unduh dari tautan di bawah)  
- Familiaritas dasar dengan sintaks Java dan konsep Excel  

## Memulai

Pertama, unduh perpustakaan Aspose.Cells for Java dari situs resmi:

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

### Langkah 4: Tambahkan objek diagram gabungan ke lembar kerja  
Kami akan memulai dengan diagram garis dan kemudian menambahkan seri kolom untuk mencapai efek **combined line column chart**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Menambahkan Data ke Diagram

Setelah kontainer diagram ada, kita perlu mengisinya dengan data.

### Langkah 5: Tentukan rentang data dan **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Parameter pertama (`"A1:A5"`) adalah rentang untuk seri pertama, dan yang kedua (`"B1:B5"`) membuat seri kedua yang akan digabungkan dengan yang pertama.

### Langkah 6: Atur data kategori (sumbu X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Menyesuaikan Diagram

Diagram yang baik menceritakan sebuah kisah. Mari beri judul, label sumbu, dan legenda yang jelas.

### Langkah 7: **Set chart axis labels** dan judul
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Langkah 8: **Add legend chart** dan sesuaikan posisinya
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Menyimpan dan Mengekspor Diagram

Setelah penyesuaian, Anda akan ingin **save workbook as xlsx** dan juga menghasilkan gambar.

### Langkah 9: Simpan workbook sebagai file Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Langkah 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metode `chart.toImage` **generates excel chart** gambar yang dapat digunakan di halaman web, laporan, atau email.

## Masalah Umum & Pemecahan Masalah

| Masalah | Solusi |
|-------|----------|
| **No data appears** | Verifikasi bahwa rentang sel (`A1:A5`, `B1:B5`, `C1:C5`) memang berisi data sebelum membuat diagram. |
| **Legend overlaps chart** | Atur `chart.getLegend().setOverlay(false)` atau pindahkan legenda ke posisi lain (mis., `RIGHT`). |
| **Image file is blank** | Pastikan diagram memiliki setidaknya satu seri dan bahwa `chart.toImage` dipanggil setelah semua penyesuaian. |
| **Saving throws an exception** | Periksa apakah Anda memiliki izin menulis ke direktori target dan bahwa file tidak terbuka di Excel. |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara menginstal Aspose.Cells for Java?**  
J: Unduh JAR dari situs resmi dan tambahkan ke classpath proyek Anda. Tautan unduhan adalah: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**T: Bisakah saya membuat tipe diagram lain selain garis dan kolom?**  
J: Ya, Aspose.Cells mendukung bar, pie, scatter, area, dan banyak tipe diagram lainnya. Lihat dokumentasi API untuk daftar lengkapnya.

**T: Apakah lisensi diperlukan untuk penggunaan produksi?**  
J: Lisensi Aspose.Cells yang valid diperlukan untuk penerapan produksi. Versi percobaan gratis tersedia untuk evaluasi.

**T: Bagaimana cara mengubah warna masing‑masing seri?**  
J: Gunakan `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (atau serupa) setelah menambahkan seri.

**T: Di mana saya dapat menemukan contoh kode lainnya?**  
J: Dokumentasi lengkap dan contoh tambahan tersedia di situs referensi Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Terakhir Diperbarui:** 2026-02-14  
**Diuji Dengan:** Aspose.Cells for Java versi terbaru  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}