---
category: general
date: 2026-06-30
description: Cara menyalin rentang di Java menggunakan Aspose.Cells – menggandakan
  rentang Excel, menyalin tabel pivot, dan memuat buku kerja Excel secara efisien.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: id
og_description: Cara menyalin rentang di Java dengan Aspose.Cells. Pelajari cara menggandakan
  rentang Excel, menyalin tabel pivot, dan memuat workbook Excel dalam hitungan menit.
og_title: Cara menyalin rentang di Java – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Cara menyalin rentang di Java – Menyalin Tabel Pivot dengan Aspose.Cells
url: /id/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin rentang di Java – Menyalin Tabel Pivot dengan Aspose.Cells

Pernah bertanya-tanya **bagaimana cara menyalin rentang** dari satu workbook Excel ke workbook lain tanpa kehilangan integritas tabel pivot? Anda bukan satu-satunya. Dalam banyak alur pelaporan, kebutuhan untuk *menyalin rentang Excel* sambil mempertahankan logika pivot menjadi masalah harian. Untungnya, Aspose.Cells untuk Java membuat ini mudah, dan dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang juga menunjukkan cara **memuat workbook Excel**, menyalin tabel pivot, dan menyimpan hasilnya.

Pada akhir panduan ini Anda akan memiliki program Java yang berdiri sendiri yang:

* Memuat workbook yang ada (`load excel workbook`);
* Menentukan sel‑sel tepat yang berisi tabel pivot;
* Menyalin **pivot table to sheet** ke dalam workbook baru;
* Menyimpan file baru, siap untuk pemrosesan lanjutan.

Tidak ada skrip eksternal, tidak ada langkah manual—hanya kode murni.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

* Java 8 atau lebih baru (kode ini juga bekerja dengan Java 11+);
* Perpustakaan Aspose.Cells untuk Java (Anda dapat mengunduhnya dari Maven Central);
* Dua file Excel contoh – satu sumber dengan tabel pivot (`source.xlsx`) dan satu folder tujuan tempat Anda akan menulis `copy-pivot.xlsx`.

Itu saja. Tidak diperlukan trik IDE yang rumit; editor teks apa pun plus `javac` sudah cukup.

## Langkah 1: Siapkan Proyek dan Impor Aspose.Cells

Pertama-tama—mari kita menambahkan perpustakaan ke dalam proyek. Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Jika Anda tidak menggunakan Maven, unduh JAR dari situs Aspose dan letakkan di classpath Anda. Setelah itu selesai, buat kelas Java baru bernama `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Jaga folder `src/main/java` Anda tetap bersih dan beri kelas nama yang bermakna; ini memudahkan pemeliharaan di masa depan.

## Langkah 2: Muat Workbook Sumber (`load excel workbook`)

Sekarang kita benar‑benar **load excel workbook** yang berisi tabel pivot yang ingin disalin. `Konstruktor Workbook` menerima jalur file, jadi pastikan jalurnya benar.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Mengapa kita memilih lembar kerja pertama? Dalam kebanyakan kasus sederhana pivot berada di lembar pertama, tetapi Anda dapat mengubah indeks atau menggunakan nama lembar jika diperlukan. Fleksibilitas ini adalah salah satu alasan mengapa Aspose.Cells bersinar.

## Langkah 3: Tentukan Rentang yang Menampung Tabel Pivot

Tabel pivot biasanya mencakup blok sel. Misalkan ia menempati `A1:G20`. Anda dapat menyesuaikan alamatnya agar cocok dengan data sebenarnya.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Jika Anda tidak yakin dengan alamat tepatnya, buka workbook di Excel, pilih seluruh pivot, dan lihat kotak nama. Ingat, **duplicate excel range** bekerja paling baik ketika Anda menargetkan area yang tepat—tanpa baris tambahan, tanpa kolom yang hilang.

## Langkah 4: Buat Workbook Baru untuk Tujuan

Kita membutuhkan workbook baru yang akan menerima rentang yang disalin. Di sinilah kita akan **copy pivot table** ke lembar baru.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Pada titik ini workbook tujuan masih kosong, tetapi Aspose.Cells secara otomatis menambahkan lembar default, yang akan kita gunakan sebagai target.

## Langkah 5: Salin Rentang – Tabel Pivot Tetap Utuh

Berikut baris ajaib yang **copy pivot table** sambil mempertahankan semua koneksi internalnya.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

`Metode copy` menerima dua argumen: `Range` sumber dan `Range` tujuan. Dengan memulai tujuan di `A1`, kita menempatkan pivot persis di tempatnya pada sumber. Aspose.Cells menyalin cache pivot yang mendasarinya, sehingga workbook baru tetap tahu cara menyegarkan pivot.

## Langkah 6: Simpan Workbook Hasil

Akhirnya, tulis file baru ke disk. Anda dapat memilih format apa pun yang didukung Aspose (`.xlsx`, `.xls`, `.csv`, dll.). Kami akan tetap menggunakan `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Jalankan program, dan Anda akan melihat workbook baru dengan tata letak pivot yang sama. Buka di Excel—jika semuanya berjalan baik, Anda dapat menyegarkan pivot tanpa error.

