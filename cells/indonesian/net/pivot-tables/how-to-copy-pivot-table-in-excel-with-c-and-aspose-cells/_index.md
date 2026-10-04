---
category: general
date: 2026-10-04
description: Pelajari cara menyalin tabel pivot dari satu buku kerja ke buku kerja
  lain menggunakan C#. Panduan ini juga mencakup cara menyalin baris, menduplikasi
  tabel pivot, dan menyalin rentang Excel secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: id
lastmod: 2026-10-04
og_description: Salin tabel pivot di Excel menggunakan C#. Ikuti tutorial lengkap
  ini untuk menduplikasi tabel pivot, menyalin baris, dan menyalin rentang Excel dengan
  Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Menyalin tabel pivot di Excel dengan C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara menyalin tabel pivot di Excel dengan C# dan Aspose.Cells
url: /id/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot di Excel dengan C# dan Aspose.Cells

Jika Anda perlu **menyalin tabel pivot** dari satu workbook ke workbook lain, tutorial ini menunjukkan solusi lengkap yang dapat dijalankan. Anda akan melihat secara tepat cara memuat file sumber, mendefinisikan rentang yang berisi pivot, menyalin baris (termasuk definisi pivot), dan menyimpan hasilnya. Baik Anda mengotomatisasi pipeline pelaporan maupun membangun alat migrasi, langkah‑langkah di bawah ini memungkinkan Anda menduplikasi tabel pivot hanya dengan beberapa baris C#.

