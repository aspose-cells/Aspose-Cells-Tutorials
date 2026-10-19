---
category: general
date: 2026-03-30
description: Bagaimana menyalin lembar kerja di C# menggunakan Aspose.Cells – panduan
  langkah demi langkah yang mencakup menyalin rentang sel, menyalin kolom antar lembar,
  menyalin tabel pivot lembar kerja, dan menambahkan kode lembar kerja baru.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: id
og_description: Pelajari cara menyalin lembar kerja di C# dengan Aspose.Cells. Panduan
  ini menunjukkan cara menyalin rentang sel, mempertahankan tabel pivot, menyalin
  kolom antar lembar, dan menambahkan kode lembar kerja baru.
og_title: Cara Menyalin Lembar Kerja di C# – Tutorial Lengkap Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cara Menyalin Worksheet di C# dengan Aspose.Cells – Panduan Lengkap
url: /id/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyalin Worksheet di C# dengan Aspose.Cells – Panduan Lengkap

Pernah bertanya-tanya **how to copy worksheet** di C# tanpa kehilangan satu pun pivot table atau formula? Anda tidak sendirian—banyak pengembang mengalami kebuntuan ketika harus menduplikasi sebuah sheet sambil menjaga semua elemen tetap utuh. Dalam tutorial ini kami akan membahas solusi praktis, end‑to‑end yang tidak hanya menyalin data tetapi juga mempertahankan **copy worksheet pivot table**, menangani **copy cell range**, dan menunjukkan **add new worksheet code** yang Anda perlukan.

Kami akan membahas semuanya mulai dari memuat workbook sumber hingga menyimpan file tujuan, sehingga Anda dapat copy columns between sheets, preserve objects, dan menjaga kode tetap bersih. Tanpa referensi yang samar, hanya contoh lengkap yang dapat dijalankan yang dapat Anda masukkan ke dalam proyek Anda hari ini.

## Apa yang Dibahas dalam Tutorial Ini

- Memuat file Excel yang ada dengan Aspose.Cells  
- Menggunakan **add new worksheet code** untuk membuat sheet target  
- Mendefinisikan **copy cell range** yang mencakup pivot table  
- Menyiapkan **CopyOptions** untuk menjaga chart, formula, dan pivot table tetap utuh  
- Menjalankan **copy columns between sheets** dengan presisi per baris  
- Menyimpan hasil dan memverifikasi bahwa worksheet telah disalin dengan benar  

Di akhir panduan ini Anda akan dapat menjawab pertanyaan “how to copy worksheet” dengan percaya diri, baik Anda mengotomatisasi laporan maupun membangun UI berbasis spreadsheet.

## Cara Menyalin Worksheet – Ikhtisar

Sebelum kita masuk ke kode, mari kita rangkum alur tingkat tinggi. Anggap saja seperti resep:

1. **Load** workbook sumber (`Source.xlsx`).  
2. **Add** worksheet baru untuk menampung salinan (`add new worksheet code`).  
3. **Define** area yang ingin Anda duplikasikan (`copy cell range`).  
4. **Configure** opsi penyalinan agar pivot table tetap ada (`copy worksheet pivot table`).  
5. **Copy** baris dan kolom (`copy columns between sheets`).  
6. **Save** workbook baru (`Destination.xlsx`).  

Itu saja—enam langkah, tanpa sulap. Setiap langkah dijelaskan di bawah dengan potongan kode dan alasan di baliknya.

## Langkah 1 – Memuat Workbook Sumber

Hal pertama yang perlu dilakukan: Anda memerlukan instance `Workbook` yang menunjuk ke file yang ingin Anda duplikasikan. Langkah ini penting karena Aspose.Cells bekerja langsung dengan sistem file, bukan dengan UI Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Why this matters:* Memuat file membuat representasi dalam memori dari setiap sheet, sel, dan objek. Tanpa ini, tidak ada yang dapat disalin, dan setiap upaya `add new worksheet code` nanti akan gagal karena data sumber tidak ada.

## Langkah 2 – Menambahkan Worksheet Baru (add new worksheet code)

