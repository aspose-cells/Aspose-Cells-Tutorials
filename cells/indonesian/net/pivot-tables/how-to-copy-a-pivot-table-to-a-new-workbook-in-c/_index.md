---
category: general
date: 2026-11-16
description: Cara menyalin tabel pivot dari satu file Excel ke buku kerja baru menggunakan
  C#. Pelajari cara memuat buku kerja, menyalin rentang, dan mempertahankan tabel
  pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: id
lastmod: 2026-11-16
og_description: Cara menyalin tabel pivot dari workbook yang ada ke workbook baru
  menggunakan C#. Ikuti panduan lengkap ini untuk memuat workbook Excel, menyalin
  rentang, dan menjaga pivot tetap utuh.
og_image_alt: how to copy pivot table example in C#
og_title: Cara menyalin tabel pivot ke workbook baru di C# – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Cara menyalin tabel pivot ke buku kerja baru di C#
url: /id/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot ke workbook baru dalam C#

Jika Anda perlu **cara menyalin tabel pivot** dari satu file Excel ke workbook baru, panduan ini menunjukkan langkah‑langkah tepatnya. Anda akan belajar cara **memuat workbook excel c#**, menentukan rentang sumber, dan **menyalin rentang ke workbook baru** sambil menjaga pivot tetap utuh.

Menyalin tabel pivot adalah kebutuhan umum ketika Anda ingin menggunakan kembali templat laporan, memigrasikan data antar proyek, atau menghasilkan file ringan untuk distribusi. Contoh kode di bawah ini menggunakan Aspose.Cells, sebuah perpustakaan .NET yang sepenuhnya dikelola dan dapat bekerja tanpa Microsoft Office terpasang. Pada akhir tutorial ini Anda akan memiliki program yang dapat dijalankan yang membuat workbook baru berisi tabel pivot asli, siap untuk diproses lebih lanjut atau dibagikan.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru (contoh ini bekerja dengan .NET Core dan .NET Framework)
* Visual Studio 2022 atau editor C# apa pun yang Anda sukai
* Lisensi Aspose.Cells untuk .NET (versi percobaan gratis dapat digunakan untuk evaluasi)
* File Excel sumber (`Source.xlsx`) yang berisi setidaknya satu tabel pivot

> **Pro tip:** Jika Anda menggunakan versi percobaan gratis, atur lisensi dalam kode untuk menghindari watermark evaluasi.

## Langkah 1: Muat workbook sumber (load excel workbook c#)

Langkah pertama adalah membuka workbook yang berisi tabel pivot. Aspose.Cells membaca file ke dalam memori, memberi Anda akses penuh ke lembar kerja, sel, dan objek pivot.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Mengapa ini penting*: Memuat workbook adalah dasar bagi semua otomatisasi Excel. Tanpa objek `Workbook` yang valid Anda tidak dapat memeriksa pivot atau menyalin datanya.

## Langkah 2: Tentukan area sel yang melingkupi tabel pivot (copy range to new workbook)

Tabel pivot berada di dalam blok sel berbentuk persegi panjang. Anda harus menentukan blok tersebut agar operasi penyalinan mengetahui apa yang harus dipindahkan. Konstruktor `CellArea` menggunakan indeks berbasis nol: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Mengapa ini penting*: Dengan secara eksplisit menetapkan rentang, Anda menghindari penyalinan data yang tidak terkait dan memastikan cache pivot termasuk. Rentang dapat dihitung secara dinamis jika Anda perlu menangani ukuran pivot yang bervariasi.

## Langkah 3: Buat workbook baru dan dapatkan lembar kerja pertamanya

Sekarang buat workbook tujuan yang akan menerima baris yang disalin. Aspose.Cells secara otomatis menambahkan lembar kerja default, yang akan kita gunakan sebagai target.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Mengapa ini penting*: Memulai dengan workbook bersih menjamin bahwa hanya tabel pivot (dan baris pendukungnya) yang masuk ke dalam file, sehingga output tetap ringan.

## Langkah 4: Salin baris dari rentang sumber ke lembar tujuan (how to copy pivot table)

Metode `CopyRows` menyalin seluruh baris, mempertahankan formula, format, dan—yang paling penting—tabel pivot. Parameter metode adalah: baris mulai, baris akhir, koleksi sel target, dan indeks baris di target tempat penyalinan dimulai (di sini `0` untuk memulai pada baris pertama).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Mengapa ini penting*: Menggunakan `CopyRows` alih-alih menyalin sel individual memastikan cache pivot tetap terhubung dengan data yang disalin. Aspose.Cells menangani struktur XML di baliknya, sehingga Anda tidak perlu membangun ulang pivot secara manual.

