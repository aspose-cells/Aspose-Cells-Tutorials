---
"date": "2025-04-08"
"description": "Tutorial kode untuk Aspose.Words Java"
"title": "Aspose.Cells Java&#58; Membuat & Menyesuaikan Bagan"
"url": "/id/java/charts-graphs/aspose-cells-java-create-customize-charts/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Menguasai Pembuatan dan Kustomisasi Bagan dengan Aspose.Cells Java

Dalam dunia yang digerakkan oleh data saat ini, memvisualisasikan kumpulan data yang kompleks sangat penting untuk membuat keputusan yang tepat. Baik Anda seorang pengembang berpengalaman atau baru memulai, membuat bagan yang menarik dalam aplikasi Anda dapat meningkatkan pengalaman pengguna secara signifikan. Tutorial ini akan memandu Anda melalui proses penggunaan Aspose.Cells untuk Java untuk membuat dan menyesuaikan bagan dengan mudah.

## Apa yang Akan Anda Pelajari

- Cara mengatur Aspose.Cells untuk Java
- Membuat dan memberi nama lembar kerja
- Mengisi sel dengan data
- Menambahkan lembar bagan dan membuat bagan kolom
- Menyesuaikan bagan Anda dengan gambar, judul, dan konfigurasi seri
- Menyimpan buku kerja

Dengan langkah-langkah ini, Anda akan dapat membuat bagan yang menarik secara visual dalam waktu singkat.

## Prasyarat

Sebelum menyelami Aspose.Cells untuk Java, pastikan Anda memiliki:

- **Java Development Kit (JDK) 8 atau yang lebih baru** terinstal di komputer Anda.
- Pemahaman dasar tentang pemrograman Java dan keakraban dengan operasi Excel.
  
### Perpustakaan yang Diperlukan

Untuk memulai Aspose.Cells, sertakan dependensi berikut dalam alat manajemen proyek Anda.

#### Pakar
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Bahasa Inggris Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Akuisisi Lisensi

Aspose menawarkan uji coba gratis, yang memungkinkan Anda menguji fitur-fitur lengkap pustaka sebelum membeli. Anda juga dapat memperoleh lisensi sementara untuk pengujian ekstensif.

- **Uji Coba Gratis**: [Unduh Gratis](https://releases.aspose.com/cells/java/)
- **Lisensi Sementara**: [Minta di sini](https://purchase.aspose.com/temporary-license/)

## Menyiapkan Aspose.Cells untuk Java

Setelah lingkungan Anda siap, inisialisasi perpustakaan dengan membuat yang baru `Workbook` Misalnya. Ini akan menjadi dasar bagi perjalanan pembuatan bagan kita.

```java
import com.aspose.cells.Workbook;

// Inisialisasi Buku Kerja baru
Workbook workbook = new Workbook();
```

## Panduan Implementasi

### 1. Membuat dan Memberi Nama Lembar Kerja

#### Ringkasan
Mulailah dengan menyiapkan lembar data Anda, yang akan menampung semua data yang diperlukan untuk bagan tersebut.

#### Tangga:

**Buat Buku Kerja Baru**
```java
import com.aspose.cells.Worksheet;

// Buat contoh Buku Kerja baru
Workbook workbook = new Workbook();
```

**Beri Nama Lembar Kerja**

```java
// Akses lembar kerja pertama dan atur namanya menjadi "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Mengisi Sel dengan Data

#### Ringkasan
Mengisi data pada lembar kerja Anda penting untuk membuat bagan yang bermakna.

#### Tangga:

**Akses Koleksi Sel**

```java
import com.aspose.cells.Cells;

// Dapatkan koleksi sel dari lembar "Data"
Cells cells = sheet.getCells();
```

**Masukkan Data**

```java
// Masukkan nama wilayah dan angka penjualan
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Menambahkan Lembar Bagan

#### Ringkasan
Tambahkan lembar bagan khusus untuk memisahkan data dan visualisasi Anda.

#### Tangga:

**Buat Lembar Bagan**

```java
import com.aspose.cells.SheetType;

// Tambahkan lembar grafik baru
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Beri nama lembar kerja "Bagan"
chartSheet.setName("Chart");
```

### 4. Membuat Bagan

#### Ringkasan
Buat bagan kolom untuk memvisualisasikan data penjualan menurut wilayah.

#### Tangga:

**Buat Bagan Kolom**

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Tambahkan bagan kolom baru ke lembar "Bagan"
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Mengatur Gambar sebagai Isi Latar Belakang di Area Plot Grafik

#### Ringkasan
Tingkatkan daya tarik visual bagan Anda dengan menambahkan gambar latar belakang.

#### Tangga:

**Atur Data Gambar**

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

### 6. Mengonfigurasi Judul dan Seri Bagan

#### Ringkasan
Sesuaikan bagan Anda dengan judul, data seri, dan posisi legenda.

#### Tangga:

**Tetapkan Judul Bagan**

```java
// Konfigurasikan properti judul bagan
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

**Konfigurasikan Data Seri**

```java
// Tetapkan data seri dan kategori untuk bagan
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Posisikan legenda di bagian atas grafik
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 7. Menyimpan Buku Kerja

#### Ringkasan
Pastikan semua kerja keras Anda disimpan dengan mengekspor buku kerja.

#### Tangga:

**Simpan Buku Kerja**

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Aplikasi Praktis

- **Laporan Bisnis**: Buat laporan penjualan dan kinerja yang dinamis.
- **Alat Analisis Data**: Meningkatkan visualisasi data dalam perangkat lunak analitis.
- **Integrasi Dasbor**:Integrasikan grafik ke dalam dasbor untuk pembaruan waktu nyata.

## Pertimbangan Kinerja

- Optimalkan dengan meminimalkan jumlah operasi pada kumpulan data besar.
- Kelola memori secara efektif dengan segera membuang objek yang tidak digunakan.

## Kesimpulan

Anda kini telah menguasai pembuatan dan penyesuaian grafik menggunakan Aspose.Cells di Java. Untuk melanjutkan perjalanan Anda, jelajahi lebih banyak fitur seperti rentang data dinamis atau berbagai jenis grafik. 

## Bagian FAQ

1. **Bagaimana cara menambahkan beberapa seri ke bagan?**
   - Gunakan `add` metode pada `NSeries` dengan beberapa rentang.

2. **Bisakah saya menyesuaikan label sumbu grafik?**
   - Ya, akses dan konfigurasikan sumbu menggunakan `chart.getCategatauyAxis()` or `chart.getValueAxis()`.

3. **Bagaimana jika berkas gambar saya tidak ditampilkan dengan benar di area plot?**
   - Pastikan jalur berkas benar dan format gambar didukung oleh Aspose.Cells.

4. **Bagaimana cara menangani kumpulan data besar secara efisien?**
   - Pertimbangkan untuk membaca data dalam potongan dan memperbarui sel secara bertahap.

5. **Apakah mungkin untuk mengekspor grafik ke format lain seperti PDF atau PNG?**
   - Ya, gunakan `workbook.save()` dengan ekstensi file yang sesuai untuk format yang berbeda.

## Sumber daya

- [Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Unduh Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Beli Lisensi](https://purchase.aspose.com/buy)
- [Uji Coba Gratis](https://releases.aspose.com/cells/java/)
- [Permintaan Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- [Forum Dukungan](https://forum.aspose.com/c/cells/9)

Dengan mengikuti panduan ini, Anda akan dapat membuat dan menyesuaikan grafik dalam aplikasi Java menggunakan Aspose.Cells dengan mudah. Selamat membuat kode!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}