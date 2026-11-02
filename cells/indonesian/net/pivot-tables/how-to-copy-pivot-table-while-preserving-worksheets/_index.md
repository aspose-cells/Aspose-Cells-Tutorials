---
category: general
date: 2026-09-15
description: Pelajari cara menyalin tabel pivot, menyalin lembar kerja dengan pivot,
  dan menyimpan buku kerja sebagai pptx menggunakan Aspose.Cells dalam C#. Panduan
  langkah demi langkah lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: id
lastmod: 2026-09-15
og_description: Cara menyalin tabel pivot, menyalin lembar kerja dengan pivot, dan
  menyimpan buku kerja sebagai pptx menggunakan Aspose.Cells. Ikuti contoh C# lengkap
  yang dapat dijalankan.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Cara menyalin tabel pivot dan mengekspor lembar kerja – panduan lengkap
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara menyalin tabel pivot sambil mempertahankan lembar kerja
url: /id/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot sambil mempertahankan lembar kerja

Jika Anda perlu **how to copy pivot table** dari satu workbook ke workbook lain tanpa kehilangan pivot cache yang mendasarinya, panduan ini menyediakan solusi siap‑jalankan. Anda juga akan melihat cara **copy worksheet with pivot** dan cara **save workbook as pptx** sambil mempertahankan kotak teks yang dapat diedit. Semua contoh menggunakan Aspose.Cells terbaru untuk .NET, sehingga Anda dapat menyalin kode ke proyek C# mana pun dan melihat hasilnya secara langsung.

Bekerja dengan file Excel secara programatik sering melibatkan pemindahan data antar workbook, mengekspor ke presentasi, atau menyisipkan Smart Marker yang kompleks. Tiga potongan kode di bawah ini mencakup skenario umum tersebut dan menjelaskan mengapa setiap langkah penting.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru terpasang  
* Aspose.Cells untuk .NET (versi 25.11 atau lebih baru) direferensikan dalam proyek Anda  
* Sebuah folder bernama `YOUR_DIRECTORY` tempat file contoh akan dibaca dan ditulis  

Tidak ada paket NuGet tambahan yang diperlukan.

---

## Cara menyalin tabel pivot dengan Aspose.Cells

Menyalin rentang yang berisi tabel pivot sambil mempertahankan pivot cache adalah kebutuhan yang sering muncul. Langkah‑langkah berikut menunjukkan urutan tepat yang Anda perlukan.

### Langkah 1 – Muat workbook sumber yang berisi tabel pivot

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Mengapa*: Aspose.Cells membaca workbook ke dalam memori, memberi Anda akses ke lembar kerja, sel, dan tabel pivot.

### Langkah 2 – Buat workbook tujuan kosong

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Mengapa*: Memulai dengan workbook kosong menjamin tidak ada gaya tersembunyi atau named range yang mengganggu operasi penyalinan.

### Langkah 3 – Salin baris yang mencakup tabel pivot

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Mengapa*: `CopyRows` menyalin nilai sel mentah, format, dan referensi pivot cache yang mendasarinya. Rentang harus mencakup seluruh area tabel pivot.

### Langkah 4 – Salin kolom yang berisi tabel pivot

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Mengapa*: Tabel pivot meluas baik pada baris maupun kolom; menyalin kolom memastikan tata letak tabel lengkap tetap terjaga.

### Langkah 5 – Transfer lembar yang telah disiapkan ke dalam workbook tujuan

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Mengapa*: Metode `Copy` menggandakan worksheet, termasuk pivot cache, sehingga workbook tujuan menampilkan tabel pivot yang identik.

### Langkah 6 – Simpan hasil – tabel pivot tetap utuh

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Mengapa*: Menyimpan workbook menuliskan semua struktur internal, menjamin pivot dapat disegarkan nanti.

**Pro tip**: Setelah menyalin, Anda dapat memanggil `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` untuk memperbarui data jika data sumber berubah.

---

## Salin lembar kerja dengan pivot – alternatif singkat

