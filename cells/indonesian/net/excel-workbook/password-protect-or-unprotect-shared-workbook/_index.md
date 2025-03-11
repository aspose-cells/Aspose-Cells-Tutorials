---
title: Melindungi atau Membuka Proteksi Buku Kerja Bersama dengan Kata Sandi
linktitle: Melindungi atau Membuka Proteksi Buku Kerja Bersama dengan Kata Sandi
second_title: Referensi API Aspose.Cells untuk .NET
description: Amankan file Excel yang Anda bagikan menggunakan Aspose.Cells untuk .NET dengan panduan mudah kami tentang perlindungan kata sandi dan teknik tidak terlindungi.
weight: 120
url: /id/net/excel-workbook/password-protect-or-unprotect-shared-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Melindungi atau Membuka Proteksi Buku Kerja Bersama dengan Kata Sandi

## Perkenalan

Dalam ruang kerja digital saat ini, berbagi dokumen merupakan skenario umum yang memerlukan pertimbangan keamanan yang cermat. Saat bekerja dengan file Excel, terutama buku kerja bersama, melindungi informasi sensitif menjadi sangat penting. Dalam panduan ini, saya akan memandu Anda melalui langkah-langkah untuk melindungi kata sandi dan membuka perlindungan buku kerja bersama menggunakan Aspose.Cells for .NET. Pada akhirnya, Anda akan merasa yakin dalam mengelola keamanan Excel seperti seorang profesional!

## Prasyarat

Sebelum kita masuk ke kode, pastikan Anda telah menyiapkan hal berikut:

- Pengetahuan Dasar C#: Anda tidak perlu menjadi ahli pengkodean, tetapi Anda harus merasa nyaman dengan sintaksis dan konsep C#.
-  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka di proyek Anda. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/).
- .NET SDK: Pastikan Anda telah menginstal .NET SDK untuk menjalankan aplikasi.
- Visual Studio atau IDE apa pun: Siapkan lingkungan pengkodean pilihan Anda untuk menulis dan mengeksekusi kode.

## Paket Impor

Untuk memulai, Anda perlu mengimpor paket yang diperlukan. Dalam proyek C# Anda, sertakan pustaka Aspose.Cells. Berikut cara melakukannya:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Dengan paket yang tepat, kita dapat menavigasi dengan lancar melalui pembuatan, perlindungan, dan penghapusan perlindungan buku kerja bersama kita. 

## Langkah 1: Siapkan Direktori Output

Hal pertama yang perlu Anda lakukan adalah menentukan di mana file output Anda akan disimpan. Ini seperti menyiapkan folder sebelum membuat karya seni Anda. Berikut caranya:

```csharp
// Direktori keluaran
string outputDir = "Your Document Directory";
```

Baris kode ini mengambil jalur direktori tempat file yang dihasilkan akan disimpan. Pastikan direktori ini ada; jika tidak, Anda mungkin menghadapi kesalahan file tidak ditemukan nanti.

## Langkah 2: Buat Buku Kerja Baru

Berikutnya, kita akan membuat contoh buku kerja Excel baru. Anggap saja ini seperti meletakkan kanvas kosong untuk memulai karya agung Anda.

```csharp
// Buat file Excel kosong
Workbook wb = new Workbook();
```

 Baris ini menginisialisasi objek buku kerja baru bernama`wb`Sekarang kita siap mengerjakan kanvas baru ini.

## Langkah 3: Lindungi Buku Kerja Bersama dengan Kata Sandi

Sekarang tibalah bagian yang menarik – melindungi buku kerja kita. Dengan menerapkan kata sandi, Anda memastikan bahwa hanya mereka yang memiliki kredensial yang tepat yang dapat membuat perubahan. Berikut cara melakukannya:

```csharp
// Lindungi Buku Kerja Bersama dengan Kata Sandi
wb.ProtectSharedWorkbook("1234");
```

Dalam kasus ini, "1234" adalah kata sandi kami. Anda dapat mengubahnya sesuai keinginan Anda. Perintah ini mengunci buku kerja, mencegah penyuntingan yang tidak sah.

## Langkah 4: (Opsional) Buka Proteksi Buku Kerja

Jika Anda berubah pikiran atau perlu mengedit buku kerja nanti, Anda dapat membukanya dengan mudah dengan menghapus komentar pada baris di bawah ini. Ini seperti memiliki kunci brankas:

```csharp
// Hapus komentar pada baris ini untuk Membuka Proteksi Buku Kerja Bersama
// wb.UnprotectSharedWorkbook("1234");
```

Saat Anda siap mengedit lagi, cukup panggil metode ini dengan kata sandi yang benar.

## Langkah 5: Simpan File Excel Output

Sentuhan terakhir adalah menyimpan buku kerja Anda. Di sinilah kerja keras Anda disimpan untuk penggunaan di masa mendatang—mirip seperti menyimpan dokumen di komputer Anda.

```csharp
// Simpan file Excel keluaran
wb.Save(outputDir + "outputProtectSharedWorkbook.xlsx");
```

Baris ini menyimpan buku kerja Anda yang dilindungi dalam direktori keluaran yang ditunjuk dengan nama "outputProtectSharedWorkbook.xlsx". 

## Langkah 6: Verifikasi Eksekusi

Setelah menyimpan buku kerja, sebaiknya Anda memeriksa apakah semuanya berjalan lancar. Berikut ini pesan konfirmasi sederhana:

```csharp
Console.WriteLine("PasswordProtectOrUnprotectSharedWorkbook executed successfully.\r\n");
```

Dengan ini, Anda akan tahu kode Anda dijalankan seperti yang diharapkan dan berkas Excel Anda sudah siap!

## Kesimpulan

Dalam tutorial ini, kami telah membahas cara melindungi dan membuka proteksi buku kerja bersama menggunakan Aspose.Cells for .NET. Dengan mengikuti langkah-langkah ini, Anda dapat memastikan file Excel Anda tetap aman sekaligus tetap memungkinkan kolaborasi. Baik Anda berbagi data keuangan sensitif atau informasi klien, melindungi pekerjaan Anda sangat penting dalam lingkungan saat ini.

## Pertanyaan yang Sering Diajukan

### Bisakah saya menggunakan kata sandi yang lebih rumit?
Tentu saja! Anda dapat menggunakan string apa pun yang memenuhi persyaratan kebijakan kata sandi Anda.

### Apa yang terjadi jika saya lupa kata sandinya?
Sayangnya, jika Anda lupa kata sandinya, Anda tidak akan dapat membuka proteksi buku kerja tanpa menggunakan alat pihak ketiga atau ahli.

### Apakah Aspose.Cells gratis untuk digunakan?
 Aspose.Cells adalah produk komersial, tetapi Anda dapat mencobanya secara gratis untuk waktu terbatas melalui uji coba gratis mereka:[Uji coba gratis](https://releases.aspose.com/).

### Apakah ada cara untuk menggunakan ini dalam bahasa pemrograman lain?
Aspose.Cells terutama mendukung .NET, tetapi mereka juga memiliki pustaka untuk Java dan bahasa lainnya. Kunjungi situs mereka untuk informasi lebih lanjut!

### Bagaimana cara mendapatkan dukungan untuk Aspose.Cells?
 Anda dapat meminta bantuan melalui forum dukungan mereka:[Dukungan Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
