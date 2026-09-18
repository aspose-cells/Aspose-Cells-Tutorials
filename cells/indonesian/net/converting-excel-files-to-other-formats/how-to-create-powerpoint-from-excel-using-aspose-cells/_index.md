---
category: general
date: 2026-09-18
description: Buat PowerPoint dari Excel dengan Aspose.Cells – salin tabel pivot, ekspor
  rentang, dan simpan sebagai PPTX dalam beberapa baris kode C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: id
lastmod: 2026-09-18
og_description: Buat PowerPoint dari Excel dengan cepat. Pelajari cara menyalin tabel
  pivot, mengekspor rentang, dan menyimpan buku kerja sebagai PPTX menggunakan Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Buat PowerPoint dari Excel dengan Aspose.Cells – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Cara membuat PowerPoint dari Excel menggunakan Aspose.Cells
url: /id/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat PowerPoint dari Excel menggunakan Aspose.Cells

Jika Anda perlu membuat PowerPoint dari Excel, panduan ini menunjukkan solusi singkat end‑to‑end. Anda akan melihat cara menyalin tabel pivot, mengekspor rentang yang dipilih, dan menyimpan hasilnya sebagai file PPTX dengan hanya beberapa baris C#.

Membuat deck slide langsung dari data spreadsheet menghilangkan langkah salin‑tempel manual yang memperlambat alur kerja pelaporan. Tutorial ini mencakup semua yang Anda butuhkan, mulai dari penyiapan proyek hingga file PPTX akhir, dan bekerja dengan Aspose.Cells untuk .NET versi terbaru.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* **Aspose.Cells for .NET** (versi 23.12 atau lebih baru). Instal melalui NuGet: `Install-Package Aspose.Cells`.
* Lingkungan pengembangan **.NET 6+** (Visual Studio 2022 atau VS Code).
* Workbook Excel (`Source.xlsx`) yang berisi data dan tabel pivot yang ingin Anda gunakan kembali.
* Izin menulis ke folder output.

Tidak diperlukan pustaka pihak ketiga tambahan.

## Membuat PowerPoint dari Excel – langkah demi langkah

Proses ini terdiri dari empat langkah logis yang langsung berhubungan dengan contoh kode yang akan Anda lihat nanti.

### Langkah 1: Muat workbook sumber dan tentukan rentang

Anda harus memuat workbook yang berisi data sumber dan tabel pivot. Memilih rentang yang tepat memastikan hanya sel yang diperlukan yang ditransfer, sehingga slide yang dihasilkan tetap ringan.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Mengapa ini penting:**  
`CreateRange` membuat objek `Range` yang dapat disalin secara keseluruhan. Dengan membatasi rentang ke `A1:G20`, Anda menghindari penarikan sel yang tidak terkait, yang dapat membuat file PowerPoint menjadi lebih besar.

### Langkah 2: Siapkan workbook tujuan

Aspose.Cells memperlakukan slide PowerPoint sebagai workbook ketika Anda menyimpannya dalam format PPTX. Membuat workbook baru memberi Anda kanvas bersih untuk rentang yang disalin.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tip:** Jika Anda memerlukan beberapa slide, Anda dapat menambahkan worksheet tambahan dan kemudian menyimpan masing‑masing sebagai file PPTX terpisah.

### Langkah 3: Salin rentang sambil mempertahankan tabel pivot

Metode `CopyRange` menerima objek `PasteOptions`. Menetapkan `CopyPivotTables = true` memberi tahu Aspose.Cells untuk menjaga struktur tabel pivot tetap utuh, bukan hanya nilai yang dirender.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Cara kerjanya:**  
Ketika `CopyPivotTables` bernilai true, sheet tujuan menerima baik data sumber maupun cache pivot. Ini berarti tabel pivot tetap berfungsi penuh dan dapat disegarkan kembali nanti jika data sumber berubah.

### Langkah 4: Simpan workbook sebagai file PowerPoint

Akhirnya, ekspor workbook ke format PPTX. Flag `SaveFormat.Pptx` memberi tahu Aspose.Cells untuk menulis worksheet sebagai slide PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Hasil:**  
`CopyWithPivot.pptx` terbuka di Microsoft PowerPoint (atau penampil kompatibel lainnya) dengan satu slide yang menampilkan rentang yang disalin, termasuk tabel pivot hidup yang dapat berinteraksi di PowerPoint.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda tempel ke dalam proyek konsol baru dan jalankan langsung.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Output yang diharapkan:**  
Menjalankan program mencetak “PowerPoint file created successfully.” dan menghasilkan file bernama `CopyWithPivot.pptx`. Membuka file di PowerPoint menampilkan satu slide di mana rentang Excel yang disalin muncul persis seperti di worksheet sumber, dengan tabel pivot aktif yang dapat disegarkan dari dalam PowerPoint.

## Variasi umum dan kasus tepi

| Situasi | Apa yang harus diubah |
|-----------|----------------|
| **Beberapa tabel pivot** | Tentukan objek `Range` terpisah untuk setiap tabel dan panggil `CopyRange` untuk masing‑masing, atau salin seluruh sheet jika mereka berbagi sumber data yang sama. |
| **Set data besar** | Perbesar rentang (misalnya, `"A1:Z5000"`). Pertimbangkan mengaktifkan `PasteOptions.CompressData = true` untuk mengurangi ukuran PPTX. |
| **Tata letak slide berbeda** | Setelah menyimpan sebagai PPTX, buka file di PowerPoint dan terapkan tata letak atau tema khusus; data tetap dapat diedit. |
| **Menyimpan ke stream** | Gunakan `destinationWorkbook.Save(stream, SaveFormat.Pptx)` ketika Anda perlu mengembalikan PPTX melalui API web. |
| **Mempertahankan pemformatan sel** | Atur `PasteOptions.PasteType = PasteType.All` untuk menjaga font, warna, dan border. |

**Tips profesional:** Selalu pastikan folder tujuan ada sebelum memanggil `Save`. Jika folder tidak ada, `Save` akan melempar `DirectoryNotFoundException`.

## Kesimpulan

Anda kini tahu cara membuat PowerPoint dari Excel, menyalin tabel pivot, dan mengekspor hasilnya sebagai file PPTX menggunakan Aspose.Cells. Langkah‑langkah—memuat workbook sumber, menentukan rentang, menyalin dengan `CopyPivotTables`, dan menyimpan sebagai PPTX—menutupi seluruh alur kerja secara andal dan siap produksi.

Selanjutnya, jelajahi **cara mengekspor Excel ke PPTX** untuk beberapa worksheet, atau pelajari **cara menyalin rentang antar workbook** ketika Anda perlu menggabungkan data dari beberapa sumber sebelum menghasilkan deck slide. Kedua topik dibangun di atas permukaan API yang sama dan dapat digabungkan untuk mengotomatisasi pipeline pelaporan yang kompleks.

Selamat coding, dan nikmati mengubah spreadsheet Anda menjadi presentasi yang profesional!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menyalin Tabel Pivot di C# – Mengonversi Excel ke PPTX, Menyalin Rentang & Membuat Kotak Teks](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Buat Workbook Baru – Cara Menyalin Worksheet dengan Tabel Pivot](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Cara Membuat dan Menyimpan File Excel dengan Aspose.Cells untuk .NET: Panduan Lengkap](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}