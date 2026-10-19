---
category: general
date: 2026-06-24
description: Terapkan formula array Excel menggunakan C#. Pelajari cara menyimpan
  file Excel dengan C# dan membuat workbook Excel dengan C# menggunakan fungsi Expand
  serta menghasilkan file Excel dengan formula.
draft: false
keywords:
- apply array formula excel
- save excel file c#
- create excel workbook c#
- use expand function excel
- generate excel file with formulas
language: id
og_description: Terapkan formula array Excel di C# dan pelajari cara menyimpan file
  Excel C# dengan cepat. Panduan ini menunjukkan cara membuat workbook Excel C# dan
  menggunakan fungsi expand Excel.
og_title: Menerapkan Formula Array Excel di C# – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  headline: Apply Array Formula Excel in C# – Complete Guide
  type: TechArticle
- description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  name: Apply Array Formula Excel in C# – Complete Guide
  steps:
  - name: What if the target folder doesn’t exist?
    text: '`Workbook.Save` will throw a `DirectoryNotFoundException`. A quick fix
      is to ensure the directory exists before calling `Save`:'
  - name: Can I apply the array formula to a range other than A1?
    text: 'Absolutely. Just change the cell address:'
  - name: Does the calculation engine respect Excel’s precision settings?
    text: Aspose.Cells follows IEEE‑754 double‑precision arithmetic, which matches
      Excel’s default. If you need custom precision, you can tweak the `CalculationOptions`
      object before calling `CalculateFormula`.
  - name: What about older Excel versions that don’t support `EXPAND`?
    text: 'If you need backward compatibility, replace `EXPAND` with a combination
      of `INDEX` and `SEQUENCE` or simply write the values directly via C# loops.
      The library also lets you write values without formulas:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Menerapkan Formula Array Excel di C# – Panduan Lengkap
url: /id/net/excel-formulas-and-calculation-options/apply-array-formula-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Formula Array Excel di C# – Tutorial Pemrograman Lengkap

Pernah membutuhkan **apply array formula excel** tetapi tidak yakin cara melakukannya dari kode C#? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mencoba menghasilkan spreadsheet yang berisi formula array dinamis seperti `EXPAND` atau `COT`.  

Dalam tutorial ini kami akan membahas contoh langsung yang **creates an excel workbook c#**, menyisipkan formula array, menggunakan fungsi `EXPAND`, dan akhirnya **save excel file c#** sehingga Anda dapat membukanya di Excel dan melihat hasilnya. Pada akhir tutorial Anda juga akan mengetahui cara **generate excel file with formulas** secara siap produksi.

> **Pro tip:** Pendekatan yang ditunjukkan di sini bekerja dengan versi Excel terbaru yang mendukung fungsi array dinamis (Office 365, Excel 2021+). Jika Anda memerlukan kompatibilitas mundur, Anda harus kembali ke teknik formula lama.

![Tangkapan layar Excel yang menampilkan hasil formula array – apply array formula excel](apply-array-formula-excel.png)

*(Teks alt gambar: apply array formula excel – tangkapan layar buku kerja Excel dengan formula array dinamis)*

## Apa yang Anda Butuhkan

- **.NET 6+** (atau runtime .NET terbaru) – kode ini dapat dikompilasi dengan .NET Core dan .NET Framework secara bersamaan.  
- **Aspose.Cells for .NET** (versi percobaan gratis atau berlisensi). Perpustakaan ini memungkinkan Anda memanipulasi file Excel tanpa harus menginstal Excel.  
- IDE favorit (Visual Studio, Rider, VS Code).  
- Pengetahuan dasar C# – tidak perlu yang rumit, cukup untuk mengikuti kode.

Jika Anda sudah memiliki semua itu, bagus – mari kita mulai.

---

## Langkah 1 – Apply Array Formula Excel: Buat Workbook

