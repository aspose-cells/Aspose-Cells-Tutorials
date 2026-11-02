---
category: general
date: 2026-07-13
description: Format kolom tanggal di Excel saat mengekspor DataTable dari C#. Pelajari
  cara mengekspor DataTable ke Excel dengan C# dan mengimpor DataTable ke Excel dengan
  styling dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: id
lastmod: 2026-07-13
og_description: Format kolom tanggal di Excel dengan mudah. Panduan ini menunjukkan
  cara mengekspor datatable ke Excel dengan C# dan mengimpor datatable ke Excel dengan
  gaya khusus.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Format Kolom Tanggal Excel – Tutorial Ekspor C# Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Format Kolom Tanggal Excel – Panduan Lengkap C# untuk Mengekspor DataTable
url: /id/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Format Kolom Tanggal Excel – Panduan Lengkap C# untuk Mengekspor DataTable

Pernahkah Anda perlu **format date column Excel** saat menarik data dari database, tetapi sel-selnya terus menampilkan timestamp mentah? Anda bukan satu-satunya. Dalam banyak aplikasi bisnis, ekspor default menghasilkan nilai `DateTime` seperti `2024‑03‑15 00:00:00` dan tidak ada yang menginginkan kekacauan itu.  

Kabar baiknya, Anda dapat mengontrol tampilan tepat setiap kolom langsung dari C#. Dalam tutorial ini kami akan membahas solusi end‑to‑end yang **excel export datatable c#**, menerapkan gaya tanggal pada kolom pertama, gaya mata uang pada kolom kedua, dan akhirnya **import datatable to excel** dengan styling tanpa kesulitan.

Pada akhir tutorial, Anda akan memiliki metode yang dapat digunakan kembali yang dapat Anda sisipkan ke proyek .NET mana pun, terlepas apakah Anda menggunakan .NET 6, .NET Framework 4.8, atau versi yang lebih baru.

---

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (atau perpustakaan apa pun yang menyediakan `CreateStyle` dan `ImportDataTable`). Potongan kode menggunakan Aspose karena API‑nya bersih dan banyak diadopsi.
- Sebuah **DataTable** yang sudah Anda isi dari SQL, CSV, atau sumber lain.
- Visual Studio (atau IDE favorit Anda).  
- Runtime .NET 5.0+ (contoh menargetkan .NET 6, tetapi kerangka kerja yang lebih lama berfungsi sama).

Jika Anda belum memiliki Aspose.Cells, dapatkan percobaan gratis dari situs resmi—tanpa kartu kredit diperlukan.

---

## Langkah 1: Ambil Data Sumber sebagai DataTable

Pertama-tama, Anda memerlukan sebuah `DataTable`. Dalam skenario dunia nyata biasanya data ini berasal dari `SqlDataAdapter.Fill`, tetapi demi kejelasan kami akan membuat tabel sederhana secara mock:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Pro tip:** Saat Anda menarik data langsung dari prosedur tersimpan, pastikan tipe kolom cocok dengan format Excel yang diinginkan. Kolom `datetime` nanti akan menjadi target untuk gaya **format date column excel** kami.

---

## Langkah 2: Buat Workbook Excel dan Tentukan Gaya Kolom

Sekarang kita membuat workbook baru. Trik untuk **format date column excel** terletak pada pembuatan objek `Style`, mengatur properti `Number`‑nya ke format tanggal bawaan Excel (kode 14), dan menugaskan gaya tersebut ke indeks kolom yang tepat.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Mengapa `Number = 14`? Excel menyimpan tanggal sebagai nomor seri; format 14 memberi tahu program untuk menampilkan nomor‑nomor tersebut menggunakan pola tanggal pendek locale. Jika Anda memerlukan pola khusus (misalnya `dd‑MMM‑yyyy`), Anda dapat mengatur `columnStyles[0].Custom = "dd-MMM-yyyy"` sebagai gantinya.

---

## Langkah 3: Impor DataTable ke Worksheet dengan Gaya

Dengan array gaya siap, pemanggilan impor cukup satu baris. Inilah inti dari **excel export datatable c#** dan juga tempat kami **import datatable to excel** sambil mempertahankan format kami.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

