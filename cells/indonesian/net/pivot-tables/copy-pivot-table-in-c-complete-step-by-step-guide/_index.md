---
category: general
date: 2026-03-25
description: Salin tabel pivot dengan C# menggunakan Aspose.Cells. Pelajari cara menyalin
  pivot, mengekspor file tabel pivot, dan mempertahankan data dalam hitungan menit.
draft: false
keywords:
- copy pivot table
- how to copy pivot
- export pivot table file
- Aspose.Cells pivot
- C# Excel automation
language: id
og_description: Salin tabel pivot di C# menggunakan Aspose.Cells. Panduan ini menunjukkan
  cara menyalin pivot, mengekspor file tabel pivot, dan menjaga semua pengaturan tetap
  utuh.
og_title: Salin Tabel Pivot di C# – Tutorial Pemrograman Lengkap
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: Menyalin Tabel Pivot di C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyalin Tabel Pivot di C# – Panduan Lengkap Langkah‑per‑Langkah

Pernahkah Anda perlu **menyalin tabel pivot** dari satu workbook ke workbook lain dan bertanya-tanya apakah logika pivot tetap setelah dipindahkan? Anda bukan satu-satunya. Dalam banyak pipeline pelaporan kami menghasilkan workbook master, lalu mengirimkan salinan ringan yang masih memungkinkan pengguna akhir memotong data. Kabar baik? Dengan beberapa baris C# dan Aspose.Cells Anda dapat melakukan hal itu—tanpa perlu mengutak‑atik manual.

Dalam tutorial ini kami akan membahas seluruh proses: memuat file sumber, memilih rentang yang berisi pivot, menempelkannya ke workbook baru sambil mempertahankan definisi pivot, dan akhirnya **ekspor file tabel pivot** untuk konsumsi downstream. Pada akhir Anda akan tahu *cara menyalin pivot* secara programatis dan memiliki contoh siap‑jalankan yang dapat Anda masukkan ke proyek Anda.

## Prasyarat

- .NET 6+ (atau .NET Framework 4.6+) terpasang  
- Paket NuGet Aspose.Cells untuk .NET (`Install-Package Aspose.Cells`)  
- File Excel sumber (`source.xlsx`) yang sudah berisi tabel pivot (ukuran apa saja)  
- Pengetahuan dasar C#; tidak memerlukan pemahaman mendalam tentang internal Excel  

Jika Anda kekurangan salah satu dari ini, cukup tambahkan paket NuGet dan buka Visual Studio—tidak ada yang lain.

## Apa yang Dilakukan Kode (Ikhtisar)

1. **Load** workbook yang menyimpan pivot asli.  
2. **Define** sebuah `Range` yang melingkupi seluruh pivot (termasuk cache-nya).  
3. **Create** workbook baru yang akan menjadi tujuan.  
4. **Paste** rentang dengan `CopyPivotTable = true` sehingga definisi pivot disalin, bukan hanya nilai.  
5. **Save** file tujuan, memberi Anda **ekspor file tabel pivot** yang dapat dibagikan.  

Itulah seluruh alur kerja dalam lima langkah rapi. Mari kita selami masing‑masing langkah.

## Langkah 1 – Muat Workbook Sumber yang Berisi Tabel Pivot

Pertama kita perlu memuat file sumber ke memori. Aspose.Cells membuat ini menjadi satu baris kode.

```csharp
using Aspose.Cells;

// Load the source workbook (replace the path with your actual file)
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet – adjust the index if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

*Mengapa ini penting:* Memuat workbook memberi kami akses ke cache pivot yang mendasarinya. Jika Anda hanya menyalin nilai sel, pivot akan kehilangan kemampuan slicer-nya. Dengan menjaga objek workbook tetap hidup, kami mempertahankan metadata pivot secara lengkap.

## Langkah 2 – Tentukan Rentang yang Mencakup Tabel Pivot

Pivot bukan hanya sekumpulan sel; ia juga memiliki data cache tersembunyi. Cara paling aman adalah memilih sebuah persegi panjang yang sepenuhnya mengelilingi area yang terlihat. Dalam kebanyakan kasus `A1:E20` berfungsi, tetapi Anda dapat menemukan batas tepat secara programatis menggunakan properti `PivotTable`.

```csharp
// Example range – adjust to match your pivot's size
Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

