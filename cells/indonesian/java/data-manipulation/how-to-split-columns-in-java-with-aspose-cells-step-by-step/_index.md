---
category: general
date: 2026-10-07
description: Cara memisahkan kolom menggunakan Aspose.Cells untuk Java. Pelajari cara
  memisahkan string menjadi kolom, mengotomatiskan formula Excel, dan menulis formula
  ke sel dalam beberapa baris kode.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: id
lastmod: 2026-10-07
og_description: Cara memisahkan kolom di Java dengan Aspose.Cells. Tutorial ini menunjukkan
  cara memisahkan string menjadi kolom, mengotomatiskan evaluasi rumus Excel, dan
  menulis rumus ke sel.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Cara memisahkan kolom di Java dengan Aspose.Cells – tutorial singkat
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara memisahkan kolom di Java dengan Aspose.Cells – panduan langkah demi langkah
url: /id/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memisahkan kolom di Java dengan Aspose.Cells – panduan langkah demi langkah

Jika Anda perlu **cara memisahkan kolom** dalam lembar kerja Excel secara programatis, panduan ini menunjukkan proses lengkap dengan Aspose.Cells untuk Java. Anda juga akan belajar cara **memisahkan string menjadi kolom**, **mengotomatiskan evaluasi formula Excel**, dan **menulis formula ke sel** menggunakan kode yang singkat dan siap produksi.

Pemecahan kolom secara programatis menghilangkan penyalinan‑tempel manual, mengurangi kesalahan, dan memungkinkan transformasi data skala besar. Pada akhir tutorial ini Anda dapat menghasilkan, memodifikasi, dan mengevaluasi formula secara langsung, menjadikan Excel bagian sejati dari backend Java Anda.

## Prasyarat

* Java 17 atau yang lebih baru terpasang.
* Maven 3.8+ (atau Gradle) untuk manajemen dependensi.
* Lisensi Aspose.Cells untuk Java (versi evaluasi gratis dapat digunakan untuk belajar).
* Familiaritas dasar dengan sintaks Java dan konsep Excel.

Jika ada item yang belum terpasang, instal terlebih dahulu; contoh kode mengasumsikan proyek Maven standar.

## Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Tambahkan dependensi berikut ke `pom.xml` Anda. Ini akan mengambil pustaka Aspose.Cells stabil terbaru.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Mengapa langkah ini penting:** Pustaka menyediakan kelas `Workbook`, `Worksheet`, dan `Cell` yang diperlukan untuk memanipulasi file Excel tanpa Microsoft Office. Tanpa dependensi ini kode tidak akan dapat dikompilasi.

## Langkah 2: Buat workbook dan pilih lembar kerja pertama

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

Objek `Workbook` mewakili seluruh file Excel. Mengakses lembar kerja pertama memastikan titik awal yang dapat diprediksi untuk formula yang akan kita tulis.

## Langkah 3: Tulis formula WRAPCOLS ke sel target

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Mengapa kami menggunakan `WRAPCOLS`:** Fungsi bawaan Excel `WRAPCOLS` secara otomatis memecah satu nilai teks menjadi sejumlah kolom yang ditentukan, menangani batas kata secara cerdas. Ini adalah cara paling andal untuk **memisahkan string menjadi kolom** tanpa logika parsing khusus.

## Langkah 4: Paksa workbook mengevaluasi formula

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Memanggil `calculateFormula()` **mengotomatiskan evaluasi formula Excel** di sisi server. Tanpa pemanggilan ini sel masih berisi teks formula, bukan nilai yang dihitung.

## Langkah 5: Ambil dan tampilkan hasil yang dibungkus

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Saat Anda menjalankan program, konsol akan mencetak:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

File `SplitColumnsResult.xlsx` yang dihasilkan menampilkan tiga kolom yang terisi dengan teks yang dipisahkan.

## Memahami fungsi WRAPCOLS

