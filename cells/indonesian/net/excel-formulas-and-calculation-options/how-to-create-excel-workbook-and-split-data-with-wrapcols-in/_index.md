---
category: general
date: 2026-10-10
description: Buat buku kerja Excel dalam C# dan gunakan fungsi WRAPCOLS untuk membagi
  data array ke dalam kolom. Ikuti panduan langkah demi langkah yang lengkap dengan
  kode yang dapat dijalankan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: id
lastmod: 2026-10-10
og_description: Buat workbook Excel di C# dan terapkan fungsi WRAPCOLS untuk memisahkan
  data array ke dalam kolom. Panduan ini menampilkan kode lengkap dan menjelaskan
  setiap langkah.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Buat workbook Excel dan bagi data dengan WRAPCOLS di C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara membuat workbook Excel dan membagi data dengan WRAPCOLS di C#
url: /id/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat workbook Excel dan membagi data dengan WRAPCOLS di C#

Jika Anda perlu **membuat workbook Excel** secara programatis, panduan ini menunjukkan secara tepat cara melakukannya dan cara **membagi data array** ke beberapa kolom menggunakan fungsi `WRAPCOLS`. Anda akan mendapatkan contoh lengkap yang dapat dijalankan yang menghasilkan file `.xlsx` dengan data yang didistribusikan ke tiga kolom.

Tutorial ini mencakup semua yang Anda perlukan: paket NuGet yang diperlukan, setiap baris kode, mengapa rumus `WRAPCOLS` berfungsi, dan cara menyesuaikan solusi untuk ukuran array atau jumlah kolom yang berbeda. Pada akhir tutorial Anda akan dapat menyematkan teknik **use wrapcols function** dalam proyek C# apa pun yang menghasilkan file Excel.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru terpasang  
* IDE C# (Visual Studio, VS Code, Rider, dll.)  
* Paket NuGet **Aspose.Cells for .NET** – perpustakaan yang menyediakan kelas `Workbook` yang digunakan dalam contoh  

Anda tidak memerlukan instalasi Office; Aspose.Cells menulis file `.xlsx` secara langsung.

## Langkah 1 – membuat workbook Excel

