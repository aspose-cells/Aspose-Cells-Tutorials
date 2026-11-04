---
category: general
date: 2026-10-10
description: Pelajari cara menggunakan fungsi expand saat membaca dan menulis file
  Excel di Java. Panduan langkah demi langkah dengan kode lengkap dan penjelasan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use expand function
- read and write excel file java
- Java Excel formula
- Aspose.Cells expand
- Excel dynamic range Java
language: id
lastmod: 2026-10-10
og_description: Cara menggunakan fungsi expand saat membaca dan menulis file Excel
  di Java. Ikuti tutorial lengkap ini untuk menambahkan rentang dinamis dengan Aspose.Cells.
og_image_alt: Screenshot of Java code using the EXPAND function on an Excel worksheet
og_title: Cara menggunakan fungsi expand dalam pemrosesan Excel Java – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to use expand function while reading and writing Excel files
    in Java. Step‑by‑step guide with complete code and explanations.
  headline: How to use expand function in Java Excel processing
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Formula
title: Cara menggunakan fungsi expand dalam pemrosesan Excel Java
url: /id/java/range-management/how-to-use-expand-function-in-java-excel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Fungsi EXPAND dalam Pemrosesan Excel di Java

Jika Anda perlu **cara menggunakan fungsi expand** saat bekerja dengan file Excel di Java, panduan ini menunjukkan secara tepat caranya. Pada akhir tutorial Anda akan dapat membaca dan menulis proyek Java file Excel yang secara dinamis memperluas rentang sel dengan rumus `EXPAND`.

Bekerja dengan spreadsheet Excel sering berarti menangani rumus yang menyesuaikan diri dengan ukuran data yang berubah. Fungsi `EXPAND`, yang diperkenalkan pada versi Excel terbaru, memungkinkan Anda memperluas referensi dengan jumlah baris dan kolom tertentu. Dikombinasikan dengan pustaka Java yang kuat, Anda dapat mengotomatisasi perilaku ini tanpa meninggalkan basis kode Anda.

Dalam tutorial ini Anda akan:

* Memuat workbook yang sudah ada (skenario **read and write excel file java**)  
* Menerapkan rumus `EXPAND` ke sebuah sel  
* Menghitung ulang rumus sehingga nilai baru muncul  
* Menyimpan workbook yang telah diperbarui  

Prasyarat:

* Java 17 atau lebih baru terpasang  
* Maven atau Gradle untuk manajemen dependensi  
* Aspose.Cells untuk Java (pustaka yang menyediakan `Workbook`, `Worksheet`, dll.)  

> **Pro tip:** Aspose.Cells bekerja dengan format `.xlsx` dan `.xls` serta tidak memerlukan Microsoft Office di mesin host.

## Apa yang Anda Butuhkan

| Item | Alasan |
|------|--------|
| JDK 17+ | Fitur bahasa modern dan kinerja yang lebih baik |
| Maven/Gradle | Memudahkan penyertaan pustaka |
| Aspose.Cells untuk Java | Menyediakan `Workbook`, `Worksheet`, dan mesin rumus |
| Sebuah file Excel (`input.xlsx`) | Workbook sumber untuk mendemonstrasikan fungsi `EXPAND` |

Tambahkan Aspose.Cells ke proyek Anda dengan Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Atau dengan Gradle:

```groovy
implementation 'com.aspose:aspose-cells:23.12'
```

## Langkah 1: Muat workbook (cara menggunakan fungsi expand – inisialisasi)

Operasi pertama adalah membuka file Excel yang ingin Anda modifikasi. `Workbook` mewakili seluruh file dalam memori.

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**Mengapa ini penting:** Memuat workbook memberi Anda akses ke semua worksheet, sel, dan mesin rumus internal. Tanpa workbook yang dimuat Anda tidak dapat membaca atau menulis data **read and write excel file java**.

## Langkah 2: Akses worksheet target

Sebagian besar workbook berisi beberapa sheet; contoh ini menggunakan sheet pertama (indeks 0). Anda juga dapat mengambil sheet berdasarkan nama.

```java
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Penjelasan:** Objek `Worksheet` mengekspos koleksi `Cells`, tempat Anda menetapkan rumus. Jika Anda perlu menargetkan sheet lain, ganti indeks dengan nomor yang sesuai atau panggil `get("SheetName")`.

## Langkah 3: Tetapkan rumus EXPAND (cara menggunakan fungsi expand dalam praktik)

Sekarang kita menulis rumus `EXPAND` ke sel **B1**. Rumus ini memperluas referensi `A1` sebesar **5 baris** dan **1 kolom**, menghasilkan rentang `A1:A6` yang digeser satu kolom ke kanan.

```java
        // Apply the EXPAND formula to B1
        // =EXPAND(A1,5,1) expands A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");
