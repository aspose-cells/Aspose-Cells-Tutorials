---
category: general
date: 2026-07-29
description: Simpan workbook baru di Java sambil menyalin rentang antar workbook.
  Pelajari cara mentransfer rentang Excel dan mempertahankan format penyalinan dalam
  beberapa langkah saja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save new workbook
- copy range between workbooks
- transfer excel range
- load excel workbook java
- preserve formatting copy
language: id
lastmod: 2026-07-29
og_description: Simpan workbook baru di Java dengan Aspose.Cells—pelajari cara menyalin
  rentang antar workbook sambil mempertahankan format, semuanya dalam panduan langkah
  demi langkah yang ringkas.
og_image_alt: Java code that saves new workbook after transferring an Excel range
og_title: Simpan Workbook Baru di Java – Salin Rentang Antara Workbook
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Save new workbook in Java while copy range between workbooks. Learn
    to transfer Excel range and preserve formatting copy in just a few steps.
  headline: Save New Workbook in Java – Copy Range Between Workbooks Tutorial
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- File I/O
title: Simpan Workbook Baru di Java – Tutorial Menyalin Rentang Antara Workbook
url: /id/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save New Workbook in Java – Copy Range Between Workbooks Tutorial

Pernahkah Anda perlu **save new workbook** setelah memindahkan data dari satu file Excel ke file lainnya, tetapi tidak yakin bagaimana menjaga gaya asli? Anda tidak sendirian. Dalam banyak aplikasi perusahaan kami harus **transfer Excel range** dari templat ke file yang dihasilkan pengguna, dan triknya adalah memastikan format tetap terjaga selama proses.

Dalam panduan ini kami akan membahas contoh lengkap yang dapat dijalankan yang **load Excel workbook java**‑style menggunakan Aspose.Cells, **copy range between workbooks**, dan akhirnya **save new workbook** dengan semua warna, border, dan format angka asli tetap utuh. Tanpa basa‑basi—hanya kode yang dapat Anda masukkan ke dalam proyek Anda hari ini.

> **Pro tip:** Jika Anda sudah menggunakan Maven, tambahkan dependensi Aspose.Cells sekali saja dan Anda akan siap untuk tugas manipulasi workbook apa pun.

## Prasyarat

- Java 17 (atau JDK terbaru apa pun)
- Aspose.Cells untuk Java (versi 23.10 atau lebih baru)
- Familiaritas dasar dengan Java I/O
- Dua file Excel: sumber (`source.xlsx`) yang berisi data yang ingin Anda pindahkan, dan tujuan kosong (`dest.xlsx`) yang akan dibuat oleh kode

Sekarang, mari kita selami langkah‑langkahnya.

## Langkah 1 – Load Excel Workbook Java Style

Hal pertama yang kami lakukan adalah **load Excel workbook java**‑wise. Aspose.Cells mengabstraksi format file, sehingga Anda tidak perlu khawatir tentang XML di baliknya.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // Load the source workbook (make sure the path is correct)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // ------------------------------------------------------------
        // At this point the source workbook is fully loaded in memory.
        // ------------------------------------------------------------
```

*Mengapa ini penting:* Memuat workbook memberi Anda akses ke setiap worksheet, sel, dan objek gaya. Jika Anda melewatkan langkah ini dan mencoba menyalin langsung dari aliran file, Anda akan kehilangan kemampuan untuk mempertahankan format nanti.

## Langkah 2 – Tentukan Rentang Sumber (Preserve Formatting Copy)

Selanjutnya kami menentukan area tepat yang ingin dipindahkan. Dalam contoh kami rentang `A1:G20` berisi tabel pivot dan beberapa baris header. Dengan membuat objek `Range` kami dapat memberi tahu Aspose.Cells untuk menjaga setiap gaya tetap utuh—ini adalah esensi dari **preserve formatting copy**.

```java
        // Grab the first worksheet
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // Define the range that includes the data we want to copy
        // Using createRange ensures we capture formulas, formats, and comments.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Tip:* Jika Anda perlu menyalin area dinamis, Anda dapat menghitung baris/kolom terakhir yang digunakan dengan `sourceSheet.getCells().getMaxDataRow()` dan membangun string alamat secara langsung.

## Langkah 3 – Buat Workbook Tujuan (Tempat Kami Akan Save New Workbook)

Sekarang kami membuat workbook baru yang akan menerima data. Di sinilah aksi **save new workbook** pada akhirnya akan terjadi.

```java
        // Create a brand‑new workbook that will become our destination file
        Workbook destinationWorkbook = new Workbook();

        // Get its first worksheet – this is where we’ll paste the range
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);
```

*Mengapa kami membuat yang baru:* Memulai dengan workbook bersih menjamin tidak ada gaya yang tersisa yang dapat bentrok dengan rentang yang masuk. Ini juga membuat ukuran file akhir lebih kecil karena hanya sumber daya yang diperlukan yang disimpan.

## Langkah 4 – Copy Range Between Workbooks

