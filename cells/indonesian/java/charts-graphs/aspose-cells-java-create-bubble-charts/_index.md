---
date: '2026-04-02'
description: Pelajari cara membuat diagram dan menghasilkan diagram gelembung Excel
  menggunakan Aspose.Cells untuk Java. Panduan ini memandu Anda melalui pengaturan,
  data, dan penyimpanan diagram.
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 'Cara Membuat Grafik: Grafik Buih Excel dengan Aspose.Cells Java'
url: /id/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Diagram: Diagram Bubble Excel dengan Aspose.Cells Java

Tingkatkan laporan Excel Anda dengan diagram bubble dinamis menggunakan Aspose.Cells untuk Java. Dalam tutorial ini, Anda akan belajar **cara membuat diagram** objek yang memvisualisasikan data sebagai diagram bubble, membuat presentasi Anda lebih mendalam dan interaktif. Kami akan membimbing Anda melalui setiap langkah—dari menyiapkan lingkungan pengembangan hingga mengonfigurasi data diagram dan akhirnya menyimpan workbook.

## Jawaban Cepat
- **Library apa yang terbaik untuk diagram Excel di Java?** Aspose.Cells for Java.
- **Apakah saya dapat menghasilkan diagram bubble Excel secara programatis?** Ya, menggunakan chart API yang ditunjukkan di bawah.
- **Apakah saya memerlukan lisensi untuk menjalankan kode?** Versi percobaan gratis berfungsi, tetapi lisensi penuh membuka semua fitur.
- **Alat build Java mana yang didukung?** Maven dan Gradle keduanya didukung.
- **Metode utama untuk mengatur data diagram bubble adalah apa?** Gunakan `setBubbleSizes`, `setXValues`, dan `setValues` pada series.

## Apa Itu Diagram Bubble?
Diagram bubble adalah variasi dari scatter plot di mana setiap titik data direpresentasikan oleh sebuah bubble. Sumbu X dan Sumbu Y menentukan posisi, sementara ukuran bubble menyampaikan dimensi ketiga informasi—sempurna untuk memvisualisasikan data keuangan, penjualan, atau ilmiah.

## Mengapa Menggunakan Aspose.Cells untuk Java?
- **Zero‑install Excel engine** – tidak perlu Microsoft Office di server.
- **Rich charting API** – mendukung semua tipe diagram modern, termasuk diagram bubble.
- **Cross‑platform** – berfungsi di Windows, Linux, dan macOS.
- **High performance** – dioptimalkan untuk dataset besar dan pembuatan laporan volume tinggi.

## Prasyarat
Untuk membuat diagram bubble menggunakan Aspose.Cells untuk Java, pastikan Anda memenuhi prasyarat berikut:

### Perpustakaan dan Dependensi yang Diperlukan
- **Aspose.Cells for Java**: Instal versi terbaru (misalnya, 25.3).

### Persyaratan Penyiapan Lingkungan
- JDK (Java Development Kit) yang kompatibel terinstal.
- Konfigurasikan proyek Anda untuk menggunakan Maven atau Gradle.

### Prasyarat Pengetahuan
- Pemahaman dasar tentang pemrograman Java.
- Familiaritas dengan struktur file Excel dan tipe diagram.

## Menyiapkan Aspose.Cells untuk Java
Menyiapkan lingkungan Anda sangat penting. Berikut cara memulainya:

