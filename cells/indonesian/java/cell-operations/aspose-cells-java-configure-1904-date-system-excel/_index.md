---
date: '2026-02-22'
description: Pelajari cara mengubah sistem tanggal Excel ke 1904 menggunakan Aspose.Cells
  untuk Java, mengatur format tanggal Excel, dan mengonversi sistem 1904 Excel secara
  efisien.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Ubah sistem tanggal Excel ke 1904 dengan Aspose.Cells Java
url: /id/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

 formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Sistem Tanggal Excel ke 1904 dengan Aspose.Cells Java

Mengelola data historis di Excel dapat menjadi tantangan karena Excel mendukung dua sistem tanggal yang berbeda. **Dalam tutorial ini Anda akan belajar cara mengubah sistem tanggal Excel ke format 1904 menggunakan Aspose.Cells untuk Java**, yang membuat penanganan tanggal lama menjadi mudah. Kami akan memandu Anda melalui inisialisasi workbook, mengaktifkan sistem tanggal 1904, dan menyimpan perubahan.

## Jawaban Cepat
- **Apa yang dilakukan sistem tanggal 1904?** Sistem ini mulai menghitung hari dari 1 Januari 1904, menggeser semua tanggal sebesar 1462 hari dibandingkan dengan sistem default 1900.  
- **Mengapa menggunakan Aspose.Cells untuk mengubah sistem tanggal?** Ia menyediakan API sederhana yang berfungsi tanpa Excel terpasang dan mendukung file berukuran besar.  
- **Versi Java mana yang didukung?** JDK 8 atau yang lebih baru.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi menghilangkan batasan penggunaan.  
- **Bisakah saya mengembalikan ke sistem 1900 nanti?** Ya, cukup panggil `setDate1904(false)`.

## Apa itu sistem tanggal 1904 di Excel?
Sistem tanggal 1904 awalnya digunakan oleh versi Macintosh awal Excel. Sistem ini menghitung hari dari 1 Januari 1904, yang berguna untuk kompatibilitas dengan spreadsheet lama dan beberapa model keuangan.

## Mengapa mengubah sistem tanggal Excel dengan Aspose.Cells?
- **Kompatibilitas lintas‑platform** – berfungsi di Windows, Linux, dan macOS.  
- **Tidak memerlukan instalasi Excel** – ideal untuk pemrosesan sisi server.  
- **Kinerja tinggi** – menangani workbook besar dengan overhead memori minimal.  

## Prasyarat
- Java Development Kit (JDK) 8 atau lebih tinggi.  
- Maven atau Gradle untuk manajemen dependensi.  
- Pengetahuan dasar pemrograman Java.  

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
Sertakan baris ini di file `build.gradle` Anda:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Akuisisi Lisensi
Aspose menawarkan percobaan gratis, lisensi sementara, dan lisensi komersial penuh. Anda dapat memulai dengan [percobaan gratis](https://releases.aspose.com/cells/java/) atau memperoleh lisensi sementara dari [halaman lisensi sementara](https://purchase.aspose.com/temporary-license/).

## Ubah sistem tanggal Excel menggunakan Aspose.Cells Java

Berikut adalah panduan langkah‑demi‑langkah yang sebenarnya **mengubah sistem tanggal Excel**. Setiap langkah mencakup penjelasan singkat diikuti oleh kode tepat yang Anda perlukan.

### Langkah 1: Inisialisasi dan muat workbook
Pertama, buat instance `Workbook` yang mengarah ke file Excel Anda yang sudah ada.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Langkah 2: Aktifkan sistem tanggal 1904
Gunakan pengaturan workbook untuk mengubah sistem tanggal.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Tips pro:** Anda juga dapat memanggil `setDate1904(false)` nanti jika perlu mengembalikan.

### Langkah 3: Simpan workbook yang telah dimodifikasi
Akhirnya, tulis perubahan ke file baru (atau timpa file asli).

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Catatan:** Kode di atas menggunakan nama kelas `tWorkbook` seperti yang diberikan awalnya. Pastikan kesalahan ketik ini sesuai dengan konvensi penamaan proyek Anda atau koreksi menjadi `Workbook` jika diperlukan.

## Atur tanggal Excel secara programatis (kata kunci sekunder)
Jika Anda perlu menyesuaikan nilai sel individu setelah mengubah sistem, Anda dapat menggunakan `Cells.get(i, j).putValue(Date)` di mana tanggal akan diinterpretasikan sesuai dengan sistem tanggal yang aktif.

## Konversi sistem Excel 1904 kembali ke 1900 (kata kunci sekunder)
Untuk mengembalikan, cukup panggil:

```java
workbook.getSettings().setDate1904(false);
```

Kemudian simpan workbook lagi.

## Aplikasi Praktis
1. **Arsip Data** – Mempertahankan cap waktu lama saat memigrasikan spreadsheet berbasis Mac yang lama.  
2. **Pelaporan Lintas‑Platform** – Menghasilkan laporan yang dapat dibuka di Windows maupun macOS tanpa ketidaksesuaian tanggal.  
3. **Pemodelan Keuangan** – Menyesuaikan perhitungan tanggal dengan model keuangan lama yang mengharapkan sistem 1904.  

## Pertimbangan Kinerja
- Batasi operasi workbook dalam satu sesi untuk menjaga penggunaan memori tetap rendah.  
- Gunakan penyesuaian garbage‑collection Java untuk file yang sangat besar.  

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara sistem tanggal 1900 dan 1904?**  
A: Sistem 1900 mulai pada 1 Januari 1900, sedangkan sistem 1904 mulai pada 1 Januari 1904, menggeser semua tanggal sebesar 1462 hari.

**Q: Bisakah saya mengubah sistem tanggal workbook yang sedang terbuka di Excel?**  
A: Ya, tetapi Anda harus menutup file di Excel terlebih dahulu; jika tidak operasi penyimpanan akan gagal.

**Q: Apakah saya memerlukan lisensi untuk menggunakan `setDate1904`?**  
A: Metode ini berfungsi dalam percobaan gratis, tetapi lisensi penuh menghilangkan batasan evaluasi.

**Q: Apakah memungkinkan mengubah sistem tanggal hanya untuk satu lembar kerja?**  
A: Tidak, sistem tanggal adalah pengaturan tingkat workbook; berlaku untuk semua lembar kerja.

**Q: Bagaimana saya dapat memverifikasi bahwa sistem tanggal telah diubah?**  
A: Buka file yang disimpan di Excel, pergi ke **File → Options → Advanced**, dan centang kotak **"Use 1904 date system"**.

## Kesimpulan
Anda kini mengetahui cara **mengubah sistem tanggal Excel** ke 1904 menggunakan Aspose.Cells untuk Java, cara mengatur format tanggal Excel, dan cara mengembalikannya jika diperlukan. Gabungkan potongan kode ini ke dalam alur pemrosesan data Anda untuk menjamin kompatibilitas tanggal lintas platform.

---

**Terakhir Diperbarui:** 2026-02-22  
**Diuji Dengan:** Aspose.Cells 25.3 for Java  
**Penulis:** Aspose  

**Sumber Daya**
- **Dokumentasi:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Unduh:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Beli Lisensi:** [Beli Aspose.Cells](https://purchase.aspose.com/buy)
- **Percobaan Gratis:** [Mulai Percobaan Gratis](https://releases.aspose.com/cells/java/)
- **Lisensi Sementara:** [Dapatkan Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- **Forum Dukungan:** [Dukungan Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}