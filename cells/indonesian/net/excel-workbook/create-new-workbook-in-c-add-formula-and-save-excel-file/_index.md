---
category: general
date: 2026-02-23
description: Buat buku kerja baru secara programatis di C# dan tambahkan rumus ke
  sebuah sel. Pelajari cara menggunakan EXPAND, lalu simpan buku kerja Excel dengan
  mudah.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: id
og_description: Buat buku kerja baru secara programatis di C#. Tambahkan formula ke
  sel, pelajari cara menggunakan EXPAND, dan simpan buku kerja Excel dalam hitungan
  detik.
og_title: Buat Workbook Baru di C# – Tambahkan Rumus dan Simpan File Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Buat Workbook Baru di C# – Tambahkan Rumus dan Simpan File Excel
url: /id/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Baru di C# – Tambahkan Rumus dan Simpan File Excel

Pernah bertanya-tanya bagaimana cara **create new workbook** dari kode tanpa pernah membuka Excel? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus menghasilkan spreadsheet secara dinamis—mungkin untuk laporan, ekspor, atau dump data cepat.  

Berita baiknya? Dalam panduan ini Anda akan melihat secara tepat cara **create new workbook**, menambahkan **add formula to cell**, dan kemudian **save excel workbook** hanya dengan beberapa baris C#. Kami juga akan membahas **how to use expand** sehingga Anda dapat menghasilkan array dinamis tanpa menyalin manual. Pada akhir tutorial, Anda akan dapat **create excel file programmatically** dan mengirimkannya ke pengguna atau layanan downstream.

## Prerequisites

- .NET 6.0 atau lebih baru (semua runtime .NET terbaru dapat digunakan)
- Aspose.Cells untuk .NET (versi trial gratis atau berlisensi) – pustaka ini menyediakan kelas `Workbook` dan `Worksheet` yang digunakan di bawah.
- Pemahaman dasar tentang sintaks C#—tidak diperlukan pengetahuan mendalam tentang Excel.

Jika Anda sudah memiliki semuanya, bagus! Jika belum, dapatkan Aspose.Cells dari NuGet (`Install-Package Aspose.Cells`) dan Anda siap memulai.

---

## Step 1: Create New Workbook – The Foundation

Untuk memulai, kita perlu menginstansiasi objek workbook baru. Anggap saja ini membuka file Excel yang benar‑benar kosong.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Why this matters:** Kelas `Workbook` adalah titik masuk untuk manipulasi Excel apa pun. Dengan membuat instance baru, kita mengalokasikan memori untuk sheet, style, dan formula—semua tanpa menyentuh sistem file.

---

## Step 2: Access the First Worksheet

Setiap workbook baru dilengkapi dengan worksheet default (bernama *Sheet1*). Kita akan mengambilnya agar dapat menaruh data dan formula.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Jika Anda membutuhkan beberapa sheet, cukup panggil `workbook.Worksheets.Add("MySheet")` dan gunakan objek `Worksheet` yang dikembalikan.

---

## Step 3: Add Formula to Cell – Using EXPAND

Sekarang bagian yang menyenangkan: menyisipkan formula. Fungsi `EXPAND` sangat cocok ketika Anda ingin mengubah array statis menjadi rentang yang lebih besar dan terisi otomatis.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### How the EXPAND Formula Works

| Argument | Meaning |
|----------|---------|
| `{1,2,3}` | Array sumber (daftar horizontal tiga angka) |
| `5`       | Jumlah baris yang diinginkan pada hasil |
| `1`       | Jumlah kolom yang diinginkan (biarkan 1 untuk tetap vertikal) |

Saat Excel mengevaluasi ini, ia menghasilkan daftar **vertikal**:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Why use EXPAND?** Ini menghilangkan kebutuhan menyalin manual atau loop VBA. Fungsi ini secara dinamis merubah bentuk data, membuat spreadsheet Anda lebih kuat dan lebih mudah dipelihara.

---

## Step 4: Save Excel Workbook – Persist the Result

Dengan formula sudah ditempatkan, langkah terakhir adalah menulis workbook ke disk. Anda dapat memilih folder mana saja yang memiliki hak tulis.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **What you’ll see:** Buka `ExpandFormula.xlsx` di Excel, dan sel `A1` akan menampilkan array yang telah diperluas. Formula itu sendiri tetap berada di sel, sehingga jika Anda mengubah array sumber, output akan otomatis terupdate.

---

## Optional: Verify the Output Programmatically

Jika Anda lebih suka tidak membuka Excel secara manual, Anda dapat membaca kembali nilai‑nilai tersebut untuk memastikan mereka sesuai harapan.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Menjalankan kode di atas akan mencetak:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I use EXPAND with a larger source array?** | Tentu saja. Ganti `{1,2,3}` dengan array konstan apa pun atau rentang sel, misalnya `EXPAND(A1:C1,10,1)`. |
| **What if I need a horizontal result?** | Tukar argumen baris/kolom: `EXPAND({1,2,3},1,5)` akan menghasilkan penyebaran 1‑baris, 5‑kolom. |
| **Will this work on older Excel versions?** | `EXPAND` tersedia mulai Excel 365/2021. Untuk versi lebih lama, Anda harus mensimulasikan array dengan `INDEX`/`SEQUENCE`. |
| **Do I need to call `workbook.CalculateFormula()`?** | Tidak. Aspose.Cells secara otomatis mengevaluasi formula saat menyimpan, sehingga nilai muncul langsung. |
| **How to add more than one sheet before saving?** | Panggil `workbook.Worksheets.Add("SecondSheet")` dan ulangi langkah manipulasi sel pada worksheet baru tersebut. |

---

## Full Working Example

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke aplikasi console, sesuaikan jalur output, dan tekan **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Expected output in the console:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Buka file yang dihasilkan dan Anda akan melihat angka‑angka yang sama terisi di kolom **A**.

---

## Visual Summary

![Contoh membuat workbook baru](create-new-workbook.png "Tangkapan layar yang menunjukkan workbook baru yang dibuat dengan create new workbook di C#")

*Gambar ini menggambarkan workbook yang baru saja dibuat dengan hasil EXPAND.*

---

## Conclusion

Anda kini tahu cara **create new workbook**, **add formula to cell**, dan **save excel workbook** menggunakan C#. Dengan menguasai **how to use expand**, Anda dapat menghasilkan array dinamis tanpa usaha manual, dan seluruh proses memungkinkan Anda **create excel file programmatically** untuk skenario otomasi apa pun.

Apa selanjutnya? Coba ganti array konstan dengan referensi rentang, bereksperimen dengan dimensi `EXPAND` yang berbeda, atau rangkai beberapa formula di berbagai sheet. Pola yang sama berlaku untuk chart, styling, bahkan pivot table—jadi teruslah menjelajah.

Jika Anda mengalami kendala, tinggalkan komentar di bawah. Selamat coding, dan nikmati kekuatan Excel secara programatik!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}