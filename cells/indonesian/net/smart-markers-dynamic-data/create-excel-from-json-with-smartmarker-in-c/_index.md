---
category: general
date: 2026-11-16
description: Buat Excel dari JSON menggunakan SmartMarker. Pelajari cara mengonversi
  JSON ke Excel, menyematkan JSON di Excel, dan menyimpan workbook xlsx dalam hitungan
  menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: id
lastmod: 2026-11-16
og_description: Buat Excel dari JSON dengan cepat. Tutorial ini menunjukkan cara mengonversi
  JSON ke Excel, menyematkan JSON di Excel, dan menyimpan workbook xlsx dengan Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Buat Excel dari JSON dengan SmartMarker – panduan C# langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Buat Excel dari JSON dengan SmartMarker di C#
url: /id/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Excel dari JSON dengan SmartMarker di C#

Jika Anda perlu **membuat Excel dari JSON** dalam proyek .NET, panduan ini menunjukkan solusi lengkap yang dapat dijalankan. Dengan menggunakan processor Smart Marker dari Aspose.Cells, Anda dapat **mengonversi JSON ke Excel**, menyisipkan string JSON langsung ke dalam sel, dan **menyimpan workbook xlsx** tanpa menulis kode parsing manual.

Anda akan melihat cara mendaftarkan sumber data JSON, menyisipkan Smart Marker yang menghasilkan seluruh array sebagai satu string JSON, memproses worksheet, dan akhirnya menulis file ke disk. Pada akhir tutorial, Anda dapat menghasilkan file Excel yang berisi payload JSON asli di sel A1, siap untuk diproses lebih lanjut atau pelaporan.

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
- Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`)
- Pengetahuan dasar tentang C# dan format JSON
- IDE seperti Visual Studio atau VS Code

## Langkah 1: Siapkan proyek dan impor namespace

Buat aplikasi console baru dan tambahkan paket Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Kemudian sertakan namespace yang diperlukan di bagian atas `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Mengapa?**  
`Aspose.Cells` menyediakan model workbook, sementara `Aspose.Cells.SmartMarkers` berisi kelas `SmartMarkerProcessor` yang menafsirkan penanda `&=` di worksheet.

## Langkah 2: Definisikan sumber data JSON

Letakkan string JSON dalam sebuah variabel. Pada contoh ini kita memiliki array pesanan:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Mengapa?**  
Smart Marker bekerja dengan JSON yang terstruktur dengan baik. Menyimpan JSON dalam string memungkinkan Anda mendaftarkannya secara langsung tanpa memerlukan file di disk.

## Langkah 3: Daftarkan data JSON dengan SmartMarkerProcessor

Buat instance `SmartMarkerProcessor` dan kaitkan string JSON dengan nama yang akan Anda referensikan nanti di worksheet:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Mengapa?**  
`RegisterJsonDataSource` mengurai JSON dan membuat hierarki tersedia bagi Smart Markers. Nama `"OrdersJson"` menjadi objek akar dalam ekspresi penanda.

## Langkah 4: Buat workbook dan sisipkan Smart Marker

Instansiasi workbook baru, ambil worksheet pertama, dan tulis Smart Marker ke sel A1 yang akan menghasilkan seluruh array `Orders` sebagai satu string JSON:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Mengapa?**  
Ekspresi `OrdersJson.Orders.ArrayAsSingle` memberi tahu Smart Marker untuk mengambil array `Orders` dan men-serialize‑nya kembali ke JSON, menempatkan hasilnya di sel target. Ini adalah cara paling sederhana untuk **menyisipkan JSON dalam Excel**.

## Langkah 5: Proses worksheet

Jalankan processor sehingga ia menggantikan penanda dengan string JSON yang sebenarnya:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Mengapa?**  
Pemrosesan memeriksa setiap sel untuk penanda `&=`, mengevaluasinya terhadap sumber data yang terdaftar, dan menulis nilai yang dievaluasi kembali ke worksheet.

## Langkah 6: Simpan workbook sebagai file .xlsx

Akhirnya, tulis workbook ke disk. Sesuaikan path ke folder yang Anda miliki hak tulisnya:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Mengapa?**  
`SaveFormat.Xlsx` memastikan file disimpan dalam format Office Open XML modern, memenuhi persyaratan **save workbook xlsx**.

## Kode sumber lengkap

Menggabungkan semua bagian, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Output yang diharapkan di Excel

Buka `JsonArraySingleCell.xlsx`. Sel A1 akan berisi:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

String JSON tersebut merupakan representasi kompak dari array `Orders` asli, sehingga mudah dipindahkan atau dikonsumsi dalam alur kerja berbasis Excel selanjutnya.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian |
|-----------|------------|
| **Beberapa objek JSON** | Daftarkan setiap objek dengan nama yang berbeda (misalnya, `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) dan referensikan mereka dengan penanda terpisah. |
| **JSON yang diformat rapi di sel** | Gunakan opsi `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Payload JSON besar** | Pertimbangkan menulis JSON ke sheet tersembunyi atau menggunakan konversi `DataTable` untuk kinerja yang lebih baik. |
| **Menyisipkan JSON di beberapa sel** | Letakkan penanda berbeda di sel lain, misalnya `&=OrdersJson.Orders[0].Id` untuk mengambil bidang individual. |

**Tips pro:** Saat menangani JSON yang sangat besar, tingkatkan buffer memori workbook (`WorkbookSettings.MemorySetting`) untuk menghindari `OutOfMemoryException`.

## Menguji solusi

1. Bangun dan jalankan aplikasi console (`dotnet run`).  
2. Verifikasi konsol mencetak path lengkap ke file yang dihasilkan.  
3. Buka file tersebut di Excel atau penampil spreadsheet lainnya.  
4. Pastikan sel A1 berisi string array JSON persis seperti yang ditunjukkan di atas.

Jika sel berisi teks penanda (`&=OrdersJson...`) alih‑alih JSON, periksa kembali bahwa processor dipanggil **setelah** penanda ditempatkan dan bahwa string JSON valid.

## Kesimpulan

Anda kini tahu cara **membuat Excel dari JSON** menggunakan Aspose.Cells Smart Markers, cara **mengonversi JSON ke Excel**, menyisipkan payload JSON langsung ke dalam sel, dan **menyimpan workbook xlsx** dengan satu baris kode. Pendekatan ini menghilangkan parsing manual, bekerja dengan struktur JSON apa pun, dan menghasilkan file Excel yang bersih serta sesuai standar.

### Langkah selanjutnya

- Jelajahi **loop Smart Marker** (`&=OrdersJson.Orders`) untuk menghasilkan baris per pesanan alih‑alih satu string JSON.  
- Gabungkan teknik ini dengan **rumus Excel** untuk menghitung total dari data yang disisipkan.  
- Pelajari cara **membaca JSON kembali dari Excel** menggunakan `Workbook.Load` dan `SmartMarkerProcessor` secara terbalik.

Silakan bereksperimen dengan bentuk JSON yang berbeda, banyak worksheet, atau mengekspor ke format lain seperti CSV atau PDF. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}