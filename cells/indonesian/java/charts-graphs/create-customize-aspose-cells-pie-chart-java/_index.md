---
"date": "2025-04-08"
"description": "Pelajari cara membuat dan menyesuaikan diagram lingkaran menggunakan Aspose.Cells untuk Java. Panduan langkah demi langkah dengan contoh kode untuk pengembang."
"title": "Menguasai Aspose.Cells&#58; Membuat & Menyesuaikan Diagram Lingkaran di Java"
"url": "/id/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Menguasai Aspose.Cells: Membuat & Menyesuaikan Diagram Lingkaran di Java

## Perkenalan
Membuat diagram yang menarik secara visual merupakan persyaratan umum saat menangani visualisasi data di Excel. Baik saat Anda menyajikan informasi demografis atau menganalisis tren pasar, diagram pai menawarkan cara yang jelas untuk merepresentasikan data proporsional. Namun, menyiapkan diagram ini secara terprogram bisa jadi rumit. Tutorial ini memandu Anda dalam membuat dan menyesuaikan Diagram Pai Aspose.Cells menggunakan Java, yang menyederhanakan proses bagi para pengembang.

**Apa yang Akan Anda Pelajari:**
- Siapkan lingkungan Anda dengan Aspose.Cells untuk Java.
- Buat buku kerja baru dan akses sel lembar kerja.
- Isi data ke dalam sel tertentu untuk persiapan pembuatan bagan.
- Buat diagram lingkaran dari data ini.
- Sesuaikan tampilan diagram lingkaran Anda, termasuk warna, judul, dan legenda.

Sebelum memulai, pastikan Anda memiliki pemahaman dasar tentang pemrograman Java dan manajemen dependensi Maven atau Gradle. Mari kita siapkan lingkungan kita!

## Prasyarat
Untuk mengikuti tutorial ini, Anda memerlukan:
- **Kit Pengembangan Java (JDK)**: Versi 8 atau lebih tinggi.
- **Lingkungan Pengembangan Terpadu (IDE)**Seperti IntelliJ IDEA atau Eclipse.
- **Manajemen Ketergantungan**: Gunakan Maven atau Gradle untuk mengelola dependensi Anda.

### Pustaka dan Ketergantungan yang Diperlukan
Pastikan untuk menyertakan Aspose.Cells untuk Java dalam proyek Anda menggunakan Maven atau Gradle.

