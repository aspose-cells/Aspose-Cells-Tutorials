---
category: general
date: 2026-06-21
description: Cara menggunakan WRAPCOLS dengan Aspose.Cells Java untuk mengonversi
  array menjadi baris, menulis rumus ke sel, dan mengisi sel dengan rumus – panduan
  langkah demi langkah.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: id
og_description: Cara menggunakan WRAPCOLS di Java dengan Aspose.Cells untuk mengubah
  array menjadi baris, menulis rumus ke sel, dan mengisi sel dengan rumus—semua dalam
  satu panduan.
og_title: Cara Menggunakan WRAPCOLS di Java – Contoh Lengkap WRAPCOLS di Excel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Cara Menggunakan WRAPCOLS di Java – Contoh Lengkap WRAPCOLS Excel
url: /id/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan WRAPCOLS di Java – Contoh Lengkap Excel WRAPCOLS

Pernah bertanya‑tanya **cara menggunakan WRAPCOLS** ketika Anda perlu mengubah array sederhana menjadi tabel rapi di Excel? Anda tidak sendirian. Banyak pengembang kebingungan saat pertama kali melihat fungsi `WRAPCOLS` dan berpikir, “Bagaimana cara menulis rumus ini ke sel dari Java?” Kabar baiknya? Itu cukup mudah setelah Anda mengetahui langkah‑langkah yang tepat.

Dalam tutorial ini kami akan membahas contoh lengkap Aspose.Cells Java yang **mengonversi array menjadi baris**, menulis rumus langsung ke sel, dan menunjukkan cara **mengisi sel dengan rumus** untuk skenario dunia nyata. Pada akhir tutorial Anda akan memiliki gambaran jelas tentang **contoh excel wrapcols** dan siap mengadaptasinya ke proyek Anda sendiri.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Java 17 atau lebih baru (kode ini bekerja dengan JDK terbaru mana pun).
- Perpustakaan Aspose.Cells untuk Java (Anda dapat mengunduh JAR terbaru dari Maven Central).
- Pemahaman dasar tentang sintaks Java dan rumus Excel.
- IDE atau editor teks sederhana—tidak memerlukan alat khusus.

Sudah siap? Baik, mari kita mulai.

## Langkah 1: Siapkan Proyek dan Muat Workbook

Langkah pertama—buat proyek Maven (atau Gradle) baru dan tambahkan dependensi Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Sekarang kita dapat memuat workbook yang sudah ada (atau membuat yang baru) dan mengambil worksheet pertama:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Mengapa kita memuat workbook** – Aspose.Cells bekerja dengan representasi dalam memori dari file Excel. Dengan memuat (atau membuat) workbook kita mendapatkan akses ke sel, baris, dan rumus, yang penting untuk operasi **menulis rumus ke sel**.

## Langkah 2: Sisipkan Rumus WRAPCOLS ke dalam Sel

Inti tutorial terletak pada fungsi `WRAPCOLS`. Fungsi ini mengambil array satu dimensi dan “membungkus”nya ke dalam jumlah kolom yang ditentukan, secara otomatis meneteskan sisa ke baris baru. Berikut sintaks yang akan kita gunakan:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Perhatikan bahwa rumus berupa string biasa yang diberikan ke `setFormula`. Aspose.Cells melakukan pekerjaan berat—menganalisis rumus, mengevaluasinya, dan meneteskan hasil ke worksheet. Ini adalah cara paling langsung untuk **mengisi sel dengan rumus** tanpa harus iterasi manual atas baris dan kolom.

### Apa yang Dilakukan Rumus Ini

- `{1,2,3}` – array literal yang berisi tiga angka.
- `2` – jumlah kolom per baris.
- Hasil:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (kosong)

Jika Anda menginginkan tiga kolom, cukup ubah argumen kedua menjadi `3`, dan array akan mengisi satu baris tunggal.

## Langkah 3: Simpan Workbook dan Verifikasi Output

Setelah rumus berada di **A1**, mari simpan workbook ke disk sehingga Anda dapat membukanya di Excel dan melihat hasilnya:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Buka `output.xlsx` dan Anda akan melihat persis seperti yang dijelaskan dalam komentar—dua kolom pada baris pertama dan nilai sisanya pada baris kedua. Itulah inti dari **contoh excel wrapcols**.

