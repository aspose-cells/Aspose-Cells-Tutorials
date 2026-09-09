---
category: general
date: 2026-02-09
description: Cara membuat workbook di C# dengan latar belakang biru muda dan mengimpor
  data dengan header. Pelajari cara menambahkan latar belakang biru muda, menggunakan
  gaya default Excel, dan mengimpor DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: id
og_description: Cara membuat workbook di C# dengan latar belakang biru muda, mengimpor
  data dengan header, dan menerapkan gaya default Excel—semua dalam satu panduan singkat.
og_title: Cara Membuat Workbook – Latar Belakang Biru Muda, Impor Data
tags:
- C#
- Excel
- Aspose.Cells
title: Cara Membuat Workbook – Latar Belakang Biru Muda, Impor Data
url: /id/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Workbook – Latar Belakang Biru Muda, Impor Data

Pernah bertanya‑tanya **how to create workbook** di C# yang terlihat sedikit lebih cantik langsung dari awal? Mungkin Anda telah mengambil `DataTable` dari basis data dan bosan dengan sel putih default yang membosankan. Dalam tutorial ini kami akan menjelaskan cara membuat workbook baru, menambahkan latar belakang biru‑muda pada sebuah kolom, dan mengimpor data dengan header—semua sambil menggunakan gaya default yang disediakan Excel.

Kami juga akan menambahkan beberapa skenario “bagaimana‑jika”, seperti menangani nilai null atau menyesuaikan lebih dari satu kolom. Pada akhir tutorial, Anda akan memiliki file Excel yang sudah bergaya lengkap dan siap dikirim ke pemangku kepentingan tanpa proses pasca‑pengolahan.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* **.NET 6+** (kode ini juga berfungsi pada .NET Framework 4.6+)
* **Aspose.Cells for .NET** – pustaka yang menyediakan fungsi `Workbook`, `Style`, dan `ImportDataTable`. Instal melalui NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Sumber `DataTable` – kami akan membuat contoh palsu di sini, tetapi Anda dapat menggantinya dengan kueri ADO.NET apa pun.

Sudah siap? Bagus, mari kita mulai.

## Langkah 1: Inisialisasi Workbook Baru (Kata Kunci Utama)

Hal pertama yang harus Anda lakukan adalah **how to create workbook** – secara harfiah. Kelas `Workbook` mewakili seluruh file Excel, dan konstruktor‑nya memberi Anda kanvas bersih.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Mengapa ini penting:** Memulai dengan `Workbook` yang baru memastikan Anda mengontrol setiap gaya sejak awal. Jika Anda membuka file yang sudah ada, Anda akan mewarisi gaya apa pun yang ditinggalkan oleh pembuat aslinya, yang dapat menyebabkan format tidak konsisten.

## Langkah 2: Siapkan DataTable yang Akan Diimpor

Untuk tujuan ilustrasi, mari buat `DataTable` sederhana. Pada skenario dunia nyata, Anda mungkin akan memanggil prosedur tersimpan atau metode ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tip:** Jika Anda perlu mempertahankan urutan kolom persis seperti di basis data, setel parameter `importColumnNames` pada `ImportDataTable` menjadi `true`. Ini memberi tahu Aspose.Cells untuk menulis header kolom secara otomatis.

## Langkah 3: Definisikan Gaya Kolom – Default + Latar Belakang Biru Muda

Sekarang kita menjawab bagian **add light blue background** dari teka‑teki. Aspose.Cells memungkinkan Anda mengirimkan array objek `Style` yang berkorespondensi dengan setiap kolom yang diimpor. Entri pertama adalah gaya untuk kolom 0, yang kedua untuk kolom 1, dan seterusnya. Jika Anda memiliki lebih sedikit gaya daripada kolom, kolom yang tersisa akan menggunakan gaya default workbook.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Mengapa hanya dua gaya?** Pada contoh kami ada empat kolom, tetapi hanya kolom kedua (Name) yang ingin kami sorot. Panjang array tidak harus sama dengan jumlah kolom; entri yang tidak ada secara otomatis mewarisi gaya default workbook.

## Langkah 4: Impor DataTable dengan Header dan Gaya

Inilah tempat kami menggabungkan **excel import datatable c#** dan **import data with headers**. Metode `ImportDataTable` melakukan pekerjaan berat: menulis nama kolom, baris‑nya, dan menerapkan array gaya yang baru saja kami buat.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Hasil yang Diharapkan

Setelah menjalankan program, `workbook` akan berisi satu lembar kerja yang terlihat seperti ini:

| **ID** | **Name** (biru‑muda) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* Kolom **Name** memiliki latar belakang biru‑muda, membuktikan bahwa array gaya berfungsi.
* Header kolom secara otomatis dihasilkan karena kami mengatur `importColumnNames` ke `true`.
* Nilai null muncul sebagai sel kosong, yang merupakan perilaku default Aspose.Cells.

## Langkah 5: Simpan Workbook (Opsional tetapi Berguna)

Anda mungkin ingin menulis file ke disk atau mengirimnya kembali ke klien web. Menyimpan sangat mudah:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** Jika Anda menargetkan versi Excel yang lebih lama, ubah `SaveFormat.Xlsx` menjadi `SaveFormat.Xls`. API akan menangani konversinya untuk Anda.

## Kasus Tepi & Variasi

### Beberapa Kolom Bergaya

Jika Anda memerlukan lebih dari satu kolom bergaya, cukup perluas array `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Sekarang baik **Name** maupun **Salary** akan berwarna biru‑muda.

### Pemformatan Bersyarat Alih‑Alih Gaya Tetap

Kadang‑kadang Anda ingin sebuah kolom berubah menjadi merah ketika nilai melebihi ambang tertentu. Di sinilah **use default style excel** bertemu dengan pemformatan bersyarat:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Mengimpor Tanpa Header

Jika sistem hilir Anda sudah menyediakan headernya sendiri, cukup beri nilai `false` pada argumen `importColumnNames`. Data akan mulai pada `A1` dan Anda dapat menulis header khusus setelahnya.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Contoh Lengkap yang Berfungsi (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}