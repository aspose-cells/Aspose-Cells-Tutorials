---
title: Tambahkan Bookmark PDF dengan Tujuan Bernama di Aspose.Cells
linktitle: Tambahkan Bookmark PDF dengan Tujuan Bernama di Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara membuat PDF interaktif dengan bookmark menggunakan Aspose.Cells for .NET. Panduan langkah demi langkah ini memudahkan Anda.
weight: 10
url: /id/net/rendering-and-export/add-pdf-bookmarks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Bookmark PDF dengan Tujuan Bernama di Aspose.Cells

## Perkenalan
Jika Anda pernah bekerja dengan dokumen PDF yang panjang, Anda tahu betapa sulitnya menavigasi halaman demi halaman informasi. Bookmark memainkan peran penting dalam meningkatkan pengalaman pengguna dengan menawarkan titik navigasi cepat. Dalam tutorial ini, kita akan menjelajahi cara menambahkan bookmark dengan tujuan bernama dalam PDF yang dibuat dari file Excel menggunakan Aspose.Cells for .NET.
## Prasyarat
Sebelum kita masuk ke inti pembahasan, mari pastikan Anda telah menyiapkan semuanya. Untuk mengikuti tutorial ini, Anda memerlukan:
1. Visual Studio: Ini adalah IDE yang tepat untuk pengembangan .NET. Pastikan Anda telah menginstalnya di komputer Anda.
2.  Aspose.Cells untuk .NET: Anda perlu memiliki pustaka Aspose.Cells. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/) Jika Anda ingin mencobanya terlebih dahulu, ambil[uji coba gratis di sini](https://releases.aspose.com/).
3. .NET Framework: Pastikan Anda telah menginstal versi yang kompatibel. Aspose.Cells mendukung beberapa versi .NET.
4. Pengetahuan Dasar C#: Memahami sintaksis C# akan membantu Anda memahami cuplikan kode dengan lebih baik.
Dengan perlengkapan ini di perangkat Anda, kita siap membuat dokumen PDF lengkap dengan penanda buku!
## Paket Impor
Pertama-tama, kita perlu memastikan bahwa proyek kita dapat memanfaatkan fungsi Aspose.Cells. Mulailah dengan membuat proyek C# baru di Visual Studio. Setelah itu, Anda perlu mengimpor paket yang diperlukan. Anda biasanya akan melakukannya di bagian atas berkas kode Anda:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Apakah Anda melihat betapa mudahnya hal itu? Hanya dengan menambahkan beberapa baris akan membuka perangkat yang hebat untuk menangani berkas Excel.
## Langkah 1: Menyiapkan Direktori
Untuk memulai, Anda perlu menentukan direktori sumber dan keluaran. Di sinilah berkas Excel awal Anda berada dan tempat PDF Anda akan disimpan.
```csharp
string sourceDir = "Your Document Directory"; // misalnya, "C:\\MyFiles\\"
string outputDir = "Your Document Directory"; // misalnya, "C:\\MyOutput\\"
```
Anggaplah langkah ini sebagai persiapan ruang kerja Anda. Sama seperti pelukis yang tidak akan memulai tanpa kanvas atau papan gambar, Anda juga tidak boleh memulai pengodean tanpa menentukan lokasi berkas.
## Langkah 2: Muat File Excel Sumber
Berikutnya, kita perlu memuat berkas Excel Anda ke dalam memori menggunakan kelas buku kerja.
```csharp
Workbook wb = new Workbook(sourceDir + "samplePdfBookmarkEntry_DestinationName.xlsx");
```
Memuat buku kerja seperti membuka dokumen yang penuh potensi. Buku kerja menyediakan akses ke semua lembar kerja, sel, dan kemampuan pemformatan pada file Excel asli Anda.
## Langkah 3: Mengakses Lembar Kerja
Sekarang setelah buku kerja kita dimuat, mari kita akses lembar kerja pertama. Sel-sel yang akan kita rujuk untuk penanda buku kita berada di sini.
```csharp
Worksheet ws = wb.Worksheets[0];
```
Setiap seniman membutuhkan kanvas! Dalam skenario ini, lembar kerja berfungsi sebagai kanvas, tempat Anda menentukan sel mana yang akan menampung penanda buku.
## Langkah 4: Membuat Bookmark
### Akses Sel Tertentu
Mari kita buat penanda untuk sel tertentu—misalnya sel C5. Kita akan membuat entri penanda, menautkannya ke sel tersebut, dan menetapkan nama. 
```csharp
Cell cell = ws.Cells["C5"];
PdfBookmarkEntry bookmarkEntry = new PdfBookmarkEntry();
bookmarkEntry.Text = "Text"; // Ubah ke nama penanda pilihan Anda
bookmarkEntry.Destination = cell;
bookmarkEntry.DestinationName = "AsposeCells--" + cell.Name;
```
Anda dapat menganggapnya sebagai menempelkan catatan tempel pada dokumen Anda. Judul menunjukkan tujuan penanda buku Anda, sedangkan tujuan (sel C5) adalah tujuan yang Anda tuju dalam PDF.
### Menambahkan Sub-Bookmark
Kita dapat meningkatkan pengalaman pengguna dengan menambahkan sub-bookmark. Sekarang kita akan mengakses dua sel tambahan (G56 dan L4) dan mengaturnya sebagai sub-bookmark.
```csharp
cell = ws.Cells["G56"];
PdfBookmarkEntry subbookmarkEntry1 = new PdfBookmarkEntry();
subbookmarkEntry1.Text = "Text1"; // Sub-bookmark pertama
subbookmarkEntry1.Destination = cell;
subbookmarkEntry1.DestinationName = "AsposeCells--" + cell.Name;
cell = ws.Cells["L4"];
PdfBookmarkEntry subbookmarkEntry2 = new PdfBookmarkEntry();
subbookmarkEntry2.Text = "Text2"; // Sub-bookmark kedua
subbookmarkEntry2.Destination = cell;
subbookmarkEntry2.DestinationName = "AsposeCells--" + cell.Name;
```
Sub-bookmark ini berfungsi seperti bab-bab sebuah buku—memandu pengguna ke konten yang lebih spesifik dalam dokumen.
### Tambahkan Sub-Bookmark ke Daftar
Berikutnya, kita akan mengelompokkan sub-bookmark kita di bawah bookmark utama yang kita buat sebelumnya.
```csharp
ArrayList list = new ArrayList();
list.Add(subbookmarkEntry1);
list.Add(subbookmarkEntry2);
bookmarkEntry.SubEntry = list;
```
Organisasi ini menciptakan struktur hierarki yang menyederhanakan navigasi—tetap berpegang pada “dasar-dasar penanda” untuk pengalaman pengguna yang optimal!
## Langkah 5: Menyimpan PDF dengan Bookmark
### Buat PdfSaveOptions
Sekarang saatnya membuat opsi penyimpanan PDF dan menyertakan penanda halaman yang telah kita buat.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = bookmarkEntry;
```
Langkah ini adalah langkah di mana semua persiapan Anda sebelumnya disatukan. Pada dasarnya Anda berkata, "Saya ingin PDF saya bukan hanya dokumen datar tetapi panduan interaktif!"
### Menyimpan Dokumen
Terakhir, kami menyimpan buku kerja ke dalam format PDF, dengan menggabungkan penanda halaman kami ke dalam tindakan ini.
```csharp
wb.Save(outputDir + "outputPdfBookmarkEntry_DestinationName.pdf", opts);
```
Begitu saja, semua kerja keras Anda terbayar dengan dokumen PDF terstruktur dengan baik yang dilengkapi dengan penanda halaman yang praktis!
## Kesimpulan
Selamat! Anda telah berhasil membuat PDF dengan bookmark dan tujuan bernama menggunakan Aspose.Cells untuk .NET. Anda telah mempelajari cara menavigasi file Excel, mengakses sel tertentu, dan membuat bookmark yang meningkatkan interaksi pengguna. Bayangkan betapa mudahnya menavigasi dokumen PDF Anda dengan bookmark praktis ini.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells untuk .NET?
Aspose.Cells adalah pustaka yang hebat untuk bekerja dengan berkas Excel, yang memungkinkan Anda membuat, memodifikasi, dan mengonversi lembar kerja secara terprogram.
### Dapatkah saya menggunakan Aspose.Cells dalam proyek gratis?
Ya! Aspose menawarkan uji coba gratis jika Anda ingin mencoba fitur-fiturnya sebelum membeli lisensi.
### Bagaimana cara mendapatkan lisensi untuk Aspose.Cells?
 Anda dapat membeli lisensi langsung dari mereka[halaman pembelian](https://purchase.aspose.com/buy).
### Jenis dokumen apa yang dapat ditangani Aspose.Cells?
Dapat bekerja dengan berbagai format, termasuk XLSX, XLS, CSV, PDF, dan banyak lainnya.
### Di mana saya bisa mendapatkan bantuan jika saya mengalami masalah?
 Anda dapat menemukan dukungan di[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
