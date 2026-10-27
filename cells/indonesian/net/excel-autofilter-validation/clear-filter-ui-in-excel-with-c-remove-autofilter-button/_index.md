---
category: general
date: 2026-02-09
description: Bersihkan UI filter di Excel dengan C# dengan menghapus tombol AutoFilter.
  Pelajari cara menyembunyikan tombol filter, menampilkan baris header, dan menjaga
  lembar kerja Anda tetap rapi.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: id
og_description: Bersihkan UI filter di Excel menggunakan C#. Panduan ini menunjukkan
  cara menyembunyikan tombol filter, menampilkan baris header, dan menjaga lembar
  kerja tetap bersih.
og_title: Bersihkan UI Filter di Excel dengan C# – Hapus Tombol AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Bersihkan UI filter di Excel dengan C# – Hapus Tombol AutoFilter
url: /id/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Antarmuka Filter Bersih di Excel dengan C# – Menghapus Tombol AutoFilter

Pernah perlu **menghapus antarmuka filter** di lembar Excel tetapi tidak yakin baris kode mana yang sebenarnya menyembunyikan panah drop‑down kecil itu? Anda bukan satu‑satunya. Tombol filter dapat mengganggu ketika Anda mengirim laporan ke pengguna akhir yang tidak pernah perlu mengubah tampilan.  

Dalam tutorial ini kita akan membahas contoh lengkap yang dapat dijalankan yang **menghapus tombol AutoFilter** dari sebuah tabel, memastikan baris header tetap terlihat, dan bahkan menyentuh cara *menyembunyikan tombol filter* secara permanen. Pada akhir tutorial Anda akan tahu persis **cara menghapus AutoFilter** di C# dan mengapa setiap langkah penting.

## Apa yang Anda Butuhkan

- .NET 6+ (atau .NET Framework 4.7.2+) – runtime terbaru apa saja dapat digunakan.  
- Paket NuGet **EPPlus** (versi 6.x atau lebih baru) – menyediakan `ExcelWorksheet`, `ExcelTable`, dll.  
- Sebuah file Excel sederhana dengan tabel bernama **SalesTable** (buat saja dalam beberapa klik).

Itu saja. Tanpa COM interop, tanpa DLL tambahan, hanya beberapa pernyataan `using` dan beberapa baris kode.

## Antarmuka Filter Bersih: Menghapus Tombol AutoFilter

Inti solusi terletak pada tiga pernyataan kecil. Mari kita uraikan agar Anda mengerti *mengapa* mereka diperlukan, bukan hanya *apa* yang mereka lakukan.

### Langkah 1 – Dapatkan referensi ke tabel

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Mengapa ini penting: EPPlus bekerja dengan **tabel** (`ExcelTable`), bukan rentang mentah. Dengan mengambil objek tabel kita memperoleh akses ke properti `AutoFilter`, yang mengontrol elemen UI yang Anda lihat di lembar. Jika Anda mencoba memanipulasi worksheet secara langsung, Anda hanya akan memengaruhi nilai, bukan tombol filter.

### Langkah 2 – Hapus baris tombol AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Menetapkan `AutoFilter` ke `null` memberi tahu EPPlus untuk menghapus baris filter yang mendasarinya. Ini adalah operasi *clear filter UI* yang paling banyak dicari developer ketika mereka bertanya “**how to remove autofilter**”. Ini adalah pendekatan satu baris yang bersih dan bekerja pada semua versi Excel yang didukung EPPlus.

### Langkah 3 – Pastikan baris header tetap terlihat

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Saat Anda menghilangkan UI filter, Excel kadang‑kadang menyembunyikan baris header jika flag `ShowHeader` tabel bernilai false. Dengan secara eksplisit menetapkannya ke `true` kita menjamin judul kolom tetap di layar – detail halus namun penting untuk laporan akhir yang rapi.

### Contoh lengkap yang dapat dijalankan

Berikut adalah aplikasi console minimal yang membuka workbook yang ada, melakukan tiga langkah tersebut, dan menyimpan hasilnya. Salin‑tempel, tekan **F5**, dan saksikan tombol filter menghilang.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Hasil yang diharapkan:** Buka *SalesReport_NoFilter.xlsx* – panah filter sudah tidak ada, tetapi judul kolom tetap ada. Tidak ada lagi UI “klik‑untuk‑filter” yang mengganggu.