### Instalasi via Maven
Tambahkan dependensi berikut ke `pom.xml` Anda:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Instalasi via Gradle
Bagi yang menggunakan Gradle, tambahkan ini ke `build.gradle` Anda:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Akuisisi Lisensi
Aspose.Cells menawarkan percobaan gratis dengan fungsionalitas terbatas. Untuk kemampuan penuh:
- **Beli**: Kunjungi [halaman pembelian](https://purchase.aspose.com/buy) untuk opsi lisensi.
- **Lisensi Sementara**: Dapatkan lisensi sementara dari [sini](https://purchase.aspose.com/temporary-license/) untuk pengujian penuh.

### Inisialisasi Dasar
Sebelum menggunakan Aspose.Cells, inisialisasi di proyek Java Anda:
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## Panduan Implementasi
Mari kita uraikan proses pembuatan dan konfigurasi diagram bubble dengan Aspose.Cells.

### Cara Membuat Diagram: Menginisialisasi Objek Workbook
`Workbook` mewakili seluruh file Excel, memungkinkan Anda memanipulasi sheet, sel, dan lainnya. Inisialisasi seperti berikut:
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### Cara Mengatur Data Diagram Bubble: Mengakses dan Memanipulasi Worksheet
Siapkan data yang akan memberi makan diagram bubble:
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### Cara Menghasilkan Diagram Bubble Excel: Membuat dan Mengonfigurasi Diagram
Buat diagram bubble dengan menambahkannya ke worksheet dan mengatur sumber data:
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### Cara Menyimpan Diagram: Menyimpan Workbook
Simpan workbook (dan diagram yang tersemat) ke disk:
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## Aplikasi Praktis
- **Pelaporan Keuangan** – Visualisasikan pendapatan, laba, dan pangsa pasar dalam satu tampilan.
- **Analisis Data Penjualan** – Sorot kinerja penjualan regional di mana ukuran bubble menunjukkan volume.
- **Penelitian Ilmiah** – Tampilkan hasil eksperimen dengan tiga variabel sekaligus.

## Pertimbangan Kinerja
- Buang objek yang tidak terpakai dengan cepat untuk membebaskan memori.
- Jaga rentang data sesempit mungkin; rentang besar yang tidak diperlukan dapat memperlambat rendering.
- Gunakan praktik terbaik manajemen memori Java saat memproses dataset besar.

## Masalah Umum dan Solusinya
| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| **Diagram kosong** | Rentang data tidak cocok dengan series | Verifikasi bahwa `setBubbleSizes`, `setXValues`, dan `setValues` merujuk ke sel yang benar. |
| **Ukuran bubble tidak tepat** | Panjang rentang tidak cocok | Pastikan ketiga rentang berisi jumlah titik yang sama. |
| **Pengecualian lisensi** | Menjalankan tanpa lisensi yang valid | Terapkan lisensi sementara atau yang dibeli sebelum membuat workbook. |

## Pertanyaan yang Sering Diajukan

**Q: Apa versi minimum Aspose.Cells yang diperlukan?**  
**A:** Versi 25.3 direkomendasikan untuk tutorial ini agar kompatibel dengan semua fitur yang ditunjukkan.

**Q: Bagaimana saya dapat menyesuaikan warna diagram bubble?**  
**A:** Gunakan metode pemformatan series, seperti `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`.

**Q: Bisakah saya menjalankan kode ini di server Linux?**  
**A:** Ya, Aspose.Cells untuk Java sepenuhnya lintas‑platform dan berfungsi di sistem operasi apa pun dengan JDK yang kompatibel.

**Q: Apa yang harus saya lakukan jika mendapatkan error “Data source size mismatch”?**  
**A:** Periksa kembali bahwa rentang untuk ukuran bubble, nilai X, dan nilai Y berisi jumlah sel yang sama.

**Q: Di mana saya dapat memperoleh lisensi sementara untuk pengujian?**  
**A:** Kunjungi [halaman lisensi sementara Aspose](https://purchase.aspose.com/temporary-license/) untuk meminta lisensi percobaan.

## Sumber Daya
- **Dokumentasi**: Untuk detail lebih lanjut, lihat [dokumentasi resmi](https://reference.aspose.com/cells/java/).
- **Unduh**: Dapatkan versi terbaru dari [halaman rilis](https://releases.aspose.com/cells/java/).
- **Beli**: Jelajahi opsi lisensi di [halaman ini](https://purchase.aspose.com/buy).
- **Percobaan Gratis**: Mulai dengan percobaan gratis untuk menguji kemampuan di [bagian rilis Aspose](https://releases.aspose.com/cells/java/).
- **Forum Dukungan**: Untuk pertanyaan apa pun, [forum dukungan](https://forum.aspose.com/c/cells/9) tersedia.

---

**Terakhir Diperbarui:** 2026-04-02  
**Diuji Dengan:** Aspose.Cells 25.3 untuk Java  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}