## Langkah 4: Memperluas Contoh – Mengonversi Array Lebih Besar

Proyek nyata jarang hanya bekerja dengan tiga angka. Misalnya Anda memiliki koleksi yang lebih besar, seperti `{10,20,30,40,50,60,70}` dan ingin tiga kolom per baris. Berikut cara menyesuaikan kode:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Sekarang penetesan dimulai pada **C5**, menghasilkan:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Ini menunjukkan bagaimana Anda dapat **mengonversi array menjadi baris** secara dinamis, hanya dengan mengubah string rumus. Tanpa loop, tanpa penugasan sel manual—Aspose.Cells menangani sisanya.

## Langkah 5: Menangani Kasus Tepi dan Gotchas Umum

### 1. Array Kosong

Jika literal array kosong (`{}`), `WRAPCOLS` mengembalikan error `#VALUE!`. Untuk menghindari kerusakan sheet, lindungi pembuatan rumus:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Data Non‑Numerik

`WRAPCOLS` juga bekerja dengan teks. Misalnya, `WRAPCOLS({"A","B","C","D"},2)` menghasilkan tata letak dua kolom berisi string. Ingat untuk menuliskan string dalam tanda kutip di dalam literal array.

### 3. Kompatibilitas

Fungsi `WRAPCOLS` tersedia di Excel 365 dan Excel 2019+ (Office 2019, Excel untuk web). Jika Anda harus mendukung versi yang lebih lama, Anda perlu kembali ke looping manual atau menggunakan fungsi spill‑compatible lain.

## Langkah 6: Tips Praktis dan Trik Pro

- **Tip pro:** Gunakan `Cell.setFormulaLocal` jika Anda memerlukan pemisah lokal (koma vs titik koma) tergantung pada pengaturan regional pengguna.
- **Waspadai:** Menimpa data yang sudah ada. Area spill akan menggantikan konten apa pun yang sudah ada di rentang target.
- **Catatan performa:** Menetapkan rumus tidak berat; beban kerja utama terjadi saat Anda **menyimpan** atau **menghitung ulang** workbook. Jika Anda menghasilkan ribuan rumus, pertimbangkan menonaktifkan perhitungan otomatis (`wb.calculateFormula()` nanti) untuk mempercepat proses.

## Contoh Lengkap yang Siap Dijalan

Berikut kelas Java lengkap yang siap dijalankan dan mencakup semua yang telah dibahas:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Output yang diharapkan:** Buka `output.xlsx` dan Anda akan melihat tiga wilayah spill terpisah:

- **A1:B2** – angka 1‑3 dibungkus menjadi dua kolom.
- **C5:E7** – angka 10‑70 dibungkus menjadi tiga kolom.
- **G1:H2** – nama buah dibungkus menjadi dua kolom.

## Kesimpulan

Kami baru saja membahas **cara menggunakan WRAPCOLS** dengan Aspose.Cells untuk Java, menunjukkan cara **mengonversi array menjadi baris**, **menulis rumus ke sel**, dan **mengisi sel dengan rumus** secara bersih dan dapat diulang. Pendekatan ini menghilangkan looping yang melelahkan, memanfaatkan perilaku spill native Excel, dan membuat kode Anda tetap ringkas.

Siap untuk tantangan berikutnya? Cobalah menggabungkan `WRAPCOLS` dengan sumber data dinamis—misalnya menarik nilai dari basis data, membangun string array secara langsung, dan membiarkan Excel mengatur tata letaknya. Anda juga dapat bereksperimen dengan fungsi spill lain seperti `SEQUENCE` atau `FILTER` untuk membuat laporan yang lebih kaya.

Jika Anda menemui kendala, tinggalkan komentar di bawah atau jelajahi dokumentasi lengkap Aspose. Selamat coding, dan nikmati kekuatan rumus Excel modern langsung dari Java!

![contoh cara menggunakan wrapcols](/images/wrapcols-demo.png "cara menggunakan wrapcols di Java – tangkapan layar data yang ditumpahkan")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Memilih Rentang Sel di Excel Menggunakan Aspose.Cells untuk Java (Panduan 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [Cara Menetapkan Sel Aktif di Excel Menggunakan Aspose.Cells untuk Java: Panduan Lengkap](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Cara Menyisipkan Baris ke dalam Workbook Excel Menggunakan Aspose.Cells untuk Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}