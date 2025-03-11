---
title: Dapatkan Dimensi Halaman Lembar Kerja
linktitle: Dapatkan Dimensi Halaman Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mendapatkan dimensi halaman dalam lembar kerja Excel dengan Aspose.Cells for .NET. Panduan langkah demi langkah untuk menyesuaikan ukuran kertas A2, A3, A4, dan Letter.
weight: 13
url: /id/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Dimensi Halaman Lembar Kerja

## Perkenalan
Jika Anda bekerja dengan file Excel secara terprogram menggunakan Aspose.Cells for .NET, mungkin ada saatnya Anda perlu mengakses dan mengatur dimensi halaman lembar kerja. Mengetahui dimensi dapat membantu tata letak, pencetakan, dan kustomisasi lembar Excel untuk tujuan tertentu. Dalam artikel ini, kita akan membahas cara mengambil dan menampilkan berbagai dimensi halaman di Excel menggunakan Aspose.Cells for .NET. Kita akan membahas tutorial langkah demi langkah untuk memastikan Anda memiliki semua detail untuk memulai dengan percaya diri.
## Prasyarat
Sebelum memulai, mari pastikan Anda memiliki semua yang dibutuhkan untuk mengikuti tutorial ini.
1.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal Aspose.Cells untuk .NET. Anda dapat[unduh perpustakaan di sini](https://releases.aspose.com/cells/net/) atau instal melalui NuGet di proyek .NET Anda.
2. Lingkungan .NET: Lingkungan pengembangan .NET yang kompatibel (misalnya, Visual Studio).
3.  Pengaturan Lisensi: Untuk fungsionalitas penuh Aspose.Cells, terapkan lisensi. Anda dapat[meminta lisensi sementara gratis](https://purchase.aspose.com/temporary-license/) untuk tujuan evaluasi.
Mulailah dengan versi uji coba gratis Aspose.Cells jika Anda mengevaluasinya untuk pertama kali.
## Paket Impor
Sebelum kita masuk ke kode, Anda perlu mengimpor namespace Aspose.Cells ke proyek Anda untuk mengakses semua kelas dan metode yang diperlukan.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Mari kita uraikan prosesnya menjadi beberapa langkah mudah. Di sini, kita akan mengakses berbagai ukuran kertas, menerapkannya pada lembar kerja, dan mencetak dimensi untuk masing-masing ukuran.
## Langkah 1: Buat Contoh Buku Kerja
 Langkah pertama adalah membuat instance dari`Workbook` kelas. Objek ini akan bertindak sebagai buku kerja utama yang berisi lembar kerja yang dapat kita manipulasi.
```csharp
Workbook book = new Workbook();
```
 Pikirkanlah`Workbook` sebagai wadah utama untuk berkas Excel Anda. Kita memerlukannya untuk mengakses dan mengontrol lembar kerja individual.
## Langkah 2: Akses Lembar Kerja Pertama
 Selanjutnya, mari kita akses lembar kerja pertama di buku kerja. Secara default, buku kerja baru dilengkapi dengan satu lembar, jadi kita dapat langsung merujuknya menggunakan indeks`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
 Itu`Worksheets` koleksi di`Workbook` memungkinkan kita mengakses setiap lembar kerja berdasarkan indeks. Di sini, kita ambil lembar pertama untuk mulai mengatur dimensi halaman.
## Langkah 3: Atur Ukuran Kertas ke A2 dan Tampilkan Dimensi
Sekarang setelah kita memiliki akses ke lembar kerja kita, mari kita atur ukuran kertasnya ke A2. Pengaturan ukuran kertas berguna untuk memformat halaman sebelum mencetak atau mengekspornya. Setelah kita mengatur ukuran kertas, kita akan mencetak dimensi halaman dalam inci.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
 Di sini, kita mengubah`PaperSize` properti untuk`PaperA2` Setelah mengatur ukuran,`PageSetup.PaperWidth` Dan`PageSetup.PaperHeight` mengambil lebar dan tinggi lembar dalam inci. Ini memberi kita gambaran singkat tentang dimensi halaman.
## Langkah 4: Atur Ukuran Kertas ke A3 dan Tampilkan Dimensi
Dengan mengikuti langkah yang sama seperti di atas, mari sesuaikan dimensi halaman ke ukuran A3. Perubahan ini berguna untuk cetakan yang sedikit lebih besar atau untuk memuat lebih banyak konten pada satu halaman.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Ukuran A3 dua kali lebih besar dari A4, sehingga cocok untuk tabel besar atau diagram terperinci. Mengubah ukuran kertas membantu menyesuaikan tata letak lembar kerja.
## Langkah 5: Atur Ukuran Kertas ke A4 dan Tampilkan Dimensi
Sekarang, mari kita atur ukuran kertas ke A4. Ini adalah ukuran halaman yang paling umum digunakan untuk mencetak dokumen. Kita akan menampilkan dimensi yang diperbarui setelahnya.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Jika target Anda adalah format dokumen standar, A4 biasanya merupakan ukuran yang paling sesuai. Mengetahui dimensi dapat membantu dalam menyesuaikan tata letak konten untuk menghindari masalah pencetakan.
## Langkah 6: Atur Ukuran Kertas ke Letter dan Tampilkan Dimensi
Terakhir, kita akan mengatur ukuran kertas ke format Letter, yang umum digunakan di Amerika Utara. Mari kita cetak dimensinya sekali lagi.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Ukuran Letter banyak digunakan untuk dokumen di Amerika Utara, jadi pengaturan ukuran ini membantu saat berkolaborasi dengan tim atau klien yang berbasis di sana.
## Kesimpulan
Dalam tutorial ini, kami membahas cara mengatur dan mengambil dimensi halaman untuk berbagai ukuran kertas menggunakan Aspose.Cells untuk .NET. Dengan mengonfigurasi ukuran halaman seperti A2, A3, A4, dan Letter, Anda dapat memformat lembar kerja Excel agar sesuai dengan kebutuhan pencetakan dan tata letak tertentu. Kontrol atas dimensi halaman ini sangat berharga untuk pelaporan dan presentasi profesional, karena memastikan konten Anda pas di setiap ukuran halaman.
## Pertanyaan yang Sering Diajukan
### Bagaimana cara mengubah orientasi halaman di Aspose.Cells?  
 Anda dapat mengubah orientasi menggunakan`PageSetup.Orientation` properti, mengaturnya ke`PageOrientationType.Portrait` atau`PageOrientationType.Landscape`.
### Bisakah saya mengatur dimensi halaman khusus di Aspose.Cells?  
 Ya, Anda dapat mengatur dimensi halaman khusus dengan menyesuaikan margin dan opsi skala di bawah`PageSetup` untuk kontrol lebih lanjut.
### Berapa ukuran kertas default di Aspose.Cells?  
Ukuran kertas standar biasanya A4. Namun, ini mungkin bergantung pada pengaturan regional dan dapat disesuaikan sesuai kebutuhan.
### Apakah mungkin untuk melihat pratinjau tata letak halaman di Aspose.Cells?  
Meskipun Aspose.Cells tidak menawarkan pratinjau grafis, Anda dapat mengatur tata letak secara terprogram dan menggunakan pratinjau cetak di Excel.
### Bagaimana cara menginstal Aspose.Cells untuk .NET?  
 Anda dapat menginstal Aspose.Cells menggunakan NuGet Package Manager di Visual Studio atau mengunduh DLL dari[Halaman unduhan Aspose.Cells](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
