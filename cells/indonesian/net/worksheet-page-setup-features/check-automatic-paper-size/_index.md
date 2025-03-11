---
title: Periksa apakah Ukuran Kertas Lembar Kerja Otomatis
linktitle: Periksa apakah Ukuran Kertas Lembar Kerja Otomatis
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara memeriksa apakah ukuran kertas lembar kerja otomatis menggunakan Aspose.Cells untuk .NET dalam panduan langkah demi langkah terperinci kami.
weight: 11
url: /id/net/worksheet-page-setup-features/check-automatic-paper-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Periksa apakah Ukuran Kertas Lembar Kerja Otomatis

## Perkenalan
Dalam hal mengelola lembar kerja dan memastikan bahwa lembar kerja diformat dengan sempurna untuk dicetak, satu aspek penting yang perlu dipertimbangkan adalah pengaturan ukuran kertas. Dalam panduan ini, kita akan membahas cara memeriksa apakah ukuran kertas lembar kerja diatur ke otomatis menggunakan Aspose.Cells untuk .NET. Pustaka ini menawarkan berbagai alat canggih untuk semua kebutuhan terkait Excel Anda, yang membuat pekerjaan Anda tidak hanya lebih mudah tetapi juga lebih efisien.
## Prasyarat
Sebelum mulai membuat kode, pastikan Anda telah menyiapkan semuanya. Berikut ini adalah prasyarat yang Anda perlukan:
1. Lingkungan Pengembangan C#: Anda memerlukan IDE C# seperti Visual Studio. Jika Anda belum menginstalnya, kunjungi situs web Microsoft.
2.  Pustaka Aspose.Cells: Pastikan Anda memiliki pustaka Aspose.Cells. Anda dapat mengunduhnya dari[tautan ini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Keakraban dengan konsep pemrograman C# akan membantu Anda memahami contoh dan cuplikan kode secara efektif.
4. Contoh Berkas Excel: Pastikan Anda memiliki contoh berkas Excel yang memiliki pengaturan halaman yang diperlukan. Untuk contoh kita, Anda memerlukan dua berkas:
- `samplePageSetupIsAutomaticPaperSize-False.xlsx`
- `samplePageSetupIsAutomaticPaperSize-True.xlsx`
Memiliki prasyarat ini akan mempersiapkan Anda untuk sukses saat kita menjelajahi fungsionalitas yang disediakan oleh Aspose.Cells.
## Paket Impor
Untuk memulai, Anda perlu mengimpor paket yang diperlukan ke dalam proyek C# Anda. Berikut cara melakukannya:
### Buat Proyek C# Baru
- Buka Visual Studio dan buat Aplikasi Konsol C# baru.
-  Beri nama seperti`CheckPaperSize`.
### Tambahkan Referensi Aspose.Cells
- Klik kanan pada proyek Anda di Solution Explorer.
- Pilih "Kelola Paket NuGet".
- Cari "Aspose.Cells" dan instal.
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Setelah Anda menyiapkan semuanya, Anda siap untuk memasuki bagian yang menyenangkan!
Sekarang, mari kita uraikan proses tersebut menjadi beberapa langkah yang dapat dikelola.
## Langkah 1: Tentukan Direktori Sumber dan Output
Pertama, kita perlu menentukan di mana file contoh Excel kita berada dan di mana kita ingin menyimpan hasilnya. 
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Excel contoh Anda disimpan. Hal ini penting bagi program untuk menemukan file yang dibutuhkannya untuk bekerja.
## Langkah 2: Muat Buku Kerja
Selanjutnya, kita akan memuat dua buku kerja yang telah kita siapkan sebelumnya. Berikut ini cara melakukannya:
```csharp
// Muat buku kerja pertama yang memiliki ukuran kertas otomatis salah
Workbook wb1 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-False.xlsx");
// Muat buku kerja kedua yang memiliki ukuran kertas otomatis benar
Workbook wb2 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-True.xlsx");
```
Kami memuat dua buku kerja ke dalam memori. Buku kerja pertama diatur agar fitur ukuran kertas otomatis dinonaktifkan, sedangkan buku kerja kedua mengaktifkannya. Pengaturan ini memungkinkan kita untuk membandingkannya dengan mudah nanti.
## Langkah 3: Akses Lembar Kerja
Sekarang kita akan mengakses lembar kerja pertama dari kedua buku kerja untuk memeriksa pengaturan ukuran kertasnya.
```csharp
// Akses lembar kerja pertama dari kedua buku kerja
Worksheet ws11 = wb1.Worksheets[0];
Worksheet ws12 = wb2.Worksheets[0];
```
Dengan mengakses lembar kerja pertama (indeks 0) dari kedua buku kerja, kita berfokus pada halaman relevan yang ingin kita selidiki. 
## Langkah 4: Periksa Properti IsAutomaticPaperSize
 Mari kita luangkan waktu sejenak untuk memeriksa`IsAutomaticPaperSize` properti dari setiap lembar kerja.
```csharp
// Cetak properti PageSetup.IsAutomaticPaperSize dari kedua lembar kerja
Console.WriteLine("First Worksheet of First Workbook - IsAutomaticPaperSize: " + ws11.PageSetup.IsAutomaticPaperSize);
Console.WriteLine("First Worksheet of Second Workbook - IsAutomaticPaperSize: " + ws12.PageSetup.IsAutomaticPaperSize);
```
 Di sini, kita mencetak apakah setiap lembar kerja memiliki fitur ukuran kertas otomatis yang diaktifkan atau tidak. Properti`IsAutomaticPaperSize` mengembalikan nilai boolean (benar atau salah), yang menunjukkan pengaturan.
## Langkah 5: Output Akhir dan Konfirmasi
Terakhir, mari kita letakkan hasil program kita dalam konteks dan pastikan program tersebut berhasil dijalankan.
```csharp
Console.WriteLine();
Console.WriteLine("DetermineIfPaperSizeOfWorksheetIsAutomatic executed successfully.\r\n");
```
Setelah mencetak pengaturan, kami mencetak pesan berhasil untuk menunjukkan bahwa program kami berjalan tanpa masalah.
## Kesimpulan
Dalam tutorial ini, kami membahas cara memeriksa apakah pengaturan ukuran kertas lembar kerja dalam file Excel diatur ke otomatis menggunakan Aspose.Cells untuk .NET. Dengan mengikuti langkah-langkah ini, Anda sekarang memiliki keterampilan dasar untuk memanipulasi file Excel secara terprogram dengan mudah dan memeriksa konfigurasi tertentu seperti ukuran kertas. 
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka hebat yang dirancang untuk memanipulasi format dokumen Excel dalam aplikasi .NET.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Aspose menawarkan versi uji coba gratis. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/).
### Bagaimana cara membeli lisensi untuk Aspose.Cells?
 Anda dapat membeli lisensi melalui halaman pembelian mereka yang ditemukan[Di Sini](https://purchase.aspose.com/buy).
### Jenis berkas Excel apa yang dapat saya gunakan menggunakan Aspose.Cells?
Anda dapat bekerja dengan berbagai format Excel, termasuk XLS, XLSX, CSV, dan banyak lainnya.
### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?
 Anda dapat menemukan forum dukungan dan sumber daya[Di Sini](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
