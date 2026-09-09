---
category: general
date: 2026-03-01
description: Impor data dengan pemformatan ke Excel menggunakan C#. Pelajari cara
  mengimpor DataTable ke Excel dan menambahkan warna latar belakang pada sel dalam
  beberapa langkah saja.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: id
og_description: Impor data dengan format ke Excel menggunakan C#. Panduan langkah
  demi langkah yang menunjukkan cara mengimpor DataTable dan menambahkan warna latar
  belakang ke sel.
og_title: Impor Data dengan Pemformatan ke Excel – Panduan C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Impor Data dengan Pemformatan ke Excel menggunakan C#
url: /id/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Impor Data dengan Pemformatan ke Excel menggunakan C#

Pernah perlu **mengimpor data dengan pemformatan** ke dalam workbook Excel tetapi selalu mendapatkan lembar yang polos dan membosankan? Anda tidak sendirian. Kebanyakan pengembang mengalami hal ini ketika mereka menemukan bahwa impor default menghapus semua warna dan gaya yang mereka susun dengan susah payah di data sumber.

Dalam tutorial ini kita akan membahas solusi lengkap yang **siap dijalankan** yang **mengimpor DataTable ke Excel** dan **menambahkan warna latar belakang ke sel Excel** secara bersamaan. Tidak diperlukan pemrosesan tambahan—spreadsheet Anda akan terlihat persis seperti yang Anda inginkan langsung dari awal.

## Apa yang Akan Anda Pelajari

- Cara mengambil data ke dalam `DataTable`.
- Cara mendefinisikan array objek `Style` yang membawa warna latar belakang.
- Cara memanggil `ImportDataTable` dengan gaya tersebut sehingga impor mempertahankan pemformatan.
- Contoh lengkap yang dapat dijalankan yang dapat Anda salin ke aplikasi console dan melihat hasilnya secara instan.
- Tips, jebakan, dan variasi untuk proyek dunia nyata.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+).
- Library **GemBox.Spreadsheet** (versi gratis sudah cukup untuk demo).
- Familiaritas dasar dengan C# dan konsep Excel.

Jika Anda bertanya‑tanya *mengapa GemBox?* karena ia menawarkan metode satu baris `ImportDataTable` yang menerima array gaya—tepat apa yang kita butuhkan untuk **mengimpor data dengan pemformatan** tanpa menulis loop.

---

## Langkah 1: Siapkan Proyek dan Tambahkan GemBox.Spreadsheet

Untuk memulai, buat aplikasi console baru:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** Versi gratis membatasi lembar kerja hingga 150 k sel, yang cukup untuk demo. Jika Anda mencapai batas, upgrade atau beralih ke EPPlus, tetapi API‑nya akan sedikit berbeda.

## Langkah 2: Ambil Data Sumber sebagai `DataTable`

Hal pertama yang kita butuhkan adalah `DataTable` yang meniru data yang biasanya Anda tarik dari basis data. Berikut helper kecil yang membuatnya di memori:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Mengapa ini penting:** Dengan memisahkan pengambilan data ke dalam metode terpisah, Anda dapat mengganti sumber apa saja—SQL, CSV, layanan web—tanpa menyentuh logika impor. Ini membuat kode bersih dan menjadikan tutorial **cara mengimpor datatable ke excel** dapat digunakan kembali.

## Langkah 3: Definisikan Gaya yang Ingin Diterapkan

Sekarang bagian yang menyenangkan: kita akan membuat array objek `Style`, masing‑masing dengan `ForegroundColor` yang berbeda. GemBox memungkinkan Anda mengatur `BackgroundPatternColor` (isi sel) dan `ForegroundColor` (warna teks). Untuk demo ini kita akan memberi warna berbeda pada dua kolom pertama.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Penjelasan:**  
- Objek `Style` adalah kontainer ringan; Anda tidak perlu membuat yang baru untuk setiap sel.  
- Dengan menyelaraskan urutan array dengan urutan kolom, GemBox secara otomatis menerapkan gaya yang cocok selama impor.  
- Inilah kunci **mengimpor data dengan pemformatan**—pemformatan menyertai data, bukan setelahnya.

## Langkah 4: Impor `DataTable` ke Worksheet dengan Gaya

Dengan data dan gaya siap, kita kini dapat membuat workbook, memilih worksheet pertama, dan memanggil `ImportDataTable`. Tanda tangan metodenya terlihat seperti ini:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Berikut cara menggunakannya:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Apa yang terjadi di balik layar?**  
- `true` memberi tahu GemBox untuk menulis nama kolom sebagai baris pertama.  
- `0, 0` menempatkan impor pada sel A1.  
- `importStyles` mengaitkan setiap kolom dengan warna yang telah kita definisikan sebelumnya.  

Saat Anda membuka *Report.xlsx*, Anda akan melihat kolom **ID** berwarna biru muda, kolom **Name** berwarna hijau muda, dan kolom **Score** tidak berubah. Itulah **mengimpor data dengan pemformatan** dalam satu panggilan.

## Langkah 5: Verifikasi Hasil (Output yang Diharapkan)

Buka `Report.xlsx` yang dihasilkan. Anda seharusnya melihat sesuatu seperti ini:

| ID (biru muda) | Nama (hijau muda) | Skor |
|----------------|-------------------|------|
| 1              | Alice             | 93.5 |
| 2              | Bob               | 78.0 |
| 3              | Charlie           | 85.2 |
| 4              | Diana             | 91.3 |
| 5              | Ethan             | 67.8 |

- Sel kolom **ID** memiliki latar belakang biru muda.  
- Sel kolom **Nama** memiliki latar belakang hijau muda.  
- Kolom **Skor** tetap dengan latar belakang putih default.

Petunjuk visual ini membuat laporan langsung dapat dipindai—sentuhan kecil yang dapat secara dramatis meningkatkan pengalaman pengguna.

![Lembar Excel yang menunjukkan mengimpor data dengan pemformatan – kolom ID biru muda, kolom Nama hijau muda](excel-screenshot.png "contoh mengimpor data dengan pemformatan")

*Teks alt gambar mencakup kata kunci utama untuk SEO.*

---

## Pertanyaan Umum & Kasus Pinggir

### Bisakah saya menerapkan lebih dari sekadar warna latar belakang?

Tentu saja. `Style` memungkinkan Anda mengatur font, border, format angka, bahkan pemformatan bersyarat. Misalnya, untuk membuat skor di atas 90 menjadi tebal dan merah:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Bagaimana jika `DataTable` saya memiliki lebih banyak kolom daripada gaya?

GemBox akan menerapkan gaya hanya pada kolom yang memiliki entri yang cocok dalam array. Kolom tambahan akan kembali ke gaya default—tidak ada error yang dilempar.

### Apakah ini bekerja dengan dataset besar?

Ya, tetapi perhatikan batas sel versi gratis (150 k sel). Untuk laporan yang sangat besar, pertimbangkan lisensi berbayar atau alirkan data baris‑per‑baris dengan `worksheet.Cells[row, col].Value = …`—meskipun Anda akan kehilangan kemudahan satu baris.

### Bagaimana cara mengimpor data dengan pemformatan dari template Excel yang sudah ada?

Anda dapat memuat workbook template terlebih dahulu:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Ini memungkinkan Anda mempertahankan logo header, footer, dan gaya yang sudah ada sambil tetap **mengimpor data dengan pemformatan** untuk bagian dinamis.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Jalankan program (`dotnet run`) dan buka *Report.xlsx* yang dihasilkan untuk melihat warna yang diterapkan secara instan.

---

## Kesimpulan

Anda kini memiliki solusi yang solid, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}