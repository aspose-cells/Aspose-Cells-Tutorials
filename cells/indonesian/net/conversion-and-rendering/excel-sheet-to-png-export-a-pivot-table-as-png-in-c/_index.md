---
category: general
date: 2026-03-18
description: Tutorial mengonversi lembar Excel ke PNG yang menunjukkan cara mengekspor
  pivot, mengatur area cetak pivot, dan mengekspor gambar rentang Excel menggunakan
  Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: id
og_description: Tutorial mengubah lembar Excel ke PNG yang memandu Anda cara mengekspor
  tabel pivot, mengatur area cetak pivot, dan mengekspor gambar rentang Excel dengan
  C#.
og_title: Lembar Excel ke PNG – Panduan Lengkap Mengekspor Tabel Pivot
tags:
- Aspose.Cells
- C#
- Excel automation
title: Lembar Excel ke PNG – Ekspor Pivot Table sebagai PNG dalam C#
url: /id/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Ekspor Pivot Table sebagai PNG di C#

Pernah perlu mengubah **excel sheet to png** tetapi tidak yakin cara menangkap hanya pivot table? Anda tidak sendirian. Dalam banyak pipeline pelaporan visual pivot adalah bintang, dan mengekspornya sebagai PNG memungkinkan Anda menyematkannya dalam email, dasbor, atau dokumentasi tanpa harus mengambil seluruh workbook.

Dalam panduan ini kami akan menunjukkan **cara mengekspor pivot**, **menetapkan print area pivot**, dan akhirnya **mengekspor excel range image** sehingga Anda mendapatkan file **export worksheet to image** yang bersih. Tanpa tautan misterius ke dokumen eksternal—hanya potongan kode lengkap yang dapat dijalankan dan penjelasan di balik setiap baris.

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (paket NuGet `Aspose.Cells` – versi 23.12 atau lebih baru).  
- Lingkungan pengembangan .NET (Visual Studio, Rider, atau `dotnet` CLI).  
- File Excel (`input.xlsx`) yang berisi setidaknya satu pivot table.

Itu saja. Jika Anda sudah memiliki semua itu, mari kita mulai.

## Langkah 1 – Muat Workbook dan Ambil Worksheet Pertama

Sebelum kita dapat menyentuh pivot, kita perlu workbook berada di memori.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Mengapa ini penting:* Memuat file memberi kami akses ke semua objek (tabel, grafik, pivot). Menggunakan worksheet pertama adalah default sederhana; Anda dapat mengganti `0` dengan indeks atau nama sheet yang sebenarnya jika diperlukan.

## Langkah 2 – Dapatkan Rentang Pivot Table

Pivot table berada di dalam blok sel. Kita memerlukan blok itu agar dapat memberi tahu Excel apa yang harus dicetak.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Mengapa kita melakukan ini:* `PivotTableRange` memberi tahu kami baris dan kolom awal serta akhir yang tepat. Tanpa ini, ekspor akan mencakup seluruh sheet, yang mengalahkan tujuan **set print area pivot**.

## Langkah 3 – Tentukan Print Area Agar Hanya Pivot yang Dihasilkan

Mesin pencetakan Excel menghormati properti `PrintArea`. Dengan mempersempitnya ke pivot, kita menghindari data sampingan atau sel kosong.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Tips pro:* Jika Anda memiliki beberapa pivot pada sheet yang sama, Anda dapat menggabungkan rentangnya menggunakan daftar dipisahkan koma (`"0,0:10,5,12,0:22,5"`). Itu adalah teknik **export excel range image** untuk beberapa blok.

## Langkah 4 – Siapkan Opsi Ekspor Gambar (Format PNG)

Aspose.Cells memungkinkan Anda menyesuaikan output secara detail. PNG bersifat lossless, sempurna untuk visual pivot yang tajam.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Mengapa PNG?* Tidak seperti JPEG, PNG mempertahankan ketajaman teks dan latar belakang transparan, menjadikannya pilihan utama untuk skenario **excel sheet to png**.

## Langkah 5 – Ekspor Worksheet (Area Pivot) ke File PNG

Sekarang keajaiban terjadi—render area print yang telah ditentukan ke gambar.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Apa yang akan Anda lihat:* File `pivot.png` yang berisi hanya pivot table, tanpa baris atau kolom tambahan. Buka di penampil gambar apa pun dan Anda akan memiliki visual siap dibagikan.

---

## Pertanyaan yang Sering Diajukan & Kasus Tepi

### Bagaimana jika workbook memiliki **multiple pivot tables**?

Ambil `PivotTableRange` masing‑masing pivot, gabungkan rentangnya, dan tetapkan string gabungan ke `PrintArea`. Contoh:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Bisakah saya mengekspor ke **other image formats**?

Tentu saja. Ubah `imgOptions.ImageFormat = ImageFormat.Jpeg;` (atau `Bmp`, `Gif`, `Tiff`). Ingat bahwa JPEG memperkenalkan artefak kompresi—biasanya tidak ideal untuk pivot yang banyak teks.

### Bagaimana cara menangani **large pivots** yang meluas ke banyak halaman?

Set `imgOptions.OnePagePerSheet = false;` untuk mengizinkan rendering multi‑halaman, lalu iterasi melalui halaman:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### Bagaimana dengan **hidden rows/columns**?

Aspose menghormati pengaturan visibilitas worksheet. Jika Anda perlu mengabaikan elemen tersembunyi, sementara waktu tampilkan mereka sebelum mengekspor atau sesuaikan `PrintArea` secara manual.

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Jalankan program, dan Anda akan menemukan `pivot.png` tepat di lokasi yang Anda tentukan. Buka file tersebut—Anda akan melihat rendering tajam dari hanya pivot table, tidak ada yang lain.

---

## Kesimpulan

Anda kini memiliki **solusi lengkap end‑to‑end** untuk mengubah **excel sheet to png** yang fokus secara eksklusif pada pivot table. Dengan **menetapkan print area pivot**, mengonfigurasi **image export options**, dan menggunakan metode `ToImage` dari Aspose.Cells, Anda dapat mengotomatisasi pembuatan laporan, menyematkan visual di halaman web, atau sekadar mengarsipkan snapshot analitik.

Apa selanjutnya? Coba ganti PNG dengan PDF resolusi tinggi (`ImageFormat.Pdf`), bereksperimen dengan beberapa pivot pada satu sheet, atau gabungkan pendekatan ini dengan ekspor grafik untuk pipeline ekspor dashboard lengkap.

Punya trik yang ingin dibagikan? Tinggalkan komentar, atau ikuti tutorial berikutnya di mana kami akan mengeksplor **export worksheet to image** untuk snapshot seluruh sheet, termasuk grafik dan pemformatan bersyarat. Selamat coding!  

<img src="pivot.png" alt="contoh excel sheet to png dari ekspor pivot table export">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}