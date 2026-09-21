---
category: general
date: 2026-09-21
description: Ekspor Excel ke PowerPoint dengan grafik yang dapat diedit menggunakan
  Aspose.Cells. Ikuti panduan langkah demi langkah ini untuk mengonversi lembar kerja
  ke PPTX sambil mempertahankan grafik yang dapat diedit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: id
lastmod: 2026-09-21
og_description: Ekspor Excel ke PowerPoint dengan grafik yang dapat diedit menggunakan
  Aspose.Cells. Pelajari cara mengonversi lembar kerja ke PPTX sambil mempertahankan
  kemampuan mengedit grafik secara penuh.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Ekspor Excel ke PowerPoint dengan Grafik yang Dapat Diedit – Tutorial C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Ekspor Excel ke PowerPoint dengan grafik yang dapat diedit di C#
url: /id/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Excel ke PowerPoint dengan grafik yang dapat diedit di C#

Mengekspor Excel ke PowerPoint dengan grafik yang dapat diedit adalah kebutuhan umum ketika Anda perlu menggunakan kembali visual spreadsheet dalam presentasi. Panduan ini menunjukkan cara **mengekspor Excel ke PowerPoint** sambil mempertahankan kemampuan mengedit grafik, menggunakan Aspose.Cells untuk .NET.

Anda akan belajar cara:

* Memuat workbook yang sudah ada yang berisi grafik dan kotak teks.  
* Mengonfigurasi opsi ekspor PPTX sehingga grafik dan bentuk tetap dapat diedit.  
* Mengonversi worksheet tertentu ke file PowerPoint yang dapat dibuka dan diedit di Microsoft PowerPoint.

Tutorial ini mengasumsikan Anda memiliki pengetahuan dasar C# dan versi .NET terbaru (≥ .NET 6). Tidak diperlukan pengalaman sebelumnya dengan Aspose.Cells.

---

## Ekspor Excel ke PowerPoint – ikhtisar

Ide utama di balik **export Excel to PowerPoint** adalah memperlakukan setiap worksheet sebagai sumber gambar yang dapat dirender ke slide PPTX. Dengan mengaktifkan flag `ExportChartAsEditableText` dan `ExportShapeAsEditableText`, Aspose.Cells menulis data grafik yang mendasarinya sebagai objek gambar PowerPoint alih‑alih bitmap datar. Hal ini membuat slide yang dihasilkan sepenuhnya dapat diedit—seperti grafik yang dibuat langsung di PowerPoint.

> **Why use editable charts?**  
> Grafik yang dapat diedit memungkinkan presenter menyesuaikan data, warna, atau label tanpa harus kembali ke file Excel asli, mempercepat perubahan menit‑terakhir dan menjaga alur kerja presentasi tetap lancar.

---

## Mengonversi worksheet ke PowerPoint (worksheet ke PowerPoint)

Berikut adalah contoh lengkap yang dapat dijalankan yang mendemonstrasikan konversi **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Penjelasan setiap langkah

| Langkah | Apa yang dilakukan kode | Mengapa penting untuk **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | Memuat `input.xlsx` ke dalam objek `Aspose.Cells.Workbook`. | Workbook menyediakan akses ke grafik yang ingin Anda ekspor. |
| 2️⃣   | Mengatur `ExportType` ke `Pptx` dan mengaktifkan `ExportChartAsEditableText` & `ExportShapeAsEditableText`. | Flag ini adalah kunci untuk **editable charts pptx** – mereka memberi tahu perpustakaan untuk menulis geometri grafik sebagai objek gambar PowerPoint alih‑alih gambar raster. |
| 3️⃣   | Memanggil `ConvertToImage` pada worksheet pertama, menghasilkan `Worksheet.pptx`. | Metode ini melakukan operasi **export excel to powerpoint** dan menulis file PPTX yang dapat dibuka langsung di PowerPoint. |

> **Pro tip:** Jika Anda perlu mengekspor *multiple* worksheet, lakukan loop pada `workbook.Worksheets` dan panggil `ConvertToImage` untuk setiapnya, secara opsional memberi nama file output `Sheet1.pptx`, `Sheet2.pptx`, dll.

---

## Mengaktifkan grafik yang dapat diedit di PPTX (export excel chart pptx)

