---
title: Kirim Bentuk Depan atau Belakang di Excel
linktitle: Kirim Bentuk Depan atau Belakang di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara mengirim bentuk ke depan atau belakang di Excel menggunakan Aspose.Cells untuk .NET. Panduan ini menyediakan tutorial langkah demi langkah dengan kiat-kiat.
weight: 16
url: /id/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kirim Bentuk Depan atau Belakang di Excel

## Perkenalan
Saat bekerja dengan file Excel, Anda mungkin merasa perlu lebih banyak kontrol atas elemen visual dalam lembar kerja Anda. Bentuk, seperti gambar dan grafik, dapat menyempurnakan penyajian data Anda. Namun, apa yang terjadi jika bentuk-bentuk ini tumpang tindih atau perlu disusun ulang? Di sinilah Aspose.Cells for .NET berperan. Dalam tutorial ini, kami akan memandu Anda melalui langkah-langkah untuk memanipulasi bentuk dalam lembar kerja Excel, khususnya dengan menempatkan bentuk di bagian depan atau belakang bentuk lain. Jika Anda siap untuk meningkatkan kemampuan Excel Anda, mari langsung mulai!
## Prasyarat
Sebelum kita memulai, Anda perlu menyiapkan beberapa hal:
1.  Pemasangan Pustaka Aspose.Cells: Pastikan Anda telah memasang pustaka Aspose.Cells untuk .NET. Anda dapat menemukannya[Di Sini](https://releases.aspose.com/cells/net/).
2. Lingkungan Pengembangan: Pastikan Anda memiliki lingkungan pengembangan yang disiapkan dengan dukungan .NET, seperti Visual Studio.
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
Baiklah, Anda sudah memenuhi semua persyaratan di daftar prasyarat? Bagus! Mari kita lanjut ke bagian yang menyenangkan – menulis kode!
## Paket Impor
Sebelum kita menyelami pengkodean yang sebenarnya, mari impor paket-paket yang diperlukan. Cukup tambahkan perintah berikut di bagian atas berkas C# Anda:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Ruang nama ini penting karena berisi kelas dan metode yang akan kita gunakan untuk memanipulasi file dan bentuk Excel.
## Langkah 1: Tentukan Jalur File Anda
Pada langkah pertama ini, kita perlu membuat direktori sumber dan keluaran. Di sinilah berkas Excel Anda berada dan tempat Anda ingin menyimpan berkas yang dimodifikasi.
```csharp
//Direktori sumber
string sourceDir = "Your Document Directory";
//Direktori keluaran
string outputDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Excel Anda disimpan.
## Langkah 2: Muat Buku Kerja
Sekarang setelah kita menetapkan direktori, mari muat buku kerja (file Excel) yang berisi bentuk yang ingin kita manipulasi.
```csharp
//Muat file Excel sumber
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Baris kode ini menginisialisasi yang baru`Workbook` objek, memuat file Excel yang ditentukan ke dalam memori sehingga kita dapat bekerja dengannya.
## Langkah 3: Akses Lembar Kerja 
Selanjutnya, kita perlu mengakses lembar kerja tertentu tempat bentuk kita berada. Untuk contoh ini, kita akan menggunakan lembar kerja pertama.
```csharp
//Akses lembar kerja pertama
Worksheet ws = wb.Worksheets[0];
```
 Dengan merujuk`Worksheets[0]`, kami menargetkan lembar pertama buku kerja kami. Jika bentuk Anda berada di lembar yang berbeda, sesuaikan indeksnya.
## Langkah 4: Akses Bentuknya
Setelah lembar kerja siap diakses, mari ambil bentuk yang kita minati. Untuk contoh ini, kita akan mengakses bentuk pertama dan keempat.
```csharp
//Akses bentuk pertama dan keempat
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Garis-garis ini mendapatkan bentuk spesifik dari lembar kerja berdasarkan indeksnya.
## Langkah 5: Cetak Posisi Urutan Z Bentuk
Sebelum kita memindahkan bentuk apa pun, mari cetak posisi Z-Order-nya saat ini. Ini membantu kita melacak posisinya sebelum kita membuat perubahan.
```csharp
//Cetak posisi Z-Order dari bentuk tersebut
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 Dengan menyebut`ZOrderPosition`, kita dapat melihat posisi setiap bentuk dalam urutan gambar.
## Langkah 6: Kirim Bentuk Pertama ke Depan
Sekarang saatnya beraksi! Mari kita kirim bentuk pertama ke bagian depan Z-Order.
```csharp
//Kirim bentuk ini ke depan
sh1.ToFrontOrBack(2);
```
 Dengan melewati`2` ke`ToFrontOrBack`, kami memerintahkan Aspose.Cells untuk membawa bentuk ini ke depan. 
## Langkah 7: Cetak Posisi Z-Order dari Bentuk Kedua
Sebelum kita mengirim bentuk kedua ke belakang, mari periksa di mana posisinya.
```csharp
//Cetak posisi Z-Order dari bentuk tersebut
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Ini memberi kita wawasan tentang posisi bentuk keempat sebelum kita membuat perubahan apa pun.
## Langkah 8: Kirim Bentuk Keempat ke Belakang
Terakhir, kita akan mengirim bentuk keempat ke bagian belakang tumpukan Z-Order.
```csharp
//Kirim bentuk ini ke belakang
sh4.ToFrontOrBack(-2);
```
 Menggunakan`-2` karena parameter mengirimkan bentuk ke bagian belakang tumpukan, memastikannya tidak akan menghalangi bentuk atau teks lainnya.
## Langkah 9: Simpan Buku Kerja 
Langkah terakhir adalah menyimpan buku kerja Anda dengan bentuk yang baru diposisikan.
```csharp
//Simpan file Excel keluaran
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Perintah ini menyimpan buku kerja yang dimodifikasi ke direktori keluaran yang ditentukan.
## Langkah 10: Pesan Konfirmasi
Terakhir, mari berikan konfirmasi sederhana untuk memberi tahu kami bahwa tugas kami berhasil diselesaikan.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Dan itu merangkum kode untuk tutorial kita!
## Kesimpulan
Memanipulasi bentuk di Excel menggunakan Aspose.Cells for .NET tidak hanya mudah tetapi juga hebat. Dengan mengikuti panduan ini, Anda sekarang dapat mengirim bentuk ke depan atau belakang dengan mudah, yang memungkinkan kontrol yang lebih baik atas presentasi Excel Anda. Dengan alat-alat ini, Anda siap untuk meningkatkan daya tarik visual spreadsheet Anda.
## Pertanyaan yang Sering Diajukan
### Bahasa pemrograman apa yang saya perlukan untuk Aspose.Cells?  
Anda perlu menggunakan C# atau bahasa apa pun yang mendukung .NET untuk bekerja dengan Aspose.Cells.
### Dapatkah saya mencoba Aspose.Cells secara gratis?  
 Ya, Anda dapat memulai dengan uji coba gratis Aspose.Cells[Di Sini](https://releases.aspose.com/).
### Bentuk apa saja yang dapat saya manipulasi di Excel?  
Anda dapat memanipulasi berbagai bentuk seperti persegi panjang, lingkaran, garis, dan gambar.
### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.Cells?  
 Anda dapat mengunjungi forum komunitas mereka untuk dukungan atau pertanyaan apa pun[Di Sini](https://forum.aspose.com/c/cells/9).
### Apakah ada lisensi sementara yang tersedia untuk Aspose.Cells?  
 Ya, Anda dapat meminta lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
