---
category: general
date: 2026-06-21
description: Impor JSON ke Excel dengan cepat dan pelajari cara mengonversi JSON ke
  XLSX, menghasilkan Excel dari JSON, serta mengekspor JSON ke spreadsheet dalam beberapa
  langkah mudah.
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: id
og_description: Impor JSON ke Excel dengan mudah. Panduan ini menunjukkan cara mengonversi
  JSON ke XLSX, menghasilkan Excel dari JSON, dan mengekspor JSON ke spreadsheet menggunakan
  C#.
og_title: Impor JSON ke Excel dengan Aspose.Cells – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Impor JSON ke Excel dengan Aspose.Cells – Panduan Pemrograman Lengkap
url: /id/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Impor JSON ke Excel – Panduan Pemrograman Lengkap

Pernah bertanya-tanya **bagaimana cara mengimpor JSON ke Excel** tanpa menulis parser khusus? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus mengubah payload JSON menjadi spreadsheet rapi untuk laporan atau tugas analisis data. Kabar baiknya? Dengan Aspose.Cells Anda dapat **mengonversi JSON ke XLSX** hanya dengan beberapa baris kode, dan seluruh prosesnya cepat serta tipe‑aman.

Dalam tutorial ini kami akan membimbing Anda melalui setiap langkah yang diperlukan untuk **menghasilkan Excel dari JSON**, menyimpan hasilnya sebagai file `.xlsx`, dan bahkan mengeksplorasi beberapa variasi berguna—seperti mengekspor JSON ke spreadsheet yang otomatis memperbarui ketika Anda mengubah data sumber. Pada akhir tutorial, Anda akan memiliki potongan kode yang dapat dipakai ulang di proyek .NET mana pun.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru (kode ini juga berfungsi di .NET Framework)
- Lisensi Aspose.Cells for .NET yang valid atau kunci evaluasi sementara
- Visual Studio 2022 (atau IDE C# lain yang Anda sukai)
- Familiaritas dasar dengan struktur JSON dan sintaks C#

Tidak diperlukan paket NuGet tambahan selain **Aspose.Cells**, sehingga penyiapannya ringan.

## Langkah 1: Instal Aspose.Cells dan Siapkan Proyek

Hal pertama yang harus dilakukan, tambahkan pustaka Aspose.Cells ke proyek Anda. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.Cells
```

Jika Anda menggunakan .NET CLI, perintah yang setara adalah:

```bash
dotnet add package Aspose.Cells
```

> **Tip pro:** Setelah instalasi, tambahkan file lisensi Anda (`Aspose.Cells.lic`) ke root proyek dan muat di saat startup:

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Sekarang Anda siap untuk mulai **mengimpor JSON ke Excel**.

## Langkah 2: Siapkan Payload JSON

Untuk demonstrasi, kami akan menggunakan array sederhana berisi objek orang. Pada skenario dunia nyata Anda mungkin membaca string ini dari file, respons API, atau basis data.

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

Perhatikan bahwa JSON tersebut merupakan array datar—bentuk yang paling cocok dengan smart marker Aspose.Cells.

## Langkah 3: Konfigurasikan Opsi Memuat JSON

Aspose.Cells memungkinkan Anda memperlakukan seluruh array JSON sebagai *satu* sumber data. Ini penting ketika Anda ingin baris secara otomatis memperluas di dalam worksheet.

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

Menetapkan `ArrayAsSingle = true` memberi tahu pustaka **untuk menghasilkan smart marker yang diulang untuk setiap elemen** dalam array, yang merupakan inti dari alur kerja **mengonversi JSON ke XLSX**.

## Langkah 4: Buat Workbook dan Impor JSON

Sekarang kita buat instance `Workbook` baru dan mengimpor JSON menggunakan smart marker bernama `"People"`.

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

Di balik layar, Aspose.Cells mem-parsing JSON, memetakan setiap properti (`Name`, `Age`) ke kolom, dan menyiapkan placeholder yang nanti akan diperluas menjadi baris.

## Langkah 5: Tempatkan Smart Marker di Worksheet

Smart marker terlihat seperti `{{People}}`. Saat workbook disimpan, Aspose.Cells menggantikan marker ini dengan tabel yang berisi semua data dari array JSON.

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

Anda dapat memindahkan marker ke mana saja—pojok kiri‑atas biasanya dipilih karena memberi ruang bagi tabel untuk tumbuh ke bawah dan ke kanan.

## Langkah 6: Simpan Workbook sebagai File XLSX

Akhirnya, tulis workbook ke disk. Di sinilah kita **menyimpan JSON sebagai Excel** dan mendapatkan file `.xlsx` yang dapat dibuka di Excel, Google Sheets, atau aplikasi spreadsheet lainnya.

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Saat Anda membuka `JsonSingleCell.xlsx`, akan terlihat seperti:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

Itulah hasil **menghasilkan Excel dari JSON** yang beraksi.

## Contoh Lengkap yang Siap Dijalan

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### Output yang Diharapkan

Menjalankan program akan mencetak:

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

Membuka file menampilkan tabel dua baris dengan header **Name** dan **Age**, persis sama dengan array JSON asal.

## Variasi Lanjutan

### 1. Impor Beberapa Array JSON ke Sheet yang Berbeda

Jika Anda memiliki beberapa array—misalnya `"Employees"` dan `"Departments"`—Anda dapat mengimpor masing‑masing ke worksheet terpisah:

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

Sekarang Anda telah **mengekspor JSON ke spreadsheet** dengan banyak tab, masing‑masing mencerminkan dataset yang berbeda.

### 2. Menata Tabel yang Dihasilkan

Anda dapat menerapkan gaya setelah data diperluas:

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

Penyempurnaan kecil ini membuat baris header menonjol, yang berguna untuk dasbor laporan.

### 3. Menggunakan File JSON Alih-alih String

Jika JSON Anda berada di disk, cukup baca dulu:

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

Langkah‑langkah selanjutnya tetap sama, sehingga Anda dapat **menyimpan JSON sebagai Excel** dari sumber apa pun.

## Kesalahan Umum & Cara Menghindarinya

- **Tidak Menyetel `ArrayAsSingle`** – Lupa mengaktifkan flag ini akan memperlakukan setiap objek sebagai sumber data terpisah, menghasilkan sel kosong. Selalu setel flag ini ketika JSON Anda berupa array tingkat atas.
- **Nama Smart Marker Salah** – Marker (`{{People}}`) harus cocok dengan `DataSourceName` yang Anda berikan (`"People"`). Kesalahan ketik akan membuat placeholder tidak terganti.
- **Lisensi Tidak Dimuat** – Dalam mode evaluasi, file output berisi watermark. Muat lisensi Anda di awal agar workbook bersih.
- **Izin Jalur File** – Mencoba menyimpan ke folder yang dilindungi akan menimbulkan pengecualian. Gunakan `Environment.CurrentDirectory` atau jalur yang dapat ditulisi pengguna.

## Menguji Hasil Secara Programatik

Jika Anda ingin memverifikasi bahwa ekspor berhasil tanpa membuka Excel, Anda dapat membaca kembali sel pertama:

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

Pengecekan konsol cepat seperti ini memastikan bahwa **mengonversi JSON ke XLSX** berhasil sesuai harapan.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **mengimpor JSON ke Excel** menggunakan Aspose.Cells: mulai dari instalasi pustaka, menyiapkan JSON, mengonfigurasi smart marker, hingga akhirnya **menyimpan JSON sebagai Excel**. Baik Anda perlu **mengonversi JSON ke XLSX**, **menghasilkan Excel dari JSON**, atau **mengekspor JSON ke spreadsheet** untuk analisis, pola kerjanya tetap sama—smart marker melakukan pekerjaan berat.

Silakan bereksperimen dengan penataan, banyak sheet, atau bahkan pembaruan dinamis dengan meng‑impor ulang JSON pada runtime. Langkah selanjutnya yang logis adalah mengintegrasikan kode ini ke dalam web API yang menyajikan laporan Excel secara on‑demand—cukup ganti baris penyimpanan file dengan stream yang dikembalikan ke klien.

Ada pertanyaan tentang kasus khusus, seperti objek JSON bersarang atau dataset besar? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut membahas topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Efficiently Import JSON to Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Effortlessly Import JSON into Excel using Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}