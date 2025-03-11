---
title: Sesuaikan Tingkat Kompresi di Buku Kerja
linktitle: Sesuaikan Tingkat Kompresi di Buku Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyesuaikan tingkat kompresi buku kerja Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah ini. Optimalkan manajemen berkas Anda.
weight: 14
url: /id/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sesuaikan Tingkat Kompresi di Buku Kerja

## Perkenalan
Dalam hal mengelola file Excel yang besar, kompresi adalah pengubah permainan. Tidak hanya menghemat ruang penyimpanan, tetapi juga membuat transfer file lebih cepat dan lebih efisien. Jika Anda bekerja dengan Aspose.Cells untuk .NET, Anda dapat dengan mudah menyesuaikan tingkat kompresi buku kerja Anda. Dalam panduan ini, kami akan memandu Anda melalui proses langkah demi langkah, memastikan bahwa Anda memahami setiap bagian kode dan cara kerjanya.
## Prasyarat
Sebelum menyelami kodenya, ada beberapa prasyarat yang perlu Anda penuhi:
1. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
2.  Pustaka Aspose.Cells: Anda perlu menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/cells/net/).
3. Visual Studio: Lingkungan pengembangan seperti Visual Studio akan diperlukan untuk menjalankan kode.
4. .NET Framework: Pastikan proyek Anda disiapkan dengan versi .NET Framework yang kompatibel.
## Paket Impor
Untuk memulai, Anda perlu mengimpor paket yang diperlukan ke dalam proyek C# Anda. Berikut cara melakukannya:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Paket-paket ini penting untuk bekerja dengan file Excel menggunakan pustaka Aspose.Cells.`Aspose.Cells` namespace berisi semua kelas yang Anda butuhkan untuk memanipulasi file Excel, sementara`Aspose.Cells.Xlsb` menyediakan opsi untuk menyimpan file dalam format XLSB.
Sekarang, mari kita uraikan proses penyesuaian tingkat kompresi dalam buku kerja menjadi langkah-langkah yang dapat dikelola.
## Langkah 1: Tentukan Direktori Sumber dan Output
Pertama, Anda perlu menentukan di mana file sumber Anda berada dan di mana Anda ingin menyimpan file output. Hal ini penting untuk memastikan bahwa program Anda mengetahui di mana menemukan file yang dibutuhkannya untuk bekerja.
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya ke direktori Anda. Ini akan membantu program menemukan file yang ingin Anda kompres.
## Langkah 2: Muat Buku Kerja
Berikutnya, Anda akan memuat buku kerja yang ingin dikompres. Di sinilah keajaiban dimulai!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
Pada baris ini, kita membuat instance baru dari`Workbook` kelas dan memuat berkas Excel yang ada. Pastikan nama berkas sesuai dengan yang ada di direktori sumber Anda.
## Langkah 3: Siapkan Opsi Penyimpanan
Sekarang saatnya mengonfigurasi opsi penyimpanan. Kita akan mengatur jenis kompresi untuk file output. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 Itu`XlsbSaveOptions` kelas memungkinkan Anda menentukan berbagai opsi saat menyimpan buku kerja dalam format XLSB, termasuk tingkat kompresi.
## Langkah 4: Mengukur Waktu Kompresi untuk Level 1
Mari kita mulai dengan tingkat kompresi pertama. Kita akan mengukur berapa lama waktu yang dibutuhkan untuk menyimpan buku kerja dengan tingkat kompresi ini.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Di sini, kami menetapkan jenis kompresi ke Level 1, menyimpan buku kerja, lalu mengukur waktu yang telah berlalu. Ini memberi kita gambaran tentang berapa lama proses tersebut berlangsung.
## Langkah 5: Mengukur Waktu Kompresi untuk Level 6
Berikutnya, mari kita lihat bagaimana kinerja kompresi Level 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Langkah ini mirip dengan langkah sebelumnya, tetapi kita mengubah level kompresi ke Level 6. Anda akan melihat bahwa waktu yang dibutuhkan mungkin berbeda-beda berdasarkan kompleksitas buku kerja.
## Langkah 6: Mengukur Waktu Kompresi untuk Level 9
Terakhir, mari kita periksa kinerja dengan tingkat kompresi tertinggi.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
Pada langkah ini, kami menetapkan level kompresi ke Level 9. Di sinilah Anda biasanya akan melihat pengurangan ukuran file yang paling signifikan, tetapi prosesnya mungkin memerlukan waktu lebih lama.
## Langkah 7: Hasil Akhir
Setelah menjalankan semua level kompresi, Anda dapat menampilkan pesan yang menunjukkan bahwa proses telah berhasil diselesaikan.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Baris kode sederhana ini mengonfirmasi bahwa program Anda telah selesai dijalankan tanpa hambatan apa pun.
## Kesimpulan
Menyesuaikan tingkat kompresi buku kerja Anda menggunakan Aspose.Cells for .NET merupakan proses mudah yang dapat menghasilkan manfaat signifikan dalam hal ukuran dan kinerja file. Dengan mengikuti langkah-langkah yang diuraikan dalam panduan ini, Anda dapat dengan mudah menerapkan kompresi dalam aplikasi Anda dan meningkatkan efisiensi pengelolaan file Excel Anda.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?  
Aspose.Cells adalah pustaka hebat untuk .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel tanpa memerlukan Microsoft Excel.
### Bagaimana cara menginstal Aspose.Cells?  
 Anda dapat mengunduh dan menginstal Aspose.Cells dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
### Tingkat kompresi apa yang tersedia?  
Aspose.Cells mendukung beberapa tingkat kompresi mulai dari Tingkat 1 (kompresi terendah) hingga Tingkat 9 (kompresi tertinggi).
### Bisakah saya menguji Aspose.Cells secara gratis?  
 Ya! Anda bisa mendapatkan uji coba Aspose.Cells secara gratis[Di Sini](https://releases.aspose.com/).
### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?  
 Untuk pertanyaan atau dukungan apa pun, Anda dapat mengunjungi forum dukungan Aspose[Di Sini](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
