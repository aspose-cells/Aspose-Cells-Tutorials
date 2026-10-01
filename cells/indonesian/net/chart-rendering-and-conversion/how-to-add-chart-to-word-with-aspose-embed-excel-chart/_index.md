---
category: general
date: 2026-10-01
description: Tambahkan diagram ke Word dengan Aspose dalam hitungan menit. Pelajari
  cara menyematkan diagram Excel ke Word, mengekspor diagram Excel ke Word, membuat
  dokumen Word dengan Aspose, dan menyimpan diagram di dokumen Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: id
lastmod: 2026-10-01
og_description: Tambahkan diagram ke Word dengan Aspose dalam hitungan menit. Panduan
  ini menunjukkan cara menyematkan diagram Excel ke Word, mengekspor diagram Excel
  ke Word, membuat dokumen Word dengan Aspose, dan menyimpan diagram dalam dokumen
  Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Tambahkan grafik ke Word dengan Aspose – sematkan grafik Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Cara menambahkan grafik ke Word dengan Aspose – menyematkan grafik Excel
url: /id/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan diagram ke Word dengan Aspose – menyematkan diagram Excel

Jika Anda perlu **menambahkan diagram ke Word** dengan cepat, tutorial ini memberikan solusi lengkap yang siap dijalankan. Anda akan melihat cara menyematkan diagram Excel ke dalam file Word, mengekspor diagram dari Excel ke Word, dan akhirnya **menyimpan dokumen Word berisi diagram** dengan hanya beberapa baris kode C#.

Menyematkan diagram adalah kebutuhan umum ketika Anda menghasilkan laporan, faktur, atau dasbor secara programatis. Pada akhir panduan ini Anda akan dapat **membuat dokumen Word Aspose** yang berisi diagram apa pun dari workbook Excel, tanpa menyalin‑tempel secara manual.

## Prasyarat

- .NET 6.0 atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
- Paket NuGet Aspose.Cells dan Aspose.Words (pasang via `dotnet add package Aspose.Cells` dan `dotnet add package Aspose.Words`)
- File Excel yang sudah ada (`Chart.xlsx`) yang berisi setidaknya satu diagram
- Lingkungan pengembangan seperti Visual Studio 2022 atau VS Code

## Menambahkan diagram ke Word dengan Aspose

Berikut adalah program lengkap yang berdiri sendiri. Salin ke dalam proyek konsol baru, pulihkan paket-paketnya, dan jalankan. Program ini memuat workbook Excel, membuat dokumen Word, menyisipkan diagram pertama, dan menyimpan hasilnya.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Mengapa setiap baris penting

1. **Memuat workbook** – `Workbook` mengurai file Excel dan memberi Anda akses programatik ke lembar kerja dan diagramnya.  
2. **Membuat dokumen Word** – `Document` adalah titik masuk Aspose.Words untuk setiap tugas pengolahan Word.  
3. **DocumentBuilder** – Kelas pembantu ini memungkinkan Anda menyisipkan konten (teks, gambar, diagram) pada posisi kursor saat ini.  
4. **InsertChart** – Overload yang menerima objek `Aspose.Cells.Chart` menyalin data, format, dan seri diagram langsung ke dalam file Word. Tidak diperlukan konversi gambar perantara, sehingga kualitas vektor tetap terjaga.  
5. **Save** – `Save` menulis paket .docx ke disk, menyelesaikan langkah **menyimpan dokumen Word berisi diagram**.

#### Output yang diharapkan

Setelah menjalankan program, buka `Chart.docx`. Anda akan melihat diagram persis yang disimpan di `Chart.xlsx`, ditempatkan di mana builder berada (awal dokumen). Diagram tetap dapat diedit sepenuhnya di dalam Word (Anda dapat mengubah ukuran, mengubah warna, atau memodifikasi sumber data).

## Menyematkan diagram Excel ke Word

