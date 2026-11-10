---
category: general
date: 2026-10-26
description: Perluas smart marker lembar kerja di C# untuk melakukan loop pada lembar
  Excel dan mengisi template Excel dengan cepat menggunakan data dinamis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- expand worksheet smart markers
- loop sheets excel
- fill excel template c#
language: id
lastmod: 2026-10-26
og_description: Perluas smart markers lembar kerja di C# untuk mengulangi lembar Excel
  dan secara otomatis mengisi templat Excel Anda dengan data.
og_image_alt: Screenshot showing expanded worksheet smart markers in an Excel file
og_title: Perluas smart marker lembar kerja di C# – isi templat Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Expand worksheet smart markers in C# to loop sheets Excel and fill
    an Excel template quickly with dynamic data.
  headline: Expand worksheet smart markers in C# for Excel templates
  type: TechArticle
- description: Expand worksheet smart markers in C# to loop sheets Excel and fill
    an Excel template quickly with dynamic data.
  name: Expand worksheet smart markers in C# for Excel templates
  steps:
  - name: Expected output
    text: 'When you open **Result.xlsx**, the worksheet should look like this:'
  - name: Adding more columns to the repeated row
    text: 'If your template needs additional data (e.g., a sales figure), add extra
      placeholders in the same row:'
  - name: Handling empty collections
    text: When `Sheets` is empty, Aspose.Cells removes the entire repeated row, leaving
      only the header. This behavior is useful for optional sections.
  - name: Using a strongly‑typed model
    text: 'For production code, define a class:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Smart markers
title: Perluas smart marker lembar kerja dalam C# untuk templat Excel
url: /id/net/smart-markers-dynamic-data/expand-worksheet-smart-markers-in-c-for-excel-templates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memperluas smart markers lembar kerja di C# untuk templat Excel

Jika Anda perlu **memperluas smart markers lembar kerja** dalam aplikasi C#, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan belajar **mengulang koleksi lembar Excel** dan **mengisi proyek templat Excel C#** tanpa menulis loop manual atau kode sel‑per‑sel.

Bekerja dengan templat Excel sering berarti mengulang baris untuk setiap item dalam kumpulan data—pikirkan laporan bulanan, baris faktur, atau tabel jadwal. Smart markers memungkinkan Anda mendefinisikan placeholder sekali dan membiarkan perpustakaan memperluas lembar kerja secara otomatis. Pada akhir tutorial ini Anda akan memiliki contoh lengkap yang dapat dijalankan yang memperluas smart markers lembar kerja, mengulang koleksi lembar, dan menghasilkan file Excel siap‑pakai.

## Apa yang akan Anda pelajari

* Cara menambahkan paket Aspose.Cells (perpustakaan yang menyediakan smart markers) ke proyek .NET.  
* Cara mendefinisikan **smart marker** yang mengulang untuk setiap elemen dalam sebuah koleksi.  
* Cara membangun **model data** yang berisi koleksi `Sheets`.  
* Cara memanggil `ProcessSmartMarkers` sehingga lembar kerja memperluas secara otomatis.  
* Cara memverifikasi output dan memecahkan masalah umum.  

**Prasyarat**

* .NET 6.0 atau lebih baru (kode ini juga berfungsi dengan .NET Framework 4.6+).  
* Familiaritas dasar dengan C# dan Visual Studio atau IDE C# apa pun.  
* Salinan gratis **Aspose.Cells for .NET** paket NuGet (edisi komunitas berfungsi untuk contoh ini).  

---

## Langkah 1: Siapkan proyek dan tambahkan Aspose.Cells

Buat proyek konsol baru dan instal paket NuGet Aspose.Cells.

```bash
dotnet new console -n SmartMarkersDemo
cd SmartMarkersDemo
dotnet add package Aspose.Cells
```

> **Tip pro:** Gunakan versi stabil terbaru dari Aspose.Cells untuk memastikan Anda memiliki fitur smart‑marker terbaru dan perbaikan bug.

Sekarang buka `Program.cs`. Tambahkan direktif `using` yang diperlukan:

```csharp
using System;
using Aspose.Cells;
```

Namespace ini memberi Anda akses ke API `Workbook`, `Worksheet`, dan smart‑marker.

## Langkah 2: Muat templat Excel yang berisi smart marker

Buat file Excel sederhana bernama **Template.xlsx** dengan tata letak berikut (Anda dapat membuatnya secara manual di Excel):

| A | B |
|---|---|
| **Bulan** | **Data** |
| `${Sheets:Repeat}` |  |

Marker `${Sheets:Repeat}` memberi tahu Aspose.Cells untuk mengulang seluruh baris untuk setiap item dalam koleksi `Sheets`. Simpan file di folder root proyek.

```csharp
// Load the template workbook
var wb = new Workbook("Template.xlsx");

// Get the first worksheet (index 0)
var ws = wb.Worksheets[0];
```

> **Mengapa ini berhasil:** Kelas `Workbook` membaca file Excel, mempertahankan semua smart marker yang Anda tempatkan. Objek `Worksheet` memberi Anda akses langsung ke sel tempat Anda akan menyuntikkan nilai nanti.

## Langkah 3: Definisikan smart marker yang akan diulang untuk setiap lembar

