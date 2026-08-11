---
category: general
date: 2026-08-11
description: Cara mengganti nama tabel di Excel dengan C# menggunakan Aspose.Cells.
  Pelajari cara membuat workbook Excel, menambahkan named range, dan menghindari konflik
  penggantian nama.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: id
lastmod: 2026-08-11
og_description: Cara mengganti nama tabel di Excel dengan C# menggunakan Aspose.Cells.
  Panduan ini menunjukkan cara membuat workbook Excel, menambahkan rentang bernama,
  dan mengganti nama tabel Excel dengan aman.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Cara mengganti nama tabel di Excel dengan C# – tutorial pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Cara mengganti nama tabel di Excel dengan C# – panduan langkah demi langkah
url: /id/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengganti nama tabel di Excel dengan C# – panduan langkah demi langkah

Jika Anda perlu **mengganti nama tabel** dalam file Excel secara programatis, tutorial ini menunjukkan pendekatan tepat menggunakan Aspose.Cells untuk .NET. Anda akan melihat cara **membuat Excel workbook**, mendefinisikan **named range**, dan mengganti nama tabel Excel yang sudah ada tanpa menyebabkan konflik nama.

Solusi ini bekerja untuk proyek .NET apa pun yang menargetkan .NET 6 atau yang lebih baru dan hanya memerlukan paket NuGet Aspose.Cells. Pada akhir panduan, Anda dapat mengganti nama tabel Excel dengan aman dan memahami mengapa konflik dapat muncul ketika nama tabel sama dengan range yang didefinisikan.

## Prasyarat

- .NET 6 SDK atau yang lebih baru terpasang  
- Visual Studio 2022 (atau IDE C# apa pun)  
- Paket Aspose.Cells untuk .NET (`dotnet add package Aspose.Cells`)  

Tidak diperlukan assembly interop Excel tambahan karena Aspose.Cells beroperasi sepenuhnya di memori.

## Gambaran Solusi

1. **Create Excel workbook** – buat instance `Workbook` dan tambahkan beberapa data contoh.  
2. **Add a named range** – gunakan `Worksheets.Names.Add` untuk membuat range bernama `MyRange`.  
3. **Create an Excel table (ListObject)** – ubah data menjadi tabel sehingga kita memiliki sesuatu untuk diganti namanya.  
4. **Rename the table** – coba set properti `Name` tabel ke identifier yang sama dengan named range.  
5. **Handle name conflicts** – tangkap exception, jelaskan mengapa terjadi, dan tunjukkan strategi mengganti nama yang aman.  

Setiap langkah dijelaskan secara detail di bawah ini.

## Langkah 1: Cara membuat Excel workbook dan mengisi data

Membuat workbook adalah dasar untuk setiap tugas otomasi Excel. Kelas `Workbook` mewakili seluruh file dalam memori.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**Why this matters:** Workbook harus berisi data sebelum Anda dapat membuat tabel. Aspose.Cells menyimpan data dalam koleksi berbasis nol, sehingga `Worksheets[0]` selalu merujuk ke lembar pertama.

## Langkah 2: Cara menambahkan named range ke worksheet

Sebuah **named range** memungkinkan Anda merujuk ke sel atau rentang tertentu dengan identifier yang mudah diingat. Menambahkan range sangat sederhana:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Why this matters:** Named range disimpan dalam koleksi nama global workbook. Jika sebuah tabel kemudian menerima nama yang sama, Aspose.Cells akan melempar `CellException` karena Excel tidak mengizinkan nama duplikat.

## Langkah 3: Cara menambahkan Excel table (ListObject)

Sebuah tabel menyediakan penanganan data terstruktur, penyaringan, dan styling. Di Aspose.Cells disebut **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**Why this matters:** Tabel kini ada dengan nama `InitialTable`. Mengganti namanya memperlihatkan proses **cara mengganti nama tabel**.

## Langkah 4: Cara mengganti nama Excel table dan menangani konflik

Mencoba mengganti nama tabel menjadi `MyRange` akan bentrok dengan named range yang kita buat sebelumnya. Kode berikut menunjukkan pola yang tepat untuk mendeteksi dan menyelesaikan konflik.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### Apa yang dilakukan kode

| Langkah | Aksi | Alasan |
|------|--------|--------|
| **Coba ganti nama** | `table.Name = "MyRange"` | Menunjukkan skenario konflik. |
| **Tangkap exception** | Prints the conflict message. | Memberikan umpan balik langsung tentang masalah tersebut. |
| **Buat nama aman** | `GetUniqueTableName` adds a numeric suffix until the name is free. | Menjamin bahwa nama tabel baru **tidak** bentrok dengan named range atau tabel yang sudah ada. |
| **Simpan workbook** | `workbook.Save("RenamedTable.xlsx")` | Menyimpan perubahan sehingga Anda dapat membuka file di Excel dan memverifikasi hasilnya. |

**Output yang diharapkan** ketika Anda menjalankan program:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Membuka `RenamedTable.xlsx` menampilkan tabel bernama `MyRange_1` dan named range terpisah `MyRange` yang mengarah ke sel A1.

## Mengapa konflik terjadi dan praktik terbaik untuk mengganti nama tabel Excel

- Excel menyimpan **named ranges** dan **table names** dalam namespace yang sama.  
- Ketika Anda mencoba menetapkan nama tabel yang sudah ada sebagai range, Aspose.Cells melempar `CellException`.  
- Pendekatan yang disarankan adalah **memeriksa keberadaan nama terlebih dahulu** (seperti yang ditunjukkan di `NameExists`) atau menggunakan konvensi penamaan yang menjamin keunikan (misalnya, menambahkan awalan `tbl_` pada tabel).  

Menerapkan pola ini mencegah error runtime dan membuat otomasi Anda lebih kuat.

## Tips tambahan untuk bekerja dengan Aspose.Cells

- **Pro tip:** Gunakan `Workbook.Worksheets.Names.Remove("MyRange")` jika Anda secara sengaja ingin mengganti range dengan nama tabel.  
- **Watch out for case sensitivity:** Excel memperlakukan nama secara tidak sensitif huruf besar/kecil; metode bantu menggunakan `OrdinalIgnoreCase` untuk meniru perilaku Excel.  
- **Performance:** Jika Anda memproses banyak worksheet, cache koleksi nama daripada iterasi berulang.

## Contoh lengkap dalam satu blok

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol. Program ini mencakup semua langkah mulai dari membuat workbook hingga mengganti nama tabel dengan aman.

```csharp
using System;
using Aspose.Cells;

class RenameTableDemo
{
    static void Main()
    {
        // Create workbook and populate data
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);

        // Add named range "MyRange" pointing to A1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");

        // Convert the data range into a table named "InitialTable"
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(0, 0, 4, 3, true)];
        table.Name = "InitialTable";

        // Attempt to rename the table to "MyRange" – this will conflict
        try
        {
            table.Name = "MyRange";
            Console


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat Workbook Scoped Named Ranges di Excel Menggunakan Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Cara Mengimplementasikan Rumus Named Range di .NET menggunakan Aspose.Cells untuk Otomasi Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Cara Menambahkan Slicer ke Tabel Excel Menggunakan Aspose.Cells untuk .NET: Panduan Komprehensif](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}