---
title: Kelompokkan Baris dan Kolom di Excel dengan Aspose.Cells
linktitle: Kelompokkan Baris dan Kolom di Excel dengan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengelompokkan baris dan kolom di Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah ini.
weight: 12
url: /id/net/row-and-column-management/grouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kelompokkan Baris dan Kolom di Excel dengan Aspose.Cells

## Perkenalan
Jika Anda bekerja dengan lembar Excel yang besar, Anda tahu betapa pentingnya menjaga semuanya terorganisasi dengan baik dan mudah digunakan. Pengelompokan baris dan kolom membantu Anda membuat bagian, membuat navigasi data jauh lebih lancar. Dengan Aspose.Cells untuk .NET, Anda dapat dengan mudah mengelompokkan baris dan kolom di Excel secara terprogram, memberi Anda kendali penuh atas tata letak file Anda.
Dalam tutorial ini, kami akan membahas semua hal yang perlu Anda ketahui untuk menyiapkan, mengelompokkan, dan menyembunyikan baris dan kolom dalam lembar Excel dengan Aspose.Cells for .NET. Pada akhirnya, Anda akan dapat memanipulasi file Excel seperti seorang profesional tanpa perlu membuka Excel itu sendiri. Siap untuk mencobanya?
## Prasyarat
Sebelum kita masuk ke kode, mari pastikan Anda telah menyiapkan dan menyiapkan semuanya:
1.  Pustaka Aspose.Cells untuk .NET: Anda memerlukan pustaka ini untuk bekerja dengan file Excel. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
2. Visual Studio: Tutorial ini menggunakan Visual Studio untuk contoh kode.
3. Pengetahuan Dasar C#: Keakraban dengan C# dan .NET akan sangat membantu.
4. Lisensi Aspose: Lisensi berbayar atau sementara diperlukan untuk menghindari batasan evaluasi. Dapatkan lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).
## Paket Impor
Untuk memulai, impor namespace Aspose.Cells yang diperlukan, bersama dengan pustaka .NET penting untuk penanganan file. 
```csharp
using System.IO;
using Aspose.Cells;
```
Mari kita uraikan setiap bagian kode, sehingga lebih mudah bagi Anda untuk mengikuti dan memahaminya.
## Langkah 1: Siapkan Direktori Data Anda
Pertama-tama, kita perlu menentukan jalur ke berkas Excel yang akan kita gunakan. Ini biasanya jalur lokal, tetapi bisa juga jalur pada jaringan.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Di sini, ganti`"Your Document Directory"` dengan jalur sebenarnya ke berkas Excel Anda. Pengaturan ini membantu kode Anda menemukan berkas yang dibutuhkan untuk bekerja.
## Langkah 2: Buat Aliran File untuk Mengakses File Excel
Aspose.Cells mengharuskan Anda untuk membuka berkas melalui aliran berkas. Aliran ini membaca dan memuat konten berkas untuk diproses.
```csharp
// Membuat aliran file yang berisi file Excel yang akan dibuka
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Kode di atas terbuka`book1.xls` dari direktori yang Anda tentukan. Jika berkas tersebut tidak ada, pastikan untuk membuatnya atau mengubah nama berkasnya.
## Langkah 3: Muat Buku Kerja dengan Aspose.Cells
Sekarang, mari kita inisialisasikan buku kerja melalui Aspose.Cells. Langkah ini memberi kita akses ke berkas Excel, yang memungkinkan manipulasi mudah.
```csharp
// Membuka file Excel melalui aliran file
Workbook workbook = new Workbook(fstream);
```
 Setelah baris ini,`workbook` Objek akan berisi semua data dan struktur dari berkas Excel Anda. Anggap saja seperti memuat seluruh lembar kerja ke dalam memori.
## Langkah 4: Akses Lembar Kerja yang Ingin Anda Ubah
Aspose.Cells menyimpan setiap lembar kerja dalam buku kerja sebagai objek terpisah. Di sini, kita memilih lembar kerja pertama.
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Jika Anda memerlukan lembar kerja tertentu, Anda dapat mengubah baris ini untuk mengaksesnya berdasarkan nama atau indeks.
## Langkah 5: Kelompokkan Baris di Lembar Kerja
Sekarang saatnya untuk bagian yang menyenangkan—mengelompokkan baris! Mari kelompokkan enam baris pertama dan sembunyikan.
```csharp
// Kelompokkan enam baris pertama (dari 0 hingga 5) dan buat mereka tersembunyi dengan meneruskan true
worksheet.Cells.GroupRows(0, 5, true);
```
Berikut ini fungsi masing-masing parameter:
- 0, 5: Indeks awal dan akhir untuk baris yang ingin dikelompokkan. Di Excel, pengindeksan baris dimulai dari 0.
- benar: Mengatur ini ke benar akan menyembunyikan baris yang dikelompokkan.
Setelah dieksekusi, baris dari 0 hingga 5 akan dikelompokkan dan disembunyikan dari pandangan.
## Langkah 6: Kelompokkan Kolom di Lembar Kerja
Sama seperti baris, Anda dapat mengelompokkan kolom untuk membuat tata letak yang lebih rapi dan teratur. Berikut cara mengelompokkan tiga kolom pertama.
```csharp
// Kelompokkan tiga kolom pertama (dari 0 hingga 2) dan buat mereka tersembunyi dengan meneruskan true
worksheet.Cells.GroupColumns(0, 2, true);
```
Parameter untuk fungsi ini adalah:
- 0, 2: Rentang kolom yang akan dikelompokkan, di mana pengindeksan dimulai dari 0.
- benar: Parameter ini menyembunyikan kolom yang dikelompokkan.
Kolom yang Anda pilih (0 hingga 2) sekarang akan muncul dikelompokkan dan disembunyikan dalam berkas Excel.
## Langkah 7: Simpan File Excel yang Telah Dimodifikasi
Setelah membuat perubahan, mari simpan berkas dengan nama baru untuk menghindari penimpaan berkas asli.
```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(dataDir + "output.xls");
```
 Anda sekarang telah berhasil menyimpan baris dan kolom yang dikelompokkan ke dalam`output.xls`Anda dapat menyesuaikan nama berkas sesuai kebutuhan.
## Langkah 8: Tutup Aliran File ke Sumber Daya Gratis
Terakhir, tutup aliran file untuk melepaskan semua sumber daya. Jika tidak, hal itu dapat menimbulkan masalah jika Anda perlu mengakses atau mengubah file tersebut lagi.
```csharp
// Menutup aliran file untuk membebaskan semua sumber daya
fstream.Close();
```
Selesai! Anda sekarang telah mengelompokkan baris dan kolom dalam file Excel menggunakan Aspose.Cells for .NET.
## Kesimpulan
Pengelompokan baris dan kolom di Excel dengan Aspose.Cells for .NET merupakan proses mudah yang dapat membuat lembar kerja Anda lebih mudah digunakan dan terorganisasi. Hanya dengan beberapa baris kode, Anda telah menguasai fitur hebat yang akan memerlukan lebih banyak langkah jika dilakukan secara manual di Excel. Selain itu, Anda dapat mengotomatiskan proses ini di banyak file, menghemat waktu dan mengurangi kesalahan. Panduan ini telah menunjukkan kepada Anda semua langkah yang Anda perlukan untuk mengendalikan file Excel Anda secara terprogram.
## Pertanyaan yang Sering Diajukan
### Bisakah saya mengelompokkan baris dan kolom tanpa menyembunyikannya?  
 Ya! Lewati saja`false` sebagai parameter ketiga dalam`GroupRows` atau`GroupColumns` metode.
### Bagaimana jika saya ingin memisahkan baris atau kolom?  
 Menggunakan`worksheet.Cells.UngroupRows(startRow, endRow)` atau`worksheet.Cells.UngroupColumns(startColumn, endColumn)` untuk memisahkannya.
### Bisakah saya mengelompokkan beberapa rentang dalam lembar kerja yang sama?  
 Tentu saja. Hubungi`GroupRows` atau`GroupColumns`metode pada setiap rentang yang ingin Anda kelompokkan.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells untuk .NET?  
 Ya, meskipun versi uji coba tersedia, Anda memerlukan lisensi untuk membuka fungsionalitas penuh. Anda bisa mendapatkan lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).
### Bisakah saya mengelompokkan baris dan kolom dengan logika kondisional?  
Ya! Anda dapat membuat pengelompokan bersyarat dengan memasukkan logika ke dalam kode Anda sebelum pengelompokan, tergantung pada data di setiap baris atau kolom.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
