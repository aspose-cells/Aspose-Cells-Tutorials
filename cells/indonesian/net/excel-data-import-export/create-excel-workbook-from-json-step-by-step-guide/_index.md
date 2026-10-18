---
category: general
date: 2026-03-25
description: Buat buku kerja Excel dari JSON dan simpan buku kerja sebagai xlsx. Pelajari
  cara mengekspor JSON ke xlsx, menghasilkan Excel dari JSON, dan mengisi Excel dari
  JSON dalam hitungan menit.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: id
og_description: Buat buku kerja Excel dari JSON secara instan. Panduan ini menunjukkan
  cara mengekspor JSON ke XLSX, menghasilkan Excel dari JSON, dan mengisi Excel dari
  JSON dengan Aspose.Cells.
og_title: Buat Workbook Excel dari JSON – Tutorial C# Lengkap
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Buat Workbook Excel dari JSON – Panduan Langkah demi Langkah
url: /id/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel dari JSON – Tutorial Lengkap C#

Pernah perlu **create excel workbook** dari payload JSON tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian; banyak pengembang mengalami kebuntuan saat mencoba mengubah data API menjadi spreadsheet yang rapi. Kabar baiknya? Dengan beberapa baris C# dan Aspose.Cells Anda dapat **export json to xlsx**, **generate excel from json**, dan **populate excel from json** tanpa harus menggunakan konverter pihak ketiga.

Dalam panduan ini kami akan membahas seluruh proses—mulai dari string JSON mentah, menaruhnya ke dalam SmartMarker, dan akhirnya **save workbook as xlsx** ke disk. Pada akhir tutorial Anda akan memiliki file Excel siap pakai yang tampak seperti ini:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Jika Anda sudah menggunakan Aspose.Cells di bagian lain proyek Anda, Anda dapat menggunakan kembali instance `Workbook` yang sama untuk beberapa impor JSON—sangat berguna untuk pemrosesan batch.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework terbaru yang mendukung C# 10)
- **Aspose.Cells for .NET** – instal via NuGet: `dotnet add package Aspose.Cells`
- Pemahaman dasar tentang sintaks C# (tidak memerlukan pengetahuan mendalam tentang Excel)

Itu saja. Tanpa layanan eksternal, tanpa COM interop, hanya kode managed murni.

---

## Langkah 1: Inisialisasi Workbook Excel Baru

Hal pertama yang kami lakukan adalah membuat objek workbook baru. Anggap saja ini membuka file Excel kosong di mana nanti kami akan menaruh data.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Mengapa memulai dengan workbook baru? Ini menjamin kanvas bersih, mencegah sisa gaya dari eksekusi sebelumnya, dan menjaga ukuran file tetap minimal—sempurna untuk pipeline otomatis.

---

## Langkah 2: Siapkan Data JSON yang Ingin Diimpor

Untuk demonstrasi kami akan menggunakan array JSON kecil, tetapi Anda dapat menggantinya dengan JSON valid apa pun yang Anda terima dari layanan web, file, atau kueri basis data.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Perhatikan tanda kutip yang di‑escape ganda (`\"`)—itu hanya sintaks literal string C#. Dalam skenario dunia nyata Anda mungkin akan membaca ini dari file:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Langkah 3: Beri Tahu SmartMarker untuk Menganggap Seluruh Array sebagai Satu Record

Engine SmartMarker milik Aspose.Cells dapat mengiterasi koleksi secara otomatis. Dengan mengaktifkan **ArrayAsSingle**, kami memperlakukan seluruh array JSON sebagai satu record, tepat seperti yang dibutuhkan untuk tabel datar.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Jika Anda lupa mengatur flag ini, SmartMarker akan mencoba membuat sheet terpisah untuk setiap elemen—tentu bukan yang Anda inginkan saat menghasilkan tabel sederhana.

---

## Langkah 4: Letakkan Token SmartMarker di Worksheet

Token SmartMarker terlihat seperti `${jsonArray}`. Saat processor dijalankan, token tersebut digantikan dengan data dari sumber JSON. Kami akan menaruh token di sel **A1** sehingga output dimulai dari pojok kiri‑atas.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Anda juga dapat memformat baris header terlebih dahulu sebelum pemrosesan. Misalnya, beri font tebal pada baris pertama:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Langkah 5: Jalankan Processor SmartMarker

Sekarang keajaiban terjadi. Processor membaca JSON, memetakan setiap properti ke kolom, dan menulis baris‑baris di bawah token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Di balik layar, Aspose.Cells:

1. Mengurai JSON menjadi objek .NET.
2. Mencocokkan nama properti (`Name`, `Score`) dengan header kolom.
3. Menulis setiap elemen array sebagai baris baru.

Jika JSON Anda berisi objek bersarang, Anda dapat merujuknya dengan notasi titik (`${parent.child}`) – fitur berguna untuk laporan yang lebih kompleks.

---

## Langkah 6: Simpan Workbook sebagai File XLSX

Akhirnya, simpan workbook ke disk. Ekstensi file `.xlsx` memberi tahu Excel (dan kebanyakan aplikasi spreadsheet lainnya) bahwa ini adalah workbook OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Tentu saja, Anda juga dapat mengalirkan workbook langsung ke respons HTTP jika Anda membangun API web:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan yang menggabungkan semua langkah di atas. Salin‑tempel ke proyek konsol baru dan tekan **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Expected result:** Membuka `json-single.xlsx` menampilkan dua baris di bawah header tebal—`John` dengan skor `90` dan `Anna` dengan `85`. Nama kolom secara otomatis diambil dari nama properti JSON.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika kunci JSON saya mengandung spasi atau karakter khusus?

SmartMarker mengharapkan nama identifier yang valid. Ganti spasi dengan garis bawah atau gunakan pemetaan khusus:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Bagaimana cara mengekspor array JSON besar (ribuan baris)?

Processor mengalirkan data secara internal, sehingga penggunaan memori tetap rendah. Namun, Anda mungkin ingin:

- Meningkatkan batas `MaxRows` worksheet (`worksheet.Cells.MaxRow = 1_048_576;` – batas maksimum Excel).
- Menonaktifkan gridlines untuk meningkatkan performa (`worksheet.IsGridlinesVisible = false;`).

### Bisakah saya menambahkan beberapa tabel JSON ke workbook yang sama?

Tentu. Letakkan token SmartMarker yang berbeda di rentang terpisah (mis., `${orders}` di `A10`, `${customers}` di `D1`) dan panggil `Process` sekali per token atau sekali dengan objek JSON komposit yang berisi kedua array.

---

## Bonus: Menambahkan Grafik Sederhana (Opsional)

Jika Anda ingin memvisualisasikan skor, tambahkan grafik kolom cepat setelah data terisi:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

---

## Kesimpulan

Anda kini tahu **how to create excel workbook** dari string JSON, **export json to xlsx**, **generate excel from json**, dan **populate excel from json** menggunakan fitur SmartMarker Aspose.Cells. Solusi lengkap—inisialisasi workbook, konfigurasi SmartMarker, pemrosesan JSON, dan penyimpanan file—hanya memerlukan beberapa baris kode, namun dapat menangani set data yang sangat besar.

Langkah selanjutnya? Coba ganti JSON statis dengan panggilan API, tambahkan pemformatan bersyarat berdasarkan skor, atau hasilkan beberapa sheet untuk domain data yang berbeda. Pola yang sama juga berlaku untuk CSV, XML, atau bahkan result set basis data—cukup ubah string sumber dan sesuaikan token SmartMarker.

Selamat coding, semoga spreadsheet Anda selalu rapi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}