// (Optional) Dynamically get the used range of the pivot:
PivotTable pivot = sourceSheet.PivotTables[0];
int firstRow = pivot.Row - 1;      // include header row
int firstCol = pivot.Column - 1;   // include field list
int lastRow  = pivot.Row + pivot.RowCount;
int lastCol  = pivot.Column + pivot.ColumnCount;
Range dynamicRange = sourceSheet.Cells.CreateRange(firstRow, firstCol,
                                                    lastRow - firstRow + 1,
                                                    lastCol - firstCol + 1);
```

*Mengapa kami memilih rentang:* Metode `Paste` bekerja pada objek `Range`. Dengan menentukan area yang tepat, kami memastikan bahwa tata letak pivot dan cache-nya berpindah bersama.

## Langkah 3 – Buat Workbook Tujuan Baru

Sekarang kami membuat workbook kosong yang akan menerima pivot yang disalin. Tidak ada yang rumit, hanya kanvas bersih.

```csharp
// Initialize an empty workbook – it comes with one default worksheet
Workbook destinationWorkbook = new Workbook();
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

*Tip:* Jika Anda perlu mempertahankan worksheet yang ada (misalnya, template), Anda dapat menambahkan workbook baru sebagai klon dari file template alih‑alih menggunakan konstruktor kosong.

## Langkah 4 – Tempel Rentang Sambil Mempertahankan Tabel Pivot

Inilah inti dari operasi. Menetapkan `CopyPivotTable = true` memberi tahu Aspose.Cells untuk mentransfer definisi pivot, bukan hanya nilai yang ditampilkan.

```csharp
destinationSheet.Cells.Paste(
    sourceRange,
    new PasteOptions
    {
        PasteType = PasteType.All,      // copy everything: formulas, formats, etc.
        CopyPivotTable = true           // crucial – keeps the pivot functional
    });
```

*Apa yang terjadi di balik layar?* Aspose.Cells membuat ulang cache pivot di workbook tujuan, menghubungkan kembali sumber data pivot, dan mempertahankan slicer, filter, serta field terhitung. Hasilnya adalah pivot yang sepenuhnya interaktif—tepat seperti yang Anda harapkan jika Anda menyalin sheet secara manual di Excel.

## Langkah 5 – Simpan Workbook Hasil (Ekspor File Tabel Pivot)

Akhirnya kami menulis workbook tujuan ke disk. File yang Anda dapatkan adalah **ekspor file tabel pivot** Anda yang siap didistribusikan.

```csharp
destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");
```

Buka `copy-pivot.xlsx` di Excel, dan Anda akan melihat tabel pivot tetap utuh, siap untuk disegarkan atau dipotong.

