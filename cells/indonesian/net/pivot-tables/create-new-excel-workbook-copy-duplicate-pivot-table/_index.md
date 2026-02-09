---
category: general
date: 2026-02-09
description: Buat buku kerja Excel baru dan pelajari cara menyalin tabel pivot dengan
  mudah. Panduan ini menunjukkan cara menggandakan tabel pivot dan menyimpan buku
  kerja sebagai yang baru.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: id
og_description: Buat buku kerja Excel baru di C# dan salin tabel pivot secara instan.
  Pelajari cara menduplikasi tabel pivot dan menyimpan buku kerja sebagai yang baru
  dengan contoh kode lengkap.
og_title: Buat Buku Kerja Excel Baru – Salinan Pivot Langkah demi Langkah
tags:
- excel
- csharp
- aspose.cells
- automation
title: Buat Buku Kerja Excel Baru – Salin & Gandakan Tabel Pivot
url: /id/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel Baru – Salin & Gandakan Tabel Pivot

Pernah membutuhkan **create new Excel workbook** yang membawa tabel pivot kompleks dari file yang ada? Anda bukan satu-satunya—banyak pengembang mengalami kendala ini saat mengotomatiskan pipeline pelaporan. Kabar baiknya, dengan beberapa baris C# dan perpustakaan Aspose.Cells Anda dapat **how to copy pivot** dengan cepat, **duplicate pivot table**, dan **save workbook as new** tanpa membuka Excel secara manual.

Dalam panduan ini kami akan membahas seluruh proses, mulai dari memuat workbook sumber hingga menyimpan versi yang digandakan. Pada akhir Anda akan memiliki potongan kode siap‑jalankan yang dapat Anda sisipkan ke proyek .NET mana pun. Tanpa basa‑basi, hanya solusi praktis yang dapat Anda uji hari ini.

## Apa yang Dibahas dalam Tutorial Ini

* **Prerequisites** – .NET 6+ (atau .NET Framework 4.6+), Visual Studio, dan paket NuGet Aspose.Cells untuk .NET.
* Kode langkah‑demi‑langkah yang **creates new Excel workbook**, menyalin pivot, dan menulis hasilnya ke disk.
* Penjelasan tentang **why** setiap baris penting, bukan hanya **what** yang dilakukannya.
* Tips untuk menangani kasus tepi seperti lembar kerja tersembunyi atau rentang data besar.
* Sekilas tentang **how to copy worksheet** jika Anda pernah membutuhkan seluruh lembar alih‑alih hanya pivot.

Siap? Mari kita mulai.

![ilustrasi membuat workbook excel baru](image.png "Diagram yang menunjukkan workbook sumber, salinan pivot, dan workbook tujuan")

## Langkah 1: Siapkan Proyek dan Instal Aspose.Cells

Sebelum kita dapat **create new Excel workbook**, kita memerlukan proyek yang merujuk ke perpustakaan yang tepat.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Mengapa ini penting:* Aspose.Cells bekerja sepenuhnya di memori, sehingga Anda tidak pernah perlu meluncurkan Excel di server. Ia juga mempertahankan informasi cache pivot, yang penting untuk **duplicate pivot table** yang sesungguhnya.

> **Pro tip:** Jika Anda menargetkan .NET Core, pastikan identifier runtime (RID) proyek Anda cocok dengan platform tempat Anda akan menyebarkan; jika tidak, Anda mungkin akan mengalami kesalahan pemuatan pustaka native.

## Langkah 2: Muat Workbook Sumber yang Menyimpan Pivot

Sekarang kami akan **how to copy pivot** dari file yang ada. Workbook sumber dapat berada di mana saja di disk, sebuah stream, atau bahkan array byte.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Mengapa kami memilih rentang:* Tabel pivot berada di dalam rentang sel biasa, tetapi juga memiliki data cache tersembunyi yang terlampir pada lembar. Dengan menyalin rentang **including the pivot**, Aspose.Cells memastikan cache ikut terbawa, memberi Anda **duplicate pivot table** yang berfungsi di file tujuan.

