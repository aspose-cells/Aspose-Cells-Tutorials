---
date: '2026-04-11'
description: Pelajari cara menampilkan versi Aspose Cells, memuat workbook Excel di
  Java, dan menangani enum chart dengan Aspose.Cells. Ikuti contoh langkah demi langkah.
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: Tampilkan Versi Aspose Cells & Penanganan Enum Grafik di Java
url: /id/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tampilkan Versi Aspose Cells & Penanganan Enum Grafik di Java

## Pendahuluan

Jika Anda perlu **menampilkan versi Aspose Cells**, memuat workbook Excel di Java, dan bekerja dengan enum grafik, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan memandu langkah‑langkah tepat yang Anda perlukan untuk mengintegrasikan Aspose.Cells untuk Java ke dalam proyek Anda, mengekstrak data grafik, dan mengonversi enum berbasis integer menjadi string yang dapat dibaca. Pada akhir tutorial Anda akan memiliki solusi yang solid dan siap produksi yang dapat langsung Anda gunakan dalam basis kode Anda.

**Apa yang Akan Anda Pelajari**
- Cara menampilkan versi Aspose.Cells.
- Cara **memuat workbook Excel Java** dan mengakses data grafik.
- Cara mengonversi nilai enum integer ke ekivalen stringnya.
- Cara mengambil tipe nilai X dan Y dari sebuah titik grafik.

Mari kita mulai!

## Jawaban Cepat
- **Bagaimana cara memeriksa versi Aspose.Cells?** Panggil `CellsHelper.getVersion()` dan cetak hasilnya.  
- **Koordinat Maven mana yang menambahkan Aspose.Cells?** `com.aspose:aspose-cells:25.3`.  
- **Bisakah saya memuat workbook Excel di Java?** Ya—gunakan `new Workbook(filePath)`.  
- **Bagaimana nilai enum dikonversi?** Simpan `HashMap<Integer, String>` dan cari kunci integer tersebut.  
- **Metode apa yang mencetak tipe nilai X/Y?** `pnt.getXValueType()` dan `pnt.getYValueType()`.

## Apa itu “menampilkan versi Aspose Cells”?
Frasa ini mengacu pada pengambilan string versi runtime perpustakaan. Mengetahui versi yang tepat membantu dalam debugging, memastikan kompatibilitas, dan mengonfirmasi bahwa lisensi Anda diterapkan pada rilis yang dimaksud.

## Mengapa menampilkan versi dan memuat workbook Excel Java?
- **Debugging** – Mengonfirmasi bahwa perpustakaan yang benar berada di classpath.  
- **Kepatuhan** – Memudahkan verifikasi bahwa Anda menggunakan versi berlisensi.  
- **Otomatisasi** – Memungkinkan skrip yang menyesuaikan dengan rilis perpustakaan yang berbeda tanpa perubahan manual.

## Prasyarat

### Perpustakaan dan Dependensi yang Diperlukan
- **Aspose.Cells for Java** – perpustakaan inti untuk manipulasi Excel.  
- **Java Development Kit (JDK)** – versi 8 atau lebih baru.

### Penyiapan Lingkungan
- IDE pilihan Anda (IntelliJ IDEA, Eclipse, NetBeans).  
- Alat build: Maven **atau** Gradle (instruksi di bawah).

### Pengetahuan yang Diperlukan
- Pemrograman Java dasar.  
- Familiaritas dengan konsep Excel (lembar kerja, grafik) berguna tetapi tidak wajib.

## Menyiapkan Aspose.Cells untuk Java

