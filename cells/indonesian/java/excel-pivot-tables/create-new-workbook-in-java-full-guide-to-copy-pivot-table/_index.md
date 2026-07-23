---
category: general
date: 2026-07-23
description: Buat workbook baru di Java dan pelajari cara menyalin tabel pivot, menyalin
  rentang Excel, serta mengekspor tabel pivot dengan Aspose.Cells dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: id
lastmod: 2026-07-23
og_description: Buat workbook baru di Java dan segera salin tabel pivot, salin rentang
  Excel, lalu ekspor tabel pivot menggunakan Aspose.Cells. Ikuti tutorial lengkap
  ini.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Buat Workbook Baru di Java – Salin Tabel Pivot Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Buat Workbook Baru di Java – Panduan Lengkap untuk Menyalin Tabel Pivot
url: /id/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Baru di Java – Panduan Lengkap Menyalin Pivot Table

Pernah bertanya-tanya bagaimana cara **create new workbook** di Java sambil mempertahankan pivot table yang kompleks? Anda bukan satu-satunya yang kebingungan tentang ini. Dalam banyak aplikasi pelaporan Anda perlu memindahkan pivot dari file sumber ke workbook baru, mungkin untuk dikirim ke klien atau untuk melakukan perhitungan lebih lanjut. Kabar baiknya? Dengan beberapa baris kode Anda dapat melakukan hal itu—tanpa harus menyalin‑tempel secara manual.

Dalam tutorial ini kami akan membahas seluruh proses: memuat file sumber, mendefinisikan rentang yang berisi pivot, **copying the Excel range**, membuat **new workbook**, dan akhirnya **exporting the pivot table** ke file baru. Pada akhir tutorial Anda akan memiliki program Java yang berdiri sendiri dan dapat dijalankan yang menjawab pertanyaan “**how to copy pivot**” tanpa tebakan.

## Prasyarat

- Java 17 atau lebih baru (kode ini bekerja dengan JDK terbaru apa pun)
- Perpustakaan Aspose.Cells untuk Java (versi percobaan gratis atau berlisensi)
- Contoh `source.xlsx` yang berisi pivot table dalam rentang `A1:G20`
- IDE atau alat build (Maven/Gradle) untuk mengelola JAR Aspose.Cells

Sudah siap? Bagus—mari kita mulai.

## Langkah 1: Siapkan Proyek dan Impor Aspose.Cells

First things first, you need to add Aspose.Cells to your project. If you’re using Maven, drop this dependency into your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

If you prefer Gradle, the equivalent is:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Once the library is on the classpath, import the classes you’ll need:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells adalah perpustakaan komersial, tetapi menyediakan evaluasi 30‑hari yang berfungsi penuh dan menambahkan watermark pada output—sempurna untuk mencoba ini.

## Langkah 2: Muat Workbook Sumber

Sekarang kami akan **create new workbook** objek, tetapi pertama-tama kami membutuhkan sumber yang berisi pivot. Langkah ini adalah dasar untuk setiap operasi **copy excel range** karena objek rentang mengetahui tepat sel mana (termasuk pivot cache) yang harus dipindahkan.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Mengapa tidak langsung membaca rentang? Karena metadata pivot table berada di pivot cache worksheet, dan Aspose.Cells secara otomatis menggabungkannya saat Anda menyalin rentang.

## Langkah 3: Definisikan Rentang yang Menyimpan Pivot Table

Dalam banyak file dunia nyata, pivot menempati blok persegi panjang. Untuk contoh ini kami akan mengasumsikan berada di `A1:G20`. Tentu saja Anda dapat menyesuaikan alamatnya agar sesuai dengan tata letak Anda.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Jika Anda tidak yakin dengan alamat tepatnya, Anda dapat menggunakan `sourceSheet.getCells().getMaxDataRow()` dan `getMaxDataColumn()` untuk menghitung batas secara dinamis. Itu trik berguna ketika ukuran pivot berubah seiring waktu.

## Langkah 4: **Create New Workbook** dan Worksheet Tujuan

