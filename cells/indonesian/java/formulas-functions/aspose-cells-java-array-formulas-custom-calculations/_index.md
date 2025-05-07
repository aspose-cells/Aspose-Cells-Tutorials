---
"date": "2025-04-08"
"description": "Pelajari cara menetapkan rumus array, menerapkan gaya angka, menyesuaikan perhitungan, dan menyimpan buku kerja secara efisien menggunakan Aspose.Cells untuk Java."
"title": "Kuasai Rumus Array Excel dengan Aspose.Cells Java&#58; Sederhanakan Perhitungan dan Pemformatan"
"url": "/id/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Menguasai Rumus Array dan Perhitungan Kustom dengan Aspose.Cells Java

## Perkenalan

Apakah Anda ingin menyederhanakan tugas pemrosesan data Excel menggunakan Java? Banyak pengembang menghadapi tantangan saat mencoba memanipulasi rumus spreadsheet yang rumit secara terprogram. Tutorial ini akan memandu Anda memanfaatkan **Aspose.Cells untuk Java** untuk mengatur rumus array, menerapkan gaya angka, menyesuaikan perhitungan, dan menyimpan pekerjaan Anda secara efisien. Apakah Anda seorang pengembang berpengalaman atau baru memulai dengan otomatisasi Excel di Java, panduan lengkap ini sangat cocok untuk Anda.

### Apa yang Akan Anda Pelajari
- Cara mengatur rumus array menggunakan Aspose.Cells
- Menerapkan format angka ke sel secara terprogram
- Menerapkan opsi perhitungan khusus dengan fungsi yang ditentukan pengguna
- Mengatur mode perhitungan dan menyimpan buku kerja sebagai XLSX atau PDF
- Aplikasi dunia nyata dari fitur-fitur ini dalam proyek Java Anda

Mari kita bahas prasyarat yang Anda perlukan sebelum menerapkan fitur-fitur hebat ini.

## Prasyarat
Sebelum masuk ke Aspose.Cells untuk Java, pastikan Anda memiliki:

### Pustaka yang Diperlukan dan Pengaturan Lingkungan
- **Aspose.Cells untuk Java** versi 25.3 atau lebih baru
- IDE yang cocok (misalnya, IntelliJ IDEA atau Eclipse)
- JDK terinstal di mesin Anda

### Persyaratan Pengetahuan
- Pemahaman dasar tentang pemrograman Java
- Keakraban dengan konsep spreadsheet Excel

Sekarang, mari kita atur Aspose.Cells di proyek Anda!

## Menyiapkan Aspose.Cells untuk Java
Untuk mulai menggunakan Aspose.Cells untuk Java, sertakan sebagai dependensi dalam proyek Anda. Berikut adalah langkah-langkah instalasi untuk Maven dan Gradle:

