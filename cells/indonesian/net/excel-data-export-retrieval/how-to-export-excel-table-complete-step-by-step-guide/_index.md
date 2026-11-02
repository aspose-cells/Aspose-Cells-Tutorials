---
category: general
date: 2026-07-03
description: Pelajari cara mengekspor tabel Excel ke file .txt dan menyimpan tabel
  Excel ke file .txt menggunakan C#. Ekspor data Excel sebagai teks biasa dengan contoh
  kode lengkap.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: id
og_description: Cara mengekspor tabel Excel sebagai teks biasa. Panduan ini menunjukkan
  cara mengekspor data Excel sebagai teks biasa dan menyimpan tabel Excel ke file
  .txt dengan Aspose.Cells.
og_title: Cara Mengekspor Tabel Excel – Tutorial C# Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Cara Mengekspor Tabel Excel – Panduan Lengkap Langkah demi Langkah
url: /id/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Tabel Excel – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya‑tanya **cara mengekspor tabel Excel** tanpa harus memuat seluruh workbook ke memori? Anda bukan satu‑satunya. Dalam banyak pekerjaan otomatisasi sistem hilir hanya menerima file `.txt` sederhana, jadi Anda perlu **menyimpan tabel Excel ke file .txt** dengan cepat dan dapat diandalkan.  

Dalam tutorial ini kita akan membahas solusi C# yang bersih yang **mengekspor data Excel sebagai teks biasa** menggunakan Aspose.Cells. Pada akhir tutorial Anda akan memiliki program siap‑jalankan, memahami mengapa setiap baris kode penting, dan melihat cara menyesuaikan ekspor untuk kasus khusus Anda.

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (versi terbaru, misalnya 23.12).  
- .NET 6 SDK atau yang lebih baru – kode ini juga dapat dikompilasi dengan .NET Core.  
- Sebuah contoh `input.xlsx` yang berisi setidaknya satu tabel Excel.  
- Editor teks atau IDE (Visual Studio, VS Code, Rider… pilih yang Anda suka).

Tidak ada paket NuGet tambahan selain Aspose.Cells yang diperlukan, dan seluruh proses dapat dijalankan di Windows, Linux, atau macOS.

## Langkah 1: Siapkan Proyek dan Impor

Pertama, buat aplikasi console dan sertakan namespace yang diperlukan.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Pro tip:** Jika Anda menggunakan .NET CLI, jalankan `dotnet new console -n ExcelTableExport` lalu `dotnet add package Aspose.Cells` sebelum menempelkan kode di atas.

## Langkah 2: Muat Workbook dan Ambil Worksheet Pertama

Objek workbook mewakili seluruh file Excel. Memuatnya sekali saja menjaga penggunaan memori tetap rendah.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Mengapa kita memilih worksheet pertama? Pada banyak laporan yang dihasilkan secara otomatis data berada di sheet pertama, tetapi Anda dapat mengubah indeks atau menggunakan `wb.Worksheets["SheetName"]` untuk sheet yang bernama.

## Langkah 3: Ambil Tabel Pertama yang Didefinisikan pada Worksheet

Tabel Excel (ListObjects) memberi kita data terstruktur, sehingga ekspor menjadi lebih dapat diprediksi.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Jika workbook Anda berisi beberapa tabel, cukup iterasi `ws.Tables` atau pilih berdasarkan `tbl.Name`.

## Langkah 4: Konfigurasikan Opsi Ekspor – Ekspor Setiap Sel sebagai String

Aspose.Cells memungkinkan Anda mengontrol format setiap sel saat diekspor. Menetapkan `ExportAsString` memastikan angka, tanggal, dan formula menjadi teks biasa.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Menambahkan Aksi Ekspor Kustom untuk Memangkas Spasi

Seringkali data sumber mengandung spasi di awal atau akhir. Memangkasnya membuat file `.txt` akhir menjadi lebih bersih.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

Lambda menerima objek `Cell` dan `TextWriter`. Anda juga dapat menambahkan logika bersyarat di sini—misalnya, mengganti koma dengan titik koma untuk output bergaya CSV.

