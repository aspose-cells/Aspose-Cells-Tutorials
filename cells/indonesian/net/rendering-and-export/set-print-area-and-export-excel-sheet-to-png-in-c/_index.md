---
category: general
date: 2026-10-26
description: Atur area cetak dan ekspor lembar Excel ke PNG dalam C#. Pelajari opsi
  ekspor gambar, cara mengekspor PNG, dan dapatkan gambar yang dapat dicetak dari
  buku kerja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: id
lastmod: 2026-10-26
og_description: Atur area cetak dan ekspor lembar Excel ke PNG dalam C#. Tutorial
  langkah demi langkah ini mencakup opsi ekspor gambar serta cara mengekspor PNG dari
  buku kerja.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Atur area cetak dan ekspor lembar Excel ke PNG – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Atur area cetak dan ekspor lembar Excel ke PNG dalam C#
url: /id/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur area cetak dan ekspor lembar Excel ke PNG dalam C#

Jika Anda perlu **set print area** sebelum mengekspor lembar Excel ke PNG, panduan ini menunjukkan cara melakukannya. Anda akan melihat contoh lengkap C# yang mengonfigurasi opsi ekspor gambar, menyesuaikan area cetak worksheet, dan menyimpan hasilnya sebagai gambar.

Mengekspor lembar Excel ke PNG adalah kebutuhan umum ketika Anda ingin menyisipkan snapshot worksheet ke dalam laporan, email, atau halaman web. Kode di bawah ini bekerja dengan workbook apa pun yang berisi pivot table, tetapi teknik ini juga berlaku untuk rentang data biasa. Tidak diperlukan alat eksternal—hanya pustaka Aspose.Cells untuk .NET.

## Prerequisites

- .NET 6.0 atau yang lebih baru (contoh ini menargetkan .NET 6, tetapi versi .NET terbaru mana pun dapat digunakan)
- Aspose.Cells untuk .NET (pasang via NuGet: `Install-Package Aspose.Cells`)
- Familiaritas dasar dengan C# dan konsep Excel seperti worksheet dan area cetak

## Step 1: Configure image export options

Hal pertama yang Anda lakukan adalah membuat instance `ImageOrPrintOptions`. Objek ini memberi tahu Aspose.Cells cara merender sheet sebagai gambar.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Mengapa ini penting:** `ImageOrPrintOptions` mengontrol format output, resolusi, dan detail rendering lainnya. Menggunakan PNG memastikan kualitas lossless, yang ideal untuk laporan yang memerlukan teks dan grafik tajam.

## Step 2: Load the workbook and access the target worksheet

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Mengapa ini penting:** Anda harus bekerja dengan objek `Worksheet` tertentu karena area cetak merupakan pengaturan pada level worksheet.

## Step 3: Identify the range you want to print

Dalam banyak skenario data yang Anda butuhkan berada di dalam pivot table. Kode berikut mengekstrak rentang data dari pivot table pertama pada sheet.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Jika worksheet Anda tidak berisi pivot table, Anda dapat mengganti `pivotDataRange` dengan `CellArea` apa pun yang Anda buat secara manual, misalnya:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Step 4: **Set print area** to match the selected range

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Mengapa ini penting:** Area cetak memberi tahu Excel (dan Aspose.Cells) sel mana yang harus disertakan saat merender sheet menjadi gambar. Dengan menyelaraskan area cetak dengan rentang data pivot, Anda menghindari margin kosong dan memastikan PNG yang diekspor hanya berisi data yang relevan.

## Step 5: Export the worksheet to a PNG image

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Mengapa ini penting:** `worksheet.ToImage` menghormati area cetak yang telah ditetapkan sebelumnya, sehingga file PNG berisi tepat sel‑sel yang Anda definisikan. Menetapkan gambar ke shape picture memungkinkan Anda menyisipkannya kembali ke workbook bila diperlukan, sementara menyimpannya ke disk memberi Anda file mandiri.

## Full working example

Menggabungkan semua langkah menghasilkan program mandiri yang dapat Anda jalankan langsung.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Expected output

Menjalankan program akan membuat `C:\Temp\WorksheetExport.png`. Membuka file tersebut menampilkan gambar PNG yang tajam dan hanya berisi sel‑sel yang didefinisikan oleh **set print area** (data pivot table dalam contoh ini). Gambar tersebut dapat disisipkan ke dokumen Word, slide PowerPoint, atau halaman web tanpa langkah konversi tambahan.

## Handling multiple worksheets or pivot tables

- **Multiple worksheets:** Lakukan loop melalui `wb.Worksheets` dan ulangi langkah 3‑5 untuk setiap sheet yang ingin Anda ekspor.
- **Multiple pivot tables:** Pilih `PivotTables[index]` yang sesuai atau iterasi melalui `worksheet.PivotTables` untuk mengekspor tiap tabel secara terpisah.
- **No pivot table:** Buat `CellArea` secara manual (lihat komentar pada Step 3) dan tetapkan ke `PrintArea`.

## Practical tips (E‑E‑A‑T)

- **Pro tip:** Atur `HorizontalResolution` dan `VerticalResolution` ke 300 DPI untuk PNG siap cetak; nilai lebih rendah mengurangi ukuran file untuk penggunaan web.
- **Watch out for empty picture shapes:** Jika worksheet tidak memiliki picture shape, tambahkan satu sebelum menetapkan gambar:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Performance:** Menggunakan kembali satu instance `ImageOrPrintOptions` untuk beberapa worksheet menghindari alokasi yang tidak perlu.
- **Compatibility:** Aspose.Cells 23.9+ sepenuhnya mendukung .NET 6 dan yang lebih baru; versi sebelumnya mungkin memerlukan penyesuaian pada nama API.

## Conclusion

Anda kini tahu cara **set print area** dan mengekspor sebuah Excel


## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}