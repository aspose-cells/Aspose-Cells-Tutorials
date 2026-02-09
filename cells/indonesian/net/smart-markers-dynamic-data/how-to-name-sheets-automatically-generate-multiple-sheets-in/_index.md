---
category: general
date: 2026-02-09
description: Cara memberi nama sheet di C# dengan SmartMarker – pelajari cara menghasilkan
  banyak sheet dan mengotomatisasi penamaan sheet hanya dengan beberapa baris kode.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: id
og_description: Cara memberi nama sheet di C# menggunakan opsi SmartMarker. Panduan
  ini menunjukkan cara menghasilkan banyak sheet dan mengotomatisasi penamaan sheet
  dengan mudah.
og_title: Cara Menamai Lembar Kerja Secara Otomatis – Panduan Cepat C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cara Menamai Sheet Secara Otomatis – Menghasilkan Banyak Sheet di C#
url: /id/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menamai Sheet Secara Otomatis – Menghasilkan Banyak Sheet di C#

Pernah bertanya‑tanya **cara menamai sheet** dalam sebuah workbook Excel tanpa harus mengklik “Rename” secara manual setiap kali? Anda tidak sendirian. Dalam banyak skenario pelaporan, Anda berakhir dengan puluhan sheet detail yang memerlukan nama yang sistematis, dan melakukannya secara manual adalah mimpi buruk.  

Kabar baiknya, dengan beberapa baris C# Anda dapat **menghasilkan banyak sheet** dan **mengotomatiskan penamaan sheet** sehingga setiap sheet detail baru mengikuti pola yang dapat diprediksi. Pada tutorial ini kami akan membahas solusi lengkap, menjelaskan mengapa setiap bagian penting, dan memberikan contoh kode siap‑jalankan.

## Apa yang Dibahas dalam Panduan Ini

* Menyiapkan workbook yang berisi SmartMarkers.  
* Mengonfigurasi `SmartMarkerOptions` untuk mengontrol nama dasar sheet yang dihasilkan.  
* Menjalankan `ProcessSmartMarkers` sehingga perpustakaan membuat `Detail`, `Detail_1`, `Detail_2`, … secara otomatis.  
* Tips menangani kasus tepi seperti nama sheet yang sudah ada atau konvensi penamaan khusus.  
* Contoh lengkap yang dapat Anda tempel ke Visual Studio dan langsung melihat hasilnya.

Tidak diperlukan pengalaman sebelumnya dengan Aspose.Cells—hanya setup C# dasar dan IDE pilihan Anda.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6.0 atau yang lebih baru | Fitur bahasa modern dan kompatibilitas pustaka |
| Aspose.Cells untuk .NET (paket NuGet) | Menyediakan pemrosesan `SmartMarker` dan pembuatan sheet |
| Proyek console kosong (atau aplikasi .NET apa pun) | Memberikan tempat untuk mengeksekusi kode |

Pasang pustaka dengan:

```bash
dotnet add package Aspose.Cells
```

Setelah dasar‑dasarnya selesai, mari masuk ke implementasi sebenarnya.

## Langkah 1: Buat Workbook dengan SmartMarkers

Pertama kita membutuhkan workbook yang berisi placeholder SmartMarker. Anggap SmartMarker sebagai tag templat yang memberi tahu engine di mana menyuntikkan data dan, dalam kasus kita, kapan membuat sheet baru.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Pro tip:** Jaga agar sheet templat tetap ringan. Hanya baris yang perlu diduplikasi yang harus berisi SmartMarkers; sisanya tetap statis.

## Langkah 2: Konfigurasi Opsi SmartMarker – Inti Penamaan Sheet

Sekarang saatnya sihir. Dengan mengatur `DetailSheetNewName` kita memberi tahu engine nama dasar apa yang akan digunakan untuk setiap sheet yang dihasilkan. Perpustakaan akan menambahkan “_1”, “_2”, dll., setiap kali nama dasar sudah ada.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Jika Anda memerlukan konvensi berbeda (misalnya “Report_2023”), cukup ubah string‑nya. Engine menangani benturan secara otomatis, itulah mengapa pendekatan ini **mengotomatiskan penamaan sheet** tanpa kode tambahan.