## Contoh Kerja Lengkap (Semua Langkah Digabungkan)

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi console. Program ini mencakup penanganan error dan komentar untuk kejelasan.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load source workbook with the pivot table
                Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
                Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

                // 2️⃣ Define the range that fully encloses the pivot
                // Adjust "A1:E20" as needed, or use dynamic detection shown earlier
                Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

                // 3️⃣ Create a fresh destination workbook
                Workbook destinationWorkbook = new Workbook();
                Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

                // 4️⃣ Paste the range and keep the pivot definition
                destinationSheet.Cells.Paste(
                    sourceRange,
                    new PasteOptions
                    {
                        PasteType = PasteType.All,
                        CopyPivotTable = true
                    });

                // 5️⃣ Save the new file – this is your exported pivot table file
                destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

                Console.WriteLine("✅ Pivot table copied successfully! File saved as copy-pivot.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

**Hasil yang diharapkan:** Saat Anda membuka `copy-pivot.xlsx`, tabel pivot muncul persis seperti di `source.xlsx`. Anda dapat menyegarkannya, mengubah filter, atau bahkan menambahkan sumber data baru tanpa kehilangan fungsionalitas.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika workbook sumber memiliki banyak pivot?

Lakukan loop melalui `sourceSheet.PivotTables` dan ulangi proses copy‑paste untuk masing‑masing. Pastikan setiap rentang tujuan tidak tumpang tindih.

```csharp
int destRow = 0;
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Calculate a non‑overlapping destination range for each pivot
    Range src = sourceSheet.Cells.CreateRange(pt.Row, pt.Column,
                                              pt.RowCount + 5, pt.ColumnCount + 5);
    destinationSheet.Cells.Paste(src, new PasteOptions { PasteType = PasteType.All, CopyPivotTable = true });
    destRow += pt.RowCount + 10; // move down for the next pivot
}
```

### Apakah ini bekerja dengan sumber data eksternal (mis., SQL)?

Jika pivot asli mengambil data dari koneksi eksternal, string koneksi juga disalin. Namun, workbook tujuan harus memiliki akses ke sumber data yang sama. Anda mungkin perlu menyesuaikan kredensial atau menggunakan `WorkbookSettings` untuk mengizinkan koneksi eksternal.

### Bisakah saya menyalin hanya tata letak pivot (tanpa data)?

Setel `PasteOptions.PasteType = PasteType.Formulas` dan pertahankan `CopyPivotTable = true`. Ini menyalin struktur sambil membiarkan cache data kosong, memaksa penyegaran pada pembukaan pertama.

### Bagaimana dengan melindungi sheet?

Jika sheet sumber dilindungi, lepaskan proteksinya sebelum menyalin, atau berikan `Password` yang sesuai ke `Worksheet.Unprotect`. Setelah menempel, Anda dapat menerapkan kembali proteksi pada sheet tujuan.

## Tips Pro & Perangkap

- **Pro tip:** Selalu gunakan versi Aspose.Cells terbaru; rilis lama memiliki bug dimana `CopyPivotTable` mengabaikan slicer.  
- **Watch out for:** Cache pivot yang besar dapat membuat file tujuan menjadi lebih besar. Jika ukuran penting, pertimbangkan membersihkan field yang tidak terpakai sebelum menyalin.  
- **Performance tip:** Saat menyalin banyak worksheet, nonaktifkan sementara `WorkbookSettings.EnableThreadedCalculation` untuk mempercepat operasi.  
- **Naming clash:** Jika workbook tujuan sudah berisi pivot dengan nama yang sama, Aspose akan mengganti nama yang masuk (`PivotTable1_1`). Ganti nama secara manual jika Anda memerlukan identifier khusus.

## Ringkasan Visual

![Menyalin tabel pivot di C# – diagram yang menunjukkan workbook sumber → pemilihan rentang → tempel dengan preservasi pivot → file tujuan](copy-pivot-diagram.png "Ilustrasi alur kerja menyalin tabel pivot")

*Teks alternatif:* **Menyalin tabel pivot** diagram alur yang menggambarkan sumber, rentang, opsi tempel, dan file yang diekspor.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **menyalin tabel pivot** menggunakan C# dan Aspose.Cells: memuat sumber, memilih rentang yang tepat, mempertahankan definisi pivot saat menempel, dan akhirnya mengekspor hasil sebagai file mandiri. Potongan kode di atas siap produksi; cukup masukkan jalur Anda dan Anda siap.

Sekarang Anda tahu *cara menyalin pivot* secara programatis, Anda dapat mengotomatisasi distribusi laporan, membangun generator template, atau mengintegrasikan analitik Excel ke layanan .NET yang lebih besar. Selanjutnya Anda mungkin ingin mengeksplor **ekspor file tabel pivot** ke format lain (PDF, CSV) atau menyematkan workbook ke API web untuk analitik secara langsung.

Ada trik yang ingin Anda bagikan—mungkin menyalin pivot antar versi Excel yang berbeda atau menangani model PowerPivot? Tinggalkan komentar, dan mari teruskan diskusi. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}