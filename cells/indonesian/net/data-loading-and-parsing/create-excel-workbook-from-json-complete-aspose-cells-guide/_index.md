---
category: general
date: 2026-02-14
description: Buat workbook Excel menggunakan Aspose.Cells dan pelajari cara memproses
  JSON, mengonversi JSON ke Excel, serta memuat JSON ke dalam Excel dalam beberapa
  langkah mudah.
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: id
og_description: Buat buku kerja Excel dengan Aspose.Cells, pelajari cara memproses
  JSON, mengonversi JSON ke Excel, dan memuat JSON ke Excel dengan cepat dan andal.
og_title: Buat Workbook Excel dari JSON – Tutorial Aspose.Cells Langkah demi Langkah
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Buat Workbook Excel dari JSON – Panduan Lengkap Aspose.Cells
url: /id/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel dari JSON – Panduan Lengkap Aspose.Cells

Pernah perlu **create Excel workbook** dari sepotong JSON tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Banyak pengembang mengalami hal yang sama ketika mereka memiliki payload JSON dan membutuhkan spreadsheet rapi untuk pelaporan atau pertukaran data.  

Berita baik? Dengan **Aspose.Cells** Anda dapat mengubah JSON tersebut menjadi file Excel yang lengkap hanya dengan beberapa baris kode. Dalam tutorial ini kami akan membahas **how to process JSON**, **convert JSON to Excel**, dan **load JSON into Excel** menggunakan `SmartMarkerProcessor` yang kuat. Pada akhir tutorial Anda akan memiliki workbook siap‑simpan dan gambaran jelas tentang opsi‑opsi yang dapat Anda sesuaikan.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan proyek Aspose.Cells untuk penanganan JSON.  
- Kode tepat yang diperlukan untuk **create Excel workbook** dari array JSON.  
- Mengapa opsi `ArrayAsSingle` penting dan kapan Anda mungkin ingin mengubahnya.  
- Tips untuk menangani struktur JSON yang lebih besar, penanganan error, dan penyimpanan file.  

> **Prasyarat:** .NET 6+ (atau .NET Framework 4.6+), paket NuGet Aspose.Cells untuk .NET, dan pemahaman dasar tentang C#. Tidak diperlukan pustaka lain.

---

## Langkah 1: Instal Aspose.Cells dan Tambahkan Namespace yang Diperlukan

Sebelum kode apa pun dijalankan, Anda perlu mereferensikan pustaka Aspose.Cells dalam proyek Anda.

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **Tip Pro:** Jika Anda menggunakan Visual Studio, UI NuGet Package Manager melakukan pekerjaan yang sama—cukup cari *Aspose.Cells* dan klik Install.

---

## Langkah 2: Siapkan Data JSON yang Ingin Anda Konversi

`SmartMarkerProcessor` bekerja dengan string JSON apa pun, tetapi Anda harus memutuskan bagaimana pustaka harus menginterpretasikan array. Dalam contoh ini kami akan memperlakukan array numerik sederhana sebagai **single record**, yang berguna ketika Anda hanya membutuhkan daftar nilai datar.

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **Mengapa ini penting:** Secara default, Aspose.Cells memperlakukan setiap elemen array sebagai record terpisah. Menetapkan `ArrayAsSingle = true` menggabungkan seluruh array menjadi satu record, yang cocok untuk banyak skenario pelaporan.

---

## Langkah 3: Buat Instance Workbook Baru

Sekarang kami benar‑benarnya **create Excel workbook** di memori. Belum ada file yang ditulis; kami hanya menyiapkan kontainer.

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

Pada titik ini `workbook.Worksheets[0]` adalah lembar kosong bernama *Sheet1*. Anda dapat mengganti namanya nanti jika diinginkan.

---

## Langkah 4: Konfigurasikan Opsi SmartMarker untuk Pemrosesan JSON

Kelas `SmartMarkerOptions` memberi Anda kontrol detail tentang bagaimana JSON diinterpretasikan. Flag kunci untuk skenario kami adalah `ArrayAsSingle`.

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **Kapan mengubah ini:** Jika JSON Anda mewakili kumpulan baris (mis., array objek), biarkan `ArrayAsSingle` tetap `false`. Setiap objek akan menjadi baris baru secara otomatis.

---

## Langkah 5: Jalankan Pemrosesan Smart Marker pada Worksheet

Dengan workbook dan opsi siap, kami memasukkan JSON ke dalam processor. Processor memindai worksheet untuk smart marker (placeholder) dan menggantinya dengan data dari JSON. Karena kami tidak memiliki marker eksplisit, processor hanya membuat tata letak default.

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

