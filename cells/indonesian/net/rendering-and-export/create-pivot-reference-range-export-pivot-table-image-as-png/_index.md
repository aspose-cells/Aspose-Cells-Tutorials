---
category: general
date: 2026-02-09
description: Buat rentang referensi pivot di C# dan ekspor gambar tabel pivot. Pelajari
  cara menyimpan rentang Excel sebagai png menggunakan Aspose.Cells – panduan cepat
  dan lengkap.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: id
og_description: Buat rentang referensi pivot di C# dan ekspor gambar tabel pivot ke
  PNG. Panduan lengkap langkah demi langkah untuk menyimpan rentang Excel sebagai
  PNG.
og_title: Buat Rentang Referensi Pivot – Ekspor Gambar Tabel Pivot sebagai PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Buat Rentang Referensi Pivot – Ekspor Gambar Tabel Pivot sebagai PNG
url: /id/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Rentang Referensi Pivot – Ekspor Gambar Tabel Pivot sebagai PNG

Perlu **membuat rentang referensi pivot** dalam workbook Excel menggunakan C#? Anda juga dapat **mengekspor gambar tabel pivot** dan **menyimpan rentang Excel sebagai png** dengan hanya beberapa baris kode. Menurut pengalaman saya, mengubah pivot yang aktif menjadi gambar statis adalah cara yang praktis untuk menyisipkan analitik ke dalam laporan, email, atau dasbor tanpa harus menyertakan seluruh workbook.

Dalam tutorial ini kita akan membahas semua yang perlu Anda ketahui: pustaka yang diperlukan, kode yang tepat, mengapa setiap pemanggilan penting, dan beberapa hal yang perlu diwaspadai. Pada akhir tutorial Anda akan dapat menghasilkan file PNG dari tabel pivot apa pun dengan percaya diri, serta memahami cara menyesuaikan pola ini untuk banyak lembar kerja atau format gambar khusus.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- **Aspose.Cells for .NET** (versi percobaan gratis sudah cukup untuk pengujian).  
- **.NET 6.0** atau yang lebih baru – API yang kami gunakan sepenuhnya kompatibel dengan .NET Standard 2.0+, sehingga kerangka kerja yang lebih lama juga dapat dikompilasi.  
- Proyek C# dasar (Console App, WinForms, atau ASP.NET – apa saja yang dapat merujuk paket NuGet).  

Jika Anda belum menginstal Aspose.Cells, jalankan:

```bash
dotnet add package Aspose.Cells
```

Itu saja – tidak ada COM interop, tidak ada Excel yang harus diinstal di server.

## Langkah 1: Buka Workbook dan Akses Worksheet Pertama

Hal pertama yang Anda lakukan adalah memuat file workbook dan mengambil worksheet yang berisi tabel pivot. Kami sengaja memilih **worksheet pertama** (`Worksheets[0]`) karena kebanyakan file demo menempatkan pivot di sana, tetapi Anda dapat mengganti indeks dengan nama jika lebih suka.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Mengapa ini penting:* `Worksheet` adalah titik masuk untuk setiap operasi berbasis rentang. Jika Anda menunjuk ke sheet yang salah, pemanggilan `PivotTables[0]` berikutnya akan melempar `IndexOutOfRangeException`.

## Langkah 2: Buat Rentang Referensi Pivot

Sekarang kami meminta tabel pivot itu sendiri untuk memberikan **rentang referensi**. Rentang ini mewakili sel‑sel tepat yang membentuk pivot – header, baris data, dan total. Metode `CreateReferenceRange()` melakukan pekerjaan berat secara internal, menangani sel yang digabung dan baris tersembunyi untuk Anda.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** Jika workbook Anda berisi beberapa pivot, iterasikan `worksheet.PivotTables` dan pilih yang Anda butuhkan berdasarkan properti `Name`‑nya.

## Langkah 3: Render Rentang Referensi menjadi Gambar

