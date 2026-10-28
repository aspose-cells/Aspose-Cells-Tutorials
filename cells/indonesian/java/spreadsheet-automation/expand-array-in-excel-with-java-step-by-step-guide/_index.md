---
category: general
date: 2026-07-03
description: Pelajari cara memperluas array di Excel menggunakan Java. Tutorial ini
  mencakup memperluas array ke baris, cara menggunakan expand, dan cara menyisipkan
  formula secara efisien.
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: id
og_description: Perluas array di Excel dengan Java. Ikuti panduan ini untuk mempelajari
  cara menggunakan expand, menetapkan rumus di sel, dan memperluas array ke baris
  secara instan.
og_title: Perluas Array di Excel dengan Java – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Perluas Array di Excel dengan Java – Panduan Langkah demi Langkah
url: /id/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memperluas Array di Excel dengan Java – Panduan Pemrograman Lengkap

Pernah bertanya-tanya bagaimana **memperluas array di Excel** tanpa harus menyeret sel secara manual? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus menghasilkan rentang dinamis secara programatik—terutama ketika fungsi Excel `EXPAND` yang baru masih segar. Dalam panduan ini kami akan menunjukkan secara tepat **cara menggunakan EXPAND**, menyisipkan rumus ke dalam lembar kerja, dan membuat hasilnya menumpah ke baris yang Anda inginkan. Pada akhir tutorial Anda akan dapat **memperluas array ke baris** dalam satu baris kode Java.

Kami akan menelusuri contoh lengkap yang dapat dijalankan menggunakan pustaka Aspose.Cells for Java. Tanpa referensi yang samar, hanya kode konkret yang dapat Anda salin‑tempel, kompilasi, dan jalankan. Sepanjang jalan kami akan membahas mengapa setiap langkah penting, menyinggung kasus tepi seperti array tidak berurutan, dan menambahkan beberapa tip profesional yang tidak ada di dokumentasi resmi. Siap? Mari kita mulai.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* Java 17 (atau JDK terbaru apa pun) terpasang.
* Maven atau Gradle untuk mengelola dependensi.
* Lisensi Aspose.Cells for Java yang valid (versi percobaan gratis cukup untuk pengujian).
* Familiaritas dasar dengan rumus Excel—jika Anda pernah menggunakan `VLOOKUP` atau `SUMIF` sebelumnya, Anda sudah siap.

Jika ada yang belum Anda kenal, jeda sejenak dan siapkan dulu; sisa tutorial mengasumsikan semuanya sudah siap.

## Langkah 1: Siapkan Proyek Maven Anda dan Tambahkan Aspose.Cells

Agar tetap teratur, buat proyek Maven baru bernama `ExpandArrayDemo`. Tambahkan dependensi Aspose.Cells ke dalam `pom.xml` Anda:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **Tip pro:** Jika Anda menggunakan Gradle, dependensi yang sama terlihat seperti `implementation 'com.aspose:aspose-cells:23.12'`.

Setelah Maven selesai mengunduh, Anda siap menulis kode Java yang **menetapkan rumus di sel**.

## Langkah 2: Buat Workbook dan Akses Worksheet Pertama

Potongan kode pertama mencerminkan snippet yang sudah Anda lihat, tetapi kami akan menambahkan beberapa pemeriksaan keamanan dan komentar agar Anda memahami *mengapa* di balik setiap baris.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*Mengapa ini penting:* Menginstansiasi `Workbook` mengalokasikan struktur internal yang dibutuhkan Aspose untuk mengelola sel, rumus, dan gaya. Mengakses worksheet pertama adalah titik masuk paling umum, terutama saat Anda masih bereksperimen.

## Langkah 3: Sisipkan Rumus EXPAND – “Cara Menyisipkan Rumus”

Sekarang masuk ke inti tutorial: **cara menyisipkan rumus** yang memperluas array. Fungsi Excel `EXPAND` menerima tiga argumen—array sumber, jumlah baris yang dibutuhkan, dan jumlah kolom yang dibutuhkan. Dalam kasus kami kami ingin memperluas `{1,2,3}` menjadi **5 baris** dan **1 kolom**.

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

Perhatikan kami menggunakan `putFormula` alih‑alih `putValue`. Ini memberi tahu Aspose untuk memperlakukan string sebagai rumus Excel yang sebenarnya, bukan entri teks biasa. Metode `putFormula` secara otomatis mengurai string dan menyimpan pohon rumus secara internal.

### Mengapa Menggunakan EXPAND?

`EXPAND` menghilangkan langkah melelahkan menyeret pegangan isian. Ia juga bekerja dengan array dinamis, artinya jika array sumber berubah, rentang yang menumpah akan otomatis diperbarui. Ini sangat berguna saat menghasilkan laporan secara programatik.