```

**Mengapa ini berhasil:** `setFormula` menyimpan string rumus; Aspose.Cells tidak mengevaluasinya secara langsung. Fungsi `EXPAND` dievaluasi kemudian ketika kami memicu proses perhitungan.

## Langkah 4: Hitung ulang rumus (menyelesaikan fungsi expand)

Setelah menyisipkan rumus, minta workbook menghitung ulang semua sel yang bergantung. Langkah ini memastikan nilai baru muncul di worksheet.

```java
        // Recalculate all formulas so the EXPAND result is evaluated
        workbook.calculateFormula();
```

**Apa yang terjadi di balik layar:** Mesin perhitungan mem-parsing ekspresi `EXPAND`, menentukan rentang baru, dan menuliskan array nilai hasil kembali ke sheet. Jika `A1` berisi angka, rentang yang diperluas akan mengulang angka tersebut ke sel‑sel baru.

## Langkah 5: Simpan workbook yang telah diperbarui

Akhirnya, tulis workbook yang telah dimodifikasi kembali ke disk (atau ke output stream). Ini menyelesaikan siklus **read and write excel file java**.

```java
        // Save the workbook with the new formula evaluated
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Menjalankan program menghasilkan `output.xlsx` di mana sel **B1** kini berisi rentang spill yang meniru nilai `A1` selama lima baris dan satu kolom. Buka file tersebut di Excel untuk melihat array dinamis beraksi.

### Output yang Diharapkan

Dengan asumsi `A1` awalnya berisi angka `42`, sel‑sel hasil akan menjadi:

| B1 | B2 | B3 | B4 | B5 | B6 |
|----|----|----|----|----|----|
| 42 | 42 | 42 | 42 | 42 | 42 |

Jika `A1` berisi string teks, teks yang sama akan spill ke seluruh rentang yang diperluas.

## Variasi Umum dan Kasus Tepi

| Skenario | Penyesuaian |
|----------|------------|
| **Sel awal yang berbeda** | Ubah `"B1"` ke alamat apa pun, misalnya `"C3"` |
| **Perluas hanya kolom** | Gunakan `=EXPAND(A1,0,3)` untuk menambah tiga kolom |
| **Jumlah baris dinamis** | Ganti `5` statis dengan referensi sel seperti `D1` yang berisi jumlah baris yang diinginkan |
| **Menggunakan named range** | Ganti `A1` dengan nama yang didefinisikan, misalnya `=EXPAND(MyRange,5,1)` |
| **Kesalahan rumus** | Pastikan workbook disimpan dalam format yang mendukung array dinamis (`.xlsx`). File `.xls` lama akan memotong spill. |

### Menangani Spreadsheet Besar

Saat bekerja dengan workbook yang sangat besar, panggil `workbook.calculateFormula(CalcOptions)` dengan objek `CalcOptions` khusus untuk membatasi penggunaan memori atau mengaktifkan perhitungan multi‑thread.

```java
CalcOptions options = new CalcOptions();
options.setCalculateOnOpen(true); // Faster if you only need the result later
workbook.calculateFormula(options);
```

## Kode Sumber Lengkap (siap salin‑tempel)

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Set a formula that expands the range of A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");

        // Step 4: Recalculate all formulas so the new value is evaluated
        workbook.calculateFormula();

        // Step 5: Save the workbook with the updated data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **Catatan:** Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif ke file Excel Anda. Kode ini bekerja pada platform apa pun yang didukung Java (Windows, macOS, Linux).

## Kesimpulan

Anda kini mengetahui **cara menggunakan fungsi expand** dalam lingkungan Java untuk secara dinamis memperluas referensi sel, dan telah melihat alur kerja lengkap **read and write excel file java** menggunakan Aspose.Cells. Langkah‑langkah—memuat workbook, menerapkan rumus `EXPAND`, menghitung ulang, dan menyimpan—mencakup seluruh siklus otomatisasi Excel.

**Langkah selanjutnya** yang dapat Anda jelajahi:

* Menggabungkan `EXPAND` dengan fungsi array dinamis lain seperti `FILTER` atau `SORT`.  
* Menggunakan pola yang sama untuk **read and write excel file java** data dari basis data atau REST API.  
* Bereksperimen dengan pemformatan bersyarat berdasarkan rentang yang diperluas.  

Silakan sesuaikan contoh ini dengan proyek Anda sendiri, dan biarkan fungsi `EXPAND` menyederhanakan setiap skenario di mana ukuran data berubah seiring waktu.

--- 

*Selamat coding!*


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide](/cells/english/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}