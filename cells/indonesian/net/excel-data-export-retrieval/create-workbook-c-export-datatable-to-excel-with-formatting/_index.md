---
category: general
date: 2026-02-15
description: Buat workbook C# dan ekspor DataTable ke Excel dengan pemformatan baris,
  atur latar belakang baris, serta otomatisasi tugas Excel dalam hitungan menit.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: id
og_description: Buat workbook C# dengan cepat, terapkan gaya baris, dan otomatisasi
  ekspor Excel dengan contoh kode lengkap serta tips praktik terbaik.
og_title: Buat Workbook C# – Ekspor DataTable ke Excel dengan Pemformatan
tags:
- C#
- Excel
- DataExport
title: Buat Workbook C# – Ekspor DataTable ke Excel dengan Pemformatan
url: /id/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook C# – Ekspor DataTable ke Excel dengan Pemformatan

Pernahkah Anda perlu **create workbook C#** dan mengekspor sebuah `DataTable` ke Excel dengan gaya khusus? Anda tidak sendirian. Dalam banyak aplikasi lini‑bisnis, kebutuhan adalah menghasilkan spreadsheet yang terformat rapi sehingga pengguna non‑teknis dapat membuka dan memahaminya secara instan.  

Dalam panduan ini kami akan menelusuri solusi lengkap yang siap dijalankan yang menunjukkan **how to create workbook C#**, menerapkan **excel export formatting**, mengatur **row background**, dan memanfaatkan **excel automation c#** untuk menghasilkan file yang halus. Tidak ada jalan pintas “lihat dokumen” yang samar—hanya kode lengkap, penjelasan mengapa setiap baris penting, dan tips yang benar‑benar akan Anda gunakan besok.

---

## Prasyarat

- .NET 6 (atau .NET Framework 4.6+).  
- Visual Studio 2022 atau IDE yang kompatibel dengan C#.  
- Paket NuGet **Aspose.Cells for .NET** (atau perpustakaan apa pun yang menyediakan `Workbook`, `Worksheet`, `Style`).  
- Pemahaman dasar tentang `DataTable`.  

Jika Anda belum memiliki Aspose.Cells, jalankan:

```bash
dotnet add package Aspose.Cells
```

> **Tips Pro:** Versi percobaan gratis berfungsi untuk kebanyakan skenario pengembangan; cukup ingat untuk mengganti kunci lisensi sebelum dipublikasikan.

![Contoh create workbook C# yang menampilkan baris berformat di Excel]( "Contoh create workbook C# dengan warna latar belakang baris")

---

## Langkah 1: Inisialisasi Workbook dan Worksheet (Create Workbook C#)

Hal pertama yang harus Anda lakukan adalah menginstansiasi sebuah `Workbook`. Anggaplah ini seperti membuka file Excel baru yang sepenuhnya berada di memori.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Mengapa?**  
`Workbook` menyimpan seluruh dokumen Excel, sementara `Worksheet` mewakili satu tab. Memulai dengan workbook bersih memastikan Anda mengontrol setiap aspek output—tidak ada gaya default tersembunyi yang menyusup.

---

## Langkah 2: Siapkan Contoh DataTable (Export DataTable Excel)

Dalam proyek nyata Anda akan mengambil data dari basis data, tetapi untuk ilustrasi kami akan membuat `DataTable` kecil secara langsung.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Mengapa ini penting:**  
Mengekspor sebuah `DataTable` adalah cara paling umum untuk memindahkan data tabel dari aplikasi ke Excel. Metode di atas sepenuhnya mandiri, sehingga Anda dapat menyalin‑tempelnya ke proyek mana pun dan akan langsung berfungsi.

---

## Langkah 3: Buat Style per Baris (Excel Export Formatting)

Untuk memberi setiap baris warna latar belakangnya sendiri, kami menghasilkan objek `Style` untuk setiap baris dalam `DataTable`. Di sinilah **excel export formatting** bersinar.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Mengapa styling per‑baris?**  
Jika Anda perlu menyorot catatan tertentu (misalnya faktur yang jatuh tempo) Anda dapat mengganti siklus warna sederhana dengan logika kondisional—cukup atur `style.ForegroundColor` berdasarkan data pada baris tersebut.

---

## Langkah 4: Impor DataTable dengan Style Baris (Set Row Background)

Sekarang kami menggabungkan semuanya: data, workbook, dan style.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Apa yang akan Anda lihat:**  
Membuka `EmployeesReport.xlsx` menampilkan baris header dengan format default, diikuti oleh empat baris data masing‑masing berwarna latar belakang ringan. Hasilnya tampak seperti laporan buatan tangan, bukan sekadar dump datar.

---

## Langkah 5: Tips Lanjutan Excel Automation C# (Excel Automation C#)

Berikut beberapa trik cepat yang dapat Anda tambahkan di atas contoh dasar:

| Tips | Potongan Kode | Kapan Digunakan |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Setelah mengimpor data untuk menghindari teks terpotong. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Saat tabel dapat menggulir melampaui layar. |
| **Conditional Formatting** | <details><summary>Tampilkan</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Sorot gaji di atas ambang tertentu. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Saat Anda memerlukan laporan hanya‑baca. |

Potongan‑potongan ini menunjukkan luasnya **excel automation c#**—Anda dapat terus memperluas workbook tanpa menulis ulang logika impor inti.

---

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika DataTable memiliki ribuan baris?**  
Aspose.Cells menyalurkan data secara efisien, tetapi Anda mungkin ingin menonaktifkan pembuatan style untuk setiap baris demi menghemat memori. Sebagai gantinya, terapkan satu style pada rentang:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Bisakah saya mengekspor ke .csv alih‑alih .xlsx?**  
Tentu—cukup ubah format penyimpanan:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Gaya akan hilang (CSV tidak mendukung styling), tetapi ekspor data tetap sama.

**Apakah ini bekerja di .NET Core?**  
Ya. Aspose.Cells mendukung .NET Standard 2.0 dan yang lebih baru, sehingga kode yang sama berjalan di .NET 6, .NET 7, atau .NET Framework.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}