---
category: general
date: 2026-08-07
description: Konversi JSON ke XLSX di C# dengan Aspose.Cells. Pelajari cara mengekspor
  JSON ke Excel, menggunakan sumber data JSON, dan membuat workbook dari JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- export json to excel
- json data source excel
- create workbook from json
language: id
lastmod: 2026-08-07
og_description: Konversi JSON ke XLSX di C# dan ekspor JSON ke Excel dengan satu smart
  marker. Ikuti panduan ini untuk membuat workbook dari JSON dengan cepat.
og_image_alt: Screenshot showing Convert JSON to XLSX result in Excel cell
og_title: Konversi JSON ke XLSX di C# – panduan pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Convert JSON to XLSX in C# with Aspose.Cells. Learn how to export JSON
    to Excel, use a JSON data source, and create a workbook from JSON.
  headline: Convert JSON to XLSX in C# – complete step‑by‑step guide
  type: TechArticle
- description: Convert JSON to XLSX in C# with Aspose.Cells. Learn how to export JSON
    to Excel, use a JSON data source, and create a workbook from JSON.
  name: Convert JSON to XLSX in C# – complete step‑by‑step guide
  steps:
  - name: '**Define the JSON data source** – The `json` variable holds a standard
      JSON object. The outer property `Products` contains an array, which matches
      the placeholder name used later (`{{Products}}`).'
    text: '**Define the JSON data source** – The `json` variable holds a standard
      JSON object. The outer property `Products` contains an array, which matches
      the placeholder name used later (`{{Products}}`).'
  - name: '**Create a new workbook** – `Workbook()` creates an empty Excel file. The
      first worksheet is accessed via `Worksheets[0]`. The `PutValue` call inserts
      the Smart Marker placeholder in cell **A1**.'
    text: '**Create a new workbook** – `Workbook()` creates an empty Excel file. The
      first worksheet is accessed via `Worksheets[0]`. The `PutValue` call inserts
      the Smart Marker placeholder in cell **A1**.'
  - name: '**Configure Smart Marker** – `SmartMarkerOptions.ArrayAsSingle = true`
      tells the engine to treat the whole array as a single value instead of expanding
      it into multiple rows. This is the key setting for **convert json to xlsx**
      when you need the raw JSON in one cell.'
    text: '**Configure Smart Marker** – `SmartMarkerOptions.ArrayAsSingle = true`
      tells the engine to treat the whole array as a single value instead of expanding
      it into multiple rows. This is the key setting for **convert json to xlsx**
      when you need the raw JSON in one cell.'
  - name: '**Process the JSON data** – `SmartMarkerProcessor` combines the workbook,
      the options, and the `JsonDataSource`. The `Process` call replaces the placeholder
      with the JSON string.'
    text: '**Process the JSON data** – `SmartMarkerProcessor` combines the workbook,
      the options, and the `JsonDataSource`. The `Process` call replaces the placeholder
      with the JSON string.'
  - name: '**Save the workbook** – `workbook.Save` writes the file to disk. The console
      output confirms the file location and prints the exact cell content for verification.'
    text: '**Save the workbook** – `workbook.Save` writes the file to disk. The console
      output confirms the file location and prints the exact cell content for verification.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Mengonversi JSON ke XLSX di C# – panduan lengkap langkah demi langkah
url: /id/net/excel-data-import-export/convert-json-to-xlsx-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi JSON ke XLSX di C# – panduan lengkap langkah demi langkah

Jika Anda perlu **convert JSON to XLSX** dalam aplikasi .NET, panduan ini menunjukkan langkah‑langkah tepatnya. Anda akan melihat cara **export JSON to Excel** menggunakan Aspose.Cells, mengonfigurasi sumber data JSON, dan **create a workbook from JSON** dengan hanya beberapa baris kode.

Tutorial ini mencakup semua yang diperlukan untuk mengubah string JSON menjadi representasi Excel satu sel, memverifikasi output, dan menyesuaikan pendekatan untuk kumpulan data yang lebih besar. Tidak diperlukan alat eksternal selain Aspose.Cells.

## Apa yang akan Anda pelajari

