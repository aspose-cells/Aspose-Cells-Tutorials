---
category: general
date: 2026-10-20
description: Salin tabel pivot ke buku kerja baru menggunakan Aspose.Cells dan pelajari
  cara mengekspor bentuk yang dapat diedit ke PowerPoint dalam satu panduan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: id
lastmod: 2026-10-20
og_description: Salin tabel pivot ke buku kerja baru menggunakan Aspose.Cells dan
  ekspor bentuk yang dapat diedit ke PowerPoint—kode langkah demi langkah yang dapat
  Anda jalankan hari ini.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Salin tabel pivot ke buku kerja baru, ekspor bentuk ke PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Salin tabel pivot ke buku kerja baru, ekspor bentuk ke PowerPoint
url: /id/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin tabel pivot ke buku kerja baru, ekspor bentuk ke PowerPoint

Jika Anda perlu **copy pivot table to new workbook** sambil mempertahankan fungsionalitasnya, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells. Anda juga akan melihat cara tercepat untuk **export an editable shape to PowerPoint**, sehingga textbox tetap dapat diedit setelah konversi.

Banyak pengembang berasumsi bahwa menyalin rentang yang berisi tabel pivot akan kehilangan logika pivot, atau bahwa bentuk menjadi gambar statis saat disimpan sebagai PPTX. Tutorial ini membantah mitos tersebut dan memberikan solusi yang dapat diandalkan serta siap produksi.

Pada bagian berikut Anda akan:

* Memuat buku kerja sumber dan menyalin rentang yang mencakup tabel pivot.
* Membuat buku kerja tujuan yang berisi tabel pivot yang sama.
* Menambahkan bentuk textbox, mengubah teksnya, dan menyimpan buku kerja sebagai presentasi PowerPoint dimana textbox tetap dapat diedit.
* Memahami mengapa setiap panggilan API diperlukan dan bagaimana menghindari jebakan umum.

**Prerequisites**

* .NET 6.0 atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.7+).
* Aspose.Cells untuk .NET terinstal (`Install-Package Aspose.Cells`).
* Pengetahuan dasar tentang C# dan Visual Studio (atau IDE lain yang Anda sukai).

---

## Salin tabel pivot ke buku kerja baru

Bagian langkah‑demi‑langkah ini memperlihatkan cara menyalin rentang yang berisi tabel pivot dan mempertahankan definisi pivot di file baru.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Mengapa?*  
`Workbook` adalah titik masuk untuk setiap manipulasi Excel di Aspose.Cells. Memilih worksheet yang tepat memastikan kita bekerja pada lokasi tabel pivot yang tepat.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Mengapa?*  
Tabel pivot berada di dalam blok sel tertentu. Dengan menentukan `CellArea` yang sepenuhnya melingkupi pivot, Aspose.Cells mengetahui untuk menyalin cache pivot yang mendasarinya juga.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Mengapa?*  
Buku kerja baru menjamin tidak ada named range yang berbenturan atau pivot yang sudah ada, sehingga operasi penyalinan menjadi bersih.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Mengapa?*  
`CopyRows` adalah bagian dari **Aspose.Cells copy rows** API. Ia menyalin nilai sel serta cache pivot tersembunyi, sehingga tabel pivot tetap berfungsi setelah pemindahan.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Hasil*  
Buka `CopyWithPivot.xlsx` di Excel. Tabel pivot muncul persis seperti di file sumber, dan Anda dapat menyegarkan atau memodifikasinya secara normal.

---

## Ekspor bentuk yang dapat diedit ke PowerPoint

Sekarang kita akan menambahkan bentuk textbox, mengubah isinya, dan menyimpan buku kerja sebagai file PPTX. Bentuk tersebut tetap sepenuhnya dapat diedit ketika dibuka di PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Mengapa?*  
`AddTextBox` membuat **editable textbox in PowerPoint**‑compatible shape. Koordinatnya dalam satuan poin; sesuaikan agar cocok dengan tata letak Anda.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Mengapa?*  
Mengakses objek `Shape` secara langsung memungkinkan Anda mengubah properti seperti `Text`, `Font`, atau `Fill`. Langkah ini memperlihatkan cara mengatur konten awal secara programatik.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Hasil*  
Buka `Presentation.pptx` di Microsoft PowerPoint. Textbox muncul pada slide pertama, dan Anda dapat double‑click untuk mengedit teks seperti bentuk PowerPoint asli.

---

## Output yang Diharapkan

| File | Apa yang akan Anda lihat |
|------|--------------------------|
| `CopyWithPivot.xlsx` | Sebuah worksheet yang berisi tabel pivot asli, berfungsi penuh (penyegaran bekerja). |
| `Presentation.pptx` | Sebuah slide tunggal dengan textbox yang dapat diedit yang berisi teks “Change me in PowerPoint”. |

---

## Kesalahan umum dan tips praktik terbaik

* **Pivot cache loss** – Jika Anda hanya menyalin nilai sel (misalnya menggunakan `CopyRows` dengan flag `PasteOptions` diatur ke `PasteValues`), cache pivot akan diabaikan dan tabel menjadi statis. Selalu gunakan overload default `CopyRows` seperti yang ditunjukkan.
* **Shape positioning** – `AddTextBox` menggunakan satuan poin, bukan indeks sel Excel. Uji koordinat pada file contoh untuk menghindari penempatan di luar slide.
* **File format mismatch** – Menyimpan buku kerja sebagai PPTX dengan `SaveFormat.Pptx` secara otomatis mengonversi semua bentuk yang didukung. Mencoba menyimpan sebagai `Pdf` akan merasterisasi bentuk, menjadikannya tidak dapat diedit.

---

## Kesimpulan

Anda kini tahu cara **copy pivot table to new workbook** dan cara **export an editable shape to PowerPoint** menggunakan Aspose.Cells untuk .NET. Contoh kode lengkap yang dapat dijalankan mencakup setiap panggilan API yang diperlukan, menjelaskan mengapa setiap langkah penting, dan menampilkan hasil yang diharapkan.

Selanjutnya, Anda dapat menjelajahi:

* **Bekerja dengan chart** – menyalin chart bersama tabel pivot (`Aspose.Cells copy rows between worksheets`).
* **

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}