> **Pro tip:** Jika Anda memiliki **banyak tabel** dan ingin menyembunyikan tombol filter untuk semuanya, lakukan loop melalui `worksheet.Tables` dan terapkan tiga baris yang sama di dalam loop.

## Cara menghapus AutoFilter di Excel menggunakan C# – penjelasan mendalam

Anda mungkin bertanya, “Bagaimana jika workbook sudah memiliki filter yang diterapkan? Apakah menetapkan `AutoFilter = null` juga menghapus baris yang terfilter?” Jawabannya **ya**. EPPlus menghapus baik UI maupun kriteria filter yang mendasarinya, sehingga data kembali ke urutan semula.  

Jika Anda hanya ingin *menyembunyikan* tombol tetapi tetap menjaga filter aktif, Anda dapat menetapkan properti `AutoFilter` ke **filter kosong baru**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Variasi ini berguna ketika Anda ingin *hide filter button* untuk tampilan yang lebih bersih tetapi tetap memberi pengguna tingkat lanjut kemampuan mengaktifkan filter melalui VBA atau ribbon.

### Kasus khusus: Tabel tanpa baris header

Beberapa laporan lama menggunakan rentang biasa alih‑alih tabel. Dalam skenario itu, EPPlus tidak akan menampilkan objek `ExcelTable`, sehingga kode di atas akan melempar error. Solusinya adalah **mengonversi rentang menjadi tabel** terlebih dahulu:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Sekarang Anda telah *removed autofilter excel* style UI bahkan pada rentang yang awalnya bukan tabel formal.

## Menampilkan baris header setelah menyembunyikan tombol filter – mengapa penting

Keluhan umum adalah setelah Anda menyembunyikan UI filter, baris header kadang menghilang, terutama bila workbook awalnya dibuat dengan “Hide Header” aktif. Dengan secara eksplisit menetapkan `salesTable.ShowHeader = true;` kita menghindari kejutan tersebut.  

Jika Anda ingin **hide filter button** tetapi tetap menyembunyikan header (misalnya saat menghasilkan dump data mentah), cukup tetapkan `salesTable.ShowHeader = false;` setelah menghapus filter. Kode ini simetris, sehingga mudah di‑toggle berdasarkan flag konfigurasi.

## Hide filter button – tips praktis dan jebakan

- **Kompatibilitas versi:** EPPlus 6+ hanya bekerja dengan file `.xlsx`. Jika Anda berurusan dengan format lama `.xls`, Anda memerlukan library lain (misalnya NPOI) karena API *clear filter UI* tidak tersedia.  
- **Kinerja:** Membuka workbook besar hanya untuk menyembunyikan satu tombol dapat lambat. Pertimbangkan menggunakan `ExcelPackage.Load(stream, true)` untuk membuka dalam mode **read‑only**, terapkan perubahan, lalu simpan.  
- **Pengujian:** Selalu validasi file output secara manual pertama kali. Tes UI otomatis dapat memverifikasi bahwa panah filter memang hilang (`worksheet.Tables[0].AutoFilter == null`).  
- **Lisensi:** EPPlus beralih ke lisensi ganda pada versi 5. Untuk proyek komersial Anda memerlukan lisensi berbayar atau beralih ke library alternatif.

## File sumber lengkap untuk copy‑paste

Berikut adalah file persis yang dapat Anda masukkan ke proyek console baru. Tanpa dependensi tersembunyi, semuanya self‑contained.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Jalankan `dotnet add package EPPlus --version 6.0.8` (atau versi terbaru) sebelum membangun, dan Anda akan memiliki lembar bersih siap didistribusikan.

## Kesimpulan

Kami baru saja menunjukkan **cara menghapus AutoFilter** dan **clear filter UI** di workbook Excel menggunakan C#. Inti tiga baris (`AutoFilter = null;`, `ShowHeader = true;`) melakukan pekerjaan utama, sementara boilerplate di sekitarnya membuat solusi

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}