Menyalin tabel pivot lebih dari sekadar menyalin nilai sel; cache dan pengaturan bidang yang mendasarinya harus ikut dipindahkan. Contoh ini menggunakan pustaka **Aspose.Cells** karena secara otomatis menangani metadata pivot, sehingga Anda tidak perlu membangun ulang cache secara manual. Pada akhir panduan ini Anda akan dapat **cara menyalin pivot**, **menyalin rentang excel**, dan **cara menyalin baris** dengan aman.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru terpasang (kode ini juga berfungsi dengan .NET Framework 4.7+).
- Lisensi Aspose.Cells for .NET yang valid atau lisensi evaluasi sementara.
- Dua file Excel: `Source.xlsx` yang berisi tabel pivot yang ingin Anda duplikat, dan folder kosong tempat `CopyWithPivot.xlsx` akan disimpan.
- Visual Studio 2022 (atau IDE apa pun yang mendukung C#).

## Langkah 1: Siapkan proyek dan tambahkan Aspose.Cells

Buat proyek konsol baru dan tambahkan paket NuGet Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Paket ini menyediakan kelas `Workbook`, `Worksheet`, dan `CellArea` yang digunakan dalam kode di bawah.

## Langkah 2: Muat workbook sumber yang berisi tabel pivot

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Mengapa ini penting:** Memuat workbook membuat representasi dalam memori dari semua lembar kerja, termasuk cache pivot yang tersembunyi. Tanpa memuat file, Anda tidak dapat merujuk ke rentang pivot.

## Langkah 3: Definisikan area sel yang mencakup tabel pivot

Anda harus memberi tahu Aspose.Cells baris dan kolom mana yang termasuk dalam pivot. Struktur `CellArea` memungkinkan Anda menentukan blok persegi panjang.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Tip:** Jika Anda tidak yakin tentang ukuran tepatnya, buka file sumber di Excel, pilih pivot, dan catat rentang yang ditampilkan di Name Box (misalnya `A1:K31`). Konversikan koordinat Excel ke indeks berbasis nol untuk kode.

## Langkah 4: Buat workbook tujuan baru dan dapatkan lembar kerja pertamanya

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Mengapa langkah ini diperlukan:** Workbook tujuan harus ada sebelum Anda dapat menyalin baris. Aspose.Cells secara otomatis membuat lembar kerja default, yang akan kita gunakan sebagai target.

## Langkah 5: Salin baris (termasuk tabel pivot) dari sumber ke tujuan

Metode `CopyRows` menyalin nilai sel serta cache pivot yang mendasarinya.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Cara kerjanya:**  
> - `CopyRows` menerima lembar kerja sumber, baris awal, dan jumlah baris yang akan disalin.  
> - Ia juga menerima lembar kerja tujuan dan baris tempat penyalinan harus dimulai.  
> - Karena rentang sumber mencakup tabel pivot, metode ini mentransfer cache pivot, daftar bidang, dan tata letak secara utuh. Inilah inti **cara menyalin pivot** tanpa kehilangan fungsionalitas.

### Kasus khusus: menyalin pivot yang melintasi beberapa lembar kerja

Jika data sumber pivot berada di lembar lain selain lembar tempat pivot berada, cache tetap ikut disalin karena Aspose.Cells menyimpan cache di dalam workbook, bukan di lembar. Namun, Anda harus memastikan workbook tujuan berisi rentang data sumber yang sama; jika tidak, pivot akan menampilkan error `#REF!`. Dalam kasus seperti itu, salin dulu rentang data sumber, kemudian salin baris pivot.

## Langkah 6: Simpan workbook yang kini berisi tabel pivot yang disalin

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Menjalankan program menghasilkan `CopyWithPivot.xlsx` dengan replika persis tabel pivot asli, termasuk semua slicer, filter, dan field terhitung.

### Output yang diharapkan

Saat Anda membuka `CopyWithPivot.xlsx`:

- Tabel pivot muncul di posisi yang sama (misalnya A1:K31) seperti di `Source.xlsx`.
- Semua label baris dan kolom, total, serta pemformatan tetap terjaga.
- Memperbarui pivot menampilkan data yang sama dengan sumber, menegaskan bahwa cache telah disalin dengan benar.

## Cara menyalin baris tanpa pivot (menyalin rentang excel)

Jika Anda hanya perlu **menyalin rentang excel** tanpa data pivot, Anda dapat menggunakan metode `CopyRows` yang sama tetapi mengarah ke rentang yang tidak mengandung pivot. Contohnya:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Ini memperlihatkan **cara menyalin baris** untuk data umum, menegaskan fleksibilitas API yang sama.

## Duplikat tabel pivot dalam workbook yang sama (pendekatan alternatif)

Kadang Anda ingin **menduplikasi tabel pivot** di dalam workbook yang sama alih‑alih membuat file baru. Anda dapat melakukannya dengan menyalin baris ke lokasi lain:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Setelah disimpan, workbook akan berisi dua pivot yang identik—berguna untuk perbandingan berdampingan atau membuat salinan cadangan.

## Kesalahan umum dan cara menghindarinya

| Kesalahan | Mengapa terjadi | Solusi |
|-----------|----------------|--------|
| Pivot menampilkan `#REF!` setelah disalin | Rentang data sumber tidak ada di workbook tujuan | Salin dulu rentang data sumber, atau gunakan `CopyRows` pada lembar data sumber sebelum menyalin pivot |
| Pemformatan hilang | Hanya nilai yang disalin (misalnya menggunakan `Copy` alih‑alih `CopyRows`) | Selalu gunakan `CopyRows` yang mempertahankan gaya, pemformatan, dan metadata pivot |
| Offset baris tak terduga | Baris mulai tujuan tidak cocok dengan baris mulai sumber | Pastikan baris mulai `destWorksheet.Cells` sesuai dengan lokasi yang diinginkan |
| Workbook besar menyebabkan tekanan memori | `CopyRows` memuat seluruh lembar kerja ke memori | Proses penyalinan dalam potongan atau gunakan API streaming bila bekerja dengan >100.000 baris |

## Contoh lengkap yang dapat dijalankan

Berikut program lengkap yang dapat Anda tempel ke `Program.cs` dan jalankan langsung (ganti `YOUR_DIRECTORY` dengan path aktual di mesin Anda).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Jalankan program dengan `dotnet run`. Setelah eksekusi, buka `CopyWithPivot.xlsx` untuk memverifikasi bahwa tabel pivot muncul persis seperti di file sumber.

## Kesimpulan

Anda kini tahu cara **menyalin tabel pivot** dari satu workbook Excel ke workbook lain menggunakan C# dan Aspose.Cells. Panduan ini mencakup alur kerja lengkap—dari memuat file sumber, mendefinisikan area sel pivot, menyalin baris, hingga menyimpan workbook tujuan. Anda juga telah mempelajari **cara menyalin baris**, **menyalin rentang excel**, dan **duplikat tabel pivot** dalam file yang sama, serta kesalahan umum dan tip praktik terbaik.

Siap untuk langkah berikutnya? Cobalah menambahkan kode untuk memperbarui pivot yang disalin secara programatis, atau jelajahi mengekspor pivot ke PDF dengan Aspose.Cells. Bereksperimenlah dengan berbagai rentang sumber, dan Anda akan cepat menguasai otomasi Excel di .NET.

---


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}