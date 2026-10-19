---
category: general
date: 2026-07-13
description: Cara menggunakan WRAPCOLS di C# untuk mengonversi array menjadi kolom,
  menerapkan formula array di Excel, dan membuat workbook Excel secara programatis—semua
  dengan langkah‑langkah yang jelas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: id
lastmod: 2026-07-13
og_description: Cara menggunakan WRAPCOLS di C# memungkinkan Anda dengan cepat mengubah
  array menjadi kolom, menerapkan formula array gaya Excel, dan mengevaluasi hasilnya
  secara programatik.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: Cara Menggunakan WRAPCOLS di C# – Pembuatan Buku Kerja Excel Cepat
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Cara Menggunakan WRAPCOLS – Panduan Lengkap untuk Otomatisasi Excel dengan
  C#
url: /id/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan WRAPCOLS – Panduan Lengkap untuk Otomatisasi Excel dengan C#

Pernah bertanya‑tanya **bagaimana cara menggunakan WRAPCOLS** ketika Anda perlu mengubah daftar datar menjadi tabel rapi di dalam file Excel yang dihasilkan dari C#? Anda tidak sendirian. Baik Anda sedang membangun mesin pelaporan, mengekspor hasil survei, atau sekadar bermain‑main dengan data, fungsi WRAPCOLS dapat langsung mengubah sebuah array menjadi jumlah kolom yang Anda tentukan.  

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari **membuat workbook Excel secara programatis** hingga **menerapkan formula array ala Excel**, dan akhirnya **mengevaluasi formula dengan C#**. Pada akhir tutorial Anda akan dapat **mengonversi array ke kolom** dalam satu baris kode, tanpa harus melakukan manipulasi sel satu per satu secara manual.

> **Apa yang akan Anda dapatkan:** contoh kode yang dapat dijalankan, penjelasan tiap langkah, tips untuk menghindari jebakan umum, dan saran untuk memperluas solusi.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0+ (atau runtime .NET terbaru)
- IDE C# (Visual Studio, Rider, atau VS Code)
- Perpustakaan **Aspose.Cells for .NET** (versi trial gratis sudah cukup) – ini cara termudah untuk memanipulasi file Excel tanpa harus menginstal Excel.
- Pengetahuan dasar tentang sintaks C# dan formula Excel.

Jika Anda lebih suka perpustakaan lain (misalnya EPPlus atau ClosedXML), konsep dasarnya tetap sama—hanya ganti pemanggilan API saja.

---

## Langkah 1: Siapkan Proyek Anda dan Tambahkan Perpustakaan Excel

Langkah pertama, buat aplikasi console baru dan tambahkan Aspose.Cells melalui NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Gunakan flag `--version` untuk mengunci ke versi stabil tertentu, misalnya `Aspose.Cells 24.9`.

Sekarang buka `Program.cs`. Kita akan mulai dengan menambahkan namespace yang diperlukan:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

Dengan referensi perpustakaan ini, kita dapat **membuat workbook Excel secara programatis** dan bekerja dengan formula.

---

## Langkah 2: Buat Workbook Baru dan Tentukan Sel Target

Selanjutnya, buat instance workbook baru dan pilih sel tempat formula WRAPCOLS akan ditempatkan. Dalam istilah Excel, sel **A1** adalah baris 0, kolom 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Mengapa kita melakukannya? Objek `Workbook` adalah wadah untuk semua sheet, gaya, dan perhitungan. Dengan secara eksplisit merujuk ke sel, kode menjadi lebih jelas dan menghindari “angka ajaib” di kemudian hari.

---

## Langkah 3: Sisipkan Formula Array WRAPCOLS

Berikutnya adalah inti tutorial—**cara menggunakan WRAPCOLS**. Fungsi ini menerima sebuah array dan jumlah kolom, lalu menghasilkan rentang dua dimensi. Dalam sintaks Excel tampilannya seperti ini:

```
=WRAPCOLS({1,2,3,4}, 2)
```

Itu memberi tahu Excel untuk menata angka 1‑4 menjadi **2 kolom**, menghasilkan:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

