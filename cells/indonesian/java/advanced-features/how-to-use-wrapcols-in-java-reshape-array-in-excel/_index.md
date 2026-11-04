---
category: general
date: 2026-08-04
description: cara menggunakan wrapcols dengan contoh Java lengkap, mengubah bentuk
  array di Excel, dan menyimpan workbook ke file menggunakan Aspose.Cells
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: id
lastmod: 2026-08-04
og_description: cara menggunakan wrapcols untuk mengubah bentuk array di Excel dengan
  Java. Pelajari contoh lengkap wrapcols di Excel, buat workbook Excel dengan Java,
  dan simpan workbook ke file.
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: Cara menggunakan wrapcols di Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara menggunakan wrapcols di Java – mengubah bentuk array di Excel
url: /id/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menggunakan wrapcols di Java – mengubah bentuk array di Excel

Jika Anda perlu **how to use wrapcols** untuk mengubah daftar nilai datar menjadi rentang multi‑baris, panduan ini menunjukkan langkah‑langkah tepatnya. Anda akan melihat **excel wrapcols example** yang mengubah array 1‑D menjadi blok 3‑baris × 2‑kolom, dan Anda akan belajar cara **save workbook to file** dengan Aspose.Cells.

Pada akhir tutorial ini Anda akan dapat menulis kode **create excel workbook java** yang:

* Menginisialisasi workbook baru dan memilih sel A1.  
* Menerapkan fungsi `WRAPCOLS` untuk mengubah bentuk data.  
* Memaksa perhitungan formula sehingga hasil muncul secara instan.  
* Mengambil nilai dari array yang dihitung.  
* Menyimpan workbook ke disk.

Satu-satunya prasyarat adalah lingkungan pengembangan Java (JDK 8 atau yang lebih baru) dan pustaka Aspose.Cells untuk Java.

---

## Prasyarat

* JDK 8 + (atau versi lebih baru).  
* Maven atau Gradle untuk mengelola dependensi Aspose.Cells.  
* Pemahaman dasar tentang sintaks Java dan formula Excel.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Jika Anda menggunakan Gradle, ganti potongan XML dengan baris `implementation` yang sesuai.

---

## Langkah 1: Buat workbook Excel di Java

Operasi pertama adalah menulis kode **create excel workbook java** yang membuka workbook baru dan mengambil lembar kerja pertama serta sel A1.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

Membuat workbook dengan cara ini memberi Anda kanvas bersih, memastikan contoh ini dapat berjalan di mesin mana pun tanpa file yang sudah ada.

---

## Langkah 2: Terapkan fungsi WRAPCOLS – contoh excel wrapcols

`WRAPCOLS` mengambil array satu‑dimensi dan jumlah kolom, kemudian mengembalikan rentang yang mengisi baris terlebih dahulu. Ini adalah inti dari **reshape array in excel**.

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

Mengapa ini berhasil:

* Array literal `{1,2,3,4,5,6}` menyediakan enam angka.  
* `WRAPCOLS(..., 2)` memberi tahu Excel untuk membungkus nilai menjadi 2 kolom, secara otomatis menghasilkan cukup baris (dalam kasus ini 3) untuk menampung semua item.  
* Rentang yang dihasilkan menempati sel **A1:B3**:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## Langkah 3: Paksa perhitungan agar workbook mencerminkan formula

Aspose.Cells tidak mengevaluasi formula secara otomatis ketika Anda menetapkannya. Anda harus memanggil `calculateFormula()` untuk mewujudkan hasilnya.

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

Memanggil metode ini memastikan bahwa array yang dihasilkan oleh `WRAPCOLS` dituliskan ke sel, sehingga Anda dapat membaca nilai secara langsung.

---

## Langkah 4: Ambil nilai dari array yang telah diubah bentuk

