---
category: general
date: 2026-05-23
description: Cara menggunakan WRAPCOLS di C# untuk mengubah array 1D menjadi matriks
  2D. Pelajari fungsi wrap columns, menulis formula ke sel, dan mengonversi 1D ke
  2D dengan mudah.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: id
og_description: Cara menggunakan WRAPCOLS di C# memungkinkan Anda mengubah array 1D
  menjadi matriks 2D dengan satu rumus. Ikuti panduan ini untuk menulis rumus ke sel
  dan menguasai fungsi wrap columns.
og_title: Cara Menggunakan WRAPCOLS di C# – Mengubah Array Menjadi Matriks
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Cara Menggunakan WRAPCOLS di C# – Mengubah Array Menjadi Matriks
url: /id/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan WRAPCOLS di C# – Mengubah Array Menjadi Matriks

Pernah bertanya-tanya **bagaimana cara menggunakan WRAPCOLS** ketika Anda perlu mengubah daftar angka datar menjadi tabel yang rapi? Anda tidak sendirian—banyak pengembang mengalami kebuntuan saat mencoba mengonversi daftar 1‑dimensi menjadi grid 2‑dimensi tanpa menulis banyak kode perulangan. Kabar baiknya? Fungsi WRAPCOLS (kadang disebut fungsi wrap columns) melakukan pekerjaan berat dalam satu baris, dan Anda dapat menyisipkannya langsung ke dalam workbook Excel dari C#.

Dalam tutorial ini kita akan melangkah melalui seluruh proses: mulai dari membuat workbook, ke **menulis formula ke sel**, ke **mengubah array menjadi matriks**, dan akhirnya ke **mengonversi 1d ke 2d** menggunakan formula WRAPCOLS. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali untuk array numerik apa pun, dan Anda akan memahami mengapa fungsi wrap columns sering menjadi alternatif yang lebih bersih dibandingkan reshaping array manual.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode ini juga bekerja pada .NET Framework 4.6+)
* Perpustakaan **Aspose.Cells for .NET** (versi percobaan gratis atau salinan berlisensi) – ini adalah komponen yang menyediakan objek `Workbook`, `Worksheet`, dan `Cell` yang digunakan di bawah.
* Pemahaman dasar tentang sintaks C#—tidak diperlukan pengetahuan Excel tingkat lanjut.

Sudah siap? Bagus—mari kita mulai.

