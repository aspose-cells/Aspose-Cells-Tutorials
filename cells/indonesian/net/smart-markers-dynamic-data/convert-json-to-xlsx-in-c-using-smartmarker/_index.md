---
category: general
date: 2026-10-10
description: Konversi JSON ke XLSX di C# dengan SmartMarker – pelajari cara mengimpor
  JSON ke Excel dan mengisi workbook secara programatis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: id
lastmod: 2026-10-10
og_description: Konversi JSON ke XLSX di C# dengan SmartMarker. Ikuti panduan ini
  untuk mengimpor JSON ke Excel, membuat workbook Excel dengan C#, dan mengisi Excel
  dari JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: Mengonversi JSON ke XLSX di C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Konversi JSON ke XLSX di C# menggunakan SmartMarker
url: /id/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi JSON ke XLSX di C# menggunakan SmartMarker

Jika Anda perlu **mengonversi JSON ke XLSX di C#**, panduan ini menunjukkan cara **mengimpor JSON ke Excel** dan **mengisi Excel dari JSON** dengan hanya beberapa baris kode. Anda akan melihat cara **membuat workbook Excel C#**, mengonfigurasi processor SmartMarker, dan akhirnya **mengimpor JSON ke sel worksheet**.

> **Apa yang akan Anda dapatkan** – contoh yang dapat dijalankan sepenuhnya yang membaca array JSON, memperlakukannya sebagai satu rekaman, dan menulis data ke file `.xlsx` yang siap untuk pelaporan atau analisis lanjutan.

## Mengonversi JSON ke XLSX – ikhtisar

SmartMarker adalah bagian dari pustaka Aspose.Cells dan memungkinkan Anda mengikat JSON, XML, atau objek .NET apa pun langsung ke template Excel. Dalam tutorial ini kami:

1. **Membuat workbook Excel** dalam memori.
2. **Memuat data JSON** yang mewakili daftar sederhana orang.
3. **Mengonfigurasi SmartMarker** untuk memperlakukan array JSON sebagai satu rekaman (`ArrayAsSingle = true`).
4. **Memproses worksheet**, membiarkan SmartMarker mengganti penanda dengan nilai JSON.
5. **Menyimpan workbook** sebagai file `.xlsx`.

Seluruh alur berjalan pada .NET 6+ dan hanya memerlukan paket NuGet `Aspose.Cells`.

## Langkah 1: Membuat workbook Excel di C#

Pertama, tambahkan paket Aspose.Cells ke proyek Anda:

```bash
dotnet add package Aspose.Cells
```

Sekarang Anda dapat menginstansiasi `Workbook` baru. Workbook dimulai kosong, tetapi Anda dapat menambahkan worksheet dan menempatkan tag SmartMarker di mana data JSON harus muncul.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **Mengapa kami membuat workbook terlebih dahulu** – SmartMarker bekerja pada objek `Worksheet` yang sudah ada; workbook menyediakan wadah untuk semua operasi selanjutnya.

## Langkah 2: Menentukan data JSON dan mengonfigurasi SmartMarker

Kami akan menggunakan payload JSON kecil yang berisi dua orang. Opsi `ArrayAsSingle` memberi tahu SmartMarker untuk memperlakukan seluruh array sebagai satu rekaman logis, yang ideal ketika Anda menginginkan tabel sederhana tanpa loop bersarang.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

> **Tip:** Jika Anda menghilangkan `ArrayAsSingle`, SmartMarker akan mencoba membuat rekaman terpisah untuk setiap elemen array, yang dapat menyebabkan baris duplikat atau tata letak yang tidak terduga.

## Langkah 3: Menyisipkan tag SmartMarker ke dalam worksheet

Tag SmartMarker adalah placeholder teks biasa yang dikelilingi oleh `&`. Tempatkan mereka di sel tempat Anda ingin nilai JSON muncul. Dalam contoh ini kami menulis tag secara langsung melalui kode, tetapi Anda juga dapat merancang template di Excel terlebih dahulu.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

> **Penjelasan:** `&=Name&` memberi tahu SmartMarker untuk mengganti sel dengan bidang `Name` dari objek JSON, sementara `&=Age&` melakukan hal yang sama untuk `Age`.

## Langkah 4: Memproses worksheet – mengisi Excel dari JSON

Sekarang biarkan SmartMarker membaca string JSON dan mengisi placeholder.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

Di balik layar, SmartMarker mem-parsing `jsonData`, memetakan setiap properti objek ke tag yang sesuai, dan secara otomatis memperluas baris karena `ArrayAsSingle` bernilai `true`. Setelah diproses, worksheet terlihat seperti ini:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

## Langkah 5: Menyimpan file XLSX

Akhirnya, tulis workbook yang telah terisi ke disk.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Menjalankan program membuat `SmartMarkerJson.xlsx` di desktop Anda. Membuka file tersebut di Excel menampilkan tabel bersih dengan data JSON yang diimpor dengan benar.

## Kesalahan umum saat mengimpor JSON ke worksheet

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **Missing SmartMarker tags** | SmartMarker hanya mengganti sel yang berisi `&=...&`. | Periksa kembali ejaan tag dan kapitalisasinya secara tepat. |
| **Incorrect JSON format** | Tanda kutip tunggal (`'`) tidak valid sebagai JSON untuk parser bawaan. | Gunakan tanda kutip ganda (`\"`) atau biarkan Aspose.Cells menangani format yang lebih longgar seperti yang ditunjukkan. |
| **Array treated as multiple records** | Nilai default `ArrayAsSingle` adalah `false`. | Setel `processor.Options.ArrayAsSingle = true` ketika Anda menginginkan tabel datar. |
| **Saving to a read‑only folder** | `workbook.Save` melemparkan pengecualian. | Pilih direktori yang dapat ditulisi (mis., Desktop atau folder sementara). |

## Memperluas solusi

- **Multiple worksheets:** Buat lembar tambahan dan panggil `processor.Process` pada masing‑masing dengan sumber JSON yang berbeda.
- **Styling:** Setelah diproses, terapkan gaya sel (font, border) seperti operasi Aspose.Cells biasa.
- **Large datasets:** Untuk ribuan baris, pertimbangkan streaming workbook untuk mengurangi penggunaan memori (`WorkbookDesigner` atau `SaveOptions` dengan `EnableMemoryOptimization`).

## Kesimpulan

Anda sekarang tahu cara **mengonversi JSON ke XLSX di C#** menggunakan Aspose.Cells SmartMarker. Alur kerja lengkap—**membuat workbook Excel C#**, menambahkan tag SmartMarker, mengonfigurasi processor, **mengisi Excel dari JSON**, dan menyimpan file—memungkinkan Anda **mengimpor JSON ke sel worksheet** dengan kode minimal.  

Silakan bereksperimen dengan struktur JSON yang lebih kompleks, menambahkan formula, atau menghasilkan diagram langsung dari data yang terisi. Jika Anda menyukai panduan ini, coba tutorial berikutnya tentang **cara mengimpor JSON ke Excel** untuk pembuatan diagram atau tentang **membuat workbook Excel C#** dengan pemformatan lanjutan.

---


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Mengonversi JSON ke Excel dengan C# – Panduan Langkah‑per‑Langkah](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [Cara Menyisipkan JSON ke Template Excel – Langkah‑per‑Langkah](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [Buat Workbook Excel C# – Sisipkan JSON dan Simpan sebagai XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}