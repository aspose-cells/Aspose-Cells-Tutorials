---
category: general
date: 2026-05-30
description: Cara menggunakan AutoFilter dalam otomatisasi Excel dengan C#. Pelajari
  cara membuat workbook Excel, memfilter baris berdasarkan nilai, dan menyederhanakan
  tugas spreadsheet Anda.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: id
og_description: Cara menggunakan AutoFilter dalam otomatisasi Excel dengan C#. Kuasai
  pembuatan workbook Excel, memfilter baris berdasarkan nilai, dan mengotomatisasi
  spreadsheet dengan mudah.
og_title: Cara Menggunakan AutoFilter dalam Otomasi Excel C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Cara Menggunakan AutoFilter dalam Otomatisasi Excel C# – Panduan Langkah demi
  Langkah Lengkap
url: /id/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan AutoFilter dalam Otomasi Excel C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara menggunakan AutoFilter** ketika Anda menghasilkan file Excel dari kode C#? Anda tidak sendirian—banyak pengembang mengalami masalah ini ketika mereka perlu menyembunyikan baris yang tidak cocok dengan kriteria tertentu.  

Dalam tutorial ini kami akan membahas contoh konkret yang dapat dijalankan yang **membuat workbook Excel**, menambahkan tabel, dan kemudian **menyaring baris berdasarkan nilai** di kolom B. Pada akhir tutorial Anda akan memiliki potongan kode yang bersih dan dapat digunakan kembali yang dapat Anda sisipkan ke dalam proyek C# apa pun yang membutuhkan otomasi Excel.

## Apa yang Akan Anda Pelajari

- Siapkan proyek C# dengan pustaka Aspose.Cells (atau Microsoft.Office.Interop).  
- **Buat workbook Excel** secara programatik dan tambahkan tabel yang bergaya.  
- Terapkan **AutoFilter** untuk menampilkan hanya baris di mana **kolom B** sama dengan string tertentu.  
- Hapus filter sepenuhnya, mengembalikan seluruh dataset.  
- Tips untuk menangani kasus tepi seperti kolom yang hilang atau beberapa kriteria filter.

Tidak diperlukan pengalaman Excel‑VBA sebelumnya; cukup pemahaman dasar tentang C# dan paket NuGet.

---

## Prasyarat

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 atau lebih baru (atau .NET Framework 4.7+) | Runtime modern memberikan kinerja yang lebih baik dan manajemen paket yang lebih mudah. |
| Aspose.Cells untuk .NET (atau Microsoft.Office.Interop.Excel) diinstal melalui NuGet | Pustaka ini memberikan objek `Workbook`, `Worksheet`, dan `Table` yang digunakan dalam kode. |
| Editor kode (Visual Studio, VS Code, Rider, dll.) | Anda perlu mengompilasi dan menjalankan contoh. |
| Pengetahuan dasar C# | Tutorial menjelaskan *mengapa* setiap baris ada, bukan hanya *apa* yang dilakukannya. |

Anda dapat menginstal Aspose.Cells dengan:

```bash
dotnet add package Aspose.Cells
```

---

## Cara Menggunakan AutoFilter dengan Aspose.Cells di C#

Berikut adalah program lengkap yang berdiri sendiri. Simpan sebagai `Program.cs` dalam proyek konsol dan jalankan – Anda akan mendapatkan `FilteredWorkbook.xlsx` di folder output.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Cara Kerja Kode

