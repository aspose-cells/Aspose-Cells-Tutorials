---
category: general
date: 2026-10-26
description: Pelajari cara mengekspor grafik Excel ke PowerPoint dengan C#. Pertahankan
  kemampuan mengedit bentuk dan simpan sebagai PPTX dalam beberapa baris kode.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: id
lastmod: 2026-10-26
og_description: Ekspor diagram Excel ke PowerPoint dengan C#. Panduan ini menunjukkan
  cara menjaga bentuk tetap dapat diedit dan menyimpan sebagai PPTX menggunakan Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Ekspor diagram Excel ke PowerPoint dengan C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Cara mengekspor grafik Excel ke PowerPoint menggunakan C#
url: /id/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor diagram Excel ke PowerPoint menggunakan C#

Jika Anda perlu **mengekspor diagram Excel ke PowerPoint**, panduan ini akan memandu Anda melalui solusi lengkap yang siap dijalankan. Baik Anda sedang membangun dasbor pelaporan atau mengotomatisasi deck slide, Anda akan melihat bagaimana beberapa baris kode C# menjaga bentuk diagram Anda tetap dapat diedit sepenuhnya setelah konversi.

Dalam tutorial ini Anda akan belajar cara:

* Memuat workbook Excel yang sudah ada yang berisi diagram.  
* (Opsional) menyesuaikan pengaturan workbook sebelum konversi.  
* Menyimpan workbook sebagai file PowerPoint sambil mempertahankan kemampuan mengedit bentuk.  

Semua ini dilakukan dengan **Aspose.Cells for .NET**, sebuah perpustakaan yang menangani konversi Excel‑ke‑PowerPoint tanpa memerlukan Microsoft Office di server.

## Apa yang Anda butuhkan

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 atau lebih baru | Runtime modern dengan fitur bahasa lengkap |
| Visual Studio 2022 (atau IDE apa pun) | Editor dan debugger yang nyaman |
| **Aspose.Cells for .NET** paket NuGet | Menyediakan kelas `Workbook` dan dukungan `SaveFormat.Pptx` |
| File Excel (`ChartAndShapes.xlsx`) yang berisi setidaknya satu diagram | Sumber diagram yang ingin Anda ekspor |

> **Tip pro:** Gunakan versi **Aspose.Cells Evaluation** gratis untuk menguji kode; kunci lisensi menghapus watermark evaluasi.

```bash
dotnet add package Aspose.Cells
```

## Mengekspor diagram Excel ke PowerPoint – alur kerja lengkap

Berikut adalah kode end‑to‑end yang melakukan ekspor sambil **mempertahankan kemampuan mengedit bentuk**. Setiap langkah dijelaskan secara detail.

### Langkah 1: Memuat workbook Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*Kelas `Workbook` mewakili seluruh file Excel. Memuat file membaca semua lembar kerja, diagram, dan bentuk ke memori, yang diperlukan untuk manipulasi lebih lanjut.*

### Langkah 2: (Opsional) Menyesuaikan pengaturan workbook

Dalam kebanyakan kasus pengaturan default sudah cukup untuk ekspor yang bersih. Namun, jika Anda perlu mengubah mode perhitungan, pengaturan halaman, atau menyembunyikan lembar tertentu, Anda dapat melakukannya di sini.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Mengapa ini penting:** Menyesuaikan pengaturan sebelum konversi menjamin bahwa slide yang dihasilkan mencerminkan keadaan tepat yang Anda inginkan, terutama ketika formula atau lembar tersembunyi dapat memengaruhi data diagram.

### Langkah 3: Menyimpan workbook sebagai file PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*Konstanta `SaveFormat.Pptx` memberi tahu Aspose.Cells untuk menulis presentasi PowerPoint. Secara internal, perpustakaan mengonversi setiap diagram Excel menjadi bentuk PowerPoint yang tetap dapat diedit sepenuhnya di Microsoft PowerPoint.*

### Langkah 4: Memverifikasi hasil

Buka `Shapes.pptx` di PowerPoint dan:

1. Pilih diagram pada slide mana pun.  
2. Klik kanan → **Edit Data**.  
3. Pastikan tabel data diagram muncul dan Anda dapat mengubah nilai.

Jika diagram membuka panel **Edit Data**, konversi berhasil dan **kemampuan mengedit bentuk** dipertahankan.

![Contoh mengekspor diagram Excel ke PowerPoint](export-excel-charts-to-powerpoint.png){.img-fluid alt="Contoh mengekspor diagram Excel ke PowerPoint"}

## Kesulitan umum dan cara menghindarinya

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| Diagram muncul sebagai gambar statis | Menggunakan versi Aspose.Cells yang lebih lama yang tidak mendukung ekspor PPTX | Upgrade ke Aspose.Cells 23.x terbaru atau yang lebih baru |
| Data hilang pada diagram PowerPoint | Workbook tidak dihitung sepenuhnya sebelum ekspor | Panggil `workbook.CalculateFormula()` sebelum `Save` |
| Bentuk tidak dapat diedit | Menyimpan dengan `SaveFormat.Xlsx` alih-alih `SaveFormat.Pptx` | Pastikan Anda menggunakan `SaveFormat.Pptx` pada `Workbook.Save` |
| Pengecualian lisensi saat runtime | Versi evaluasi tanpa lisensi terdaftar | Daftarkan lisensi Anda dengan `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Kasus khusus: Mengekspor beberapa lembar kerja dengan diagram terpisah

Jika file Excel Anda berisi beberapa lembar kerja, masing‑masing dengan diagramnya, Aspose.Cells secara otomatis membuat slide terpisah untuk setiap diagram. Anda dapat mengontrol urutan slide dengan menyusun ulang lembar kerja sebelum operasi penyimpanan.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Tips kinerja: Stream output alih‑alih menulis ke disk

Saat menghasilkan file PowerPoint dalam API web, hindari file sementara dengan menulis ke `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Contoh lengkap yang dapat dijalankan

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Output yang diharapkan:** Konsol mencetak pesan konfirmasi, dan `Shapes.pptx` terbuka di PowerPoint dengan setiap diagram Excel muncul pada slide masing‑masing. Memilih sebuah diagram memungkinkan Anda mengedit datanya, mengonfirmasi bahwa **kemampuan mengedit bentuk** tetap terjaga.

## Ringkasan dan langkah selanjutnya

Anda kini tahu cara **mengekspor diagram Excel ke PowerPoint** dengan C# sambil menjaga diagram tetap dapat diedit sepenuhnya. Inti solusi adalah metode `Workbook.Save` dengan `SaveFormat.Pptx`, sebuah fitur **Ekspor Aspose.Cells** yang menyederhanakan penanganan Open XML yang kompleks.

Dari sini Anda dapat menjelajahi:

* Menambahkan judul slide khusus atau catatan menggunakan API **Aspose.Slides**.  
* Mengonversi objek Excel lain (tabel, gambar) bersama diagram.  
* Mengotomatiskan pemrosesan batch beberapa workbook dalam layanan latar belakang.

Silakan bereksperimen dengan pengaturan opsional yang ditunjukkan di atas, dan integrasikan pola ini ke dalam alur pelaporan Anda untuk menghasilkan PowerPoint yang cepat dan andal.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Mengekspor diagram Excel ke PowerPoint dengan C# – panduan lengkap Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Cara Mengekspor Excel ke PowerPoint dengan C# – Panduan Lengkap](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Cara Mengekspor Bentuk dari Excel ke PowerPoint – Panduan Lengkap](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}