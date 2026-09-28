---
category: general
date: 2026-09-27
description: Pelajari cara menghapus baris dari tabel Excel di C# dengan panduan langkah
  demi langkah yang juga menunjukkan cara memuat workbook Excel di C# dengan cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: id
lastmod: 2026-09-27
og_description: Hapus baris dari tabel Excel di C# dengan contoh yang jelas. Tutorial
  ini juga mencakup cara memuat workbook Excel di C# dan menangani kasus tepi umum.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Hapus baris dari tabel Excel di C# – panduan kode lengkap
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Cara menghapus baris dari tabel Excel menggunakan C#
url: /id/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delete rows from Excel table in C# – complete programming guide

Jika Anda perlu **menghapus baris dari tabel Excel** dalam file .xlsx, tutorial ini menunjukkan secara tepat cara melakukannya dengan C#. Anda akan melihat contoh singkat yang dapat dijalankan yang memuat workbook Excel, menghapus baris tertentu dari tabel pertama, dan menyimpan hasilnya. Pendekatan ini bekerja dengan library Aspose.Cells yang populer dan dapat disesuaikan dengan API Excel .NET lainnya.

Menghapus baris dari sebuah tabel adalah tugas umum saat membersihkan data yang diimpor, memotong bagian laporan, atau mengotomatiskan pembaruan spreadsheet. Pada akhir panduan ini Anda akan dapat **memuat workbook Excel C#**, menemukan sebuah tabel (ListObject), menghapus baris mana pun yang Anda pilih, dan menulis file yang telah dimodifikasi kembali ke disk.

## Prasyarat

* .NET 6.0 atau yang lebih baru terpasang (kode juga berfungsi dengan .NET Framework 4.7+).
* Referensi ke paket NuGet **Aspose.Cells** (atau library kompatibel lain yang menyediakan tipe `Workbook`, `Worksheet`, dan `ListObject`).
* File input bernama `input.xlsx` ditempatkan di folder yang dapat Anda referensikan dari proyek Anda.
* Familiaritas dasar dengan sintaks C# dan Visual Studio (atau IDE pilihan Anda).

> **Pro tip:** Jika Anda lebih menyukai alternatif sumber terbuka, logika yang sama dapat diterapkan dengan **ClosedXML** – cukup ganti kelas spesifik Aspose dengan `XLWorkbook`, `IXLWorksheet`, dan `IXLTable`.

## Langkah 1: Muat workbook Excel di C#

Operasi pertama adalah membaca file sumber ke memori. Memuat workbook tidak memakan banyak sumber daya untuk ukuran spreadsheet tipikal dan memberi Anda akses penuh ke lembar kerja, tabel, dan nilai sel.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Mengapa ini penting:* `Workbook` mengurai struktur Open XML dari file .xlsx, menampilkan koleksi objek `Worksheet`. Jika file tidak ditemukan, Aspose akan melempar `FileNotFoundException`, jadi pastikan jalurnya benar.

## Langkah 2: Akses lembar kerja target

Sebagian besar spreadsheet berisi beberapa lembar; Anda perlu memilih lembar yang berisi tabel yang ingin Anda ubah. Di sini kami menggunakan lembar pertama (`Worksheets[0]`), yang merupakan nilai default yang aman untuk file sederhana.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Mengapa ini penting:* `Worksheet` adalah wadah untuk tabel (`ListObjects`). Mengakses lembar yang tepat mencegah perubahan tidak sengaja pada data yang tidak terkait.

## Langkah 3: Hapus baris dari tabel Excel

Tabel Excel direpresentasikan oleh objek `ListObject`. Tabel pertama pada lembar adalah `ListObjects[0]`. Metode `DeleteRows(startIndex, rowCount)` menghapus baris **relatif terhadap area data tabel**, bukan nomor baris absolut pada lembar kerja.  

