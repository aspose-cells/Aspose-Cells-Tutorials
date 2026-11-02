---
category: general
date: 2026-09-27
description: Pelajari cara menyalin tabel pivot di C# menggunakan Aspose.Cells. Termasuk
  menyalin baris dengan format, menyalin tabel pivot ke lembar lain, dan mengekspor
  tabel pivot ke buku kerja baru.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: id
lastmod: 2026-09-27
og_description: Cara menyalin tabel pivot di C# menggunakan Aspose.Cells. Ikuti panduan
  langkah demi langkah untuk menyalin baris dengan format, memindahkan tabel pivot
  ke lembar lain, dan mengekspornya ke buku kerja baru.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Cara menyalin tabel pivot di C# – panduan lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Cara menyalin tabel pivot di C# dengan Aspose.Cells
url: /id/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot di C# dengan Aspose.Cells

Jika Anda perlu **menyalin tabel pivot** dari satu lembar kerja ke lembar kerja lain, mempelajari **cara menyalin tabel pivot** di C# dengan Aspose.Cells dapat menghemat berjam‑jam kerja manual. Pendekatan ini juga memungkinkan Anda **menyalin baris dengan pemformatan**, menjaga cache pivot tetap utuh, dan bahkan **mengekspor tabel pivot ke buku kerja baru** ketika Anda memerlukan file terpisah.

Tutorial ini memandu Anda melalui alur kerja lengkap:

* membuat buku kerja,  
* menyalin rentang tabel pivot sambil mempertahankan pemformatan,  
* menempatkan data yang disalin ke lembar baru, dan  
* menyimpan hasilnya sebagai file terpisah.