* **Sintaks:** `WRAPCOLS(text, columns, [delimiter])`
* **Parameter:**
  * `text` – string yang ingin Anda pisahkan.
  * `columns` – jumlah kolom untuk mendistribusikan teks.
  * `delimiter` (opsional) – karakter yang digunakan untuk memecah string; default adalah spasi.
* **Nilai kembali:** Sebuah array yang menyebar ke sel-sel berdekatan, setiap elemen berisi bagian dari teks asli.

Karena fungsi ini menyebar secara horizontal, Anda hanya perlu menulis formula di sel paling kiri (A1 dalam contoh). Excel secara otomatis mengisi B1, C1, … sesuai kebutuhan.

## Variasi umum dan kasus tepi

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Jumlah kolom variabel** | Ganti nilai `3` yang ditulis keras dengan variabel: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Delimiter khusus** | Gunakan argumen ketiga, misalnya `=WRAPCOLS(A2,4,",")` untuk memisahkan dengan koma. |
| **String sumber kosong** | Fungsi mengembalikan sel kosong; lindungi terhadap `null` atau string kosong sebelum menetapkan formula. |
| **Dataset besar** | Terapkan formula dalam loop untuk setiap baris, lalu panggil `calculateFormula()` sekali setelah loop untuk meningkatkan kinerja. |
| **Karakter non‑ASCII** | WRAPCOLS bekerja dengan Unicode; pastikan file sumber Java Anda disimpan sebagai UTF‑8. |

**Tips pro:** Saat memproses banyak baris, simpan formula dalam variabel string dan gunakan kembali untuk menghindari overhead penggabungan string berulang.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang siap disalin‑tempel. Program ini mencakup pernyataan import, penanganan pengecualian, dan operasi penyimpanan opsional.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Menjalankan program ini menghasilkan output konsol yang sama seperti sebelumnya dan menulis file Excel yang jelas menunjukkan **cara memisahkan kolom**.

## Daftar periksa pemecahan masalah

* **Formula tidak dievaluasi** – Pastikan `workbook.calculateFormula()` dipanggil setelah menetapkan formula.
* **Sel kosong setelah pemisahan** – Verifikasi bahwa string sumber tidak `null` atau kosong, dan bahwa jumlah kolom lebih besar dari nol.
* **Pengecualian lisensi** – Sediakan file lisensi Aspose.Cells yang valid (`License license = new License(); license.setLicense("Aspose.Total.lic");`) sebelum membuat workbook untuk menghapus watermark evaluasi.
* **Keterlambatan kinerja pada lembar besar** – Panggil `calculateFormula()` sekali setelah semua formula ditulis, bukan setelah setiap sel individu.

## Kesimpulan

Anda kini tahu **cara memisahkan kolom** di Java menggunakan Aspose.Cells, cara **memisahkan string menjadi kolom** dengan fungsi `WRAPCOLS`, cara **mengotomatiskan evaluasi formula Excel**, dan cara **menulis formula ke sel** secara programatis. Teknik ini menghilangkan langkah persiapan data manual dan mengintegrasikan kemampuan penanganan teks Excel yang kuat langsung ke dalam aplikasi Java Anda.

### Langkah selanjutnya

* Jelajahi fungsi teks lain seperti `TEXTSPLIT` dan `FILTERXML` untuk skenario parsing yang lebih kompleks.
* Gabungkan `WRAPCOLS` dengan `IFERROR` untuk menangani input tak terduga secara elegan.
* Integrasikan solusi ke dalam layanan Spring Boot yang menerima data CSV melalui REST dan mengembalikan file Excel yang terisi.

Dengan menguasai pola-pola ini Anda dapat membangun alur kerja Excel yang kuat dan otomatis yang dapat diskalakan sesuai kebutuhan bisnis Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [aspose cells java – Memisahkan Nama ke Kolom](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Kolom Excel di Java Menggunakan Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Cara Menghapus Kolom Kosong di Excel Menggunakan Aspose.Cells Java&#58; Panduan Komprehensif](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}