Letakkan smart marker di sel pertama baris yang ingin Anda ulang. Langkah ini opsional jika Anda sudah menambahkan marker di templat, tetapi ini menunjukkan cara mengaturnya secara programatis.

```csharp
// Define a smart marker that repeats for each item in the "Sheets" collection
ws.Cells[1, 0].PutValue("${Sheets:Repeat}");
```

> **Penjelasan:** `PutValue` menulis string marker ke sel **A2** (indeks baris 1, indeks kolom 0). Saat `ProcessSmartMarkers` dijalankan, perpustakaan mencari `${Sheets:Repeat}` dan memperluas baris untuk setiap elemen dalam koleksi `Sheets`.

## Langkah 4: Bangun model data yang berisi koleksi informasi lembar

Siapkan objek anonim yang cocok dengan nama marker (`Sheets`). Setiap item dalam array harus memiliki properti bernama `Name` karena templat dapat merujuk `${Name}` nanti jika diperlukan.

```csharp
// Build a data model with a collection of sheet names
var model = new
{
    Sheets = new[]
    {
        new { Name = "Jan" },
        new { Name = "Feb" },
        new { Name = "Mar" }   // add more items to see additional rows
    }
};
```

> **Mengapa menggunakan tipe anonim?** Ini cepat untuk demo, tetapi Anda juga dapat mendefinisikan kelas bertipe kuat (`public class SheetInfo { public string Name { get; set; } }`) untuk proyek yang lebih besar.

## Langkah 5: Proses smart markers – lembar kerja memperluas secara otomatis

Sekarang panggil API inti yang memperluas lembar kerja berdasarkan koleksi.

```csharp
// Process smart markers – the worksheet will be expanded with a row for each sheet
wb.ProcessSmartMarkers(model);
```

Selama pemanggilan ini perpustakaan:

1. Memindai lembar kerja untuk `${Sheets:Repeat}`.  
2. Menggandakan baris yang berisi marker untuk setiap elemen dalam `model.Sheets`.  
3. Mengganti semua marker tambahan (misalnya `${Name}`) dengan nilai properti yang sesuai.

## Langkah 6: Simpan hasil dan verifikasi output

Akhirnya, tulis workbook ke file baru dan buka di Excel untuk melihat baris yang diperluas.

```csharp
// Save the expanded workbook
string outputPath = "Result.xlsx";
wb.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the expanded rows.");
```

### Output yang diharapkan

Saat Anda membuka **Result.xlsx**, lembar kerja seharusnya terlihat seperti ini:

| Bulan | Data |
|-------|------|
| Jan   |      |
| Feb   |      |
| Mar   |      |

Setiap baris sesuai dengan elemen dalam koleksi `Sheets`, mengonfirmasi bahwa **memperluas smart markers lembar kerja** berfungsi seperti yang diharapkan.

---

## Variasi umum dan kasus tepi

### Menambahkan lebih banyak kolom ke baris yang diulang

Jika templat Anda membutuhkan data tambahan (mis., angka penjualan), tambahkan placeholder ekstra di baris yang sama:

| A | B | C |
|---|---|---|
| `${Sheets:Repeat}` | `${Sales}` | `${Comments}` |

Kemudian perpanjang model data:

```csharp
var model = new
{
    Sheets = new[]
    {
        new { Name = "Jan", Sales = 1200, Comments = "Good" },
        new { Name = "Feb", Sales = 950,  Comments = "Average" }
    }
};
```

### Menangani koleksi kosong

Ketika `Sheets` kosong, Aspose.Cells menghapus seluruh baris yang diulang, meninggalkan hanya header. Perilaku ini berguna untuk bagian opsional.

```csharp
var model = new { Sheets = Array.Empty<object>() };
wb.ProcessSmartMarkers(model); // Results in a worksheet with just the header row
```

### Menggunakan model bertipe kuat

Untuk kode produksi, definisikan sebuah kelas:

```csharp
public class SheetInfo
{
    public string Name { get; set; }
    public double Sales { get; set; }
    public string Comments { get; set; }
}
```

Kemudian berikan daftar objek `SheetInfo`. Pengetikan kuat memberikan keamanan pada waktu kompilasi dan meningkatkan dukungan IntelliSense.

## Tips pro untuk ekspansi smart‑marker yang andal

* **Tempatkan marker `${Collection:Repeat}` di sel pertama baris yang ingin Anda duplikat.** Jika Anda menaruhnya di kolom yang lebih jauh, hanya sel di sebelah kanan marker yang akan disalin.  
* **Hindari menggabungkan sel melintasi baris yang diulang.** Sel yang digabung dapat menyebabkan masalah tata letak tak terduga setelah ekspansi.  
* **Jaga templat tetap sederhana.** Rumus kompleks yang merujuk ke baris yang diulang harus menggunakan referensi relatif  

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Automate Excel Workbooks with Aspose.Cells .NET&#58; Utilize Smart Markers for Efficient Data Processing](/cells/english/net/automation-batch-processing/automate-excel-aspose-cells-workbook-smart-markers/)
- [Create Excel Template with Smart Markers in C# – Complete Guide](/cells/english/net/smart-markers-dynamic-data/create-excel-template-with-smart-markers-in-c-complete-guide/)
- [How to create smart marker data and fill Excel template data](/cells/english/net/smart-markers-dynamic-data/how-to-create-smart-marker-data-and-fill-excel-template-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}