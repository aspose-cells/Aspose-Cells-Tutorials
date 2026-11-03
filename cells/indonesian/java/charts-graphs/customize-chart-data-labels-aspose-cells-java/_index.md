---
date: '2026-10-17'
description: Pelajari cara mengatur bentuk label data grafik Excel di Java menggunakan
  Aspose.Cells. Panduan ini menunjukkan cara memodifikasi label grafik Excel dengan
  cepat dan efisien.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Pelajari cara mengatur bentuk label data grafik Excel di Java menggunakan
  Aspose.Cells. Panduan langkah demi langkah ini membantu Anda memodifikasi label
  grafik Excel dengan cepat.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Cara mengatur bentuk label data grafik Excel di Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Cara mengatur bentuk label data grafik Excel di Java
url: /id/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menguasai penyesuaian diagram di Java dengan Aspose.Cells: mengubah bentuk label data

## Pendahuluan

Meningkatkan daya tarik visual diagram Excel sangat penting saat menyiapkan laporan atau dasbor, terutama jika Anda menggunakan Java. Dengan Aspose.Cells—sebuah perpustakaan kuat untuk manajemen dan manipulasi spreadsheet—Anda dapat **how to set shape** label data diagram hanya dalam beberapa baris kode. Tutorial ini akan memandu Anda melalui mengubah bentuk label data dalam diagram Excel menggunakan Aspose.Cells untuk Java. Pada akhir tutorial, Anda akan mengetahui cara:

- Mengakses dan memodifikasi label data diagram
- Menetapkan bentuk khusus untuk label data
- Menyimpan perubahan ke workbook Anda

## Jawaban Cepat
- **Apa kelas utama untuk bekerja dengan file Excel?** `Workbook` mewakili seluruh file Excel dalam memori.  
- **Metode mana yang mengatur bentuk label?** `setShapeType(DataLabelShapeType shape)` pada objek `DataLabel`.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya menerapkan bentuk ke beberapa seri?** Ya—iterasi setiap seri dan panggil `setShapeType`.  
- **Apakah pendekatan ini kompatibel dengan workbook besar?** Aspose.Cells memproses workbook ratusan halaman tanpa memuat seluruh file ke memori.

## Apa itu how to set shape?
Frasa **how to set shape** merujuk pada konfigurasi kontur visual label data diagram, seperti mengubah persegi panjang polos menjadi callout atau elips. Mengubah bentuk meningkatkan keterbacaan dan menyoroti poin data penting. Dengan memilih bentuk yang tepat, Anda dapat membuat label menonjol, mengelompokkan poin terkait, atau menyesuaikan dengan pedoman merek perusahaan, sehingga meningkatkan keterbacaan keseluruhan diagram.

## Mengapa menggunakan Aspose.Cells untuk penyesuaian label diagram?
Aspose.Cells mendukung **lebih dari 50 format input dan output**—termasuk XLSX, CSV, ODS, dan PDF—dan dapat memanipulasi workbook yang berisi **hingga 1 juta baris** tanpa menghabiskan memori. API‑nya memungkinkan Anda memodifikasi diagram secara programatis, menghilangkan kebutuhan edit manual di Excel dan memastikan gaya konsisten di seluruh laporan otomatis.

## Prasyarat

- **Aspose.Cells untuk Java Library**: Versi 25.3 atau lebih baru diperlukan.  
- **Lingkungan Pengembangan Java**: JDK terinstal di mesin Anda.  
- **Pengaturan IDE**: Gunakan IDE seperti IntelliJ IDEA atau Eclipse untuk menulis dan menjalankan kode Anda.

### Perpustakaan dan dependensi yang diperlukan

Untuk pengguna Maven, sertakan dependensi berikut dalam `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Pengguna Gradle harus menambahkan ini ke file `build.gradle` mereka:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Akuisisi lisensi

Aspose.Cells menawarkan lisensi percobaan gratis, yang dapat Anda dapatkan dari [Aspose temporary license page](https://purchase.aspose.com/temporary-license/). Ini memberikan akses penuh ke semua fitur tanpa batasan untuk waktu terbatas.

## Menyiapkan Aspose.Cells untuk Java

Setelah lingkungan Anda siap, mari siapkan Aspose.Cells. Berikut cara memulainya:

### Langkah-langkah instalasi

1. **Unduh perpustakaan**: Gunakan Maven atau Gradle seperti yang ditunjukkan di atas.  
2. **Konfigurasi lisensi**:  
   - `License` adalah kelas yang menerapkan file lisensi Aspose.Cells Anda untuk mengaktifkan fungsionalitas penuh.  
   - Unduh dan terapkan lisensi sementara menggunakan cuplikan kode ini setelah menginisialisasi objek `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Inisialisasi dasar**: Buat instance `Workbook` untuk mulai bekerja dengan file Excel.

## Cara mengatur bentuk label data dalam diagram?

Muat workbook Anda, temukan diagram target, dan terapkan bentuk yang diinginkan pada label datanya. Langkah langsung berikut menyelesaikannya dalam kurang dari satu menit.

### Panduan langkah demi langkah

#### Langkah 1: muat workbook Anda

Kelas `Workbook` adalah objek tingkat‑atas Aspose.Cells yang mewakili satu file Excel dalam memori. Gunakan `new Workbook("input.xlsx")` untuk memuat file yang ingin Anda modifikasi.

#### Langkah 2: akses diagram