### Output yang Diharapkan

Ketika Anda mengeksekusi `CopyPivotDemo`, konsol mencetak:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Membuka `copy-pivot.xlsx` memperlihatkan lembar yang tampak identik dengan area pivot sumber, dan **pivot table to sheet** berfungsi persis seperti aslinya.

## Contoh Lengkap yang Berfungsi

Berikut adalah kelas Java lengkap yang siap dijalankan yang menggabungkan semua langkah. Salin‑tempel ke IDE Anda, sesuaikan jalur file, dan jalankan.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Catatan:** Jika tabel pivot Anda melintasi lebih dari satu lembar kerja, ulangi langkah penyalinan untuk setiap lembar yang relevan, atau gunakan `Workbook.copy` untuk menggandakan seluruh lembar kerja.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika workbook sumber memiliki banyak lembar kerja?

Anda dapat melakukan loop melalui `sourceWorkbook.getWorksheets()` dan menyalin setiap rentang yang relevan. Hati‑hati untuk mempertahankan nama lembar yang sama di tujuan jika Anda perlu menjaga referensi.

### Apakah pivot yang disalin mempertahankan sumber datanya?

Ya. Aspose.Cells menyalin cache pivot bersama dengan rentang, sehingga workbook tujuan masih mengacu pada sumber data asli dalam file yang sama. Jika Anda kemudian memindahkan data ke lembar lain, Anda mungkin perlu menyegarkan pivot secara manual.

### Bagaimana menyalin pivot yang menggunakan sumber data eksternal?

Ketika sumber data pivot adalah file eksternal, Anda harus menyematkan data tersebut ke dalam workbook tujuan terlebih dahulu (misalnya, menyalin rentang data sumber) sebelum menyalin pivot. Jika tidak, pivot akan menampilkan error “#REF!”.

### Bisakah saya menyalin pivot tanpa data di sekitarnya?

Tentu saja. Cukup sesuaikan `pivotRange` untuk mencakup hanya sel‑sel pivot (biasanya sudut kiri‑atas plus area data). Anda juga dapat menggunakan `sourceSheet.getPivotTables().get(0).getPivotTableArea()` untuk mengambil rentang tepat secara programatis.

## Tips untuk Proyek Dunia Nyata

* **Batch processing:** Jika Anda perlu menyalin puluhan workbook, bungkus kode di atas dalam sebuah metode dan panggil di dalam loop yang mengiterasi direktori.
* **Performance:** Untuk file besar, gunakan kembali satu instance `Workbook` dan panggil `Workbook.calculateFormula()` hanya setelah semua penyalinan selesai.
* **Error handling:** Bungkus logika penyalinan dengan blok try‑catch dan log `Exception.getMessage()`; Aspose melempar `CellsException` untuk rentang yang tidak valid.

## Kesimpulan

Kami baru saja membahas **how to copy range** di Java menggunakan Aspose.Cells, menunjukkan cara **duplicate excel range**, **copy pivot table**, dan **load excel workbook** semuanya dalam satu program rapi. Langkah‑langkahnya sederhana, kode dapat dijalankan sepenuhnya, dan pendekatannya dapat diskalakan dari demo satu lembar hingga pekerjaan batch tingkat perusahaan.

Siap untuk tantangan berikutnya? Coba ekspor pivot yang disalin ke PDF, atau segarkan secara programatis setelah menambahkan data baru. Kedua tugas tersebut dibangun di atas fondasi yang sama yang kami jelaskan di sini, sehingga Anda siap menghadapinya.

Ada pertanyaan atau ingin berbagi modifikasi Anda? Tinggalkan komentar di bawah—selamat coding! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengimplementasikan Named Range dengan Lingkup Workbook di Aspose.Cells Java untuk Manajemen Data Excel yang Ditingkatkan](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Cara Menyalin Beberapa Kolom di Excel Menggunakan Aspose.Cells Java: Panduan Lengkap](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Menyalin Data Rentang](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}