## Langkah 5: Simpan workbook hasil (copy range to new workbook)

Akhirnya, tulis file baru ke disk. Workbook tujuan kini berisi tabel pivot yang identik dan berfungsi secara independen dari file sumber.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Output yang diharapkan

Menjalankan program menghasilkan `CopyWithPivot.xlsx`. Membuka file tersebut di Excel menampilkan:

* Tata letak tabel pivot yang sama seperti di `Source.xlsx`
* Semua baris data sumber yang merupakan bagian dari cache pivot
* Tidak ada referensi ke workbook asli (pivot berfungsi secara offline)

## Menangani variasi umum

### Menyalin beberapa tabel pivot

Jika lembar sumber Anda berisi beberapa pivot, perluas `CellArea` untuk mencakup gabungan semua rentang, atau ulangi langkah penyalinan untuk setiap area yang berbeda.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Mempertahankan gaya dan pemformatan bersyarat

`CopyRows` menyalin gaya sel secara otomatis. Jika Anda perlu mempertahankan gaya bernama yang berlaku di seluruh workbook atau format angka khusus, panggil `destWorkbook.Worksheets[0].CopyStyle` sebelum menyimpan.

### Bekerja dengan workbook besar

Untuk file yang lebih besar dari 100 MB, pertimbangkan menggunakan `Workbook.LoadOptions` dengan `MemorySetting` diatur ke `MemorySetting.MemoryPreference` untuk mengurangi tekanan memori.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Kode sumber lengkap (siap dijalankan)

Berikut adalah program lengkap, termasuk direktif `using` dan komentar. Salin ke dalam proyek konsol baru dan ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Jalankan program (`dotnet run` atau `Ctrl+F5` di Visual Studio). Setelah eksekusi, buka `CopyWithPivot.xlsx` untuk memverifikasi bahwa pivot berperilaku persis seperti yang asli.

## Pertanyaan yang sering diajukan

**Q: Apakah ini bekerja dengan workbook yang berisi macro atau VBA?**  
A: Aspose.Cells dapat membaca file yang berisi macro (`.xlsm`), tetapi kode macro tidak disalin. Tabel pivot itu sendiri tetap dipertahankan karena merupakan bagian dari XML lembar kerja.

**Q: Bagaimana jika pivot menggunakan sumber data eksternal?**  
A: Operasi penyalinan hanya menyertakan data yang di‑cache. Jika workbook tujuan perlu menyegarkan dari sumber asli, Anda harus mengkonfigurasi ulang koneksi data secara manual.

**Q: Bisakah saya menyalin pivot tanpa baris data yang mendasarinya?**  
A: Tidak. Tabel pivot memerlukan cache-nya. Cara paling dapat diandalkan adalah menyalin baris yang berisi cache, seperti yang ditunjukkan. Anda dapat menyembunyikan baris tersebut nanti jika tidak ingin mereka terlihat.

## Kesimpulan

Anda sekarang tahu **cara menyalin tabel pivot** dari satu file Excel ke file lain menggunakan C#. Tutorial ini mencakup **load excel workbook c#**, mendefinisikan **copy range to new workbook**, dan menggunakan metode `CopyRows` Aspose.Cells untuk menjaga pivot tetap utuh. Dengan contoh lengkap yang dapat dijalankan, Anda dapat mengintegrasikan pola ini ke dalam pipeline pelaporan, alat ekspor otomatis, atau skenario apa pun di mana pivot harus dipindahkan antar workbook.

### Langkah selanjutnya

* Jelajahi fitur **Aspose.Cells** seperti menyegarkan pivot secara programatis.  
* Gabungkan pendekatan ini dengan **ExcelPackage** (EPPlus) jika Anda memerlukan alternatif sumber terbuka.  
* Otomatiskan penyalinan lintas beberapa lembar dengan melakukan loop melalui `srcWorkbook.Worksheets`.  

Silakan bereksperimen dengan rentang yang berbeda, tambahkan gaya khusus, atau sematkan logika ini dalam layanan pemrosesan data yang lebih besar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Baru dalam C# – Salin Tabel Pivot](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [Cara menyalin tabel pivot di Excel dengan C# dan Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Salin tabel pivot ke workbook baru, ekspor shape ke PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}