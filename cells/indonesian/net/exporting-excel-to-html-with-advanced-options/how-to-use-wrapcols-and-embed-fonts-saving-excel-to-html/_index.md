---
category: general
date: 2026-10-20
description: Pelajari cara menggunakan wrapcols di Aspose.Cells, menyematkan font
  dalam HTML, dan menyimpan Excel sebagai HTML dengan contoh lengkap C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: id
lastmod: 2026-10-20
og_description: Cara menggunakan wrapcols di Aspose.Cells, menyematkan font dalam
  HTML, dan mengonversi workbook ke HTML dengan panduan C# yang jelas untuk pengembang.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Cara menggunakan wrapcols dan menyematkan font saat mengekspor Excel ke
  HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Cara menggunakan wrapcols dan menyematkan font saat menyimpan Excel ke HTML
url: /id/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan wrapcols dan menyematkan font saat menyimpan Excel ke HTML

Jika Anda perlu **how to use wrapcols** dalam formula Aspose.Cells, panduan ini menunjukkan langkah‑langkah tepatnya. Anda juga akan belajar cara **embed fonts in HTML** dan **save Excel as HTML** sehingga outputnya terlihat identik di semua browser.  

Tutorial ini mencakup tiga skenario praktis: menggunakan fungsi `WRAPCOLS`, mengekspor workbook dengan font yang disematkan, dan menghasilkan laporan master‑detail dengan Smart Markers. Pada akhir tutorial, Anda akan memiliki satu program C# yang dapat dijalankan yang mendemonstrasikan semua fitur ini.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 (atau lebih baru) terpasang.
* Aspose.Cells untuk .NET ditambahkan ke proyek Anda (`dotnet add package Aspose.Cells`).
* Familiaritas dasar dengan C# dan formula Excel.

Tidak diperlukan pustaka pihak ketiga tambahan; Aspose.Cells menangani konversi HTML dan penyematan font secara internal.

## Langkah 1: Demonstrasikan fungsi **how to use wrapcols** dalam sebuah formula

Fungsi `WRAPCOLS` membagi rentang satu‑dimensi menjadi array dua‑dimensi, mengisi kolom terlebih dahulu. Ini berguna ketika Anda perlu mengubah bentuk data untuk pelaporan atau pembuatan grafik.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Mengapa ini berhasil:**  
`WRAPCOLS` mengambil dua argumen – rentang sumber dan jumlah kolom. Fungsi ini mengisi array secara kolom, mengabaikan nilai berlebih (angka `3` dalam contoh). Hasilnya muncul di sel kiri‑atas dari rentang target (`B1`), dan Anda dapat memperluas rentang secara manual jika memerlukan seluruh array.

> **Pro tip:** Setelah mengatur formula, panggil `workbook.CalculateFormula()` untuk memastikan hasilnya terbaru sebelum membaca nilai sel.

## Langkah 2: **Convert workbook to HTML** dan **embed fonts in html**

Saat Anda mengekspor file Excel ke HTML, font sering digantikan oleh font default browser, yang dapat merusak tata letak visual. Aspose.Cells memungkinkan Anda menyematkan font yang tepat digunakan dalam workbook langsung ke dalam file HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Mengapa penyematan font penting:**  
Ketika `EmbedFonts` bernilai `true`, Aspose.Cells mengonversi setiap font TrueType/OpenType yang digunakan menjadi aturan `@font-face` yang dienkode Base64 di dalam HTML yang dihasilkan. Ini menghilangkan kebutuhan mesin klien untuk memiliki font yang sama terpasang, menjamin rendering pixel‑perfect.

> **Edge case:** Jika workbook sumber merujuk pada font yang tidak terpasang di server, Aspose.Cells akan kembali ke font default dan mengeluarkan peringatan. Pastikan font yang diperlukan tersedia

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan WRAPCOLS di C# – Membuat Workbook Excel dengan Fungsi Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Cara Menyematkan Font di HTML – Mengonversi Excel ke HTML dengan C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Cara Mengonversi File Excel ke HTML Menggunakan Aspose.Cells untuk .NET: Menyembunyikan Konten yang Tertindih](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}