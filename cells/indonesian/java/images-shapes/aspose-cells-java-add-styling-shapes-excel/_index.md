---
"date": "2025-04-07"
"description": "Pelajari cara menambahkan dan menata bentuk seperti persegi panjang di Excel menggunakan pustaka Aspose.Cells yang canggih dengan Java. Panduan ini mencakup semuanya mulai dari penyiapan hingga penerapan."
"title": "Cara Menambahkan dan Menata Bentuk di Excel Menggunakan Aspose.Cells Java"
"url": "/id/java/images-shapes/aspose-cells-java-add-styling-shapes-excel/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Cara Menambahkan dan Menata Bentuk di Excel Menggunakan Aspose.Cells Java

## Perkenalan

Tingkatkan lembar kerja Excel Anda dengan menambahkan bentuk khusus secara terprogram dengan `Aspose.Cells` untuk Java. Tutorial ini memandu Anda menambahkan bentuk persegi panjang, mengonfigurasi gaya garisnya, dan menerapkan isian gradien.

**Apa yang Akan Anda Pelajari:**
- Menyiapkan Aspose.Cells di proyek Java Anda.
- Menambahkan bentuk persegi panjang ke lembar kerja Excel.
- Mengonfigurasi gaya garis dan gradien untuk bentuk.
- Menyimpan buku kerja yang dimodifikasi.

Mari kita mulai dengan memastikan Anda memenuhi semua prasyarat.

## Prasyarat

Sebelum menyelami kodenya, pastikan:
- **Perpustakaan:** Pustaka Aspose.Cells (versi 25.3 atau yang lebih baru) disertakan dalam proyek Anda.
- **Lingkungan:** Kemampuan menggunakan lingkungan pengembangan Java seperti Maven atau Gradle untuk manajemen ketergantungan.
- **Pengetahuan:** Pemahaman dasar tentang pemrograman Java dan manipulasi file Excel.

## Menyiapkan Aspose.Cells untuk Java

Integrasikan Aspose.Cells ke dalam proyek Java Anda menggunakan alat pembangun Anda:

**Pakar:**
Tambahkan ke Anda `pom.xml`:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradasi:**
Sertakan dalam Anda `build.gradle` mengajukan:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Akuisisi Lisensi