Jika Anda hanya perlu menduplikasi seluruh lembar kerja yang sudah berisi tabel pivot, Anda dapat melewatkan langkah penyalinan baris/kolom dan langsung menggunakan metode `Copy` pada tingkat worksheet.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Pendekatan ini berguna ketika lembar kerja tidak berisi data tambahan di luar area pivot. Operasi **copy worksheet with pivot** secara otomatis mempertahankan semua format, named range, dan pivot cache.

---

## Simpan workbook sebagai PPTX dengan kotak teks yang dapat diedit

Mengekspor lembar Excel yang berisi kotak teks yang dapat diedit ke PowerPoint dapat diperlukan untuk dasbor pelaporan. Kode di bawah ini menunjukkan **save workbook as pptx** sambil menjaga kotak teks tetap dapat diedit.

### Langkah 1 – Muat workbook yang mencakup kotak teks

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Langkah 2 – Konfigurasikan opsi penyimpanan PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Mengapa*: Menetapkan `ExportEditableTextBox` memberi tahu Aspose.Cells untuk menerjemahkan kotak teks Excel menjadi bentuk PowerPoint yang tetap dapat diedit setelah ekspor.

### Langkah 3 – Simpan workbook sebagai PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Expected result**: Buka `Result.pptx` di PowerPoint, pilih kotak teks, dan edit isinya seperti bentuk asli mana pun.

**Common question**: *What if I need to keep the textbox locked?*  
Set `pptxOptions.ExportEditableTextBox = false`; the shape will be converted to a static image instead.

---

## Ekspor Smart Marker yang berisi array JSON sebagai nilai sel tunggal

Smart Markers memungkinkan Anda mengisi templat Excel dengan struktur data yang kompleks. Di bawah ini contoh lengkap yang mendemonstrasikan **how to copy pivot table**‑style data handling sambil menyisipkan array JSON ke dalam satu sel.

### Langkah 1 – Siapkan SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Langkah 2 – Sisipkan Smart Marker ke sel A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Langkah 3 – Definisikan sumber data dengan array bergaya JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Langkah 4 – Proses workbook

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Langkah 5 – Simpan workbook hasil

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Result verification**: Buka `JsonSingleCell.xlsx` dan pastikan sel A1 berisi `A,B,C`. Ini menunjukkan cara memperlakukan koleksi sebagai nilai sel tunggal, pola yang sering dibutuhkan saat mengekspor data untuk sistem hilir.

---

## Contoh kerja lengkap

Berikut adalah satu program yang menggabungkan tiga skenario. Anda dapat menyalin kode ke aplikasi console, menyesuaikan jalur file, dan menjalankannya untuk melihat ketiga output.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Menjalankan program ini menghasilkan:

* `CopyWithPivot.xlsx` – salinan sempurna dari tabel pivot asli.  
* `Result.pptx` – slide PowerPoint dengan kotak teks yang dapat diedit.  
* `JsonSingleCell.xlsx` – lembar di mana array JSON muncul dalam satu sel.

---

## Kesimpulan

Anda kini tahu **how to copy pivot table** dengan aman, cara **copy worksheet with pivot** dalam satu panggilan, dan cara **save workbook as pptx** sambil mempertahankan kotak teks yang dapat diedit. Pola‑polanya mencakup alur kerja Excel‑to‑PowerPoint dan Excel‑to‑JSON yang paling umum yang akan Anda temui dalam proyek otomasi perusahaan.

Selanjutnya, pertimbangkan untuk mengeksplor:

* Menyegarkan tabel pivot yang disalin secara programatik (`PivotTable.Refresh()`)  
* Mengekspor ke format lain seperti PDF atau HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Menggunakan opsi Smart Marker lanjutan seperti fungsi kustom atau pemformatan bersyarat  

Jangan ragu bereksperimen dengan rentang berbeda, beberapa lembar kerja, atau struktur JSON yang lebih besar. Aspose.Cells API memberi Anda kontrol detail, sehingga Anda dapat menyesuaikan contoh ini ke skenario dunia nyata apa pun. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat Workbook Baru – Cara Menyalin Lembar Kerja dengan Tabel Pivot](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Cara Menyalin Tabel Pivot di C# – Mengonversi Excel ke PPTX, Menyalin Rentang & Membuat Kotak Teks](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Salin Lembar dalam Workbook Menggunakan Aspose.Cells untuk .NET - Panduan Langkah‑per‑Langkah](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}