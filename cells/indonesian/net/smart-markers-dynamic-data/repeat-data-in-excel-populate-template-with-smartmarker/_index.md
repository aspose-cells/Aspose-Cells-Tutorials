---
category: general
date: 2026-02-21
description: Ulang data di Excel dengan cepat menggunakan SmartMarker—pelajari cara
  mengisi templat Excel dan mengulang baris dengan mudah.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: id
og_description: Ulang data di Excel menggunakan SmartMarker. Pelajari cara mengisi
  templat Excel, mengulang baris, dan mengotomatisasi spreadsheet Anda.
og_title: Ulang data di Excel – Isi templat dengan SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Ulang data di Excel – Isi template dengan SmartMarker
url: /id/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengulang data di excel – Mengisi templat dengan SmartMarker

Pernah membutuhkan untuk **mengulang data di Excel** tetapi tidak yakin bagaimana menghindari penyalinan‑tempel manual? Anda tidak sendirian. Dalam banyak skenario pelaporan Anda memiliki daftar item yang harus berkembang menjadi baris secara otomatis, dan melakukannya secara manual adalah resep untuk kesalahan.

Begini—menggunakan **SmartMarkerProcessor** dari pustaka **GemBox.Spreadsheet** memungkinkan Anda **mengisi templat Excel** dengan satu baris C# dan membuat baris berulang untuk setiap item dalam koleksi Anda. Dalam panduan ini kami akan menelusuri langkah‑langkah tepat, menunjukkan kode lengkap, dan menjelaskan mengapa setiap bagian penting, sehingga Anda dapat dengan percaya diri mengulang baris di Excel tanpa berkeringat.

## Apa yang akan Anda pelajari

* Cara mendefinisikan struktur data yang menggerakkan operasi pengulangan.  
* Cara mengaitkan `SmartMarkerProcessor` ke workbook yang berisi lembar templat tersembunyi.  
* Bagaimana penanda `${Repeat:Item}` memperluas menjadi beberapa baris secara otomatis.  
* Tips untuk menangani kasus tepi seperti koleksi kosong atau pemformatan khusus.  

Pada akhir tutorial ini Anda akan dapat **mengisi excel dari data** dengan cara yang skalabel, mudah dipelihara, dan bekerja dengan proyek .NET apa pun.

---

## Prasyarat