Berikut inti dari tutorial: **copy range between workbooks** sambil mempertahankan setiap petunjuk visual. Kelas `CopyOptions` memungkinkan kami menentukan bahwa kami menginginkan salinan penuh, bukan hanya nilai.

```java
        // Set up copy options to keep everything—values, formulas, formats, comments.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // ensures formatting stays

        // Perform the copy. The destination starts at cell A1 (row 0, column 0).
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);
```

*Pertanyaan umum:* *Bagaimana jika saya hanya membutuhkan nilai, bukan format?* Ubah `PasteType.ALL` menjadi `PasteType.VALUES` dan format akan diabaikan.

## Langkah 5 – Save New Workbook

Akhirnya kami menulis file tujuan ke disk. Inilah momen di mana kami benar‑benar **save new workbook** dan melihat hasil dari langkah‑langkah sebelumnya.

```java
        // Persist the destination workbook to the file system
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

Saat Anda membuka `dest.xlsx` Anda akan melihat tampilan dan nuansa yang persis sama dengan rentang `source.xlsx` asli—warna, border, dan format angka semuanya tetap utuh.

---

<img src="excel-copy.png" alt="Kode Java yang menyimpan workbook baru setelah mentransfer rentang Excel" />

## Contoh Kerja Lengkap (Semua Langkah Digabungkan)

Berikut adalah program lengkap yang berdiri sendiri. Salin ke dalam file bernama `ExcelRangeTransfer.java`, sesuaikan jalur file, dan jalankan dengan `javac`/`java`.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2️⃣ Get the first worksheet and define the range we want to copy
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the defined range – preserving formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);

        // 5️⃣ Save new workbook to disk
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

**Output yang diharapkan** ketika Anda menjalankan program:

```
Destination workbook saved successfully.
```

Buka `dest.xlsx` dan Anda akan melihat replika persis `A1:G20` dari sumber, lengkap dengan gaya aslinya.

## Pertanyaan yang Sering Diajukan & Kasus Tepi

| Question | Answer |
|----------|--------|
| *Bisakah saya menyalin antar workbook yang menggunakan versi Excel berbeda?* | Ya. Aspose.Cells menormalkan format secara internal, sehingga sumber `.xls` dapat disalin ke tujuan `.xlsx` tanpa pekerjaan tambahan. |
| *Bagaimana jika tujuan sudah berisi data?* | Gunakan `copyRange` dengan baris/kolom mulai yang berbeda (mis., `5, 2`) untuk menempel di tempat lain, atau bersihkan sheet terlebih dahulu dengan `destSheet.getCells().clearAll()`. |
| *Apakah formula tetap terhubung ke workbook asli?* | Secara default mereka menjadi **relative** terhadap tujuan. Jika Anda memerlukan referensi eksternal, setel `copyOptions.setPasteType(PasteType.FORMULAS)` dan tangani tautan workbook secara manual. |
| *Bagaimana cara mempertahankan lebar kolom?* | Lebar kolom merupakan bagian dari format; `PasteType.ALL` sudah menyalinnya. Jika Anda melihat perbedaan, panggil `destSheet.autoFitColumns()` setelah penyalinan. |

## Langkah Selanjutnya – Melampaui Dasar

Sekarang Anda tahu cara **save new workbook**, **copy range between workbooks**, dan **preserve formatting copy**, Anda mungkin ingin menjelajahi:

- **Batch processing** – iterasi melalui folder berkas sumber dan hasilkan laporan terpusat.
- **Conditional formatting transfer** – gunakan `CopyOptions.setPasteType(PasteType.FORMATS)` untuk fokus hanya pada gaya.
- **Streaming API** – untuk file besar, kelas `Workbook` menawarkan mode memori rendah yang tetap mendukung penyalinan rentang.

Setiap topik ini dibangun secara alami dari konsep yang dibahas di sini, dan semuanya berputar di sekitar ide inti yang sama: memanipulasi file Excel di Java dengan percaya diri dan presisi.

---

### TL;DR

Kami memulai dengan **load excel workbook java**, menentukan **transfer excel range**, menggunakan **copy range between workbooks** dengan `CopyOptions` untuk **preserve formatting copy**, membuat file baru, dan akhirnya **save new workbook**. Hasilnya adalah `dest.xlsx` yang berfungsi penuh dan mencerminkan rentang sumber hingga gaya sel terakhir.

Cobalah, ubah alamat rentang, dan lihat betapa cepatnya Anda dapat mengotomatisasi tugas pelaporan Excel di Java. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengimplementasikan Named Range dengan Workbook Scope di Aspose.Cells Java untuk Manajemen Data Excel yang Ditingkatkan](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Simpan Workbook Excel dengan Aspose.Cells untuk Java – Panduan Lengkap](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [Simpan File Excel Java dengan Aspose.Cells – Menguasai Otomatisasi Workbook](/cells/english/java/automation-batch-processing/aspose-cells-java-excel-workbook-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}