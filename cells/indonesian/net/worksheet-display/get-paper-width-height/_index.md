---
title: Dapatkan Lebar dan Tinggi Kertas untuk Pencetakan Lembar Kerja
linktitle: Dapatkan Lebar dan Tinggi Kertas untuk Pencetakan Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mendapatkan lebar dan tinggi kertas untuk pencetakan lembar kerja di Aspose.Cells untuk .NET dengan panduan langkah demi langkah ini.
weight: 16
url: /id/net/worksheet-display/get-paper-width-height/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Lebar dan Tinggi Kertas untuk Pencetakan Lembar Kerja

## Perkenalan
Mencetak dokumen secara akurat memerlukan pengetahuan tentang dimensi kertas. Jika Anda seorang pengembang atau bekerja pada aplikasi yang menangani file Excel, Anda mungkin perlu mengetahui cara mendapatkan lebar dan tinggi kertas saat mencetak lembar kerja. Untungnya, Aspose.Cells for .NET menyediakan cara yang kuat untuk mengelola dokumen Excel secara terprogram. Dalam artikel ini, kami akan memandu Anda melalui proses penentuan ukuran kertas secara spesifik, menggunakan contoh-contoh sederhana untuk mengilustrasikan konsep-konsep mendasar. 
## Prasyarat
Sebelum kita menyelami detail teknisnya, mari kita bahas beberapa hal mendasar. Untuk mengikuti tutorial ini dengan sukses, Anda memerlukan:
### 1. Pengetahuan Dasar C#
Anda harus memiliki pemahaman yang baik tentang pemrograman C#, karena kita akan bekerja dalam lingkungan .NET.
### 2. Pustaka Aspose.Cells
Pastikan Anda telah menginstal pustaka Aspose.Cells di proyek Anda. Jika Anda belum melakukannya, Anda dapat mengunduh versi terbaru dari[Halaman unduhan Aspose.Cells](https://releases.aspose.com/cells/net/).
### 3. IDE Visual Studio
Ada baiknya Anda memiliki Visual Studio untuk menjalankan dan mengelola proyek C# Anda. Versi apa pun yang mendukung .NET akan berfungsi dengan baik.
### 4. Lisensi Aspose yang Valid
 Meskipun Aspose.Cells dapat dicoba, pertimbangkan untuk membeli lisensi jika Anda menggunakannya untuk proyek jangka panjang. Anda dapat membelinya melalui[tautan ini](https://purchase.aspose.com/buy) atau jelajahi[lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk fase pengujian singkat.
Setelah semuanya siap, mari masuk ke kode!
## Mengimpor Paket
Langkah pertama dalam perjalanan kita melibatkan pengimporan namespace penting. Ini penting, karena memungkinkan kita mengakses kelas dan metode yang akan kita gunakan untuk memanipulasi file Excel. Berikut cara melakukannya:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Pastikan untuk menyertakan baris ini di bagian atas file .cs Anda. Sekarang setelah impor siap, mari lanjutkan dengan membuat buku kerja dan mengakses lembar kerja.
## Langkah 1: Buat Buku Kerja Anda
Kita mulai dengan membuat sebuah instance dari`Workbook` kelas. Ini merupakan dasar dari manipulasi file Excel kita.
```csharp
Workbook wb = new Workbook();
```
Baris ini memberi tahu program untuk menginisialisasi buku kerja baru, yang menyiapkan kita untuk masuk ke lembar kerja kita.
## Langkah 2: Akses Lembar Kerja Pertama
Selanjutnya, kita akan mengakses lembar kerja pertama di buku kerja yang baru kita buat. Cukup mudah:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Di sini, kita mengakses lembar pertama (diindeks pada 0) di buku kerja kita. Di sinilah kita akan mengatur ukuran kertas.
## Mengatur Ukuran Kertas dan Mengambil Dimensi
Sekarang kita memasuki inti operasi—mengatur ukuran kertas dan mengambil dimensinya! Mari kita uraikan ini selangkah demi selangkah.
## Langkah 3: Atur Ukuran Kertas ke A2
Pertama-tama, atur ukuran kertas kita ke A2 dan cetak dimensinya.
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
 Setelah pengaturan ini, kami menggunakan`Console.WriteLine` untuk menampilkan dimensi. Saat Anda menjalankan ini, Anda akan melihat lebar dan tinggi dalam inci untuk ukuran kertas A2.
## Langkah 4: Atur Ukuran Kertas ke A3
Sekarang saatnya untuk A3! Kita cukup mengulang prosesnya:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Voila! Deklarasi akan mencetak tinggi dan lebar spesifik untuk kertas A3.
## Langkah 5: Atur Ukuran Kertas ke A4
Mengikuti pola yang sama, mari kita periksa bagaimana ukuran A4:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Ini memberi kita dimensi untuk A4—salah satu ukuran kertas yang paling umum digunakan.
## Langkah 6: Atur Ukuran Kertas ke Letter
Untuk melengkapi penjelajahan kita tentang ukuran kertas, mari kita atur ke ukuran Letter:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Sekali lagi, kita akan melihat lebar dan tinggi spesifik untuk ukuran Surat.
## Kesimpulan
Nah, itu dia! Anda baru saja mempelajari cara mendapatkan lebar dan tinggi kertas untuk berbagai ukuran saat menyiapkan lembar kerja untuk dicetak menggunakan Aspose.Cells for .NET. Utilitas ini bisa sangat membantu, terutama saat Anda merencanakan tata letak pencetakan atau mengelola pengaturan cetak secara terprogram. Dengan mengetahui dimensi yang tepat dalam inci, Anda dapat menghindari kesalahan umum dan memastikan bahwa dokumen Anda dicetak sesuai keinginan.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang menyediakan berbagai fitur untuk bekerja dengan file Excel secara terprogram.
### Bagaimana cara memulai dengan Aspose.Cells?
Mulailah dengan mengunduh perpustakaan dari[Situs web Aspose](https://releases.aspose.com/cells/net/) dan ikuti dokumentasi untuk mengaturnya di proyek Anda.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
Aspose.Cells menawarkan versi uji coba, yang dapat Anda gunakan untuk menjelajahi fitur-fiturnya. Untuk penggunaan jangka panjang, Anda perlu membeli lisensi.
### Ukuran kertas apa yang didukung oleh Aspose.Cells?
Aspose.Cells mendukung berbagai ukuran kertas termasuk A2, A3, A4, Letter, dan banyak lainnya.
### Di mana saya dapat menemukan lebih banyak sumber daya atau dukungan untuk Aspose.Cells?
 Anda dapat memeriksa[Forum Aspose](https://forum.aspose.com/c/cells/9) untuk bantuan masyarakat dan[dokumentasi](https://reference.aspose.com/cells/net/) untuk tutorial dan materi referensi.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
