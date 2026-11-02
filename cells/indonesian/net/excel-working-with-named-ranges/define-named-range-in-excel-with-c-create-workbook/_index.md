---
category: general
date: 2026-08-07
description: Definisikan rentang bernama di Excel dengan C# dan pelajari cara menambahkan
  tabel ke lembar kerja, lalu simpan buku kerja ke file secara programatis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: id
lastmod: 2026-08-07
og_description: Definisikan rentang bernama di Excel dengan C# dan lihat cara menambahkan
  tabel, membuat workbook secara programatik, serta menyimpan workbook ke file dalam
  satu alur.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Mendefinisikan rentang bernama di Excel dengan C# – tutorial lengkap buku
  kerja
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Mendefinisikan rentang bernama di Excel dengan C# – membuat workbook
url: /id/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Define named range in Excel with C# – create workbook

Jika Anda perlu **mendefinisikan named range di Excel** dari kode C#, tutorial ini menunjukkan secara tepat cara melakukannya. Anda juga akan melihat cara **menambahkan tabel ke worksheet**, membuat workbook **secara programatis**, dan akhirnya **menyimpan workbook ke file** tanpa meninggalkan IDE.

Bekerja dengan file Excel secara programatis menghemat waktu, menghilangkan kesalahan manual, dan memungkinkan pipeline pelaporan otomatis. Dalam panduan ini Anda akan:

* Membuat workbook Excel baru dari awal.  
* Menambahkan tabel yang mencakup rentang sel tertentu.  
* Mendefinisikan named range dan menangani konflik penamaan.  
* Menyimpan workbook ke disk.

Semua langkah menggunakan pustaka **Aspose.Cells for .NET**, yang bekerja dengan .NET 6+ dan .NET Framework 4.6+. Tidak diperlukan interop COM tambahan atau instalasi Office.

## Prerequisites

* .NET 6 SDK (atau .NET Framework 4.6+).  
* Visual Studio 2022 atau IDE kompatibel C# lainnya.  
* Paket NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **Pro tip:** Gunakan lisensi evaluasi gratis saat pengujian; ganti dengan lisensi produksi sebelum deployment.

## Step 1: Create Excel workbook programmatically

Operasi pertama adalah menginstansiasi objek `Workbook`. Objek ini mewakili seluruh file Excel di memori.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Why this matters*: Membuat workbook dalam kode memberi Anda kontrol penuh atas sheet, style, dan data sebelum file apa pun menyentuh disk.

## Step 2: Add table to worksheet

Sebuah tabel (juga dikenal sebagai ListObject) menyediakan penyaringan, pengurutan, dan styling bawaan. Di sini kita membuat tabel yang mencakup sel **A1:B5** dan memberi nama **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Why this matters*: Menambahkan tabel di awal memungkinkan Anda merujuk data nanti dengan **named range**, dan referensi terstruktur tabel dapat digunakan dalam rumus.

## Step 3: Define named range excel – handle conflicts

Sebuah **named range** adalah identifier yang menunjuk ke sel atau rentang, membuat rumus lebih mudah dibaca. Jika sebuah nama sudah ada (misalnya, nama tabel **SalesData**), Excel akan menimbulkan konflik. Kode di bawah ini menunjukkan cara menangkap pengecualian tersebut dan melanjutkan dengan aman.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Why this matters*: Menangani tabrakan nama mencegah crash runtime pada pekerjaan otomatis. Named range kedua **SalesTotal** mendemonstrasikan referensi kolom tabel dalam sebuah rumus.

## Step 4: Save workbook to file

Setelah semua modifikasi, simpan workbook ke disk. Metode `Save` mendukung banyak format; di sini kami menggunakan default `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Why this matters*: Menggunakan **save workbook to file** secara programatis memungkinkan pemrosesan batch, pembuatan laporan terjadwal, dan integrasi dengan web API.

## Full source code in one view

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Expected result

* Sebuah file Excel bernama **NameConflictHandled.xlsx** muncul di `C:\Temp`.  
* Sheet 1 berisi tabel terformat **SalesData** dengan baris produk‑unit.  
* Sel **B6** menampilkan jumlah kolom **Units**, dihitung melalui named range **SalesTotal**.  
* Konsol mencetak pesan tentang konflik nama (jika ada) dan mengonfirmasi lokasi file.

## Common questions & edge cases

| Question | Answer |
|----------|--------|
| **Can I define a named range that spans multiple worksheets?** | Yes. Use `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` and reference it from any sheet. |
| **What if I need to overwrite an existing file?** | Call `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **How do I add a named range without a conflict when the name already exists?** | Use `worksheet.Names.Remove("ExistingName")` before adding the new one, or generate a unique identifier (e.g., `Guid.NewGuid().ToString("N")`). |
| **Is there a way to apply a style to the table automatically?** | Set `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` after creating the table. |
| **Does this work on .NET Core?** | Aspose.Cells supports .NET Core, .NET 5/6/7, and .NET Framework. Just reference the same NuGet package. |

## Conclusion

Anda kini tahu cara **mendefinisikan named range di Excel** menggunakan C#, **menambahkan tabel ke worksheet**, dan **menyimpan workbook ke file** secara programatis. Contoh lengkap menunjukkan cara membuat workbook Excel dari nol, menangani konflik penamaan, dan menghasilkan file laporan yang dapat digunakan dalam alur kerja yang dapat diulang.

Selanjutnya, jelajahi topik terkait seperti **menambahkan chart ke worksheet**, **mengekspor ke PDF**, atau **membaca workbook yang ada**. Masing‑masing membangun di atas dasar yang sama yang dibahas di sini, sehingga Anda siap memperluas solusi ke skenario otomasi yang lebih kompleks. Selamat coding!


## What Should You Learn Next?


Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create Named Range of Cells in Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}