Hal pertama yang kami lakukan adalah **create excel workbook c#** menggunakan Aspose.Cells. Ini memberi kami objek workbook bersih yang kemudian dapat diisi dengan formula.

```csharp
using System;
using Aspose.Cells;

namespace ExcelArrayFormulaDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new workbook
            Workbook workbook = new Workbook();

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

> **Mengapa ini penting:** Membuat objek `Workbook` adalah titik masuk untuk setiap otomatisasi Excel. Ia mewakili seluruh file, dan lembar kerja pertama adalah tempat yang nyaman untuk mulai menguji formula.

---

## Langkah 2 – Use Expand Function Excel untuk Mengisi Array

Sekarang kami **use expand function excel** untuk mengubah array statis sederhana `{1,2,3}` menjadi tumpahan vertikal sebanyak lima baris. Fungsi `EXPAND` merupakan bagian dari mesin array dinamis Excel dan secara otomatis mengisi rentang.

```csharp
            // Set a formula that expands an array into 5 rows, 1 column
            // The formula will spill into A1:A5
            worksheet.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";
```

> **Penjelasan:**  
> - `{1,2,3}` adalah konstanta array literal.  
> - `5` memberi tahu Excel untuk mengembalikan lima baris, sementara `1` menjaga agar tetap satu kolom.  
> - Saat Anda membuka file, sel A1 hingga A5 akan menampilkan `1, 2, 3, 0, 0` (baris tambahan diisi dengan nol).

---

## Langkah 3 – Tambahkan Formula Matematika Klasik (Cotangent)

Array dinamis bukan satu‑satunya formula yang dapat Anda sisipkan. Mari juga **generate excel file with formulas** yang menghitung cotangent dari π/4. Ini menunjukkan bahwa formula biasa dapat bekerja berdampingan dengan yang dinamis.

```csharp
            // Set a formula that calculates the cotangent of π/4 (≈1)
            worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Mengapa menyertakan ini?** Ini menunjukkan bahwa Anda dapat mencampur fungsi lama dan baru tanpa konfigurasi tambahan. Fungsi `COT` tersedia di semua versi Excel modern.

---

## Langkah 4 – Hitung Ulang Semua Formula di Workbook

Aspose.Cells tidak secara otomatis mengevaluasi formula saat Anda menetapkannya. Anda perlu memberi tahu mesin untuk **recalculate** sebelum menyimpan, jika tidak file hanya akan berisi formula mentah.

```csharp
            // Force calculation of all formulas
            workbook.CalculateFormula();
```

> **Apa yang terjadi di balik layar?** Perpustakaan ini mem-parsing setiap formula, membangun pohon ekspresi, dan mengevaluasinya menggunakan mesin perhitungan miliknya sendiri. Langkah ini penting jika Anda ingin file yang dihasilkan menampilkan nilai segera setelah dibuka.

---

## Langkah 5 – Save Excel File C# – Simpan Hasil

Akhirnya kami **save excel file c#** ke disk. Anda dapat memilih folder mana saja; pastikan aplikasi memiliki izin menulis.

