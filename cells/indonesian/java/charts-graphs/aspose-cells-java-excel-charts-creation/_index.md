---
date: '2026-04-08'
description: Pelajari cara membuat diagram garis dengan penanda menggunakan Aspose.Cells
  untuk Java, menambahkan diagram ke lembar kerja, dan menyesuaikan diagram Excel
  untuk pelaporan otomatis.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Buat Diagram Garis dengan Penanda Menggunakan Aspose.Cells untuk Java
url: /id/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Membuat dan Menata Grafik Excel dengan Aspose.Cells Java

## Pendahuluan

Di dunia yang didorong oleh data saat ini, **line chart with markers** adalah salah satu cara paling efektif untuk memvisualisasikan tren dan outlier. Baik Anda membuat laporan otomatis atau dasbor yang diperbarui setiap hari, kemampuan untuk secara programatis menambahkan line chart with markers ke lembar kerja menghemat banyak langkah manual. Tutorial ini memandu Anda menggunakan Aspose.Cells untuk Java untuk membuat, menata, dan mengekspor grafik tersebut, sehingga Anda dapat fokus pada wawasan alih‑alih mengutak‑atik Excel yang membosankan.

**Apa yang Akan Anda Pelajari**
- Menginisialisasi workbook dan mengisinya dengan data menggunakan Aspose.Cells.  
- **Cara menambahkan line chart dengan markers ke worksheet** dan mengonfigurasi tampilannya.  
- Menyesuaikan warna seri, marker, dan opsi penataan lainnya.  
- Menyimpan workbook sebagai file Excel yang mencakup grafik yang telah ditata.

## Jawaban Cepat
- **Apa kelas utama untuk memulai?** `Workbook` menginisialisasi file Excel baru.  
- **Jenis grafik mana yang membuat line chart dengan markers?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Bagaimana cara mengatur warna khusus untuk titik seri?** Gunakan `chart.getNSeries().setColorVaried(true)` dan atur warna area marker.  
- **Apakah saya memerlukan lisensi untuk fungsionalitas penuh?** Ya, lisensi Aspose.Cells berbayar atau sementara menghapus batas evaluasi.  
- **Bisakah saya mengekspor hasil sebagai XLSX?** Tentu—`workbook.save("StyledChart.xlsx")` membuat file XLSX.

## Prasyarat

Sebelum membuat dan menata grafik menggunakan Aspose.Cells untuk Java, pastikan Anda memiliki pengaturan berikut:

### Perpustakaan yang Diperlukan
Sertakan Aspose.Cells sebagai dependensi dalam proyek Anda. Berikut adalah petunjuk untuk pengguna Maven dan Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Persyaratan Penyiapan Lingkungan
- Java Development Kit (JDK) terpasang di sistem Anda.  
- Integrated Development Environment (IDE) seperti IntelliJ IDEA atau Eclipse untuk menulis kode dan pengujian.

### Prasyarat Pengetahuan
Pemahaman dasar tentang pemrograman Java diperlukan, bersama dengan familiaritas dengan workbook Excel dan konsep pembuatan grafik.

### Akuisisi Lisensi
Aspose.Cells adalah produk komersial yang memerlukan lisensi untuk fungsionalitas penuh. Anda dapat memperoleh percobaan gratis untuk mengevaluasi fiturnya, meminta lisensi sementara untuk pengujian yang lebih lama, atau membeli produk untuk penggunaan jangka panjang.

