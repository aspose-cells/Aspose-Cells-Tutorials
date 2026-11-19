---
category: general
date: 2026-11-19
description: Atur format nomor sel di C# dan pelajari cara menerapkan format tanggal
  Excel untuk tanggal era Jepang, memungkinkan konversi tanggal Excel C# yang dapat
  diandalkan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: id
lastmod: 2026-11-19
og_description: Atur format nomor sel di C# dan terapkan format tanggal Excel ke tanggal
  era Jepang. Ikuti panduan lengkap ini untuk konversi tanggal Excel C# yang akurat.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Atur format nomor sel dan konversi tanggal Jepang di C# – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Atur format nomor sel dan konversi tanggal Jepang di C#
url: /id/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur format nomor sel dan konversi tanggal Jepang di C#

Jika Anda perlu **set cell number format** dalam proyek otomatisasi Excel C#, panduan ini menunjukkan cara **apply Excel date format** dan melakukan **C# Excel date conversion** untuk tanggal era Jepang. Anda akan mendapatkan contoh lengkap yang dapat dijalankan yang mengonversi string era Reiwa (mis., `R3/04/01`) menjadi tanggal Gregorian `2021‑04‑01`.

## Apa yang akan Anda pelajari

* Cara membuat workbook dan mengakses worksheet pertama.  
* Cara **set cell number format** sehingga Excel memperlakukan nilai sebagai tanggal.  
* Cara **apply Excel date format** yang mengenali string era Jepang.  
* Cara memicu **C# Excel date conversion** dengan menghitung ulang formula.  
* Output yang diharapkan dan tips pemecahan masalah untuk kasus tepi.

**Prasyarat**

* .NET 6 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.6+).  
* Aspose.Cells untuk .NET 2024 atau yang lebih baru – instal via NuGet: `dotnet add package Aspose.Cells`.  
* Familiaritas dasar dengan C# dan penanganan tanggal Excel.

> **Pro tip:** Aspose.Cells berfungsi tanpa Microsoft Office terpasang, menjadikannya ideal untuk otomatisasi sisi‑server.

## Atur format nomor sel dengan Aspose.Cells di C#

Langkah pertama adalah memberi tahu Excel bahwa sel berisi tanggal. Excel menyimpan tanggal sebagai nomor seri, jadi kita perlu menerapkan format nomor tanggal bawaan (ID 14) ke sel target.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Mengapa ini berhasil

* `Style.Number = 14` memetakan ke format *Short Date* Excel (`mm/dd/yyyy` secara default).  
* Ketika sel berisi string era Jepang seperti `R3/04/01`, parser internal Aspose.Cells mengenali era tersebut dan mengonversinya ke nomor seri Gregorian yang sesuai selama `CalculateFormula()`.  
* Setelah perhitungan, `StringValue` mengembalikan tanggal Gregorian yang diformat.

## Terapkan format tanggal Excel untuk tanggal era Jepang

Jika Anda ingin sel menampilkan era Jepang alih-alih tanggal Gregorian, Anda dapat menggunakan format nomor khusus yang menyertakan kode era. Ini menunjukkan kemampuan **apply excel date format**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` memaksa locale Jepang.  
* `ggg` mewakili nama era (mis., `R` untuk Reiwa).  
* Menambahkan karakter literal (`年`, `月`, `日`) membuat tata letak tanggal Jepang yang familiar.

### Kapan menggunakan format khusus

* Laporan yang ditujukan untuk audiens Jepang.  
* Ketika Anda perlu mempertahankan informasi era asli untuk dokumen hukum.  
* Di dasbor dimana tanggal Gregorian dan era ditampilkan berdampingan.

## Konversi tanggal Excel C# – menangani era Jepang

Proses **c# excel date conversion** dapat dibagi menjadi tiga bagian logis:

1. **Parse the era string** – Aspose.Cells secara otomatis mengenali `R` (Reiwa), `H` (Heisei), `S` (Showa), dll.  
2. **Convert to a serial number** – Excel menyimpan tanggal sebagai hari sejak 1899‑12‑30.  
3. **Format the serial number** – baik dengan format bawaan (ID 14) atau format Jepang khusus.

### Contoh lengkap end‑to‑end

Berikut adalah program mandiri yang menunjukkan output Gregorian dan era dalam satu kali jalankan.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Output konsol yang diharapkan**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Kasus tepi & jebakan umum

| Situation                              | What to watch for                                   | Fix / Recommendation                                   |
|----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
| Empty or malformed era string         | `PutValue` stores the literal text; conversion fails| Validate the input with a regular expression before writing to the cell. |
| Locale mismatch                        | Custom format shows western digits instead of Japanese characters | Ensure the `Custom` format includes `[$-ja-JP]` or set `Workbook.Settings.CultureInfo` to `ja-JP`. |
| Workbook contains formulas referencing the date cell | Recalculation may overwrite formula results | Call `CalculateFormula` **after** all formatting steps, or use `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` if you need to skip errors. |
| Using older Aspose.Cells versions      | Japanese era support was added in 2022 Q3          | Upgrade to the latest NuGet package.                     |

## Menguji solusi

1. **Jalankan program** dari Visual Studio atau `dotnet run`.  
2. Verifikasi bahwa konsol mencetak tanggal Gregorian `2021‑04‑01` dan string era `R3年04月01日`.  
3. Buka workbook yang dihasilkan (jika Anda menambahkan `wb.Save("Demo.xlsx");`) di Microsoft Excel untuk melihat pemformatan yang sama diterapkan pada sel.

### Tips otomatisasi

Jika Anda perlu memproses rentang besar tanggal era (mis., kolom A berisi banyak tanggal Jepang), bungkus logika konversi dalam loop:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Pendekatan ini menjaga operasi **set cell number format** tetap cepat dan efisien memori.

## Kesimpulan

Anda sekarang tahu cara **set cell number format** di C# menggunakan Aspose.Cells, cara **apply Excel date format** untuk string era Jepang, dan cara melakukan **C# Excel date conversion** yang dapat diandalkan dari era ke tanggal Gregorian. Kode lengkap yang dapat dijalankan menunjukkan kedua output dan menyoroti kasus tepi umum.  

**Langkah selanjutnya**

* Jelajahi ID format bawaan lainnya

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [atur format tanggal excel di C# – Panduan Lengkap Langkah‑per‑Langkah](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Cara menerapkan format nomor excel dengan Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Cara menerapkan format nomor khusus excel di C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}