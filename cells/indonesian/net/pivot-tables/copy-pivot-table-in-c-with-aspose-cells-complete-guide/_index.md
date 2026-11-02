---
category: general
date: 2026-08-11
description: Salin tabel pivot menggunakan C# dan Aspose.Cells. Pelajari cara memuat
  buku kerja Excel, menduplikasi tabel pivot, dan mempertahankan formatnya dengan
  cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: id
lastmod: 2026-08-11
og_description: Salin tabel pivot di C# dengan Aspose.Cells. Panduan ini menunjukkan
  cara memuat buku kerja Excel, menggandakan tabel pivot, dan menjaga semua format
  tetap utuh.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Menyalin tabel pivot di C# – tutorial Aspose.Cells langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Menyalin tabel pivot di C# dengan Aspose.Cells – panduan lengkap
url: /id/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin tabel pivot di C# dengan Aspose.Cells – panduan lengkap

Jika Anda perlu **menyalin tabel pivot** dari satu lokasi ke lokasi lain dalam workbook Excel menggunakan C#, tutorial ini menunjukkan caranya. Anda akan melihat solusi singkat, menyeluruh yang memuat workbook, menduplikasi tabel pivot, dan mempertahankan setiap detail format.

Bekerja dengan Excel secara programatik sering berarti menangani objek kompleks seperti tabel pivot. Dalam panduan ini Anda akan belajar **menduplikasi tabel pivot excel** tanpa kehilangan filter, bidang terhitung, atau gaya. Satu-satunya prasyarat adalah referensi ke pustaka Aspose.Cells, yang memberi Anda kontrol penuh atas file Excel dari .NET.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.7+)
* Lisensi Aspose.Cells for .NET yang valid (Anda dapat menggunakan versi evaluasi gratis untuk pengujian)
* File Excel (`Source.xlsx`) yang berisi tabel pivot yang ingin Anda salin
* Lingkungan pengembangan seperti Visual Studio 2022

## Cara menyalin tabel pivot dengan Aspose.Cells

Langkah‑langkah inti adalah:

1. **Muat workbook Excel C#** – buka file sumber.
2. **Pilih rentang yang berisi tabel pivot** – sertakan seluruh area pivot.
3. **Salin rentang ke lokasi baru** – tabel pivot tetap utuh.
4. **Simpan workbook** – file baru berisi tabel pivot yang diduplikasi.

Setiap langkah dijelaskan di bawah ini dengan kode lengkap.

### Langkah 1: Muat workbook Excel C#

Memuat workbook adalah tindakan pertama ketika Anda **load excel workbook c#**. Aspose.Cells membaca file ke memori, memberi Anda akses ke lembar kerja, sel, dan tabel pivot.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Mengapa ini penting:** Memuat workbook membuat objek `Workbook` yang mewakili seluruh file Excel. Semua operasi selanjutnya bekerja pada representasi dalam memori ini, yang lebih cepat daripada mengakses sistem file berulang‑ulang.

### Langkah 2: Identifikasi dan salin rentang tabel pivot

Sebuah tabel pivot berada di dalam rentang sel persegi panjang. Untuk **move pivot table cell** dengan aman, Anda harus menyalin seluruh rentang, bukan hanya sel‑sel individual.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Mengapa ini berhasil:** `Range.Copy` menduplikasi tidak hanya nilai sel tetapi juga cache pivot yang mendasari dan formatnya. Ini adalah cara yang direkomendasikan untuk **duplicate pivot table excel** tanpa harus membangun ulang pivot secara manual.

### Langkah 3: Simpan workbook dengan tabel pivot yang disalin

Setelah menyalin, Anda cukup menyimpan workbook. File baru akan berisi baik tabel pivot asli maupun yang diduplikasi.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Mengapa Anda harus mempertahankan format:** Persyaratan `preserve pivot formatting` terpenuhi secara otomatis karena Aspose.Cells menyimpan informasi gaya selama operasi penyalinan. Tidak diperlukan kode styling tambahan.

### Contoh lengkap yang dapat dijalankan

Menggabungkan ketiga langkah memberikan program lengkap yang dapat dijalankan:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Hasil yang diharapkan:**  
Buka `CopyPivot.xlsx` di Excel. Anda akan melihat tabel pivot asli tetap tidak berubah dan tabel pivot kedua yang identik mulai dari sel `I1`. Semua filter, bidang terhitung, dan gaya visual cocok dengan sumber.

## Variasi umum dan kasus tepi

| Situasi | Cara menanganinya |
|-----------|------------------|
| **Tabel pivot mencakup rentang dinamis** | Gunakan `PivotTable.PivotTableRange` untuk memperoleh alamat tepat pada waktu berjalan alih‑alih meng‑hard‑code `"A1:G20"`. |
| **Anda perlu memindahkan tabel pivot ke lembar kerja lain** | Panggil `sourceRange.Copy(otherWorksheet.Cells, "A1")` setelah membuat `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Hanya mempertahankan format, bukan data** | Setelah menyalin, bersihkan nilai data dengan `targetRange.Clear(ClearOptions.Contents)` sambil membiarkan gaya tetap. |
| **Workbook besar menyebabkan tekanan memori** | Gunakan `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` agar Aspose.Cells melakukan streaming data. |
| **Anda ingin mengganti nama tabel pivot yang diduplikasi** | Akses pivot baru lewat `sheet.PivotTables[sheet.PivotTables.Count - 1]` dan atur properti `Name`‑nya. |

Tips ini membantu Anda **move pivot table cell** ke posisi baru, **duplicate pivot table excel**, dan menjaga persyaratan **preserve pivot formatting** tetap terpenuhi.

## Pro tip untuk penyalinan yang dapat diandalkan

* **Pro tip:** Selalu pastikan rentang sumber mencakup seluruh cache pivot. Kehilangan satu kolom dapat merusak pivot yang disalin.
* **Waspadai sel yang digabung** di dalam rentang; mereka dapat menyebabkan `Copy` melempar pengecualian. Lepaskan penggabungan sebelum menyalin atau sesuaikan rentangnya.
* **Tip performa:** Jika Anda hanya perlu menyalin definisi pivot (tanpa data), gunakan `PivotTable.Clone` alih‑alih menyalin seluruh rentang.

## Kesimpulan

Anda kini tahu cara **menyalin tabel pivot** secara programatik di C# menggunakan Aspose.Cells sambil **preserve pivot formatting**, **load excel workbook c#**, dan bahkan **move pivot table cell** ke posisi lintas lembar kerja. Solusi lengkap memuat workbook, menduplikasi rentang pivot, dan menyimpan file baru dengan kedua tabel tetap utuh.

Selanjutnya, Anda dapat menjelajahi skenario **duplicate pivot table excel** seperti menyalin antar workbook berbeda, atau mengotomatisasi pembuatan laporan dengan banyak tabel pivot. Untuk kustomisasi lebih dalam, lihat API PivotTable Aspose.Cells untuk memodifikasi filter, bidang terhitung, atau koneksi grafik.

Selamat coding, dan silakan bereksperimen dengan kode untuk menyesuaikannya dengan kebutuhan otomatisasi Excel Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Efficiently Change Excel Pivot Table Layouts Using Aspose.Cells for .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}