Sekarang kita membutuhkan tempat untuk menempelkan data yang disalin. Di sinilah **add new worksheet code** berperan. Anda dapat memberi nama sheet sesuka hati; di sini kami menamakannya `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro tip:* Jika Anda berencana menyalin beberapa sheet, panggil `Worksheets.Add` di dalam loop dan beri setiap sheet nama unik. Dengan begitu Anda menghindari bentrok nama dan menjaga workbook tetap rapi.

## Langkah 3 – Mendefinisikan Copy Cell Range

Sebuah **copy cell range** memberi tahu Aspose.Cells secara tepat baris dan kolom mana yang akan diduplikasi. Dalam banyak skenario dunia nyata, rentang tersebut mencakup pivot table, jadi kita harus tepat.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Why we need this:* Dengan secara eksplisit menyatakan rentang, Anda menghindari menyalin seluruh sheet (yang dapat membuang-buang) dan memastikan pivot table berada di dalam area yang disalin. Ini adalah inti dari **how to copy worksheet** ketika Anda hanya membutuhkan sebagian sheet.

## Langkah 4 – Mengatur Copy Options (preserve copy worksheet pivot table)

Aspose.Cells menyediakan objek `CopyOptions` yang mengontrol apa yang ditempelkan. Untuk mempertahankan pivot table, chart, dan formula, kami mengatur `PasteType.All` dan mengaktifkan `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Explanation:* `PasteType.All` adalah opsi paling inklusif, sementara `PasteSpecial` memberi tahu engine untuk memperlakukan objek kompleks—seperti pivot tables—dengan tepat. Melewatkan langkah ini adalah jebakan umum; sheet yang disalin akan kehilangan fitur interaktifnya.

## Langkah 5 – Menyalin Baris dan Kolom (copy columns between sheets)

Sekarang saatnya kerja berat: memindahkan data sebenarnya. Kami akan menggunakan `CopyRows` dan `CopyColumns` untuk menangani **copy columns between sheets**. Melakukan keduanya memastikan sel yang digabung dan lebar kolom tetap terjaga.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*What’s happening:* `CopyRows` memindahkan data baris per baris, sementara `CopyColumns` melakukan hal yang sama kolom per kolom. Menjalankan keduanya menjamin seluruh blok persegi panjang diduplikasi, yang penting ketika Anda perlu **copy columns between sheets** yang memiliki lebar kolom berbeda atau kolom tersembunyi.

## Langkah 6 – Menyimpan Workbook

Akhirnya, tulis perubahan kembali ke disk. Langkah ini menyelesaikan proses **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verification tip:* Buka `Destination.xlsx` dan periksa bahwa sheet `"Copy"` tampak identik dengan yang asli, pivot table berfungsi, dan lebar kolom cocok. Jika ada yang tidak beres, tinjau kembali pengaturan `CopyOptions`.

## Kasus Pojok & Variasi Umum

### Menyalin Beberapa Worksheet

Jika Anda perlu menduplikasi beberapa sheet, bungkus logika di atas dalam loop `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Mempertahankan Formula di Berbagai Workbook

Ketika workbook sumber dan tujuan memiliki named range yang berbeda, atur `copyOptions` ke `PasteType.Formulas` selain `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Rentang Besar dan Kinerja

Untuk dataset besar (ratusan ribu baris), pertimbangkan menggunakan hanya `CopyRows` dan melewatkan `CopyColumns` jika lebar kolom tidak kritis. Ini dapat menghemat beberapa detik.

## Contoh Lengkap yang Berjalan

Berikut adalah program lengkap yang siap dijalankan yang mencakup semua yang telah kami bahas. Tempelkan ke aplikasi console, sesuaikan jalur file, dan tekan **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Expected result:** Membuka `Destination.xlsx` menampilkan sheet bernama **Copy** yang mencerminkan sheet pertama dari `Source.xlsx`—termasuk semua pivot table, format, dan lebar kolom. File asli tetap tidak tersentuh.

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan file .xlsx yang dibuat oleh Excel 2019?**  
A: Tentu saja. Aspose.Cells mendukung semua format Excel modern, jadi kode yang sama bekerja untuk file `.xlsx`, `.xlsm`, dan bahkan file `.xls` yang lebih lama

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}