---
category: general
date: 2026-10-26
description: ExportTableOptions khusus saat ExportAsStrin memungkinkan Anda mengekspor
  data Excel sebagai string di C#. Ikuti panduan langkah demi langkah untuk mengonfigurasi
  dan menjalankan ekspor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: id
lastmod: 2026-10-26
og_description: ExportTableOptions khusus ketika ExportAsStrin mengaktifkan ekspor
  Excel hanya string. Pelajari langkah‑langkah tepat untuk mengonfigurasi dan menjalankan
  ekspor di C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: ExportTableOptions Kustom saat ExportAsString – mengekspor Excel sebagai
  string di C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Opsi ExportTable Kustom saat ExportAsString untuk Excel
url: /id/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – mengekspor Excel sebagai string di C#

Jika Anda membutuhkan **Custom ExportTableOptions when ExportAsStrin** untuk mendapatkan setiap nilai sel sebagai string biasa, panduan ini menunjukkan secara tepat cara melakukannya. Baik Anda sedang membangun pipeline impor data atau membutuhkan dump CSV yang bersih, Anda akan melihat mengapa mengonfigurasi opsi seperti ini menghindari kejutan konversi tipe.

Dalam tutorial ini Anda akan belajar **cara mengekspor excel sebagai string** menggunakan library Aspose.Cells, melihat kode lengkap yang dapat dijalankan, dan memahami alasan di balik setiap pengaturan. Tidak diperlukan dokumentasi eksternal – semua yang Anda butuhkan ada di sini.

## Prasyarat

Sebelum Anda mulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru terinstal  
* Visual Studio 2022 (atau IDE apa pun yang mendukung .NET)  
* Paket Aspose.Cells for .NET (install via NuGet: `Install-Package Aspose.Cells`)  
* Sebuah workbook Excel (`sample.xlsx`) ditempatkan di folder root proyek  

Item-item ini adalah satu‑satunya dependensi; kode dapat dijalankan di Windows, Linux, atau macOS tanpa perpustakaan tambahan.

## Langkah 1: Muat workbook yang ingin Anda ekspor

Hal pertama yang Anda lakukan saat menggunakan **Custom ExportTableOptions when ExportAsStrin** adalah memperoleh objek `Worksheet` dari workbook yang sudah dimuat. Objek ini memberi Anda akses ke baris, kolom, dan API ekspor.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Mengapa ini penting:*  
`Workbook` reads the file once and keeps all formatting information in memory. By selecting a specific `Worksheet`, you limit the export scope and avoid unnecessary processing of hidden sheets.

## Langkah 2: Konfigurasikan ExportTableOptions dengan ExportAsString = true

Inti dari **Custom ExportTableOptions when ExportAsStrin** adalah objek `ExportTableOptions`. Menetapkan `ExportAsString` memaksa exporter memperlakukan setiap sel sebagai string, terlepas dari tipe data aslinya (tanggal, angka, boolean, dll.). Mengaktifkan `PreserveFormatting` menjaga gaya visual (misalnya simbol mata uang) dalam string yang dihasilkan.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Mengapa ini penting:*  
When you later call `ExportDataTable`, the library normally tries to infer the .NET type of each column. With `ExportAsString = true`, that inference step is skipped, preventing unexpected `DateTime` or `double` conversions that can break downstream CSV parsers.

## Langkah 3: Ekspor rentang ke DataTable menggunakan opsi khusus

Sekarang Anda dapat mengekspor rentang persegi panjang (baris 0‑9, kolom 0‑4) dari worksheet. Metode ini mengembalikan sebuah `DataTable` di mana setiap field adalah `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Mengapa ini penting:*  
`ExportDataTable` is the most convenient way to move Excel data into a relational structure that many .NET APIs already understand (e.g., Entity Framework, Dapper). By passing the **Custom ExportTableOptions when ExportAsStrin**, you guarantee that each `DataColumn.DataType` will be `typeof(string)`.

## Langkah 4: Verifikasi hasil – semua nilai adalah string

Sangat disarankan untuk memastikan bahwa ekspor berjalan sesuai harapan. Loop berikut mencetak setiap sel beserta tipe runtime-nya.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Expected output**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Setiap sel menampilkan `String` sebagai tipenya, mengonfirmasi bahwa **Custom ExportTableOptions when ExportAsStrin** berfungsi dengan benar.

## Langkah 5: Opsional – menulis DataTable ke CSV

Jika tujuan akhir Anda adalah file teks biasa, Anda dapat dengan mudah menyerialkan `DataTable` ke CSV:



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekspor String HTML dari Excel ke DataTable menggunakan Aspose.Cells untuk .NET: Panduan Langkah‑per‑Langkah](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Ekspor Properti Kustom Excel PDF Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Filter Muat Kustom Ekspor Excel](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}