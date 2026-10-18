---
category: general
date: 2026-07-13
description: Buat Workbook Excel di C# dan pelajari cara menambahkan rentang bernama,
  menetapkan nama ke tabel, serta menangani konflik penamaan—semua dalam satu contoh
  yang jelas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: id
lastmod: 2026-07-13
og_description: Buat Workbook Excel di C# dengan Aspose.Cells. Pelajari cara menambahkan
  rentang bernama, mengatur nama tabel, dan mengatasi konflik penamaan dalam panduan
  singkat yang dapat dijalankan.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Buat Buku Kerja Excel di C# – Tambahkan Rentang Bernama & Atur Nama Tabel
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Buat Workbook Excel di C# – Tambahkan Rentang Bernama & Atur Nama Tabel
url: /id/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel di C# – Panduan Lengkap Menambahkan Named Ranges dan Menetapkan Nama Tabel

Pernahkah Anda perlu **create Excel workbook** dari awal dan bertanya-tanya di mana menempatkan named range atau bagaimana memberi tabel identifier sendiri? Anda tidak sendirian. Dalam banyak skenario pelaporan atau ekspor data, Anda akan menemukan diri Anda mengelola ranges, tables, dan konflik penamaan sesekali.  

Dalam tutorial ini kami akan menelusuri contoh yang dapat dijalankan sepenuhnya yang **creates an Excel workbook**, **adds a named range**, dan kemudian **assigns a name to a table**—menunjukkan secara tepat apa yang harus dilakukan ketika nama‑nama bentrok. Pada akhir tutorial Anda akan memahami “bagaimana” dan “mengapa” di balik setiap langkah, plus beberapa tips untuk menjaga kode tetap bersih.

> **Quick win:** Kode ini menggunakan library **Aspose.Cells**, yang bekerja dengan .NET 6+ dan tidak memerlukan instalasi Excel di server.

---

## What You’ll Need

- **.NET 6 SDK** (atau versi .NET terbaru apa pun)  
- Paket NuGet **Aspose.Cells for .NET**  
- IDE yang memadai (Visual Studio, Rider, atau VS Code)  
- Pengetahuan dasar C#—tidak perlu hal yang rumit, cukup pernyataan `using` biasa

Jika Anda sudah memiliki semua itu, kita dapat langsung melompat ke proses **create excel workbook**.

---

## ## Membuat Workbook Excel – Ikhtisar Langkah‑per‑Langkah

Berikut adalah program lengkap yang siap disalin‑tempel. Program ini menunjukkan segala hal mulai dari pembuatan workbook hingga penanganan konflik penamaan ketika Anda mencoba **assign name to table**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Expected output** ketika Anda menjalankan program:

```
Naming conflict detected:
A name with the same text already exists.
```

Dan jika Anda membuka *DemoWorkbook.xlsx* Anda akan melihat sebuah tabel bernama **Table1** dan sebuah named range yang disebut **MyRange**—tepat seperti yang kami harapkan, tanpa bentrok.

---

## ## Add Named Range – Why It Matters

Sebuah **named range** pada dasarnya adalah alias untuk sekumpulan sel. Daripada terus‑menerus merujuk ke `A1:B5`, Anda dapat menulis `MyRange` dalam rumus, validasi data, atau bahkan dalam kode. Hal ini meningkatkan keterbacaan dan mengurangi kemungkinan bug akibat typo.

Pada cuplikan di atas kami memanggil:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- Argumen pertama adalah **name** yang akan Anda gunakan nanti.  
- Argumen kedua adalah **address** (relatif terhadap worksheet).  

Jika Anda pernah perlu **how to add range** secara dinamis, Anda dapat membangun string alamat dengan `Cell.GetRefersTo()` atau menggunakan `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Assign Name to Table – Handling Conflicts

Tabel (juga disebut *list objects*) sudah memiliki properti nama bawaan. Secara default Aspose.Cells menamainya `Table1`, `Table2`, dll. Ketika Anda mencoba memberi tabel identifier yang sama dengan named range yang sudah ada, library akan melempar exception—sama seperti yang terjadi di Excel.

Mengapa hal ini terjadi?

- Lingkup penamaan Excel bersifat **workbook‑wide** untuk baik ranges maupun tables.  
- Nama duplikat akan membuat rumus menjadi ambigu, sehingga mesin memblokirnya.

### Pro tip

Jika Anda benar‑benar perlu sebuah tabel berbagi nama logis dengan sebuah range, pertimbangkan **prefixing** salah satunya, misalnya:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Atau ubah nama range terlebih dahulu:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Kedua pendekatan tersebut menjaga ruang nama tetap rapi dan menghindari error pada runtime.

---

## ## Set Table Name – Best Practices

Saat Anda **set table name** secara programatik, perhatikan panduan berikut:

1. **Use a consistent prefix** (`tbl_`, `rng_`, dll.) – langsung memberi tahu jenis objek.  
2. **Stay within 255 characters** – batas Excel untuk nama.  
3. **Avoid spaces and special characters** – hanya huruf, angka, dan underscore yang aman.  
4. **Validate before assigning** – pemeriksaan cepat `if (!sheet.Names.Contains(name))` mencegah bentrok yang kami demonstrasikan.

Berikut metode bantu yang dapat Anda tambahkan ke proyek mana pun:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Memanggil `SafeSetTableName(sheet, table, "MyRange")` secara otomatis akan mengubah `MyRange` menjadi `MyRange_1` bila terjadi konflik, memastikan operasi **create excel workbook** tidak berhenti secara tak terduga.

---

## ## Full Working Example – Putting It All Together

Berikut versi ringkas yang dapat Anda salin langsung ke aplikasi console. Contoh ini mencakup rutinitas keamanan dan memperlihatkan alur end‑to‑end.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Menjalankan skrip ini menghasilkan `FinalDemo.xlsx` dimana tabel bernama `MyRange_1` (atau sufiks unik lainnya) dan range tetap `MyRange`. Tidak ada exception, tidak ada misteri—hanya penamaan yang bersih dan deterministik.

---

## ## Frequently Asked Questions (FAQ)

**Q: Can I add a named range that spans multiple worksheets?**  
A: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`. The `Names.Add` method accepts that format.

**Q: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?**  
A: Absolutely. You can pass a formula string instead of a static address, such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: What if I need to rename an existing table?**  
A: Just set `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}