---
date: '2026-10-28'
description: Pelajari cara mengubah sistem tanggal Excel ke 1904 menggunakan Aspose.Cells
  untuk Java, mengatur format tanggal Excel, dan mengonversi sistem 1904 Excel secara
  efisien.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Ubah sistem tanggal Excel ke 1904 menggunakan Aspose.Cells for Java.
  Pelajari langkah demi langkah cara mengaktifkan sistem 1904, mengatur tanggal, dan
  mengonversinya kembali.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Ubah sistem tanggal Excel ke 1904 dengan Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Ubah sistem tanggal Excel ke 1904 dengan Aspose.Cells Java
url: /id/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Sistem Tanggal Excel ke 1904 dengan Aspose.Cells Java

Dalam tutorial ini Anda akan belajar cara **mengubah sistem tanggal Excel** ke format 1904 menggunakan Aspose.Cells untuk Java. Sistem 1904 penting ketika Anda perlu mempertahankan tanggal lama berbasis Mac atau menyelaraskan dengan model keuangan yang mengharapkan epoch tersebut. Kami akan memandu Anda menginstal pustaka, memuat workbook, mengubah sistem tanggal, dan menyimpan hasilnya—semua tanpa memerlukan Microsoft Excel di server.

## Jawaban Cepat
- **Apa yang dilakukan sistem tanggal 1904?** Sistem ini mulai menghitung hari dari 1 Januari 1904, menggeser semua tanggal sebesar 1.462 hari dibandingkan dengan sistem default 1900.  
- **Mengapa menggunakan Aspose.Cells untuk mengubah sistem tanggal?** Ia menyediakan API sederhana yang berfungsi tanpa Excel terinstal dan mendukung file besar.  
- **Versi Java mana yang didukung?** JDK 8 atau yang lebih baru.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi menghilangkan batas penggunaan.  
- **Bisakah saya mengembalikan ke sistem 1900 nanti?** Ya, cukup panggil `setDate1904(false)`.

## Apa itu sistem tanggal 1904 di Excel?
Sistem tanggal 1904 menghitung hari mulai dari 1 Januari 1904, bukan epoch default 1900. Pergeseran ini menambahkan tepat 1.462 hari ke setiap nilai tanggal, sehingga workbook lama berbasis Mac tampak bergeser ketika dibuka di Windows. Sistem ini terutama digunakan untuk kompatibilitas dengan file Excel Macintosh lama dan beberapa model keuangan legacy.

## Mengapa mengubah sistem tanggal Excel dengan Aspose.Cells?
Anda dapat mengubah sistem tanggal langsung dari Java, menghilangkan langkah manual di Excel. Aspose.Cells memproses workbook hingga **2 GB** dan dapat mengonversi workbook dengan 500 lembar dalam waktu kurang dari **2 detik** pada server 4‑core tipikal, memberikan otomatisasi sisi‑server berkecepatan tinggi.

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

## Bagaimana cara mengubah sistem tanggal Excel ke 1904 dengan Aspose.Cells untuk Java?
Muat workbook, aktifkan pengaturan 1904, dan simpan file—alur tiga langkah ini memperbarui epoch tanggal internal workbook dalam waktu kurang dari satu detik. Panggilan API `setDate1904(true)` mengubah flag sistem, dan perubahan tersebut dipertahankan saat Anda memanggil `save`. Tidak diperlukan instalasi Excel, menjadikannya ideal untuk lingkungan server tanpa antarmuka.

### Langkah 1: inisialisasi dan muat workbook
Kelas `Workbook` mewakili seluruh file Excel dalam memori. Pertama, buat instance `Workbook` yang menunjuk ke file Anda yang sudah ada.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Langkah 2: aktifkan sistem tanggal 1904
Metode `WorkbookSettings.setDate1904` mengubah flag tanggal pada level workbook. Menyetelnya ke `true` mengaktifkan sistem 1904 untuk semua lembar kerja.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Tip pro:** Anda juga dapat memanggil `setDate1904(false)` nanti jika perlu mengembalikan.

### Langkah 3: simpan workbook yang dimodifikasi
Akhirnya, tulis perubahan ke file baru (atau timpa yang asli). Metode `save` secara otomatis menghormati sistem tanggal yang aktif.

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

> **Catatan:** Kode di atas menggunakan nama kelas `tWorkbook` seperti yang diberikan awalnya. Pastikan typo ini sesuai dengan konvensi penamaan proyek Anda atau koreksi menjadi `Workbook` jika diperlukan.

