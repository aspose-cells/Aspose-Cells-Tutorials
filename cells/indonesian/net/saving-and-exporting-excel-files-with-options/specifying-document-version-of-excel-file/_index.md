---
title: Menentukan Versi Dokumen File Excel Secara Terprogram di .NET
linktitle: Menentukan Versi Dokumen File Excel Secara Terprogram di .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menentukan properti dokumen seperti versi, penulis, dan judul dalam file Excel secara terprogram menggunakan Aspose.Cells untuk .NET dengan petunjuk langkah demi langkah.
weight: 12
url: /id/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menentukan Versi Dokumen File Excel Secara Terprogram di .NET

## Perkenalan
Aspose.Cells untuk .NET adalah pustaka canggih yang memungkinkan pengembang memanipulasi file Excel secara terprogram dengan mudah. Baik Anda ingin membuat file Excel dari awal atau memodifikasi file yang sudah ada, Aspose.Cells menawarkan API yang komprehensif untuk mencapai tujuan Anda. Salah satu fitur tersebut adalah menentukan properti dokumen seperti versi, penulis, atau judul. Tutorial ini akan memandu Anda tentang cara menentukan versi dokumen file Excel secara terprogram menggunakan Aspose.Cells untuk .NET.
## Prasyarat
Sebelum kita membahas lebih dalam, mari pastikan Anda memiliki semua yang dibutuhkan untuk mengikuti tutorial ini:
1. Aspose.Cells untuk .NET: Anda dapat mengunduh versi terbaru[Di Sini](https://releases.aspose.com/cells/net/) Jika Anda belum membeli lisensi, Anda dapat memilih[lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk menjelajahi fitur-fiturnya.
2. Lingkungan Pengembangan .NET: Anda dapat menggunakan Visual Studio atau IDE apa pun yang kompatibel dengan .NET.
3. Pengetahuan Dasar C#: Memahami pemrograman C# akan membuatnya lebih mudah untuk diikuti.
## Paket Impor
Sebelum Anda dapat mulai membuat kode, Anda perlu mengimpor namespace yang diperlukan dari pustaka Aspose.Cells. Ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk manipulasi file Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Kedua ruang nama ini penting untuk berinteraksi dengan buku kerja dan properti dokumen bawaannya.
Sekarang, mari kita uraikan proses penentuan properti dokumen dalam file Excel, termasuk versi, judul, dan penulis.
## Langkah 1: Inisialisasi Objek Buku Kerja
 Langkah pertama adalah membuat instance baru dari`Workbook` objek. Objek ini mewakili keseluruhan berkas Excel yang akan Anda gunakan.
```csharp
Workbook wb = new Workbook();
```
 Itu`Workbook`class menyediakan representasi dari file Excel. Dengan membuat instance-nya, kita membuat buku kerja Excel kosong yang dapat kita manipulasi.
## Langkah 2: Akses Properti Dokumen Bawaan
 Aspose.Cells menawarkan properti dokumen bawaan, yang mencakup bidang seperti judul, penulis, dan versi dokumen. Anda dapat mengakses properti ini melalui`BuiltInDocumentProperties`koleksi.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 Itu`BuiltInDocumentPropertyCollection` kelas menyediakan akses ke kumpulan properti dokumen bawaan, seperti judul, penulis, dan metadata lainnya yang biasanya dikaitkan dengan dokumen.
## Langkah 3: Mengatur Judul Dokumen Excel
Selanjutnya, kita akan menetapkan judul dokumen Excel. Metadata ini membantu dalam mengidentifikasi dan mengelola berkas di kemudian hari.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Menetapkan judul penting untuk pengorganisasian dokumen. Metadata ini dapat dilihat di properti file dan dapat digunakan oleh sistem eksternal untuk membuat katalog atau mengidentifikasi dokumen secara lebih efektif.
## Langkah 4: Tentukan Penulis
Penulis dokumen juga dapat ditentukan untuk mencerminkan siapa yang membuat atau memodifikasi berkas tersebut.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Langkah ini membantu dalam menghubungkan dokumen dengan pembuatnya, menyediakan metadata tambahan untuk manajemen dokumen atau skenario kolaborasi.
## Langkah 5: Tentukan Versi Dokumen
Salah satu properti terpenting yang akan kita bahas dalam tutorial ini adalah versi dokumen. Langkah ini memungkinkan Anda menentukan versi dokumen, yang berguna saat bekerja di lingkungan yang memerlukan kontrol versi.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Menetapkan versi dokumen memberikan kejelasan mengenai versi dokumen atau pustaka mana yang digunakan untuk membuat berkas. Hal ini khususnya penting dalam lingkungan yang perlu melacak revisi berkas atau kompatibilitas dengan versi pustaka yang berbeda.
## Langkah 6: Simpan File Excel
 Terakhir, Anda dapat menyimpan berkas Excel dengan semua properti yang baru saja Anda atur. Aspose.Cells memungkinkan Anda menyimpan berkas dalam berbagai format, tetapi untuk contoh ini, kita akan tetap menggunakan`.xlsx` format.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 Itu`Save` metode ini digunakan untuk menyimpan file ke direktori yang Anda tentukan. Di sini, kami menyimpannya sebagai file Excel di`.xlsx`format. Jika diperlukan, Aspose.Cells juga mendukung format seperti`.xls`, `.csv` , Dan`.pdf`, memberikan fleksibilitas berdasarkan kebutuhan proyek Anda.
## Kesimpulan
Dalam tutorial ini, kami membahas cara menentukan properti dokumen, khususnya versi dokumen, dalam file Excel menggunakan Aspose.Cells untuk .NET. Aspose.Cells adalah alat yang sangat fleksibel dan canggih yang memungkinkan Anda memanipulasi file Excel secara terprogram, menjadikannya aset yang hebat bagi pengembang .NET mana pun yang bekerja dengan spreadsheet.
## Pertanyaan yang Sering Diajukan
### Bisakah saya memodifikasi properti bawaan lainnya menggunakan Aspose.Cells?  
Ya, Anda dapat memodifikasi properti bawaan lainnya seperti subjek, kata kunci, dan komentar, antara lain.
### Format file apa yang didukung oleh Aspose.Cells?  
 Aspose.Cells mendukung berbagai macam format termasuk`.xls`, `.xlsx`, `.csv`, `.pdf`, dan banyak lagi.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells untuk .NET?  
 Anda dapat menjelajahi Aspose.Cells dengan[uji coba gratis](https://releases.aspose.com/) atau melamar[lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk pengujian lanjutan.
### Dapatkah saya menggunakan Aspose.Cells dalam aplikasi web?  
Ya, Aspose.Cells dapat digunakan di aplikasi desktop dan web. Aplikasi ini sangat serbaguna dan terintegrasi dengan baik dengan kerangka kerja web .NET.
### Di mana saya bisa mendapatkan dukungan untuk Aspose.Cells?  
 Anda dapat mengakses komunitas dan dukungan melalui[Forum dukungan Aspose.Cells](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
