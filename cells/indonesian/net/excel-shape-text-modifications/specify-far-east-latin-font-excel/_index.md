---
title: Tentukan Font Timur Jauh & Latin di Excel
linktitle: Tentukan Font Timur Jauh & Latin di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menentukan font Timur Jauh dan Latin di Excel menggunakan Aspose.Cells untuk .NET dalam tutorial yang komprehensif dan mudah diikuti ini.
weight: 17
url: /id/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tentukan Font Timur Jauh & Latin di Excel

## Perkenalan
Apakah Anda ingin menyempurnakan laporan atau dokumen Excel Anda dengan persyaratan font tertentu? Baik Anda menggunakan banyak bahasa atau hanya ingin mendapatkan estetika unik di lembar kerja Anda, memahami cara menentukan font Timur Jauh dan Latin di Excel adalah keterampilan yang penting. Beruntung bagi Anda, kami punya solusinya! Dalam tutorial ini, kami akan membahas cara menggunakan Aspose.Cells for .NET untuk mengimplementasikan fitur ini dengan lancar. Mari kita bahas!
## Prasyarat
Sebelum kita masuk ke inti pembahasan, ada beberapa hal yang perlu Anda siapkan sebelum memulai dengan Aspose.Cells:
### .NET Framework atau .NET Core
Pastikan Anda telah menginstal .NET Framework atau .NET Core di komputer Anda. Pustaka ini berfungsi baik dengan keduanya.
### Instalasi Aspose.Cells
 Anda perlu mengunduh pustaka Aspose.Cells. Anda dapat[unduh dari sini](https://releases.aspose.com/cells/net/) Jika Anda tidak terbiasa dengan menginstal paket NuGet, ikuti[panduan ini](https://www.nuget.org/).
### Lingkungan Pengembangan Terpadu (IDE)
Memiliki IDE seperti Visual Studio atau JetBrains Rider dapat menyederhanakan pengkodean, debugging, dan menjalankan proyek Anda.
### Pengetahuan Dasar C#
Kemampuan dalam pemrograman C# akan sangat bermanfaat dalam mengikuti tutorial ini.
## Paket Impor
Sebelum kita dapat bekerja dengan Aspose.Cells, kita perlu mengimpor paket-paket yang diperlukan ke dalam proyek kita. Berikut ini cara melakukannya:
### Buat Proyek Baru
1. Buka IDE Anda dan buat proyek Aplikasi Konsol baru.
2.  Beri nama proyek Anda sesuatu yang deskriptif, seperti`FontSpecifyingApp`.
### Tambahkan Paket NuGet Aspose.Cells
1. Klik kanan pada proyek Anda di Solution Explorer.
2.  Memilih`Manage NuGet Packages...`.
3.  Pencarian untuk`Aspose.Cells` dan menginstalnya.
Pada akhir langkah-langkah ini, Anda akan memiliki segalanya yang siap untuk memulai pengkodean!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Setelah pengaturan selesai, saatnya menyingsingkan lengan baju dan mulai membuat kode. Secara khusus, kita akan membuat buku kerja Excel baru dan menentukan jenis huruf Timur Jauh dan Latin untuk kotak teks. Berikut cara melakukannya langkah demi langkah:
## Langkah 1: Siapkan Direktori Output
Kita mulai dengan menentukan di mana kita ingin menyimpan berkas Excel kita. Ini penting karena kita ingin memastikan bahwa berkas keluaran kita disimpan di lokasi yang mudah diakses.
```csharp
// Direktori keluaran
string outputDir = "Your Document Directory";
```
## Langkah 2: Buat Buku Kerja Kosong
Sekarang setelah direktori kita siap, mari buat buku kerja baru tempat kita akan menambahkan konten. Ini mirip dengan memulai dengan kanvas baru sebelum melukis.
```csharp
// Membuat buku kerja kosong.
Workbook wb = new Workbook();
```
## Langkah 3: Akses Lembar Kerja Pertama
Berikutnya, kita ingin bekerja dengan lembar kerja dari buku kerja kita. Bayangkan lembar kerja sebagai halaman di buku Anda tempat semua keajaiban terjadi.
```csharp
// Akses lembar kerja pertama.
Worksheet ws = wb.Worksheets[0];
```
## Langkah 4: Tambahkan Kotak Teks
Sekarang, kita akan menambahkan kotak teks ke lembar kerja kita. Di sinilah kita akan mengetik teks kita. Bayangkan ini seperti membuat kotak teks di dalam slide presentasi.
```csharp
// Tambahkan kotak teks di dalam lembar kerja.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Langkah 5: Mengatur Teks Kotak Teks
Mari kita ketik beberapa teks. Dalam contoh ini, kita akan memasukkan karakter Jepang untuk menunjukkan font Timur Jauh. Semudah menulis di kotak teks di komputer Anda!
```csharp
// Mengatur teks kotak teks.
tb.Text = "こんにちは世界"; //Ini berarti "Halo Dunia" dalam bahasa Jepang.
```
## Langkah 6: Tentukan Font
Sekarang tibalah bagian yang menarik! Kita akan mengatur font Latin dan Timur Jauh untuk teksnya. Ini sama seperti memilih font yang sempurna untuk undangan pernikahan yang mewah!
```csharp
// Tentukan nama Timur Jauh dan nama Latin dari font tersebut.
tb.TextOptions.LatinName = "Comic Sans MS"; // Ini adalah font Latin pilihan kami.
tb.TextOptions.FarEastName = "KaiTi"; // Inilah font Timur Jauh yang kami inginkan.
```
## Langkah 7: Simpan File Excel Output
Terakhir, mari kita simpan buku kerja kita! Langkah ini mengakhiri tugas kita dan memastikan bahwa semua kerja keras yang telah kita lakukan tersimpan dengan benar. 
```csharp
// Simpan berkas Excel keluaran.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Langkah 8: Pesan Konfirmasi
Untuk memberi tahu kami bahwa semuanya telah berhasil dijalankan, kami akan mencetak pesan konfirmasi ke konsol:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Kesimpulan
Nah, itu dia! Anda telah berhasil menentukan fon Timur Jauh dan Latin dalam buku kerja Excel menggunakan Aspose.Cells untuk .NET. Keterampilan ini tidak hanya memberikan sentuhan profesional pada dokumen Anda, tetapi juga memperkaya pengalaman membaca bagi pengguna dalam berbagai bahasa.
Jangan ragu untuk bereksperimen dengan berbagai jenis font dan gaya untuk menemukan kombinasi yang sesuai dengan kebutuhan spesifik Anda. Selamat membuat kode!
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET untuk membuat dan mengelola lembar kerja Excel tanpa perlu menginstal Microsoft Excel di komputer Anda. 
### Dapatkah saya menggunakan Aspose.Cells untuk aplikasi web?
Ya! Aspose.Cells dapat digunakan untuk aplikasi desktop dan aplikasi web yang dibangun dengan .NET.
### Apakah ada versi gratis Aspose.Cells?
 Ya, Aspose menawarkan uji coba gratis. Anda dapat[unduh disini](https://releases.aspose.com/).
### Bagaimana cara mendapatkan dukungan untuk Aspose.Cells?
 Anda dapat meminta dukungan dan menemukan sumber daya berharga di[Forum Aspose](https://forum.aspose.com/c/cells/9).
### Di mana saya dapat membeli Aspose.Cells?
 Anda dapat membeli Aspose.Cells langsung dari[Situs web Aspose](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
