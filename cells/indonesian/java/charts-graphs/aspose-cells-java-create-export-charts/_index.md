---
date: '2026-04-05'
description: Pelajari cara membuat diagram di Java dengan Aspose.Cells, mengonversi
  diagram Excel menjadi gambar, dan mengekspor diagram secara efisien.
keywords:
- how to create chart
- excel chart to image
- convert excel chart
- aspose cells chart
- how to export chart
- create chart java
title: Cara Membuat Grafik dan Mengekspor sebagai Gambar di Java Menggunakan Aspose.Cells
  – Panduan Lengkap
url: /id/java/charts-graphs/aspose-cells-java-create-export-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Grafik dan Mengekspor sebagai Gambar di Java Menggunakan Aspose.Cells – Panduan Lengkap

## Pendahuluan

Jika Anda mencari cara yang dapat diandalkan **cara membuat grafik** objek langsung dari kode Java, Aspose.Cells for Java mempermudahnya. Dalam tutorial ini Anda akan belajar cara membuat pyramid chart, mengonfigurasi output gambar resolusi tinggi, dan akhirnya mengekspor grafik sebagai gambar PNG. Pada akhir tutorial Anda juga akan memahami cara **mengonversi grafik excel** ke file gambar dan mengapa pendekatan ini ideal untuk pelaporan otomatis.

**Apa yang Akan Anda Pelajari**
- Menyiapkan Aspose.Cells untuk Java
- Membuat pyramid chart dalam workbook Excel menggunakan Java
- Mengonfigurasi opsi output gambar untuk rendering berkualitas tinggi
- Mengekspor grafik sebagai gambar untuk dasbor, email, atau PDF

Sekarang mari kita tinjau prasyarat dan menyiapkan lingkungan Anda.

## Jawaban Cepat
- **Perpustakaan apa yang dibutuhkan?** Aspose.Cells for Java (v25.3+)
- **Jenis grafik apa yang ditunjukkan?** Pyramid chart (Anda dapat beralih ke jenis lain)
- **Bagaimana mengekspor grafik?** Gunakan `Chart.toImage()` dengan `ImageOrPrintOptions`
- **Bisakah saya mengekspor ke format lain?** Ya – PNG, JPEG, BMP, GIF, dan TIFF didukung
- **Apakah saya memerlukan lisensi?** Lisensi percobaan gratis dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi

## Apa itu “cara membuat grafik” dengan Aspose.Cells?
Aspose.Cells menyediakan API yang kaya yang memungkinkan pengembang secara program menghasilkan lembar kerja Excel, menambahkan grafik, dan merendernya sebagai gambar—semua tanpa perlu menginstal Microsoft Office. Hal ini membuatnya sempurna untuk pelaporan sisi server, dasbor analitik data, dan pembuatan dokumen otomatis.

## Mengapa menggunakan Aspose.Cells untuk mengonversi grafik Excel ke gambar?
- **Tidak bergantung pada Office:** Berjalan di platform apa pun yang mendukung Java.
- **Rendering dengan fidelitas tinggi:** Mendukung anti‑aliasing dan pengaturan DPI untuk gambar yang tajam.
- **Dukungan format luas:** Mengekspor ke PNG, JPEG, SVG, PDF, dan lainnya.
- **Berorientasi kinerja:** Bekerja secara efisien dengan workbook besar dan dapat digabungkan dengan multi‑threading.

## Prasyarat
- **Perpustakaan yang Diperlukan:** Aspose.Cells for Java versi 25.3 atau lebih tinggi.
- **IDE:** IntelliJ IDEA, Eclipse, atau IDE kompatibel Java apa pun.
- **JDK:** Java 8 atau lebih baru.
- **Pengetahuan Dasar:** Familiaritas dengan Java, Maven/Gradle, dan konsep file Excel.

## Menyiapkan Aspose.Cells untuk Java

### Maven
Tambahkan dependensi berikut ke file `pom.xml` Anda:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Sertakan baris ini dalam file `build.gradle` Anda:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

**Perolehan Lisensi:** Aspose.Cells menawarkan lisensi percobaan gratis, yang dapat Anda dapatkan dari [halaman pembelian](https://purchase.aspose.com/buy) mereka. Terapkan lisensi sementara untuk membuka semua fungsi selama pengembangan.

### Inisialisasi Dasar
Untuk memulai, buat instance `Workbook`. Objek ini akan menyimpan data dan grafik Anda:
```java
import com.aspose.cells.Workbook;

public class AsposeCellsInit {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        // Your chart creation code will go here.
    }
}
```

## Cara Membuat Grafik di Java dengan Aspose.Cells

### Membuat Pyramid Chart di Excel

#### Langkah 1: Inisialisasi Workbook dan Worksheet
Pertama, siapkan workbook dan dapatkan referensi ke worksheet default.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY"; // Update with your directory path

Workbook workbook = new Workbook();
WorksheetCollection worksheets = workbook.getWorksheets();
```

#### Langkah 2: Tambahkan Pyramid Chart
Gunakan `ChartCollection` untuk menyisipkan pyramid chart. Ini menunjukkan proses pembuatan **aspose cells chart**.
```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

Worksheet sheet = worksheets.get(0);
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.PYRAMID, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);
```

## Mengonfigurasi Opsi Output Gambar (Cara Mengekspor Grafik)

### Langkah 1: Atur Resolusi dan Antialiasing
Sesuaikan pengaturan rendering untuk konversi **excel chart to image** yang tajam.
```java
import com.aspose.cells.ImageOrPrintOptions;
import java.awt.RenderingHints;