Jika Anda perlu menyematkan lebih dari satu diagram, ulangi pemanggilan `InsertChart` untuk setiap objek diagram. Misalnya, untuk menyematkan semua diagram dari lembar kerja pertama:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Pro tip:** Gunakan `builder.Writeln()` untuk menyisipkan jeda paragraf, memastikan setiap diagram dimulai pada baris baru.

## Mengekspor diagram Excel ke Word – menangani banyak lembar kerja

Ketika diagram tersebar di beberapa lembar kerja, iterasi melalui koleksi `Worksheets` pada workbook:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Pendekatan ini **export chart Excel Word** untuk setiap tata letak workbook, membuat solusi menjadi kuat untuk laporan kompleks.

## Membuat dokumen Word Aspose – menyesuaikan tampilan

Anda dapat mengontrol ukuran dan posisi setiap diagram yang disisipkan dengan memodifikasi `Shape` yang dikembalikan oleh `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Mengatur `WrapType` ke `Inline` memastikan diagram berperilaku seperti paragraf biasa, yang sering diinginkan untuk pembuatan dokumen otomatis.

## Menyimpan dokumen Word berisi diagram – praktik terbaik

- **Gunakan nama file yang deskriptif** (`Report_Q1_2026.docx`) untuk memudahkan versioning.
- **Dispose objek** setelah selesai, terutama dalam proses batch besar:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Validasi hasil** secara programatik jika Anda menghasilkan banyak file:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Pertanyaan umum & kasus tepi

| Question | Answer |
|----------|--------|
| *Apakah saya dapat menyisipkan diagram yang bukan yang pertama pada lembar?* | Ya. Akses dengan indeks: `sheet.Charts[2]` untuk diagram ketiga. |
| *Bagaimana jika diagram Excel menggunakan sumber data yang tidak ada di dalam workbook?* | Aspose.Cells menyematkan data secara langsung ke dalam objek diagram, sehingga diagram tetap berfungsi meskipun rentang sumber dihapus. |
| *Apakah saya memerlukan lisensi untuk Aspose?* | Evaluasi gratis dapat digunakan, tetapi versi berlisensi menghilangkan watermark evaluasi dan membuka semua fitur. |
| *Apakah diagram dapat diedit di Word setelah disisipkan?* | Diagram disisipkan sebagai diagram Word asli, sehingga pengguna dapat mengedit seri, judul, dan gaya menggunakan UI Word. |
| *Bagaimana cara menyisipkan diagram sebagai gambar alih-alih diagram asli?* | Gunakan `builder.InsertImage(chart.ToImage())` untuk menyematkan gambar raster. Ini berguna ketika Anda ingin mempertahankan tampilan visual persis tanpa kemampuan edit di tingkat Word. |

## Contoh lengkap yang berfungsi (salin‑paste)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Menjalankan kode menghasilkan file Word (`ReportWithCharts.docx`) yang berisi hasil **menambahkan diagram ke word** untuk setiap diagram dalam workbook sumber.

## Kesimpulan

Anda sekarang tahu cara **menambahkan diagram ke Word** menggunakan Aspose.Cells dan Aspose.Words, cara **menyematkan diagram Excel ke Word**, **mengekspor diagram Excel ke Word**, **membuat dokumen Word Aspose**, dan akhirnya **menyimpan dokumen Word berisi diagram**. Pendekatan ini bekerja untuk skenario satu diagram maupun untuk workbook kompleks dengan banyak diagram di beberapa lembar kerja.

Langkah selanjutnya yang dapat Anda jelajahi:

- Terapkan gaya khusus pada diagram yang disisipkan (warna, font) melalui API `Chart`.
- Gabungkan penyisipan diagram dengan pembuatan teks untuk menghasilkan laporan yang sepenuhnya otomatis.
- Gunakan Aspose.Slides jika Anda membutuhkan

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menyimpan DOCX dari Excel – Panduan Lengkap Mengekspor Diagram ke Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Membuat Workbook Excel dengan Diagram Pai Menggunakan Aspose.Cells .NET - Panduan Komprehensif](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Membuat Diagram Bubble di Excel Menggunakan Aspose.Cells .NET&#58; Panduan Langkah demi Langkah](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}