Untuk menyematkan formula tersebut dari C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Perhatikan bahwa kami menggunakan **string** yang mencerminkan apa yang Anda ketik di bilah formula Excel. Ini adalah langkah **apply array formula excel**, dan Aspose.Cells otomatis memperlakukan ini sebagai formula array karena WRAPCOLS mengembalikan sebuah rentang.

---

## Langkah 4: Paksa Perhitungan Agar Formula Dievaluasi

Excel biasanya menghitung secara malas—hanya saat Anda membuka file. Karena kami ingin membaca hasilnya segera, kita harus memicu perhitungan:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Memanggil `Calculate()` adalah aksi **evaluate excel formula c#** yang memaksa mesin menghitung semua formula, termasuk array WRAPCOLS kita. Tanpa pemanggilan ini, `targetCell.Value` tetap `null`.

---

## Langkah 5: Ambil dan Verifikasi Hasilnya

Setelah workbook dihitung, kita dapat mengambil nilai dari sel‑sel yang ditempati oleh array. Sel paling kiri atas (A1) menyimpan elemen pertama, sementara sel‑sel di sebelahnya berisi sisanya. Mari baca seluruh blok 2 × 2:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

Saat Anda menjalankan program, konsol akan menampilkan:

```
1   3
2   4
```

Output tersebut mengonfirmasi bahwa kita berhasil **convert array to columns** menggunakan WRAPCOLS.

---

## Langkah 6: Simpan Workbook (Opsional tapi Praktis)

Jika Anda ingin membuka file di Excel dan melihat formula secara langsung, cukup simpan:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

Membuka file akan menampilkan formula WRAPCOLS di A1 dan rentang 2‑kolom yang terisi di bawahnya. Langkah ini berguna untuk debugging atau untuk menyerahkan file kepada pengguna akhir.

---

## Pertanyaan Umum & Kasus Khusus

### Bagaimana jika saya membutuhkan lebih dari dua kolom?

Cukup ubah argumen kedua WRAPCOLS. Misalnya, `=WRAPCOLS({1,2,3,4,5,6},3)` akan menghasilkan tiga kolom:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Perbarui baris C# yang bersangkutan:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Bisakah saya memberi rentang dinamis alih‑alih array yang ditulis keras?

Tentu saja. Anda dapat membangun string array secara programatis:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

Dengan cara ini Anda **apply array formula excel** secara dinamis, cocok untuk laporan dengan ukuran data yang bervariasi.

### Bagaimana dengan penanganan error?

Jika formula tidak valid, `Calculate()` akan melempar `CellsException`. Bungkus perhitungan dalam blok try/catch dan catat errornya:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Apakah ini bekerja dengan versi Excel yang lebih lama?

WRAPCOLS diperkenalkan di Excel 365/2021. Saat Anda menyimpan file dalam format `.xls` lama, formula mungkin hilang. Gunakan `.xlsx` jika Anda membutuhkan fungsi ini tetap ada di luar mesin C#.

---

## Contoh Lengkap yang Siap Pakai

Menggabungkan semua bagian, berikut program lengkap yang siap disalin‑tempel:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Jalankan `dotnet run` dan Anda akan melihat matriks tercetak, diikuti konfirmasi bahwa file `.xlsx` telah dibuat.

---

## Ringkasan & Langkah Selanjutnya

Kami telah membahas **cara menggunakan WRAPCOLS** untuk **convert array to columns**, mendemonstrasikan teknik **apply array formula excel** dari C#, memaksa perhitungan untuk **evaluate excel formula c#**, dan menyimpan hasilnya untuk konsumsi lebih lanjut.  

Jika Anda ingin menggali lebih dalam:

- **Jumlah kolom dinamis:** biarkan jumlah kolom menjadi variabel yang dimasukkan pengguna.
- **Styling output:** terapkan font, border, atau conditional formatting lewat Aspose.Cells setelah perhitungan.
- **Menggabungkan dengan fungsi lain:** nest WRAPCOLS di dalam `LET` atau `FILTER`.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut membahas topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Aspose.Cells .NET&#58; Cara Membuat & Menata Workbook Excel Secara Programatis](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cara Membuat Named Ranges yang Scoped pada Workbook di Excel Menggunakan Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}