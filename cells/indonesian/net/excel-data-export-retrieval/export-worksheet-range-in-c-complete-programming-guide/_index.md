---
category: general
date: 2026-05-04
description: Ekspor rentang lembar kerja menggunakan C# dengan format khusus. Pelajari
  cara mengekspor rentang Excel dan cara menyesuaikan ekspor sel dalam beberapa langkah
  mudah.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: id
og_description: Ekspor rentang lembar kerja dengan C#. Panduan ini menunjukkan cara
  mengekspor rentang Excel dan menyesuaikan ekspor sel dengan cepat dan andal.
og_title: Ekspor rentang lembar kerja di C# – Panduan Pemrograman Lengkap
tags:
- C#
- Excel
- Data Export
title: Ekspor rentang lembar kerja di C# – Panduan Pemrograman Lengkap
url: /id/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor rentang lembar kerja di C# – Panduan Pemrograman Lengkap

Pernahkah Anda perlu **export worksheet range** tetapi output default tidak sesuai dengan yang Anda inginkan? Anda bukan satu-satunya—banyak pengembang mengalami hal yang sama ketika mencoba mengambil sekumpulan sel ke dalam file CSV atau JSON. Kabar baiknya? Dengan beberapa baris C# Anda tidak hanya dapat **export excel range** tetapi juga **customize cell export** agar cocok dengan format downstream apa pun.

Dalam tutorial ini kami akan membahas skenario dunia nyata: mengambil sel *A1:D10* dari sebuah workbook Excel, mengubah setiap nilai menjadi string dalam tanda kurung, dan menulis hasilnya ke sebuah file. Pada akhir tutorial Anda akan benar‑benar tahu **how to export worksheet range** dengan kontrol penuh atas representasi tiap sel, serta beberapa tips untuk kasus‑kasus tepi yang mungkin Anda temui nanti.

## Apa yang Anda Butuhkan

- .NET 6 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.7+)
- Paket NuGet **GemBox.Spreadsheet** (atau perpustakaan apa pun yang menyediakan `ExportTableOptions`; API yang ditampilkan berasal dari GemBox)
- Pemahaman dasar tentang sintaks C# – tidak rumit, hanya pernyataan `using` biasa dan pembuatan objek  

Jika Anda sudah memiliki semua itu, Anda siap untuk mulai.

## Langkah 1: Siapkan Export Options – Titik Kontrol Utama  

Hal pertama yang Anda lakukan adalah membuat instance `ExportTableOptions` dan memberitahukannya untuk memperlakukan setiap sel sebagai string. Ini adalah dasar untuk **how to export excel range** sambil menjaga konsistensi tipe data.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Mengapa memaksa ekspor string?*  
Ketika Anda kemudian menyesuaikan tiap sel, Anda akan menyisipkan tanda kurung dan mungkin simbol lain. Menjaga semuanya sebagai string mencegah kejutan konversi tipe (misalnya, tanggal berubah menjadi angka serial).

## Langkah 2: Sambungkan ke Event CellExport – Menyesuaikan Setiap Sel  

Sekarang bagian yang menyenangkan: **how to customize cell export**. GemBox memicu event `CellExport` untuk setiap sel yang akan ditulis. Dengan menangani event ini Anda dapat membungkus nilai dengan tanda kurung, menambahkan prefiks, atau bahkan melewatkan sel sepenuhnya.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Pro tip:* Jika Anda hanya ingin memodifikasi sel numerik, periksa `e.Value.GetType()` sebelum menerapkan tanda kurung. Guard kecil ini dapat menyelamatkan Anda dari secara tidak sengaja merusak teks header.

## Langkah 3: Ekspor Rentang yang Diinginkan – Aksi Inti  

Dengan opsi siap, Anda memanggil `ExportTable`. Metode ini menerima workbook yang telah Anda muat, alamat rentang yang Anda inginkan, dan opsi yang baru saja Anda konfigurasikan.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

Overload yang kami gunakan menulis langsung ke file (CSV secara default). Jika Anda lebih suka string dalam memori, ganti argumen terakhir dengan `StringWriter` dan baca hasilnya setelahnya.

### Contoh Lengkap yang Berfungsi

Berikut adalah aplikasi console mandiri yang dapat Anda tempel ke proyek baru dan jalankan langsung (cukup ganti jalur file).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Output yang diharapkan (potongan CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Setiap sel dari *A1* hingga *D10* kini dibungkus dalam tanda kurung siku, persis seperti yang kami definisikan di handler `CellExport`.

## Menangani Kasus Edge Umum  

### 1. Sel Kosong  
Jika sebuah sel kosong, `e.Value` akan menjadi `null`. Mencoba memformatnya dengan interpolasi string akan menimbulkan pengecualian. Lindungi kode Anda:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Rentang Besar  
Mengekspor jutaan baris dapat melampaui batas memori. Dalam skenario tersebut, alirkan output alih‑alih memuat seluruh workbook ke memori:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Delimiter Berbeda  
CSV bukan satu‑satunya format yang mungkin Anda butuhkan. Ubah delimiter dengan menyesuaikan `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Pertanyaan yang Sering Diajukan  

**Q: Apakah ini bekerja dengan file .xlsx yang dibuat oleh Excel 365?**  
Tentu saja. GemBox membaca format OpenXML modern tanpa konfigurasi tambahan.

**Q: Bisakah saya mengekspor beberapa rentang yang tidak bersebelahan sekaligus?**  
Tidak secara langsung melalui satu panggilan `ExportTable`. Lakukan loop pada setiap string rentang (`"A1:D10"`, `"F1:H5"` dll.) dan gabungkan outputnya sendiri.

**Q: Bagaimana jika saya perlu menerapkan pemformatan berbeda per kolom?**  
Di dalam handler `CellExport` Anda memiliki akses ke `e.ColumnIndex`. Gunakan pernyataan `switch` untuk menerapkan logika khusus kolom.

## Kesimpulan  

Kami telah membahas **how to export worksheet range** dengan kontrol penuh atas tampilan tiap sel, mendemonstrasikan **how to export excel range** menggunakan `ExportTableOptions`, dan menunjukkan **how to customize cell export** melalui event `CellExport`. Solusi lengkapnya hanya beberapa lusin baris C#, namun cukup fleksibel untuk skenario produksi.

Langkah selanjutnya? Coba ganti pembungkus tanda kurung dengan format yang ramah JSON, atau bereksperimen dengan logika kondisional yang melewatkan baris tersembunyi. Anda juga dapat menjelajahi ekspor langsung ke `MemoryStream` untuk respons web‑API—tanpa file sementara.

Jika Anda telah mengikuti langkah‑langkah ini, kini Anda memiliki pola yang solid dan dapat digunakan kembali untuk mengekspor rentang lembar kerja apa pun persis seperti yang Anda perlukan. Selamat coding, dan jangan ragu meninggalkan komentar jika Anda menemui kendala!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}