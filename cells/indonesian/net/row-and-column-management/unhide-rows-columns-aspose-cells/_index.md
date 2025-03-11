---
title: Menampilkan Baris dan Kolom di Aspose.Cells .NET
linktitle: Menampilkan Baris dan Kolom di Aspose.Cells .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menampilkan kembali baris dan kolom di Excel menggunakan Aspose.Cells for .NET dengan panduan langkah demi langkah kami. Sempurna untuk manipulasi data.
weight: 18
url: /id/net/row-and-column-management/unhide-rows-columns-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menampilkan Baris dan Kolom di Aspose.Cells .NET

## Perkenalan
Saat bekerja dengan file Excel secara terprogram, Anda mungkin menghadapi situasi di mana baris atau kolom tertentu disembunyikan. Hal ini dapat terjadi karena pilihan format, organisasi data, atau sekadar untuk meningkatkan daya tarik visual. Dalam tutorial ini, kita akan membahas cara menampilkan kembali baris dan kolom dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Panduan komprehensif ini akan memandu Anda melalui seluruh proses, memastikan Anda dapat menerapkan konsep-konsep ini dengan percaya diri dalam proyek Anda sendiri. Jadi, mari kita mulai!
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki hal berikut:
1.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells. Anda bisa mendapatkannya dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: Lingkungan pengembangan kerja tempat Anda dapat membuat proyek C# baru.
3. Pengetahuan Dasar C#: Pemahaman terhadap konsep pemrograman C# akan sangat membantu, namun jangan khawatir jika Anda seorang pemula; kami akan menjelaskan semuanya dengan istilah yang sederhana.
## Paket Impor
Untuk menggunakan Aspose.Cells dalam proyek Anda, Anda perlu mengimpor paket yang diperlukan. Berikut cara melakukannya:
### Buat Proyek Baru
1. Buka Visual Studio dan buat proyek C# baru.
2. Pilih jenis proyek (misalnya, Aplikasi Konsol) dan klik Buat.
### Tambahkan Referensi Aspose.Cells
1. Klik kanan pada folder Referensi di proyek Anda.
2. Pilih Kelola Paket NuGet.
3. Cari Aspose.Cells dan instal. Langkah ini memungkinkan Anda memanfaatkan fungsionalitas yang disediakan oleh pustaka Aspose.Cells.
### Impor Namespace yang Diperlukan
Di bagian atas file C# Anda, tambahkan perintah using berikut untuk mengimpor namespace Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
```
Sekarang setelah lingkungan kita disiapkan, mari beralih ke panduan langkah demi langkah untuk menampilkan kembali baris dan kolom dalam berkas Excel.
## Langkah 1: Siapkan Direktori Dokumen Anda
Sebelum Anda mulai bekerja dengan berkas Excel, Anda perlu menentukan jalur ke direktori tempat dokumen Anda disimpan. Di sinilah Anda akan membaca berkas Excel dan menyimpan versi yang dimodifikasi. Berikut cara mengaturnya:
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Tip: Ganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Excel Anda berada. Misalnya,`C:\Documents\`.
## Langkah 2: Buat Aliran File
Selanjutnya, Anda akan membuat aliran file untuk mengakses file Excel Anda. Ini memungkinkan Anda untuk membuka dan memanipulasi file tersebut secara terprogram.
```csharp
// Membuat aliran file yang berisi file Excel yang akan dibuka
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Pada langkah ini, ganti`"book1.xls"` dengan nama berkas Excel Anda. Ini akan memungkinkan aplikasi untuk membaca data yang terdapat dalam berkas tersebut.
## Langkah 3: Buat Instansiasi Objek Buku Kerja
 Sekarang saatnya untuk membuat`Workbook` objek yang akan mewakili berkas Excel Anda di memori. Ini penting untuk melakukan operasi apa pun pada berkas tersebut.
```csharp
// Membuat instance objek Buku Kerja
// Membuka file Excel melalui aliran file
Workbook workbook = new Workbook(fstream);
```
 Itu`Workbook` Objek merupakan gerbang menuju konten berkas Excel, yang memungkinkan Anda memodifikasinya sesuai kebutuhan.