Dalam contoh ini kami menghapus baris kedua dan ketiga dari tabel (header berada pada baris 0, jadi kami mulai dari indeks 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Bagaimana jika tabel memiliki nama atau posisi yang berbeda?

* **Tabel bernama:** Gunakan `ws.ListObjects["MyTableName"]` alih-alih indeks.
* **Beberapa tabel:** Lakukan loop melalui `ws.ListObjects` dan pilih yang cocok dengan kondisi (mis., nama header kolom).
* **Jumlah baris dinamis:** Anda dapat menghitung `rowCount` pada waktu berjalan dengan memeriksa `ws.ListObjects[0].DataRange.RowCount`.

### Penanganan kasus tepi

| Situation                              | Recommended code change                                      |
|----------------------------------------|--------------------------------------------------------------|
| Tabel kosong atau memiliki baris lebih sedikit      | Periksa `ws.ListObjects[0].DataRange.RowCount` sebelum menghapus. |
| Baris yang akan dihapus melebihi ukuran tabel       | Batasi `rowCount` menjadi `DataRange.RowCount - startIndex`.       |
| Perlu menghapus baris berdasarkan kondisi (mis., nilai di kolom C) | Iterasi `DataRange.Rows` dan kumpulkan indeks yang cocok, lalu hapus dalam urutan terbalik untuk menjaga indeks tetap stabil. |

## Langkah 4: Simpan workbook yang telah dimodifikasi

Setelah penghapusan, tulis kembali workbook ke file baru (atau timpa file asli jika Anda lebih suka). Menyimpan membuat file .xlsx baru yang mencerminkan tabel yang telah diperbarui.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Mengapa ini penting:* `Save` menyerialisasi representasi dalam memori ke disk. Jika Anda perlu mempertahankan file asli, selalu tulis ke jalur yang berbeda.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah memberikan Anda program mandiri yang dapat Anda salin, tempel, dan jalankan.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Output yang diharapkan** (konsol):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Buka `output.xlsx` – tabel pertama kini tidak memiliki baris yang Anda hapus, sementara baris header tetap utuh.

## Pertanyaan umum dan variasi

### Bagaimana cara menghapus baris dari **semua** tabel dalam sebuah workbook?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Bisakah saya menghapus baris berdasarkan **nilai sel**?

Ya. Pindai `DataRange` untuk sel yang cocok, kumpulkan indeks berbasis nol mereka, lalu hapus dalam urutan menurun:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Bagaimana jika saya perlu **mempertahankan format**?

`DeleteRows` menghapus seluruh baris dari tabel tetapi mempertahankan gaya tabel untuk baris yang tersisa. Jika Anda perlu menjaga format tertentu pada baris yang akan dihapus, salin gaya tersebut ke baris lain sebelum penghapusan.

### Apakah ini bekerja dengan file **.xls** (Excel 97‑2003)?

Ya. Aspose.Cells secara otomatis mendeteksi format file, sehingga kode yang sama bekerja dengan `.xls`. Cukup ubah ekstensi file dalam konstruktor `Workbook`.

## Tips kinerja

* **Penghapusan batch:** Menghapus banyak baris satu per satu dapat lebih lambat. Gunakan satu panggilan `DeleteRows(start, count)` bila memungkinkan.
* **Hindari pemblokiran thread UI:** Jika Anda mengintegrasikan ini ke dalam aplikasi desktop, jalankan manipulasi workbook pada thread latar belakang agar UI tetap responsif.
* **Dispose dengan tepat:** Meskipun Aspose.Cells menggunakan memori terkelola, bungkus `Workbook` dalam blok `using` jika Anda menangani file besar untuk membebaskan sumber daya dengan cepat.

## Kesimpulan

Anda kini memiliki contoh lengkap yang siap produksi yang **menghapus baris dari tabel Excel** menggunakan C#. Panduan ini mencakup cara **memuat workbook Excel C#**, menemukan `ListObject` yang diinginkan, menghapus baris dengan aman, dan menyimpan file yang telah diperbarui. Dengan penanganan kasus tepi dan saran kinerja yang disertakan, Anda dapat menyesuaikan pola ini untuk skenario yang lebih kompleks seperti penghapusan bersyarat, banyak tabel, atau library Excel .NET alternatif.

### Langkah selanjutnya

* Jelajahi **ClosedXML** atau **EPPlus** jika Anda lebih menyukai stack sepenuhnya sumber terbuka.
* Gabungkan penghapusan baris dengan **validasi data** untuk membersihkan spreadsheet sebelum mengimpor ke basis data.
* Otomatiskan proses untuk folder berisi workbook menggunakan `Directory.GetFiles` dan loop.

Silakan bereksperimen dengan rentang baris, nama tabel, dan logika bersyarat yang berbeda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Muat File Excel C# – Cara Menghapus Baris dan Menghapus Baris Tertentu](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Cara Menyisipkan dan Menghapus Baris di Excel dengan Aspose.Cells untuk .NET: Panduan Komprehensif](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Cara Menghapus Baris Kosong di Excel Menggunakan Aspose.Cells .NET untuk Pembersihan Data](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}