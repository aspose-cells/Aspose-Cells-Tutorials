---
title: Dapatkan Daftar Font yang Digunakan dalam Spreadsheet
linktitle: Dapatkan Daftar Font yang Digunakan dalam Spreadsheet
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengambil dan membuat daftar font dari lembar kerja Excel menggunakan Aspose.Cells untuk .NET dengan tutorial yang mudah diikuti ini.
weight: 10
url: /id/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Daftar Font yang Digunakan dalam Spreadsheet

## Perkenalan
Pernahkah Anda menggulir lembar kerja Excel, bertanya-tanya tentang font yang digunakan di berbagai selnya? Mungkin Anda pernah menemukan dokumen lama dan ingin tahu pilihan tipografi apa yang dibuat? Nah, Anda beruntung! Dengan Aspose.Cells untuk .NET, rasanya seperti memiliki kotak peralatan yang memungkinkan Anda menyaring dan mengungkap rahasia font yang tersembunyi di lembar kerja Anda. Dalam panduan ini, kami akan memandu Anda tentang cara mudah mengambil daftar semua font yang digunakan dalam file Excel. Kencangkan sabuk pengaman, dan mari selami dunia lembar kerja!
## Prasyarat
Sebelum kita mulai membuat kode, ada beberapa hal yang perlu Anda ketahui untuk memulai. Jangan khawatir, ini sangat mudah. Berikut ini adalah daftar periksa yang berisi hal-hal yang Anda perlukan:
1. Visual Studio: Pastikan Anda memiliki versi Visual Studio yang terpasang di komputer Anda. Di sinilah kita akan menulis kode.
2. Aspose.Cells untuk .NET: Anda perlu memiliki pustaka Aspose.Cells yang tersedia. Jika Anda belum mengunduhnya, Anda dapat mengambilnya dari[lokasi](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Sedikit pemahaman tentang pemrograman C# pasti akan membantu Anda menavigasi kode dengan mudah.
4. Contoh Berkas Excel: Anda akan memerlukan contoh berkas Excel, seperti "sampleGetFonts.xlsx," untuk digunakan. Di sinilah kita akan menerapkan eksplorasi fon kita.
Setelah semuanya beres, Anda siap untuk memulai pengkodean!
## Paket Impor
Untuk memulai, mari impor namespace yang diperlukan. Di .NET, mengimpor paket sama halnya dengan mengundang tamu yang tepat ke pesta Anda—tanpa mereka, semuanya tidak akan berjalan lancar.
Berikut cara mengimpor Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Dengan baris sederhana ini, kita mengundang fungsionalitas inti Aspose.Cells ke dalam proyek kita. Sekarang, mari kita lanjutkan untuk memuat buku kerja.
## Langkah 1: Mengatur Direktori Dokumen
Hal pertama yang harus dilakukan—sebelum kita mulai kodenya, Anda perlu mengatur jalur ke direktori dokumen Anda. Di sinilah berkas Excel Anda berada. 
```csharp
string dataDir = "Your Document Directory";
```
Anda akan mengganti "Direktori Dokumen Anda" dengan jalur sebenarnya tempat file Excel Anda berada. Anggap saja ini seperti memberi tahu program, "Hei, ini tempat saya menyimpan file Excel saya; coba lihat!"
## Langkah 2: Muat Buku Kerja Sumber
 Saatnya memuat file Excel. Kita akan membuat contoh baru dari`Workbook` kelas dan masukkan jalur berkas. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 Apa yang terjadi di sini? Pada dasarnya kita membuka pintu ke spreadsheet kita.`Workbook` Kelas ini memungkinkan kita berinteraksi dengan konten berkas Excel. 
## Langkah 3: Dapatkan Semua Font
 Sekarang tibalah saatnya—mari kita benar-benar mengambil kembali font tersebut!`GetFonts()` metode ini adalah tiket emas kita.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Di sini, kami meminta buku kerja untuk membocorkan semua font yang digunakan di dalamnya.`fnts` susunan itu akan menampung harta karun kita.
## Langkah 4: Cetak Font
Terakhir, mari kita cetak font-font tersebut. Ini akan membantu kita memverifikasi apa yang telah kita temukan.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Loop ini berjalan melalui setiap font di`fnts` array, lalu menampilkannya ke konsol satu per satu. Ini seperti memamerkan semua pilihan tipografi keren yang Anda miliki di berkas Excel Anda!
## Kesimpulan
Nah, itu dia! Hanya dengan beberapa baris kode, Anda telah berhasil mengambil dan mencetak daftar font yang digunakan dalam lembar kerja Excel Anda menggunakan Aspose.Cells for .NET. Ini bukan hanya tentang font; ini tentang memahami seluk-beluk dokumen Anda, menyempurnakan presentasi Anda, dan menguasai seni tipografi dalam lembar kerja Anda. Apakah Anda seorang pengembang atau seseorang yang suka mengutak-atik Excel, cuplikan kecil ini bisa menjadi pengubah permainan. 
## Pertanyaan yang Sering Diajukan
### Apakah saya perlu menginstal Aspose.Cells secara terpisah?
Ya, Anda perlu mengunduh dan merujuk pustaka dalam proyek Anda. 
### Bisakah saya menggunakan Aspose.Cells untuk format lain?
Tentu saja! Aspose.Cells bekerja dengan berbagai format Excel, seperti XLSX, XLS, dan CSV.
### Apakah ada uji coba gratis yang tersedia?
 Ya, Anda dapat mengambil uji coba gratis dari[tautan unduhan](https://releases.aspose.com/).
### Bagaimana saya bisa mendapatkan dukungan teknis?
 Jika Anda membutuhkan bantuan,[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9) adalah sumber daya yang bagus.
### Apakah Aspose.Cells kompatibel dengan .NET Core?
Ya, Aspose.Cells juga kompatibel dengan proyek .NET Core.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