### Using Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Using Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Langkah-langkah Akuisisi Lisensi
- **Uji Coba Gratis**: Unduh dari [Aspose's Release Page](https://releases.aspose.com/cells/java/).  
- **Lisensi Sementara**: Dapatkan lisensi jangka pendek di [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/).  
- **Pembelian**: Untuk proyek jangka panjang, beli lisensi melalui [Aspose Purchase Page](https://purchase.aspose.com/buy).

### Inisialisasi dan Penyiapan Dasar
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## Panduan Implementasi

### Cara Menampilkan Versi Aspose Cells
**Gambaran Umum** – Verifikasi cepat versi perpustakaan saat runtime.

#### Langkah 1: Impor Paket yang Diperlukan
```java
import com.aspose.cells.*;
```

#### Langkah 2: Buat Kelas dan Metode Main
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

#### Penjelasan
- `CellsHelper.getVersion()` mengembalikan string versi tepat dari DLL Aspose.Cells yang digunakan aplikasi Anda.

### Cara Mengonversi Enum Integer menjadi Enum String
**Gambaran Umum** – Mengubah nilai enum numerik (misalnya `CellValueType.IS_NUMERIC`) menjadi teks yang dapat dibaca.

#### Langkah 1: Siapkan HashMap untuk Konversi
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### Langkah 2: Konversi dan Cetak Nilai Enum
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

#### Penjelasan
- Peta `cvTypes` menjembatani kesenjangan antara konstanta numerik dan label yang dapat dibaca manusia.

### Cara Memuat Workbook Excel Java dan Mengakses Data Grafik
**Gambaran Umum** – Membuka workbook yang ada, menemukan grafik, dan memastikan datanya mutakhir.

#### Langkah 1: Impor Paket yang Diperlukan
```java
import com.aspose.cells.*;
```

#### Langkah 2: Muat Workbook dan Akses Worksheet
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

#### Penjelasan
- `new Workbook(filePath)` memuat file ke dalam memori.  
- `ch.calculate()` memaksa grafik menghitung ulang semua formula sehingga data yang Anda baca terkini.

### Cara Mengambil dan Mencetak Tipe Nilai X dan Y dari Titik Grafik
**Gambaran Umum** – Mengambil tipe data nilai X dan Y dari titik tertentu.

#### Langkah 1: Siapkan HashMap Konversi Enum (gunakan kembali dari sebelumnya)
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### Langkah 2: Akses Titik Grafik dan Cetak Tipe Nilai
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

#### Penjelasan
- `pnt.getXValueType()` / `pnt.getYValueType()` mengembalikan konstanta integer yang menunjukkan apakah nilai tersebut numerik, string, tanggal, dll.  
- Peta `cvTypes` menerjemahkan integer tersebut menjadi teks yang dapat dibaca.

## Aplikasi Praktis
1. **Pelaporan Keuangan** – Menghasilkan grafik secara otomatis dengan tipe data yang terverifikasi untuk jejak audit.  
2. **Dashboard Visualisasi Data** – Mengambil titik grafik ke dalam komponen UI khusus.  
3. **Pengujian Otomatis** – Memvalidasi bahwa seri grafik berisi tipe data yang diharapkan.  
4. **Business Intelligence** – Menyalurkan metadata grafik ke pipeline analitik hilir.  
5. **Alat Pelaporan Kustom** – Membangun mesin pelaporan khusus yang memerlukan penanganan enum yang tepat.

## Pertimbangan Kinerja
- **Muat Hanya Sheet yang Diperlukan** – Gunakan `Workbook.getWorksheets().get(index)` alih-alih memuat setiap sheet saat menangani file besar.  
- **Buang Objek Segera** – Setel referensi workbook ke `null` setelah pemrosesan untuk membantu pengumpulan sampah.  
- **Proses File Secara Batch** – Saat menangani banyak workbook, proses dalam batch untuk menjaga penggunaan memori tetap dapat diprediksi.

## Masalah Umum & Solusi
- **Lisensi Tidak Ditemukan** – Pastikan jalur file lisensi benar dan file tersebut termasuk dalam output build Anda.  
- **Grafik Tidak Dihitung** – Selalu panggil `chart.calculate()` sebelum membaca nilai titik.  
- **Pemetaaan Enum Salah** – Verifikasi bahwa Anda telah menambahkan semua konstanta `CellValueType` yang relevan ke `HashMap`.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan kode ini dengan Aspose.Cells 24.x?**  
A: Ya, API untuk pengambilan versi, pemuatan workbook, dan akses titik grafik tetap stabil pada rilis terbaru.

**Q: Bagaimana jika grafik saya berisi nilai tanggal?**  
A: Tambahkan `CellValueType.IS_DATE_TIME` ke peta `cvTypes` dan petakan ke `"IsDateTime"`.

**Q: Apakah saya memerlukan lisensi untuk penggunaan percobaan?**  
A: Lisensi percobaan diperlukan untuk fungsi penuh; tanpa itu Anda akan melihat watermark pada file yang dihasilkan.

**Q: Bagaimana cara menangani banyak worksheet?**  
A: Iterasi melalui `wb.getWorksheets()` dan proses setiap objek `Chart` yang Anda temui.

**Q: Apakah ada cara mengekspor data grafik ke CSV?**  
A: Ya—ekstrak nilai seri melalui `chart.getNSeries().get(i).getValues()` dan tulis menggunakan I/O Java standar.

---

**Terakhir Diperbarui:** 2026-04-11  
**Diuji Dengan:** Aspose.Cells 25.3 for Java  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}