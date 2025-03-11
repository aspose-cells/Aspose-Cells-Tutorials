---
title: Sesuaikan Tingkat Kompresi
linktitle: Sesuaikan Tingkat Kompresi
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara menyesuaikan tingkat kompresi untuk file Excel menggunakan Aspose.Cells for .NET. Optimalkan ukuran file Anda secara efisien dengan panduan langkah demi langkah ini.
weight: 50
url: /id/net/excel-workbook/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sesuaikan Tingkat Kompresi

## Perkenalan

Saat menangani file Excel yang besar, penyimpanan yang efisien adalah kuncinya. Baik Anda seorang pengembang yang ingin mengoptimalkan ukuran file atau analis data yang ingin mempercepat transfer file, memahami cara menyesuaikan tingkat kompresi di Aspose.Cells untuk .NET dapat menjadi pengubah permainan. Dalam panduan ini, kami akan memandu Anda melalui langkah-langkah untuk menyesuaikan tingkat kompresi saat menyimpan file Excel, memastikan Anda mempertahankan kinerja tanpa mengorbankan kualitas.

## Prasyarat

Sebelum menyelami seluk-beluk level kompresi, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai:

1. Pengetahuan Dasar tentang C#: Pemahaman dasar tentang pemrograman C# sangatlah penting. Jika Anda memahami variabel, loop, dan operasi file dasar, Anda siap untuk memulai!
2. Pustaka Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya dari[situs web](https://releases.aspose.com/cells/net/) Jika Anda baru memulai, pertimbangkan untuk mengambil uji coba gratis[Di Sini](https://releases.aspose.com/).
3. Lingkungan Pengembangan: Siapkan lingkungan pengembangan Anda, idealnya Visual Studio, untuk menulis dan mengeksekusi kode C# Anda. 
4. Contoh Berkas Excel: Siapkan berkas Excel berukuran besar untuk pengujian. Anda dapat membuat berkas Excel atau menggunakan berkas yang sudah ada, tetapi pastikan ukurannya cukup besar untuk melihat efek kompresi.

Jika semua prasyarat itu terpenuhi, mari kita mulai!

## Paket Impor

Sebelum kita dapat memanipulasi file Excel, kita perlu mengimpor namespace yang diperlukan. Ini adalah langkah penting yang memungkinkan kita mengakses kelas dan metode yang disediakan oleh Aspose.Cells.

### Impor Namespace Aspose.Cells

```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```

 Potongan kode ini mengimpor`Aspose.Cells` namespace, yang berisi semua kelas yang dibutuhkan untuk bekerja dengan file Excel.`Aspose.Cells.Xlsb` namespace khusus untuk menangani format file XLSB.

Setelah semuanya siap, mari kita bagi proses penyesuaian tingkat kompresi menjadi beberapa langkah yang mudah dikelola. Kita akan menyimpan buku kerja dengan berbagai tingkat kompresi dan mengukur waktu yang dibutuhkan untuk setiap operasi. 

## Langkah 1: Siapkan Direktori Anda

Pertama-tama, kita perlu menentukan di mana file kita akan disimpan. Ini melibatkan penentuan direktori sumber untuk file masukan dan direktori keluaran untuk file terkompresi.

```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```

## Langkah 2: Muat Buku Kerja

Selanjutnya, kita akan memuat buku kerja Excel yang ingin kita kompres. Di sinilah Anda akan mengarahkan ke berkas Excel Anda yang besar.

```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```

 Baris ini menginisialisasi yang baru`Workbook` objek dengan file yang ditentukan. Pastikan jalur file sudah benar; jika tidak, Anda akan mengalami kesalahan.

## Langkah 3: Buat Opsi Penyimpanan untuk XLSB

 Sekarang, kita akan membuat sebuah instance dari`XlsbSaveOptions`, yang memungkinkan kita menentukan bagaimana kita ingin menyimpan buku kerja kita, termasuk tingkat kompresi.

```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```

Baris ini mempersiapkan opsi yang akan kita gunakan untuk menyimpan buku kerja kita dalam format XLSB.

## Langkah 4: Tetapkan dan Ukur Tingkat Kompresi

Sekarang tibalah bagian yang menyenangkan! Kita akan menyimpan buku kerja menggunakan berbagai tingkat kompresi dan mengukur waktu yang dibutuhkan untuk setiap operasi. 

### Kompresi Level 1

Mari kita mulai dengan tingkat kompresi terendah:

```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```

Dalam cuplikan ini, kami menetapkan jenis kompresi ke Level 1, menyimpan buku kerja, dan mencatat waktu yang dibutuhkan. 

### Kompresi Level 6

Berikutnya, kita akan mencoba tingkat kompresi jarak menengah:

```csharp
options.CompressionType = OoxmlCompressionType.Level6;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```

Kali ini, kami mengatur jenis kompresi ke Level 6 dan mengulangi operasi penyimpanan.

### Kompresi Level 9

Terakhir, mari simpan menggunakan tingkat kompresi tertinggi:

```csharp
options.CompressionType = OoxmlCompressionType.Level9;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```

Pada langkah ini, kami menetapkan jenis kompresi ke Level 9, yang seharusnya menghasilkan ukuran file terkecil tetapi mungkin memerlukan waktu lebih lama untuk disimpan.

## Langkah 5: Hasil Akhir

Setelah menjalankan semua langkah di atas, Anda akan melihat waktu yang telah berlalu untuk setiap tingkat kompresi yang dicetak pada konsol. 

```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```

Baris ini mengonfirmasi bahwa seluruh proses telah diselesaikan tanpa masalah.

## Kesimpulan

Menyesuaikan tingkat kompresi saat menyimpan file Excel dengan Aspose.Cells untuk .NET merupakan teknik yang mudah namun ampuh. Dengan mengikuti langkah-langkah yang diuraikan dalam panduan ini, Anda dapat dengan mudah memanipulasi ukuran file, membuatnya lebih mudah dikelola untuk penyimpanan dan transfer. Apakah Anda memerlukan akses cepat ke data atau ingin mengoptimalkan kinerja aplikasi Anda, menguasai teknik-teknik ini niscaya akan meningkatkan keterampilan Anda sebagai pengembang.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel secara terprogram.

### Bagaimana cara mengunduh Aspose.Cells?
 Anda dapat mengunduh pustaka Aspose.Cells dari[situs web](https://releases.aspose.com/cells/net/).

### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Aspose menawarkan versi uji coba gratis yang dapat Anda akses[Di Sini](https://releases.aspose.com/).

### Apa saja tingkat kompresi yang tersedia?
Aspose.Cells mendukung beberapa tingkat kompresi mulai dari Tingkat 1 (kompresi paling sedikit) hingga Tingkat 9 (kompresi maksimum).

### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?
 Anda bisa mendapatkan dukungan dan mengajukan pertanyaan di[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
