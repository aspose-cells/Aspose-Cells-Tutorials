---
category: general
date: 2026-06-08
description: Buat workbook Excel dengan C# langkah demi langkah dan pelajari cara
  menggunakan fungsi expand di Excel untuk rentang dinamis. Sempurna untuk pengembang
  .NET.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: id
og_description: Buat workbook Excel C# dengan contoh yang jelas dan temukan cara menggunakan
  fungsi expand di Excel untuk menghasilkan array dinamis.
og_title: Membuat Workbook Excel C# – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Membuat Workbook Excel C# – Panduan Lengkap dengan Fungsi Expand
url: /id/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel C# – Panduan Lengkap dengan Fungsi Expand

Pernah bertanya-tanya bagaimana **membuat workbook Excel C#** tanpa harus berurusan dengan COM interop atau memanipulasi XML? Anda tidak sendirian. Dalam banyak proyek .NET kami perlu menghasilkan spreadsheet, mengisinya dengan rumus, dan menyerahkannya kepada pengguna non‑teknis. Kabar baiknya? Dengan library modern seperti **Aspose.Cells** seluruh proses menjadi sangat mudah.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang **membuat workbook Excel C#**, menambahkan beberapa rumus—termasuk cara **menggunakan fungsi expand di Excel**—dan menyimpan file sehingga Anda dapat langsung membukanya di Excel. Pada akhir tutorial Anda akan tahu tidak hanya *apa* yang harus diketik, tetapi *mengapa* setiap baris penting, dan Anda akan memiliki templat yang dapat disalin ke proyek mana pun.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6 SDK (atau versi .NET terbaru) terpasang.
- IDE yang mendukung NuGet (Visual Studio, VS Code, Rider, dll.).
- Paket NuGet **Aspose.Cells** – menyediakan kelas `Workbook` dan `Worksheet` yang digunakan dalam kode.
- Pengetahuan dasar C#; tidak diperlukan pengalaman khusus Excel.

Sudah semua? Baik—mari kita mulai.

## Langkah 1: Siapkan Proyek dan Tambahkan Aspose.Cells

Pertama, buat aplikasi console dan tambahkan pustaka tersebut.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Jika Anda berada di jaringan korporat, mungkin perlu mengonfigurasi proxy NuGet. Paket Aspose.Cells ringan, jadi instalasinya selesai dalam hitungan detik.

Sekarang buka `Program.cs`. Anda akan melihat metode `Main` default—ganti dengan kerangka di bawah ini.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

Baris `using Aspose.Cells;` membawa kelas spreadsheet ke dalam ruang lingkup. Jika Anda lupa menambahkannya, kompiler akan mengeluh bahwa `Workbook` tidak terdefinisi—sesuatu yang akan kita hindari nanti.

## Langkah 2: Buat Excel Workbook C# dan Akses Worksheet Pertama

Setelah proyek siap, kita akhirnya dapat **membuat workbook Excel C#**. Konstruktor `Workbook` memberikan workbook kosong yang baru, dan indeks `Worksheets[0]` mengembalikan sheet default (bernama “Sheet1”).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Mengapa kita mengambil worksheet pertama secara eksplisit? Karena banyak API downstream (seperti penetapan rumus) memerlukan objek `Worksheet`, bukan hanya `Workbook`. Ini juga membuat kode lebih jelas bagi siapa pun yang membacanya nanti.

## Langkah 3: Gunakan Fungsi Expand di Excel untuk Mengisi Rentang Dinamis

Sekarang tiba saatnya bintang utama: **menggunakan fungsi expand di Excel**. Fungsi `EXPAND` (tersedia mulai Excel 365) mengambil array sumber dan memperluasnya ke ukuran yang diinginkan. Dalam contoh kami kita mulai dengan array vertikal 3‑baris yang dihasilkan oleh `SEQUENCE(3)` dan memperluasnya menjadi blok 5 × 5.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

Apa yang sebenarnya terjadi?

1. `SEQUENCE(3)` menghasilkan array vertikal `{1;2;3}`.
2. `EXPAND(...,5,5)` memberi tahu Excel untuk memperbesar array tersebut menjadi 5 baris dan 5 kolom.
3. Hasilnya adalah grid 5 × 5 di mana tiga baris pertama berisi angka 1‑3 yang diulang di setiap kolom, dan dua baris terakhir kosong.

Karena kita menulis rumus sebagai string, Excel mengevaluasinya *saat file dibuka*, bukan pada saat runtime. Itu berarti workbook tetap ringan, dan setiap perubahan pada array sumber akan otomatis merambat.