ImageOrPrintOptions options = new ImageOrPrintOptions();
options.setVerticalResolution(300);
options.setHorizontalResolution(300);
options.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
options.setRenderingHint(RenderingHints.KEY_TEXT_ANTIALIASING, RenderingHints.VALUE_TEXT_ANTIALIAS_ON);
```

## Mengekspor Grafik sebagai Gambar (Mengonversi Grafik Excel)

### Langkah 1: Simpan Grafik sebagai Gambar
Akhirnya, tulis grafik ke file PNG menggunakan opsi yang telah dikonfigurasi sebelumnya.
```java
chart.toImage(dataDir + "chart.png", options);
```

**Tips Pemecahan Masalah**
- Verifikasi bahwa `dataDir` mengarah ke folder yang dapat ditulisi.
- Pastikan versi Aspose.Cells Anda adalah 25.3 atau lebih baru; versi lama mungkin tidak memiliki overload `toImage` yang digunakan di sini.

## Aplikasi Praktis
Berikut adalah skenario umum di mana kemampuan **how to export chart** bersinar:
1. **Pelaporan Bisnis:** Menghasilkan dasbor penjualan bulanan secara otomatis.
2. **Alat Pendidikan:** Membuat laporan kinerja visual untuk siswa.
3. **Analitik Kesehatan:** Merender statistik pasien untuk presentasi tanpa pekerjaan manual di Excel.

Kasus penggunaan ini menggambarkan mengapa pengembang memilih Aspose.Cells untuk pembuatan grafik sisi server dan ekspor gambar.

## Pertimbangan Kinerja
Saat meningkatkan skala:
- Buang objek `Workbook` yang tidak terpakai untuk membebaskan memori.
- Gunakan API streaming untuk kumpulan data yang besar.
- Paralelkan pembuatan grafik saat menghasilkan banyak laporan secara bersamaan.

Mengikuti tips ini memastikan layanan Java Anda tetap responsif bahkan di bawah beban berat.

## Kesimpulan
Anda kini memiliki dasar yang kuat untuk objek **cara membuat grafik**, menyesuaikan rendering, dan **mengekspor grafik** sebagai gambar menggunakan Aspose.Cells untuk Java. Bereksperimenlah dengan nilai `ChartType` lain, terapkan gaya, atau integrasikan output PNG ke PDF, halaman web, atau lampiran email.

**Langkah Selanjutnya**
- Coba grafik garis, batang, atau pai dengan mengganti `ChartType.PYRAMID`.
- Jelajahi kelas `Chart` untuk penyesuaian judul, legenda, dan sumbu.
- Bergabunglah dengan komunitas untuk wawasan yang lebih mendalam.

Pertimbangkan mengunjungi [forum Aspose](https://forum.aspose.com/c/cells/9) untuk tips tambahan dan contoh dunia nyata.

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara menambahkan jenis grafik yang berbeda?**  
J: Gunakan nilai lain dari enumerasi `ChartType`, seperti `ChartType.BAR` atau `ChartType.PIE`.

**T: Bisakah saya menghasilkan grafik dari file Excel yang sudah ada?**  
J: Ya. Muat workbook dengan `new Workbook("existing.xlsx")` dan kemudian tambahkan atau modifikasi grafik.

**T: Apa jebakan umum saat menggunakan **excel chart to image**?**  
J: Jalur file yang salah, izin menulis yang tidak cukup, atau menggunakan versi Aspose.Cells yang lebih lama dari 25.3.

**T: Bagaimana saya dapat menangani workbook yang sangat besar secara efisien?**  
J: Manfaatkan API streaming Aspose.Cells dan buang objek dengan cepat untuk menjaga penggunaan memori tetap rendah.

**T: Apakah memungkinkan untuk menyesuaikan judul atau legenda grafik?**  
J: Tentu saja. Kelas `Chart` menyediakan metode seperti `setTitle()`, `setLegend()`, dan `setSeries()` untuk penyesuaian penuh.

---

**Terakhir Diperbarui:** 2026-04-05  
**Diuji Dengan:** Aspose.Cells for Java 25.3  
**Penulis:** Aspose  

**Sumber Daya**
- [Dokumentasi](https://reference.aspose.com/cells/java/)
- [Unduh Aspose.Cells untuk Java](https://releases.aspose.com/cells/java/)
- [Beli Lisensi](https://purchase.aspose.com/buy)
- [Unduhan Percobaan Gratis](https://releases.aspose.com/cells/java/)
- [Dapatkan Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- [Forum Dukungan](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}