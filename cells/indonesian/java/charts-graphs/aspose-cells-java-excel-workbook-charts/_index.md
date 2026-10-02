---
date: '2026-04-11'
description: Pelajari otomatisasi Excel Java dengan Aspose.Cells. Tutorial ini menunjukkan
  cara membuat workbook Excel Java, mengisi data Excel Java, dan menyimpan file Excel
  Java dengan diagram.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Otomatisasi Excel Java: Membuat Buku Kerja & Diagram menggunakan Aspose'
url: /id/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Otomatisasi Excel Java: Membuat Workbook & Grafik menggunakan Aspose

## Pendahuluan

Mengotomatiskan tugas Excel dengan Java dapat menghemat jam kerja manual, terutama ketika Anda perlu menghasilkan laporan, dasbor, atau grafik berbasis data secara cepat. **Excel automation java** dengan Aspose.Cells memberi Anda API yang bersih dan berperforma tinggi yang menangani segala hal mulai dari pembuatan workbook hingga penataan grafik yang canggih. Dalam tutorial ini Anda akan belajar cara menyiapkan Aspose.Cells, **membuat workbook Excel java**, mengisinya dengan data, menambahkan grafik, menerapkan pemformatan 3‑D, dan akhirnya **menyimpan file Excel java**.

### Jawaban Cepat
- **Library mana yang menyederhanakan otomatisasi Excel di Java?** Aspose.Cells for Java.  
- **Bisakah saya menambahkan grafik 3‑D secara programatis?** Ya – API mendukung pemformatan 3‑D dan efek pencahayaan.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi percobaan gratis tersedia; lisensi komersial diperlukan untuk produksi.  
- **Alat build Java apa yang didukung?** Maven dan Gradle keduanya didukung sepenuhnya.  
- **Format file apa yang dapat saya ekspor?** XLS, XLSX, CSV, PDF, dan banyak lagi.

## Apa itu otomatisasi Excel java?

Otomatisasi Excel java mengacu pada proses menghasilkan, memodifikasi, dan menyimpan workbook Excel secara programatis menggunakan kode Java. Ini menghilangkan pengeditan spreadsheet manual, memastikan konsistensi, dan memungkinkan integrasi dengan sistem lain seperti basis data atau layanan web.

## Mengapa menggunakan Aspose.Cells untuk Java?

- **Set fitur lengkap** – mulai dari nilai sel sederhana hingga grafik kompleks, tabel pivot, dan pemformatan bersyarat.  
- **Tanpa ketergantungan Microsoft Office** – berfungsi di lingkungan server mana pun.  
- **Performa tinggi** – dioptimalkan untuk set data besar dan skenario multi‑thread.  
- **Dukungan format luas** – membaca/menulis XLS, XLSX, ODS, CSV, PDF, HTML, dan lainnya.

## Prasyarat

- **Java Development Kit (JDK) 8+**  
- **Maven atau Gradle** untuk manajemen dependensi  
- **Aspose.Cells for Java 25.3 atau lebih baru** (trial atau berlisensi)  

## Menyiapkan Aspose.Cells untuk Java

Tambahkan pustaka ke proyek Anda menggunakan salah satu konfigurasi berikut.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Akuisisi Lisensi

Minta lisensi percobaan gratis dari situs web Aspose, atau beli lisensi penuh untuk penggunaan produksi. Tempatkan file lisensi di proyek Anda dan muat pada saat runtime.

## Inisialisasi dan Penyiapan Dasar

Setelah dependensi teratasi, Anda dapat mulai menulis kode.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Panduan Langkah‑per‑Langkah

### Langkah 1: Cara membuat workbook excel java

Buat instance workbook baru yang akan menampung semua lembar kerja Anda.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Langkah 2: Tambahkan lembar kerja (termasuk lembar grafik)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Langkah 3: Cara mengisi data excel java

Masukkan data contoh yang akan direferensikan oleh grafik.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Langkah 4: Tambahkan grafik kolom ke workbook

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Langkah 5: Terapkan pemformatan warna ke area grafik

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Langkah 6: Konfigurasikan legenda dan seri data

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Langkah 7: Terapkan pemformatan 3D ke seri

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Langkah 8: Atur warna seri untuk perbedaan visual yang lebih baik

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Langkah 9: Cara menyimpan file excel java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Aplikasi Praktis

- **Pelaporan Keuangan** – Hasilkan pernyataan kuartalan dengan grafik dinamis.  
- **Dasbor Analisis Data** – Bangun dasbor interaktif yang menyegarkan secara otomatis.  
- **Manajemen Inventaris** – Ekspor tingkat stok dan tren ke Excel untuk tinjauan pemangku kepentingan.  
- **Perencanaan Proyek** – Buat grafik gaya Gantt langsung dari sistem penjadwalan berbasis Java.

## Tips Kinerja untuk Otomatisasi Excel Java

- **Gunakan Kembali Objek Workbook** saat memproses banyak lembar untuk mengurangi beban memori.  
- **Pembaruan Sel secara Batch** menggunakan `Cells.importArray` untuk set data besar alih-alih panggilan `putValue` individual.  
- **Buang Sumber Daya** dengan memanggil `book.dispose()` setelah menyimpan file besar.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menghasilkan XLSX alih-alih XLS?**  
A: Ya – cukup ubah ekstensi file di `book.save("output.xlsx")`; Aspose secara otomatis memilih format yang tepat.

**Q: Apakah lisensi diperlukan untuk pengembangan?**  
A: Lisensi percobaan gratis dapat digunakan untuk pengembangan dan pengujian. Penyebaran produksi memerlukan lisensi yang dibeli.

**Q: Bagaimana cara menambahkan lebih banyak jenis grafik?**  
A: Gunakan enum `ChartType` (mis., `ChartType.PIE`, `ChartType.LINE`) saat memanggil `charts.add(...)`.

**Q: Bagaimana jika saya perlu melindungi workbook?**  
A: Panggil `book.getSettings().setPassword("yourPassword")` sebelum menyimpan.

**Q: Apakah Aspose.Cells mendukung file yang mendukung macro?**  
A: Ya – Anda dapat membuat atau mempertahankan makro VBA dalam workbook XLSM.

---

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}