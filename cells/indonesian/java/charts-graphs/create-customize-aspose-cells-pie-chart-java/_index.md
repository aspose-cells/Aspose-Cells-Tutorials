---
date: '2026-09-27'
description: Pelajari cara membuat pie chart Java menggunakan Aspose.Cells. Panduan
  langkah demi langkah untuk menyesuaikan pie chart Excel, menyiapkan dependensi Maven,
  dan menghasilkan diagram profesional.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Buat pie chart Java menggunakan Aspose.Cells untuk Java. Pelajari
  cara menyesuaikan pie chart Excel, menambahkan dependensi Maven, dan menghasilkan
  diagram profesional dalam hitungan menit.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Buat pie chart Java dengan Aspose.Cells – Panduan Java Lengkap
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Cara membuat pie chart Java dengan Aspose.Cells
url: /id/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat pie chart java dengan Aspose.Cells

## Pendahuluan
Membuat **pie chart** secara programatik sering terasa seperti teka‑teki, terutama ketika Anda memerlukan kontrol yang sangat detail atas warna, legenda, dan judul. Dalam panduan ini Anda akan belajar cara **create pie chart java** menggunakan Aspose.Cells, kemudian menyesuaikan **pie chart** Excel agar sesuai dengan merek atau gaya pelaporan Anda. Kami akan membahas penyiapan lingkungan, pengisian data, pembuatan diagram, dan penyesuaian visual—semua tanpa meninggalkan IDE Java Anda.

**Apa yang akan Anda pelajari**
- Tambahkan **Maven dependency Aspose.Cells** ke proyek Anda.
- Bangun workbook, isi sel dengan data, dan hasilkan **pie chart**.
- Terapkan warna khusus, judul, dan legenda pada diagram.
- Ekspor workbook ke file XLSX yang siap dibagikan.

Sebelum memulai, Anda harus nyaman dengan sintaks Java dasar dan telah menginstal Maven atau Gradle.

## Jawaban Cepat
- **Library mana yang membuat pie chart di Java?** Aspose.Cells for Java.
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi berbayar diperlukan untuk produksi.
- **Koordinat Maven apa yang diperlukan?** `com.aspose:aspose-cells:24.10`.
- **Bisakah saya mengubah warna irisan?** Ya, melalui metode `setAreaColor` pada setiap series.
- **Apakah diagram dapat diekspor ke XLSX?** Tentu—cukup panggil `workbook.save("output.xlsx")`.

## Apa itu pie chart di Excel?
**pie chart** menvisualisasikan satu seri data sebagai irisan proporsional dari sebuah lingkaran, memudahkan perbandingan bagian-bagian dari keseluruhan. Sudut setiap irisan sesuai dengan nilai relatifnya terhadap total, memberikan wawasan cepat tentang distribusi di antara kategori seperti pangsa pasar, alokasi anggaran, atau persentase demografis.

## Mengapa menggunakan Aspose.Cells untuk membuat pie chart java?
Aspose.Cells mendukung lebih dari 50 tipe diagram dan dapat menangani worksheet dengan hingga satu juta baris tanpa memuat seluruh file ke memori. Keunggulan performa ini memungkinkan Anda menghasilkan laporan besar pada perangkat keras yang sederhana, sambil memberikan kontrol detail atas tampilan diagram, pengikatan data, dan format ekspor, menjadikannya pilihan yang lebih unggul dibanding banyak pustaka open‑source.

## Prasyarat
- **Java Development Kit (JDK)** 8 atau yang lebih baru.
- **IDE** seperti IntelliJ IDEA atau Eclipse.
- **Maven** atau **Gradle** untuk manajemen dependensi.
- Sebuah **lisensi Aspose.Cells trial atau berbayar**.

