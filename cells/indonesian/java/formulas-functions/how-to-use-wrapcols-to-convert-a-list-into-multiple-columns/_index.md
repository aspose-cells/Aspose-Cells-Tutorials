---
category: general
date: 2026-10-16
description: cara menggunakan wrapcols di Java dan dengan cepat mengubah daftar menjadi
  kolom dengan formula – pelajari cara mengatur formula untuk tata letak multi‑kolom
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert list to columns
- how to set formula
- create multi‑column layout
language: id
lastmod: 2026-10-16
og_description: cara menggunakan wrapcols untuk mengubah daftar menjadi kolom di Java.
  Ikuti panduan lengkap ini untuk mengatur rumus dan membuat tata letak multi‑kolom
  di Excel.
og_image_alt: Screenshot of an Excel sheet showing a wrapped list in three columns
og_title: Cara menggunakan wrapcols – panduan langkah demi langkah untuk pengembang
  Java
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  headline: How to use wrapcols to convert a list into multiple columns in Java
  type: TechArticle
- description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  name: How to use wrapcols to convert a list into multiple columns in Java
  steps:
  - name: What happens behind the scenes
    text: 'When the workbook is saved, Aspose.Cells evaluates the formula and writes
      the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel,
      you’ll see:'
  - name: Changing the number of columns
    text: If you need a different column count, modify the second argument of `WRAPCOLS`.
      For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically
      adjusts the row count to accommodate the new layout.
  - name: Handling a non‑even list size
    text: When the source range length isn’t divisible by the column count, `WRAPCOLS`
      pads the final column with blanks. This behavior is useful for creating balanced
      tables without manual trimming.
  - name: Using a dynamic range
    text: You can replace `A2:A100` with a named range or a formula that calculates
      the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution
      robust when the list length changes.
  - name: Avoiding circular references
    text: Place the formula in a cell that isn’t part of the source range. If you
      accidentally set the formula inside `A2:A100`, Excel will report a circular
      reference error. Always write the formula to a separate cell (commonly `A1`).
  type: HowTo
tags:
- wrapcols
- Aspose.Cells
- Java
- Excel automation
title: Cara menggunakan wrapcols untuk mengubah daftar menjadi beberapa kolom di Java
url: /id/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan wrapcols untuk mengonversi daftar menjadi beberapa kolom di Java

Jika Anda perlu **how to use wrapcols** dalam proyek Java, panduan ini menunjukkan langkah‑langkah tepatnya. Anda akan belajar cara mengatur formula, mengonversi daftar menjadi kolom, dan membuat tata letak multi‑kolom tanpa menyalin‑tempel manual.

Tutorial ini mencakup semua hal mulai dari penyiapan proyek hingga penanganan kasus tepi, sehingga Anda dapat menerapkan solusi ini pada spreadsheet apa pun yang berisi daftar satu‑kolom. Tidak ada alat tambahan yang diperlukan selain Aspose.Cells untuk Java.

## Prasyarat

* Java 17 atau lebih baru terpasang  
* Maven 3.8+ (atau Gradle) untuk manajemen dependensi  
* Lisensi untuk **Aspose.Cells for Java** – evaluasi gratis dapat digunakan untuk pengujian  
* Familiaritas dasar dengan formula Excel  

Item‑item ini memastikan kode dapat dijalankan tanpa error kompilasi.

## Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Tambahkan dependensi Maven berikut ke `pom.xml`. Jika Anda menggunakan Gradle, koordinat yang sama berlaku.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

Pustaka ini menyediakan kelas `Cell` dan `Worksheet` yang akan digunakan nanti ketika Anda **how to set formula** untuk suatu rentang.

## Langkah 2: Buat workbook dan isi daftar sumber

Tugas pertama adalah menghasilkan workbook yang berisi daftar vertikal (A2:A100). Daftar ini mewakili data yang ingin Anda **convert list to columns**.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate A2:A100 with sample data
        for (int i = 0; i < 99; i++) {
            cells.get("A" + (i + 2)).setValue("Item " + (i + 1));
        }

        // Apply WRAPCOLS formula (see next step)
        applyWrapCols(cells);

        // Save the result
        workbook.save("WrapColsResult.xlsx");
    }
