---
category: general
date: 2026-10-26
description: Pelajari cara menggunakan WRAPCOLS di C# untuk membagi rentang menjadi
  kolom, terapkan WRAPROWS untuk baris, dan simpan buku kerja sebagai XLSX secara
  programatis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: id
lastmod: 2026-10-26
og_description: Cara menggunakan WRAPCOLS di C# untuk membagi data menjadi kolom,
  gunakan WRAPROWS untuk baris, dan menyimpan buku kerja sebagai XLSX. Ikuti panduan
  langkah demi langkah lengkap.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Cara menggunakan WRAPCOLS di C# – memisahkan rentang dan menyimpan sebagai
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara menggunakan WRAPCOLS dalam C# dan menyimpan workbook sebagai XLSX
url: /id/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan WRAPCOLS di C# dan Menyimpan Workbook sebagai XLSX

Jika Anda perlu **cara menggunakan WRAPCOLS** untuk mengatur ulang data dalam file Excel, panduan ini menunjukkan solusi lengkap yang dapat dijalankan. Anda akan melihat **contoh excel wrapcols**, belajar cara **memisahkan rentang menjadi baris** dengan WRAPROWS, dan menyelesaikannya dengan **menyimpan workbook sebagai XLSX**—semua dilakukan **secara programatis**.

Bekerja dengan Excel dari C# sering berarti membuat workbook, menerapkan rumus, dan menyimpan file. Kode di bawah ini menggunakan pustaka Aspose.Cells, yang memungkinkan Anda memanipulasi file Excel tanpa perlu menginstal Microsoft Office. Pada akhir tutorial ini Anda akan dapat **membuat excel workbook secara programatis**, memisahkan data baik secara horizontal maupun vertikal, dan menghasilkan file `.xlsx` bersih yang siap diproses lebih lanjut.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
* Referensi ke paket NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Familiaritas dasar dengan C# dan rumus Excel

## Langkah 1: Cara menggunakan WRAPCOLS untuk memisahkan rentang menjadi kolom

Fungsi **WRAPCOLS** mengambil rentang satu‑dimensi dan menyebarkan nilainya ke sejumlah kolom yang ditentukan. Pada contoh ini kami memulai dengan nilai di `A1:A10` dan meminta WRAPCOLS untuk membuat tiga kolom.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Hasil:** Sel `C1:E4` kini berisi sepuluh item asli yang diatur dalam tiga kolom (kolom terakhir menampung sisa item).

![Screenshot yang menggambarkan cara menggunakan WRAPCOLS untuk memisahkan rentang menjadi kolom di Excel](image-url.png)

## Langkah 2: Memisahkan rentang menjadi baris dengan WRAPROWS

Sementara **WRAPCOLS** bekerja secara horizontal, **WRAPROWS** melakukan hal sebaliknya: ia menyebarkan rentang ke sejumlah baris yang diberikan. Di sini kami mengambil nilai dari `B1:B10` dan mengaturnya menjadi dua baris mulai dari `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Hasil:** Rumus mengisi sel `F1:K2` dengan sepuluh nilai yang didistribusikan ke dua baris.

## Langkah 3: Menyimpan workbook sebagai XLSX

Setelah menerapkan rumus, langkah terakhir adalah menyimpan file. Operasi **save workbook as xlsx** menulis workbook yang berada di memori ke disk dalam format OpenXML modern.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Tampilan file yang disimpan

Saat Anda membuka `wrapcols_wraprows_output.xlsx` di Excel, Anda akan melihat:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

dan

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

Rumus tetap berada di sel, sehingga perubahan selanjutnya pada rentang sumber akan tercermin secara otomatis.

## Langkah 4: Variasi umum dan kasus tepi

### Mengubah jumlah kolom atau baris

* **Lebih banyak kolom:** Tingkatkan argumen kedua `WRAPCOLS`.  
  Contoh: `=WRAPCOLS(A1:A10,5)` membuat lima kolom, meninggalkan sel kosong bila data habis.
* **Jumlah kolom dinamis:** Gunakan referensi sel alih‑alih angka tetap.  
  `=WRAPCOLS(A1:A10, G1)` dimana `G1` berisi jumlah kolom yang diinginkan.

### Menangani sel kosong atau non‑numeric

WRAPCOLS dan WRAPROWS mengabaikan sel kosong secara default, tetapi mereka mempertahankan urutan nilai yang tidak kosong. Jika Anda perlu mempertahankan sel kosong, bungkus rentang sumber dengan fungsi `IFERROR` atau `TEXT` sebelum menerapkan WRAPCOLS.

### Menyimpan ke format lain

Meskipun tutorial ini berfokus pada **save workbook as xlsx**, Aspose.Cells mendukung banyak format (`.xls`, `.csv`, `.pdf`, dll.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Tips profesional dan jebakan

* **Tip pro:** Atur `Workbook.Settings.CalcEngineEnabled = true` jika Anda berencana mengevaluasi rumus segera setelah menyimpan.
* **Waspada:** Rentang sumber yang besar dapat menghasilkan area spill yang sangat besar, yang dapat memengaruhi kinerja. Batasi ukuran rentang atau bagi operasi menjadi beberapa lembar kerja.
* **Keamanan thread:** Objek Aspose.Cells **tidak** thread‑safe. Buat instance `Workbook` terpisah per thread jika Anda memproses file secara paralel.

## Kesimpulan

Anda kini tahu **cara menggunakan WRAPCOLS** untuk memisahkan rentang vertikal menjadi beberapa kolom, **cara memisahkan rentang menjadi baris** dengan WRAPROWS, dan **cara menyimpan workbook sebagai XLSX** setelah melakukan transformasi tersebut. Dengan mengikuti langkah‑langkah di atas Anda dapat **membuat excel workbook secara programatis**, menerapkan rumus spill yang kuat, dan menghasilkan file Excel siap dibagikan tanpa intervensi manual.

### Apa selanjutnya?

* Jelajahi **conditional formatting** untuk menyorot data yang di‑spill.
* Gabungkan **WRAPCOLS** dengan **SORT** atau **FILTER** untuk dasbor dinamis.
* Gunakan **charting API** Aspose.Cells untuk memvisualisasikan data yang telah diatur ulang langsung dari kode.

Selamat coding, dan nikmati otomatisasi alur kerja Excel Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang berhubungan erat dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}