Anda akan melihat mengapa metode bawaan `CopyRows` adalah cara paling andal untuk **menyalin tabel pivot ke lembar lain**, dan Anda akan mendapatkan tip untuk menangani kasus tepi seperti baris tersembunyi atau sumber data eksternal.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6.0 atau lebih baru | Aspose.Cells mendukung .NET 6+ dan memberikan kinerja terbaik. |
| Visual Studio 2022 (atau IDE C# apa saja) | Anda memerlukan editor yang dapat memulihkan paket NuGet. |
| Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`) | Perpustakaan ini menyediakan API `CopyRows` yang digunakan dalam contoh. |
| File Excel sumber (`source.xlsx`) yang berisi tabel pivot dalam rentang `A1:G20` | Kode menyalin rentang spesifik ini; sesuaikan rentang jika tabel pivot Anda lebih besar. |

Instal perpustakaan dengan NuGet CLI atau Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Langkah 1: Muat buku kerja yang berisi tabel pivot

Baris pertama membuat objek `Workbook` yang mewakili seluruh file Excel. Memuat file sekali memberi Anda akses baca/tulis ke setiap lembar kerja.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Mengapa langkah ini penting** – Tanpa memuat buku kerja, tidak ada pemanggilan `CopyRows` berikutnya yang dapat merujuk ke data sumber atau cache pivot.

## Langkah 2: Siapkan lembar kerja sumber dan tujuan

Anda memerlukan lembar tujuan di mana tabel pivot yang disalin akan ditempatkan. Kode di bawah mengambil lembar kerja pertama (tempat tabel pivot asli berada) dan menambahkan lembar baru bernama **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Tip pro:** Jika lembar tujuan sudah ada, panggil `Worksheets.RemoveAt(index)` terlebih dahulu untuk menghindari nama duplikat.

## Langkah 3: Tentukan area sel yang melingkupi tabel pivot

Objek `CellArea` mendeskripsikan sel kiri‑atas dan kanan‑bawah dari rentang yang ingin Anda pindahkan. Dalam contoh ini tabel pivot menempati `A1:G20`. Sesuaikan koordinat untuk tabel yang lebih besar.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Langkah 4: Salin baris dengan pemformatan dan pertahankan cache pivot

Metode `CopyRows` menyalin **baris** dari lembar sumber ke lembar tujuan. Dengan memberikan `CopyOptions.CopyAll` Anda memastikan nilai, pemformatan, diagram, dan objek tertanam—semua bagian dari tabel pivot—dipindahkan.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Mengapa `CopyRows` bekerja lebih baik daripada `Copy` untuk tabel pivot

* `CopyRows` menghormati cache pivot internal, sehingga tabel pivot yang disalin tetap berfungsi.
* Ia mempertahankan **menyalin baris dengan pemformatan** persis seperti yang muncul di lembar asli.
* Tidak seperti `Copy` sederhana pada rentang, ia juga memindahkan baris tersembunyi dan slicer yang terkait.

## Langkah 5: Simpan buku kerja dengan tabel pivot yang disalin

Akhirnya, tulis buku kerja yang telah dimodifikasi ke disk. File baru berisi lembar asli ditambah lembar **Copy** yang memuat duplikat tabel pivot yang berfungsi penuh.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Hasil yang diharapkan

Saat Anda membuka `pivot_copied.xlsx`:

* Lembar **Sheet1** masih berisi data dan tabel pivot asli.
* Lembar **Copy** menampilkan tabel pivot identik dengan tata letak, filter, dan pemformatan yang sama.
* Semua rumus dan koneksi data tetap utuh karena cache pivot disalin bersama baris.

## Cara menyalin tabel pivot ke lembar lain dalam buku kerja yang sama

Jika Anda hanya membutuhkan tabel pivot di lembar yang sudah ada (misalnya “Report”), ganti langkah pembuatan tujuan dengan referensi ke lembar target:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Potongan kode ini menunjukkan **menyalin tabel pivot ke lembar lain** tanpa membuat lembar kerja baru.

## Ekspor tabel pivot ke buku kerja baru

Kadang‑kadang Anda menginginkan tabel pivot dalam file yang sepenuhnya terpisah. Setelah operasi penyalinan, Anda dapat menghapus semua lembar kerja kecuali yang berisi tabel pivot yang disalin, lalu menyimpan:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Sekarang `pivot_only.xlsx` berisi satu lembar dengan tabel pivot yang diduplikasi, memenuhi kebutuhan **mengekspor tabel pivot ke buku kerja baru**.

## Cara menyalin baris Excel tanpa kehilangan pemformatan

Pemanggilan `CopyRows` yang sama bekerja untuk rentang apa pun, bukan hanya tabel pivot. Jika Anda perlu **menyalin baris Excel** yang mencakup pemformatan bersyarat, validasi data, atau sel yang digabung, gunakan metode yang sama:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Karena `CopyOptions.CopyAll` mentransfer semuanya, baris tujuan terlihat persis seperti baris sumber.

## Kesalahan umum dan cara menghindarinya

| Kesalahan | Gejala | Solusi |
|-----------|--------|--------|
| Rentang sumber tidak mencakup seluruh tabel pivot | Tabel pivot yang disalin terpotong. | Pastikan `CellArea` mencakup semua baris/kolom tabel pivot. |
| Lembar tujuan sudah berisi data | Baris yang ditimpa menyebabkan kehilangan data. | Pilih lembar baru atau mulai menyalin pada indeks baris yang lebih tinggi. |
| Tabel pivot menggunakan sumber data eksternal | Salinan kehilangan koneksinya. | Setelah menyalin, panggil `pivotTable.RefreshData()` untuk memulihkan tautan. |
| Baris tersembunyi tidak disertakan | Beberapa baris menghilang dalam salinan. | `CopyRows` secara otomatis menyalin baris tersembunyi; pastikan Anda tidak menggunakan `CopyOptions.CopyValuesOnly`. |

## Contoh lengkap yang dapat dijalankan

Berikut adalah program mandiri yang dapat Anda tempel ke proyek konsol baru. Program ini mendemonstrasikan setiap langkah yang dibahas di atas.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Menjalankan program** akan membuat `pivot_copied.xlsx` dengan duplikat tabel pivot asli pada lembar baru bernama **Copy**.

## Kesimpulan

Anda kini tahu **cara menyalin tabel pivot** di C# menggunakan

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat Buku Kerja Baru – Cara Menyalin Lembar Kerja dengan Tabel Pivot](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Salin Tabel Pivot di C# – Panduan Lengkap Langkah‑per‑Langkah](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Cara menyalin rentang dengan tabel pivot di C# – Panduan Lengkap](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}