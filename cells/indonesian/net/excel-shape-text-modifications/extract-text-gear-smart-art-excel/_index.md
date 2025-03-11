---
title: Ekstrak Teks dari Smart Art Jenis Roda Gigi di Excel
linktitle: Ekstrak Teks dari Smart Art Jenis Roda Gigi di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengekstrak teks dari SmartArt bertipe roda gigi di Excel menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah dan contoh kode disertakan.
weight: 10
url: /id/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Smart Art Jenis Roda Gigi di Excel

## Perkenalan
Saat bekerja dengan Excel, Anda mungkin menemukan grafik SmartArt yang membantu menyampaikan pesan Anda dengan cara yang menarik secara visual. Di antara grafik ini, SmartArt tipe roda gigi adalah favorit karena alur hierarkis dan arahnya, yang sering digunakan dalam manajemen proyek atau pemodelan sistem. Namun, bagaimana jika Anda perlu mengekstrak teks dari bentuk ini secara terprogram? Di sinilah Aspose.Cells for .NET berguna! Dalam posting blog ini, kami akan memandu Anda melalui panduan langkah demi langkah tentang cara mengekstrak teks dari bentuk SmartArt tipe roda gigi di Excel menggunakan Aspose.Cells for .NET.
## Prasyarat
Sebelum kita mulai, ada beberapa prasyarat penting yang perlu Anda penuhi. Jangan khawatir; ini mudah, dan saya akan memandu Anda.
### Lingkungan .NET
Pastikan Anda memiliki lingkungan pengembangan .NET yang sudah disiapkan di komputer Anda. Ini bisa berupa Visual Studio atau IDE pilihan Anda yang mendukung pengembangan .NET.
### Aspose.Cells untuk .NET
 Selanjutnya, Anda perlu menginstal pustaka Aspose.Cells. Ini adalah perangkat keras yang akan memungkinkan Anda untuk memanipulasi file Excel dengan mudah. Anda dapat mengunduhnya dari[Halaman Rilis Aspose](https://releases.aspose.com/cells/net/) Jika Anda ingin menjelajahinya terlebih dahulu, manfaatkan[uji coba gratis](https://releases.aspose.com/).
### Pengetahuan Dasar C#
Pemahaman dasar tentang pemrograman C# adalah hal yang Anda perlukan untuk mengikuti tutorial ini. Jika Anda baru mengenalnya, jangan khawatir—saya akan merancang langkah-langkahnya agar seramah mungkin bagi pemula.
### Contoh File Excel
Untuk tutorial ini, Anda juga memerlukan contoh berkas Excel yang berisi bentuk SmartArt bertipe roda gigi. Anda dapat membuatnya dengan mudah atau mencari templatnya secara daring. Pastikan SmartArt menyertakan setidaknya satu bentuk bertipe roda gigi.
## Paket Impor
Untuk memulai pengkodean, Anda perlu mengimpor paket-paket yang diperlukan. Berikut cara melakukannya:
### Buat Proyek Baru
1. Buka IDE .NET Anda.
2. Buat proyek baru. Misalnya, pilih 'Aplikasi Konsol' di bawah opsi .NET.
3. Berikan nama pada proyek Anda dan tetapkan kerangka kerja yang diinginkan. 
### Tambahkan Referensi
Untuk menggunakan Aspose.Cells, Anda perlu menambahkan referensi pustaka ke proyek Anda:
1. Klik kanan pada nama proyek Anda di Solution Explorer.
2. Pilih “Kelola Paket NuGet”.
3. Cari "Aspose.Cells" dan instal.
Setelah terinstal, Anda siap untuk membuat kode!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Sekarang, mari kita bahas kode yang akan Anda gunakan untuk mengekstrak teks. Kita akan melakukannya langkah demi langkah.
## Langkah 1: Siapkan Direktori Sumber
Mulailah dengan menentukan direktori tempat file Excel Anda berada:
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
```
 Pastikan untuk mengganti`"Your Document Directory"` dengan jalur sebenarnya ke berkas Excel Anda.
## Langkah 2: Muat Buku Kerja Excel
Selanjutnya, kita akan memuat buku kerja Excel. Berikut ini cara mengakses isinya:
```csharp
// Muat contoh file Excel yang berisi bentuk seni pintar jenis roda gigi.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Bagian ini akan memuat contoh buku kerja Excel Anda.
## Langkah 3: Akses Lembar Kerja Pertama
Sekarang setelah kita memuat buku kerja, mari mengakses lembar kerja pertama tempat SmartArt kita berada:
```csharp
// Akses lembar kerja pertama.
Worksheet ws = wb.Worksheets[0];
```
Ini mengambil lembar kerja pertama untuk manipulasi lebih lanjut.
## Langkah 4: Akses Bentuk Pertama
Selanjutnya, kita perlu mengakses bentuk pertama dalam lembar kerja kita. Dengan melakukan ini, kita dapat menavigasi melalui grafik SmartArt kita:
```csharp
// Akses bentuk pertama.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Di sini, kami berfokus pada bentuk pertama, yang kami asumsikan sebagai SmartArt yang kami butuhkan.
## Langkah 5: Dapatkan Bentuk Grup
Setelah kita memiliki bentuknya, saatnya untuk mendapatkan hasil representasi SmartArt kita:
```csharp
// Dapatkan hasil bentuk seni pintar jenis roda gigi dalam bentuk bentuk grup.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Ini mengambil SmartArt jenis roda gigi kita sebagai bentuk yang dikelompokkan.
## Langkah 6: Ekstrak Bentuk Individual
Sekarang, mari kita ekstrak bentuk-bentuk individual yang membentuk SmartArt kita:
```csharp
// Dapatkan daftar bentuk individual yang terdiri dari bentuk grup.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Susunan ini akan menampung semua bentuk individual yang perlu kita ulangi.
## Langkah 7: Ekstrak dan Cetak Teks
Terakhir, kita dapat mengulang array bentuk kita dan mengekstrak teks dari bentuk roda gigi apa pun:
```csharp
// Ekstrak teks bentuk roda gigi dan cetak pada konsol.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
Dalam perulangan ini, kita memeriksa jenis bentuknya dan mencetak teks jika bentuknya adalah roda gigi.
## Langkah 8: Konfirmasi Eksekusi
Terakhir, Anda mungkin ingin menambahkan pesan konfirmasi setelah proses berhasil diselesaikan:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Dengan ini, ekstraksi Anda selesai, dan Anda akan melihat keluaran teks Anda di konsol!
## Kesimpulan
 Selamat! Anda baru saja mempelajari cara mengekstrak teks dari bentuk SmartArt tipe roda gigi di Excel menggunakan Aspose.Cells untuk .NET. Teknik praktis ini membuka pintu untuk mengotomatiskan laporan atau dokumentasi yang bergantung pada representasi data visual. Baik Anda pengembang berpengalaman atau baru memulai, mengendalikan dan mengekstrak informasi dari SmartArt dapat memperlancar alur kerja Anda dan membuat Anda lebih efisien. Jangan lupa untuk menjelajahi detailnya[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk kemampuan lebih lanjut.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat dan memanipulasi file Excel dengan mudah.
### Bisakah saya menggunakan Aspose.Cells dengan bahasa lain?
Ya! Aspose.Cells tersedia dalam berbagai bahasa pemrograman, termasuk Java dan Python.
### Apakah saya perlu membeli Aspose.Cells untuk .NET?
 Aspose.Cells menawarkan uji coba gratis, tetapi untuk penggunaan lebih lama, diperlukan pembelian. Anda dapat menemukan opsi pembelian[Di Sini](https://purchase.aspose.com/buy).
### Apakah ada dukungan yang tersedia untuk pengguna Aspose.Cells?
 Tentu saja! Anda dapat menemukan dukungan komunitas di[Forum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Bisakah saya mengekstrak tipe SmartArt lain menggunakan metode ini?
Ya, dengan sedikit modifikasi, Anda dapat mengekstrak teks dari berbagai bentuk SmartArt dengan mengubah kondisi dalam kode Anda.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
