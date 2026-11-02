---
category: general
date: 2026-09-11
description: Salin tabel pivot dan ekspor Excel ke PPTX menggunakan Aspose.Cells.
  Pelajari cara menghasilkan PPTX yang dapat diedit dan menyimpan buku kerja sebagai
  PPTX dalam C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: id
lastmod: 2026-09-11
og_description: Salin tabel pivot dan ekspor Excel ke PPTX dalam C# menggunakan Aspose.Cells.
  Hasilkan PPTX yang dapat diedit dan simpan buku kerja sebagai PPTX dengan beberapa
  baris kode.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Salin tabel pivot dan ekspor Excel ke PPTX – panduan lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Salin tabel pivot dan ekspor Excel ke PPTX dengan Aspose.Cells
url: /id/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin tabel pivot dan ekspor Excel ke PPTX dengan Aspose.Cells

Jika Anda perlu menyalin tabel pivot dari satu lembar kerja ke lembar kerja lain dan kemudian mengekspor file Excel ke presentasi PowerPoint, panduan ini menunjukkan cara melakukannya. Dengan menggunakan Aspose.Cells Anda dapat menghasilkan PPTX yang dapat diedit dan menyimpan workbook sebagai PPTX hanya dengan beberapa baris kode C#.

Tutorial ini mencakup setiap langkah yang diperlukan untuk memindahkan tabel pivot, mempertahankan fungsionalitasnya, dan menghasilkan file PPTX di mana grafik dan bentuk tetap dapat diedit. Tidak diperlukan alat eksternal—hanya pustaka Aspose.Cells dan lingkungan pengembangan .NET.

## Apa yang akan Anda capai

* **Copy pivot table** dari lembar sumber ke lembar tujuan sambil mempertahankan semua koneksi data tetap utuh.  
* **Export Excel to PPTX** sehingga slide yang dihasilkan dapat diedit di PowerPoint.  
* **Generate editable PPTX** di mana grafik, tabel, dan bentuk tidak diubah menjadi gambar.  
* **Save workbook as PPTX** dengan menggunakan panggilan API Aspose.Cells yang sama.  

### Prasyarat

* .NET 6.0 atau yang lebih baru (kode ini juga berfungsi dengan .NET Framework 4.6+).  
* Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`).  
* Pemahaman dasar tentang aplikasi konsol C#.  

> **Tips pro:** Instal paket NuGet melalui CLI untuk memastikan Anda memiliki versi terbaru:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Cara menyalin tabel pivot antar lembar kerja

Operasi pertama adalah memindahkan tabel pivot sambil mempertahankan definisinya. Aspose.Cells menyediakan metode `CopyRange` dengan objek `CopyOptions` yang mencakup flag `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Mengapa ini berhasil:**  
`CopyRange` menyalin data sel, pemformatan, dan, ketika `CopyPivotTable` bernilai true, cache serta metadata tabel pivot. Rentang tujuan dimulai pada sel `A1` (baris 0, kolom 0) tetapi Anda dapat mengubah offset untuk menempatkan tabel pivot di lokasi lain.

**Kasus tepi umum:** Jika lembar tujuan sudah berisi tabel pivot dengan nama yang sama, Aspose.Cells akan secara otomatis mengganti nama tabel yang masuk, sehingga menghindari bentrok nama.

## Ekspor Excel ke PPTX dan hasilkan PPTX yang dapat diedit

Setelah tabel pivot berada di tempatnya, Anda dapat mengekspor seluruh workbook ke file PPTX. Kelas `ImageOrPrintOptions` memungkinkan Anda menentukan `ExportImageFormat = ImageFormat.Pptx`, yang memberi tahu Aspose.Cells untuk memperlakukan output sebagai presentasi PowerPoint bukan gambar raster.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Mengapa ini berhasil:**  
Ketika `ExportImageFormat` diatur ke `Pptx`, Aspose.Cells menerjemahkan setiap lembar kerja menjadi satu slide. Bentuk, grafik, dan tabel pivot ditulis sebagai objek PowerPoint asli, sehingga Anda dapat mengklik ganda mereka di PowerPoint dan mengedit data yang mendasarinya.

**Tip untuk workbook besar:** Jika Anda hanya memerlukan sebagian lembar, gunakan `workbook.Worksheets.RemoveAt(index)` untuk lembar yang tidak ingin diekspor sebelum memanggil `Save`. Ini mengurangi ukuran file PPTX.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang menggabungkan langkah‑langkah sebelumnya. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya di mesin Anda.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Output yang diharapkan

Menjalankan program akan mencetak:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Saat Anda membuka `output.pptx` di Microsoft PowerPoint, Anda akan melihat slide yang berisi tabel pivot yang disalin sebagai grafik yang dapat diedit. Mengklik ganda grafik membuka editor grafik PowerPoint, memungkinkan Anda memodifikasi seri, sumbu, dan label data tanpa harus kembali ke Excel.

## Menangani jebakan umum

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| Tabel pivot muncul sebagai gambar statis | Flag `CopyPivotTable` tidak disertakan atau `ExportImageFormat` diatur ke `Png` | Pastikan `CopyPivotTable = true` dan `ExportImageFormat = ImageFormat.Pptx`. |
| Lembar tujuan menampilkan sel kosong | Rentang sumber tidak mencakup seluruh area tabel pivot | Perluas rentang (misalnya, `"A1:H30"`) untuk menyertakan semua bidang pivot. |
| PPTX yang diekspor sangat besar | Lembar kerja yang tidak diperlukan termasuk | Hapus lembar yang tidak diinginkan sebelum memanggil `Save`. |
| PowerPoint tidak dapat mengedit grafik | Menggunakan versi Aspose.Cells yang lebih lama yang tidak mendukung PPTX | Tingkatkan ke versi Aspose.Cells terbaru (periksa catatan rilis). |

## Langkah selanjutnya dan topik terkait

* **Export Excel sheet to PPTX with custom slide layouts** – jelajahi `WorksheetToPdfConverter` untuk kontrol yang lebih halus atas tampilan slide.  
* **Export Excel to PDF** – ganti `ImageFormat.Pptx` dengan `ImageFormat.Pdf` untuk menghasilkan PDF sebagai gantinya.  
* **Programmatically modify PPTX after export** – gunakan pustaka `Aspose.Slides` untuk menambahkan animasi atau catatan pembicara.  

Dengan menguasai **copy pivot table**, **export excel to pptx**, dan **generate editable pptx**, Anda dapat membangun alur pelaporan end‑to‑end yang memindahkan data dari spreadsheet langsung ke dek presentasi tanpa kehilangan kemampuan edit.

---


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}