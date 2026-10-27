---
category: general
date: 2026-08-11
description: Impor JSON ke Excel menggunakan C# dan Aspose.Cells. Muat JSON ke dalam
  DataSet, proses smart markers, dan simpan sebagai XLSX dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import json to excel
- convert json to xlsx
- export json data excel
- load json into dataset
- save workbook c#
language: id
lastmod: 2026-08-11
og_description: Impor JSON ke Excel menggunakan C# dan Aspose.Cells. Panduan ini menunjukkan
  cara memuat JSON ke dalam DataSet, memproses smart marker, dan menyimpan workbook
  sebagai file xlsx, memungkinkan ekspor data yang mulus.
og_image_alt: Screenshot of C# code importing JSON into an Excel workbook using Aspose.Cells
og_title: Impor JSON ke Excel dengan C# – panduan langkah demi langkah lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Import json to excel using C# and Aspose.Cells. Load JSON into a DataSet,
    process smart markers, and save as xlsx in minutes.
  headline: Import json to excel in C# – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: '`ReadJson` still creates an empty `DataTable`. The smart marker will
      produce only the header row, which is often the desired outcome for reporting
      templates.'
    question: What if the JSON array is empty?
  - answer: Yes. Load each array into its own `DataTable` within the same `DataSet`,
      then call `ProcessSmartMarkers` on each worksheet, referencing the appropriate
      table name in the marker (e.g., `&=Table(Orders)`).
    question: Can I import multiple JSON arrays into different sheets?
  - answer: After `ReadJson`, reorder columns by manipulating `dataSet.Tables[0].Columns`
      before processing the smart marker.
    question: How do I control column order?
  - answer: 'If you need the raw JSON string in a cell, skip the `DataSet` step and
      assign it directly: `worksheet.Cells["A1"].PutValue(jsonData);`'
    question: Is it possible to write JSON directly to a single cell as a string?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- JSON
- Excel automation
title: Impor JSON ke Excel di C# – Panduan Langkah demi Langkah
url: /id/net/smart-markers-dynamic-data/import-json-to-excel-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Impor json ke excel di C# – panduan langkah demi langkah

Jika Anda perlu mengimpor json ke excel dengan C#, tutorial ini akan memandu Anda melalui seluruh proses. Anda akan belajar cara memuat JSON ke dalam DataSet, menerapkan smart marker, dan menyimpan hasilnya sebagai file xlsx. Pendekatan yang sama juga memungkinkan Anda mengonversi json ke xlsx untuk pipeline pelaporan atau skrip migrasi data.

Panduan ini mencakup setiap baris kode yang diperlukan, menjelaskan mengapa setiap langkah penting, dan menyoroti jebakan umum. Pada akhir tutorial Anda dapat mengekspor data json ke excel tanpa menulis parser khusus, dan Anda akan memahami cara menyimpan workbook c# secara siap produksi. Tidak diperlukan alat eksternal selain Aspose.Cells.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru terinstal  
- Visual Studio 2022 (atau IDE apa pun yang mendukung .NET)  
- Paket NuGet Aspose.Cells untuk .NET (`Install-Package Aspose.Cells`)  
- File templat Excel yang berisi smart marker (misalnya `Template.xlsx`)  

Templat harus memiliki satu sel dengan smart marker `&=Table(Data)` dimana `Data` cocok dengan nama DataTable yang akan Anda berikan.

## Impor json ke excel – siapkan proyek

Buat aplikasi konsol baru dan tambahkan referensi Aspose.Cells:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // The complete workflow is demonstrated in the following steps.
        }
    }
}
```

Menambahkan direktif `using` di bagian atas memungkinkan kompilator menemukan `DataSet`, `Workbook`, dan tipe terkait. Fondasi ini diperlukan untuk setiap operasi selanjutnya.

## Konversi json ke xlsx – muat JSON ke dalam DataSet

Langkah fungsional pertama adalah mengubah string JSON menjadi `DataSet`. Aspose.Cells menyediakan ekstensi `ReadJson` yang praktis untuk mem-parsing array objek langsung ke dalam tabel.

```csharp
// Step 1: Define the JSON source
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

