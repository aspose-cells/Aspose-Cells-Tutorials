---
title: Membuat Slicer untuk Tabel Pivot di Aspose.Cells .NET
linktitle: Membuat Slicer untuk Tabel Pivot di Aspose.Cells .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara membuat slicer untuk tabel pivot di Aspose.Cells .NET dengan panduan langkah demi langkah kami. Sempurnakan laporan Excel Anda.
weight: 12
url: /id/net/excel-slicers-management/create-slicer-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Slicer untuk Tabel Pivot di Aspose.Cells .NET

## Perkenalan
Dalam dunia yang digerakkan oleh data saat ini, tabel pivot sangat berharga untuk menganalisis dan meringkas kumpulan data besar. Namun, mengapa berhenti pada ringkasan saja jika Anda dapat membuat tabel pivot Anda lebih interaktif? Masuki dunia pemotong! Pemotong seperti remote control untuk laporan Excel Anda, yang memberi Anda kemampuan untuk memfilter data dengan cepat dan mudah. Dalam panduan ini, kami akan memandu Anda tentang cara membuat pemotong untuk tabel pivot menggunakan Aspose.Cells for .NET. Jadi, ambil secangkir kopi, duduk, dan mari kita mulai!
## Prasyarat
Sebelum Anda memulai, ada beberapa prasyarat yang perlu Anda ingat:
1.  Aspose.Cells untuk .NET: Pastikan Anda telah memasang Aspose.Cells di proyek Anda. Anda bisa mendapatkannya dari[halaman unduhan](https://releases.aspose.com/cells/net/).
2. Visual Studio atau IDE Lain: Anda memerlukan IDE tempat Anda dapat membuat dan menjalankan proyek .NET. Visual Studio merupakan pilihan yang populer.
3. Pengetahuan Dasar C#: Mengetahui sedikit C# akan membantu Anda menavigasi bagian pengkodean dengan lancar.
4. Contoh File Excel: Untuk tutorial ini, Anda akan memerlukan contoh file Excel yang berisi tabel pivot. Kami akan menggunakan file bernama`sampleCreateSlicerToPivotTable.xlsx`.
Sekarang setelah Anda mencentang semua kotak ini, mari impor paket yang diperlukan!
## Paket Impor
Untuk memanfaatkan Aspose.Cells secara efektif, Anda perlu mengimpor paket berikut dalam proyek Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Pastikan Anda menambahkan ini di bagian atas berkas kode Anda. Pernyataan impor ini memungkinkan Anda mengakses semua fungsi yang ditawarkan oleh pustaka Aspose.Cells.
Sekarang, mari kita bahas intinya. Kami akan uraikan menjadi beberapa langkah yang mudah diikuti, sehingga Anda dapat mengikutinya dengan mudah. 
## Langkah 1: Tentukan Direktori Sumber dan Output
Pertama-tama, kita perlu menentukan di mana file input dan output berada. Ini memastikan bahwa kode kita mengetahui di mana menemukan file Excel dan di mana menyimpan hasilnya.
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory"; // Berikan jalur direktori sumber Anda
// Direktori keluaran
string outputDir = "Your Document Directory"; // Berikan jalur direktori keluaran Anda
```
 Penjelasan: Pada langkah ini, Anda cukup mendeklarasikan variabel untuk direktori sumber dan keluaran. Ganti`"Your Document Directory"`dengan direktori sebenarnya tempat file Anda berada.
## Langkah 2: Muat Buku Kerja
Berikutnya, kita akan memuat buku kerja Excel yang berisi tabel pivot. 
```csharp
// Muat contoh file Excel yang berisi tabel pivot.
Workbook wb = new Workbook(sourceDir + "sampleCreateSlicerToPivotTable.xlsx");
```
 Penjelasan: Di sini, kita membuat sebuah instance dari`Workbook` kelas, yang meneruskan jalur ke berkas Excel. Baris kode ini memungkinkan kita untuk mengakses dan memanipulasi buku kerja.
## Langkah 3: Akses Lembar Kerja Pertama
Sekarang setelah buku kerja dimuat, kita perlu mengakses lembar kerja tempat tabel pivot berada.
```csharp
// Akses lembar kerja pertama.
Worksheet ws = wb.Worksheets[0];
```
Penjelasan: Lembar kerja di Aspose.Cells memiliki indeks nol, yang berarti lembar pertama memiliki indeks 0. Dengan baris ini, kita mendapatkan objek lembar kerja untuk manipulasi lebih lanjut.
## Langkah 4: Akses Tabel Pivot
Kita semakin dekat! Mari ambil tabel pivot yang ingin kita kaitkan dengan slicer.
```csharp
// Akses tabel pivot pertama di dalam lembar kerja.
Aspose.Cells.Pivot.PivotTable pt = ws.PivotTables[0];
```
Penjelasan: Mirip dengan lembar kerja, tabel pivot juga diindeks. Baris ini menarik tabel pivot pertama dari lembar kerja sehingga kita dapat menambahkan pemotong ke dalamnya.
## Langkah 5: Tambahkan Slicer
Sekarang tibalah bagian yang menarik—menambahkan slicer! Langkah ini mengikat slicer ke bidang dasar tabel pivot kita.
```csharp
// Tambahkan pemotong yang berkaitan dengan tabel pivot dengan bidang basis pertama di sel B22.
int idx = ws.Slicers.Add(pt, "B22", pt.BaseFields[0]);
```
 Penjelasan: Di sini, kita menambahkan slicer, menentukan posisi (sel B22) dan bidang dasar dari tabel pivot (yang pertama). Metode ini mengembalikan indeks, yang kita simpan di`idx` untuk referensi masa mendatang.
## Langkah 6: Akses Slicer yang Baru Ditambahkan
Setelah slicer dibuat, ada baiknya Anda memiliki referensi ke sana, terutama jika Anda ingin membuat modifikasi lebih lanjut nanti.
```csharp
// Akses pemotong yang baru ditambahkan dari koleksi pemotong.
Aspose.Cells.Slicers.Slicer slicer = ws.Slicers[idx];
```
Penjelasan: Dengan indeks pemotong yang baru dibuat, kita sekarang dapat mengaksesnya langsung dari koleksi pemotong lembar kerja.
## Langkah 7: Simpan Buku Kerja
Akhirnya, saatnya menyimpan kerja keras Anda! Anda dapat menyimpan buku kerja dalam berbagai format.
```csharp
// Simpan buku kerja dalam format keluaran XLSX.
wb.Save(outputDir + "outputCreateSlicerToPivotTable.xlsx", SaveFormat.Xlsx);
// Simpan buku kerja dalam format keluaran XLSB.
wb.Save(outputDir + "outputCreateSlicerToPivotTable.xlsb", SaveFormat.Xlsb);
```
Penjelasan: Pada langkah ini, kita menyimpan buku kerja dalam format XLSX dan XLSB. Ini memberi Anda pilihan tergantung pada kebutuhan Anda.
## Langkah 8: Jalankan Kode
Sebagai pemanis pada kue, mari kita beri tahu pengguna bahwa semuanya berhasil dijalankan!
```csharp
Console.WriteLine("CreateSlicerToPivotTable executed successfully.");
```
Penjelasan: Pesan konsol sederhana untuk meyakinkan pengguna bahwa semuanya telah diselesaikan tanpa kesalahan.
## Kesimpulan
Nah, itu dia! Anda telah berhasil membuat slicer untuk tabel pivot menggunakan Aspose.Cells for .NET. Fitur kecil ini dapat meningkatkan interaktivitas laporan Excel Anda secara signifikan, membuatnya mudah digunakan dan menarik secara visual.
Jika Anda telah mengikuti tutorial ini, Anda akan merasa membuat dan memanipulasi tabel pivot dengan slicer sekarang menjadi hal yang mudah. Apakah Anda menikmati tutorial ini? Saya harap tutorial ini memicu minat Anda untuk lebih mengeksplorasi kemampuan Aspose.Cells!
## Pertanyaan yang Sering Diajukan
### Apa itu slicer di Excel?
Slicer adalah filter visual yang memungkinkan pengguna untuk dengan cepat memfilter data dari tabel pivot.
### Bisakah saya menambahkan beberapa pemotong ke tabel pivot?
Ya, Anda dapat menambahkan pemotong sebanyak yang Anda perlukan ke tabel pivot untuk bidang yang berbeda.
### Apakah Aspose.Cells gratis untuk digunakan?
Aspose.Cells adalah pustaka berbayar, tetapi Anda dapat mencobanya secara gratis selama masa uji coba.
### Di mana saya dapat menemukan lebih banyak dokumentasi Aspose.Cells?
 Anda dapat memeriksa[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk lebih jelasnya.
### Apakah ada cara untuk mendapatkan dukungan untuk Aspose.Cells?
 Tentu saja! Anda dapat menghubungi kami untuk mendapatkan dukungan di[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
