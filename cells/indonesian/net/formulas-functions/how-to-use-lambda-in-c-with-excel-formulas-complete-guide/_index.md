---
category: general
date: 2026-03-22
description: Cara menggunakan lambda di C# untuk bekerja dengan formula Excel. Pelajari
  cara menulis formula ke sel, mengonversi rentang menjadi array, menampilkan array
  di konsol, dan menghitung kotangen di Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: id
og_description: Cara menggunakan lambda di C# untuk memanipulasi formula Excel, mengonversi
  rentang menjadi array, menulis formula ke sel, menampilkan array di konsol, dan
  menghitung kotangen di Excel.
og_title: Cara Menggunakan Lambda di C# dengan Rumus Excel – Langkah demi Langkah
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Cara Menggunakan Lambda di C# dengan Rumus Excel – Panduan Lengkap
url: /id/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Lambda di C# dengan Rumus Excel – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana cara menggunakan lambda** saat mengotomatisasi Excel dari C#? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus menggabungkan kekuatan fungsi array dinamis baru Excel dengan kemampuan `LAMBDA` di C#. Kabar baiknya? Ini sebenarnya cukup sederhana setelah Anda melihat bagaimana bagian‑bagian tersebut cocok satu sama lain.

Dalam tutorial ini kita akan melangkah melalui **menulis rumus ke sel**, **mengonversi rentang menjadi array**, **menampilkan array tersebut di konsol**, dan bahkan **menghitung kotangen di Excel**—semua sambil menunjukkan **bagaimana cara menggunakan lambda** di dalam pemanggilan `REDUCE`. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dijalankan dan dapat disisipkan ke proyek .NET apa pun yang merujuk ke Aspose.Cells (atau perpustakaan serupa).

---

## Apa yang Akan Anda Pelajari

- Cara **menulis rumus ke sel** menggunakan C#.
- Cara **mengonversi rentang menjadi array** dengan fungsi `EXPAND`.
- Cara **menampilkan array di konsol** setelah perhitungan.
- Cara **menghitung kotangen di Excel** menggunakan `COT` dan `COTH`.
- Sintaks tepat **bagaimana cara menggunakan lambda** di dalam fungsi `REDUCE` Excel dari C#.

> **Prasyarat:** Anda memerlukan versi .NET terbaru (Core 6+ atau .NET Framework 4.7+) dan perpustakaan Aspose.Cells untuk .NET yang diinstal melalui NuGet.

---

## Langkah 1: Siapkan Workbook dan Tulis Rumus ke Sel

Hal pertama yang kita lakukan adalah membuat workbook baru dan mengambil worksheet pertama. Kemudian kita **menulis rumus ke sel** – dalam contoh ini sel `A1` akan menampung hasil pemanggilan `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Mengapa ini penting:** Menulis rumus langsung dari kode berarti Anda dapat menghasilkan spreadsheet kompleks secara dinamis tanpa harus membuka Excel. Ini juga menyiapkan panggung untuk langkah berikutnya di mana kita **mengonversi rentang menjadi array**.

---

## Langkah 2: Mengonversi Rentang menjadi Array dengan EXPAND

`EXPAND` adalah cara Excel mengubah rentang kecil menjadi matriks yang lebih besar. Dengan menempatkan rumus di `A1`, Excel akan menumpahkan blok 4 × 5 yang dimulai dari sel tersebut. Dari C#, kita tidak perlu menyalin nilai secara manual – perpustakaan akan melakukan pekerjaan berat ketika kita memanggil `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Bagaimana cara menggunakan lambda:** Belum, tapi tunggu dulu. Pertama kita butuh data di lembar, kemudian kita akan mereduksinya dengan lambda.

---

## Langkah 3: Gunakan LAMBDA di Dalam REDUCE – Inti dari “Cara Menggunakan Lambda”

Excel 365 memperkenalkan `REDUCE`, yang menerima **nilai awal**, **rentang**, dan **LAMBDA** yang menentukan cara menggabungkan setiap elemen. Dari C# kita cukup menetapkan string rumus; lambda berada di dalam rumus Excel, bukan di kode C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Penjelasan:**  
- `0` adalah akumulator awal (`acc`).  
- `A1:D4` adalah rentang yang ingin kita proses (empat kolom pertama dari spill).  
- `LAMBDA(acc, x, acc + x)` memberi tahu Excel untuk menambahkan setiap sel (`x`) ke akumulator.  

Itulah esensi **bagaimana cara menggunakan lambda** untuk agregasi dalam konteks spreadsheet.

---

## Langkah 4: Hitung Kotangen di Excel – Dari Derajat ke Hiperbolik

Jika Anda membutuhkan hasil trigonometri, fungsi `COT` dan `COTH` Excel sangat mudah digunakan. Kita akan menempatkannya di `G1` dan `G2` masing‑masing.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Mengapa ini berguna:** Mengetahui **cara menghitung kotangen di Excel** dapat menghemat Anda dari menulis kode matematika khusus, terutama ketika workbook akan dibagikan kepada non‑developer.

---

## Langkah 5: Paksa Perhitungan dan Ambil Array yang Diperluas

Sekarang kita memberi tahu workbook untuk mengevaluasi setiap rumus, lalu mengambil array yang ditumpahkan dari `A1`. Di sinilah kita **menampilkan array di konsol**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Apa yang akan Anda lihat:**  
- Matriks 4 × 5 yang diformat rapi, dicetak baris per baris.  
- Jumlah yang dihitung oleh lambda `REDUCE`.  
- Dua nilai kotangen.

Itulah alur lengkap dari **menulis rumus ke sel** hingga **menampilkan array di konsol**.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut adalah seluruh program yang dapat Anda tempel ke aplikasi console. Ingat untuk menambahkan paket NuGet `Aspose.Cells` terlebih dahulu (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Output console yang diharapkan (nilai dapat berbeda tergantung isi default B1:C2, yang secara default 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Silakan isi `B1:C2` dengan angka pilihan Anda sebelum menjalankan – matriks akan mencerminkan nilai‑nilai tersebut.

---

## Tips Pro & Kesalahan Umum

- **Tip pro:** Jika Anda ingin rentang yang ditumpahkan mulai dari sel lain, cukup ubah sel target (`A1`). Fungsi `EXPAND` menghormati anchor tersebut.  
- **Waspada:** Sel kosong di rentang sumber menjadi `0` dalam array yang ditumpahkan, yang dapat memengaruhi jumlah `REDUCE` Anda.  
- **Kasus tepi:** Ketika workbook berisi rumus yang bergantung pada fungsi volatil (misalnya `NOW()`), panggil `workbook.Calculate()` setelah menetapkan semua rumus untuk memastikan semuanya up‑to‑date.  
- **Catatan kinerja:** Untuk spill yang sangat besar, pertimbangkan membatasi ukuran dalam pemanggilan `EXPAND`; jika tidak, Anda mungkin mengalokasikan memori lebih banyak dari yang diperlukan.  
- **Kompatibilitas:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}