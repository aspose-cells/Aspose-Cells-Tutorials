---
category: general
date: 2026-07-03
description: Cara menggunakan SEQUENCE di C# untuk menghasilkan nomor berurutan di
  Excel. Pelajari cara membuat workbook Excel dengan C# dan ASP.NET serta membuat
  file Excel dengan beberapa baris kode.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: id
og_description: Cara menggunakan SEQUENCE di C# untuk menghasilkan nomor berurutan
  di Excel. Panduan langkah demi langkah membuat workbook Excel dengan C# dan ASP.NET
  untuk membuat file Excel.
og_title: Cara Menggunakan SEQUENCE di C# – Membuat Workbook Excel
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Cara Menggunakan SEQUENCE di C# – Membuat Workbook Excel
url: /id/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan SEQUENCE di C# – Membuat Workbook Excel

Pernah bertanya‑tanya **cara menggunakan SEQUENCE** untuk menghasilkan daftar angka dalam lembar Excel dari C#? Anda tidak sendirian. Baik Anda sedang membangun dasbor pelaporan, mengisi data‑grid, atau hanya membutuhkan cara cepat untuk menghasilkan ID, menguasai trik ini menyelamatkan Anda dari harus menulis loop.

Dalam tutorial ini kita akan **membuat workbook Excel di C#**, menempatkan formula array‑dinamis `SEQUENCE` ke sel A1, dan menghasilkan kolom angka bertingkat yang rapi. Kami juga akan menunjukkan cara menyajikan file tersebut dari controller ASP.NET—ya, **ASP.NET create Excel file** juga dibahas. Pada akhir tutorial Anda akan dapat **menghasilkan angka bertingkat gaya Excel** dengan satu baris kode.

## Apa yang Anda Butuhkan

- .NET 6+ (kode ini juga bekerja pada .NET Framework 4.6+)  
- Paket NuGet **Aspose.Cells for .NET** (atau perpustakaan apa pun yang menyediakan objek `Workbook`/`Worksheet`)  
- Proyek ASP.NET Core atau MVC dasar jika Anda ingin mencoba bagian unduhan web  

Itu saja. Tidak ada interop COM tambahan, tidak perlu instalasi Office.

---

## Cara Menggunakan SEQUENCE untuk Menghasilkan Angka Bertingkat

Fungsi Excel `SEQUENCE(rows, [columns], [start], [step])` mengembalikan rentang **spill**. Dalam kasus kami kami menginginkan 5 baris, 1 kolom, mulai dari 10, langkah 2. Formulanya terlihat seperti ini:

```excel
=SEQUENCE(5,1,10,2)
```

Saat Excel mengevaluasinya, sel A1:A5 akan berisi **10, 12, 14, 16, 18**. Keindahannya adalah kita tidak perlu menulis loop C#—formula yang melakukan pekerjaan berat.

Berikut potongan kode C# lengkap yang membuat workbook, menyisipkan formula, memaksa perhitungan, dan menyimpan file.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Output yang diharapkan** – buka *DynamicArray.xlsx* dan Anda akan melihat:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

Itulah seluruh cerita **cara menggunakan sequence** di C#. Sederhana, kan? Tetapi mari kita selami sedikit lebih dalam.

### Mengapa Menggunakan SEQUENCE Daripada Loop?

- **Performa** – Excel melakukan perhitungan dengan mesin internalnya, yang sangat dioptimalkan.  
- **Pemeliharaan** – Formula bersifat self‑documenting; siapa pun yang membuka sheet langsung mengerti maksudnya.  
- **Ukuran dinamis** – Ubah argumen `rows` dan rentang spill akan otomatis memperluas.

---

## Membuat Workbook Excel C# – Langkah demi Langkah

Jika Anda baru mengenal **create excel workbook c#**, checklist berikut membantu menghindari jebakan umum.

1. **Tambahkan paket Aspose.Cells**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Anda juga dapat menggunakan ClosedXML atau EPPlus, tetapi API yang ditunjukkan cocok dengan kode di atas.)

2. **Setel lisensi** (opsional untuk trial).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instansiasi `Workbook`** – ini memberi Anda workbook baru yang kosong.

4. **Referensikan worksheet** – `workbook.Worksheets[0]` adalah sheet default bernama *Sheet1*.

5. **Terapkan formula SEQUENCE** – seperti yang ditunjukkan sebelumnya.

6. **Hitung** – `workbook.CalculateFormula()` memaksa spill; jika tidak, file hanya akan berisi formula.

7. **Simpan** – Anda dapat menulis ke disk, `MemoryStream`, atau langsung ke respons HTTP.

### Pro Tip

Jika Anda memerlukan workbook di memori (misalnya, untuk mengirimnya lewat API web), gunakan `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – Streaming ke Browser

Sekarang kita sudah tahu **create excel workbook c#**, mari integrasikan ke dalam controller ASP.NET Core sehingga pengguna dapat mengunduh file secara langsung.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Ketika pengguna mengakses `/api/excel/download`, browser akan menampilkan dialog unduhan *DynamicArray.xlsx*. File tersebut sudah berisi kolom **generated incremental numbers excel** berkat formula `SEQUENCE`.

### Bagaimana Jika Klien Menggunakan Versi Excel yang Lebih Lama?

Array dinamis (termasuk `SEQUENCE`) diperkenalkan di Excel 365/2019. Jika Anda memerlukan kompatibilitas mundur, gunakan pengisian manual:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Potongan kode itu menunjukkan pendekatan klasik **generate incremental numbers excel** tanpa mengandalkan fungsi baru.

---

## Pertanyaan Umum & Kasus Edge

- **Apakah saya perlu mengaktifkan perhitungan iteratif?**  
  Tidak. `SEQUENCE` adalah fungsi non‑iteratif; panggilan `CalculateFormula()` sederhana sudah cukup.

- **Bagaimana jika saya ingin spill secara horizontal?**  
  Ubah argumen kedua: `=SEQUENCE(1,5,10,2)` akan spill ke B1:F1.

- **Bisakah saya menggabungkan SEQUENCE dengan fungsi lain?**  
  Tentu. Misalnya, `=INDEX(A:A, SEQUENCE(5,1,10,2))` dapat mengambil baris dari kolom lain.

- **Apakah ukuran workbook menjadi masalah?**  
  Dampak ukuran file akibat formula hampir tidak terasa. Hanya ketika Anda mulai mengisi jutaan sel secara manual ukuran akan menjadi masalah.

---

## Kesimpulan

Kami telah menelusuri **cara menggunakan sequence** di C# untuk **create excel workbook c#**, menyajikan workbook tersebut melalui **ASP.NET create excel file**, dan memperlihatkan cara **generate incremental numbers excel** tanpa menulis loop. Inti utamanya: biarkan mesin array‑dinamis Excel yang menghitung, dan biarkan kode .NET Anda fokus pada orkestrasi.

Silakan bereksperimen—ganti argumen `rows`, `start`, atau `step`, spill secara horizontal, atau gabungkan formula dengan `IF` atau `FILTER` untuk laporan yang lebih canggih. Saat Anda siap, coba rangkai beberapa sheet atau ekspor workbook sebagai CSV untuk sistem downstream.

Ada trik yang ingin Anda bagikan? Tinggalkan komentar di bawah, atau hubungi saya di GitHub. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}