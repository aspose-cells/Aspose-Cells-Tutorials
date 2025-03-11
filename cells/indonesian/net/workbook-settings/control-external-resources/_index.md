---
title: Kontrol Sumber Daya Eksternal menggunakan Pengaturan Buku Kerja
linktitle: Kontrol Sumber Daya Eksternal menggunakan Pengaturan Buku Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengontrol sumber daya eksternal di Excel menggunakan Aspose.Cells untuk .NET dengan tutorial langkah demi langkah kami yang komprehensif.
weight: 10
url: /id/net/workbook-settings/control-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kontrol Sumber Daya Eksternal menggunakan Pengaturan Buku Kerja

## Perkenalan
Dalam ranah manipulasi dan penyajian data, penanganan sumber daya eksternal secara efisien dapat menjadi pengubah permainan. Jika Anda bekerja dengan file Excel dan ingin mengelola sumber daya eksternal dengan lancar menggunakan Aspose.Cells for .NET, Anda telah tiba di tempat yang tepat! Dalam artikel ini, kita akan menyelami secara mendalam pengendalian sumber daya eksternal saat bekerja dengan buku kerja Excel. Di akhir panduan ini, Anda akan dapat menerapkan solusi khusus untuk memuat gambar dan data dari sumber eksternal dengan mudah.
## Prasyarat
Sebelum kita masuk ke inti coding, ada beberapa prasyarat yang perlu Anda penuhi. Pastikan Anda:
1. Memiliki Visual Studio: Anda memerlukan IDE untuk menulis dan menguji aplikasi .NET Anda. Visual Studio adalah pilihan yang paling direkomendasikan karena dukungannya yang luas dan kemudahan penggunaannya.
2.  Unduh Aspose.Cells untuk .NET: Jika Anda belum melakukannya, ambil pustaka Aspose.Cells dari[tautan unduhan](https://releases.aspose.com/cells/net/). 
3. Pemahaman Dasar tentang C#: Keakraban dengan konsep C# dan .NET framework akan membuat proses lebih lancar bagi Anda.
4. Siapkan Lingkungan Anda: Pastikan proyek Anda merujuk ke pustaka Aspose.Cells. Anda dapat melakukannya melalui NuGet Package Manager dalam Visual Studio.
5. File Contoh: Siapkan file Excel contoh yang menyertakan sumber daya eksternal, seperti gambar yang ditautkan. File ini akan membantu mendemonstrasikan fungsionalitas yang kita bahas.
Setelah Anda menyiapkannya, Anda siap untuk mengendalikan sumber daya eksternal dengan Aspose.Cells.
## Paket Impor
Untuk memulai pengkodean, Anda perlu mengimpor paket yang diperlukan ke dalam berkas C# Anda. Berikut ini yang Anda perlukan:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Ruang nama ini menyediakan akses ke fungsionalitas yang diperlukan untuk memanipulasi berkas Excel dan menangani gambar.
 Mari kita uraikan menjadi langkah-langkah yang dapat dikelola untuk membantu Anda mengendalikan sumber daya eksternal menggunakan`Workbook Settings`. Kami akan memandu Anda membuat penyedia aliran kustom, memuat file Excel, dan merender lembar kerja menjadi gambar. Silakan ikuti!
## Langkah 1: Tentukan Direktori Sumber dan Output
Untuk memulai, kita perlu menentukan direktori tempat kita akan membaca file dan tempat kita akan menyimpan output. Sangat penting untuk menetapkan jalur yang benar guna menghindari kesalahan file tidak ditemukan.
```csharp
// Direktori sumber
static string sourceDir = "Your Document Directory";
// Direktori keluaran
static string outputDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Anda berada.
## Langkah 2: Terapkan Antarmuka IStreamProvider
 Selanjutnya, kita akan membuat kelas khusus yang mengimplementasikan`IStreamProvider` antarmuka. Kelas ini akan mengelola cara mengakses sumber daya eksternal (seperti gambar).
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // Bersihkan semua sumber daya jika perlu
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Buka aliran file sumber daya eksternal
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
 Di dalam`InitStream` metode, kami membuka file yang bertindak sebagai sumber daya eksternal kami dan menetapkannya ke`Stream`properti. Ini mengizinkan buku kerja untuk mengakses sumber daya saat melakukan rendering.
## Langkah 3: Muat File Excel
Sekarang setelah penyedia aliran kita siap, mari muat buku kerja Excel yang berisi sumber daya eksternal.
```csharp
public static void Run()
{
    // Muat contoh file Excel
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Berikan implementasi IStreamProvider Anda
    wb.Settings.StreamProvider = new SP();
```
 Dalam cuplikan ini, kami memuat file Excel kami dan menetapkan kustom kami`StreamProvider` implementasi untuk menangani sumber daya eksternal.
## Langkah 4: Akses Lembar Kerja
Setelah memuat buku kerja, kita dapat dengan mudah mengakses lembar kerja yang diinginkan. Mari kita ambil yang pertama.
```csharp
    // Akses lembar kerja pertama
    Worksheet ws = wb.Worksheets[0];
```
Mudah saja, bukan? Anda dapat mengakses lembar kerja apa pun dengan menentukan indeksnya.
## Langkah 5: Konfigurasikan Opsi Gambar atau Cetak
Sekarang kita akan menentukan tampilan gambar keluaran yang kita inginkan. Kita akan mengonfigurasi opsi seperti memastikan bahwa ada satu halaman untuk setiap lembar dan menentukan jenis gambar keluaran.
```csharp
    // Tentukan pilihan gambar atau cetak
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Memilih PNG sebagai format keluaran memastikan kualitasnya tetap tajam dan jernih!
## Langkah 6: Render Lembar Kerja ke Gambar
Setelah semuanya siap, mari kita ubah lembar kerja pilihan kita menjadi berkas gambar! Inilah bagian yang menarik; Anda akan melihat lembar Excel Anda berubah menjadi gambar yang indah.
```csharp
    // Buat render lembar dengan meneruskan parameter yang diperlukan
    SheetRender sr = new SheetRender(ws, opts);
    // Ubah seluruh lembar kerja Anda menjadi gambar png
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
 Itu`ToImage` Fungsi ini melakukan semua pekerjaan berat, mengubah lembar menjadi gambar. Setelah langkah ini selesai, Anda akan menemukan gambar tersimpan di direktori keluaran Anda.
## Kesimpulan
Nah, itu dia! Kini Anda memiliki pengetahuan untuk mengendalikan sumber daya eksternal saat bekerja dengan file Excel menggunakan Aspose.Cells di .NET. Ini tidak hanya meningkatkan kemampuan aplikasi Anda, tetapi juga membuat penanganan kumpulan data dan presentasi menjadi mudah. Dengan mengikuti langkah-langkah yang diberikan, Anda dapat dengan mudah meniru dan mengadaptasi fungsionalitas ini agar sesuai dengan kebutuhan spesifik proyek Anda.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka hebat yang dirancang untuk pengembang C# dan .NET untuk membuat, memanipulasi, dan mengelola file Excel tanpa perlu menginstal Microsoft Excel.
### Bagaimana cara mengunduh Aspose.Cells untuk .NET?
 Anda dapat mengunduhnya dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
### Apakah ada uji coba gratis yang tersedia?
 Ya! Anda dapat mengakses uji coba gratis Aspose.Cells dari[halaman rilis](https://releases.aspose.com/).
### Jenis file apa yang didukung Aspose.Cells?
Aspose.Cells mendukung berbagai format Excel, termasuk XLS, XLSX, CSV, dan banyak lagi.
### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?
 Anda dapat mengunjungi forum dukungan Aspose di[Forum Aspose](https://forum.aspose.com/c/cells/9) untuk bantuan.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
