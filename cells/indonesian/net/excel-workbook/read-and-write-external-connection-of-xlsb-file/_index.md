---
title: Membaca dan Menulis Koneksi Eksternal File XLSB
linktitle: Membaca dan Menulis Koneksi Eksternal File XLSB
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara mengelola koneksi eksternal dalam file XLSB menggunakan Aspose.Cells untuk .NET dalam tutorial komprehensif ini.
weight: 130
url: /id/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membaca dan Menulis Koneksi Eksternal File XLSB

## Perkenalan

Hai, penggemar Excel! Apakah Anda siap menyelami dunia file XLSB dan koneksi eksternal yang menarik? Jika Anda pernah bekerja dengan Excel, Anda tahu betapa hebat dan serbagunanya Excel, tetapi terkadang Excel memiliki kekurangannya sendiri—terutama saat menangani koneksi ke basis data eksternal. Di sinilah Aspose.Cells for .NET hadir untuk menyelamatkan Anda! Pustaka praktis ini memungkinkan Anda untuk memanipulasi file Excel dengan cara yang mudah. Dalam artikel ini, kami akan memandu Anda melalui panduan langkah demi langkah tentang cara membaca dan menulis koneksi eksternal dalam file XLSB.

## Prasyarat

Sebelum kita mulai, berikut beberapa hal yang Anda perlukan:

1. Pengetahuan Dasar tentang C#: Mengetahui bahasa pemrograman C# akan sangat membantu. Jika Anda merasa nyaman menulis kode C#, Anda siap melakukannya!
2.  Aspose.Cells untuk .NET: Anda harus memasang pustaka ini di lingkungan pengembangan Anda. Jika Anda belum melakukannya, Anda dapat mengunduhnya dengan mudah[Di Sini](https://releases.aspose.com/cells/net/). 
3. IDE: Anda memerlukan editor kode atau Lingkungan Pengembangan Terpadu (IDE) seperti Visual Studio. 
4. Contoh Berkas XLSB: Kita akan bekerja dengan contoh berkas XLSB yang berisi koneksi eksternal. Anda dapat membuatnya sendiri atau mengunduh contoh secara daring. 

Setelah Anda memiliki semua prasyarat ini, kita siap untuk masuk ke kodenya!

## Paket Impor

Untuk memulainya, mari impor paket-paket yang diperlukan ke dalam proyek kita. Pastikan Anda telah menambahkan referensi ke Aspose.Cells di proyek Anda. Berikut ini cara melakukannya di C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Impor ini memberi Anda akses ke fungsionalitas yang Anda perlukan untuk memanipulasi file Excel dan koneksinya.

## Langkah 1: Siapkan Direktori

Sebelum bekerja dengan berkas XLSB, Anda perlu mengatur direktori sumber dan keluaran. Langkah ini penting untuk menjaga berkas Anda tetap teratur.

```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Output Directory";
```

 Dalam potongan kode ini,`"Your Document Directory"` Dan`"Your Document Directory"` diasumsikan mengambil jalur masing-masing tempat file input dan output Anda akan berada. Anda dapat mengganti metode ini dengan jalur hardcoded jika Anda mau.

## Langkah 2: Muat File XLSB

Sekarang saatnya memuat berkas Excel Anda ke dalam objek Buku Kerja. Ini memberi Anda kemampuan untuk memanipulasi data di dalamnya.

```csharp
// Muat file Excel Xlsb sumber
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

 Pastikan file XLSB Anda berada di lokasi yang ditentukan`sourceDir`Jika jalurnya benar, buku kerja Anda akan siap untuk dimanipulasi!

## Langkah 3: Akses Koneksi Eksternal

Dengan buku kerja yang dimuat, Anda dapat mengakses koneksi eksternalnya. Dalam kasus kami, kami akan mengambil koneksi basis data pertama.

```csharp
// Baca koneksi eksternal pertama yang sebenarnya adalah Koneksi DB
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

 Di Sini,`DataConnections[0]` mengacu pada koneksi pertama di buku kerja. Kami mentransmisikannya sebagai`DBConnection` ketik untuk manipulasi lebih lanjut.

## Langkah 4: Ekstrak Informasi Koneksi

Sekarang setelah Anda memiliki akses ke koneksi basis data, mari mengekstrak dan mencetak detailnya ke konsol. Ini akan membantu kita melihat dengan tepat apa yang sedang kita kerjakan.

```csharp
// Cetak Nama, Perintah dan Info Koneksi dari DB-Connection
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Langkah ini memungkinkan Anda untuk memverifikasi status terkini koneksi eksternal Anda. Anda akan melihat nama koneksi, perintah yang digunakan, dan info koneksi yang tercetak di konsol.

## Langkah 5: Ubah Koneksi

Terkadang, perubahan nama sudah cukup untuk membuat semuanya lebih jelas atau sesuai dengan konvensi penamaan yang baru. Mari kita ubah nama koneksi yang ada menjadi sesuatu yang lebih relevan.

```csharp
// Ubah Nama Koneksi
dbCon.Name = "NewCust";
```

Baris kode ini secara efektif mengganti nama koneksi Anda dari nama aslinya menjadi "NewCust". Ini adalah perubahan yang sederhana namun berdampak!

## Langkah 6: Simpan Perubahan Anda

Setelah melakukan modifikasi, sebaiknya Anda menyimpan perubahan kembali ke berkas XLSB. Berikut cara melakukannya:

```csharp
// Simpan file Excel Xlsb
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Baris kode ini menyimpan buku kerja Anda yang telah diperbarui, mempertahankan semua perubahan Anda, termasuk nama koneksi baru.

## Langkah 7: Konfirmasi Eksekusi

Terakhir, mari kita pastikan bahwa semuanya berjalan lancar. Pesan sederhana di akhir akan memperjelasnya.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Pesan ini akan meyakinkan Anda bahwa kode Anda berjalan dengan sukses dan semua perubahan disimpan seperti yang diharapkan.

## Kesimpulan

Nah, itu dia! Anda telah berhasil mempelajari cara membaca dan menulis koneksi eksternal dalam file XLSB menggunakan Aspose.Cells untuk .NET. Dengan mengikuti langkah-langkah ini, Anda dapat mengelola koneksi data Excel secara efektif, sehingga pekerjaan Anda dengan Excel menjadi jauh lebih mudah dan tidak membuat frustrasi. Ingat, baik Anda menangani kumpulan data yang banyak atau sekadar mengatur informasi, Aspose.Cells memiliki alat yang Anda butuhkan.

## Pertanyaan yang Sering Diajukan

### Apa itu berkas XLSB?  
File XLSB adalah format file Excel biner yang menyimpan data lembar kerja dalam format biner, membuatnya lebih ringkas dan lebih cepat untuk dibuka.

### Bagaimana cara menginstal Aspose.Cells untuk .NET?  
 Anda dapat dengan mudah mengunduhnya dari situs web Aspose[Di Sini](https://releases.aspose.com/cells/net/).

### Bisakah saya menggunakan Aspose.Cells secara gratis?  
 Ya! Anda dapat memulai dengan uji coba gratis, yang tersedia[Di Sini](https://releases.aspose.com/).

### Apakah Aspose.Cells mendukung format file lain?  
Tentu saja! Aspose.Cells mendukung berbagai format file, termasuk XLSX, CSV, dan banyak lagi.

### Di mana saya dapat mencari bantuan jika saya mengalami masalah?  
Anda bisa mendapatkan dukungan dari forum Aspose[Di Sini](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
