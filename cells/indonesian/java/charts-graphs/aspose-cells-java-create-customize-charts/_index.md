---
date: '2026-04-08'
description: Pelajari cara menghasilkan diagram kolom di Java menggunakan Aspose.Cells,
  meliputi membuat diagram Java, menambahkan lembar diagram, dan mengekspor buku kerja
  Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Buat Diagram Kolom dengan Tutorial Aspose.Cells Java
url: /id/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Buat Diagram Kolom dengan Aspose.Cells Java

Dalam aplikasi berbasis data saat ini, **menghasilkan diagram kolom** dengan cepat dan secara programatik dapat mengubah angka mentah menjadi wawasan visual yang jelas. Apakah Anda membangun dasbor pelaporan, alat analitik, atau fitur ekspor sederhana, Aspose.Cells untuk Java memberikan API yang mudah digunakan untuk **create chart java** proyek tanpa harus berurusan dengan UI Excel. Dalam tutorial ini Anda akan belajar cara menyiapkan pustaka, **populate Excel cells**, menambahkan **chart sheet**, menyesuaikan **chart title**, dan akhirnya **export workbook excel** ke sebuah file.

## Jawaban Cepat
- **What does “generate column chart” mean?** Ini membuat visualisasi tipe batang vertikal dari data tabel.  
- **Which library is required?** Aspose.Cells for Java (trial gratis tersedia).  
- **Do I need an Excel installation?** Tidak, pustaka ini bekerja secara independen dari Microsoft Excel.  
- **Can I export to formats other than XLS?** Ya – PDF, PNG, SVG, dll., via `workbook.save()`.  
- **Is a license mandatory for production?** Ya, lisensi yang dibeli atau lisensi sementara diperlukan.

## Apa itu generate column chart?
Diagram kolom menampilkan rangkaian data sebagai batang vertikal, memudahkan perbandingan nilai antar kategori seperti wilayah, bulan, atau lini produk. Aspose.Cells memungkinkan Anda membangun diagram ini sepenuhnya dengan kode, memberi Anda kontrol penuh atas data, gaya, dan format output.

## Mengapa menggunakan Aspose.Cells untuk create chart java?
- **No COM interop** – berfungsi pada semua OS dengan JVM.  
- **Rich styling options** – gambar, gradien, legenda, dan font khusus.  
- **High performance** – cocok untuk dataset besar.  
- **Multiple export formats** – XLS, XLSX, PDF, PNG, dan lainnya.

## Prasyarat
- **Java Development Kit (JDK) 8+** terpasang.  
- Pengetahuan dasar Java dan familiaritas dengan konsep Excel.

### Perpustakaan yang Diperlukan
Tambahkan Aspose.Cells ke proyek Anda menggunakan salah satu potongan kode di bawah.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Perolehan Lisensi
Aspose menawarkan trial gratis dan lisensi sementara untuk pengujian ekstensif.

- **Free Trial**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Request Here](https://purchase.aspose.com/temporary-license/)

## Menyiapkan Aspose.Cells untuk Java

Pertama, buat instance `Workbook` – ini akan menjadi kanvas untuk data dan diagram kami.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Panduan Langkah‑per‑Langkah

### 1. Buat dan Beri Nama Worksheet
Kami akan menyimpan data mentah di lembar yang disebut **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Isi Sel Excel
Masukkan nama wilayah dan angka penjualan yang akan divisualisasikan oleh diagram kolom.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Tambahkan Chart Sheet
Memisahkan diagram dari data mentah membuat workbook tetap rapi.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Buat Diagram Kolom
Sekarang kami benar‑benar membuat objek **generate column chart**.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Atur Gambar sebagai Isi Latar Belakang di Area Plot
Gambar latar belakang dapat membuat diagram lebih menonjol.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Atur Judul Diagram
Menyesuaikan **set chart title** meningkatkan keterbacaan.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Konfigurasikan Data Seri dan Legenda
Hubungkan rentang data ke diagram dan atur posisi legenda.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Ekspor Workbook Excel
Akhirnya, **export workbook excel** ke file XLS (atau format lain yang didukung).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Aplikasi Praktis
- **Business Reports** – Membuat diagram penjualan secara otomatis untuk PDF bulanan.  
- **Data Analysis Tools** – Menyematkan diagram dinamis dalam dasbor analitik khusus.  
- **Enterprise Dashboards** – Memperbarui gambar diagram secara langsung untuk pemantauan waktu nyata.

## Pertimbangan Kinerja
- Lakukan pembaruan sel secara batch saat bekerja dengan dataset besar untuk mengurangi beban.  
- Lepaskan sumber daya (`workbook.dispose()`) jika Anda memproses banyak workbook dalam loop.  

## Masalah Umum dan Solusinya
- **Image not showing** – Verifikasi jalur file dan pastikan format gambar (PNG, JPEG) didukung.  
- **Chart appears blank** – Pastikan referensi rentang data (`Data!B2:B8`) sesuai dengan sel yang telah diisi.  
- **Out‑of‑memory errors** – Proses data dalam potongan dan panggil `System.gc()` setelah penyimpanan besar.

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana cara menambahkan beberapa seri ke diagram kolom?**  
A: Panggil `chart.getNSeries().add()` berulang kali dengan rentang data yang berbeda, misalnya, `"Data!C2:C8"` untuk seri kedua.

**Q: Bisakah saya mengubah label sumbu?**  
A: Ya. Gunakan `chart.getCategoryAxis().setTitle("Regions")` dan `chart.getValueAxis().setTitle("Sales")`.

**Q: Format apa yang dapat saya ekspor selain XLS?**  
A: Gunakan `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, atau `workbook.save("chart.xlsx")` untuk PDF, PNG, dan XLSX masing‑masing.

**Q: Apakah lisensi diperlukan untuk build pengembangan?**  
A: Trial gratis dapat digunakan untuk evaluasi, tetapi lisensi permanen atau sementara diperlukan untuk penerapan produksi.

**Q: Bagaimana cara meningkatkan kecepatan rendering untuk ribuan baris?**  
A: Isi sel menggunakan `cells.importArray()` dan minimalkan penggambaran ulang diagram dengan membuat diagram setelah semua data dimuat.

---

**Terakhir Diperbarui:** 2026-04-08  
**Diuji Dengan:** Aspose.Cells 25.3 for Java  
**Penulis:** Aspose  

## Sumber Daya

- [Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Unduh Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Beli Lisensi](https://purchase.aspose.com/buy)
- [Trial Gratis](https://releases.aspose.com/cells/java/)
- [Permintaan Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- [Forum Dukungan](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}