## Langkah 4: Akses Lembar Kerja
 Setelah Anda memiliki`Workbook` objek, Anda perlu mengakses lembar kerja tertentu yang ingin Anda ubah. Dalam contoh ini, kita akan bekerja dengan lembar kerja pertama dalam buku kerja.
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Indeks`[0]`merujuk ke lembar kerja pertama. Jika Anda ingin mengakses lembar kerja lain, cukup ubah indeksnya.
## Langkah 5: Tampilkan Baris
Setelah lembar kerja diakses, Anda sekarang dapat menampilkan kembali baris yang tersembunyi. Berikut cara menampilkan kembali baris ketiga dan mengatur tingginya:
```csharp
// Menampilkan baris ke-3 dan mengatur tingginya menjadi 13,5
worksheet.Cells.UnhideRow(2, 13.5);
```
 Pada kode di atas,`2` mengacu pada indeks baris (ingat, ini berbasis nol), dan`13.5` mengatur tinggi baris tersebut. Sesuaikan nilai ini sesuai kebutuhan untuk kasus spesifik Anda.
## Langkah 6: Tampilkan Kolom
Demikian pula, jika Anda ingin menampakkan kembali kolom, Anda dapat melakukannya dengan mengikuti metode ini. Berikut cara menampakkan kembali kolom kedua dan mengatur lebarnya:
```csharp
// Menampilkan kolom ke-2 dan mengatur lebarnya menjadi 8,5
worksheet.Cells.UnhideColumn(1, 8.5);
```
 Lagi,`1` adalah indeks berbasis nol untuk kolom, dan`8.5` menentukan lebar kolom tersebut. Ubah parameter ini berdasarkan kebutuhan Anda.
## Langkah 7: Simpan File Excel yang Telah Dimodifikasi
Setelah melakukan perubahan yang diperlukan, Anda perlu menyimpan berkas Excel yang telah dimodifikasi. Ini memastikan bahwa tindakan menampilkan kembali baris dan kolom akan berhasil.
```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(dataDir + "output.xls");
```
 Di Sini,`output.xls` adalah nama berkas yang ingin Anda gunakan untuk menyimpan konten yang dimodifikasi. Anda dapat memilih nama apa pun yang Anda suka, tetapi pastikan nama tersebut memiliki`.xls` perpanjangan.
## Langkah 8: Tutup Aliran File
Terakhir, penting untuk menutup aliran file guna membebaskan sumber daya sistem. Ini mencegah potensi kebocoran memori atau penguncian file.
```csharp
// Menutup aliran file untuk membebaskan semua sumber daya
fstream.Close();
```
Selesai! Anda telah berhasil menampilkan kembali baris dan kolom dalam file Excel menggunakan Aspose.Cells for .NET.
## Kesimpulan
Dalam tutorial ini, kami telah membahas langkah-langkah untuk menampakkan kembali baris dan kolom dalam file Excel menggunakan Aspose.Cells for .NET. Pustaka ini memudahkan Anda untuk memanipulasi dokumen Excel secara terprogram, sehingga meningkatkan kemampuan Anda untuk mengelola data secara efisien. Baik Anda memperbarui lembar kerja untuk laporan atau menjaga integritas data, mengetahui cara menampakkan kembali baris dan kolom dapat sangat berguna.
## Pertanyaan yang Sering Diajukan
### Bisakah saya menampilkan kembali beberapa baris dan kolom sekaligus?  
Ya, Anda dapat menampilkan kembali beberapa baris dan kolom dengan mengulangi indeks dan menerapkan`UnhideRow` Dan`UnhideColumn` metode yang sesuai.
### Format file apa yang didukung Aspose.Cells?  
Aspose.Cells mendukung berbagai format termasuk XLS, XLSX, CSV, dan masih banyak lagi. Anda dapat membaca dan menulis format ini dengan lancar.
### Apakah ada uji coba gratis yang tersedia untuk Aspose.Cells?  
 Tentu saja! Anda dapat mengunduh versi uji coba gratis dari[Situs web Aspose](https://releases.aspose.com/).
### Bagaimana cara mengatur tinggi yang berbeda untuk beberapa baris?  
Anda dapat menampilkan beberapa baris dalam satu loop, dengan menentukan tinggi yang berbeda sesuai kebutuhan. Ingatlah untuk menyesuaikan indeks baris dalam loop Anda.
### Apa yang harus saya lakukan jika saya menemui kesalahan saat bekerja dengan file Excel?  
Jika Anda mengalami masalah, periksa pesan kesalahan untuk mendapatkan petunjuk. Anda juga dapat mencari bantuan dari forum dukungan Aspose untuk mengatasi masalah.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