## Langkah 3: Buat Workbook Excel Baru untuk Menerima Data yang Disalin

Di sinilah kami benar‑benar **create new Excel workbook** yang akan menampung pivot yang digandakan.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Mengapa workbook baru?** Memulai dari awal yang bersih menjamin tidak ada format sisa atau objek tersembunyi yang mengganggu pivot yang disalin. Ini juga membuat file hasil lebih kecil, yang berguna untuk lampiran email otomatis.

## Langkah 4: Salin Rentang Pivot ke Workbook Baru

Sekarang kami melakukan operasi **how to copy pivot** yang sebenarnya.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Baris tunggal itu melakukan pekerjaan berat:

* Nilai sel, formula, dan format dipindahkan.
* Cache pivot digandakan, sehingga pivot baru tetap berfungsi penuh.
* Referensi relatif di dalam pivot menyesuaikan secara otomatis ke lokasi baru.

### Menangani Kasus Tepi

* **Hidden worksheets:** Jika lembar sumber tersembunyi, pivot tetap dapat disalin dengan baik, tetapi Anda mungkin ingin menampilkan lembar tujuan untuk visibilitas pengguna:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Large data sets:** Untuk rentang yang lebih besar dari beberapa ribu baris, pertimbangkan menggunakan `CopyTo` dengan `CopyOptions` untuk melakukan streaming operasi dan mengurangi tekanan memori.

## Langkah 5: Simpan Workbook Tujuan sebagai File Baru

Akhirnya, kami **save workbook as new** dan memverifikasi hasilnya.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Jika Anda membuka `copied.xlsx` Anda akan melihat replika persis dari pivot asli, siap untuk manipulasi atau distribusi lebih lanjut.

### Opsional: Cara Menyalin Worksheet Alih‑alih Hanya Pivot

Kadang‑kadang Anda menginginkan seluruh lembar, bukan hanya pivot. API yang sama membuatnya sangat mudah:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Ini menjawab pertanyaan **how to copy worksheet** dan dapat berguna ketika Anda perlu mempertahankan pengaturan tingkat lembar tambahan.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut aplikasi konsol mandiri yang dapat Anda kompilasi dan jalankan:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Output yang diharapkan:** Konsol mencetak pesan sukses, dan `copied.xlsx` muncul di `C:\Reports` dengan pivot yang berfungsi identik dengan yang ada di `source.xlsx`.

## Pertanyaan Umum & Jebakan

* **Will formulas inside the pivot break?** Tidak—karena cache pivot terbawa bersama rentang, semua bidang terhitung tetap utuh.
* **What if the source pivot uses external data connections?** Koneksi tersebut *tidak* disalin. Anda perlu membuatnya kembali di workbook tujuan atau mengubah pivot menjadi tabel statis terlebih dahulu.
* **Can I copy multiple pivots at once?** Tentu—cukup definisikan rentang yang lebih besar yang mencakup semua pivot, atau lakukan loop melalui setiap objek `PivotTable` di `sourceSheet.PivotTables` dan salin satu per satu.
* **Do I need to dispose of the `Workbook` objects?** Mereka mengimplementasikan `IDisposable`, jadi membungkusnya dalam pernyataan `using` adalah kebiasaan yang baik, terutama pada layanan dengan throughput tinggi.

## Kesimpulan

Anda sekarang tahu **how to create new Excel workbook**, menyalin pivot, **duplicate pivot table**, dan **save workbook as new** menggunakan C# dan Aspose.Cells. Langkah‑langkahnya sederhana: muat, buat, salin, dan simpan. Dengan potongan kode opsional **how to copy worksheet** Anda juga memiliki alternatif untuk duplikasi seluruh lembar.

Selanjutnya, Anda mungkin ingin menjelajahi:

* Menambahkan format khusus ke pivot yang digandakan.
* Menyegarkan cache pivot secara programatik setelah perubahan data.
* Mengekspor workbook ke PDF atau CSV untuk sistem hilir.

Cobalah, sesuaikan rentangnya, dan biarkan otomatisasi mengurangi pekerjaan berat dalam alur kerja pelaporan Anda. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}