**Pakar**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Bahasa Inggris Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Langkah-langkah Memperoleh Lisensi
Aspose.Cells untuk Java adalah pustaka komersial, tetapi Anda dapat memulai dengan uji coba gratis atau mengajukan lisensi sementara. Kunjungi [halaman pembelian](https://purchase.aspose.com/buy) untuk menjelajahi pilihan perizinan.

## Menyiapkan Aspose.Cells untuk Java
Pertama-tama, pastikan lingkungan proyek Anda menyertakan pustaka yang diperlukan dengan menambahkannya melalui Maven atau Gradle seperti yang ditunjukkan di atas. Setelah disertakan, Anda dapat menginisialisasi Aspose.Cells:

```java
import com.aspose.cells.Workbook;

// Inisialisasi contoh buku kerja baru
Workbook workbook = new Workbook();
```

## Panduan Implementasi

### Membuat dan Mengonfigurasi Buku Kerja
Membuat buku kerja adalah langkah awal di mana Anda menyiapkan data Anda.

#### Impor Perpustakaan
Pastikan impor ini disertakan di bagian atas berkas Anda:

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

#### Langkah 1: Buat Contoh Buku Kerja
```java
// Membuat contoh buku kerja kosong untuk digunakan.
Workbook workbook = new Workbook();
```
Langkah ini menginisialisasi berkas Excel Anda secara terprogram, memungkinkan Anda untuk memanipulasinya menggunakan fungsionalitas Aspose.Cells.

### Mengakses atau Memodifikasi Sel Lembar Kerja
Berikutnya, isi data ke dalam sel lembar kerja yang akan digunakan untuk diagram lingkaran.

#### Langkah 2: Mengakses Lembar Kerja dan Sel-selnya
```java
// Akses lembar kerja pertama dalam buku kerja.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Masukkan nilai sampel yang digunakan untuk diagram lingkaran ke dalam sel tertentu.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Masukkan nilai persentase untuk diagram lingkaran ke dalam sel tertentu.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Di sini, Anda mengisi lembar kerja dengan data yang akan mewakili berbagai segmen diagram lingkaran.

### Membuat Diagram Lingkaran

#### Langkah 3: Tambahkan Diagram Lingkaran ke Lembar Kerja
```java
// Buat diagram lingkaran pada lembar kerja.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Langkah ini menambahkan diagram lingkaran baru ke lembar kerja Anda pada posisi dan dimensi yang ditentukan.

### Konfigurasikan Seri dan Data Diagram Lingkaran

#### Langkah 4: Mengatur Seri untuk Bagan
```java
// Konfigurasikan rentang data seri untuk bagan.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Tautkan judul diagram lingkaran ke sel yang berisi teks judul.
pie.getTitle().setLinkedSource("D2");
```
Kode ini menghubungkan rentang data Anda dan menyiapkan seri untuk diagram lingkaran.

### Konfigurasikan Legenda dan Tampilan Judul Bagan

#### Langkah 5: Sesuaikan Legenda dan Judul Bagan
```java
// Tetapkan posisi legenda di bagian bawah bagan.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Tetapkan properti font untuk judul bagan.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Menyesuaikan tampilan meningkatkan keterbacaan dan daya tarik visual.

### Sesuaikan Warna Seri Bagan

#### Langkah 6: Ubah Warna Segmen Pai
```java
import com.aspose.cells.Color;

// Akses dan sesuaikan warna segmen diagram lingkaran individual.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Pengaturan ini mempersonalisasi bagan Anda agar sesuai dengan skema warna tertentu.

### Sesuaikan Kolom Secara Otomatis dan Simpan Buku Kerja

#### Langkah 7: Sesuaikan Lebar Kolom dan Simpan File
```java
// Sesuaikan otomatis semua kolom.
worksheet.autoFitColumns();

// Tentukan jalur tempat penampung direktori keluaran untuk menyimpan buku kerja.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Simpan buku kerja yang dimodifikasi ke file Excel di direktori yang ditentukan.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Terakhir, sesuaikan kolom secara otomatis dan simpan buku kerja Anda.

## Aplikasi Praktis
1. **Analisis Demografi**: Gunakan diagram lingkaran untuk menampilkan distribusi populasi di berbagai negara atau wilayah.
2. **Laporan Pangsa Pasar**: Mengilustrasikan pangsa pasar berbagai perusahaan di suatu sektor.
3. **Alokasi Anggaran**: Visualisasikan bagaimana anggaran dialokasikan di berbagai departemen dalam suatu organisasi.

Aplikasi ini menunjukkan fleksibilitas dan kegunaan Aspose.Cells dalam skenario dunia nyata.

## Pertimbangan Kinerja
Untuk mengoptimalkan kinerja saat menggunakan Aspose.Cells:
- Minimalkan penggunaan memori dengan membuang objek yang tidak lagi diperlukan.
- Gunakan struktur data yang efisien untuk memproses kumpulan data besar.
- Profilkan aplikasi Anda untuk mengidentifikasi hambatan.

Mematuhi praktik terbaik memastikan aplikasi berjalan lancar dan responsif.

## Kesimpulan
Tutorial ini memandu Anda melalui langkah-langkah untuk membuat dan menyesuaikan diagram pai menggunakan Aspose.Cells di Java. Dengan pengetahuan ini, Anda sekarang dapat menerapkan teknik-teknik ini ke berbagai tugas visualisasi data dalam proyek Anda. Untuk eksplorasi lebih lanjut, pertimbangkan untuk mempelajari jenis-jenis diagram tambahan dan opsi penyesuaian lanjutan yang tersedia dengan Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}