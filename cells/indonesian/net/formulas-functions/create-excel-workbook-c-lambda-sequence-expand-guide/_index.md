---
category: general
date: 2026-03-30
description: Buat workbook Excel C# menggunakan Aspose.Cells. Pelajari cara menerapkan
  fungsi lambda di Excel, fungsi sequence di Excel, memperluas array di Excel, dan
  menyimpan workbook sebagai xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: id
og_description: Buat workbook Excel C# dengan cepat. Panduan ini menunjukkan cara
  menggunakan fungsi lambda Excel, fungsi sequence Excel, memperluas array Excel,
  dan menyimpan workbook sebagai xlsx.
og_title: Buat Workbook Excel C# – Panduan Lambda, SEQUENCE & EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat Workbook Excel C# – Panduan Lambda, SEQUENCE & EXPAND
url: /id/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel C# – Panduan LAMBDA, SEQUENCE & EXPAND

Pernah perlu **membuat workbook Excel C#** untuk laporan otomatis, tetapi tidak yakin panggilan API mana yang harus digunakan? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat pertama kali menyelami pembuatan Excel secara programatik. Dalam panduan ini Anda akan melihat contoh lengkap yang dapat dijalankan yang mencakup semuanya mulai dari **fungsi SEQUENCE Excel** baru hingga **fungsi LAMBDA Excel** yang kuat, dan bahkan cara **memperluas array Excel**.  

Kami juga akan menunjukkan langkah‑langkah tepat untuk **menyimpan workbook sebagai xlsx** sehingga Anda dapat memberikan file tersebut kepada siapa saja yang menggunakan Excel. Pada akhir tutorial ini Anda akan memiliki potongan kode siap produksi yang dapat Anda sisipkan ke proyek .NET apa pun. Tidak ada tautan “lihat dokumentasi” yang samar—hanya kode yang berfungsi hari ini.

## Apa yang Anda Butuhkan

- **.NET 6.0 atau lebih baru** – contoh ini menargetkan .NET 6, tetapi versi terbaru lainnya juga dapat digunakan.  
- **Aspose.Cells untuk .NET** – instal melalui NuGet (`Install-Package Aspose.Cells`).  
- Pemahaman dasar tentang sintaks C# (variabel, objek, dan ekspresi lambda).  
- IDE yang Anda sukai (Visual Studio, Rider, atau VS Code).  

Itu saja. Tidak ada interop COM tambahan, tidak ada Office yang harus diinstal di server—Aspose.Cells menangani semuanya di memori.

## Membuat Workbook Excel C# – Implementasi Langkah‑per‑Langkah

Di bawah ini kami memecah proses menjadi langkah‑langkah kecil. Setiap langkah memiliki judul yang jelas, cuplikan kode singkat, dan penjelasan **mengapa** kami melakukannya. Silakan salin blok lengkap di akhir dan jalankan sebagai aplikasi konsol.

### Langkah 1 – Inisialisasi Workbook Baru

Hal pertama yang harus dilakukan: kita membutuhkan objek workbook kosong yang mewakili file Excel di memori.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Mengapa ini penting:* `Workbook` adalah titik masuk untuk semua operasi Aspose.Cells. Dengan mengambil `Worksheet` pertama kita mendapatkan kanvas tempat kita dapat menulis formula, nilai, atau format.  

> **Tip pro:** Jika Anda memerlukan beberapa lembar, cukup panggil `workbook.Worksheets.Add()` dan simpan referensi ke masing‑masing.

### Langkah 2 – Gunakan Fungsi SEQUENCE Excel untuk Menghasilkan Data

**fungsi sequence excel** membuat array dinamis berisi angka tanpa VBA. Kami akan menaruhnya di sel `A1` dan membiarkan Excel memperluasnya secara otomatis.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Mengapa ini penting:* `SEQUENCE(3)` menghasilkan `[1,2,3]`. Membungkusnya dengan `EXPAND` memaksa hasilnya menjadi rentang 5 baris, mengisi baris tambahan dengan kosong. Ini memperlihatkan **fungsi sequence excel** dan **expand array excel** sekaligus.

### Langkah 3 – Gabungkan Angka dengan Fungsi LAMBDA Excel

Sekarang mari tunjukkan kemampuan **fungsi lambda excel**. Kami akan menjumlahkan angka 1‑5 menggunakan fungsi `REDUCE` baru, yang secara internal mengandalkan lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Mengapa ini penting:* `REDUCE` mengiterasi array yang dihasilkan oleh `SEQUENCE(5)`, memberi setiap elemen (`b`) ke lambda bersama akumulator (`a`). Lambda `a+b` menambahkan mereka, menghasilkan `15` di `B1`. Ini adalah cara bersih berbasis formula untuk melakukan reduksi tanpa loop di C#.

### Langkah 4 – Terapkan Fungsi Trigonometri Langsung di Sel

Fungsi matematika bawaan Excel berguna untuk perhitungan cepat. Kami akan menaruh cotangent dan hyperbolic cotangent di sel yang berdekatan.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Mengapa ini penting:* Menunjukkan bahwa Anda dapat mencampur fungsi matematika klasik dengan formula array dinamis yang lebih baru. Tidak perlu menghitung nilai ini di C# kecuali Anda memiliki alasan performa khusus.

### Langkah 5 – Hitung Semua Formula

Aspose.Cells tidak secara otomatis mengevaluasi formula saat Anda menetapkannya. Anda harus memintanya untuk menghitung.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Mengapa ini penting:* Setelah pemanggilan ini, properti `Value` setiap sel berisi hasil yang telah dievaluasi, siap untuk disimpan atau dibaca kembali.

### Langkah 6 – Simpan Workbook sebagai Xlsx

Akhirnya, kami menyimpan workbook ke disk menggunakan pola **save workbook as xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Mengapa ini penting:* Metode `Save` secara otomatis mendeteksi ekstensi file. Dengan menggunakan “.xlsx” kami memastikan file kompatibel dengan versi Excel modern. Path mengarah ke desktop untuk memudahkan akses selama pengujian.

### Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda tempel ke proyek konsol baru. Ia mencakup semua langkah di atas, plus blok verifikasi kecil yang mencetak nilai yang dihitung ke konsol.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Output yang diharapkan di konsol**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

Dan ketika Anda membuka *NewFunctions.xlsx* Anda akan melihat angka yang sama tertata di empat kolom pertama.

![tangkapan layar membuat workbook excel c# dari spreadsheet yang dihasilkan](/images/create-excel-workbook-csharp.png)

## Kasus Pojok, Tips, dan Pertanyaan Umum

- **Bagaimana jika saya membutuhkan lebih dari satu lembar?**  
  Cukup panggil `workbook.Worksheets.Add()` dan ulangi penetapan formula pada setiap objek `Worksheet` baru.  

- **Apakah saya dapat menggunakan versi Excel yang lebih lama?**  
  Fungsi array dinamis (`SEQUENCE`, `EXPAND`, `REDUCE`) memerlukan Excel 365 atau Excel 2021+. Jika Anda menargetkan versi yang lebih lama, gunakan formula klasik atau hitung nilai di C# sebelum menuliskannya.  

- **Kekhawatiran performa?**  
  Untuk ribuan baris, menetapkan formula pada sebuah rentang lalu memanggil `CalculateFormula` biasanya lebih cepat daripada melakukan loop dan menetapkan nilai satu‑per‑satu.  

- **Menyimpan ke stream alih‑alih file?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}