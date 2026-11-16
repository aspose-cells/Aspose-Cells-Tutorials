---
category: general
date: 2026-11-16
description: Pelajari cara memperluas array di Excel menggunakan Aspose.Cells, fungsi
  array dinamis, dan reducer lambda, kemudian menulis file Excel dari C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: id
lastmod: 2026-11-16
og_description: Cara memperluas array di Excel menggunakan Aspose.Cells, fungsi array
  dinamis, dan reducer lambda. Ikuti contoh lengkap C# untuk menulis file Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Cara memperluas array di Excel dengan Aspose.Cells – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara memperluas array di Excel dengan Aspose.Cells
url: /id/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memperluas array di Excel dengan Aspose.Cells

Jika Anda perlu **cara memperluas array** dalam lembar kerja Excel dari C#, tutorial ini menunjukkan langkah‑langkah tepatnya. Anda akan membuat workbook Excel, menggunakan fungsi array dinamis seperti `EXPAND` dan `REDUCE`, menerapkan akumulator **lambda**, dan akhirnya **menulis file Excel** ke disk. Pendekatan ini bekerja dengan Aspose.Cells 23.10 atau lebih baru dan tidak memerlukan instalasi Excel manual.

Pada akhir panduan ini Anda akan memiliki file `ExpandReduceDemo.xlsx` yang berfungsi penuh yang menunjukkan kekuatan formula array dinamis dalam konteks pemrograman.

## Apa yang Anda perlukan

- .NET 6.0 (atau versi .NET apa pun yang didukung oleh Aspose.Cells)
- Paket Aspose.Cells untuk .NET (`dotnet add package Aspose.Cells`)
- Editor kode atau IDE (Visual Studio, VS Code, Rider, dll.)

Tidak diperlukan interop COM tambahan atau instalasi Office karena Aspose.Cells menangani format file secara internal.

## Langkah 1: Membuat workbook Excel

Tugas pertama adalah **membuat workbook excel** di memori. Aspose.Cells menyediakan kelas `Workbook`, yang mewakili seluruh file XLSX.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Mengapa ini penting:** Membuat instance `Workbook` memberi Anda kanvas yang bersih. Lembar kerja default sudah disiapkan, jadi Anda tidak perlu menambahkannya secara manual kecuali Anda menginginkan beberapa lembar.

## Langkah 2: Menyisipkan konstanta array vertikal

Mesin array dinamis Excel dapat bekerja dengan konstanta array literal. Kami akan menempatkan array vertikal `{1;2;3;4;5}` ke sel **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tip:** Tanda titik koma (`;`) memisahkan baris dalam konstanta, sedangkan koma (`,`) akan memisahkan kolom. Ini mencerminkan sintaks Excel sendiri.

## Langkah 3: Memperluas array menjadi matriks

Sekarang kami menjawab pertanyaan inti – **cara memperluas array** – menggunakan fungsi `EXPAND`. Rumus tersebut memperluas array satu‑kolom menjadi matriks 5‑baris × 2‑kolom, dimulai dari **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Mengapa EXPAND?** `EXPAND(source, rows, cols)` memaksa rentang sumber menempati ukuran yang ditentukan, menambahkan ruang kosong jika diperlukan. Ini adalah cara paling mudah dibaca untuk menghasilkan matriks yang lebih besar dari satu array.

## Langkah 4: Mengurangi matriks dengan akumulator lambda

Fungsi `REDUCE` mengiterasi rentang dan mengagregasi nilai menggunakan ekspresi **lambda**. Di sini kami menjumlahkan setiap nilai kolom ke dalam satu kolom, menempatkan hasilnya di **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Cara menggunakan lambda:** `LAMBDA(acc, val, acc+val)` menerima akumulator saat ini (`acc`) dan nilai sel berikutnya (`val`). Ia mengembalikan akumulator baru, secara efektif melakukan total berjalan. Ini menunjukkan **cara menggunakan lambda** dalam rumus Excel dari kode.

## Langkah 5: Menghitung rumus agar hasil muncul

Aspose.Cells tidak secara otomatis mengevaluasi rumus ketika Anda menetapkannya. Memanggil `CalculateFormula` memaksa mesin menghitung setiap rumus dalam workbook.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Catatan:** Jika Anda membuka file yang dihasilkan di Excel, nilai-nilai sudah terlihat karena telah dihitung sebelumnya.

## Langkah 6: Menulis file Excel ke disk

Akhirnya, **menulis file excel** menggunakan metode `Save`. Pilih folder yang Anda miliki izin menulis.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Hasil yang diharapkan

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Kolom B** dan **C** berisi matriks 5 × 2 yang dihasilkan oleh `EXPAND`.
- **Sel D1** menampilkan `15`, jumlah semua angka, dihitung oleh rumus `REDUCE` + **lambda**.

## Pertanyaan umum dan kasus tepi

- **Apakah saya dapat memperluas ke lebih banyak kolom daripada yang disediakan sumber?**  
  Ya. `EXPAND` menambahkan kolom yang hilang dengan sel kosong. Hal yang sama berlaku untuk baris.

- **Bagaimana jika array sumber horizontal (`{1,2,3,4,5}`)?**  
  `EXPAND` akan memperlakukan sumber sebagai satu baris; Anda masih dapat menentukan baris dan kolom untuk mengubah bentuknya.

- **Apakah `REDUCE` bekerja dengan data non‑numerik?**  
  Lambda harus mengembalikan nilai yang kompatibel dengan tipe akumulator. Untuk penggabungan teks Anda dapat menggunakan `LAMBDA(acc, val, acc & val)`.

- **Apakah saya perlu memanggil `CalculateFormula` untuk setiap perubahan?**  
  Hanya ketika Anda membutuhkan nilai yang dihitung sebelum menyimpan. Excel akan menghitung ulang saat dibuka jika Anda melewatkannya.

## Tips profesional

- **Kinerja:** Untuk workbook besar, panggil `workbook.CalculateFormula` sekali setelah semua rumus diatur, bukan setelah setiap sel.
- **Keamanan versi:** `EXPAND` dan `REDUCE` tersedia di Excel 365 dan versi lebih baru. Aspose.Cells mengimplementasikannya terlepas dari versi Excel target karena mesin perhitungan sudah terintegrasi.
- **Debugging rumus:** Gunakan `sheet.Cells["B1"].Formula` untuk membaca kembali string persis yang Anda tetapkan; ini membantu saat Anda membangun rumus secara dinamis.

## Kesimpulan

Anda sekarang tahu **cara memperluas array** di Excel menggunakan Aspose.Cells, memanfaatkan **fungsi array dinamis**, menerapkan **lambda** dengan `REDUCE`, dan **menulis file excel** dari C#. Contoh end‑to‑end ini dapat disesuaikan untuk transformasi data yang lebih kompleks, seperti transposisi matriks, total kumulatif, atau agregasi khusus.

---

*Langkah selanjutnya:*  
- Jelajahi fungsi dinamis lainnya seperti `FILTER`, `SORT`, dan `UNIQUE`.  
- Gabungkan beberapa ekspresi `LAMBDA` untuk membangun fungsi buatan pengguna yang dapat digunakan kembali.  
- Integrasikan pembuatan workbook ke dalam API ASP.NET Core untuk pembuatan laporan secara langsung.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}