## Langkah 3: Proses SmartMarkers dan Hasilkan Sheet

Dengan workbook, data, dan opsi yang siap, satu pemanggilan metode melakukan semua pekerjaan berat.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Hasil yang Diharapkan

Saat Anda membuka *GeneratedSheets.xlsx* Anda akan melihat:

| Nama Sheet | Konten |
|------------|--------|
| Template   | Tata letak marker asli (disimpan untuk referensi) |
| Detail     | Set baris pertama (Apple, Banana, Cherry) |
| Detail_1   | Salinan kedua – data identik (berguna saat Anda memiliki beberapa koleksi) |
| Detail_2   | …dan seterusnya, tergantung berapa banyak grup SmartMarker yang berbeda |

Pola penamaan (`Detail`, `Detail_1`, `Detail_2`) memperlihatkan **cara menamai sheet** secara programatis sekaligus **menghasilkan banyak sheet** sesuai kebutuhan.

## Kasus Tepi & Variasi

### 1. Nama Sheet yang Sudah Ada

Jika workbook Anda sudah memiliki sheet bernama “Detail”, engine akan memulai dengan “Detail_1”. Ini mencegah penimpaan yang tidak disengaja.

### 2. Format Inkrementasi Kustom

Ingin “Detail‑A”, “Detail‑B” alih‑alih sufiks numerik? Anda dapat memproses nama setelah `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Beberapa Grup SmartMarker

Jika workbook Anda berisi lebih dari satu grup SmartMarker (misalnya `{{invoice}}` dan `{{detail}}`), setiap grup akan menghasilkan set sheet masing‑masing berdasarkan `DetailSheetNewName` yang sama. Untuk memberi setiap grup prefiks yang berbeda, buat instance `SmartMarkerOptions` terpisah dan panggil `ProcessSmartMarkers` untuk setiap koleksi.

## Tips Praktis dari Lapangan

* **Pro tip:** Matikan `AllowDuplicateNames` di `WorkbookSettings` jika Anda ingin perpustakaan melemparkan pengecualian alih‑alih menamakan ulang sheet secara diam‑diam. Ini membantu menangkap bug logika penamaan lebih awal.  
* **Waspadai:** Nama dasar yang sangat panjang. Excel membatasi nama sheet hingga 31 karakter; perpustakaan memotong secara otomatis, tetapi Anda mungkin berakhir dengan nama yang ambigu.  
* **Catatan performa:** Menghasilkan ratusan sheet dapat mengonsumsi memori. Buang workbook (`wb.Dispose()`) sesegera mungkin jika Anda menjalankannya dalam layanan yang hidup lama.

## Gambaran Visual

![diagram cara menamai sheet](image.png "Diagram yang menunjukkan alur dari template SmartMarker ke sheet yang dihasilkan – cara menamai sheet")

*Alt text mencakup kata kunci utama untuk memenuhi SEO.*

## Kode Sumber Lengkap (Siap Salin‑Tempel)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Jalankan program, buka file yang dihasilkan, dan Anda akan melihat sheet secara otomatis dinamai sesuai pola yang telah kita definisikan.

## Kesimpulan

Anda kini tahu **cara menamai sheet** dalam workbook C#, **cara menghasilkan banyak sheet** dengan SmartMarker, dan **cara mengotomatiskan penamaan sheet** sehingga tidak pernah lagi harus mengganti nama secara manual. Pendekatan ini dapat diskalakan dari beberapa halaman detail hingga ratusan, dan pola yang sama bekerja untuk koleksi apa pun yang Anda berikan ke `ProcessSmartMarkers`.

Apa selanjutnya? Coba ganti sumber data dengan kueri basis data, bereksperimen dengan format sufiks kustom, atau rangkaikan beberapa grup SmartMarker untuk mesin pelaporan lengkap. Langit adalah batasnya ketika Anda membiarkan perpustakaan menangani pekerjaan penamaan yang berulang.

Jika panduan ini membantu, beri bintang di GitHub, bagikan kepada rekan tim, atau tinggalkan komentar di bawah dengan trik penamaan Anda sendiri. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}