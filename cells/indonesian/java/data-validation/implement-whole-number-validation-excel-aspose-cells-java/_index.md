---
"date": "2025-04-07"
"description": "Pelajari cara menerapkan validasi data bilangan bulat di Excel menggunakan Aspose.Cells untuk Java. Panduan langkah demi langkah ini mencakup penyiapan, penerapan, dan aplikasi praktis."
"title": "Menerapkan Validasi Data Bilangan Bulat di Excel dengan Aspose.Cells untuk Java; Panduan Lengkap"
"url": "/id/java/data-validation/implement-whole-number-validation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Menerapkan Validasi Data Bilangan Bulat di Excel dengan Aspose.Cells untuk Java

## Perkenalan
Saat bekerja dengan formulir entri data Excel, memastikan bahwa pengguna memasukkan data yang valid sangatlah penting. Dengan Aspose.Cells untuk Java, Anda dapat dengan mudah menerapkan validasi bilangan bulat dalam rentang tertentu. Panduan lengkap ini akan memandu Anda dalam menyiapkan lingkungan dan menerapkan validasi ini ke buku kerja Excel Anda.

**Apa yang Akan Anda Pelajari:**
- Inisialisasi buku kerja Excel dengan Aspose.Cells untuk Java
- Akses dan kelola validasi lembar kerja
- Terapkan validasi data bilangan bulat ke rentang sel
- Simpan buku kerja Excel yang dimodifikasi

Mari kita mulai dengan meninjau prasyarat sebelum menerapkan fitur-fitur ini.

## Prasyarat
Untuk mengikuti tutorial ini, Anda memerlukan:
- **Aspose.Cells untuk Java**Penting untuk membuat dan memanipulasi file Excel. Kami akan menggunakan versi 25.3.
- Pengetahuan dasar tentang pemrograman Java
- IDE atau editor teks untuk menulis kode Java

