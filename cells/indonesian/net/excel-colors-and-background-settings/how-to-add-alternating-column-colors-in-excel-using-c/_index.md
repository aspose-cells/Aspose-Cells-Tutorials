---
category: general
date: 2026-10-01
description: warna kolom bergantian di Excel menggunakan C# – pelajari cara membuat
  file Excel dari DataTable, mengatur warna latar belakang sel dengan C#, dan mengimpor
  DataTable ke Excel dengan kolom yang bergaya.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: id
lastmod: 2026-10-01
og_description: Warna kolom bergantian di Excel menjadi mudah. Ikuti panduan ini untuk
  membuat file Excel dari DataTable, mengatur warna latar belakang sel dengan C#,
  dan mengimpor DataTable ke Excel dengan kolom yang bergaya.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Tambahkan warna kolom bergantian di Excel dengan C# – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Cara menambahkan warna kolom bergantian di Excel menggunakan C#
url: /id/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan warna kolom bergantian di Excel menggunakan C#

Jika Anda membutuhkan **alternating column colors excel** dalam laporan yang dihasilkan dari aplikasi Anda, panduan ini menunjukkan solusi lengkap. Anda akan melihat cara membuat file Excel dari `DataTable`, mengatur warna latar belakang sel dengan gaya C#, dan mengimpor datatable ke excel sambil menerapkan gaya berbeda pada setiap kolom.

Tutorial ini mencakup semua yang Anda perlukan: paket NuGet yang diperlukan, contoh kode lengkap yang dapat dijalankan, dan penjelasan mengapa setiap langkah penting. Pada akhir tutorial Anda akan memiliki workbook yang bergaya dan dapat dibuka langsung di Microsoft Excel.

## Prasyarat

Sebelum Anda mulai, pastikan Anda memiliki:

* .NET 6.0 (atau lebih baru) SDK terinstal  
* Visual Studio 2022 (atau IDE kompatibel C# lainnya)  
* Perpustakaan **Aspose.Cells for .NET** – instal dengan  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells menyediakan kelas `Workbook`, `Worksheet`, `Style`, dan `BackgroundType` yang digunakan dalam contoh.

## Langkah 1: Ambil data sumber sebagai `DataTable`

Tugas pertama adalah mendapatkan data yang ingin Anda ekspor. Dalam proyek nyata Anda mungkin mengisi `DataTable` dari kueri basis data, panggilan API, atau koleksi dalam memori apa pun.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Mengapa ini penting:**  
`DataTable` adalah wadah universal yang dapat dipetakan dengan bersih ke lembar kerja Excel. Menggunakan `DataTable` memungkinkan Anda **create excel file from datatable c#** tanpa menulis loop khusus untuk setiap kolom.

## Langkah 2: Buat workbook baru dan dapatkan lembar kerja pertamanya

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Penjelasan:**  
`Workbook` adalah objek akar; `Worksheets[0]` memberikan Anda lembar default tempat data akan ditempatkan.

## Langkah 3: Siapkan gaya berbeda untuk setiap kolom (warna latar belakang bergantian)

Untuk mencapai **alternating column colors excel**, kami membuat `Style` untuk setiap kolom dan menetapkan warna latar belakang ringan yang berganti antara dua nuansa.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Mengapa kami menggunakan loop:**  
Loop memastikan bahwa **set cell background color c#** diterapkan secara konsisten, bahkan jika jumlah kolom berubah pada waktu berjalan. Ini membuat solusi tahan terhadap laporan dinamis.

## Langkah 4: Impor `DataTable` ke dalam lembar kerja, menerapkan gaya kolom

Aspose.Cells dapat mengimpor `DataTable` secara langsung, dan kami dapat mengirimkan array gaya untuk memberi warna pada setiap kolom.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Apa yang terjadi di balik layar:**  
`ImportDataTable` menulis baris header, kemudian setiap baris data. Karena kami menyediakan `columnStyles`, setiap sel dalam kolom tertentu menerima gaya yang sesuai, memberi kami warna bergantian yang diinginkan.

## Langkah 5: Simpan workbook yang bergaya ke file

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Saat Anda membuka *StyledTable.xlsx* di Excel, Anda akan melihat setiap kolom diberi bayangan secara bergantian, membuat tabel lebih mudah dibaca.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut adalah program mandiri yang dapat Anda salin, tempel, dan jalankan.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Output yang diharapkan

* Sebuah file bernama **StyledTable.xlsx** yang terletak di `C:\Temp\`.
* Lembar kerja menampilkan tiga kolom (`Id`, `Name`, `Score`) dengan warna latar belakang bergantian: kolom 1 dan 3 berwarna *LightYellow*, kolom 2 berwarna *LightCyan*.
* Semua baris dari `DataTable` muncul di bawah baris header.

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| *Apakah saya dapat menggunakan warna lain?* | Ya. Ganti `System.Drawing.Color.LightYellow` dan `LightCyan` dengan nilai `System.Drawing.Color` apa pun. |
| *Bagaimana jika DataTable memiliki banyak kolom?* | Loop secara otomatis membuat gaya untuk setiap kolom, sehingga pola dapat diskalakan tanpa perubahan kode. |
| *Apakah saya perlu membuang (dispose) workbook?* | Aspose.Cells mengimplementasikan `IDisposable`. Jika Anda membungkus `Workbook` dalam blok `using`, sumber daya akan segera dibebaskan. |
| *Bagaimana menerapkan warna bergantian yang sama pada baris alih-alih kolom?* | Buat `Style[]` untuk baris dan panggil `worksheet.Cells.ImportDataTable(..., rowStyles)` – overload Aspose.Cells mendukung keduanya. |
| *Apakah saya dapat menulis file langsung ke stream (misalnya, untuk web API)?* | Ya. Gunakan `workbook.Save(stream, SaveFormat.Xlsx);` alih-alih jalur file. |

## Tips dari lapangan

* **Pro tip:** Cache objek gaya jika Anda menghasilkan banyak lembar kerja dalam satu kali jalan – membuat gaya relatif murah, tetapi menggunakan kembali mengurangi beban memori.  
* **Watch out for:** Saat menggunakan `System.Drawing.Color` pada platform non‑Windows, tambahkan paket NuGet `System.Drawing.Common` dan pastikan runtime mendukung GDI+.

## Kesimpulan

Anda sekarang tahu cara **alternating column colors excel** dengan membuat file Excel dari `DataTable` di C#, mengatur warna latar belakang sel dengan Aspose.Cells, dan **import datatable to excel** dengan array kolom yang bergaya. Pendekatan ini cepat, mudah dipelihara, dan bekerja dengan ukuran data apa pun.

### Langkah selanjutnya

* Jelajahi **set cell background color c#** untuk pemformatan bersyarat (mis., menyorot skor rendah).  
* Gabungkan teknik ini dengan **create excel file from datatable c#** untuk menghasilkan laporan multi‑sheet.  
* Pelajari API charting Aspose.Cells untuk menambahkan ringkasan visual ke workbook yang sama.

Silakan sesuaikan warna, format file, atau sumber data agar sesuai dengan kebutuhan proyek Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Set Kolom Latar Belakang di Excel dengan C# – Panduan Lengkap](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Tambah warna latar belakang excel – Gaya Baris Bergantian di C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Buat Workbook C# – Impor DataTable ke Excel dengan Gaya](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}