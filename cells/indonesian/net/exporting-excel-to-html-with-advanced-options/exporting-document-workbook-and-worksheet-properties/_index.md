---
title: Mengekspor Properti Buku Kerja dan Lembar Kerja Dokumen dalam HTML
linktitle: Mengekspor Properti Buku Kerja dan Lembar Kerja Dokumen dalam HTML
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengekspor dokumen Excel, buku kerja, dan properti lembar kerja ke HTML menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah yang mudah disertakan.
weight: 11
url: /id/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengekspor Properti Buku Kerja dan Lembar Kerja Dokumen dalam HTML

## Perkenalan

Saat menangani spreadsheet, kita sering kali perlu mengonversi file Excel ke berbagai format untuk dibagikan, disimpan, atau dipresentasikan. Salah satu tugas umum adalah mengekspor properti workbook dan worksheet ke format HTML. Dalam artikel ini, kami akan memandu Anda untuk melakukannya menggunakan Aspose.Cells for .NET. Jangan khawatir jika Anda baru mengenal coding atau pustaka Aspose; kami akan menguraikannya langkah demi langkah agar mudah diikuti!

## Prasyarat

Sebelum kita masuk ke kode, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai:

1. .NET Framework: Pastikan lingkungan pengembangan Anda diatur dengan .NET Framework. Aspose.Cells kompatibel dengan versi .NET Framework hingga 4.8.
   
2.  Aspose.Cells untuk .NET: Anda harus menginstal Aspose.Cells. Anda dapat mengunduh pustaka dari[halaman unduhan](https://releases.aspose.com/cells/net/). 

3. IDE: Lingkungan Pengembangan Terpadu (IDE) yang cocok seperti Visual Studio akan menyederhanakan pengalaman pengkodean Anda.

4.  Contoh File Excel: Untuk tujuan pengujian, pastikan Anda memiliki file Excel bernama`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx` di direktori kerja Anda.

## Paket Impor

Setelah kita membahas prasyaratnya, mari kita mulai dengan mengimpor paket-paket yang diperlukan ke dalam proyek C# kita. Berikut ini cara melakukannya:

### Buat Proyek Baru

- Buka IDE Anda dan buat proyek C# baru. Anda dapat memilih aplikasi konsol, yang sangat cocok untuk menjalankan jenis tugas ini.

### Tambahkan Paket NuGet Aspose.Cells

Untuk menambahkan paket Aspose.Cells, ikuti langkah-langkah berikut:

- Klik kanan pada proyek Anda di Solution Explorer dan pilih "Kelola Paket NuGet."
- Di NuGet Package Manager, cari "Aspose.Cells" dan instal.
- Paket ini akan menyediakan kelas dan metode yang diperlukan untuk bekerja dengan berkas Excel.

### Mengimpor Ruang Nama

Di bagian atas file program utama Anda, pastikan Anda menyertakan namespace berikut:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

 Ini akan memberi kita akses ke`Workbook` Dan`HtmlSaveOptions` kelas, yang akan kita gunakan dalam contoh kita.

Sekarang setelah semuanya siap, mari kita uraikan prosesnya menjadi beberapa langkah sederhana.

## Langkah 1: Siapkan Direktori File Anda

Pertama, kita perlu menentukan di mana file input dan output akan ditempatkan. Dalam kode Anda, inisialisasi direktori seperti ini:

```csharp
// Direktori sumber
string sourceDir = "Your Document Directory/";  // Perbarui dengan jalur Anda yang sebenarnya

// Direktori keluaran
string outputDir = "Your Document Directory/";  // Perbarui dengan jalur Anda yang sebenarnya
```

- Direktori Sumber: Di sinilah file Excel input Anda (`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`) disimpan.
- Direktori Keluaran: Ini adalah jalur tempat Anda ingin menyimpan berkas HTML keluaran.

## Langkah 2: Muat File Excel Anda

 Sekarang kita perlu memuat file Excel menggunakan`Workbook` kelas:

```csharp
// Muat file Excel contoh
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

-  Contoh Buku Kerja:`Workbook` konstruktor mengambil jalur file ke file Excel Anda dan membuat contoh baru yang dapat Anda manipulasi.

## Langkah 3: Siapkan Opsi Penyimpanan HTML

Berikutnya, kita tentukan bagaimana kita ingin menyimpan data Excel ke HTML:

```csharp
// Tentukan Opsi Penyimpanan HTML
HtmlSaveOptions options = new HtmlSaveOptions();

// Mencegah pengeksporan properti dokumen, buku kerja, dan lembar kerja
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions: Kelas ini membantu mengelola bagaimana file Excel akan diubah ke HTML.
-  Kami menetapkan beberapa opsi untuk`false`karena kita tidak ingin menyertakan properti buku kerja dan lembar kerja dalam keluaran HTML kita.

## Langkah 4: Ekspor Semuanya ke HTML

Sekarang kita siap untuk menyimpan buku kerja kita ke dalam format HTML:

```csharp
// Ekspor file Excel ke HTML dengan Opsi Penyimpanan HTML
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

-  Itu`Save` Metode ini menggunakan dua parameter: jalur file untuk file HTML keluaran dan opsi yang telah kita atur. Menjalankan metode ini akan membuat file HTML Anda di direktori keluaran yang ditentukan.

## Langkah 5: Umpan Balik Konsol

Terakhir, mari berikan umpan balik di konsol untuk mengetahui proses telah berhasil diselesaikan:

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## Kesimpulan

Dan begitu saja, Anda telah berhasil mengekspor properti workbook dan worksheet ke HTML menggunakan Aspose.Cells untuk .NET! Anda telah mengikuti proses yang mudah, mulai dari menyiapkan lingkungan hingga mengekspor data Excel Anda. Keunggulan menggunakan pustaka seperti Aspose.Cells adalah menyederhanakan tugas-tugas yang rumit, sehingga memudahkan pengembang. Kini, Anda dapat berbagi spreadsheet secara lebih luas dengan HTML, seperti membiarkan orang lain mengintip workbook Anda tanpa harus memberikan seluruh buku kepada mereka.

## Pertanyaan yang Sering Diajukan

### Bagaimana cara menginstal Aspose.Cells untuk .NET?  
Anda dapat menginstal pustaka Aspose.Cells melalui NuGet di proyek Visual Studio Anda melalui Manajer Paket NuGet.

### Bisakah saya menyesuaikan keluaran HTML?  
 Ya, Aspose.Cells menyediakan berbagai opsi di`HtmlSaveOptions` untuk menyesuaikan cara file Excel Anda dikonversi ke HTML.

### Apakah ada cara untuk menyertakan properti dokumen dalam ekspor HTML?  
 Anda dapat mengatur`ExportDocumentProperties`, `ExportWorkbookProperties` , Dan`ExportWorksheetProperties` ke`true` di dalam`HtmlSaveOptions` jika Anda ingin menyertakannya.

### Format apa saja yang dapat saya ekspor berkas Excel saya selain HTML?  
Aspose.Cells mendukung berbagai format termasuk PDF, CSV, XML, dan lainnya.

### Apakah ada versi uji coba yang tersedia?  
 Ya, Anda bisa mendapatkan versi uji coba gratis Aspose.Cells dari[situs web](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