### Perpustakaan dan dependensi yang diperlukan
Tambahkan artefak Maven Aspose.Cells ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Atau setara Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Langkah-langkah memperoleh lisensi
Aspose.Cells for Java bersifat komersial, tetapi Anda dapat memulai dengan percobaan gratis. Kunjungi [halaman pembelian](https://purchase.aspose.com/buy) untuk mendapatkan kunci lisensi sementara.

## Menyiapkan Aspose.Cells untuk Java
Pertama, pastikan pustaka berada di classpath Anda. Setelah menambahkan dependensi, Anda dapat menginisialisasi API seperti ditunjukkan di bawah.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Panduan Implementasi

### Membuat dan mengkonfigurasi workbook
Kelas `Workbook` mewakili seluruh file Excel dalam memori.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Langkah 1: membuat instance workbook
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Ini membuat workbook baru yang kosong yang dapat Anda isi segera.

### Mengakses atau memodifikasi sel worksheet
`Worksheet` mewakili satu lembar dalam workbook, berisi sel, baris, dan kolom.  
Anda akan menuliskan data yang menggerakkan **pie chart** ke dalam worksheet.

#### Langkah 2: dapatkan worksheet pertama dan sel-selnya
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Isi sel dengan nama kategori dan nilai yang akan digunakan diagram.

### Membuat pie chart
Objek `Chart` memvisualisasikan data dalam worksheet dan mendukung berbagai tipe seperti pie, column, dan line.

#### Langkah 3: tambahkan pie chart ke worksheet
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Mengkonfigurasi seri dan data pie chart
`Series` mendefinisikan rentang data dan pemformatan untuk diagram, menghubungkan sel worksheet ke elemen visual.

#### Langkah 4: atur seri untuk diagram
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Mengkonfigurasi tampilan legenda dan judul diagram
`Legend` diagram menampilkan nama seri dan warna, membantu pembaca mengidentifikasi setiap irisan.

#### Langkah 5: sesuaikan legenda dan judul diagram
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Menyesuaikan warna seri diagram
`setAreaColor` mengatur warna isi irisan seri diagram menggunakan nilai RGB.

#### Langkah 6: ubah warna segmen pie
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Autofit kolom dan simpan workbook
`autoFitColumns` secara otomatis menyesuaikan lebar kolom agar sesuai dengan isi sel.

#### Langkah 7: sesuaikan lebar kolom dan simpan file
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Kasus penggunaan umum
- **Analisis demografis:** Menampilkan distribusi populasi di seluruh wilayah.
- **Pelaporan pangsa pasar:** Memvisualisasikan pangsa masing‑masing kompetitor dalam satu pandangan.
- **Alokasi anggaran:** Menyoroti bagaimana dana dibagi di antara departemen.

## Pertimbangan kinerja
- Lepaskan objek (`workbook.dispose()`) ketika tidak lagi diperlukan untuk membebaskan memori native.
- Untuk set data yang sangat besar, gunakan `WorkbookDesigner` untuk streaming data alih-alih memuat semuanya sekaligus.
- Profil dengan Java Flight Recorder untuk menemukan bottleneck dalam pembuatan diagram.

## Pertanyaan yang sering diajukan

**Q: Bisakah saya menghasilkan beberapa pie chart dalam satu workbook yang sama?**  
A: Ya, ulangi langkah pembuatan diagram untuk setiap rentang data; setiap diagram bersifat independen.

**Q: Apakah Aspose.Cells mendukung pie chart 3‑D?**  
A: Ya; set tipe diagram ke `ChartType.PIE_3D` saat menambahkan diagram.

**Q: Bagaimana cara menerapkan tema khusus ke semua diagram?**  
A: Gunakan metode `Workbook.setDefaultTheme` sebelum membuat diagram apa pun.

**Q: Format file apa yang dapat saya ekspor dari workbook?**  
A: Lebih dari 30 format, termasuk XLSX, CSV, PDF, dan HTML.

**Q: Apakah lisensi diperlukan untuk penyebaran komersial?**  
A: Ya, lisensi yang valid menghapus watermark evaluasi dan membuka semua fungsi.

## Kesimpulan
Anda kini memiliki resep lengkap, end‑to‑end untuk **create pie chart java** dengan Aspose.Cells. Dengan mengikuti langkah‑langkah di atas, Anda dapat menghasilkan **pie chart** Excel yang halus, menyesuaikan warna dan judul, serta menyematkannya ke dalam pipeline pelaporan apa pun. Jelajahi tipe diagram lain—column, line, radar—untuk memperluas toolkit visualisasi data Anda.

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## Tutorial Terkait

- [Sesuaikan Label Data Diagram Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Buat Diagram Excel Dinamis dengan Aspose.Cells Java: Panduan Komprehensif untuk Pengembang](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Buat dan Sesuaikan Workbook Excel Menggunakan Aspose.Cells Java: Panduan Langkah demi Langkah](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}