Untuk membuktikan bahwa formula berhasil, baca representasi string dari sel target. Karena `WRAPCOLS` mengembalikan sebuah array, Excel menampilkan **elemen pertama** (nilai `1`) di sel tempat formula berada.

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**Output konsol yang diharapkan**

```
First element: 1
```

Jika Anda memeriksa lembar kerja di Excel, Anda akan melihat blok 3 × 2 penuh terisi seperti yang dijelaskan sebelumnya.

---

## Langkah 5: Simpan workbook ke file – cara menyimpan workbook ke file

Menyimpan workbook memungkinkan Anda membukanya nanti di Excel atau membagikannya dengan rekan kerja. Gunakan metode `save` dengan jalur lengkap.

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

Menjalankan program menghasilkan `WrapFunctions.xlsx` di direktori kerja. Membuka file tersebut memperlihatkan array yang telah diubah bentuk di sel A1:B3, mengonfirmasi bahwa **save workbook to file** berhasil.

---

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut adalah program lengkap yang dapat Anda salin‑tempel ke IDE dan jalankan:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**Verifikasi hasil**

1. Konsol mencetak `First element: 1`.  
2. File `WrapFunctions.xlsx` yang dihasilkan berisi:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

Jika Anda perlu merujuk ke array di tempat lain, Anda dapat membaca salah satu sel yang terisi menggunakan `worksheet.getCells().get("B2").getIntValue()`, misalnya.

---

## Pertanyaan umum dan kasus tepi

| Question | Answer |
|----------|--------|
| *Apakah WRAPCOLS dapat menangani array non‑numerik?* | Ya. Anda dapat memasukkan string, tanggal, atau nilai logika di dalam kurung kurawal, dan Excel akan membungkusnya sesuai. |
| *Bagaimana jika saya membutuhkan lebih banyak baris daripada yang dapat ditampilkan Excel?* | WRAPCOLS akan terus melanjutkan ke baris tambahan hingga array sumber habis. Pastikan lembar kerja memiliki cukup baris (batas default adalah 1.048.576). |
| *Bagaimana cara mengubah jumlah kolom?* | Ubah argumen kedua dari `WRAPCOLS`. Untuk tiga kolom, gunakan `=WRAPCOLS({1,2,3,4,5,6}, 3)`, yang menghasilkan blok 2 × 3. |
| *Apakah memungkinkan menulis hasil ke sel awal yang berbeda?* | Ya. Tetapkan formula pada sel mana pun (misalnya, `C5`) dan rentang yang dibungkus akan berkembang relatif terhadap sel tersebut. |
| *Apakah saya perlu memanggil `calculateFormula` setiap kali mengubah formula?* | Setiap kali Anda memodifikasi formula secara programatik, panggil `calculateFormula` atau `calculateFormula(true)` untuk menyegarkan sel yang bergantung. |

---

## Kesimpulan

Tutorial ini menunjukkan **how to use wrapcols** di Java untuk **reshape array in excel**, menyediakan **excel wrapcols example** yang jelas, dan memperlihatkan cara yang tepat untuk **save workbook to file**. Anda kini memiliki dasar yang kuat untuk proyek **create excel workbook java** yang memerlukan transformasi array dinamis.

Selanjutnya, jelajahi topik terkait seperti **using other array functions** (`TRANSPOSE`, `SEQUENCE`) atau **writing large data sets** dengan streaming API Aspose.Cells. Bereksperimenlah dengan berbagai array sumber, jumlah kolom, dan posisi mulai untuk menyesuaikan pola ini dengan alur kerja pelaporan atau pemrosesan data Anda sendiri. Selamat coding!

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuka File Excel Menggunakan Aspose.Cells untuk Java: Panduan Lengkap](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [Cara Membuat dan Menggabungkan Workbook Excel Menggunakan Aspose.Cells untuk Java | Panduan Lengkap](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [Cara Merender Lembar Excel menjadi Gambar Menggunakan Aspose.Cells untuk Java (Operasi Workbook)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}