## Langkah 5: Ekspor Tabel Mulai dari Sel A1 ke File Teks

Sekarang kita benar‑benar menulis tabel ke disk. Metode `ExportTable` akan melintasi tabel baris‑per‑baris, menerapkan opsi yang baru saja kita definisikan.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**Apa yang akan Anda lihat:** Setiap baris tabel Excel menjadi satu baris dalam `Table.txt`. Kolom dipisahkan oleh karakter tab (`\t`) secara default—sempurna untuk parsing di sistem hilir.

### Contoh Output yang Diharapkan

Misalkan `input.xlsx` berisi tabel dengan tiga kolom (`ID`, `Name`, `Score`) dan dua baris data, maka `Table.txt` akan terlihat seperti:

```
1    Alice    85
2    Bob      92
```

Perhatikan spasi telah dipangkas, dan semuanya berupa teks biasa—tepat seperti yang diminta oleh kebutuhan **mengekspor data excel sebagai teks biasa**.

## Menangani Kasus Edge Umum

| Situasi | Apa yang Harus Dilakukan | Mengapa |
|-----------|------------|-----|
| **Tabel memiliki sel kosong** | Lambda menulis `cell.StringValue.Trim()` yang mengembalikan string kosong untuk sel kosong. | Menjaga kesejajaran kolom tanpa menambahkan karakter yang tidak diinginkan. |
| **Anda memerlukan delimiter khusus** | Ganti `writer.Write(cell.StringValue.Trim());` dengan `writer.Write($"{cell.StringValue.Trim()},");` dan pangkas delimiter akhir setelah setiap baris. | Beberapa sistem lebih menyukai koma atau pipa dibandingkan tab. |
| **Worksheet besar ( > 100 k baris )** | Gunakan `ExportTableOptions` dengan `ExportAsString = true` dan stream file seperti yang ditunjukkan; Aspose.Cells memproses baris secara streaming, menghindari error OOM. | Menjamin skalabilitas. |
| **Beberapa tabel dalam satu sheet** | Loop melalui `ws.Tables` dan panggil `ExportTable` untuk masing‑masing, opsional menambahkan baris pemisah di antara ekspor. | Memungkinkan Anda **menyimpan tabel Excel ke file .txt** untuk setiap tabel. |

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke `Program.cs`. Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif yang ada di mesin Anda.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Jalankan program dengan `dotnet run`. Jika semuanya telah disiapkan dengan benar, Anda akan melihat pesan konfirmasi dan file `Table.txt` yang baru saja dibuat berisi **mengekspor data excel sebagai teks biasa**.

## Bonus: Konfirmasi Visual (Opsional)

Jika Anda ingin melihat tangkapan layar cepat dari file yang dihasilkan, Anda dapat membukanya di editor teks apa pun. Di bawah ini adalah gambar placeholder yang menunjukkan tata letak yang diharapkan.

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*Alt text:* **how to export excel table** – menampilkan output teks biasa dari tabel Excel yang diekspor.

## Ringkasan & Langkah Selanjutnya

Kami telah membahas semua yang perlu Anda ketahui **cara mengekspor tabel Excel** menggunakan Aspose.Cells, mulai dari memuat workbook hingga memangkas nilai sel dan akhirnya menulis file `.txt` yang bersih.  

- Sekarang Anda memahami **menyimpan tabel Excel ke file .txt** dengan logika kustom.  
- Anda dapat menyesuaikan lambda untuk menangani tanggal, angka, atau delimiter khusus.  
- Untuk proyek yang lebih besar, pertimbangkan membungkus logika ke dalam metode atau kelas yang dapat digunakan kembali.

**Apa selanjutnya?** Coba ekspor beberapa tabel, atau ubah format output menjadi CSV dengan mengubah delimiter. Anda juga dapat mengeksplor **mengekspor data excel sebagai teks biasa** langsung ke stream jaringan untuk integrasi waktu nyata.

Punya pertanyaan atau mengalami kendala? Tinggalkan komentar, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}