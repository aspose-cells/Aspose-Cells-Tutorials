---
category: general
date: 2026-05-30
description: Ubah ukuran font kotak teks di Excel menggunakan C#. Pelajari cara memodifikasi
  font kotak teks Excel dengan cepat menggunakan kode langkah demi langkah.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: id
og_description: Ubah ukuran font kotak teks di Excel menggunakan C#. Panduan ini menunjukkan
  cara memodifikasi font kotak teks Excel secara aman dan efisien.
og_title: Ubah Ukuran Font Kotak Teks di Excel dengan C# – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Ubah Ukuran Font Kotak Teks di Excel dengan C# – Panduan Lengkap
url: /id/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Ukuran Font Kotak Teks di Excel dengan C# – Panduan Lengkap

Perlu **mengubah ukuran font kotak teks** di lembar kerja Excel menggunakan C#? Anda berada di tempat yang tepat. Baik Anda membuat laporan, membangun dasbor, atau sekadar menyesuaikan templat, mengatur tampilan kotak teks dapat membuat spreadsheet Anda terlihat jauh lebih profesional.

Dalam tutorial ini kami juga akan **memodifikasi font kotak teks Excel** lebih dari sekadar ukuran—pikirkan keluarga font, ketebalan, dan bahkan penanganan banyak bentuk. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang mencakup setiap sudut proses, mulai dari membuka workbook hingga membersihkan objek COM. Tanpa basa‑basi, hanya kode praktis yang dapat Anda masukkan ke dalam proyek Anda hari ini.

## Prasyarat — Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Menyediakan kompiler dan runtime C#. |
| **Microsoft.Office.Interop.Excel** NuGet package | Memberikan tipe interop COM yang diperlukan untuk berkomunikasi dengan Excel. |
| **Excel installed** (any recent version) | Lapisan Interop hanya berfungsi ketika aplikasi Office terpasang. |
| **Basic C# knowledge** | Anda akan dapat mengikutinya dengan mudah, namun kami akan menjelaskan setiap baris. |

Jika ada yang belum terpasang, berhentilah sejenak dan instal dulu; sisa panduan mengasumsikan semuanya sudah tersedia.

## Langkah 1: Siapkan Proyek dan Impor Namespace

Langkah pertama—buat aplikasi console baru (atau integrasikan ke dalam yang sudah ada) dan impor namespace interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Tips Pro:** Jika Anda menargetkan .NET 6+, tambahkan paket `Microsoft.Office.Interop.Excel` melalui `dotnet add package Microsoft.Office.Interop.Excel`. Ini memastikan alias `Excel` terresolusi dengan benar.

## Langkah 2: Buka Workbook dan Dapatkan Worksheet Target

Sekarang kita perlu meluncurkan Excel, membuka file, dan menunjuk ke lembar yang berisi kotak teks. Membungkusnya dalam blok `try/finally` menjamin objek COM dilepaskan meskipun terjadi kesalahan.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Mengapa ini penting

Membuka workbook melalui COM memberi kita model objek yang hidup—artinya setiap perubahan yang kita buat langsung tercermin dalam file. Menetapkan `Visible = false` mempercepat proses dan menghindari jendela muncul selama otomatisasi.

## Langkah 3: Ambil Bentuk Kotak Teks

Excel memperlakukan kotak teks sebagai objek `Shape` dalam koleksi `Shapes`, bukan sebagai koleksi `TextBox` khusus. Itulah mengapa kode di bawah terlihat sedikit berbeda dari potongan kode yang mungkin Anda lihat secara daring.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Waspada:** Koleksi `Shapes` berindeks mulai dari 1, jadi kami menambahkan `+1` ke `textboxIndex` yang berbasis nol yang Anda berikan. Lupa melakukan ini menyebabkan error “index out of range” yang dapat membuat frustrasi saat debugging.

## Langkah 4: Ubah Ukuran Font Kotak Teks (dan Nama)

Di sinilah kita akhirnya **mengubah ukuran font kotak teks**. Properti `TextFrame2` memberi kita akses ke opsi pemformatan teks kaya, yang mencakup `Font.Name` dan `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Mengapa kami menggunakan `TextFrame2`

`TextFrame2` adalah model objek yang lebih baru yang diperkenalkan sejak Office 2007. Ia mendukung fitur tipografi lanjutan dan umumnya lebih andal dibandingkan `TextFrame` yang lebih lama. Menggunakannya memastikan operasi **mengubah ukuran font kotak teks** kami berfungsi pada versi Excel modern.

## Langkah 5: Simpan, Bersihkan, dan Verifikasi

Setelah mengubah font, kita perlu menyimpan perubahan dan melepaskan setiap referensi COM. Melewatkan pembersihan dapat meninggalkan proses Excel yang menjadi yatim piatu berjalan di latar belakang.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Tips Pro:** Jika Anda perlu **memodifikasi font kotak teks Excel** pada banyak worksheet, bungkus logika dalam loop yang mengiterasi `Workbook.Worksheets`. Hanya ingat untuk mengatur ulang `textboxIndex` untuk setiap lembar.

## Menangani Kasus Pinggir — Beberapa Kotak Teks dan Bentuk yang Hilang

Spreadsheet dunia nyata jarang hanya berisi satu kotak teks. Di bawah ini ada dua strategi cepat yang dapat Anda gunakan tanpa menulis ulang seluruh metode.

### 1. Ubah *semua* kotak teks pada sebuah lembar

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identifikasi kotak teks berdasarkan **Nama**nya alih-alih indeks

Jika Anda memberi kotak teks nama yang bermakna (misalnya, “TitleBox”), Anda dapat mengambilnya secara langsung:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Kedua pendekatan memungkinkan Anda **memodifikasi font kotak teks Excel** dengan presisi, terlepas dari bagaimana workbook disusun.

## Gambaran Visual (Opsional)

Jika Anda lebih suka petunjuk visual cepat, bayangkan diagram berikut:

![Tangkapan layar menunjukkan lembar kerja Excel dengan kotak teks yang disorot – menunjukkan cara mengubah ukuran font kotak teks](change-textbox-font-size.png)

*Alt text:* *ubah ukuran font kotak teks di Excel – kotak teks yang disorot siap untuk modifikasi font.*

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut satu file yang dapat Anda salin‑tempel ke proyek console dan jalankan segera (hanya perbarui jalur file dan nama lembar).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Apa yang Harus Anda Pelajari Selanjutnya?

- [Mengubah Ukuran Font di Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Cara Menyesuaikan Ukuran Font di Sel Excel Menggunakan Aspose.Cells .NET | Panduan Lengkap](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Cara Mengatur Gaya Font di Excel Menggunakan Aspose.Cells untuk .NET (Panduan Langkah demi Langkah)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}