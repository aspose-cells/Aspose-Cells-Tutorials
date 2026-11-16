---
category: general
date: 2026-11-16
description: Pelajari cara menggunakan WRAPCOLS di C# untuk memisahkan baris menjadi
  kolom, mengotomatisasi buku kerja Excel, menghitung rumus, dan menyimpan file Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: id
lastmod: 2026-11-16
og_description: Cara menggunakan WRAPCOLS di C# untuk membagi baris menjadi kolom,
  mengotomatisasi workbook Excel, menjalankan perhitungan formula, dan menyimpan file
  Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Cara menggunakan WRAPCOLS di C# – memisahkan baris, menghitung rumus, dan
  menyimpan file Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Cara menggunakan WRAPCOLS untuk memisahkan baris menjadi kolom di C#
url: /id/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan WRAPCOLS untuk membagi baris menjadi kolom di C#

Jika Anda perlu **cara menggunakan WRAPCOLS** dalam proyek C#, panduan ini menunjukkan solusi lengkap yang dapat dijalankan. Anda akan melihat cara membagi baris menjadi kolom, mengotomatisasi workbook Excel, memicu perhitungan formula Excel, dan akhirnya menyimpan file Excel gaya C#.

Bekerja dengan Excel secara programatik sering berarti menangani kumpulan data besar, dan fungsi `WRAPCOLS` memungkinkan Anda mengubah satu baris menjadi matriks tanpa perulangan manual. Langkah‑langkah di bawah mencakup semua yang Anda perlukan—dari pembuatan workbook hingga output file akhir—sehingga Anda dapat mengintegrasikan teknik ini ke dalam aplikasi .NET apa pun.

## Apa yang dibahas dalam tutorial ini

* Membuat workbook baru dan mengakses worksheet pertama.  
* Mengisi baris dengan nilai berurutan (1‑20).  
* Menerapkan formula Excel `WRAPCOLS` untuk membagi baris menjadi blok 5‑kolom.  
* Menjalankan **excel formula calculation** sehingga hasil menjadi bagian dari sheet.  
* Menggunakan **save excel file c#** untuk menulis workbook ke disk.  

Tidak ada konfigurasi eksternal yang diperlukan selain pustaka Aspose.Cells untuk .NET (atau API kompatibel lain yang mendukung `WRAPCOLS`). Pada akhir panduan Anda akan memiliki file bernama `WrapColsDemo.xlsx` yang berisi empat baris dengan lima kolom masing‑masing, yang dihasilkan dari data satu‑baris asli.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core 3.1 dan .NET Framework 4.7+).  
* Referensi ke **Aspose.Cells** (tersedia via NuGet: `Install-Package Aspose.Cells`).  
* Familiaritas dasar dengan sintaks C# dan formula Excel.  

> **Pro tip:** Jika Anda menginginkan alternatif gratis, pustaka open‑source EPPlus juga mendukung formula kustom, tetapi `WRAPCOLS` hanya tersedia secara bawaan pada pustaka yang mengimplementasikan mesin perhitungan Excel penuh seperti Aspose.Cells.

## Langkah 1: Buat workbook baru dan dapatkan worksheet pertama

Operasi pertama adalah menginstansiasi objek `Workbook` dan mengambil worksheet defaultnya. Objek ini mewakili seluruh file Excel dalam memori.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Membuat workbook secara programatik adalah dasar dari tugas **automate excel workbook**. Referensi `Worksheet` memungkinkan Anda memanipulasi sel secara langsung.

## Langkah 2: Isi baris pertama dengan nilai 1‑20

Selanjutnya, isi sel `A1` hingga `T1` dengan angka 1 sampai 20. Loop `for` sederhana menulis setiap nilai ke indeks kolom yang sesuai.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Mengapa menulis nilai secara programatik? Ini menjamin demo berjalan di mesin mana pun tanpa entri data manual, yang penting saat Anda **automate excel workbook** dalam proses batch.

## Langkah 3: Terapkan fungsi WRAPCOLS untuk membagi baris menjadi blok 5‑kolom

Sekarang kita gunakan formula Excel `WRAPCOLS`. Formula ini mengambil rentang sumber dan jumlah kolom, lalu mengembalikan array dua dimensi yang “membungkus” data sumber ke dalam jumlah kolom yang ditentukan.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Menempatkan formula di sel `A2` memberi tahu Excel untuk memulai output pada baris kedua. Hasilnya akan menjadi matriks 4 × 5 karena 20 item dibagi 5 kolom menghasilkan empat baris.

### Cara kerja WRAPCOLS

* **Rentang sumber** – `A1:T1` berisi 20 nilai asli.  
* **Jumlah kolom** – `5` memberi tahu Excel membuat lima kolom per baris.  
* **Hasil** – Excel mengisi sel `A2:E5` dengan data yang telah dibungkus secara otomatis.