Aspose.Cells dapat merender sembarang `Range` menjadi gambar. Objek yang dikembalikan mendukung format raster (PNG, JPEG) dan vektor (SVG). Di sini kami meminta gambar raster default, yang merupakan objek yang kompatibel dengan `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Apa yang terjadi di balik layar?* API mengambil snapshot tata letak visual rentang, menghormati gaya sel, font, dan pemformatan bersyarat. Pada dasarnya ini sama dengan mengambil screenshot, tetapi secara programatis dan tanpa UI.

## Langkah 4: Simpan Gambar yang Dihasilkan ke File

Akhirnya, kami menyimpan gambar tersebut. Metode `Save` secara otomatis memilih PNG ketika Anda memberikan ekstensi “.png”. Anda juga dapat memberikan objek `SaveOptions` jika memerlukan kontrol DPI atau format lain.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Setelah baris ini dijalankan, buka `pivot.png` dan Anda akan melihat snapshot pixel‑perfect dari tabel pivot, siap disisipkan di mana saja.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program konsol mandiri yang dapat Anda salin‑tempel dan jalankan:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Output yang diharapkan:** sebuah file bernama `pivot.png` yang berada di `YOUR_DIRECTORY`. Buka dengan penampil gambar apa pun – Anda akan melihat tata letak persis dari pivot asli, termasuk judul kolom, baris data, dan total keseluruhan.

## Ekspor Gambar Tabel Pivot – Menyesuaikan Ukuran dan DPI

Kadang‑kadang gambar default terlalu kecil untuk slide presentasi. Anda dapat mengontrol resolusi dengan memberikan objek `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Mengapa mengatur DPI?* DPI yang lebih tinggi menghasilkan tepi yang lebih tajam, terutama ketika PNG diperbesar di PowerPoint atau PDF.

## Simpan Rentang Excel sebagai PNG – Menangani Banyak Worksheet

Jika Anda perlu mengekspor pivot dari beberapa sheet, lakukan loop melalui `Workbook.Worksheets` dan ulangi langkah‑langkahnya. Berikut cuplikan singkat:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Pola ini **mengekspor gambar tabel pivot** untuk setiap pivot di seluruh workbook, dan setiap file dinamai sesuai sheet dan pivotnya – sempurna untuk pemrosesan batch.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| `IndexOutOfRangeException` pada `PivotTables[0]` | Worksheet tidak memiliki tabel pivot. | Periksa `worksheet.PivotTables.Count` sebelum mengakses. |
| Gambar kosong | Pivot difilter sehingga semua baris tersembunyi. | Pastikan pivot memiliki data yang terlihat, atau panggil `pivot.RefreshData();` sebelum membuat rentang. |
| PNG beresolusi rendah | DPI default adalah 96. | Gunakan `ImageOrVectorSaveOptions.Resolution` seperti contoh di atas. |
| Kesalahan jalur file | Karakter tidak valid di `YOUR_DIRECTORY`. | Gunakan `Path.Combine` dan `Path.GetInvalidPathChars()` untuk membersihkan. |

## Verifikasi – Tes Cepat

Setelah menjalankan contoh lengkap:

1. Buka `pivot.png` di Windows Photo Viewer.  
2. Verifikasi bahwa judul kolom, baris data, dan baris total cocok dengan tampilan di Excel.  
3. Jika Anda melihat baris yang hilang, periksa kembali bahwa metode **RefreshData** pada pivot telah dipanggil sebelum `CreateReferenceRange()`.

## Bonus: Menyisipkan PNG ke Dokumen Word

Karena gambar sudah berupa PNG, Anda dapat langsung memasukkannya ke Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Sekarang Anda memiliki laporan Word yang berisi snapshot persis dari pivot – tanpa perlu menyalin‑tempel secara manual.

## Kesimpulan

Anda baru saja mempelajari cara **membuat rentang referensi pivot**, **mengekspor gambar tabel pivot**, dan **menyimpan rentang Excel sebagai png** menggunakan Aspose.Cells di C#. Poin penting yang dapat diingat:

- Gunakan `PivotTable.CreateReferenceRange()` untuk mengisolasi area visual pivot.  
- Konversi rentang tersebut menjadi gambar dengan `Range.ToImage()`.  
- Simpan gambar sebagai PNG, dengan opsi menyesuaikan DPI untuk kualitas cetak.  

Dari sini Anda dapat mengeksplorasi ekspor batch, format gambar lain (SVG, JPEG), atau bahkan menyisipkan PNG ke PDF atau dokumen Word. Langit adalah batasnya setelah Anda memiliki pivot yang ditangkap sebagai grafik statis.

Ada pertanyaan atau skenario rumit? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}