## Langkah 4: Paksa Perhitungan – Materialisasi Hasil

Ketika Anda *menetapkan rumus di sel* melalui API, workbook tidak secara otomatis menghitung ulang. Anda perlu memicu satu siklus perhitungan agar array **diperluas ke baris** dan nilai‑nilainya muncul di lembar.

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

Jika Anda melewatkan langkah ini, membuka file `.xlsx` yang dihasilkan di Excel akan menampilkan rumus tetapi tidak nilai yang menumpah sampai Anda menekan **F9**. Dengan memanggil `calculate()`, Anda memastikan workbook siap pakai langsung.

## Langkah 5: Simpan Workbook dan Verifikasi Output

Akhirnya, tulis workbook ke file dan secara opsional cetak nilai‑nilai yang menumpah ke konsol untuk verifikasi.

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Saat Anda menjalankan program, konsol akan menampilkan:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel mengisi baris‑baris sisanya dengan nol karena array sumber hanya memiliki tiga elemen. Ini adalah perilaku default `EXPAND`. Jika Anda lebih suka sel kosong alih‑alih nol, Anda dapat membungkus array dengan `IFERROR` atau menggunakan trik `CHOOSE`—lebih lanjut pada bagian “Variasi Lanjutan” di bawah.

## Variasi Lanjutan & Kasus Tepi

### 1. Memperluas Array Horizontal ke Beberapa Kolom

Jika Anda perlu **memperluas array ke baris** *dan* kolom, cukup ubah argumen ketiga:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

Sekarang rentang menumpah menjadi blok 5 × 3, mengisi sel‑sel yang kosong dengan nol.

### 2. Menggunakan Named Range sebagai Sumber

Alih‑alih literal `{1,2,3}`, Anda dapat merujuk ke named range yang mungkin berubah pada waktu runtime:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

Pastikan `MySourceRange` ada (Anda dapat membuatnya via `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")`).

### 3. Menangani Data Non‑Numerik

`EXPAND` juga bekerja dengan teks. Contohnya:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

Baris tambahan akan muncul sebagai string kosong, bukan nol.

### 4. Menghindari Pengisian Nol dengan `IFERROR`

Jika Anda lebih suka melihat sel kosong alih‑alih nol, bungkus `EXPAND` dengan `IFERROR`:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

Sekarang baris 4 dan 5 akan benar‑benar kosong.

## Kesalahan Umum dan Cara Menghindarinya

| Kesalahan | Mengapa Terjadi | Solusi |
|-----------|----------------|--------|
| **Rumus tidak dihitung ulang** | Lupa memanggil `ws.getCells().calculate()` | Selalu panggil `calculate()` setelah `putFormula`. |
| **Nilai nol di tempat yang seharusnya kosong** | `EXPAND` menambahkan nol secara default | Gunakan `IFERROR(..., "")` atau bungkus dengan `CHOOSE`. |
| **Alamat sel tidak tepat** | Menggunakan `"A0"` atau `"1A"` | Alamat Excel dimulai dari 1; Aspose mengharapkan gaya `"A1"`. |
| **Versi pustaka tidak cocok** | Menggunakan versi Aspose.Cells lama yang belum mendukung `EXPAND` | Tingkatkan ke versi terbaru (23.12 pada saat penulisan). |

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabung)

Berikut adalah program lengkap yang siap disalin‑tempel. Simpan sebagai `ExpandArrayDemo.java`, kompilasi, dan jalankan.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Menjalankan program ini menghasilkan file Excel di mana **sel A1** kini berisi rumus `EXPAND`, dan baris 1‑5 kolom A menampilkan `1, 2, 3, 0, 0`. Buka file tersebut di Excel untuk melihat hasil yang sama secara instan—tanpa harus menyeret secara manual.

## Kesimpulan

Anda baru saja mempelajari cara **memperluas array di Excel** menggunakan Java, **cara menggunakan EXPAND**, serta langkah‑langkah tepat untuk **menetapkan rumus di sel** dan **memperluas array ke baris** secara programatik. Dengan memanfaatkan Aspose.Cells, Anda menghindari trik UI yang canggung dan membiarkan kode melakukan pekerjaan berat. Baik Anda membangun mesin pelaporan, alat entri data otomatis, atau generator spreadsheet khusus, teknik ini akan menghemat waktu berjam‑jam.

Apa selanjutnya? Cobalah mengganti array statis dengan rentang dinamis yang diambil dari sheet lain, bereksperimen dengan spill multi‑kolom, atau menggabungkan `EXPAND` dengan `FILTER` untuk transformasi data yang kuat. Langit adalah batasnya, dan kini Anda memiliki fondasi yang solid untuk membangunnya.

Punya pertanyaan atau ingin berbagi kasus penggunaan keren? Tinggalkan komentar di bawah.


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}