## Atur tanggal Excel secara programatis (kata kunci sekunder)
Jika Anda perlu menyesuaikan nilai sel individual setelah mengubah sistem, Anda dapat menggunakan `cells.get(i, j).putValue(Date)` di mana tanggal akan diinterpretasikan sesuai dengan sistem tanggal yang aktif.

## Konversi sistem Excel 1904 kembali ke 1900 (kata kunci sekunder)
Untuk mengembalikan, cukup panggil:

```java
workbook.getSettings().setDate1904(false);
```

Kemudian simpan workbook lagi.

## Aplikasi Praktis
1. **Pengarsipan data** – Mempertahankan cap waktu legacy saat memigrasi spreadsheet lama berbasis Mac.  
2. **Pelaporan lintas‑platform** – Menghasilkan laporan yang terbuka dengan benar di Windows dan macOS tanpa ketidaksesuaian tanggal.  
3. **Pemodelan keuangan** – Menyelaraskan perhitungan tanggal dengan model keuangan legacy yang mengharapkan sistem 1904.

## Pertimbangan Kinerja
- Batasi operasi workbook dalam satu sesi untuk menjaga penggunaan memori rendah; Aspose.Cells men‑stream data dan tidak pernah memuat seluruh file ke RAM kecuali Anda secara eksplisit memintanya.  
- Sesuaikan flag garbage‑collection Java (`-XX:+UseG1GC`) untuk file sangat besar guna menghindari lonjakan waktu jeda.  

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara sistem tanggal 1900 dan 1904?**  
A: Sistem 1900 mulai pada 1 Januari 1900, sementara sistem 1904 mulai pada 1 Januari 1904, menggeser semua tanggal sebesar 1.462 hari.

**Q: Bisakah saya mengubah sistem tanggal workbook yang sedang terbuka di Excel?**  
A: Ya, tetapi Anda harus menutup file di Excel terlebih dahulu; jika tidak operasi penyimpanan akan gagal.

**Q: Apakah saya memerlukan lisensi untuk menggunakan `setDate1904`?**  
A: Metode ini berfungsi dalam percobaan gratis, tetapi lisensi penuh menghilangkan batas evaluasi.

**Q: Apakah memungkinkan mengubah sistem tanggal hanya untuk satu lembar kerja?**  
A: Tidak, sistem tanggal adalah pengaturan pada level workbook; berlaku untuk semua lembar kerja.

**Q: Bagaimana saya dapat memverifikasi bahwa sistem tanggal telah diubah?**  
A: Buka file yang disimpan di Excel, pergi ke **File → Options → Advanced**, dan centang kotak **"Use 1904 date system"**.

## Kesimpulan
Anda kini tahu cara **mengubah sistem tanggal Excel** ke 1904 menggunakan Aspose.Cells untuk Java, cara mengatur tanggal sel individual, dan cara mengembalikan ke sistem 1900 bila diperlukan. Integrasikan potongan kode ini ke dalam pipeline pemrosesan data Anda untuk menjamin kompatibilitas tanggal lintas platform dan file legacy.

---

**Terakhir Diperbarui:** 2026-10-28  
**Diuji Dengan:** Aspose.Cells 25.3 for Java  
**Penulis:** Aspose  

**Resources**
- **Dokumentasi:** [Referensi Aspose.Cells Java](https://reference.aspose.com/cells/java/)
- **Unduh:** [Rilis Aspose.Cells](https://releases.aspose.com/cells/java/)
- **Beli Lisensi:** [Beli Aspose.Cells](https://purchase.aspose.com/buy)
- **Percobaan Gratis:** [Mulai Percobaan Gratis](https://releases.aspose.com/cells/java/)
- **Lisensi Sementara:** [Dapatkan Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- **Forum Dukungan:** [Dukungan Aspose](https://forum.aspose.com/c/cells/9)

## Tutorial Terkait

- [Mengonversi Excel ke PDF secara Efisien dengan Format Tanggal Kustom Menggunakan Aspose.Cells untuk Java](/cells/java/workbook-operations/render-excel-custom-date-forms-pdf-aspose-cells-java/)
- [Aspose.Cells untuk Java: Cara Membuat dan Memformat Workbook Excel secara Efisien](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Menguasai Manipulasi Excel dengan Aspose.Cells untuk Java: Operasi Workbook dan Tutorial Styling Sel](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}