Jika Anda ingin mengontrol sel tepat di mana data dimulai, Anda dapat menambahkan marker seperti `"${Array}"` ke sel **A1** sebelum menjalankan processor. Untuk tutorial ini kami mengandalkan perilaku default, yang menulis nilai array ke sel berurutan mulai dari **A1**.

---

## Langkah 6: Simpan Workbook ke Disk (atau Stream)

Langkah terakhir adalah menyimpan workbook. Anda dapat menyimpannya ke file, ke memory stream, atau bahkan mengembalikannya langsung dari API web.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Menjalankan program lengkap menghasilkan file Excel dengan angka **1**, **2**, dan **3** ditempatkan di sel **A1**, **A2**, dan **A3** masing‑masing.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah aplikasi konsol lengkap yang siap dijalankan yang menggabungkan semua langkah. Salin‑tempel ke proyek konsol C# baru dan tekan **F5**.

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Output yang diharapkan di Excel**

| Angka |
|-------|
| 1 |
| 2 |
| 3 |

Baris header (“Angka”) bersifat opsional tetapi menunjukkan bagaimana Anda dapat mencampur edit sel manual dengan pemrosesan smart‑marker.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika JSON saya berupa objek, bukan array?

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

Anda masih dapat menggunakan `SmartMarkerProcessor`. Tempatkan marker seperti `${Name}`, `${Age}`, `${Country}` di worksheet, lalu panggil `StartSmartMarkerProcessing`. Processor akan menggantikan setiap marker dengan nilai yang sesuai.

### Bagaimana cara menangani file JSON besar (megabyte)?

- **Stream the JSON**: Alih-alih memuat seluruh string, baca file ke dalam `StreamReader` dan berikan teks ke `StartSmartMarkerProcessing`.  
- **Increase memory limit**: Tetapkan `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` jika Anda mengalami `OutOfMemoryException`.  
- **Chunk processing**: Bagi JSON menjadi array yang lebih kecil dan proses setiap bagian pada worksheet baru.

### Bisakah saya mengekspor ke CSV alih-alih XLSX?

Tentu saja. Setelah pemrosesan, cukup panggil:

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

Tata letak data tetap sama; hanya format file yang berubah.

### Bagaimana jika saya perlu memformat sel (font, warna) setelah memuat JSON?

Anda dapat menerapkan pemformatan setelah langkah smart‑marker:

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

Karena processor berjalan terlebih dahulu, setiap pemformatan yang Anda terapkan setelahnya tidak akan ditimpa.

---

## Tips & Praktik Terbaik

- **Always set `ArrayAsSingle` deliberately** – melupakan flag ini adalah sumber umum duplikasi baris yang tidak terduga.  
- **Validate JSON before processing** – string yang tidak valid akan melempar `JsonParseException`. Bungkus pemanggilan dalam blok `try/catch` untuk penanganan error yang elegan.  
- **Use named smart markers** (`${Orders}`) untuk keterbacaan, terutama saat menangani objek JSON bersarang.  
- **Keep the workbook in memory** jika Anda mengembalikannya dari API web; mengirim `MemoryStream` menghindari I/O disk yang tidak perlu.  
- **Version compatibility**: Kode di atas bekerja dengan Aspose.Cells 23.12 dan yang lebih baru. Periksa catatan rilis jika Anda menggunakan versi yang lebih lama.

---

## Kesimpulan

Kami baru saja menunjukkan cara **create Excel workbook** dari JSON menggunakan Aspose.Cells, mencakup semua hal mulai dari menginstal pustaka hingga menyimpan file akhir. Dengan menguasai `SmartMarkerProcessor` dan opsinya, Anda dapat **load JSON into Excel**, **convert JSON to Excel**, dan bahkan menyesuaikan output untuk skenario pelaporan yang kompleks.  

Siap untuk langkah selanjutnya? Cobalah memasukkan array objek JSON bersarang, tambahkan pemformatan bersyarat, atau ekspor hasilnya sebagai PDF—semua dengan API Aspose.Cells yang sama. Pipeline data‑to‑Excel Anda kini hanya beberapa baris kode lagi.

Jika Anda memiliki pertanyaan atau mengalami kendala, tinggalkan komentar di bawah. Selamat coding, dan nikmati mengubah JSON menjadi spreadsheet yang indah! 

![Buat Excel workbook dengan data JSON](/images/create-excel-workbook-json.png "Ilustrasi array JSON yang diubah menjadi lembar Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}