---
category: general
date: 2026-03-18
description: Pelajari cara menghasilkan Excel dari JSON dengan C#, izinkan nama sheet
  duplikat, buat sheet detail, dan simpan workbook C# dalam hitungan menit.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: id
og_description: Buat Excel dari JSON menggunakan C#. Panduan ini menunjukkan cara
  mengizinkan nama lembar duplikat, membuat lembar detail, dan menyimpan workbook
  C# dengan Aspose.Cells.
og_title: Buat Excel dari JSON di C# – Tutorial Lengkap
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Menghasilkan Excel dari JSON di C# – Panduan Langkah demi Langkah
url: /id/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menghasilkan Excel dari JSON di C# – Panduan Langkah‑per‑Langkah

Pernah membutuhkan **menghasilkan Excel dari JSON** tetapi tidak yakin pustaka mana yang dapat menangani pekerjaan berat? Anda tidak sendirian. Dalam banyak aplikasi perusahaan kami menerima payload sebagai JSON dan harus menyalurkan data tersebut ke spreadsheet yang terformat rapi—pikirkan laporan penjualan, dump inventaris, atau log audit. Kabar baik? Dengan mesin SmartMarker Aspose.Cells Anda dapat mengubah string JSON menjadi file Excel lengkap hanya dalam beberapa baris kode.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari menyiapkan payload JSON, mengonfigurasi SmartMarker untuk **mengizinkan nama sheet duplikat**, membuat **sheet detail**, dan akhirnya **menyimpan workbook** gaya C#. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali di proyek .NET mana pun.

> **Ringkasan cepat:**  
> • Tujuan utama – menghasilkan Excel dari JSON.  
> • Tujuan sekunder – mengizinkan nama sheet duplikat, membuat sheet detail, menyimpan workbook C#.  

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 SDK (atau versi .NET terbaru).  
- Visual Studio 2022 atau VS Code dengan ekstensi C#.  
- Lisensi aktif atau percobaan gratis **Aspose.Cells for .NET** (paket NuGetnya adalah `Aspose.Cells`).  
- File template Excel (`template.xlsx`) yang sudah berisi tag SmartMarker seperti `&=Name` dan placeholder tabel detail.

Jika ada yang belum familiar, jangan panik—menginstal paket NuGet cukup dengan satu perintah, dan template dapat berupa workbook sederhana dengan beberapa sel placeholder.

## Gambaran Umum Solusi

Secara garis besar kita akan:

1. Mendefinisikan string JSON yang mencerminkan data yang ingin dimasukkan ke dalam sheet.  
2. Menyiapkan `SmartMarkerOptions` sehingga nama sheet duplikat diizinkan dan **sheet detail** mendapatkan nama yang dapat diprediksi.  
3. Memuat template Excel yang berisi tag SmartMarker.  
4. Menjalankan prosesor SmartMarker untuk menggabungkan data JSON ke dalam workbook.  
5. Menyimpan file akhir dengan `workbook.Save(...)`.

Setiap langkah dijelaskan di bawah ini, lengkap dengan potongan kode dan alasan mengapa langkah tersebut penting.

---

## Langkah 1 – Siapkan payload JSON yang akan digabungkan

Hal pertama yang Anda butuhkan adalah dokumen JSON yang sesuai dengan tag SmartMarker di dalam template Anda. Anggap JSON sebagai sumber kebenaran; setiap kunci menjadi placeholder di file Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Mengapa ini penting:**  
SmartMarker membaca hierarki JSON dan secara otomatis memperluas tabel untuk koleksi seperti `Orders`. Jika struktur JSON Anda tidak cocok dengan tag, proses penggabungan akan menghasilkan baris kosong secara diam‑diam—sebuah jebakan umum.

---

## Langkah 2 – Konfigurasikan SmartMarker untuk mengizinkan nama sheet duplikat dan beri nama sheet detail

Secara default Aspose.Cells melarang nama sheet duplikat, yang dapat menjadi penghalang ketika Anda menghasilkan sheet detail untuk setiap record master. Kelas `SmartMarkerOptions` memungkinkan Anda melonggarkan aturan tersebut serta menentukan pola penamaan untuk sheet detail yang baru dibuat.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Mengapa ini penting:**  
Jika Anda melakukan iterasi atas banyak pelanggan dan setiap iterasi membuat sheet baru, mesin biasanya akan melemparkan pengecualian. Menetapkan `AllowDuplicateSheetNames` ke `true` memberi tahu Aspose.Cells untuk secara otomatis menambahkan sufiks numerik, menjaga proses tetap lancar.

---

## Langkah 3 – Muat template Excel yang berisi tag SmartMarker

Template Anda adalah kanvas tempat SmartMarker melukis data. Ia dapat berisi pemformatan apa pun—warna, rumus, diagram—sehingga Anda tidak perlu membuat ulang logika tersebut secara programatik.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Tip:**  
Simpan template dalam folder yang menjadi bagian dari output proyek Anda (misalnya, `Content\Templates`). Dengan begitu Anda dapat merujuknya menggunakan jalur relatif dan menghindari hard‑coding direktori absolut.

