---
title: Dapatkan Lebar Kertas Dan Tinggi Lembar Kerja
linktitle: Dapatkan Lebar Kertas Dan Tinggi Lembar Kerja
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara mendapatkan lebar dan tinggi kertas lembar kerja di Aspose.Cells untuk .NET dengan panduan langkah demi langkah yang sederhana.
weight: 80
url: /id/net/excel-display-settings-csharp-tutorials/get-paper-width-and-height-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Lebar Kertas Dan Tinggi Lembar Kerja

## Perkenalan

Pernahkah Anda mencoba mencetak lembar Excel dan berhadapan dengan dimensi yang membingungkan dari berbagai ukuran kertas? Jika Anda seperti saya, Anda tahu bahwa tidak ada yang dapat merusak hari Anda seperti tata letak yang tidak sesuai! Baik Anda mencetak laporan, faktur, atau sekadar daftar sederhana, memahami cara menyesuaikan dimensi kertas secara terprogram dapat menghemat banyak masalah bagi Anda. Hari ini, kita akan menyelami dunia Aspose.Cells untuk .NET untuk memeriksa cara mengambil dan mengatur ukuran kertas secara langsung di aplikasi Anda. Mari kita mulai dan masuk ke seluk-beluk pengelolaan dimensi kertas tersebut!

## Prasyarat 

Sebelum kita masuk ke keajaiban coding, mari kumpulkan apa saja yang Anda butuhkan untuk memulai:

1. Pemahaman Dasar tentang C#: Anda harus memiliki pemahaman dasar tentang C#. Jika Anda baru dalam pemrograman, jangan khawatir! Kami akan menjelaskannya secara sederhana.
2.  Pustaka Aspose.Cells: Pastikan Anda telah menginstal pustaka Aspose.Cells untuk .NET di komputer Anda. Anda dapat mengunduhnya dari[tautan ini](https://releases.aspose.com/cells/net/).
3. Lingkungan Pengembangan .NET: Siapkan Visual Studio atau IDE pilihan Anda untuk menulis dan menjalankan kode C#. Jika Anda tidak yakin harus mulai dari mana, Visual Studio Community Edition adalah pilihan yang tepat.
4.  Referensi dan Dokumentasi: Biasakan diri Anda dengan dokumentasi Aspose.Cells untuk wawasan yang lebih mendalam. Anda dapat menemukannya[Di Sini](https://reference.aspose.com/cells/net/).
5. Pengetahuan Dasar tentang File Excel: Memahami bagaimana file Excel terstruktur (lembar kerja, baris, dan kolom) akan sangat membantu.

Bagus! Sekarang setelah semua hal penting sudah terpenuhi, mari langsung mengimpor paket yang diperlukan.

## Paket Impor

 Untuk mempermudah hidup kita dan memanfaatkan sepenuhnya kekuatan Aspose.Cells, kita perlu mengimpor beberapa paket. Semudah menambahkan`using` pernyataan di bagian atas berkas kode Anda. Berikut ini yang perlu Anda impor:

```csharp
using System;
using System.IO;
```

Baris ini memungkinkan kita mengakses semua kelas dan metode dalam pustaka Aspose.Cells, sehingga memudahkan manipulasi file Excel. Sekarang, mari kita masuk ke panduan langkah demi langkah untuk mendapatkan lebar dan tinggi kertas untuk berbagai ukuran kertas.

## Langkah 1: Buat Buku Kerja Baru

Langkah pertama dalam bekerja dengan Aspose.Cells adalah membuat buku kerja baru. Bayangkan buku kerja sebagai kanvas kosong tempat Anda dapat menambahkan lembar kerja, sel, dan, dalam kasus kami, menentukan ukuran kertas.

```csharp
//Buat buku kerja
Workbook wb = new Workbook();
```

Baris ini membuat objek buku kerja baru, siap untuk kita manipulasi. Anda belum akan melihat apa pun, tetapi kanvas kita sudah siap!

## Langkah 2: Akses Lembar Kerja Pertama

Sekarang setelah kita memiliki buku kerja, kita perlu mengakses lembar kerja tertentu di dalamnya. Lembar kerja seperti satu halaman di buku kerja Anda, dan di sanalah semua tindakan terjadi.

```csharp
//Akses lembar kerja pertama
Worksheet ws = wb.Worksheets[0];
```

Di sini, kita mengambil lembar kerja pertama (indeks 0) dari buku kerja kita. Anda dapat menganggapnya seperti membalik halaman pertama sebuah buku. 

## Langkah 3: Atur Ukuran Kertas dan Dapatkan Dimensi

Sekarang tibalah bagian yang menarik! Kita akan mengatur ukuran kertas yang berbeda dan mengambil dimensinya satu per satu. Langkah ini penting karena memungkinkan kita melihat bagaimana ukuran yang berbeda memengaruhi tata letak.

```csharp
//Atur ukuran kertas ke A2 dan cetak lebar dan tinggi kertas dalam inci
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

 Pada blok ini, kita atur ukuran kertas ke A2 dan kemudian ambil lebar dan tingginya.`PaperWidth` Dan`PaperHeight` properties memberikan dimensi dalam inci. Ini seperti memeriksa ukuran bingkai sebelum memasukkan gambar ke dalamnya.

## Langkah 4: Ulangi untuk Ukuran Kertas Lainnya

Mari kita ulangi proses untuk ukuran kertas umum lainnya. Kita akan memeriksa ukuran A3, A4, dan Letter. Pengulangan ini penting untuk memahami bagaimana setiap ukuran didefinisikan dalam kerangka Aspose.Cells.

```csharp
//Atur ukuran kertas ke A3 dan cetak lebar dan tinggi kertas dalam inci
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//Atur ukuran kertas ke A4 dan cetak lebar dan tinggi kertas dalam inci
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//Atur ukuran kertas ke Letter dan cetak lebar dan tinggi kertas dalam inci
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

 Masing-masing blok ini meniru langkah sebelumnya tetapi menyesuaikan`PaperSize`properti yang sesuai. Hanya dengan mengubah indikator ukuran, Anda akan memperoleh dimensi kertas yang berbeda dengan mudah. Ini seperti mengubah ukuran kotak berdasarkan apa yang perlu Anda simpan!

## Kesimpulan

Nah, itu dia! Dengan mengikuti langkah-langkah ini, Anda dapat dengan mudah mengatur dan mengambil dimensi berbagai ukuran kertas di Aspose.Cells for .NET. Kemampuan ini tidak hanya menghemat waktu Anda, tetapi juga mencegah kesalahan pencetakan yang dapat terjadi karena pengaturan halaman yang salah dikonfigurasi. Jadi, lain kali Anda harus mencetak lembar Excel atau membuat laporan, Anda dapat melakukannya dengan percaya diri, karena Anda memiliki dimensi di tangan Anda. 

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang dirancang untuk memproses berkas Excel tanpa perlu menginstal Excel.

### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya! Anda dapat memulai dengan uji coba gratis yang tersedia di[tautan ini](https://releases.aspose.com/).

### Bagaimana cara mengatur ukuran kertas khusus?
 Aspose.Cells menyediakan opsi untuk mengatur ukuran kertas khusus menggunakan`PageSetup` kelas.

### Apakah pengetahuan coding diperlukan untuk menggunakan Aspose.Cells?
Pengetahuan pengkodean dasar membantu, tetapi Anda dapat mengikuti tutorial agar pemahamannya lebih mudah!

### Di mana saya dapat menemukan lebih banyak contoh?
 Itu[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) menawarkan banyak contoh dan tutorial.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
