---
category: general
date: 2026-06-27
description: Simpan Workbook Excel di C# sambil menambahkan rentang bernama. Pelajari
  cara membuat nama terdefinisi dan menggunakan rumus nama terdefinisi dengan Aspose.Cells.
draft: false
keywords:
- save excel workbook
- add named range
- create defined name
- named range excel
- use defined name formulas
language: id
og_description: Simpan Workbook Excel di C# dan pelajari cara menambahkan rentang
  bernama, membuat nama terdefinisi, serta menggunakan rumus nama terdefinisi dengan
  Aspose.Cells.
og_title: Simpan Buku Kerja Excel dan Tambahkan Rentang Bernama – Tutorial C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel Workbook in C# while adding a named range. Learn to create
    defined name and use defined name formulas with Aspose.Cells.
  headline: Save Excel Workbook and Add Named Range – Full C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Simpan Workbook Excel dan Tambahkan Rentang Bernama – Panduan Lengkap C#
url: /id/net/excel-advanced-named-ranges/save-excel-workbook-and-add-named-range-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan Workbook Excel dan Tambahkan Named Range – Panduan Lengkap C#

Pernah perlu **menyimpan workbook Excel** setelah menambahkan beberapa nama khusus di sekitar lembar? Anda tidak sendirian. Dalam banyak alat pelaporan atau aplikasi berbasis data kami sering membuat named range, kemudian merujuknya dalam rumus, dan akhirnya menyimpan perubahan kembali ke disk.  

Dalam tutorial ini kita akan melangkah melalui semuanya: memuat file *.xlsx*, **menambahkan named range**, **membuat defined name**, menggunakan nama itu di dalam rumus, dan akhirnya **menyimpan workbook Excel** dengan pembaruan. Tanpa basa‑basi—hanya contoh lengkap yang dapat dijalankan dan dapat Anda sisipkan ke proyek .NET mana pun.

> **Pro tip:** Aspose.Cells bekerja tanpa perlu menginstal Microsoft Office, menjadikannya sempurna untuk otomatisasi sisi‑server.

## Apa yang Anda Butuhkan

- .NET 6 (atau runtime .NET terbaru apa pun)  
- Paket NuGet Aspose.Cells untuk .NET (`Install-Package Aspose.Cells`)  
- Contoh `input.xlsx` (workbook apa saja, tetapi pastikan Sheet1 memiliki data di **A1**)  
- IDE favorit Anda (Visual Studio, Rider, VS Code…)

Itu saja. Jika Anda sudah memiliki semua itu, kita bisa langsung masuk ke kode.

## Langkah 1: Siapkan Proyek

Buat aplikasi console dan tambahkan Aspose.Cells:

```bash
dotnet new console -n ExcelNamedRangeDemo
cd ExcelNamedRangeDemo
dotnet add package Aspose.Cells
```

Buka `Program.cs`; Anda akan melihat metode `Main` default. Kami akan mengganti isinya dengan alur kerja lengkap pada langkah‑langkah berikutnya.

## Langkah 2: Muat Workbook

Memuat workbook adalah hal pertama yang Anda lakukan sebelum dapat **menambahkan named range**. Anggap saja seperti membuka buku sebelum mulai menulis catatan di margin.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");
```

> **Mengapa ini penting:** Objek `Workbook` mewakili seluruh file Excel dalam memori. Tanpanya Anda tidak dapat memanipulasi sel, nama, atau rumus.

## Langkah 3: Buat Defined Name (Add Named Range)

Sekarang kita benar‑benar **membuat defined name** yang menunjuk ke sel atau rentang tertentu. Di UI Excel Anda akan pergi ke *Formulas → Name Manager*; di sini kita melakukannya secara programatik.

```csharp
        // Step 3: Add a defined name that points to cell A1 on Sheet1
        // This name can be used in formulas throughout the workbook
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");
```

> **Penjelasan:** `wb.Names.Add` mendaftarkan *named range* bernama **Sales**. String `=Sheet1!$A$1` adalah rumus referensi—tepat seperti yang Anda ketik di dialog Name Manager.

## Langkah 4: Gunakan Defined Name dalam Rumus

Memiliki nama memang bagus, tetapi biasanya Anda ingin **menggunakan rumus dengan defined name** di suatu tempat. Mari tulis rumus sederhana yang menambahkan 10 ke nilai di **Sales** dan menaruh hasilnya di **B1**.

```csharp
        // Step 4: Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");