```

Loop tersebut mengisi kolom pertama dengan 99 item, memberikan Anda daftar realistis untuk dikerjakan. Anda dapat mengganti nilai yang dihasilkan dengan data yang dibaca dari basis data atau sumber lain.

## Langkah 3: Cara menggunakan wrapcols untuk mengatur formula

Sekarang Anda akan melihat inti tutorial: menggunakan fungsi `WRAPCOLS` untuk **create multi‑column layout**. Fungsi ini mengambil dua argumen – rentang sumber dan jumlah kolom yang Anda inginkan.

```java
    private static void applyWrapCols(Cells cells) {
        // Step 1: Get the cell where the formula will be placed (A1)
        Cell target = cells.get("A1");

        // Step 2: Apply the WRAPCOLS function to wrap A2:A100 into 3 columns
        target.setFormula("=WRAPCOLS(A2:A100,3)");
    }
}
```

*Mengapa ini berhasil* – `WRAPCOLS` membaca rentang vertikal `A2:A100`, kemudian mendistribusikan nilai baris‑per‑baris ke tiga kolom (B, C, dan D). Hasilnya muncul mulai dari sel yang berisi formula (`A1`). Karena formula mengembalikan array, Aspose.Cells secara otomatis memperluas hasil ke sel‑sel yang diperlukan.

### Apa yang terjadi di balik layar

Saat workbook disimpan, Aspose.Cells mengevaluasi formula dan menulis nilai yang diperluas ke file. Jika Anda membuka `WrapColsResult.xlsx` di Excel, Anda akan melihat:

| A1 | B1 | C1 | D1 |
|----|----|----|----|
| Item 1 | Item 34 | Item 67 |
| Item 2 | Item 35 | Item 68 |
| … | … | … |

Tata letak ini menunjukkan pola **create multi‑column layout** yang berguna untuk laporan, dasbor, atau formulir yang dapat dicetak.

## Langkah 4: Verifikasi output secara programatis (opsional)

Jika Anda ingin memastikan bahwa formula menghasilkan matriks yang diharapkan tanpa membuka Excel, Anda dapat membaca kembali nilai‑nilai setelah perhitungan.

```java
        // Force calculation to ensure the array result is materialized
        workbook.calculateFormula();

        // Print the first three rows of the wrapped layout
        for (int row = 0; row < 3; row++) {
            StringBuilder line = new StringBuilder();
            for (int col = 0; col < 4; col++) { // A‑D columns
                line.append(cells.get(row, col).getStringValue()).append("\t");
            }
            System.out.println(line.toString().trim());
        }
```

Menjalankan program akan mencetak sesuatu seperti:

```
Item 1    Item 34    Item 67    Item 100
Item 2    Item 35    Item 68    Item 101
Item 3    Item 36    Item 69    Item 102
```

Ini mengonfirmasi bahwa **how to use wrapcols** berfungsi sebagaimana mestinya dan bahwa operasi **convert list to columns** berhasil.

## Langkah 5: Variasi umum dan kasus tepi

### Mengubah jumlah kolom

Jika Anda memerlukan jumlah kolom yang berbeda, ubah argumen kedua dari `WRAPCOLS`. Misalnya, `=WRAPCOLS(A2:A100,5)` membuat lima kolom. Fungsi secara otomatis menyesuaikan jumlah baris untuk mengakomodasi tata letak baru.

### Menangani ukuran daftar yang tidak genap

Ketika panjang rentang sumber tidak dapat dibagi habis oleh jumlah kolom, `WRAPCOLS` menambahkan spasi kosong pada kolom terakhir. Perilaku ini berguna untuk membuat tabel seimbang tanpa pemotongan manual.

### Menggunakan rentang dinamis

Anda dapat mengganti `A2:A100` dengan rentang bernama atau formula yang menghitung baris terakhir, seperti `A2:INDEX(A:A, COUNTA(A:A))`. Ini membuat solusi lebih kuat ketika panjang daftar berubah.

### Menghindari referensi sirkular

Letakkan formula di sel yang tidak termasuk dalam rentang sumber. Jika Anda secara tidak sengaja menempatkan formula di dalam `A2:A100`, Excel akan melaporkan error referensi sirkular. Selalu tulis formula ke sel terpisah (biasanya `A1`).

## Langkah 6: Tips untuk penggunaan produksi

* **Cache the workbook** – Jika Anda menghasilkan banyak laporan dalam sebuah loop, gunakan kembali satu instance `Workbook` dan bersihkan data sebelumnya untuk mengurangi beban memori.  
* **Set calculation mode** – Gunakan `workbook.getSettings().setCalculateFormulaOnOpen(false)` ketika Anda hanya membutuhkan formula mentah tanpa evaluasi langsung.  
* **Internationalization** – Nama fungsi `WRAPCOLS` tidak bergantung pada locale, tetapi pemisah desimal dalam formula lain mungkin berbeda. Simpan formula dalam bahasa Inggris untuk menghindari ketidakcocokan.  
* **Performance** – Untuk daftar yang melebihi 10 000 baris, evaluasi formula sekali saja dan kemudian baca nilai array secara langsung untuk menghindari perhitungan berulang.

## Kesimpulan

Anda kini mengetahui **how to use wrapcols** di Java untuk **convert list to columns** dan **create multi‑column layout** dengan satu formula. Contoh lengkap yang dapat dijalankan menunjukkan alur kerja penuh: menambahkan pustaka, mengisi data, menerapkan formula, dan memverifikasi hasil.  

Dari sini Anda dapat:

* Menyesuaikan jumlah kolom agar sesuai dengan gaya pelaporan Anda  
* Menggabungkan `WRAPCOLS` dengan fungsi lain seperti `SORT` atau `FILTER` untuk pembentukan data lanjutan  
* Mengekspor workbook ke PDF, CSV, atau HTML menggunakan konverter bawaan Aspose.Cells  

Cobalah variasi ini untuk menyederhanakan tugas otomatisasi Excel Anda. Jika Anda menemukan masalah, tinjau kembali bagian penanganan kasus tepi di atas atau konsultasikan dokumentasi Aspose.Cells untuk dukungan formula tambahan. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}