Inilah saat kita benar‑benar **create new workbook** yang akan menerima konten yang disalin. Anggap ini sebagai kanvas kosong tempat Anda menempelkan pivot.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Mengapa memulai dengan workbook kosong? Ini menjamin tidak ada gaya tersembunyi atau pivot sebelumnya yang mengganggu penyalinan, memberikan hasil bersih yang siap untuk **export pivot table**.

## Langkah 5: Salin Pivot Table (dan Rentang Dasarnya)

Sekarang inti tutorial: **copy pivot table**. Aspose.Cells memperlakukan penyalinan rentang sebagai deep copy, artinya pivot cache ikut bersama sel. Itulah mengapa satu baris ini melakukan pekerjaan berat.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Jika Anda pernah bertanya-tanya **how to copy pivot** tanpa kehilangan fungsionalitasnya, ini jawabannya. Sheet tujuan kini berisi pivot yang berfungsi penuh yang dapat Anda refresh, modifikasi, atau cukup export.

### Kasus Tepi: Mempertahankan Pengaturan Refresh

Sometimes the source pivot is set to refresh on opening. To keep that behavior, you can copy the pivot’s options explicitly:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Potongan kode itu memastikan pivot yang disalin berperilaku persis seperti yang asli.

## Langkah 6: Simpan Workbook Tujuan – **Export Pivot Table**

Akhirnya, kami **export pivot table** dengan menyimpan workbook baru ke disk. Anda dapat memilih format apa pun yang didukung Aspose: XLSX, XLS, CSV, PDF, dll. Untuk panduan ini kami akan tetap menggunakan XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Jika Anda perlu mengirim file melalui layanan web, Anda dapat menulisnya ke `ByteArrayOutputStream` alih-alih ke path file—Aspose membuatnya sangat mudah.

## Contoh Lengkap yang Berjalan

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan. Silakan salin, tempel, dan jalankan di IDE Anda.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Output yang Diharapkan

When you run the program, the console prints:

```
Pivot table copied successfully!
```

Dan file `copied_with_pivot.xlsx` muncul di `YOUR_DIRECTORY`. Buka di Excel, dan Anda akan melihat pivot table tetap utuh, siap untuk di-refresh atau diedit.

## Pertanyaan Umum & Pemecahan Masalah

- **Bagaimana jika pivot sumber melintasi lebih dari satu worksheet?**  
  Anda perlu menyalin setiap rentang relevan secara terpisah, lalu membuat kembali pivot di sheet tujuan menggunakan API `PivotTable`.

- **Bisakah saya menyalin hanya tata letak pivot tanpa data?**  
  Setel `sourceRange.setCopyDataOnly(false)` sebelum penyalinan. Ini memberi tahu Aspose untuk mempertahankan cache tetapi tidak data sumber yang mendasarinya.

- **Apakah ada cara menyalin pivot ke file CSV?**  
  CSV tidak mendukung pivot, tetapi Anda dapat mengekspor *hasil* pivot dengan memanggil `pivotTable.calculate()` lalu menyimpan sheet sebagai CSV.

- **Mengapa pivot yang disalin kehilangan formatnya?**  
  Formatting berada di koleksi style. Setelah penyalinan, Anda dapat memanggil `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` untuk mentransfer style.

## Kesimpulan

Kami baru saja menunjukkan cara **create new workbook** di Java, **copy pivot table**, dan **export pivot table**—semua dengan contoh kode yang bersih dan dapat direproduksi. Dengan mendefinisikan **copy excel range** yang tepat, memanfaatkan semantik deep‑copy Aspose.Cells, dan mempertahankan pengaturan opsional, Anda dapat mengotomatisasi hampir semua tugas migrasi pivot.

Siap untuk langkah selanjutnya? Coba ubah format output ke PDF, atau lakukan loop melalui beberapa file sumber untuk memproses batch puluhan pivot. Pola yang sama berlaku—cukup sesuaikan path file dan alamat rentang.

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose.Cells untuk manipulasi pivot lanjutan. Selamat coding, dan nikmati waktu yang Anda hemat dengan mengotomatisasi pekerjaan menyalin‑tempel yang membosankan!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}