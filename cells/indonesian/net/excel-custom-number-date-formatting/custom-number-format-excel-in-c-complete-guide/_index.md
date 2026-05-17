---
category: general
date: 2026-03-22
description: Tutorial format angka khusus di Excel yang menunjukkan cara mengimpor
  datatable ke Excel, mengatur warna latar belakang kolom, memformat kolom sebagai
  mata uang, dan menyimpan workbook sebagai xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: id
og_description: Tutorial format angka khusus di Excel yang memandu Anda melalui proses
  mengimpor DataTable, mengatur warna latar belakang kolom, memformat kolom sebagai
  mata uang, dan menyimpan workbook sebagai xlsx.
og_title: Format Angka Kustom di Excel dengan C# – Panduan Langkah demi Langkah
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Format Angka Kustom Excel di C# – Panduan Lengkap
url: /id/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Format Angka Kustom Excel – Tutorial C# Full‑Stack

Pernah bertanya-tanya bagaimana cara menerapkan gaya **custom number format excel** langsung dari C#? Mungkin Anda pernah mencoba mengekspor DataTable ke spreadsheet hanya untuk melihat angka biasa, tanpa warna, dan tanpa format mata uang. Itu adalah masalah umum—terutama ketika Anda membutuhkan laporan yang rapi untuk para pemangku kepentingan.

Dalam panduan ini kami akan menyelesaikan masalah tersebut bersama: Anda akan belajar cara **import datatable to excel**, **set column background color**, **format column as currency**, dan akhirnya **save workbook as xlsx** dengan format angka kustom yang membuat angka Anda menonjol. Tanpa referensi yang samar, hanya solusi lengkap yang dapat dijalankan yang dapat Anda salin‑tempel ke dalam proyek Anda.

---

## Apa yang Akan Anda Bangun

Pada akhir tutorial ini Anda akan memiliki aplikasi konsol C# yang berdiri sendiri yang:

1. Mengambil sebuah `DataTable` (Anda dapat mengganti stub dengan kueri Anda sendiri).  
2. Membuat workbook Excel baru menggunakan Aspose.Cells (atau perpustakaan kompatibel lainnya).  
3. Menerapkan font biru, tebal pada kolom pertama, latar belakang kuning‑muda pada kolom kedua, dan format mata uang (`$#,##0.00`) pada kolom ketiga.  
4. Menyimpan file sebagai `DataTableWithStyleArray.xlsx` di folder yang Anda pilih.

Anda akan melihat secara tepat bagaimana setiap baris berkontribusi pada file Excel akhir, dan kami akan membahas mengapa pilihan tersebut penting untuk pemeliharaan dan kinerja.

---

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.7+).  
- Aspose.Cells untuk .NET (versi percobaan gratis atau berlisensi). Instal melalui NuGet:

```bash
dotnet add package Aspose.Cells
```

- Pemahaman dasar tentang `DataTable` dan aplikasi konsol C#.

---

## Langkah 1: Ambil Data Sumber sebagai DataTable

Pertama, kita membutuhkan beberapa data untuk diekspor. Dalam skenario dunia nyata Anda mungkin akan memanggil repository atau menjalankan kueri SQL. Untuk ilustrasi kami akan membuat tabel sederhana di memori.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Mengapa ini penting:** Menggunakan `DataTable` memberi Anda sumber tabular yang sadar skema yang dapat dipetakan dengan bersih ke baris dan kolom Excel. Ini juga memungkinkan Anda menggunakan kembali logika ekspor yang sama untuk dataset apa pun tanpa menulis ulang kode.

---

## Langkah 2: Buat Workbook Baru dan Ambil Worksheet Pertama

Sekarang kami membuat workbook Excel. Kelas `Workbook` mewakili seluruh file; `Worksheets[0]`-nya adalah sheet default tempat kami akan menaruh data kami.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Jika Anda membutuhkan beberapa sheet, cukup panggil `workbook.Worksheets.Add("SheetName")` dan ulangi langkah styling untuk masing‑masing.

---

## Langkah 3: Definisikan Gaya Kolom – Font, Latar Belakang, dan Format Angka

Styling di Aspose.Cells dilakukan melalui objek `Style`. Kami akan membuat array di mana setiap elemen sesuai dengan sebuah kolom dalam DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Mengapa array gaya?** Mengirimkan array ke `ImportDataTable` memungkinkan Anda menerapkan gaya yang berbeda untuk setiap kolom dalam satu panggilan, yang sekaligus ringkas dan cepat. Ini juga menjamin bahwa pemformatan tetap sinkron dengan urutan data.

