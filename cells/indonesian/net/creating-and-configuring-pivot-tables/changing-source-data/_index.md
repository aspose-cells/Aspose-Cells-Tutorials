---
title: Mengubah Sumber Data Tabel Pivot Secara Terprogram di .NET
linktitle: Mengubah Sumber Data Tabel Pivot Secara Terprogram di .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengubah data sumber tabel pivot secara terprogram menggunakan Aspose.Cells untuk .NET dengan tutorial langkah demi langkah kami yang komprehensif.
weight: 10
url: /id/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengubah Sumber Data Tabel Pivot Secara Terprogram di .NET

## Perkenalan
Dalam dunia analisis data, hanya sedikit alat yang sehebat Microsoft Excel. Setiap hari, banyak sekali pengguna yang bergantung pada Excel untuk mengelola dan menganalisis data, tetapi di balik layar, Excel jauh lebih rumit daripada sekadar mengeklik dan menyeret. Jika Anda pernah ingin memanipulasi file Excel secara terprogram—khususnya, untuk mengubah data sumber tabel pivot—Anda berada di tempat yang tepat! Dalam panduan ini, kami akan membahas cara melakukannya menggunakan Aspose.Cells untuk .NET. Baik Anda seorang pengembang berpengalaman atau baru saja terjun ke dunia pemrograman, Anda akan menemukan tutorial ini yang berisi informasi berharga yang mudah diikuti.
## Prasyarat
Sebelum kita memulai perjalanan mengubah data sumber tabel pivot, mari pastikan Anda telah menyiapkan semuanya dan siap untuk melakukannya:
1. Visual Studio: Pastikan Anda telah menginstal salinan Microsoft Visual Studio, karena kita akan menulis kode di sini.
2. Pustaka Aspose.Cells: Anda harus mengunduh dan merujuk pustaka Aspose.Cells ke dalam proyek Anda. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Meskipun tutorial ini disederhanakan, pemahaman tentang C# akan membantu Anda lebih memahami kodenya.
4. File Excel: Anda harus memiliki contoh file Excel (seperti "Book1.xlsx") yang berisi tabel pivot yang dapat kita manipulasi.
Baiklah, jika prasyarat ini terpenuhi, kita dapat melanjutkan mengimpor paket yang diperlukan dan mulai mengode!
## Paket Impor
Hal pertama yang harus dilakukan—mari impor paket yang kita perlukan. Buka proyek C# Anda di Visual Studio dan tambahkan perintah berikut di bagian atas berkas kode Anda:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Ruang nama ini akan memberi Anda akses ke kelas-kelas penting yang dibutuhkan untuk bekerja dengan file Excel dan memanipulasi kontennya menggunakan Aspose.Cells.

Sekarang, mari kita uraikan prosesnya menjadi beberapa langkah yang mudah dikelola. Kita akan membahas cara membuka file Excel, memodifikasi lembar kerja, mengubah sumber data tabel pivot, dan menyimpan hasilnya.
## Langkah 1: Tentukan Direktori Dokumen Anda
 Pertama, Anda perlu menentukan di mana file Excel Anda berada. Ubah`dataDir` variabel untuk menunjuk ke folder yang berisi "Book1.xlsx" Anda.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
Baris ini mengatur direktori tempat berkas Excel Anda disimpan, membuatnya lebih mudah diakses nanti.
## Langkah 2: Tentukan Jalur Input
Berikutnya, mari buat string untuk menentukan jalur lengkap ke file Excel input Anda:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Ini membantu dalam memperlancar akses berkas Anda; Anda tidak perlu terus-menerus mengetik jalur yang sama beberapa kali di seluruh kode Anda.
## Langkah 3: Buat Aliran File
 Sekarang saatnya untuk membuka file Excel. Kita akan membuat`FileStream` yang memungkinkan Anda membaca konten file Excel:
```csharp
// Membuat aliran file yang berisi file Excel yang akan dibuka
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Baris ini membuka berkas dalam mode baca, yang memungkinkan kita mengakses datanya.
## Langkah 4: Muat Buku Kerja
Setelah aliran file tersedia, langkah berikutnya adalah memuat buku kerja:
```csharp
// Membuka file Excel melalui aliran file
Workbook workbook = new Workbook(fstream);
```
 Perintah ini mengambil file Excel Anda dan memuatnya ke dalam`Workbook` objek. Setelah dimuat, Anda dapat memanipulasi berkas sesuai kebutuhan.
## Langkah 5: Akses Lembar Kerja
Saatnya menyelami hal-hal spesifik. Kita akan mengakses lembar kerja pertama dalam buku kerja:
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Ini memberi Anda akses langsung ke data dalam lembar kerja pertama, sehingga memudahkan modifikasi.
## Langkah 6: Mengisi Data Baru
Selanjutnya, kita ingin memasukkan data baru ke dalam sel. Dalam contoh ini, kita akan menambahkan beberapa contoh data:
```csharp
// Mengisi data baru ke sel lembar kerja
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Di sini, kami memasukkan nilai "Golf", "Qtr4", dan`7000` ke dalam sel tertentu. Anda dapat mengubah nilai ini sesuai kebutuhan Anda.
## Langkah 7: Ubah Rentang Bernama
Sekarang, kita akan mengubah rentang bernama yang dirujuk oleh tabel pivot. Ini melibatkan pembuatan atau pembaruan rentang:
```csharp
// Mengubah rentang bernama "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Dengan mendefinisikan rentang baru, kami memastikan bahwa tabel pivot menggunakan data baru ini saat diperbarui.
## Langkah 8: Simpan File Excel yang Dimodifikasi
Setelah semua perubahan dilakukan, sangat penting untuk menyimpan pekerjaan Anda! Mari kita simpan buku kerja yang dimodifikasi:
```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(dataDir + "output.xls");
```
Perintah ini menyimpan buku kerja ke berkas baru, jadi Anda tidak perlu menimpa berkas asli kecuali Anda menginginkannya!
## Langkah 9: Tutup Aliran File
Terakhir, penting untuk menutup aliran file untuk melepaskan sumber daya apa pun yang Anda gunakan:
```csharp
// Menutup aliran file untuk membebaskan semua sumber daya
fstream.Close();
```
Langkah ini memastikan bahwa aplikasi Anda tidak mengalami kebocoran memori dan tetap efisien.
## Kesimpulan
Selamat! Anda baru saja berhasil mengubah data sumber tabel pivot secara terprogram di .NET menggunakan Aspose.Cells. Fungsionalitas ini membuka banyak kemungkinan untuk mengotomatiskan tugas Excel dan meningkatkan alur kerja Anda. Baik Anda memperbarui laporan keuangan, melacak data penjualan, atau bahkan sekadar bermain-main dengan kumpulan data, memiliki kemampuan untuk melakukan ini secara terprogram dapat menghemat banyak waktu dan mengurangi risiko kesalahan.

## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang canggih untuk bekerja dengan berkas Excel, yang memungkinkan pengguna untuk membuat, memodifikasi, dan memanipulasi dokumen Excel secara terprogram.
### Bisakah saya mengubah sumber data tabel pivot yang ada menggunakan metode ini?
Tentu saja! Metode ini memungkinkan Anda memperbarui sumber data untuk tabel pivot yang ada dalam buku kerja Excel Anda.
### Apakah saya perlu menginstal Office untuk menggunakan Aspose.Cells?
Tidak! Aspose.Cells adalah pustaka mandiri, yang berarti Anda tidak perlu menginstal Microsoft Office untuk bekerja dengan file Excel.
### Apakah Aspose.Cells gratis untuk digunakan?
Aspose.Cells menawarkan versi uji coba gratis, tetapi untuk fungsionalitas penuh, Anda harus membeli lisensi. Anda dapat menemukan detailnya[Di Sini](https://purchase.aspose.com/buy).
### Di mana saya dapat menemukan lebih banyak contoh dan dukungan?
 Untuk contoh dan dukungan lebih lanjut, lihat[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) dan forum komunitas mereka[Di Sini](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
