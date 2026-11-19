---
category: general
date: 2026-11-19
description: Atur format mata uang di Excel dengan C# – pelajari cara mengatur format
  angka dan gaya kolom Excel saat mengimpor lembar kerja Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: id
lastmod: 2026-11-19
og_description: Atur format mata uang di Excel dengan C# dan temukan cara mengatur
  format angka, menetapkan format angka, serta menata kolom Excel saat mengimpor lembar
  kerja Excel.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Atur format mata uang di Excel dengan C# – panduan lengkap langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Atur format mata uang saat mengimpor data ke Excel menggunakan C#
url: /id/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur format mata uang saat mengimpor data ke Excel menggunakan C#

Jika Anda perlu **mengatur format mata uang** dalam lembar kerja Excel, panduan ini menunjukkan cara **mengatur format angka** dan menata kolom saat melakukan **impor lembar kerja Excel**. Anda akan melihat contoh lengkap yang dapat dijalankan yang menetapkan format angka yang tepat untuk setiap kolom dari `DataTable` dan mengimpor data dengan gaya yang diinginkan.

Bekerja dengan Excel dari C# sering memerlukan lebih dari sekadar menuliskan nilai mentah—Anda juga harus mengontrol bagaimana angka ditampilkan. Baik Anda membuat faktur, laporan keuangan, atau dasbor, memformat mata uang, persentase, atau tanggal dengan benar membuat output langsung dapat dibaca.

## Prasyarat

* .NET 6.0 (atau lebih baru) terpasang.
* Referensi ke **Aspose.Cells for .NET** (atau perpustakaan apa pun yang menyediakan kelas `Style` dengan properti `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Familiaritas dasar dengan `DataTable` dan koleksi C#.
* Sebuah IDE seperti Visual Studio 2022 atau VS Code.

## Langkah 1: Ambil data yang akan ditulis ke lembar kerja

Pertama dapatkan sebuah `DataTable` yang berisi data mentah yang ingin Anda ekspor. Pada proyek nyata, ini bisa berasal dari kueri basis data, panggilan API, atau parser CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Mengapa ini penting:** Mengimpor `DataTable` yang sepenuhnya terisi memungkinkan Anda memisahkan logika pengambilan data dari logika pembuatan Excel, yang meningkatkan kemampuan pengujian dan pemeliharaan.

## Langkah 2: Buat array gaya – satu entri per kolom dalam DataTable

Aspose.Cells mengharapkan sebuah `Style[]` yang panjangnya sesuai dengan jumlah kolom yang akan Anda impor. Setiap elemen dapat menyimpan format angka tertentu.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Tip profesional:** Bahkan jika Anda hanya membutuhkan pemformatan untuk sebagian kolom, Anda tetap harus membuat instance `Style` untuk setiap kolom; jika tidak, Anda akan mendapatkan `NullReferenceException` saat impor.

## Langkah 3: Tetapkan format angka ke kolom yang diinginkan

Nomor gaya bawaan berbeda per perpustakaan. Pada Aspose.Cells:

* `0` → General (integer)  
* `2` → Currency (misalnya `$#,##0.00`)  
* `3` → Date, dll.

Di sini kami **menetapkan format angka** ke dua kolom: kolom pertama (Id) tetap sebagai integer, sementara kolom kedua (Amount) menerima format mata uang.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Cara mengatur format angka**: Menggunakan properti `Number` adalah cara tercepat untuk memilih format bawaan. Untuk mata uang yang spesifik locale, pertimbangkan menggunakan string format khusus yang menyertakan simbol mata uang yang sesuai.

## Langkah 4: Impor DataTable ke lembar kerja, menerapkan gaya kolom

Sekarang array gaya sudah siap, impor data. Metode `ImportDataTable` menghormati gaya yang Anda berikan.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Hasil yang diharapkan

Saat Anda membuka **FinancialReport.xlsx**, Anda akan melihat:

| Id | Jumlah      | Deskripsi          |
|----|------------|--------------------|
| 1  | $1,234.56  | Perlengkapan kantor |
| 2  | $98,765.43 | Biaya konsultasi   |
| 3  | $0.99      | Lain-lain          |

*Kolom **Jumlah** ditampilkan menggunakan format mata uang yang Anda atur, sementara **Id** tetap berupa integer.*

## Cara mengatur format angka untuk skenario tambahan

### Tetapkan format angka ke kolom tanggal

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Gunakan format angka khusus untuk persentase

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Penataan di luar format angka

Anda juga dapat mengatur font, warna latar belakang, atau perataan pada objek `Style` yang sama:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Mengapa ini berhasil:** Objek `Style` menggabungkan semua properti visual untuk sebuah sel. Ketika Anda mengirimkan array ke `ImportDataTable`, setiap sel secara otomatis mewarisi gaya yang telah ditentukan.

## Kesalahan umum dan cara menghindarinya

| Kesalahan | Gejala | Solusi |
|-----------|--------|--------|
| Lupa menginstansiasi setiap `Style` | `NullReferenceException` saat impor | Loop melalui array dan panggil `CreateStyle()` sebelum mengatur properti. |
| Menggunakan indeks angka bawaan yang salah | Format salah (misalnya, tanggal muncul sebagai integer) | Lihat dokumentasi perpustakaan untuk konstanta `Number` yang benar. |
| Tidak menyimpan workbook | Tidak ada file output atau file kosong | Panggil `workbook.Save(...)` setelah impor selesai. |
| Ketidaksesuaian locale untuk simbol mata uang | `$` muncul bahkan di locale non‑US | Gunakan string format khusus dengan simbol yang sesuai (misalnya, `"€#,##0.00"`). |

## Contoh lengkap yang dapat dijalankan



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat file excel c# – gaya sel dan atur format mata uang](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Cara Memformat Kolom Excel di C# – Panduan Lengkap](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Buat Workbook Excel C# – Terapkan Format Mata Uang dan Impor DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}