## Menyiapkan Aspose.Cells untuk Java
### Instalasi
Untuk memulai, sertakan Aspose.Cells dalam dependensi proyek Anda.

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
implementation(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Akuisisi Lisensi
- **Uji Coba Gratis:** Unduh uji coba dari [Aspose.Cells untuk Rilis Java](https://releases.aspose.com/cells/java/).
- **Lisensi Sementara:** Dapatkan lisensi sementara untuk menjelajahi fitur lengkap tanpa batasan di [Aspose Lisensi Sementara](https://purchase.aspose.com/temporary-license/).
- **Pembelian:** Untuk penggunaan jangka panjang, beli lisensi di [Halaman Pembelian Aspose](https://purchase.aspose.com/buy).

### Inisialisasi dan Pengaturan Dasar
Untuk menyiapkan Aspose.Cells untuk Java, impor kelas yang diperlukan seperti yang ditunjukkan di bawah ini:
```java
import com.aspose.cells.Workbook;
```
Buat buku kerja Excel baru dengan baris kode sederhana ini:
```java
Workbook workbook = new Workbook();
WorksheetCollection worksheets = workbook.getWorksheets();
```

## Panduan Implementasi
Kami akan membagi implementasinya menjadi beberapa fitur utama.

### Fitur: Inisialisasi Buku Kerja
#### Ringkasan
Mulailah dengan membuat contoh `Workbook`, yang merupakan file Excel Anda. Langkah ini menginisialisasi buku kerja untuk operasi selanjutnya.

#### Contoh Kode:
```java
// Impor paket Aspose.Cells
import com.aspose.cells.Workbook;

// Membuat buku kerja Excel baru
tWorkbook workbook = new Workbook();
WorksheetCollection worksheets = workbook.getWorksheets();
```

### Fitur: Mengakses Lembar Kerja dan Koleksi Validasi
#### Ringkasan
Berikutnya, akses koleksi validasi lembar kerja untuk menerapkan validasi data.

#### Tangga:
1. **Akses Lembar Kerja Pertama:** Ambil lembar kerja pertama dalam buku kerja Anda.
2. **Dapatkan Koleksi Validasi:** Mendapatkan `ValidationCollection` dari lembar kerja.

```java
// Impor kelas yang diperlukan
import com.aspose.cells.Worksheet;
import com.aspose.cells.ValidationCollection;

// Mengakses lembar kerja pertama
tWorksheet worksheet = worksheets.get(0);

// Mendapatkan koleksi validasi lembar kerja
tValidationCollection validations = worksheet.getValidations();
```

### Fitur: Menerapkan Validasi Data Bilangan Bulat
#### Ringkasan
Terapkan validasi data bilangan bulat untuk memastikan bahwa hanya angka dalam rentang tertentu yang diterima.

#### Tangga:
1. **Definisi Area Sel:** Tentukan rentang sel untuk validasi.
2. **Tambahkan dan Konfigurasikan Validasi:** Siapkan kriteria validasi menggunakan pengaturan Aspose.Cells.

```java
// Impor kelas yang diperlukan
import com.aspose.cells.CellArea;
import com.aspose.cells.Validation;
import com.aspose.cells.ValidationType;
import com.aspose.cells.OperatorType;

// Tentukan area sel untuk validasi
tCellArea area = new CellArea();
area.StartRow = 0;
area.StartColumn = 0;
area.EndRow = 1; // Memperbaiki kesalahan ketik dari 'aera' menjadi 'area'
area.EndColumn = 1;

// Tambahkan validasi ke koleksi validasi dan dapatkan indeksnya
int index = validations.add(area);

// Konfigurasikan pengaturan validasi
tValidation validation = validations.get(index);
validation.setType(ValidationType.WHOLE_NUMBER); // Atur tipe ke Bilangan Bulat
validation.setOperator(OperatorType.BETWEEN);    // Gunakan operator Between untuk memeriksa rentang
validation.setFormula1("10");                   // Nilai minimum
validation.setFormula2("1000");                 // Nilai maksimum
```

### Fitur: Menyimpan File Excel
#### Ringkasan
Terakhir, simpan buku kerja Anda dengan validasi yang diterapkan untuk memastikan persistensi.

```java
// Impor kelas yang diperlukan
import com.aspose.cells.SaveFormat;

// Tentukan direktori untuk menyimpan file
tString dataDir = "YOUR_DATA_DIRECTORY"; 

// Simpan buku kerja dalam format XLS
tWorkbook.save(dataDir + "WNDValidation_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## Aplikasi Praktis
1. **Formulir Entri Data:** Gunakan validasi bilangan bulat untuk menerapkan pembatasan input pada formulir.
2. **Sistem Manajemen Inventaris:** Pastikan jumlah yang dimasukkan adalah bilangan bulat dalam rentang yang valid.
3. **Alat Pelaporan Keuangan:** Validasi entri data numerik dalam lembar keuangan.

Contoh-contoh ini menunjukkan fleksibilitas Aspose.Cells untuk Java di berbagai industri, dari keuangan hingga manajemen inventaris.

## Pertimbangan Kinerja
- **Penggunaan Memori yang Efisien:** Menggunakan `Workbook.dispose()` jika Anda sudah selesai dengan buku kerja untuk membebaskan sumber daya.
- **Optimalkan Rentang Validasi:** Terapkan validasi hanya bila diperlukan untuk mengurangi overhead.
- **Pemrosesan Batch:** Memproses buku kerja secara berkelompok saat menangani kumpulan data besar untuk kinerja yang lebih baik.

## Kesimpulan
Dengan mengikuti tutorial ini, Anda telah mempelajari cara menginisialisasi buku kerja Excel menggunakan Aspose.Cells untuk Java, mengakses dan mengelola validasi lembar kerja, menerapkan validasi data bilangan bulat, dan menyimpan buku kerja Anda. Pengetahuan ini meningkatkan keandalan proses entri data dalam aplikasi Excel.

Langkah selanjutnya dapat mencakup penjelajahan jenis validasi data lain yang disediakan oleh Aspose.Cells atau mengintegrasikan fungsi ini ke dalam proyek yang lebih besar.

## Bagian FAQ
1. **Apa itu Aspose.Cells untuk Java?**
   - Ini adalah pustaka yang tangguh untuk mengelola berkas Excel secara terprogram tanpa perlu menginstal Microsoft Office.
2. **Bagaimana saya dapat menguji fitur Aspose.Cells?**
   - Gunakan versi uji coba gratis untuk menjelajahi dan menguji fungsinya secara ekstensif.
3. **Dapatkah saya menerapkan berbagai jenis validasi menggunakan Aspose.Cells?**
   - Ya, selain validasi bilangan bulat, Anda dapat menggunakan tanggal, daftar, panjang teks, dan rumus khusus untuk validasi data.
4. **Apa saja masalah umum saat menyiapkan Aspose.Cells?**
   - Pastikan versi pustaka yang benar disertakan dalam dependensi proyek Anda. Verifikasi bahwa berkas lisensi Anda (jika berlaku) dikonfigurasi dengan benar.
5. **Di mana saya dapat menemukan dokumentasi yang lebih rinci tentang Aspose.Cells?**
   - Kunjungi [Dokumentasi Aspose.Cells untuk Java](https://reference.aspose.com/cells/java/) untuk panduan lengkap dan referensi API.

## Sumber daya
- **Dokumentasi:** https://reference.aspose.com/sel/java/
- **Unduh:** https://releases.aspose.com/sel/java/
- **Pembelian:** https://purchase.aspose.com/beli
- **Uji Coba Gratis:** https://releases.aspose.com/sel/java/
- **Lisensi Sementara:** https://purchase.aspose.com/lisensi-sementara/
- **Mendukung:** https://forum.aspose.com/c/sel/9

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}