> **Kasus khusus:** Jika pengguna membuka workbook di versi Excel yang lebih lama dan tidak mendukung `EXPAND`, sel akan menampilkan `#NAME?`. Untuk mengantisipasinya Anda dapat membungkus rumus dengan `IFERROR`, tetapi untuk lingkungan modern fungsi ini aman digunakan.

## Langkah 4: Tambahkan Rumus Cotangent untuk Pelengkap

Mari tambahkan satu rumus lagi untuk menunjukkan betapa mudahnya menambahkan ekspresi matematika. Kita akan menghitung cotangent dari π/4, yang hasilnya tepat `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Fungsi `COT` di Excel tidak sepopuler `SIN` atau `COS`, namun sangat berguna untuk alur kerja trigonometri. Saat Anda membuka workbook, sel **B1** akan menampilkan `1`.

## Langkah 5: Simpan Workbook dan Verifikasi Hasilnya

Semua kerja keras akan sia-sia jika kita tidak menyimpan file. Metode `Save` menuliskan workbook yang berada di memori ke disk. Pilih folder yang Anda miliki hak tulisnya, dan beri nama file yang mudah diingat.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Jalankan program:

```bash
dotnet run
```

Anda akan melihat pesan di konsol yang mengonfirmasi penyimpanan. Buka `output.xlsx` di Excel, dan Anda akan melihat:

- Sel **A1:E5** terisi dengan urutan yang diperluas (1,2,3 pada tiga baris pertama, kosong pada baris 4‑5).
- Sel **B1** menampilkan nilai `1` dari rumus cotangent.

Itulah siklus lengkap: **membuat workbook excel c#**, menyisipkan rumus, dan menghasilkan spreadsheet yang dapat dipakai.

![Screenshot of the generated Excel workbook showing the expanded array and cotangent result](/images/create-excel-workbook-csharp.png "contoh workbook excel c#")

*Teks alt gambar: membuat workbook excel c# – tampilan spreadsheet yang terisi.*

## Langkah 6: Opsional – Auto‑Fit Kolom untuk Tampilan Lebih Rapi

Jika Anda berencana mendistribusikan file ke pengguna akhir, auto‑fit cepat akan membuatnya terlihat profesional.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Baris ini melintasi setiap kolom yang berisi data dan menyesuaikan lebar kolom ke entri terpanjang. Sentuhan kecil ini mencegah overflow “…###” ketika angka lebih lebar daripada lebar kolom default.

## Langkah 7: Penutup dan Langkah Selanjutnya

Selamat—Anda baru saja menguasai cara **membuat workbook excel c#** dari awal dan belajar cara **menggunakan fungsi expand di excel** untuk menghasilkan array dinamis. Kode dibuat sesederhana mungkin sehingga Anda dapat menyalinnya ke proyek mana pun, namun konsepnya dapat diskalakan:

- **Sumber data dinamis:** Ganti `SEQUENCE(3)` dengan referensi ke rentang lain atau tabel bernama.
- **Pemformatan bersyarat:** Gunakan `ws.Cells["A1:E5"].Style` untuk menambahkan warna berdasarkan nilai.
- **Grafik dan gambar:** Aspose.Cells dapat menyisipkan chart, gambar, bahkan pivot table.

Silakan bereksperimen—ubah dimensi `EXPAND`, coba `FILTER` atau `SORT`, atau rangkaian beberapa rumus sekaligus. Library menangani semuanya tanpa Anda harus menyentuh format OpenXML tingkat rendah.

---

### Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan .NET Framework 4.8?**  
J: Tentu saja. Aspose.Cells menargetkan .NET Standard 2.0, yang kompatibel dengan .NET Core maupun Framework klasik.

**T: Bagaimana jika saya perlu melindungi sheet?**  
J: Gunakan `ws.Protect(ProtectionType.All, "yourPassword");` sebelum menyimpan.

**T: Bisakah saya menulis workbook langsung ke `MemoryStream`?**  
J: Ya—`workbook.Save(stream, SaveFormat.Xlsx);` sangat berguna untuk API web yang mengembalikan file sebagai unduhan.

---

## TL;DR

Kami membangun **aplikasi console C# lengkap** yang:

1. **Membuat workbook Excel C#** menggunakan Aspose.Cells.  
2. **Menggunakan fungsi EXPAND di Excel** untuk mengubah array 3‑baris menjadi blok 5 × 5.  
3. Menambahkan rumus cotangent (`COT(PI()/4)`).  
4. Menyimpan file dan opsional melakukan auto‑fit kolom.

Sekarang Anda memiliki fondasi kuat untuk tugas otomatisasi apa pun yang melibatkan pembuatan file Excel dari .NET. Selamat coding, semoga spreadsheet Anda selalu bebas error!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [How to Create and Use Union Ranges in Excel with Aspose.Cells .NET (C# Guide)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step-by-Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}