**Pakar:**

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradasi:**

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Akuisisi Lisensi
Aspose.Cells menawarkan lisensi uji coba gratis, yang dapat Anda peroleh dengan mengunjungi [Halaman lisensi sementara Aspose](https://purchase.aspose.com/temporary-license/)Untuk akses penuh, pertimbangkan untuk membeli langganan.

### Inisialisasi dan Pengaturan Dasar
Setelah menambahkan dependensi, inisialisasi Aspose.Cells sebagai berikut:

```java
import com.aspose.cells.Workbook;

// Inisialisasi buku kerja
Workbook workbook = new Workbook();
```

## Panduan Implementasi
Sekarang setelah Anda menyiapkannya, mari kita jelajahi setiap fitur langkah demi langkah.

### Mengatur Rumus Array dalam Sel
Rumus array memungkinkan Anda melakukan kalkulasi kompleks di beberapa sel. Berikut cara mengaturnya menggunakan Aspose.Cells:

#### Ringkasan
Menggunakan `setArrayFormula` metode ini, Anda dapat menetapkan rumus array secara terprogram.

#### Langkah-langkah Implementasi
1. **Inisialisasi Buku Kerja dan Sel**

   ```java
   import com.aspose.cells.Cell;
   import com.aspose.cells.Cells;
   import com.aspose.cells.Workbook;

   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook();
   Cells cells = workbook.getWorksheets().get(0).getCells();
   Cell cell = cells.get(0, 0);
   ```

2. **Mengatur Rumus Array**

   ```java
   // Tetapkan rumus array dalam rentang 2x2 yang dimulai dari (0,0)
   cell.setArrayFormula("=MYFUNC()", 2, 2);
   ```

#### Konfigurasi Kunci
- Itu `setArrayFormula` metode ini mengambil tiga parameter: string rumus, jumlah baris, dan kolom.
- Pastikan fungsi kustom Anda (`MYFUNC`) didefinisikan dalam Excel atau sebagai UDF (Fungsi yang Ditentukan Pengguna) jika diperlukan.

### Menerapkan Gaya Angka ke Sel
Memformat sel meningkatkan keterbacaan. Berikut cara menerapkan gaya angka:

#### Ringkasan
Gunakan `setNumber` metode pada objek gaya sel untuk memformatnya.

#### Langkah-langkah Implementasi
1. **Ambil dan Atur Gaya**

   ```java
   import com.aspose.cells.Style;

   // Dapatkan gaya sel saat ini
   Style style = cell.getStyle();
   
   // Mengatur format angka (misalnya, mata uang)
   style.setNumber(14);
   
   // Terapkan gaya kembali ke sel
   cell.setStyle(style);
   ```

#### Konfigurasi Kunci
- Format angka didefinisikan oleh konstanta seperti `14` untuk mata uang.
- Ubah nilai ini berdasarkan persyaratan pemformatan Anda.

### Opsi Perhitungan Kustom dengan Fungsi yang Ditentukan Pengguna
Tingkatkan perhitungan menggunakan fungsi khusus untuk kebutuhan spesifik:

#### Ringkasan
Sesuaikan evaluasi rumus menggunakan `CalculationOptions`.

#### Langkah-langkah Implementasi
1. **Siapkan Fungsi Kustom**

   ```java
   import com.aspose.cells.CalculationOptions;
   import com.aspose.cells.CustomFunctionStaticValue;

   // Inisialisasi opsi perhitungan dengan fungsi kustom
   CalculationOptions copt = new CalculationOptions();
   copt.setCustomEngine(new CustomFunctionStaticValue());
   
   // Hitung rumus dengan mesin khusus
   workbook.calculateFormula(copt);
   ```

#### Konfigurasi Kunci
- Menggunakan `setCustomEngine` untuk menentukan logika perhitungan khusus Anda.
- Pastikan fungsi kustom Anda selaras dengan harapan Aspose.Cells.

### Mengatur Mode Perhitungan dan Menyimpan sebagai XLSX
Kontrol bagaimana perhitungan dilakukan dan simpan pekerjaan Anda secara efisien:

#### Ringkasan
Atur mode perhitungan ke manual untuk pengoptimalan kinerja sebelum menyimpan buku kerja.

#### Langkah-langkah Implementasi
1. **Konfigurasikan Pengaturan Perhitungan**

   ```java
   import com.aspose.cells.CalcModeType;

   String outDir = "YOUR_OUTPUT_DIRECTORY";
   
   // Atur mode perhitungan ke MANUAL
   workbook.getSettings().getFormulaSettings().setCalculationMode(CalcModeType.MANUAL);
   ```

2. **Simpan sebagai XLSX**

   ```java
   // Simpan buku kerja dalam format Excel
   workbook.save(outDir + "output.xlsx");
   ```

#### Konfigurasi Kunci
- `MANUAL` Mode ini mencegah perhitungan ulang otomatis, sehingga meningkatkan kinerja.
- Sesuaikan pengaturan perhitungan berdasarkan kebutuhan proyek Anda.

### Menyimpan Buku Kerja sebagai PDF
Mengekspor ke PDF dapat berguna untuk berbagi atau mencetak:

```java
// Simpan buku kerja dalam format PDF
workbook.save(outDir + "output.pdf");
```

## Aplikasi Praktis
Berikut ini adalah beberapa skenario dunia nyata di mana fitur-fitur ini sangat berguna:
1. **Pelaporan Keuangan:** Otomatisasi dan format model keuangan yang rumit.
2. **Analisis Data:** Terapkan perhitungan khusus untuk meningkatkan wawasan data.
3. **Pembuatan Dokumen Otomatis:** Membuat laporan standar untuk didistribusikan.

Aplikasi ini mendemonstrasikan bagaimana Aspose.Cells dapat terintegrasi ke dalam sistem yang lebih besar, menyederhanakan alur kerja lintas industri.

## Pertimbangan Kinerja
Untuk kinerja optimal:
- Minimalkan penggunaan fungsi volatil dalam rumus array.
- Memanfaatkan mode perhitungan manual untuk mengurangi overhead pemrosesan.
- Kelola memori Java secara efektif dengan membuang objek yang tidak digunakan.

Mengikuti praktik terbaik ini memastikan aplikasi Anda tetap efisien dan responsif.

## Kesimpulan
Anda kini telah menguasai pengaturan rumus array, penerapan gaya angka, penyesuaian perhitungan, dan penyimpanan buku kerja menggunakan Aspose.Cells untuk Java. Keterampilan ini memberdayakan Anda untuk mengotomatiskan tugas spreadsheet yang rumit dengan mudah. Terus jelajahi fitur-fitur Aspose yang tangguh dengan mengunjungi [dokumentasi](https://reference.aspose.com/cells/java/).

Siap untuk melangkah ke tahap berikutnya? Pelajari topik yang lebih mendalam atau integrasikan solusi ini ke dalam proyek Anda saat ini!

## Bagian FAQ
1. **Apa rumus array di Excel?**
   - Rumus array melakukan beberapa perhitungan pada satu atau beberapa item dalam suatu rentang.
2. **Bagaimana cara menerapkan gaya angka menggunakan Aspose.Cells?**
   - Gunakan `setNumber` metode pada objek gaya sel untuk memformatnya.
3. **Bisakah saya menyesuaikan logika perhitungan dengan Aspose.Cells?**
   - Ya, dengan menyiapkan fungsi khusus dan menggunakan `CalculationOptions`.
4. **Apa keuntungan mode perhitungan manual?**
   - Ini meningkatkan kinerja dengan mencegah perhitungan ulang yang tidak diperlukan.
5. **Bagaimana cara menyimpan buku kerja sebagai PDF menggunakan Aspose.Cells?**
   - Gunakan `save` metode dengan ekstensi file yang sesuai (`.pdf`).

## Sumber daya
- [Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Unduh Aspose.Cells untuk Java](https://releases.aspose.com/cells/java/)
- [Beli Lisensi](https://purchase.aspose.com/pricing/aspose.cells)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}