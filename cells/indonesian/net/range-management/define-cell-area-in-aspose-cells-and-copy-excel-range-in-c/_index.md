---
category: general
date: 2026-08-04
description: Tentukan area sel di Aspose.Cells dan pelajari cara menyalin tabel pivot,
  menyalin rentang Excel menggunakan C#, serta menyalin rentang pada lembar yang sama
  secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: id
lastmod: 2026-08-04
og_description: Tentukan area sel di Aspose.Cells dan salin rentang Excel dalam C#
  sambil mempertahankan tabel pivot. Ikuti panduan langkah demi langkah ini untuk
  hasil yang dapat diandalkan.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Mendefinisikan area sel di Aspose.Cells – menyalin rentang Excel dalam C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Mendefinisikan area sel di Aspose.Cells dan menyalin rentang Excel di C#
url: /id/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mendefinisikan area sel di Aspose.Cells dan menyalin rentang Excel di C#

Jika Anda perlu **mendefinisikan area sel** untuk sebuah rentang dan kemudian menyalin rentang tersebut pada lembar kerja yang sama, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells untuk .NET. Baik Anda memindahkan laporan berbasis pivot atau menduplikasi blok data, Anda akan mempelajari proses lengkapnya dalam beberapa langkah saja.

Anda juga akan menemukan **cara menyalin pivot** tanpa kehilangan koneksinya, dan melihat contoh bersih dari **copy excel range c#** yang berfungsi pada skenario **copy range same sheet**. Tidak diperlukan alat eksternal—hanya Aspose.Cells dan beberapa baris kode C#.

## Apa yang Anda perlukan

- .NET 6.0 atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
- Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`)
- Sebuah workbook Excel (`input.xlsx`) yang berisi tabel pivot pada rentang A1:J50
- Lingkungan pengembangan seperti Visual Studio 2022

## Langkah 1: Mendefinisikan area sel untuk rentang sumber

Tugas pertama adalah **mendefinisikan area sel** yang mewakili blok yang ingin Anda salin. Aspose.Cells menggunakan struct `CellArea`, yang menyimpan indeks baris dan kolom berbasis nol.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Mengapa ini penting:** `CellArea` memberi tahu Aspose.Cells secara tepat sel mana yang akan diproses. Menggunakan indeks berbasis nol menghindari kesalahan off‑by‑one yang umum ketika menerjemahkan notasi A1 Excel ke kode.

## Langkah 2: Mendefinisikan area sel tujuan pada lembar kerja yang sama

Untuk **copy range same sheet**, Anda juga harus menentukan di mana data akan ditempatkan. Tujuan dapat dimulai pada baris mana saja; di sini kami memulai pada baris 61 (indeks berbasis nol 60) untuk memberikan ruang kosong.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Mengapa ini penting:** Dengan mencerminkan dimensi sumber, Anda menjamin bahwa blok yang disalin pas secara sempurna tanpa pemotongan.

## Langkah 3: Menyalin rentang sambil mempertahankan tabel pivot

Sekarang Anda dapat **how to copy pivot** dengan aman. Kelas `CopyOptions` mencakup flag `CopyPivotTables` yang mempertahankan definisi pivot, sumber data, dan pemformatannya.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Mengapa ini penting:** Tanpa mengatur `CopyPivotTables = true`, pivot akan menjadi snapshot statis, kehilangan interaktivitas. Opsi ini menyalin cache dan koneksi yang mendasarinya, sehingga pivot baru berperilaku persis seperti yang asli.

## Langkah 4: Menyimpan workbook

Akhirnya, tulis perubahan kembali ke disk. File output menunjukkan bahwa tabel pivot telah diduplikasi pada lembar yang sama.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Tips pro:** Gunakan `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` jika Anda perlu memaksa format tertentu, terutama saat bekerja dengan versi Excel yang lebih lama.

## Langkah 5: Memverifikasi tabel pivot yang disalin

Buka `CopyWithPivot.xlsx` di Excel dan periksa hal berikut:

1. Rentang A61:J110 berisi salinan data asli.
2. Tabel pivot baru muncul di bagian atas rentang yang disalin.
3. Memperbarui pivot mencerminkan perubahan pada data sumber, mengonfirmasi bahwa **how to copy pivot** berhasil.

Jika pivot tidak memperbarui, pastikan bahwa rentang data sumber dalam definisi pivot masih mengarah ke area workbook asli. Aspose.Cells secara otomatis memperbarui referensi sumber ketika `CopyPivotTables` bernilai true.

## Kasus khusus dan variasi

| Situasi | Apa yang harus diubah |
|-----------|----------------|
| **Menyalin ke lembar kerja yang berbeda** | Ganti `srcWorkbook.Worksheets[0]` dengan indeks atau nama lembar kerja target, dan sesuaikan `destinationRange` sesuai kebutuhan. |
| **Menyalin blok sel yang digabung** | Atur `CopyOptions.PasteType = PasteType.All` untuk mempertahankan sel yang digabung dan pemformatannya. |
| **Menyalin hanya nilai, bukan formula** | Gunakan `CopyOptions.PasteType = PasteType.Values` untuk menghindari transfer formula yang merujuk ke lembar kerja asli. |
| **Rentang besar ( > 10.000 baris )** | Pertimbangkan menggunakan `Workbook.Copy` untuk menyalin seluruh lembar kerja guna meningkatkan kinerja, kemudian hapus baris yang tidak diinginkan. |

Variasi ini menunjukkan bahwa logika **aspose.cells copy range** yang sama dapat disesuaikan untuk banyak skenario dunia nyata.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang siap dijalankan. Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Output yang diharapkan:** Setelah menjalankan program, `CopyWithPivot.xlsx` berisi data asli ditambah blok identik yang dimulai pada baris 61, lengkap dengan tabel pivot yang berfungsi.

## Kesimpulan

Anda kini tahu cara **mendefinisikan area sel** di Aspose.Cells, **copy excel range c#**, dan **copy range same sheet** sambil mempertahankan semua fungsi pivot. Teknik ini menghilangkan kesalahan salin‑tempel manual dan dapat diskalakan untuk workbook yang besar.

Selanjutnya, jelajahi topik terkait seperti **how to copy pivot** antar beberapa lembar kerja, atau gunakan **aspose.cells copy range** untuk menduplikasi seluruh lembar dengan pemformatan. Bereksperimenlah dengan berbagai pengaturan `CopyOptions` untuk menyesuaikan perilaku penyalinan sesuai kebutuhan proyek Anda.

Selamat mengoding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}