* Siapkan string JSON yang mewakili array objek.  
* Buat workbook Excel dan letakkan placeholder Smart Marker.  
* Konfigurasikan **Smart Marker** sehingga seluruh array muncul sebagai satu string JSON di dalam sel.  
* Proses sumber data JSON dengan opsi **json data source excel**.  
* Simpan workbook dan pastikan sel berisi teks JSON yang diharapkan.

### Prasyarat

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+).  
* Aspose.Cells untuk .NET – versi 23.12 atau lebih baru.  
* Lingkungan pengembangan seperti Visual Studio 2022 atau VS Code.  

Menyiapkan item-item ini memungkinkan Anda menjalankan contoh tanpa konfigurasi tambahan.

## Mengonversi JSON ke XLSX – ikhtisar

Ide utama adalah membiarkan Aspose.Cells memperlakukan string JSON sebagai sumber data. Dengan menempatkan **Smart Marker** seperti `{{Products}}` di sel lembar kerja dan mengaktifkan opsi `ArrayAsSingle`, prosesor menulis seluruh array JSON ke dalam sel tersebut sebagai teks biasa. Teknik ini ideal ketika Anda ingin menyematkan JSON mentah dalam laporan Excel atau mengirim data ke hilir.

## Export JSON ke Excel: buat workbook dari JSON

Berikut ini program lengkap yang dapat dijalankan. Program ini menunjukkan setiap langkah mulai dari mendefinisikan JSON hingga menyimpan file XLSX yang dihasilkan.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Tables;          // Smart Marker classes
using Aspose.Cells.DataSource;      // JsonDataSource class

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Define the JSON data source
            var json = @"{
                ""Products"": [
                    { ""Name"": ""A"", ""Qty"": 10 },
                    { ""Name"": ""B"", ""Qty"": 20 }
                ]
            }";

            // Step 2: Create a new workbook and place a Smart Marker placeholder
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
            // The placeholder tells Smart Marker where to inject the JSON string
            worksheet.Cells["A1"].PutValue("{{Products}}");

            // Step 3: Configure Smart Marker to render the whole array as a single JSON string
            var smartMarkerOptions = new SmartMarkerOptions
            {
                // When true, the processor writes the entire array into one cell
                ArrayAsSingle = true
            };

            // Step 4: Process the JSON data with the configured options
            var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
            processor.Process(new JsonDataSource(json));

            // Step 5: Save the workbook – cell A1 now contains the JSON array as a single string
            const string outputPath = "JsonSingleValue.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Cell A1 content:");
            Console.WriteLine(worksheet.Cells["A1"].StringValue);
        }
    }
}
```

### Penjelasan setiap langkah

1. **Define the JSON data source** – Variabel `json` menyimpan objek JSON standar. Properti luar `Products` berisi sebuah array, yang cocok dengan nama placeholder yang digunakan kemudian (`{{Products}}`).  
2. **Create a new workbook** – `Workbook()` membuat file Excel kosong. Lembar kerja pertama diakses melalui `Worksheets[0]`. Pemanggilan `PutValue` menyisipkan placeholder Smart Marker di sel **A1**.  
3. **Configure Smart Marker** – `SmartMarkerOptions.ArrayAsSingle = true` memberi tahu mesin untuk memperlakukan seluruh array sebagai satu nilai alih-alih memperluasnya menjadi beberapa baris. Ini adalah pengaturan kunci untuk **convert json to xlsx** ketika Anda membutuhkan JSON mentah dalam satu sel.  
4. **Process the JSON data** – `SmartMarkerProcessor` menggabungkan workbook, opsi, dan `JsonDataSource`. Pemanggilan `Process` menggantikan placeholder dengan string JSON.  
5. **Save the workbook** – `workbook.Save` menulis file ke disk. Output konsol mengonfirmasi lokasi file dan mencetak isi sel yang tepat untuk verifikasi.

Saat Anda membuka *JsonSingleValue.xlsx* Anda akan melihat sel **A1** berisi:

```json
[{"Name":"A","Qty":10},{"Name":"B","Qty":20}]
```

Output tersebut membuktikan operasi **export json to excel** berhasil.

## Konfigurasi sumber data JSON untuk Excel

Jika Anda perlu bekerja dengan struktur JSON yang lebih kompleks—seperti objek bersarang atau beberapa array—sesuaikan sintaks placeholder sesuai kebutuhan. Misalnya, untuk menyematkan objek bersarang Anda dapat menggunakan `{{Orders.Customer}}`. Flag `ArrayAsSingle` bekerja pada tingkat array, sehingga setiap array yang ingin Anda gabungkan harus memiliki placeholder masing‑masing.

**Tip:** Ketika JSON berisi karakter khusus (kutipan, baris baru), Aspose.Cells secara otomatis meng‑escape mereka untuk penyimpanan sel Excel. Anda tidak memerlukan langkah encoding tambahan.

## Membuat workbook dari JSON – menangani file besar

Memproses payload JSON yang sangat besar dapat meningkatkan penggunaan memori karena seluruh string JSON disimpan di memori sebelum ditulis ke sel. Untuk mengurangi hal ini:

* Gunakan parser JSON streaming jika Anda hanya membutuhkan sebagian data.  
* Bagi JSON menjadi potongan lebih kecil dan tulis setiap potongan ke sel terpisah.  
* Tingkatkan batas memori proses melalui konfigurasi runtime .NET jika Anda menemui `OutOfMemoryException`.

Pertimbangan ini menjaga pendekatan **create workbook from json** tetap dapat diskalakan.

## Kesalahan umum dan cara menghindarinya

| Gejala | Penyebab | Solusi |
|--------|----------|--------|
| Sel A1 tetap kosong setelah pemrosesan | Nama placeholder tidak cocok dengan properti JSON | Pastikan placeholder (`{{Products}}`) persis cocok dengan nama array JSON. |
| JSON muncul dengan kutipan yang di‑escape (`\"`) | Workbook disimpan dengan format file yang berbeda (misalnya CSV) | Simpan sebagai `.xlsx` atau `.xls` untuk mempertahankan teks mentah. |
| Processor melempar `ArgumentException` | Versi Aspose.Cells lebih lama dari 23.12 | Tingkatkan ke paket Aspose.Cells terbaru. |
| Output terpotong setelah 32.767 karakter | Batas karakter sel Excel tercapai | Bagi JSON ke beberapa sel atau tulis ke file teks sebagai gantinya. |