Tugas pertama adalah menginstansiasi objek workbook baru dan mendapatkan referensi ke worksheet pertama. Langkah ini merupakan dasar untuk manipulasi selanjutnya.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` mewakili seluruh file, sementara `Worksheet` mewakili satu lembar. Dengan membuat workbook di memori, Anda menghindari I/O disk sampai Anda secara eksplisit menyimpannya.

## Langkah 2 – menerapkan WRAPCOLS untuk membagi kolom array

Sekarang Anda akan menempatkan rumus di sel **A1** yang menggunakan `WRAPCOLS`. Fungsi ini menerima dua argumen: array sumber dan jumlah kolom yang ingin Anda bungkus array ke dalamnya.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Mengapa ini bekerja:** `WRAPCOLS` mengambil array datar `{1,2,3,4,5,6}` dan mengisi worksheet baris‑per‑baris, membuat tiga kolom per baris. Argumen pertama dapat berupa literal array Excel apa pun, named range, atau rumus array dinamis. Argumen kedua (`3`) memberi tahu Excel berapa banyak kolom yang harus dihasilkan sebelum berpindah ke baris berikutnya.

### Menggunakan fungsi dengan tipe data berbeda

Fungsi `WRAPCOLS` tidak terbatas pada angka. Anda dapat membagi nilai teks, tanggal, atau tipe campuran:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Ketika array sumber berisi string, Excel secara otomatis memperlakukan hasilnya sebagai sel teks. Fleksibilitas ini memungkinkan Anda **excel formula split data** untuk pelaporan, dasbor, atau tugas migrasi data.

## Langkah 3 – menghitung rumus sehingga worksheet terisi

Rumus disimpan sebagai string sampai Anda meminta workbook untuk mengevaluasinya. Memanggil `CalculateFormula` memaksa evaluasi dan menulis hasil ke dalam sel.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Tanpa pemanggilan ini, file yang disimpan hanya akan berisi teks rumus, bukan nilai yang dihitung. Metode ini bekerja di seluruh workbook, sehingga Anda dapat menempatkan rumus tambahan di tempat lain dan semuanya akan diselesaikan dengan satu panggilan.

## Langkah 4 – menyimpan workbook untuk melihat hasil

Akhirnya, tulis workbook ke disk. Pilih folder yang Anda memiliki izin menulis, dan beri file nama yang jelas.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Saat Anda membuka `output.xlsx` di Excel (atau penampil kompatibel lainnya), Anda akan melihat:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Jika Anda menggunakan contoh tipe campuran, baris 3‑4 akan berisi teks dan angka sesuai.

## Variasi lanjutan dan penanganan kasus tepi

### Jumlah kolom variabel pada runtime

Seringkali jumlah kolom yang Anda butuhkan bergantung pada input pengguna. Anda dapat membangun string rumus secara dinamis:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Array besar dan kinerja

`WRAPCOLS` dapat menangani ribuan elemen, tetapi mengevaluasi array yang sangat besar dalam satu sel dapat meningkatkan waktu perhitungan. Jika Anda memperhatikan perlambatan:

* Bagi array sumber menjadi potongan yang lebih kecil dan tulis setiap potongan ke sel awal yang terpisah.  
* Gunakan `WorkbookSettings` untuk mengaktifkan perhitungan multi‑threaded:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Menangani sel kosong

Jika array sumber berisi string kosong (`""`) atau nilai `NULL`, `WRAPCOLS` menyisipkan sel kosong, mempertahankan tata letak kolom. Perilaku ini berguna ketika Anda memerlukan kolom placeholder untuk entri data selanjutnya.

### Menggunakan named range alih-alih literal

Untuk kemudahan pemeliharaan, definisikan named range yang menyimpan data sumber, lalu referensikan:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Sekarang rumus membaca data dari worksheet itu sendiri, memungkinkan **how to use wrapcols** dalam skenario pelaporan dinamis.

## Kesalahan umum dan tip profesional

* **Jangan menghilangkan argumen kedua.** `WRAPCOLS(array)` tanpa jumlah kolom mengembalikan satu kolom, yang menghilangkan tujuan membagi data.  
* **Hindari mencampur dimensi array.** Array sumber harus satu‑dimensi; memberikan array dua‑dimensi (misalnya `{ {1,2},{3,4} }`) memicu error `#VALUE!`.  
* **Simpan setelah perhitungan.** Jika Anda memanggil `wb.Save` sebelum `CalculateFormula`, file akan berisi hanya teks rumus.  
* **Periksa izin file.** Saat menjalankan di lingkungan terbatas (mis., ASP.NET), pastikan identitas proses dapat menulis ke folder target.  

## Contoh lengkap yang berfungsi

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan. Program ini mencakup semua impor, penanganan error, dan komentar.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Menjalankan program menghasilkan `output.xlsx` dengan tiga wilayah terpisah yang menunjukkan **excel formula split data** menggunakan fungsi `WRAPCOLS`.

## Kesimpulan

Anda kini tahu cara **membuat workbook Excel** dalam C# dan cara **use wrapcols function** untuk **membagi kolom array** secara efisien. Langkah utama—menginstansiasi `Workbook`, menyisipkan rumus `WRAPCOLS`, menghitung, dan menyimpan—membentuk pola yang dapat digunakan kembali untuk tugas otomasi apa pun yang memerlukan distribusi data ke kolom.

Dari sini Anda dapat:

* Menggabungkan `WRAPCOLS` dengan fungsi array dinamis lainnya seperti `FILTER` atau `SORT`.  
* Mengekspor set data besar dari basis data dan membiarkan Excel menangani tata letak secara otomatis.  
* Membuat laporan berbasis pengguna di mana jumlah kolom dipilih melalui kontrol UI.

Bereksperimenlah dengan sumber array yang berbeda, jumlah kolom, dan rumus tambahan untuk memperluas fondasi ini. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menggunakan WRAPCOLS di C# – Membuat Workbook Excel dengan Fungsi Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Membuat Workbook Excel – Mengonversi Array ke Matriks dengan WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Membuat Workbook Excel C# – Panduan Langkah‑per‑Langkah](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}