Overload `ImportDataTable` yang kami gunakan menerima array gaya, menerapkan setiap gaya ke kolom yang bersesuaian saat data ditulis. Tidak diperlukan loop pasca‑proses—kolom tanggal Anda sudah diformat dengan cantik.

---

## Langkah 4: Simpan Workbook (atau Stream Langsung ke Browser)

Tergantung pada skenario, Anda mungkin menyimpan ke disk, memory stream, atau mengembalikan file sebagai respons HTTP. Berikut tiga pola umum:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Watch out for:** Jika Anda menggunakan `FileResult` di ASP.NET Core, pastikan mengatur `Response.Headers["Cache-Control"] = "no-cache"` saat file dihasilkan secara dinamis. Ini mencegah browser menyajikan versi usang.

---

## Langkah 5: Verifikasi Hasil – Tampilan Sheet Excel

Setelah menjalankan kode, buka `ExportedReport.xlsx`. Anda akan melihat:

| Tanggal Pesanan (diformat) | TotalAmount (mata uang) | Pelanggan |
|----------------------------|--------------------------|-----------|
| 03/13/2024                 | $1,245.67                | Acme Corp |
| 03/14/2024                 | $980.00                  | Beta Ltd  |
| 03/15/2024                 | $1,500.25                | Gamma Inc |

![format date column excel – tangkapan layar lembar Excel dengan kolom tanggal yang diformat dengan benar](/images/format-date-column-excel.png)

* *Teks alt gambar: format date column excel – tangkapan layar lembar Excel dengan kolom tanggal yang diformat dengan benar.*

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana Jika DataTable Saya Memiliki Lebih Dari Tiga Kolom?

Cukup perpanjang array `columnStyles`. Untuk kolom mana pun yang tidak Anda beri gaya secara eksplisit, biarkan entri `null`; Excel akan menerapkan format General default.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Bagaimana Cara Menerapkan Format Tanggal Kustom (misalnya “dd‑MMM‑yyyy”)?

Ganti nomor bawaan dengan string kustom:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Bisakah Saya Menggunakan Pendekatan Ini dengan EPPlus atau ClosedXML?

Ya, konsepnya identik: buat objek gaya, tugaskan ke kolom, lalu muat `DataTable`. API‑nya berbeda, tetapi pola **excel export datatable c#** tetap sama.

### Bagaimana Dengan DataSet Besar (100k+ baris)?

`ImportDataTable` dioptimalkan untuk penulisan massal, tetapi Anda mungkin menemui batas memori. Dalam kasus tersebut, pertimbangkan streaming baris dengan `Cells.ImportDataTable` secara bertahap, atau gunakan `Worksheet.Cells["A1"].PutValue` dalam loop sambil menggunakan kembali objek gaya.

---

## Contoh Lengkap yang Berfungsi (Semua Langkah dalam Satu Metode)

Berikut adalah metode mandiri yang dapat Anda copy‑paste ke aplikasi console atau controller ASP.NET mana pun. Metode ini mendemonstrasikan alur lengkap—dari pengambilan data hingga ekspor Excel ber‑gaya.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Jalankan program, buka `StyledExport.xlsx`, dan Anda akan melihat **format date column excel** diterapkan dengan sempurna.

---

## Ringkasan & Langkah Selanjutnya

Kami baru saja membahas cara **format date column excel** saat melakukan **excel export datatable c#**, dan cara **import datatable to excel** dengan styling per‑kolom dalam satu panggilan. Poin penting yang harus diingat:

1. Buat `Style` per kolom yang ingin Anda format.  
2. Gunakan `Number = 14` untuk tanggal, `Number = 2` untuk mata uang, atau format kustom apa pun yang Anda perlukan.  
3. Kirimkan array gaya ke `ImportDataTable`—perpustakaan akan melakukan pekerjaan berat.

Apa yang dapat Anda eksplorasi selanjutnya?

- **Conditional formatting** untuk menyorot tanggal yang lewat tempo.  
- **

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengimpor DataTable ke Excel Menggunakan Aspose.Cells untuk .NET (Panduan Langkah-demi-Langkah)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Ekspor Data Excel ke DataTable Menggunakan Aspose.Cells untuk .NET: Panduan Lengkap](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Ekspor String HTML dari Excel ke DataTable menggunakan Aspose.Cells untuk .NET: Panduan Langkah-demi-Langkah](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}