Jika Anda perlu **split row into columns** dengan ukuran blok berbeda, cukup ubah argumen kedua. Misalnya, `WRAPCOLS(A1:T1,4)` akan menghasilkan lima baris dengan empat kolom masing‑masing.

## Langkah 4: Hitung formula sehingga hasil WRAPCOLS menjadi material

Formula yang baru ditambahkan tetap tidak dievaluasi hingga mesin perhitungan dijalankan. Dengan memanggil `CalculateFormula()`, Anda memastikan langkah **excel formula calculation** menulis nilai sebenarnya ke worksheet.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Menjalankan perhitungan sangat penting ketika Anda kemudian **save excel file c#** karena file yang disimpan harus berisi nilai yang telah dihitung, bukan hanya teks formula. Tanpa langkah ini, workbook output akan menampilkan `#N/A` atau formula mentah alih‑alih angka yang diharapkan.

## Langkah 5: Simpan workbook ke disk

Akhirnya, persistenkan workbook menggunakan metode `Save`. Anda dapat menentukan jalur file yang valid; contoh ini menggunakan direktori placeholder yang harus Anda ganti dengan jalur Anda sendiri.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Pemanggilan `Save` memperlihatkan **save excel file c#** dalam bentuk paling sederhana. Aspose.Cells secara otomatis memilih format XLSX berdasarkan ekstensi file. Jika Anda memerlukan file `.xls` yang lebih lama, ubah ekstensi sesuai.

### Output yang diharapkan

Buka `WrapColsDemo.xlsx` dan Anda akan melihat:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

Baris tunggal asli telah **split row into columns** menjadi empat baris, masing‑masing berisi lima kolom.

## Kode sumber lengkap

Menggabungkan semua langkah menghasilkan program yang ringkas dan mandiri:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Salin kode ke proyek konsol baru, pulihkan paket NuGet Aspose.Cells, dan jalankan. Program akan membuat file Excel di desktop Anda dalam hitungan detik.

## Variasi umum dan kasus tepi

| Situation | Adjustment |
|-----------|------------|
| **Different block size** | Ubah `WRAPCOLS(A1:T1,5)` menjadi `WRAPCOLS(A1:T1, n)` dimana `n` adalah jumlah kolom yang diinginkan. |
| **Multiple source rows** | Gunakan `WRAPCOLS(A1:A10,5)` untuk membungkus rentang vertikal menjadi matriks 5‑kolom. |
| **Dynamic source range** | Bangun string alamat di C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) sebelum menetapkan formula. |
| **Large worksheets** | Panggil `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` untuk melewati sel yang menyebabkan error dan meningkatkan performa. |
| **Saving as CSV** | Ganti `workbook.Save(outputPath)` dengan `workbook.Save(outputPath, SaveFormat.Csv)`. |

Variasi‑variasi ini menunjukkan bahwa pola **how to use wrapcols** yang sama dapat disesuaikan untuk banyak skenario transformasi data.

## Tips pemecahan masalah

* **Formula tidak dievaluasi** – Pastikan Anda memanggil `workbook.CalculateFormula()` *setelah* menetapkan formula. Melewatkan langkah ini akan meninggalkan sel berisi teks `WRAPCOLS` mentah.  
* **Akses file ditolak** – Verifikasi bahwa direktori target ada dan proses Anda memiliki izin menulis. Menggunakan `Environment.SpecialFolder.Desktop` menghindari sebagian besar masalah izin.  
* **Jumlah baris tidak tepat** – Periksa kembali argumen kedua `WRAPCOLS`. Argumen ini menentukan jumlah kolom, bukan baris; baris dihitung dari total sel sumber dibagi jumlah kolom.

## Kesimpulan

Anda kini mengetahui **cara menggunakan WRAPCOLS** di C# untuk **split row into columns**, sepenuhnya **automate excel workbook**, menjalankan **excel formula calculation**, dan **save excel file c#** dengan basis kode yang bersih. Teknik ini menghilangkan operasi salin‑tempel manual dan dapat diskalakan dengan mudah untuk pipeline transformasi data besar.

### Langkah selanjutnya

* Jelajahi fungsi array dinamis lain seperti `SEQUENCE`, `FILTER`, dan `UNIQUE` untuk memperkaya toolkit otomatisasi Excel Anda.  
* Gabungkan `WRAPCOLS` dengan API pembuatan chart untuk menghasilkan laporan siap terbit.  
* Integrasikan kode ke dalam layanan latar belakang yang memproses unggahan CSV dan menghasilkan file Excel yang telah di‑reshape untuk analitik downstream.

Silakan bereksperimen dengan rentang sumber dan jumlah kolom yang berbeda—sesuaikan formula, jalankan kembali perhitungan, dan saksikan workbook terupdate secara instan. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}