* .NET 6.0 atau lebih baru (kode menggunakan fitur C# modern).  
* Paket NuGet **GemBox.Spreadsheet** (versi gratis bekerja hingga 150 baris).  
* File templat Excel dasar (`Template.xlsx`) dengan lembar tersembunyi bernama `HiddenTemplate`.  
* Familiaritas dengan objek C# dan LINQ membantu tetapi tidak wajib.

---

## Langkah 1 – Definisikan struktur data pengulangan

Pertama, Anda memerlukan sumber data yang dapat diiterasi oleh mesin SmartMarker. Dalam kebanyakan aplikasi dunia nyata ini akan berasal dari basis data, API, atau file CSV. Untuk kejelasan kita akan menggunakan tipe anonim dengan satu properti bernama `Item` yang menyimpan array string.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Mengapa ini penting:** Penanda `${Repeat:Item}` di dalam templat Excel mencari properti bernama `Item`. Jika Anda mengganti nama properti, perbarui penanda yang bersangkutan. Keterkaitan yang ketat ini memastikan templat tetap sinkron dengan kode Anda, memudahkan **mengisi templat excel** tanpa menebak nama kolom.

### Variasi umum

* **Objek kompleks:** Alih‑alih array string sederhana, Anda dapat menyediakan daftar objek (`new[] { new { Name = "A", Qty = 10 } }`). Penanda akan mengulang baris dan Anda dapat merujuk `${Item.Name}` serta `${Item.Qty}` di lembar.  
* **Koleksi kosong:** Jika `Item` kosong, SmartMarker cukup menghapus blok pengulangan, meninggalkan templat tidak berubah—ideal untuk bagian opsional.

---

## Langkah 2 – Buat SmartMarkerProcessor untuk lembar templat tersembunyi

Selanjutnya, muat workbook Anda dan buat instance `SmartMarkerProcessor`. Arahkan ke workbook yang berisi lembar templat tersembunyi; SmartMarker akan menyalin lembar tersebut ke lembar yang terlihat dan memperluas penanda pengulangan.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Tips pro:** Jika Anda memiliki beberapa templat dalam file yang sama, Anda dapat menentukan nama lembar sumber saat memanggil `processor.Process`. Ini membantu ketika Anda perlu **mengulang baris di excel** untuk bagian laporan yang berbeda.

### Penanganan kasus tepi

* **Lembar templat tidak ditemukan:** Bungkus pemuatan dalam try/catch dan catat kesalahan yang jelas—ini mencegah kegagalan diam ketika jalur file salah.  
* **Set data besar:** Untuk ribuan baris, pertimbangkan streaming output ke file (`processor.Save`) alih‑alih menyimpan semuanya di memori.

---

## Langkah 3 – Terapkan data dan perluas penanda `${Repeat:Item}`

Sekarang datang baris ajaib yang benar‑benar mengulang baris. Kirimkan objek yang Anda buat pada Langkah 1 ke `processor.Process`. SmartMarker akan menemukan setiap penanda `${Repeat:Item}`, menduplikasi baris untuk setiap elemen, dan mengganti placeholder dengan nilai sebenarnya.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Apa yang akan Anda lihat

Saat Anda membuka `Result.xlsx`, lembar templat tersembunyi telah disalin ke lembar baru yang terlihat (secara default bernama `Sheet1`). Baris yang berisi `${Repeat:Item}` kini muncul tiga kali, dengan sel menampilkan **A**, **B**, dan **C** masing‑masing.

| Item |
|------|
| A    |
| B    |
| C    |

Jika Anda menambahkan kolom lain seperti `${Item.Price}`, kolom tersebut akan terisi otomatis dari sumber data.

---

## Cara mengulang baris di Excel tanpa SmartMarker (perbandingan cepat)

| Pendekatan               | Kompleksitas Kode | Pemeliharaan | Kinerja |
|--------------------------|-------------------|--------------|---------|
| Salin‑tempel manual      | Tinggi            | Rendah       | Buruk   |
| Makro VBA                | Menengah          | Menengah     | Baik    |
| **SmartMarkerProcessor**| Rendah            | Tinggi       | Luar Biasa |

Seperti yang Anda lihat, menggunakan SmartMarker untuk **mengulang data di excel** memberi Anda pemisahan paling bersih antara desain templat dan logika bisnis. Ini juga bersifat bahasa‑agnostik—konsep serupa ada di pustaka Java, Python, dan JavaScript.

---

## Tips lanjutan & jebakan umum

### 1. Memformat baris yang diulang

SmartMarker menyalin seluruh baris—termasuk gaya sel, batas, dan pemformatan bersyarat. Jika Anda memerlukan gaya berbeda untuk baris pertama atau terakhir, tambahkan penanda ekstra seperti `${If:Item.IsFirst}` dan gunakan rumus bersyarat di dalam Excel.

### 2. Menangani dataset besar

Saat bekerja dengan > 10 000 baris, nonaktifkan perhitungan otomatis Excel sebelum memproses:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Aktifkan kembali setelah menyimpan untuk menjaga kinerja tetap cepat.

### 3. Mengisi Excel dari data di basis data nyata

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Kemudian gunakan `${Repeat:Order}` di templat untuk menampilkan setiap pesanan. Pola ini menunjukkan betapa mudahnya **mengisi excel dari data** langsung dari Entity Framework.

### 4. Menggunakan beberapa blok pengulangan

Anda dapat memiliki beberapa penanda `${Repeat:...}` pada lembar yang sama atau pada lembar berbeda. SmartMarker memprosesnya secara berurutan, sehingga urutan hanya penting bila satu blok bergantung pada output blok lain.

---

## Contoh lengkap yang dapat dijalankan

Berikut adalah aplikasi konsol mandiri yang dapat Anda tempel ke Visual Studio dan jalankan langsung. Ia mendemonstrasikan ketiga langkah serta penyimpanan file.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Output yang diharapkan:** `Result.xlsx` berisi lembar di mana baris dengan `${Repeat:Item}` muncul tiga kali, menampilkan A, B, dan C. Tidak diperlukan penyesuaian manual.

---

## Kesimpulan

Anda kini tahu cara **mengulang data di excel** secara efisien dengan memanfaatkan SmartMarkerProcessor. Dengan mendefinisikan objek data sederhana, memuat workbook templat, dan memanggil `Process`, Anda dapat **mengisi templat excel**, **mengulang baris di excel**, dan secara umum **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}