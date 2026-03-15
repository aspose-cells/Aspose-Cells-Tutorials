---
date: '2026-03-15'
description: Pelajari cara memisahkan nama menjadi kolom terpisah dan menyimpan workbook
  xlsx menggunakan Aspose Cells Java dalam tutorial langkah demi langkah.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Membagi Nama menjadi Kolom
url: /id/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Menguasai **aspose cells java**: Membagi Nama menjadi Kolom

Selamat datang di tutorial **aspose cells java** kami yang komprehensif. Dalam panduan ini Anda akan belajar **cara membagi nama** yang disimpan dalam satu kolom Excel menjadi dua kolom terpisah—nama depan dan nama belakang—dengan menggunakan fitur text‑to‑columns yang kuat. Baik Anda sedang membersihkan daftar kontak, menyiapkan data untuk impor CRM, atau sekadar membutuhkan cara cepat untuk merestrukturisasi spreadsheet, tutorial ini menunjukkan secara tepat bagaimana **save workbook xlsx** setelah transformasi.

## Jawaban Cepat
- **Apa yang dibahas dalam tutorial ini?** Membagi string nama lengkap menjadi kolom nama depan dan nama belakang dengan Aspose.Cells untuk Java.  
- **Versi perpustakaan apa yang digunakan?** Rilis stabil terbaru (per 2026).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya membagi dengan pemisah lain?** Ya—cukup ubah pemisah di `TxtLoadOptions`.  
- **Apakah outputnya berupa file .xlsx?** Tentu saja, workbook disimpan dalam format XLSX.

## Apa itu **aspose cells java**?
**Aspose.Cells java** adalah API Java berkinerja tinggi yang memungkinkan pengembang membuat, memodifikasi, mengonversi, dan merender file Excel tanpa memerlukan Microsoft Office. Ia mendukung semua format Excel utama dan menyediakan fitur lanjutan seperti formula, diagram, dan manipulasi data.

## Mengapa menggunakan **aspose cells java** untuk membagi nama?
- **Tanpa instalasi**: Berfungsi di lingkungan Java sisi‑server mana pun.  
- **Kecepatan**: Memproses spreadsheet besar lebih cepat dibandingkan interop Excel native.  
- **Presisi**: Kontrol penuh atas pemisah, rentang kolom, dan format output.  
- **Keandalan**: Tanpa ketergantungan COM atau Office, ideal untuk penyebaran di cloud atau kontainer.

## Prasyarat
- Java Development Kit (JDK) 8 atau yang lebih baru.  
- IDE seperti IntelliJ IDEA atau Eclipse (opsional namun disarankan).  
- Maven atau Gradle untuk manajemen dependensi.  

### Pengaturan Maven
Tambahkan dependensi Aspose.Cells ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Pengaturan Gradle
Tambahkan pustaka ke `build.gradle` Anda:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tip:** Gunakan lisensi sementara dari portal Aspose untuk membuka semua fungsi selama pengembangan.

## Implementasi Langkah‑demi‑Langkah

### Langkah 1: Buat Workbook dan Akses Worksheet Pertama
Pertama, impor kelas inti dan buat instance workbook baru. Ini memberi Anda file Excel bersih yang siap untuk penyisipan data.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Langkah 2: Isi Worksheet dengan Contoh Nama
Selanjutnya, tambahkan beberapa string nama lengkap ke kolom **A**. Pada proyek nyata Anda akan membaca data ini dari basis data atau file CSV.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Langkah 3: Konfigurasikan Text Load Options untuk Membagi Kolom
Kelas `TxtLoadOptions` memberi tahu Aspose.Cells cara menafsirkan teks. Di sini kami menggunakan spasi (`' '`) sebagai pemisah.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Langkah 4: Bagi Teks menjadi Dua Kolom
Sekarang panggil `textToColumns()` pada area sel yang berisi nama. Parameter `(0, 0, 5, opts)` berarti *mulai dari baris 0, kolom 0, proses 5 baris, menggunakan opsi yang baru saja kami definisikan*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Setelah pemanggilan ini, kolom A berisi nama depan dan kolom B berisi nama belakang.

### Langkah 5: Simpan Workbook sebagai File XLSX
Akhirnya, tulis workbook yang telah dimodifikasi ke disk. Enum `SaveFormat` memastikan file disimpan dalam format XLSX modern.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Mengapa ini penting:** Dengan menggunakan **save workbook xlsx**, Anda menjamin kompatibilitas dengan versi terbaru Excel, Google Sheets, dan alat spreadsheet lainnya.

## Aplikasi Praktis
- **Pembersihan Data:** Memisahkan bidang yang digabungkan dengan cepat sebelum dimuat ke pipeline analitik.  
- **Integrasi CRM:** Mengubah daftar kontak datar menjadi tabel terstruktur untuk impor.  
- **Sistem HR:** Membagi nama lengkap karyawan untuk penggajian atau proses tunjangan.

## Pertimbangan Kinerja
Saat bekerja dengan ribuan baris:

1. **Pembaruan Batch:** Gunakan `ws.getCells().setRowHeight()` atau metode batch serupa untuk mengurangi overhead.  
2. **Manajemen Memori:** Panggil `wb.calculateFormula()` hanya bila diperlukan, dan buang objek besar sesegera mungkin.  
3. **Garbage Collection:** Jalankan JVM dengan pengaturan heap yang tepat (`-Xmx2g` untuk file besar) agar terhindar dari error OutOfMemory.

## Masalah Umum dan Solusinya
| Masalah | Solusi |
|-------|----------|
| **Nama mengandung inisial tengah** (mis., “John A. Doe”) | Sesuaikan pemisah atau proses kolom kedua untuk mengekstrak nama belakang. |
| **Sel kosong yang tidak terduga** | Pastikan rentang sumber (`textToColumns` parameters) cocok dengan baris data sebenarnya. |
| **Lisensi tidak ditemukan** | Letakkan file lisensi sementara (`Aspose.Cells.lic`) di root proyek atau set lisensi secara programatis. |

## Pertanyaan yang Sering Diajukan

**T: Apa itu Aspose.Cells Java?**  
J: Sebuah perpustakaan kuat yang memungkinkan Anda membuat, memodifikasi, dan mengonversi file Excel secara programatis menggunakan Java.

**T: Bisakah saya membagi kolom berdasarkan pemisah selain spasi?**  
J: Ya, sesuaikan pemisah `TxtLoadOptions` sesuai kebutuhan data Anda.

**T: Bagaimana cara menangani dataset besar dengan Aspose.Cells?**  
J: Optimalkan kinerja dengan mengelola memori dan meminimalkan operasi workbook, seperti dijelaskan di atas.

**T: Apakah ada dukungan jika saya mengalami masalah?**  
J: Kunjungi [Aspose Forum](https://forum.aspose.com/c/cells/9) untuk bantuan komunitas atau hubungi tim dukungan Aspose secara langsung.

**T: Format apa saja yang dapat Aspose.Cells simpan untuk workbook?**  
J: Mendukung beragam format file Excel, termasuk XLSX, XLS, CSV, dan lainnya.

## Sumber Daya

- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Free Trial**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Temporary License**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Selamat coding, dan nikmati memanfaatkan kekuatan penuh **aspose cells java** dalam proyek Anda!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Terakhir Diperbarui:** 2026-03-15  
**Diuji Dengan:** Aspose.Cells 25.3 untuk Java  
**Penulis:** Aspose