```csharp
            // Define the output path (adjust as needed)
            string outputPath = @"C:\Temp\output.xlsx";

            // Save the workbook – this writes the calculated values into the file
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Saat Anda membuka `output.xlsx` di Excel, Anda akan melihat:

| A   | B |
|-----|---|
| 1   | 1 |
| 2   |   |
| 3   |   |
| 0   |   |
| 0   |   |

- Kolom **A** menampilkan array yang tumpah yang dihasilkan oleh `EXPAND`.  
- Sel **B1** menampilkan `1`, hasil dari `COT(π/4)`.

Itulah alur kerja lengkap **generate excel file with formulas**.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika folder target tidak ada?

`Workbook.Save` akan melempar `DirectoryNotFoundException`. Solusi cepat adalah memastikan direktori ada sebelum memanggil `Save`:

```csharp
if (!System.IO.Directory.Exists(System.IO.Path.GetDirectoryName(outputPath)))
{
    System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath));
}
```

### Bisakah saya menerapkan formula array ke rentang selain A1?

Tentu saja. Cukup ubah alamat sel:

```csharp
worksheet.Cells["D4"].Formula = "=EXPAND({10,20,30},3,1)";
```

Tumpahan akan dimulai di D4 dan mengisi D4:D6.

### Apakah mesin perhitungan menghormati pengaturan presisi Excel?

Aspose.Cells mengikuti aritmetika double‑precision IEEE‑754, yang cocok dengan default Excel. Jika Anda memerlukan presisi khusus, Anda dapat menyesuaikan objek `CalculationOptions` sebelum memanggil `CalculateFormula`.

```csharp
var options = new CalculationOptions { PrecisionAsDisplayed = true };
workbook.CalculateFormula(options);
```

### Bagaimana dengan versi Excel lama yang tidak mendukung `EXPAND`?

Jika Anda memerlukan kompatibilitas mundur, gantikan `EXPAND` dengan kombinasi `INDEX` dan `SEQUENCE` atau cukup tulis nilai secara langsung melalui loop C#. Perpustakaan juga memungkinkan Anda menulis nilai tanpa formula:

```csharp
object[] values = { 1, 2, 3, 0, 0 };
for (int i = 0; i < values.Length; i++)
{
    worksheet.Cells[i, 0].PutValue(values[i]); // Column A
}
```

---

## Tips Pro untuk Bekerja dengan Formula di C#

- **Perhitungan batch:** Jika Anda menyisipkan ratusan formula, panggil `CalculateFormula` sekali setelah semua penyisipan. Ini mengurangi beban CPU.  
- **Hindari fungsi volatile:** Fungsi seperti `NOW()` menghitung ulang setiap kali dibuka, yang dapat memperlambat workbook besar.  
- **Gunakan named ranges:** Mereka membuat formula lebih mudah dibaca dan dipelihara, terutama saat Anda menghasilkan mereka secara programatis.  
- **Jaga perpustakaan tetap terbaru:** Rilis Aspose.Cells sering menyertakan perbaikan kinerja dan dukungan untuk fungsi Excel baru (mis., `XLOOKUP`, `FILTER`).  

---

## Ringkasan – Apa yang Telah Kami Bahas

Kami memulai dengan **apply array formula excel** pada workbook baru, kemudian **use expand function excel** untuk menumpahkan array statis ke lima baris. Selanjutnya kami menambahkan perhitungan klasik `COT`, memaksa perhitungan ulang penuh, dan akhirnya **save excel file c#** ke disk. Hasilnya adalah spreadsheet siap‑buka yang menunjukkan perilaku array dinamis serta evaluasi formula biasa – fondasi yang kuat untuk proyek **generate excel file with formulas** apa pun.

---

## Langkah Selanjutnya

- **Gaya output:** Terapkan font, border, atau pemformatan bersyarat melalui Aspose.Cells untuk membuat lembar tampak rapi.  
- **Tambahkan diagram:** Gunakan API diagram perpustakaan untuk memvisualisasikan data array secara otomatis.  
- **Ekspor ke format lain:** Workbook yang sama dapat disimpan sebagai CSV, PDF, atau HTML dengan satu pemanggilan metode (`workbook.Save("output.pdf")`).  
- **Integrasikan ke ASP.NET:** Sajikan file yang dihasilkan langsung kepada pengguna melalui endpoint API web.

Silakan bereksperimen—ganti `EXPAND` dengan `SEQUENCE`, coba tumpahan multi‑kolom, atau hasilkan seluruh dasbor secara programatis. Tidak ada batasnya ketika Anda tahu cara **apply array formula excel** dari C#.

Selamat coding! 🚀

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Simpan File Excel Aspose Cells .NET](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Cara Menyimpan Halaman Tertentu dari File Excel sebagai PDF Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}