Anda dapat memperoleh lisensi sementara untuk menguji Aspose.Cells tanpa batasan atau membelinya untuk penggunaan jangka panjang. Mulailah dengan [uji coba gratis](https://releases.aspose.com/cells/java/) dan pertimbangkan untuk memperoleh [lisensi sementara](https://purchase.aspose.com/temporary-license/) jika diperlukan.

### Inisialisasi Dasar

Setelah menambahkan dependensi, inisialisasi Aspose.Cells di proyek Java Anda:
```java
import com.aspose.cells.Workbook;

public class ExcelShapeDemo {
    public static void main(String[] args) throws Exception {
        Workbook excelBook = new Workbook();
        // Operasi selanjutnya akan dilakukan di sini.
    }
}
```

## Panduan Implementasi

### Menambahkan Bentuk Persegi Panjang ke Lembar Kerja Excel

**Ringkasan:** Pelajari cara menambahkan dan memposisikan bentuk persegi panjang di lembar kerja Anda menggunakan Aspose.Cells.

#### Langkah 1: Buat Buku Kerja Baru
```java
Workbook excelBook = new Workbook();
```
Ini menginisialisasi contoh buku kerja baru tempat Anda akan menambahkan bentuk.

#### Langkah 2: Tambahkan Bentuk Persegi Panjang
```java
import com.aspose.cells.RectangleShape;
import com.aspose.cells.MsoDrawingType;

RectangleShape rectangle = (RectangleShape) excelBook.getWorksheets().get(0)
        .getShapes().addShape(MsoDrawingType.RECTANGLE, 3, 2, 0, 0, 70, 130);
```
Di sini, persegi panjang ditambahkan ke lembar kerja pertama. Parameter menentukan jenis, posisi, dan ukurannya.

#### Langkah 3: Atur Penempatan
```java
rectangle.setPlacement(com.aspose.cells.PlacementType.FREE_FLOATING);
```
Ini mengonfigurasikan bentuk agar mengambang bebas dan tidak terikat pada rentang sel tertentu.

### Mengonfigurasi Gaya Garis Bentuk

**Ringkasan:** Sesuaikan gaya garis dan isian gradien untuk bentuk persegi panjang Anda.

#### Langkah 1: Konfigurasikan Gaya Garis
```java
import com.aspose.cells.LineFormat;
import com.aspose.cells.MsoLineStyle;

LineFormat linestyle = rectangle.getLine();
linestyle.setDashStyle(MsoLineStyle.THICK_THIN);
linestyle.setWeight(4);
```
Ini mengatur gaya garis ke pola garis putus-putus tebal-tipis dan menyesuaikan ketebalannya.

#### Langkah 2: Terapkan Isian Gradien
```java
import com.aspose.cells.FillFormat;
import com.aspose.cells.GradientStyleType;

FillFormat fillformat = rectangle.getFill();
fillformat.setOneColorGradient(com.aspose.cells.Color.getBlue(), 1, 
    GradientStyleType.HORIZONTAL, 1);
```
Efek gradien diterapkan pada isian persegi panjang untuk peningkatan visual.

### Menyimpan Buku Kerja

Terakhir, simpan buku kerja Anda dengan semua konfigurasi:
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
excelBook.save(outDir + "/StyledRectangle_out.xls");
```

## Aplikasi Praktis

- **Visualisasi Data:** Gunakan bentuk di dasbor untuk menyorot titik data utama.
- **Desain Template:** Buat templat untuk laporan atau faktur yang memerlukan elemen grafis tertentu.
- **Pembuatan Laporan Otomatis:** Tingkatkan proses otomatis dengan menambahkan dan menata bentuk secara terprogram.

## Pertimbangan Kinerja

Saat bekerja dengan file Excel berukuran besar, pertimbangkan kiat berikut:
- Minimalkan penggunaan memori dengan membuang objek yang tidak lagi diperlukan.
- Gunakan struktur data yang efisien untuk menyimpan properti bentuk sebelum menerapkannya.
- Perbarui pustaka Aspose.Cells secara berkala untuk peningkatan kinerja.

## Kesimpulan

Anda telah mempelajari cara menambahkan dan memberi gaya pada bentuk dalam buku kerja Excel menggunakan Aspose.Cells untuk Java. Untuk lebih mengeksplorasi kemampuannya, pelajari manipulasi yang lebih rumit seperti menambahkan bagan atau pemformatan bersyarat.

**Langkah Berikutnya:**
Bereksperimenlah dengan berbagai jenis dan gaya bentuk atau integrasikan perpustakaan ke dalam aplikasi yang lebih besar yang memerlukan pembuatan dokumen Excel yang dinamis.

## Bagian FAQ

1. **Versi Aspose.Cells apa yang kompatibel dengan Java 11?**
   - Versi 25.3 dan yang lebih baru seharusnya kompatibel, tetapi selalu periksa catatan rilis untuk persyaratan khusus apa pun.
   
2. **Bagaimana cara menerapkan isian gradien ke bentuk lain selain persegi panjang?**
   - Metode `setOneColorGradient` dapat diterapkan secara serupa di berbagai jenis bentuk yang mendukung isian.

3. **Bisakah Aspose.Cells menangani file Excel berukuran besar secara efisien?**
   - Ya, dengan manajemen memori dan pembaruan pustaka yang tepat, ia dapat menangani file besar dengan baik.

4. **Apa saja masalah umum saat menata bentuk di Aspose.Cells?**
   - Kesalahan yang umum terjadi antara lain pengaturan koordinat yang salah atau tidak menerapkan gaya sebelum menyimpan buku kerja.

5. **Bagaimana saya dapat berkontribusi untuk meningkatkan dokumentasi atau fitur Aspose.Cells?**
   - Berinteraksi dengan komunitas di [forum dukungan](https://forum.aspose.com/c/cells/9) dan berbagi masukan atau saran untuk perbaikan.

## Sumber daya
- **Dokumentasi:** Jelajahi panduan terperinci di [Dokumentasi Aspose](https://reference.aspose.com/cells/java/).
- **Unduh:** Akses rilis Aspose.Cells dari [Di Sini](https://releases.aspose.com/cells/java/).
- **Pembelian:** Untuk fitur lengkap, pertimbangkan untuk membeli lisensi [Di Sini](https://purchase.aspose.com/buy).
- **Mendukung:** Cari bantuan di [Forum Dukungan Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}