Menangani masalah ini lebih awal menghemat waktu ketika Anda **export json to excel** dalam skenario produksi.

## Verifikasi konversi

Setelah menjalankan program, buka file yang dihasilkan di Microsoft Excel atau LibreOffice Calc. String JSON harus muncul persis seperti yang dicetak di konsol. Anda juga dapat membaca sel secara programatik kembali:

```csharp
var loadedWorkbook = new Workbook("JsonSingleValue.xlsx");
string cellContent = loadedWorkbook.Worksheets[0].Cells["A1"].StringValue;
Console.WriteLine(cellContent == json ? "Conversion verified" : "Mismatch detected");
```

Pesan `Conversion verified` mengonfirmasi bahwa operasi **convert json to xlsx** mempertahankan data asli.

## Kesimpulan

Anda kini memiliki metode lengkap dan siap produksi untuk **convert JSON to XLSX** di C#. Dengan menempatkan placeholder Smart Marker, mengaktifkan `ArrayAsSingle`, dan memproses `JsonDataSource`, Anda dapat **export JSON to Excel** dalam satu langkah yang dapat diprediksi. Dari sini Anda dapat menjelajahi:

* Menambahkan beberapa placeholder untuk menyematkan beberapa array JSON.  
* Menggunakan `ArrayAsSingle = false` untuk memperluas array menjadi baris tabel.  
* Mengintegrasikan alur kerja ke dalam API ASP.NET Core untuk pembuatan laporan secara langsung.

Bereksperimenlah dengan berbagai bentuk JSON, sesuaikan opsi Smart Marker, dan Anda akan cepat menguasai pola **json data source excel** untuk skenario pelaporan atau pertukaran data apa pun. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat Workbook dan Menyisipkan JSON ke Excel](/cells/english/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/)
- [Impor Data JSON ke Excel Menggunakan Aspose.Cells Java: Panduan Komprehensif](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Impor Data Json ke Excel Aspose Cells Java](/cells/german/java/import-export/import-json-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}