```

Saat workbook menghitung ulang, `B1` akan menampilkan apa pun yang ada di `A1` ditambah sepuluh. Itu menunjukkan kekuatan *named range excel*—Anda dapat mengubah referensi dasar sekali dan semua rumus akan otomatis terupdate.

## Langkah 5: Simpan Workbook yang Telah Dimodifikasi

Akhirnya kita **menyimpan workbook Excel** ke file baru agar perubahan tetap ada. Anda dapat menimpa file asli atau menulis ke lokasi baru; di sini kami menyimpan keduanya.

```csharp
        // Step 5: Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

Menjalankan program menghasilkan output konsol serupa dengan:

```
Workbook loaded successfully.
Defined name 'Sales' added (named range Excel).
Formula '=Sales + 10' written to B1.
Workbook saved as 'YOUR_DIRECTORY\output.xlsx'.
```

Buka `output.xlsx` dan Anda akan melihat **B1** kini berisi `=Sales + 10`, sementara **A1** tetap tidak berubah. Nama **Sales** muncul di bawah *Formulas → Name Manager*.

## Kasus Khusus & Pertanyaan Umum

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika nama sheet mengandung spasi?** | Bungkus dengan tanda kutip tunggal: `= 'My Sheet'!$A$1`. |
| **Bisakah saya menunjuk nama ke rentang multi‑sel?** | Tentu—gunakan `=Sheet1!$A$1:$A$5` saat memanggil `wb.Names.Add`. |
| **Apakah saya harus menghitung ulang secara manual?** | Aspose.Cells menghitung ulang secara otomatis ketika Anda membaca nilai sel. Jika membutuhkan penyegaran penuh, panggil `wb.CalculateFormula()`. |
| **Bagaimana dengan nama yang sudah ada?** | `wb.Names.Add` akan melempar error jika nama sudah ada. Gunakan `wb.Names["Sales"]?.RefersTo = "...";` untuk memperbarui. |

## Contoh Lengkap yang Siap Pakai (Semua Langkah Digabung)

Berikut program lengkap yang siap disalin‑tempel. Ganti `YOUR_DIRECTORY` dengan folder yang sebenarnya di mesin Anda.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");

        // Add a defined name (named range) that points to cell A1 on Sheet1
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");

        // Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");

        // Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

**Hasil yang Diharapkan:**  

- `output.xlsx` berisi nama baru **Sales** yang menunjuk ke `Sheet1!A1`.  
- Sel **B1** menampilkan nilai **A1** ditambah `10`.  
- File tersebut sepenuhnya kompatibel dengan Excel, Google Sheets, atau perpustakaan apa pun yang memahami named range.

## Kesimpulan

Anda kini tahu cara **menyimpan workbook Excel**, **menambahkan named range**, **membuat defined name**, dan **menggunakan rumus dengan defined name** menggunakan Aspose.Cells di C#. Langkah‑langkahnya sederhana: muat, beri nama, referensikan, dan simpan.  

Dari sini Anda dapat memperluas ke:  

- Membuat rentang dinamis dengan fungsi `OFFSET`.  
- Menerapkan nama yang sama di beberapa sheet (`Scope = Worksheet`).  
- Menghasilkan ribuan named range untuk model keuangan yang kompleks.

Cobalah, ubah referensinya, atau masukkan nama ke dalam pivot table—kemungkinan otomatisasi Anda hampir tak terbatas.

---

![Diagram alur Simpan Workbook Excel](excel-workflow.png){: .align-center alt="Diagram alur Simpan Workbook Excel"}

*Siap mengotomatisasi laporan Excel Anda? Tinggalkan komentar, bagikan modifikasi Anda, atau fork repositori di GitHub. Selamat coding!*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut membahas topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Simpan Workbook Excel Aspose Cells .NET](/cells/english/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Buat Simpan Workbook Excel PDF Aspnet Aspose Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}