- **Percobaan Gratis:** [Unduh Percobaan Gratis](https://releases.aspose.com/cells/java/)  
- **Lisensi Sementara:** [Minta Lisensi Sementara](https://purchase.aspose.com/temporary-license/)  
- **Beli:** [Beli Aspose.Cells](https://purchase.aspose.com/buy)

## Menyiapkan Aspose.Cells untuk Java

Setelah Anda menginstal dependensi yang diperlukan, siapkan lingkungan pengembangan Anda untuk menggunakan Aspose.Cells. Mulailah dengan mengimpor perpustakaan dan menginisialisasi objek `Workbook` dalam aplikasi Java Anda:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Panduan Implementasi

Pada bagian ini, kami akan memecah implementasi menjadi fitur-fitur terpisah: Inisialisasi Workbook dan Pengisian Data, Pembuatan dan Konfigurasi Grafik, Kustomisasi Seri, dan Penyimpanan Workbook.

### Fitur 1: Inisialisasi Workbook dan Pengisian Data

**Gambaran Umum:** Fitur ini berfokus pada pembuatan workbook baru, mengakses worksheet pertama, dan mengisinya dengan data untuk pembuatan grafik.

#### Langkah 1: Inisialisasi Workbook
Mulailah dengan membuat instance objek `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Langkah 2: Atur Judul Kolom dan Isi Data
Tentukan judul kolom dan isi baris dengan data contoh:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Fitur 2: Pembuatan dan Konfigurasi Grafik

**Gambaran Umum:** Fitur ini menunjukkan cara menambahkan grafik ke worksheet workbook, mengatur gaya, dan mengonfigurasi properti dasar.

#### Langkah 3: Tambahkan Grafik ke Worksheet
Tambahkan line chart dengan data markers:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Fitur 3: Konfigurasi dan Kustomisasi Seri

**Gambaran Umum:** Tingkatkan daya tarik visual grafik Anda dengan menyesuaikan pengaturan seri, seperti warna beragam dan gaya marker.

#### Langkah 4: Kustomisasi Pengaturan Seri
Konfigurasikan data seri, terapkan pemformatan khusus, dan sesuaikan marker:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Fitur 4: Penyimpanan Workbook

**Gambaran Umum:** Akhirnya, simpan workbook untuk mempertahankan perubahan Anda dan memastikan grafik termasuk dalam file Excel.

#### Langkah 5: Simpan Workbook
Simpan workbook Anda dengan grafik yang baru dibuat:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Masalah Umum dan Pemecahan Masalah
- **Grafik muncul kosong:** Verifikasi bahwa rentang sel yang digunakan dalam `setXValues` dan `setValues` benar‑benar merujuk ke sel yang terisi.  
- **Warna tidak diterapkan:** Pastikan `chart.getNSeries().setColorVaried(true)` dipanggil sebelum menyesuaikan seri individual.  
- **Kesalahan lisensi:** Lisensi percobaan mungkin membatasi jumlah grafik; instal lisensi penuh untuk menghapus batasan.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya membuat tipe grafik lain (mis., batang, pai) dengan Aspose.Cells?**  
A: Ya, Aspose.Cells mendukung berbagai tipe grafik; cukup ganti `ChartType.LINE_WITH_DATA_MARKERS` dengan nilai enum yang diinginkan.

**Q: Apakah saya perlu menutup workbook atau melepaskan sumber daya?**  
A: Kelas `Workbook` mengelola sumber daya secara otomatis, tetapi Anda dapat memanggil `workbook.dispose()` dalam aplikasi yang berjalan lama untuk membebaskan memori.

**Q: Apakah memungkinkan menambahkan beberapa grafik ke worksheet yang sama?**  
A: Tentu—panggil `worksheet.getCharts().add(...)` untuk setiap grafik yang ingin Anda sisipkan.

**Q: Bagaimana cara mengekspor file sebagai format Excel lama (XLS)?**  
A: Gunakan `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Q: Apakah grafik akan mempertahankan penataannya saat dibuka di Microsoft Excel?**  
A: Ya, Aspose.Cells menulis objek grafik Excel asli, sehingga semua gaya, warna, dan marker muncul persis seperti yang didefinisikan.

---

**Terakhir Diperbarui:** 2026-04-08  
**Diuji Dengan:** Aspose.Cells 25.3 untuk Java  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}