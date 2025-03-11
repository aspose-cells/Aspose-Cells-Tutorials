---
title: Terapkan Urutan Halaman di Lembar Kerja
linktitle: Terapkan Urutan Halaman di Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengatur urutan halaman dalam lembar kerja Excel menggunakan Aspose.Cells for .NET dalam panduan langkah demi langkah yang sederhana. Sempurna untuk pemula dan ahli.
weight: 24
url: /id/net/worksheet-page-setup-features/implement-page-order/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Urutan Halaman di Lembar Kerja

## Perkenalan
Ingin menyesuaikan urutan halaman dalam lembar kerja Excel? Terkadang, mengendalikan cara data dicetak itu penting, terutama dengan lembar kerja besar yang tidak muat dalam satu halaman. Di sinilah Aspose.Cells for .NET berperan, memberi Anda alat yang hebat untuk menyusun halaman cetak sesuai keinginan Anda. Dalam panduan ini, kami akan memandu Anda mengatur urutan halaman dalam lembar kerja, khususnya untuk mencetak di baris terlebih dahulu, lalu ke kolom. Kedengarannya teknis? Jangan khawatir—saya akan membuatnya tetap sederhana, menguraikan semuanya langkah demi langkah.
## Prasyarat
Sebelum kita memulai, pastikan Anda telah menyiapkan hal berikut:
1.  Aspose.Cells untuk .NET: Jika Anda belum melakukannya, unduh[Aspose.Cells untuk .NET di sini](https://releases.aspose.com/cells/net/)Instal di proyek Anda untuk mengakses fitur yang akan kita gunakan.
2. Lingkungan Pengembangan: IDE apa pun yang kompatibel dengan .NET seperti Visual Studio akan berfungsi.
3. Pengetahuan Dasar C#: Kita akan bekerja dengan beberapa kode C#, jadi pemahaman mengenai konsep pemrograman dasar akan sangat membantu.
Mencoba[Aspose.Cells untuk .NET dengan uji coba gratis](https://releases.aspose.com/)atau dapatkan[lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk mengakses semua fitur!
## Paket Impor
Untuk memulai, kita perlu mengimpor namespace Aspose.Cells yang diperlukan. Ini akan memberi kita akses ke semua yang diperlukan untuk operasi kita.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Mari kita uraikan tutorial ini menjadi beberapa langkah mudah. Kita akan mulai dengan membuat buku kerja baru, mengakses pengaturan halaman lembar kerja, mengatur urutan halaman, lalu menyimpannya. 
## Langkah 1: Buat Buku Kerja
Hal pertama yang perlu kita lakukan adalah membuat objek buku kerja. Objek ini mewakili berkas Excel kita di Aspose.Cells.
```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
```
 Di sini, kita membuat sebuah instance dari`Workbook` kelas. Anggap saja seperti membuka buku kerja Excel baru yang kosong di program Anda.
## Langkah 2: Akses PageSetup dari Lembar Kerja
 Untuk mengontrol pengaturan cetak, kita perlu mengakses`PageSetup` objek lembar kerja. Ini akan memungkinkan kita untuk menyesuaikan bagaimana lembar kerja dicetak atau diekspor.
```csharp
// Mendapatkan referensi PageSetup dari lembar kerja
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
 Pada baris ini, kita mengambil`PageSetup` dari lembar kerja pertama (`Worksheets[0]`). Di sinilah kita akan mengonfigurasi pengaturan cetak, termasuk urutan halaman yang dicetak.
## Langkah 3: Atur Urutan Halaman ke OverThenDown
Sekarang untuk langkah kunci: mengatur urutan halaman. Secara default, Excel dapat mencetak setiap kolom sebelum pindah ke baris berikutnya, tetapi di sini kita menentukannya untuk menjadi "OverThenDown"—secara horizontal terlebih dahulu, kemudian vertikal.
```csharp
// Mengatur urutan pencetakan halaman ke atas lalu ke bawah
pageSetup.Order = PrintOrderType.OverThenDown;
```
 Kami telah mengatur`Order` milik`PageSetup` ke`PrintOrderType.OverThenDown`. Ini memberi tahu Excel untuk mencetak di seluruh baris sebelum berpindah ke baris halaman berikutnya. Jika Anda mencetak lembar kerja yang lebar, pengaturan ini memastikan semuanya mengalir secara logis pada hasil cetak.
## Langkah 4: Simpan Buku Kerja
Terakhir, mari kita simpan buku kerja kita untuk melihat hasilnya. Kita akan menentukan jalur dan nama file tempat penyimpanannya.
```csharp
// Jalur ke direktori dokumen
string dataDir = "Your Document Directory";
// Simpan buku kerja
workbook.Save(dataDir + "SetPageOrder_out.xls");
```
 Pada kode di atas, kita menyimpan buku kerja di direktori yang ditentukan dengan nama`SetPageOrder_out.xls` . Mengganti`"Your Document Directory"` dengan jalur tempat Anda ingin menyimpan berkas Anda.
Butuh bantuan dengan format output? Aspose.Cells mendukung banyak format, jadi bereksperimenlah dengan format seperti`.xlsx` jika Anda memerlukan format Excel terbaru.
## Kesimpulan
Nah, itu dia! Anda baru saja mengatur urutan halaman dalam lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Hanya dengan beberapa baris kode, kami mengendalikan cara data dicetak, yang dapat menjadi pengubah permainan untuk menyajikan kumpulan data besar dengan jelas di atas kertas. Ini hanyalah salah satu dari sekian banyak pengaturan cetak yang dapat Anda sesuaikan dengan Aspose.Cells. Jadi, apakah Anda sedang mempersiapkan laporan, lembar kerja siap cetak, atau dokumen terorganisasi, Aspose.Cells siap membantu Anda.
## Pertanyaan yang Sering Diajukan
### Bisakah saya mengubah urutan halaman untuk beberapa lembar kerja sekaligus?
 Ya, cukup ulangi setiap lembar kerja di buku kerja dan terapkan hal yang sama`PageSetup.Order` pengaturan.
### Apa saja pilihan lain untuk pemesanan cetak selain OverThenDown?
 Pilihan alternatifnya adalah`DownThenOver`, yang akan mencetak kolom terlebih dahulu, kemudian mencetak baris demi baris.
### Apakah kode ini memerlukan lisensi?
Beberapa fitur mungkin terbatas tanpa lisensi. Anda dapat mencoba[Aspose.Cells untuk .NET dengan uji coba gratis](https://releases.aspose.com/).
### Bisakah saya melihat dulu susunan halaman sebelum mencetaknya?
Meskipun Aspose.Cells memungkinkan pengaturan cetak, Anda harus membuka file yang disimpan di Excel untuk melihat pratinjaunya karena tidak ada pratinjau langsung di Aspose.
### Apakah pengaturan urutan halaman ini kompatibel dengan format lain seperti PDF?
Ya, setelah ditetapkan, urutan halaman akan berlaku untuk ekspor PDF atau format lain yang didukung, memastikan alur halaman yang konsisten.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
