---
category: general
date: 2026-10-26
description: Pelajari cara mengimpor DataTable ke lembar kerja Excel dengan C# dan
  Aspose.Cells, sambil mempertahankan gaya serta header hanya dalam beberapa baris
  kode.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: id
lastmod: 2026-10-26
og_description: cara mengimpor datatable ke dalam lembar kerja Excel menggunakan C#
  dan Aspose.Cells. Ikuti panduan lengkap ini untuk mempertahankan gaya, header, dan
  pemformatan.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Cara mengimpor DataTable ke lembar kerja Excel – Panduan langkah demi langkah
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Cara mengimpor DataTable ke lembar kerja Excel menggunakan C#
url: /id/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengimpor DataTable ke lembar kerja Excel menggunakan C#

Jika Anda perlu **cara mengimpor datatable** ke lembar kerja Excel, panduan ini menunjukkan langkah‑langkah tepat dalam C#. Baik Anda membangun mesin pelaporan atau mengekspor data grid, Anda akan melihat cara mempertahankan header kolom dan gaya sel dengan Aspose.Cells. Solusi ini bekerja dengan .NET 6+ dan hanya memerlukan beberapa baris kode.

Mengimpor DataTable adalah tugas umum saat bekerja dengan spreadsheet, tetapi pengembang sering lupa mengaktifkan transfer gaya atau mengatur flag header dengan benar. Dalam tutorial ini Anda akan belajar cara mengonfigurasi **ImportTableOptions**, mengaktifkan **ImportDataTableStyle**, dan memanggil `ImportDataTable` secara aman. Pada akhir tutorial Anda akan memiliki metode siap‑jalankan yang dapat Anda sisipkan ke proyek C# mana pun.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6 SDK atau yang lebih baru terpasang.
* Salinan berlisensi **Aspose.Cells for .NET** (versi trial gratis dapat digunakan untuk pengujian).
* Familiaritas dasar dengan `DataTable` dan konsep Excel.
* IDE seperti Visual Studio 2022 (editor apa pun yang mendukung C# dapat dipakai).

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Cells`.

## Langkah 1: Ambil data sumber ke dalam DataTable

Hal pertama yang Anda lakukan ketika menjawab **cara mengimpor datatable** adalah menyiapkan data. Dalam kebanyakan skenario dunia nyata `DataTable` berasal dari kueri basis data, parser CSV, atau koleksi dalam memori. Berikut contoh minimal yang membuat tabel dengan beberapa baris:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Mengapa ini penting*: Dengan membangun `DataTable` terlebih dahulu, Anda mengontrol urutan kolom, tipe data, dan nama header—semua ini akan dipertahankan ketika Anda mengimpor tabel ke lembar kerja Excel nanti.

## Langkah 2: Buat `ImportTableOptions` dan aktifkan impor gaya

Saat Anda menjawab **cara mengimpor datatable**, keputusan selanjutnya adalah apakah Anda menginginkan gaya visual (font, warna, border) yang mungkin sudah didefinisikan pada `DataTable` sumber. Aspose.Cells menyediakan kelas `ImportTableOptions` untuk kontrol yang lebih halus. Menetapkan `ImportDataTableStyle = true` menyalin informasi gaya ke lembar kerja target.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Mengapa ini penting*: Tanpa mengaktifkan `ImportDataTableStyle`, sel yang diimpor akan menggunakan gaya default lembar kerja, sehingga kehilangan pemformatan khusus yang mungkin Anda terapkan pada `DataTable`. Flag ini penting untuk ekspor yang tampak profesional.

## Langkah 3: Impor DataTable ke lembar kerja, termasuk header

Sekarang Anda memiliki semua yang diperlukan untuk menjawab **cara mengimpor datatable** ke file Excel. Anda membuat workbook, memilih lembar kerja, dan memanggil `ImportDataTable`. Argumen kedua metode (`true`) memberi tahu Aspose.Cells untuk menulis header kolom sebagai baris pertama.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Menjalankan `ExportDataTableToExcel("Employees.xlsx")` menghasilkan file `Employees.xlsx` di mana baris pertama berisi **Id**, **Name**, dan **Department**, dan setiap sel mempertahankan gaya yang didefinisikan dalam `DataTable` asli.

### Contoh lengkap yang dapat dijalankan

Berikut adalah program konsol lengkap yang berdiri sendiri dan mendemonstrasikan **cara mengimpor datatable** serta menyimpan hasilnya ke direktori saat ini. Salin‑tempel ke proyek konsol baru dan jalankan.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Output yang diharapkan**  
Saat Anda membuka `Employees.xlsx`, akan terlihat:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Semua sel mempertahankan gaya default DataTable (font, perataan). Jika Anda menerapkan gaya khusus pada `DataTable` sebelum impor, gaya tersebut akan muncul persis sama di lembar kerja karena `ImportDataTableStyle` diatur ke `true`.

## Kesulitan umum dan tip praktik terbaik

| Masalah | Mengapa terjadi | Cara menghindarinya |
|---------|----------------|--------------------|
| **Header tidak muncul** | Menetapkan `false` pada argumen kedua `ImportDataTable` melewatkan nama kolom. | Selalu gunakan `true` ketika Anda memerlukan header, atau tulis secara manual sebelum impor. |
| **Gaya tidak ditransfer** | Lupa mengaktifkan `ImportDataTableStyle`. | Set `ImportDataTableStyle = true` pada `ImportTableOptions`. |
| **Tabel besar menyebabkan lag** | Mengimpor jutaan baris tanpa paging. | Impor dalam batch atau gunakan overload `ImportDataTable` dengan parameter `startRow` untuk streaming data. |
| **Referensi lembar kerja salah** | Menggunakan `workbook.Worksheets[1]` padahal hanya ada satu sheet. | Gunakan `workbook.Worksheets[0]` atau buat sheet baru dengan `workbook.Worksheets.Add()`. |
| **Lisensi kedaluwarsa** | Versi trial Aspose.Cells menampilkan watermark setelah 30 hari. | Terapkan lisensi yang valid dengan `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Tip pro**: Jika Anda perlu menerapkan tema khusus setelah impor, panggil `ws.Cells.ApplyStyle(style)` dimana `style` adalah objek `Style` yang Anda konfigurasikan sekali dan gunakan kembali pada baris‑baris.

## Memperluas solusi

Setelah Anda memahami **cara mengimpor datatable**, Anda dapat mengeksplorasi skenario terkait:

* **Mengimpor beberapa tabel** – ulangi proses impor pada lembar kerja yang berbeda.
* **Pemformatan bersyarat** – setelah impor, tambahkan aturan dengan `ws.Cells.ApplyConditionalFormatting`.
* **Ekspor ke CSV** – gunakan `workbook.Save("file.csv", SaveFormat.Csv)` bila format teks biasa diperlukan.
* **Membaca kembali ke DataTable** – gunakan `ws.Cells.ExportDataTable` untuk memverifikasi integritas round‑trip.

Semua ekstensi ini dibangun di atas pola inti yang ditunjukkan di atas: ambil data, konfigurasikan opsi impor, dan panggil satu metode Aspose.Cells.

## Kesimpulan

Anda kini memiliki jawaban lengkap dan siap produksi untuk **cara mengimpor datatable** ke lembar kerja Excel menggunakan C#. Tutorial ini mencakup pengambilan data sumber, konfigurasi `ImportTableOptions` dengan `ImportDataTableStyle`, serta melakukan impor dengan `ImportDataTable`. Dengan mengikuti contoh kode, Anda akan secara otomatis mempertahankan header dan gaya, serta dapat menyesuaikan pola ini untuk dataset yang lebih besar, banyak sheet, atau kebutuhan pemformatan tambahan.

Siap mengotomatisasi alur kerja pelaporan Anda? Cobalah mengganti `DataTable` contoh dengan kueri basis data nyata, bereksperimen dengan gaya sel khusus, dan integrasikan metode ini ke lapisan layanan yang sudah ada. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}