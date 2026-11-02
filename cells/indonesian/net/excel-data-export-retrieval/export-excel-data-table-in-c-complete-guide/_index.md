---
category: general
date: 2026-03-21
description: Ekspor tabel data Excel ke DataTable dengan header, batasi jumlah desimal,
  dan ekspor 100 baris pertama menggunakan Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: id
og_description: Pelajari cara mengekspor tabel data Excel ke DataTable, mempertahankan
  header, membatasi angka desimal, dan mengambil 100 baris pertama dalam C#.
og_title: Ekspor Tabel Data Excel di C# – Panduan Langkah demi Langkah
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Mengekspor Tabel Data Excel di C# – Panduan Lengkap
url: /id/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Tabel Data Excel – Panduan Lengkap C#

Perlu **mengekspor tabel data excel** dari sebuah workbook ke dalam .NET `DataTable`? Anda berada di tempat yang tepat—panduan ini menunjukkan secara tepat cara melakukannya, mempertahankan header kolom, membatasi angka desimal, dan mengambil hanya 100 baris pertama.  

Jika Anda pernah menatap spreadsheet dan berpikir, “Bagaimana cara memasukkan ini ke dalam aplikasi saya tanpa kehilangan format?” Anda tidak sendirian. Dalam beberapa menit ke depan kami akan mengubah “bagaimana jika” itu menjadi solusi konkret yang dapat disalin‑tempel dan bekerja dengan Aspose.Cells, sebuah perpustakaan populer untuk manipulasi Excel.

## Apa yang Akan Anda Pelajari

- Cara **mengekspor excel ke datatable** menggunakan metode `ExportDataTable`.  
- Cara mempertahankan nama kolom asli (`export excel with headers`).  
- Cara **membatasi angka desimal excel** dengan mengonfigurasi `ExportTableOptions`.  
- Cara mengambil dengan aman hanya 100 baris teratas (`export first 100 rows`).  

Tanpa skrip eksternal, tanpa string ajaib—hanya C# biasa yang dapat Anda sisipkan ke proyek .NET mana pun.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6 atau lebih baru (atau .NET Framework 4.7+) | Aspose.Cells mendukung keduanya, tetapi runtime yang lebih baru memberikan API yang siap async. |
| Paket NuGet Aspose.Cells untuk .NET | Menyediakan `Workbook`, `ExportTableOptions`, dan helper `ExportDataTable`. |
| File Excel contoh (misalnya `Numbers.xlsx`) | Sumber data yang akan Anda ekspor. |
| Pengetahuan dasar C# | Anda akan mengikuti contoh kode, namun tidak memerlukan hal yang rumit. |

Jika ada yang belum familiar, dapatkan paket NuGet dengan `dotnet add package Aspose.Cells` dan buat file Excel kecil dengan beberapa angka—data uji Anda.

![contoh mengekspor tabel data excel](excel-data-table.png "Tangkapan layar lembar Excel yang akan diekspor ke DataTable")

## Langkah 1: Muat Workbook (export excel data table)

Hal pertama yang Anda butuhkan adalah instance `Workbook` yang menunjuk ke file Excel Anda. Anggaplah ini seperti membuka buku sebelum Anda dapat membaca bab apa pun.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Mengapa ini penting:** Memuat workbook memberi Anda akses ke lembar kerja, sel, dan gaya di dalamnya. Jika jalur file salah, Aspose akan melempar `FileNotFoundException`, jadi periksa kembali lokasinya.

## Langkah 2: Konfigurasi Opsi Ekspor – limit decimal places excel

Secara default Aspose mengekspor setiap nilai numerik dengan presisi penuh. Seringkali Anda hanya membutuhkan beberapa digit signifikan, terutama saat memasukkan data ke dalam grid UI atau API yang mengharapkan angka yang dibulatkan.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Pro tip:** Jika Anda memerlukan strategi pembulatan yang berbeda (misalnya selalu membulatkan ke atas), Anda dapat memproses `DataTable` setelah ekspor. Pengaturan `SignificantDigits` adalah cara tercepat untuk **membatasi angka desimal excel** tanpa menulis loop tambahan.

## Langkah 3: Ekspor Rentang yang Diinginkan (export first 100 rows)

Sekarang kami memberi tahu Aspose blok sel mana yang ingin kami tarik ke dalam `DataTable`. Dalam tutorial ini kami mengambil 100 baris pertama dan 10 kolom pertama, tetapi Anda dapat menyesuaikan angka-angka tersebut sesuai skenario Anda.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Edge case:** Jika lembar berisi kurang dari 100 baris, Aspose akan mengekspor apa yang ada tanpa melempar error. Namun, Anda mungkin ingin melindungi diri dari rentang yang secara tak terduga terlalu kecil:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Langkah 4: Verifikasi Hasil – Dump Cepat ke Konsol

Melihat data di debugger memang menyenangkan, tetapi mencetak beberapa baris ke konsol memastikan bahwa **export excel to datatable** benar‑benar berhasil dan bahwa angka desimal telah dipangkas.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Output yang Diharapkan

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Perhatikan bagaimana kolom numerik kini hanya menampilkan empat digit signifikan, sesuai dengan pengaturan `SignificantDigits = 4` yang kami terapkan sebelumnya.

## Langkah 5: Menyelesaikan – Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini mencakup penanganan error, guard opsional untuk jumlah baris, dan metode bantu untuk mencetak.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Jalankan program, dan Anda akan melihat 100 baris pertama dari lembar Anda, dibulatkan dengan rapi, dengan nama kolom tetap utuh.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika lembar saya memiliki sel yang digabung?** | `ExportDataTable` meratakan sel yang digabung dengan mengambil nilai sel paling kiri‑atas. Jika Anda memerlukan penanganan khusus, lepaskan penggabungan terlebih dahulu atau baca objek `Cell` mentah. |
| **Bisakah saya mengekspor ke `DataSet` instead?** | Ya—gunakan `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}