---

## Langkah 4: Impor DataTable Sambil Menerapkan Gaya

Berikut inti dari operasi: kami memasukkan `DataTable` ke dalam worksheet, memberi tahu Aspose untuk menyertakan baris header, dan menyerahkan array `columnStyles` kami.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Apa yang terjadi di balik layar?** Aspose mengiterasi setiap kolom, menulis header, lalu menulis nilai setiap baris. Selama proses itu ia menerapkan `Style` yang sesuai dari array, sehingga Anda mendapatkan header biru untuk “Product”, “Quantity” berbayang kuning, dan kolom “Revenue” yang diformat dengan baik.

---

## Langkah 5: Simpan Workbook sebagai File XLSX

Akhirnya, kami menyimpan workbook ke disk. Metode `Save` secara otomatis memilih format XLSX berdasarkan ekstensi file.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** Jika Anda perlu men‑stream file (mis., untuk API web), gunakan `workbook.Save(stream, SaveFormat.Xlsx)` alih‑alih jalur file.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda tempel ke dalam proyek konsol baru. Program ini dapat dikompilasi dan dijalankan apa adanya, menghasilkan file Excel yang bergaya.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Hasil yang Diharapkan

Saat Anda membuka `DataTableWithStyleArray.xlsx` Anda akan melihat:

| **Product** (blue, bold) | **Quantity** (light‑yellow) | **Revenue** (currency) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

Format **custom number format excel** yang Anda tentukan (`$#,##0.00`) memastikan setiap sel revenue menampilkan tanda dolar, pemisah ribuan, dan dua tempat desimal—tepat seperti yang diharapkan tim keuangan.

---

## Pertanyaan yang Sering Diajukan & Kasus Tepi

### Bisakah saya menggunakan ini dengan perpustakaan Excel yang berbeda?

Tentu saja. Konsep—membuat gaya per kolom dan menerapkannya selama impor—dapat diterapkan pada EPPlus, ClosedXML, atau NPOI. Panggilan API berbeda, tetapi pola tetap sama.

### Bagaimana jika DataTable saya memiliki lebih banyak kolom daripada gaya?

Aspose akan menerapkan gaya default pada kolom mana pun yang tidak memiliki entri yang cocok di array `columnStyles`. Untuk menghindari kejutan, ukuran array harus sama dengan `dataTable.Columns.Count` atau hasilkan gaya secara dinamis dalam loop.

### Bagaimana cara mengatur format angka kustom untuk tanggal?

Cukup set `style.Custom = "dd‑mm‑yyyy"` (atau string format Excel yang valid lainnya). Pendekatan berbasis array yang sama bekerja untuk tanggal, persentase, atau notasi ilmiah.

### Apakah ada cara untuk mengatur ukuran kolom secara otomatis setelah impor?

Ya—panggil `worksheet.AutoFitColumns();` setelah impor. Ini melakukan perhitungan lebar cepat berdasarkan isi sel.

### Bagaimana dengan set data besar (100k+ baris)?

`ImportDataTable` dioptimalkan untuk operasi bulk, tetapi Anda mungkin menemui batas memori. Dalam kasus tersebut, pertimbangkan untuk men‑stream baris secara manual dengan `Cells[i, j].PutValue(...)` dan menggunakan kembali satu objek `Style` untuk mengurangi beban.

---

## Tips Pro & Kesalahan Umum

- **Hindari hard‑coding jalur** dalam kode produksi; gunakan `Environment.GetFolderPath` atau pengaturan konfigurasi.  
- **Dispose workbook** jika Anda berada dalam layanan yang berjalan lama—bungkus dalam blok `using` untuk membebaskan sumber daya native.  
- **Waspadai pemisah spesifik budaya**. Format kustom `$#,##0.00` memaksa titik sebagai pemisah desimal terlepas dari locale OS, yang biasanya diinginkan untuk laporan keuangan.  
- **Ingat untuk mereferensikan System.Drawing** (atau `System.Drawing.Common` pada .NET Core) untuk struct warna yang digunakan dalam styling.  
- **Uji output pada versi Excel yang berbeda**; versi lama mungkin menafsirkan beberapa format kustom sedikit berbeda.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **custom number format excel** file dari C#: mengambil data dari `DataTable`, **import datatable to excel**, menerapkan **set column background color**, menggunakan **format column as currency**, dan akhirnya **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}