Saat `ExportChartAsEditableText` diatur ke `true`, Aspose.Cells menulis setiap grafik sebagai kumpulan elemen `<a:graphic>` di dalam XML PPTX. PowerPoint kemudian memperlakukan elemen‑elemen tersebut sebagai objek grafik native, yang dapat Anda double‑click untuk membuka editor grafik.

**Common pitfalls**

* **Missing Aspose.Cells license** – Tanpa lisensi, perpustakaan menambahkan watermark pada output. Daftarkan lisensi di awal program Anda (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Unsupported chart types** – Meskipun sebagian besar grafik 2‑D (kolom, garis, pai) dapat diedit sepenuhnya, beberapa grafik 3‑D atau kombinasi yang kompleks mungkin kembali menjadi gambar. Uji tipe grafik spesifik Anda jika mengandalkan kemampuan edit penuh.  
* **Large worksheets** – Mengekspor worksheet yang sangat besar dapat mengonsumsi memori signifikan. Pertimbangkan menggunakan `ExportMaxRows` atau `ExportMaxColumns` dalam `ImageOrPrintOptions` untuk membatasi area yang dikonversi.

---

## Tips untuk menjaga grafik tetap dapat diedit (editable charts pptx)

1. **Preserve chart data ranges** – Pastikan sumber data grafik berada di worksheet yang sama dengan yang Anda ekspor. Referensi lintas‑sheet diubah menjadi nilai statis dalam PPTX.  
2. **Use the latest Aspose.Cells version** – Rilis terbaru meningkatkan dukungan untuk fitur grafik tambahan dan memperbaiki bug kasus‑tepi terkait ekspor PPTX.  
3. **Validate the output** – Setelah konversi, buka PPTX yang dihasilkan di PowerPoint dan verifikasi bahwa Anda dapat mengedit judul grafik, seri, dan label sumbu. Jika ada elemen yang muncul sebagai gambar, periksa kembali bahwa `ExportChartAsEditableText` diaktifkan dan tipe grafik didukung.  
4. **Batch processing** – Untuk skenario otomatisasi (misalnya, menghasilkan deck slide dari banyak laporan Excel), bungkus logika konversi dalam metode yang menerima `Workbook`, `int worksheetIndex`, dan `string outputPath`. Ini memisahkan alur kerja **export excel to powerpoint** dan membuatnya dapat digunakan kembali.

---

## Ringkasan contoh kerja penuh

Menggabungkan semua bagian, berikut program minimal yang dapat Anda salin‑tempel ke proyek konsol .NET baru:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Expected result**

* File bernama `Worksheet.pptx` muncul di `YOUR_DIRECTORY`.  
* Membuka file tersebut di Microsoft PowerPoint menampilkan slide yang berisi grafik asli dan semua kotak teks.  
* Double‑click pada grafik membuka editor grafik PowerPoint, memungkinkan Anda mengubah nilai seri, warna, atau judul sumbu—memastikan fitur **editable charts pptx** berfungsi sebagaimana mestinya.

---

## Kesimpulan

Anda kini memiliki solusi lengkap untuk **export Excel to PowerPoint** yang menjaga grafik tetap dapat diedit. Dengan mengonfigurasi `ImageOrPrintOptions` dengan `ExportChartAsEditableText` dan `ExportShapeAsEditableText`, proses konversi menghasilkan file PPTX native di mana grafik berperilaku seperti yang dibuat langsung di PowerPoint.  

Dari sini Anda dapat:

* Memperluas kode untuk menangani banyak worksheet (**worksheet to PowerPoint** untuk masing‑masing).  
* Menggabungkan ekspor dengan fitur Aspose.Cells lainnya, seperti menambahkan judul slide atau menyisipkan gambar.  
* Menjelajahi topik terkait seperti **export Excel chart PPTX** dengan tema khusus atau mengotomatiskan seluruh pipeline pembuatan deck slide.

Silakan bereksperimen dengan berbagai tipe grafik, tambahkan label data, atau integrasikan alur kerja ini ke dalam sistem pelaporan yang lebih besar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengonversi Excel ke PowerPoint Menggunakan Aspose.Cells untuk .NET: Panduan Lengkap](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}