// Step 2: Load the JSON into a DataSet
DataSet dataSet = new DataSet();
dataSet.ReadJson(jsonData);
```

**Mengapa ini penting:**  
`ReadJson` secara otomatis membuat `DataTable` bernama `Table` (atau nama elemen root) dan mengisi kolom berdasarkan kunci JSON. Ini menghilangkan kebutuhan looping manual dan menjamin tipe data ditafsirkan dengan benar. Jika JSON Anda berisi objek bersarang, Aspose.Cells akan meratakannya menjadi tabel terpisah yang dapat Anda referensikan nanti.

**Tip:** Jika payload JSON berukuran besar, pertimbangkan untuk streaming dengan `StringReader` agar tidak memuat seluruh string ke memori.

## Ekspor data json ke excel – buka templat Excel dengan smart marker

Selanjutnya, buka workbook yang berisi smart marker. Smart marker memberi tahu Aspose.Cells di mana harus menyisipkan data dari `DataSet`.

```csharp
// Step 3: Open the Excel template that contains a smart marker
Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");
```

**Mengapa ini penting:**  
Templat memisahkan pemformatan dari kode. Anda dapat merancang tampilan akhir di Excel (font, border, pemformatan bersyarat) dan membiarkan perpustakaan menangani penyisipan data. Sintaks smart marker `&=Table(Data)` menginstruksikan engine untuk menulis seluruh `DataTable` ke sel tempat marker berada.

## Ekspor data json ke excel – proses smart marker

Sekarang proses smart marker, dengan memberikan `DataTable` yang telah dibuat dari JSON.

```csharp
// Step 4: Process the smart marker, writing the entire array into a single cell
workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);
```

**Mengapa ini penting:**  
`ProcessSmartMarkers` membaca marker, memperluas tabel secara vertikal, dan mempertahankan pemformatan sel asli. Metode ini juga menghormati lebar kolom dan secara otomatis menerapkan format angka berdasarkan tipe .NET yang mendasarinya.

**Kasus tepi:** Jika sel target sudah berisi data, metode ini akan menimpanya. Untuk mempertahankan konten yang ada, letakkan marker di area khusus pada templat.

## Simpan workbook c# – tulis file akhir

Akhirnya, simpan workbook sebagai file `.xlsx`. Anda dapat memilih lokasi mana saja yang dapat ditulisi oleh aplikasi Anda.

```csharp
// Step 5: Save the resulting workbook
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);
```

**Mengapa ini penting:**  
Menentukan `SaveFormat.Xlsx` menjamin output mematuhi standar Open XML, sehingga dapat dibaca oleh aplikasi spreadsheet modern. Jika Anda memerlukan file legacy `.xls`, ganti `SaveFormat.Xlsx` dengan `SaveFormat.Excel97To2003`.

**Tips pro:** Gunakan `SaveOptions` untuk mengontrol tingkat kompresi pada file besar, misalnya, `var opts = new XlsSaveOptions { CompressionLevel = CompressionLevel.Maximum }; workbook.Save("out.xls", opts);`

## Kode sumber lengkap

Menggabungkan semua langkah menghasilkan program yang dapat dijalankan:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Define the JSON source
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

            // Load the JSON into a DataSet
            DataSet dataSet = new DataSet();
            dataSet.ReadJson(jsonData);

            // Open the Excel template that contains a smart marker
            Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");

            // Process the smart marker, writing the entire array into a single cell
            workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);

            // Save the resulting workbook
            workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);

            Console.WriteLine("JSON has been imported to Excel successfully.");
        }
    }
}
```

**Output yang diharapkan:**  
Menjalankan program akan membuat `JsonSingleCell.xlsx`. Membuka file tersebut menampilkan dua baris (`John`, `30` dan `Anna`, `25`) terisi di bawah sel smart‑marker, mempertahankan pemformatan header apa pun yang Anda definisikan di `Template.xlsx`.

![Contoh kode impor json ke excel](image.png "Contoh kode impor json ke excel")

## Pertanyaan umum dan cara menanganinya

- **Bagaimana jika array JSON kosong?**  
  `ReadJson` tetap membuat `DataTable` kosong. Smart marker akan menghasilkan hanya baris header, yang sering menjadi hasil yang diinginkan untuk templat pelaporan.

- **Bisakah saya mengimpor beberapa array JSON ke lembar berbeda?**  
  Ya. Muat setiap array ke dalam `DataTable` masing‑masing dalam satu `DataSet`, lalu panggil `ProcessSmartMarkers` pada setiap worksheet, dengan merujuk nama tabel yang sesuai di marker (misalnya `&=Table(Orders)`).

- **Bagaimana cara mengontrol urutan kolom?**  
  Setelah `ReadJson`, ubah urutan kolom dengan memanipulasi `dataSet.Tables[0].Columns` sebelum memproses smart marker.

- **Apakah memungkinkan menulis JSON langsung ke satu sel sebagai string?**  
  Jika Anda memerlukan string JSON mentah di sebuah sel, lewati langkah `DataSet` dan tetapkan secara langsung: `worksheet.Cells["A1"].PutValue(jsonData);`

## Kesimpulan

Anda kini tahu cara mengimpor json ke excel di C# menggunakan Aspose.Cells, mulai dari memuat JSON ke DataSet hingga memproses smart marker dan menyimpan workbook c#. Solusi end‑to‑end ini memungkinkan Anda mengonversi json ke xlsx dengan cepat, mengekspor data json

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Effortlessly Import JSON into Excel using Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)
- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Efficiently Import JSON to Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}