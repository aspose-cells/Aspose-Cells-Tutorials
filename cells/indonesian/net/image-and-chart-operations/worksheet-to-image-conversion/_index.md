---
title: Konversi Lembar Kerja ke Gambar dalam .NET
linktitle: Konversi Lembar Kerja ke Gambar dalam .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengonversi lembar kerja Excel ke gambar dalam .NET menggunakan Aspose.Cells dengan panduan langkah demi langkah kami. Sederhanakan visualisasi data Anda.
weight: 11
url: /id/net/image-and-chart-operations/worksheet-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konversi Lembar Kerja ke Gambar dalam .NET

## Perkenalan
Jika berbicara tentang memanipulasi file Excel di .NET, Aspose.Cells menonjol sebagai pustaka yang andal dan tangguh. Salah satu tugas yang sering Anda hadapi adalah mengonversi lembar kerja Excel menjadi gambar. Apakah Anda ingin menampilkan lembar kerja di halaman web, menyertakannya dalam laporan, atau sekadar membagikan data secara visual, panduan langkah demi langkah ini akan memandu Anda melalui seluruh proses. Pada akhirnya, Anda akan dilengkapi dengan semua yang Anda butuhkan untuk mengonversi lembar kerja menjadi gambar dengan mudah. Jadi, mari kita mulai!
## Prasyarat
Sebelum memulai konversi, penting untuk memastikan Anda telah menyiapkan semuanya dengan benar. Berikut ini adalah prasyarat yang Anda perlukan:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Ini adalah IDE yang akan membantu Anda menjalankan proyek .NET dengan lancar.
2.  Pustaka Aspose.Cells untuk .NET: Anda perlu memperoleh pustaka ini. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/) atau mulai dengan[uji coba gratis](https://releases.aspose.com/).
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan bermanfaat, karena contoh dan penjelasan kami akan ditulis dalam bahasa ini.
4.  Contoh File Excel: Untuk demonstrasi, buat atau unduh file Excel. Simpan sebagai`MyTestBook1.xls` di direktori proyek Anda.
5. Pemahaman Dasar tentang Proyek .NET: Mengetahui cara membuat proyek .NET sederhana akan mempermudah hal ini, tetapi jangan khawatir—kami akan memandu Anda melalui langkah-langkahnya.
## Paket Impor
Langkah pertama dalam perjalanan kita adalah mengimpor paket Aspose.Cells yang diperlukan ke dalam proyek kita. Ini penting karena memungkinkan kita untuk memanfaatkan semua fungsi yang ditawarkan Aspose.Cells.
## Langkah 1: Buat Proyek Baru 
Untuk memulai, buat proyek .NET baru di Visual Studio:
- Buka Visual Studio.
- Klik "Buat proyek baru."
- Pilih “Aplikasi Konsol (.NET Framework)” atau “Aplikasi Konsol (.NET Core)” tergantung pada preferensi Anda.
- Beri nama proyek Anda (misalnya, WorksheetToImage) dan klik “Buat.”
## Langkah 2: Tambahkan Referensi Aspose.Cells
Sekarang setelah kita memiliki proyek kita, kita perlu menambahkan Aspose.Cells:
- Klik kanan pada proyek Anda di Solution Explorer.
- Pilih “Kelola Paket NuGet.”
- Cari “Aspose.Cells” dan instal versi terbaru.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
Anda sudah siap untuk bagian pengkodean!

Sekarang, mari kita bahas proses konversi yang sebenarnya langkah demi langkah. Kita akan menggunakan program C# sederhana yang membuka file Excel, mengonversi lembar kerja menjadi gambar, dan menyimpan gambar tersebut ke direktori tertentu.
## Langkah 3: Menyiapkan Lingkungan
Pertama, atur lingkungan Anda dengan menentukan jalur ke direktori dokumen Anda:
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Di sini, kita mendefinisikan variabel yang disebut`dataDir` yang menyimpan jalur ke direktori tempat file kita akan disimpan. Ganti`"Your Document Directory"` dengan jalur sebenarnya pada sistem Anda (misalnya, "C:\\File Saya\").
## Langkah 4: Buka Buku Kerja Excel
 Selanjutnya kita akan membuka file Excel menggunakan`Workbook` kelas dari Aspose.Cells:
```csharp
// Buka file Excel templat.
Workbook book = new Workbook(dataDir + "MyTestBook1.xls");
```
 Pada langkah ini, kita membuat sebuah instance dari`Workbook` class dan meneruskan jalur ke berkas Excel kita. Ini memungkinkan kita berinteraksi dengan konten berkas secara terprogram.
## Langkah 5: Mengakses Lembar Kerja
Sekarang setelah buku kerja kita terbuka, mari mengakses lembar kerja pertama:
```csharp
// Dapatkan lembar kerja pertama.
Worksheet sheet = book.Worksheets[0];
```
 Di sini, kita mengambil lembar kerja pertama (indeks`0` dari buku kerja. Array Aspose.Cells diindeks nol, yang berarti lembar pertama adalah`0`.
## Langkah 6: Tentukan Opsi Gambar atau Cetak
 Sebelum kita merender gambar, kita perlu menentukan bagaimana kita ingin gambar tersebut terlihat menggunakan`ImageOrPrintOptions`:
```csharp
// Tentukan ImageOrPrintOptions
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
// Tentukan format gambar
imgOptions.ImageType = Drawing.ImageType.Jpeg;
// Hanya satu halaman untuk seluruh lembar yang akan ditampilkan
imgOptions.OnePagePerSheet = true;
```
 Pada langkah ini, kita membuat sebuah instance dari`ImageOrPrintOptions` Kami menentukan bahwa kami ingin menyimpan output sebagai gambar JPEG dan mengatur`OnePagePerSheet` ke`true` untuk memastikan seluruh lembar tertangkap dalam satu gambar.
## Langkah 7: Merender Lembar Kerja
Dengan opsi yang ada, kita sekarang dapat merender lembar kerja:
```csharp
// Render lembar sesuai dengan pilihan gambar/cetak yang ditentukan
SheetRender sr = new SheetRender(sheet, imgOptions);
// Render gambar untuk lembar tersebut
Bitmap bitmap = sr.ToImage(0);
```
 Itu`SheetRender` kelas membantu merender lembar kerja menjadi gambar bitmap. Kami menyebutnya`ToImage(0)` untuk merender halaman ke nol (lembar pertama kita) menjadi bitmap.
## Langkah 8: Menyimpan Gambar
Setelah melakukan rendering, kita perlu menyimpan gambar ke direktori yang ditentukan:
```csharp
//Simpan berkas gambar dengan menentukan format gambarnya.
bitmap.Save(dataDir + "SheetImage.out.jpg");
```
 Di sini, kita menyimpan gambar bitmap yang kita buat. Baris ini menulis gambar ke`dataDir` lokasi dengan nama file`SheetImage.out.jpg`.
## Langkah 9: Pemberitahuan Penyelesaian
Untuk memastikan prosesnya selesai, mari tambahkan pesan konsol sederhana:
```csharp
// Menampilkan hasil, sehingga pengguna mengetahui pemrosesan telah selesai.
System.Console.WriteLine("Conversion to Image(s) completed.");
```
Baris ini menampilkan pesan konfirmasi ke konsol, yang memberi tahu pengguna bahwa konversi berhasil.
## Kesimpulan
Nah, itu dia! Hanya dalam beberapa langkah sederhana, Anda telah mempelajari cara mengonversi lembar kerja Excel menjadi gambar menggunakan Aspose.Cells for .NET. Proses ini tidak hanya cepat tetapi juga hebat, memungkinkan Anda membuat representasi visual data spreadsheet dengan mudah.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat, memanipulasi, mengonversi, dan memproses file Excel secara terprogram.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Anda dapat mulai menggunakan Aspose.Cells dengan mengunduh uji coba gratis dari mereka[situs web](https://releases.aspose.com/).
### Format gambar apa yang didukung Aspose.Cells untuk ekspor?
Aspose.Cells mendukung berbagai format gambar, termasuk JPEG, PNG, BMP, dan GIF.
### Di mana saya dapat menemukan dukungan tambahan untuk Aspose.Cells?
 Anda dapat mengakses forum dukungan untuk Aspose.Cells[Di Sini](https://forum.aspose.com/c/cells/9).
### Bagaimana cara mendapatkan lisensi sementara untuk Aspose.Cells?
 Lisensi sementara dapat diperoleh dengan mengunjungi[halaman lisensi sementara](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