---

## Langkah 4 – Jalankan prosesor SmartMarker dengan JSON dan opsi

Sekarang keajaiban terjadi. `SmartMarkerProcessor` membaca JSON, menghormati opsi yang Anda tetapkan, dan mengisi workbook sesuai.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Apa yang terjadi di balik layar?**  
- Prosesor memindai setiap sel untuk penanda seperti `&=Name` atau `&=Orders.Item`.  
- Ia menggantikan penanda sederhana dengan nilai skalar (`Name`, `Date`).  
- Untuk koleksi (`Orders`), ia membuat sheet detail baru (dengan nama “Detail”) dan mengisi baris tabel untuk setiap item.  
- Karena kami mengizinkan nama sheet duplikat, jika template sudah memiliki sheet bernama “Detail”, mesin akan membuat “Detail (2)”.

---

## Langkah 5 – Simpan workbook yang telah digabungkan ke disk

Akhirnya, tulis workbook yang telah terisi ke file. Anda dapat memilih format apa pun yang didukung Aspose.Cells—XLSX, CSV, PDF, dll. Di sini kami tetap menggunakan XLSX modern.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Mengapa ini penting:**  
Menyimpan adalah saat Anda benar‑benar **menyimpan workbook C#**. Jika Anda perlu mengalirkan file kembali ke klien web, Anda dapat menggunakan `workbook.Save(Stream, SaveFormat.Xlsx)` sebagai gantinya.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut adalah aplikasi konsol lengkap yang siap dijalankan. Pastikan Anda telah menginstal paket NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) sebelum melakukan kompilasi.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Hasil yang Diharapkan

- **Sheet 1** (sheet master) akan menampilkan “John” di sel `Name` dan “2023‑01‑01” di sel `Date`.  
- Sebuah sheet **Detail** baru akan muncul, berisi tabel dengan dua baris: satu untuk pesanan Laptop dan satu untuk pesanan Mouse.  
- Jika template sudah memiliki sheet bernama “Detail”, sheet baru akan dinamai “Detail (2)”, berkat flag `AllowDuplicateSheetNames`.

![Excel output showing master sheet with name and date, plus a Detail sheet with order rows](excel-output.png "generate excel from json result")

*Image alt text:* **generate excel from json – example workbook with master and detail sheets**

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika JSON saya berisi koleksi bersarang?

SmartMarker dapat menangani array bersarang, tetapi Anda perlu menambahkan sheet detail tambahan atau menggunakan penanda hierarkis. Misalnya, `&=Orders.SubItems.Product` akan secara otomatis menghasilkan sheet tingkat ketiga.

### Bagaimana cara menyesuaikan pola penamaan untuk sheet duplikat?

Alih‑alih menggunakan `DetailSheetNewName` statis, Anda dapat menetapkan callback melalui `smartMarkerOptions.DetailSheetNameGenerator`. Ini memungkinkan Anda menyisipkan timestamp atau ID unik ke dalam nama sheet.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Bisakah saya menghasilkan CSV alih‑alih XLSX?

Tentu saja. Ganti pemanggilan `Save` terakhir dengan:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Sisa alur tetap sama.

### Apakah ini bekerja di ASP.NET Core?

Ya. Kode yang sama dapat dijalankan di dalam aksi controller. Cukup alirkan workbook ke respons:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Pro Tips & Pitfalls

- **Pro tip:** Simpan tag SmartMarker Anda di sheet “Template” terpisah. Dengan begitu Anda dapat melindungi sheet tersebut dari edit tidak sengaja sekaligus tetap memungkinkan prosesor membacanya.  
- **Waspada:** Kunci JSON yang mengandung spasi atau karakter khusus. Aspose.Cells mengharapkan pengidentifikasi JavaScript yang valid; ubah namanya atau gunakan atribut `JsonProperty` jika Anda mendeserialisasi dari POCO.  
- **Tip performa:** Jika Anda memproses ribuan baris, setel `smartMarkerOptions.EnableCache = true` untuk menggunakan kembali penanda yang telah dikompilasi.  
- **Pemeriksaan versi:** Kode di atas menargetkan Aspose.Cells 23.9+. Versi lebih lama mungkin belum mendukung `AllowDuplicateSheetNames`.

---

## Kesimpulan

Anda kini memiliki resep lengkap‑end‑to‑end untuk **menghasilkan Excel dari JSON** di C#. Dengan mengonfigurasi `SmartMarkerOptions` kami menunjukkan cara **mengizinkan nama sheet duplikat**, mengendalikan penamaan **sheet detail**, dan akhirnya **menyimpan workbook** gaya C#. Pendekatan ini sepenuhnya mandiri—tanpa layanan eksternal, hanya satu paket NuGet.

Langkah selanjutnya? Coba ganti sumber JSON dengan API nyata

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}