`Worksheet` mewakili satu lembar dalam workbook.  
`Worksheet ws = workbook.getWorksheets().get(0);` mengambil lembar kerja pertama.  
`Chart` adalah objek yang mewakili diagram yang disisipkan dalam lembar kerja.  
`Chart chart = ws.getCharts().get(0);` memperoleh diagram pertama pada lembar tersebut.

#### Langkah 3: ambil seri dan modifikasi label data

`Series` mewakili seri data yang dipetakan pada diagram.  
Setiap objek `Series` berisi koleksi `DataLabel`.  
`DataLabel` mengontrol tampilan label data untuk sebuah seri.  
`DataLabelShapeType` adalah enumerasi bentuk yang mungkin untuk label data.  
Panggil `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` untuk mengatur bentuk. Enum ini menyediakan puluhan opsi, seperti `RECTANGLE`, `CLOUD`, dan `WEDGE_ELLIPSE_CALLOUT`.

#### Langkah 4: simpan workbook Anda

Setelah menerapkan bentuk, panggil `workbook.save("output.xlsx");` untuk menulis perubahan kembali ke disk.

## Tips pemecahan masalah

- **Masalah jalur file**: Pastikan jalur file bersifat absolut atau relatif dengan benar terhadap direktori kerja proyek Anda.  
- **Versi perpustakaan tidak cocok**: Pastikan Anda menggunakan Aspose.Cells versi 25.3 atau lebih baru; versi lama tidak memiliki metode `setShapeType`.  
- **Tipe diagram tidak didukung**: Beberapa tipe diagram lama (mis., radar) mungkin tidak menampilkan properti bentuk label data; beralih ke tipe diagram yang didukung seperti kolom atau garis.

## Aplikasi praktis

1. **Pelaporan keuangan** – Sorot margin keuntungan utama dengan label bergaya callout.  
2. **Konten edukasi** – Gunakan label berbentuk awan untuk menarik perhatian pada poin data penting dalam materi pembelajaran.  
3. **Analitik pemasaran** – Terapkan bentuk khusus untuk membedakan metrik kinerja kampanye dalam dasbor.

Mengintegrasikan Aspose.Cells dengan alur data atau sistem CRM memungkinkan Anda menghasilkan laporan bergaya penuh secara otomatis, mengurangi upaya manual dan memastikan visual yang konsisten dengan merek.

## Pertimbangan kinerja

Saat bekerja dengan file Excel besar:

- **Optimalkan penggunaan memori**: Panggil `workbook.dispose();` setelah menyimpan untuk segera melepaskan sumber daya native.  
- **Pemrosesan batch**: Proses diagram dalam grup daripada satu per satu untuk meminimalkan overhead pembuatan objek.  
- **Penanganan data yang efisien**: Hindari perhitungan berat di dalam loop yang mengiterasi ribuan baris; hitung nilai sebelumnya.

## Kesimpulan

Anda kini mengetahui **how to set shape** label data diagram Excel di Java menggunakan Aspose.Cells. Kemampuan ini tidak hanya meningkatkan estetika diagram tetapi juga memperbaiki pemahaman data bagi pengguna akhir. Jelajahi opsi penyesuaian tambahan—seperti warna label, font, dan garis pemimpin—untuk menyempurnakan visualisasi Anda lebih lanjut.

Untuk pertanyaan atau bantuan, lihat [Aspose support forum](https://forum.aspose.com/c/cells/9).

## Pertanyaan yang sering diajukan

**T: Bagaimana cara mengubah bentuk beberapa label data sekaligus?**  
J: Loop melalui setiap seri dalam diagram dan panggil `setShapeType` pada objek `DataLabel` seri tersebut.

**T: Bisakah Aspose.Cells untuk Java menangani file Excel besar secara efisien?**  
J: Ya. Dengan manajemen memori yang tepat, ia memproses workbook yang berisi ratusan ribu baris tanpa memuat seluruh file ke memori.

**T: Apa masalah umum saat menyiapkan Aspose.Cells?**  
J: Ketergantungan Maven yang hilang, menggunakan versi perpustakaan yang usang, atau memberikan file lisensi yang tidak valid adalah kendala tipikal.

**T: Apakah ada cara mengembalikan bentuk label data ke default?**  
J: Atur tipe bentuk ke `DataLabelShapeType.DEFAULT` untuk mengembalikan tampilan semula.

**T: Bagaimana saya dapat menerapkan penyesuaian ini ke beberapa diagram dalam satu workbook?**  
J: Iterasi melalui `ws.getCharts()` dan terapkan logika `setShapeType` yang sama pada koleksi seri setiap diagram.

## Sumber daya

- [Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Unduh Aspose.Cells untuk Java](https://releases.aspose.com/cells/java/)
- [Beli Lisensi](https://purchase.aspose.com/buy)
- [Lisensi Percobaan Gratis](https://releases.aspose.com/cells/java/)
- [Lisensi Sementara](https://purchase.aspose.com/temporary-license/)

---  

**Terakhir Diperbarui:** 2026-10-17  
**Diuji Dengan:** Aspose.Cells 25.3 untuk Java  
**Penulis:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Tutorial Terkait

- [Ubah Label Data Diagram Excel Menggunakan Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [Cara Mengubah Ukuran Label di Diagram Excel dengan Aspose.Cells untuk Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Menambahkan Label ke Diagram Excel dengan Aspose Cells untuk Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}