---
title: Simpan File Excel dalam Format 97-2003
linktitle: Simpan File Excel dalam Format 97-2003
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyimpan file Excel dalam format 97-2003 menggunakan Aspose.Cells untuk .NET. Dapatkan wawasan praktis dan panduan langkah demi langkah.
weight: 10
url: /id/net/saving-files-in-different-formats/save-excel-file-in-97-2003-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan File Excel dalam Format 97-2003

## Perkenalan
Membuat dan mengelola file Excel secara terprogram dapat menjadi pengubah permainan, terutama bagi bisnis yang sangat bergantung pada manipulasi data. Salah satu alat hebat yang tersedia untuk pengembang .NET adalah Aspose.Cells. Alat ini serbaguna dan canggih, membantu Anda menyederhanakan alur kerja dan mengotomatiskan tugas dengan spreadsheet. Jika Anda ingin menyimpan file Excel dalam format klasik 97-2003, Anda telah datang ke tempat yang tepat! Mari kita bahas.
## Prasyarat
Sebelum kita masuk ke inti permasalahan, ada beberapa prasyarat yang perlu Anda penuhi dari daftar Anda:
1. Pemahaman Dasar tentang .NET: Keakraban dengan C# atau VB.NET akan sangat membantu.
2.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells di proyek Anda. Jika belum, Anda dapat[unduh disini](https://releases.aspose.com/cells/net/).
3. Visual Studio: Lingkungan pengembangan seperti Visual Studio atau IDE yang kompatibel dengan .NET akan memfasilitasi pengkodean dan debugging.
4. Manajer Paket NuGet: Untuk instalasi Aspose.Cells termudah di proyek Anda. 
Setelah Anda menyiapkan prasyarat ini, kita siap berangkat!
## Paket Impor
Untuk memulai dengan Aspose.Cells, pertama-tama Anda perlu mengimpor namespace yang diperlukan ke dalam proyek Anda. Ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk memanipulasi file Excel. Berikut caranya:
### Buka Proyek Anda
Buka proyek .NET Anda di Visual Studio.
### Instal Aspose.Cells
Jika Anda belum menginstal paket Aspose.Cells, Anda dapat melakukannya melalui NuGet. 
1. Buka Alat -> Manajer Paket NuGet -> Kelola Paket NuGet untuk Solusi.
2. Cari Aspose.Cells.
3. Klik Instal.
### Impor Namespace
Di bagian atas file C# Anda, sertakan baris berikut:
```csharp
using System.IO;
using Aspose.Cells;
```
Sekarang Anda siap untuk memulai membuat kode!
Di bagian ini, kami akan memandu Anda melalui proses penyimpanan file Excel dalam format 97-2003 (.xls) menggunakan Aspose.Cells. Mari kita uraikan menjadi beberapa langkah yang mudah diikuti.
## Langkah 1: Siapkan Direktori Dokumen
Hal pertama yang harus dilakukan! Anda perlu menentukan direktori tempat file Excel Anda akan disimpan.
```csharp
string dataDir = "Your Document Directory";
```
- `"Your Document Directory"` : Ganti string placeholder ini dengan jalur sebenarnya tempat Anda ingin menyimpan file Excel Anda. Bisa jadi seperti ini`"C:\\ExcelFiles\\"`.
## Langkah 2: Buat Objek Buku Kerja Baru
 Selanjutnya, mari kita buat contoh baru dari`Workbook` kelas. Di sinilah semua keajaiban terjadi!
```csharp
Workbook workbook = new Workbook();
```
- `Workbook`: Kelas ini mewakili berkas Excel yang sedang Anda kerjakan. Dengan membuatnya, pada dasarnya Anda membuat buku kerja kosong yang baru.
## Langkah 3: Simpan Buku Kerja dalam Format 97-2003
Inilah saat yang Anda tunggu-tunggu! Saatnya menyimpan buku kerja Anda. Ada dua cara untuk melakukannya.
### Simpan Sederhana
Gunakan kode berikut untuk menyimpan berkas Anda langsung ke jalur yang ditentukan.
```csharp
workbook.Save(dataDir + "output.xls");
```
### Simpan dengan Format yang Ditentukan
Anda juga dapat menentukan format penyimpanan secara eksplisit:
```csharp
workbook.Save(dataDir + "output.xls", SaveFormat.Excel97To2003);
```
- `output.xls`: Ini adalah nama berkas yang Anda simpan. Anda dapat mengganti namanya sesuai kebutuhan.
- `SaveFormat.Excel97To2003`: Ini memastikan bahwa berkas Anda disimpan dalam format Excel 97-2003.
## Kesimpulan
Nah, itu dia – tutorial mudah tentang cara menyimpan file Excel dalam format klasik 97-2003 menggunakan Aspose.Cells untuk .NET. Baik Anda membuat laporan keuangan atau mengelola log data, pendekatan ini dapat menyederhanakan pekerjaan Anda dan meningkatkan produktivitas. Selamat menjelajahi kemampuan pustaka yang hebat ini!
Ingat, seperti halnya proyek pengodean lainnya, bereksperimen dan bermain-main dengan berbagai fitur akan membuka lebih banyak kemungkinan. Jadi, jangan ragu!
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka hebat untuk .NET yang memungkinkan pengembang bekerja dengan format file Excel tanpa perlu menginstal Microsoft Excel.
### Bagaimana cara mengunduh Aspose.Cells untuk .NET?
 Anda dapat mengunduhnya dari[tautan ini](https://releases.aspose.com/cells/net/).
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Anda dapat mencobanya dengan uji coba gratis yang tersedia[Di Sini](https://releases.aspose.com/).
### Dalam format apa saya dapat menyimpan file Excel?
Anda dapat menyimpan file Excel dalam berbagai format seperti XLS, XLSX, CSV, PDF, dan banyak lagi.
### Di mana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Kunjungi[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9) untuk bantuan.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