1. **Membuat workbook** – `new Workbook()` memberi Anda file bersih; `Worksheets[0]` mengambil lembar default.  
2. **Mengisi data contoh** – Kami menulis dataset kecil sehingga Anda dapat melihat filter beraksi.  
3. **Menambahkan tabel** – `ListObjects.Add` mengubah rentang menjadi tabel Excel, yang secara otomatis mendukung penyaringan dan penataan.  
4. **Menerapkan AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` memberi tahu mesin: “Tampilkan hanya baris di mana kolom kedua (B) sama dengan *Apple*.”  
5. **Menyimpan file** – Dua file ditulis: satu terfilter, satu dengan filter dihapus, membuktikan bahwa `RemoveAutoFilter()` berfungsi seperti yang diharapkan.

> **Pro tip:** Jika Anda perlu menyaring dengan beberapa kriteria (mis., “Apple” *atau* “Banana”), gunakan overload `Filter(int columnIndex, string criteria1, string criteria2)` atau berikan array string.

---

## Menyaring Baris Berdasarkan Nilai – Variasi Umum

Meskipun contoh di atas berfokus pada **filter kolom B**, Anda mungkin ingin menyaring kolom lain atau menggunakan kriteria numerik. Berikut lembar contekan cepat:

| Desired filter | Code snippet |
|----------------|--------------|
| Kecocokan teks di kolom C | `table.AutoFilter.Filter(2, "Cherry");` |
| Angka lebih besar dari 10 di kolom C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Beberapa nilai di kolom B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Kasus tepi:** Jika header kolom salah eja atau indeks kolom di luar jangkauan, Aspose.Cells akan melempar `ArgumentException`. Lindungi dari hal ini dengan memeriksa `table.ListColumns.Count` sebelum menerapkan filter.

---

## Menghapus AutoFilter – Kapan Reset

Terkadang Anda perlu menampilkan kembali seluruh dataset (mis., setelah pengguna mengosongkan kotak pencarian). Memanggil `table.RemoveAutoFilter()` menyelesaikannya dalam satu baris. Jika Anda menggunakan Microsoft.Office.Interop, Anda akan memanggil `worksheet.AutoFilterMode = false;`.

---

## Ringkasan Contoh Kerja Penuh

Berikut adalah program *seluruhnya* lagi, tanpa komentar bagi yang lebih suka tampilan singkat:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Menjalankan ini menghasilkan dua file:

- **FilteredWorkbook.xlsx** – hanya baris dengan *Apple* yang terlihat.  
- **UnfilteredWorkbook.xlsx** – data asli dipulihkan.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan file .xls lama?**  
A: Ya. Aspose.Cells dapat menyimpan ke `.xlsx` maupun `.xls` dengan mengubah ekstensi file atau menggunakan `SaveOptions`.

**Q: Bagaimana jika saya perlu menyaring *setelah* workbook sudah disimpan?**  
A: Muat file dengan `new Workbook("path.xlsx")`, terapkan filter, lalu `Save` lagi.

**Q: Bisakah saya menerapkan filter pada *rentang* yang bukan tabel?**  
A: Tentu saja. Gunakan `worksheet.AutoFilter.Range = "A1:C5";` dan kemudian `worksheet.AutoFilter.ApplyFilter();`. Namun, tabel memberikan penataan bawaan dan referensi kolom yang lebih mudah.

---

## Gambar – Konfirmasi Visual

![Tangkapan layar yang menunjukkan AutoFilter diterapkan pada kolom B dalam workbook Excel yang dibuat dengan C#](/images/autofilter-column-b.png "AutoFilter pada kolom B")

*(Gambar ini menggambarkan tampilan terfilter di mana hanya baris yang berisi “Apple” yang tetap ada.)*

---

## Kesimpulan

Kami baru saja membahas **cara menggunakan AutoFilter** dalam skenario otomasi Excel yang digerakkan oleh C#, mulai dari **membuat workbook Excel** hingga **menyaring baris berdasarkan nilai** di **kolom B**, dan akhirnya **menghapus filter** ketika tidak lagi diperlukan. Langkah inti—menginisialisasi, menambahkan tabel, menerapkan filter, dan membersihkan—dapat digunakan kembali di proyek apa pun yang membutuhkan **excel automation c#**.

Siap untuk tantangan berikutnya? Coba:

- Menambahkan pemformatan bersyarat untuk menyoroti baris yang terfilter.  
- Mengekspor data terfilter ke CSV untuk pemrosesan lanjutan.  
- Menggabungkan beberapa filter (mis., “Apple” *dan* quantity > 8).

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara Menerapkan AutoFilter di Excel menggunakan Aspose.Cells untuk .NET (Panduan Analisis Data)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Cara Menggunakan Autofilter Not Contains di Aspose.Cells .NET untuk Analisis Data Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Cara Menerapkan Excel Autofilter 'EndsWith' Menggunakan Aspose.Cells untuk .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}