![Matriks 2x3 yang dihasilkan setelah menggunakan fungsi WRAPCOLS di C# – cara menggunakan WRAPCOLS](https://example.com/images/wrapcols-result.png "Cara menggunakan WRAPCOLS – matriks 2x3 yang dihasilkan")

## Langkah 1: Siapkan Proyek dan Tambahkan Aspose.Cells

### Mengapa ini penting

Anda bisa mencoba menulis logika matriks sendiri, tetapi **fungsi wrap columns** sudah menangani kasus tepi seperti pembagian tidak merata dan input kosong. Menambahkan paket NuGet Aspose.Cells memberi kita API bersih untuk berinteraksi dengan formula Excel langsung dari C#.

```bash
dotnet add package Aspose.Cells
```

*Pro tip:* Jika Anda menggunakan Visual Studio, klik kanan proyek → **Manage NuGet Packages** → cari **Aspose.Cells** dan instal versi stabil terbaru.

## Langkah 2: Buat Workbook Baru (atau Muat yang Sudah Ada)

Sekarang perpustakaan sudah siap, kita dapat membuat objek workbook. Di sinilah langkah **menulis formula ke sel** akan terjadi.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

Di sini kami membuat workbook baru; Anda juga dapat memuat file yang sudah ada dengan `new Workbook("path/to/file.xlsx")` jika perlu menyisipkan matriks ke dalam templat yang sudah diformat.

## Langkah 3: Sisipkan Formula WRAPCOLS ke dalam Sel

### Inti dari “bagaimana cara menggunakan WRAPCOLS”

Fungsi **WRAPCOLS** menerima dua argumen: sebuah array (atau rentang) dan jumlah kolom yang Anda inginkan per baris. Dalam kasus kami kita akan mengubah array literal `{1,2,3,4,5,6}` menjadi **2 baris × 3 kolom**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

Perhatikan bagaimana formula ini mencerminkan apa yang Anda ketik di Excel sendiri. Dengan menempatkannya di `Cells[0,0]` (sel **A1**) kita **menulis formula ke sel** tanpa plumbing tambahan.

## Langkah 4: Paksa Perhitungan Agar Formula Dievaluasi

Aspose.Cells tidak mengevaluasi formula secara otomatis kecuali Anda memintanya. Langkah ini memastikan workbook benar‑benar berisi matriks yang telah di‑reshape.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

Jika Anda melewatkan baris ini, sel‑sel akan tetap menampilkan teks formula alih‑alih nilai yang dihitung.

## Langkah 5: Baca Kembali Hasil (Opsional, tapi Berguna untuk Verifikasi)

Anda mungkin ingin memastikan bahwa operasi **mengubah array menjadi matriks** berhasil. Berikut loop singkat yang mencetak grid 2‑by‑3 yang dihasilkan ke konsol.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### Output yang diharapkan

```
1   2   3
4   5   6
```

Konsol menampilkan tata letak persis yang sama seperti yang Anda lihat di Excel setelah formula WRAPCOLS dijalankan. Itulah transformasi **mengonversi 1d ke 2d** dalam aksi.

## Langkah 6: Menangani Kasus Tepi – Bagaimana Jika Panjang Array Tidak Merupakan Kelipatan Kolom?

Jika array sumber memiliki, misalnya, 7 elemen dan Anda meminta 3 kolom, WRAPCOLS akan membuat baris terakhir dengan elemen yang tersisa dan membiarkan sel‑sel lainnya kosong. Berikut penyesuaian cepat untuk mendemonstrasikannya:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

Hasil:

```
1   2   3
4   5   6
7       
```

**Fungsi wrap columns** dengan elegan menambahkan sel kosong pada baris akhir, sehingga Anda tidak perlu menulis kode tambahan untuk menangani ukuran yang tidak cocok.

## Langkah 7: Menggunakan WRAPCOLS dengan Data Dinamis

Dalam proyek nyata Anda hampir tidak akan menuliskan array secara hard‑code. Sebaliknya Anda akan membangun representasi string dari koleksi C#:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

Sekarang Anda telah **mengonversi 1d ke 2d** untuk panjang berapa pun, dan Anda tetap mendapatkan output matriks yang bersih. Formula dibangun pada runtime, tetapi **fungsi wrap columns** yang mendasarinya tetap sama.

## Kesalahan Umum dan Pro Tips

| Pitfall | Mengapa Terjadi | Solusi |
|---------|----------------|--------|
| Lupa memanggil `workbook.CalculateFormula()` | Aspose.Cells tidak mengevaluasi formula secara otomatis | Selalu panggil metode tersebut setelah menetapkan formula apa pun |
| Menggunakan literal array non‑numerik | WRAPCOLS mengharapkan angka atau string yang dapat dikonversi | Pastikan literal hanya berisi angka (atau string dalam tanda kutip) |
| Menimpa data yang sudah ada secara tidak sengaja | Menempatkan formula di sel yang sudah berisi data | Pilih sel baru (misalnya A1) atau bersihkan rentang terlebih dahulu |
| Tidak merujuk indeks worksheet yang tepat | `Worksheets[0]` adalah sheet pertama, tetapi Anda mungkin telah menambahkan sheet lain | Verifikasi `worksheet = workbook.Worksheets["SheetName"];` bila diperlukan |

## Mengapa WRAPCOLS Lebih Baik daripada Loop Manual

* **Readability** – Satu baris formula menggantikan puluhan loop `for`.  
* **Performance** – Mesin native Excel sangat dioptimalkan untuk formula array.  
* **Maintainability** – Pengembang di masa depan dapat langsung melihat maksudnya: “bungkus nilai‑nilai ini ke dalam kolom”.  
* **Portability** – Formula yang sama berfungsi jika Anda mengekspor workbook ke Google Sheets atau LibreOffice—tanpa logika khusus C#.

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)



## Tutorial Terkait

- [Cara Menggunakan Aspose.Cells untuk .NET untuk Menampilkan Rentang Sel sebagai Label Data pada Grafik](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [Cara Menggunakan Aspose.Cells untuk .NET untuk Mengelompokkan Baris dan Kolom di Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Cara Menggunakan Fungsi IF di Excel](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}