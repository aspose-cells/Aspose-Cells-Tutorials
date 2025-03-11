---
title: Menyalin Lembar Kerja dari Satu Buku Kerja ke Buku Kerja Lain menggunakan Aspose.Cells
linktitle: Menyalin Lembar Kerja dari Satu Buku Kerja ke Buku Kerja Lain menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyalin lembar kerja antar-buku kerja menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah ini menyediakan prasyarat, contoh kode, dan Tanya Jawab Umum.
weight: 13
url: /id/net/worksheet-value-operations/copy-worksheet-between-workbooks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyalin Lembar Kerja dari Satu Buku Kerja ke Buku Kerja Lain menggunakan Aspose.Cells

## Perkenalan
Perlu cara untuk mentransfer data secara efisien dari satu buku kerja Excel ke buku kerja lain di aplikasi .NET Anda? Menyalin lembar kerja dari satu buku kerja ke buku kerja lain bisa sangat berguna, baik saat Anda mengelola laporan, membuat templat, atau mengatur data dengan cepat. Untungnya, dengan Aspose.Cells untuk .NET, proses ini mudah dan canggih. Dalam tutorial ini, kita akan menjelajahi cara menyalin lembar kerja dari satu buku kerja ke buku kerja lain dengan mudah, sehingga Anda memiliki kendali penuh atas pengelolaan data.
Dalam artikel ini, kami akan membahas semua hal yang perlu Anda ketahui untuk memulai. Mulai dari menyiapkan Aspose.Cells untuk .NET di proyek Anda hingga panduan langkah demi langkah yang komprehensif, Anda akan memperoleh keterampilan untuk mengimplementasikan fitur ini dengan lancar.
## Prasyarat
Sebelum memulai, mari pastikan Anda telah menyiapkan semua alat yang diperlukan:
1.  Pustaka Aspose.Cells untuk .NET: Pustaka ini penting untuk bekerja dengan file Excel di .NET. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
2. Visual Studio: Kami akan menggunakan Visual Studio (atau IDE serupa) untuk menulis dan menjalankan kode .NET.
3.  Lisensi Aspose: Jika Anda ingin menghindari batasan evaluasi, pertimbangkan[mengajukan uji coba gratis](https://releases.aspose.com/) atau sebuah[lisensi sementara](https://purchase.aspose.com/temporary-license/).
## Paket Impor
Untuk memulai, impor namespace yang diperlukan ke dalam proyek Anda:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ruang nama ini akan menyediakan akses ke kelas-kelas yang dibutuhkan untuk membuat, mengedit, dan memanipulasi buku kerja dan lembar kerja Excel.
Dalam panduan ini, kami akan menguraikan setiap bagian dari proses menjadi langkah-langkah yang jelas dan mudah dikelola. Mari kita bahas setiap langkahnya!
## Langkah 1: Tetapkan Jalur Direktori
Sebelum membuat dan menyimpan file, tentukan direktori tempat Anda akan menyimpan buku kerja. Ini akan memudahkan akses file nanti.
```csharp
// Tetapkan jalur ke direktori dokumen Anda.
string dataDir = "Your Document Directory";
```
 Itu`dataDir` variabel menyimpan jalur ke direktori. Pastikan untuk mengganti`"Your Document Directory"` dengan jalur direktori Anda yang sebenarnya.
## Langkah 2: Buat Buku Kerja dan Lembar Kerja Pertama
Sekarang, mari membuat buku kerja baru dengan satu lembar kerja dan menambahkan beberapa data ke dalamnya.
```csharp
// Buat Buku Kerja baru.
Workbook excelWorkbook0 = new Workbook();
// Akses lembar kerja pertama dalam buku kerja.
Worksheet ws0 = excelWorkbook0.Worksheets[0];
```
 Di sini, kita membuat objek buku kerja`excelWorkbook0`dan mengambil lembar kerja pertama`ws0` untuk manipulasi data.
## Langkah 3: Tambahkan Data Header ke Lembar Kerja
Mari kita isi lembar kerja pertama dengan baris tajuk. Data ini akan berfungsi sebagai contoh untuk menunjukkan proses penyalinan.
```csharp
// Mengisi baris header (A1:A4).
for (int i = 0; i < 5; i++)
{
    ws0.Cells[i, 0].PutValue($"Header Row {i}");
}
```
Dengan menggunakan loop, kita mengisi lima baris pertama di kolom A dengan label header. Ini memperjelas di mana setiap bagian baru dimulai di lembar kerja.
## Langkah 4: Mengisi Baris Data Detail
Selanjutnya, mari tambahkan beberapa data terperinci untuk memberikan konteks pada lembar kerja kita. Ini sangat berguna untuk simulasi laporan atau lembar analisis data.
```csharp
// Isi baris detail (A5:A999).
for (int i = 5; i < 1000; i++)
{
    ws0.Cells[i, 0].PutValue($"Detail Row {i}");
}
```
Loop ini mengisi baris dari A5 hingga A999 dengan pesan sederhana, meniru konten terperinci yang umum ditemukan dalam lembar kerja.
## Langkah 5: Konfigurasikan Pengaturan Halaman untuk Pencetakan
Aspose.Cells memungkinkan kita untuk menentukan pengaturan cetak untuk lembar kerja. Di sini, kita akan mengatur lima baris teratas untuk diulang pada setiap halaman yang dicetak, yang sangat berguna untuk laporan.
```csharp
//Konfigurasikan pengaturan halaman untuk mengulang baris tajuk pada setiap halaman.
PageSetup pagesetup = ws0.PageSetup;
pagesetup.PrintTitleRows = "$1:$5";
```
 Dengan pengaturan`PrintTitleRows` ke`$1:$5`, kami memastikan bahwa lima baris pertama (header kami) akan dicetak pada setiap halaman. Fitur ini ideal untuk menjaga konteks saat mencetak kumpulan data besar.
## Langkah 6: Buat Buku Kerja Kedua
Sekarang, mari buat buku kerja kedua tempat kita akan menempelkan lembar kerja yang disalin. Buku kerja ini akan berfungsi sebagai tujuan pemindahan lembar kerja.
```csharp
// Buat Buku Kerja lainnya.
Workbook excelWorkbook1 = new Workbook();
// Akses lembar kerja pertama dalam buku kerja.
Worksheet ws1 = excelWorkbook1.Worksheets[0];
```
 Di sini, kita inisialisasi`excelWorkbook1` sebagai buku kerja tujuan kita dan mengambil lembar kerja pertamanya,`ws1`, tempat kita akan menempelkan konten yang disalin.
## Langkah 7: Beri Nama Lembar Kerja Tujuan
Agar lebih mudah dikenali, mari kita ganti nama lembar kerja pertama di buku kerja kedua.
```csharp
// Ubah nama lembar kerja.
ws1.Name = "MySheet";
```
 Mengganti nama`ws1` ke`"MySheet"` memudahkan untuk membedakan lembar kerja dalam buku kerja baru, terutama saat menangani beberapa lembar.
## Langkah 8: Salin Data dari Lembar Kerja Sumber
Sekarang untuk acara utama: menyalin data lembar kerja dari buku kerja pertama ke yang kedua. Aspose.Cells menyederhanakan ini dengan`Copy` metode.
```csharp
// Salin data dari lembar kerja pertama di buku kerja pertama ke lembar kerja pertama di buku kerja kedua.
ws1.Copy(ws0);
```
 Itu`Copy` metode mentransfer semua konten dan format dari`ws0` ke`ws1`Metode ini efisien, menangani semua data dalam satu perintah.
## Langkah 9: Simpan Buku Kerja Akhir
Setelah semuanya diatur, simpan buku kerja tujuan ke direktori yang ditentukan.
```csharp
// Simpan buku kerja kedua.
excelWorkbook1.Save(dataDir + "CopyWorksheetFromWorkbookToOther_out.xls");
```
 Itu`Save` metode menyimpan`excelWorkbook1` sebagai file Excel di direktori yang Anda tentukan. Nama file di sini adalah`"CopyWorksheetFromWorkbookToOther_out.xls"`.
## Kesimpulan
Nah, itu dia! Menyalin lembar kerja dari satu buku kerja ke buku kerja lain menggunakan Aspose.Cells for .NET sangat mudah setelah Anda memahami langkah-langkahnya. Pendekatan ini ideal untuk menangani kumpulan data besar, membuat templat, dan mengotomatiskan pembuatan laporan dalam aplikasi .NET Anda.
Baik Anda seorang pemula atau pengembang berpengalaman, Aspose.Cells membuat bekerja dengan file Excel dalam .NET menjadi mudah dan efektif. Cobalah dengan uji coba gratis, dan jangan lupa untuk menjelajahi fitur-fitur canggih lainnya di Aspose.Cells.[dokumentasi](https://reference.aspose.com/cells/net/).
## Pertanyaan yang Sering Diajukan
### Bisakah saya menyalin beberapa lembar kerja sekaligus?  
Ya, Anda dapat mengulangi beberapa lembar kerja dalam buku kerja dan menyalinnya satu per satu ke buku kerja lain.
### Apakah Aspose.Cells mempertahankan format selama penyalinan?  
 Tentu saja!`Copy` metode memastikan bahwa semua pemformatan, gaya, dan data dipertahankan.
### Bagaimana cara mengakses sel tertentu dalam lembar kerja yang disalin?  
Anda dapat menggunakan`Cells` properti untuk mengakses dan memanipulasi sel tertentu dalam lembar kerja mana pun.
### Bagaimana jika saya hanya ingin menyalin nilai tanpa memformat?  
Anda dapat menggunakan kode khusus untuk menyalin nilai sel demi sel jika Anda lebih suka mengecualikan pemformatan.
### Bisakah saya menguji fitur ini tanpa lisensi?  
 Ya, Aspose menawarkan[uji coba gratis](https://releases.aspose.com/) untuk menjelajahi fitur-fiturnya tanpa batasan.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
