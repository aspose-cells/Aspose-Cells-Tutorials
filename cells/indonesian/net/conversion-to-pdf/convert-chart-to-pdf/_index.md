---
title: Konversi Bagan ke PDF dalam .NET
linktitle: Konversi Bagan ke PDF dalam .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengonversi grafik Excel ke PDF dalam format .NET menggunakan Aspose.Cells dengan panduan langkah demi langkah ini! Sempurna untuk programmer dari semua tingkatan.
weight: 11
url: /id/net/conversion-to-pdf/convert-chart-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konversi Bagan ke PDF dalam .NET

## Perkenalan
Apakah Anda ingin mengonversi grafik dari lembar kerja Excel ke format PDF menggunakan .NET? Nah, Anda berada di tempat yang tepat! Dalam panduan ini, kita akan menjelajahi seluk-beluk penggunaan Aspose.Cells untuk mencapainya. Baik Anda seorang programmer berpengalaman atau pendatang baru, pendekatan langkah demi langkah kami akan membantu Anda menavigasi proses dengan mudah.

## Prasyarat
Sebelum kita memulai perjalanan pencerahan ini, ada beberapa prasyarat yang perlu Anda penuhi dari daftar Anda:
### 1. .NET Framework atau .NET Core Terpasang
Pastikan Anda telah menginstal .NET Framework atau .NET Core di komputer Anda. Panduan ini berlaku untuk kedua lingkungan, jadi jangan khawatir jika Anda lebih suka salah satu!
### 2. Pustaka Aspose.Cells
 Keajaiban ini terjadi berkat pustaka Aspose.Cells, yang perlu Anda sertakan dalam proyek Anda. Anda dapat mengunduhnya dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
### 3. Pemahaman Dasar Pemrograman C#
Jika Anda memiliki pemahaman dasar tentang C#, itu luar biasa! Anda akan merasa mudah mengikuti contoh-contoh yang kami berikan. Jika Anda seorang pemula, jangan terlalu khawatir; kami membuat semuanya sederhana dan mudah dipahami.
### 4. Pengaturan Visual Studio
Baik Anda menggunakan Visual Studio atau IDE lainnya, pastikan lingkungan pengembangan Anda telah disiapkan untuk menulis dan menjalankan aplikasi .NET.
## Paket Impor
Untuk memulai konversi, Anda perlu mengimpor paket yang diperlukan ke dalam proyek Anda. Berikut cara melakukannya:
### Buka Proyek Anda
Luncurkan Visual Studio dan buka proyek tempat Anda ingin menerapkan fungsi ini.
### Instal Paket NuGet Aspose.Cells
Anda dapat dengan mudah menambahkan pustaka Aspose.Cells melalui NuGet Package Manager. Berikut caranya:
- Klik kanan pada proyek Anda di Solution Explorer.
- Pilih "Kelola Paket NuGet."
- Cari "Aspose.Cells" dan tekan tombol Instal.
Ini akan memastikan Anda memiliki semua kelas dan metode yang Anda butuhkan tersedia di ujung jari Anda!

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
```

Sekarang, mari kita bahas seluk-beluk mengonversi grafik ke format PDF menggunakan Aspose.Cells. Kita akan membahas setiap langkah secara metodis, sehingga Anda akan tahu persis apa yang sedang terjadi.
## Langkah 1: Menyiapkan Direktori Dokumen Anda
Hal pertama yang harus dilakukan! Anda perlu menentukan jalur penyimpanan dokumen Excel Anda. Di sinilah Anda akan mengarahkan pustaka Aspose.Cells untuk menemukan file .xls Anda.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Baris ini mengatur`dataDir` variabel ke lokasi file Excel Anda. Pastikan untuk mengganti`"Your Document Directory"` dengan jalur Anda yang sebenarnya.
## Langkah 2: Muat File Excel
Setelah Anda menetapkan direktori, saatnya memuat berkas Excel yang berisi grafik. Berikut cara melakukannya:
```csharp
// Memuat file Excel yang berisi grafik
Workbook workbook = new Workbook(dataDir + "Sample1.xls");
```
 Dengan melakukan ini, Anda membuat contoh baru`Workbook` dan memerintahkannya untuk memuat contoh berkas Excel Anda. Pastikan nama berkas dan ekstensinya sesuai dengan berkas Anda yang sebenarnya.
## Langkah 3: Akses Lembar Kerja yang Benar
File Excel mungkin memiliki beberapa lembar, jadi Anda perlu menentukan lembar mana yang ingin Anda gunakan. Di sini, kita mengakses lembar kerja pertama:
```csharp
// Akses lembar kerja pertama
Worksheet worksheet = workbook.Worksheets[0];
```
 Menggunakan indeks`0` mengambil lembar kerja pertama. Sesuaikan indeks jika bagan Anda ada di lembar lain.
## Langkah 4: Akses Bagan
Sekarang setelah Anda memiliki lembar kerja, mari ambil bagan yang ingin Anda ubah:
```csharp
// Akses bagan pertama di dalam lembar kerja
Chart chart = worksheet.Charts[0];
```
Baris ini mengakses bagan pertama yang terdapat dalam lembar kerja. Jika Anda memiliki beberapa bagan dan ingin mengonversi yang lain, cukup tingkatkan indeksnya.
## Langkah 5: Ubah Bagan ke PDF
Setelah diagram di tangan Anda, saatnya mengonversinya ke format PDF. Berikut caranya:
```csharp
// Simpan grafik ke dalam format PDF
chart.ToPdf(dataDir + "Output-Chart_out.pdf");
```
Perintah validasi ini memberi tahu Aspose.Cells untuk menyimpan bagan sebagai PDF di jalur keluaran yang ditentukan. Dan voilà! Bagan Anda sekarang dalam format PDF.
## Langkah 6: Simpan Bagan ke Aliran Memori
Jika Anda lebih suka menyimpan bagan bukan dalam bentuk berkas, melainkan dalam aliran memori (misalnya, jika Anda berencana mengunduhnya secara dinamis), Anda dapat melakukannya dengan menggunakan kode berikut:
```csharp
// Simpan grafik ke dalam format PDF di aliran
MemoryStream ms = new MemoryStream();
chart.ToPdf(ms);
```
 Dengan melakukan ini, Anda menyimpan grafik ke dalam`MemoryStream` daripada langsung ke berkas. Hal ini dapat sangat berguna untuk aplikasi web yang memerlukan pembuatan berkas dinamis.
## Kesimpulan
Nah, itu dia! Anda baru saja mempelajari cara mengonversi bagan Excel ke berkas PDF menggunakan Aspose.Cells di .NET. Proses ini tidak hanya mencakup perintah sederhana, tetapi juga memberi Anda fleksibilitas dalam cara dan tempat penyimpanan bagan. Apakah Anda menggunakan sistem berkas atau aliran memori, pilihan ada di tangan Anda!
Sekarang, Anda akan merasa yakin dalam mengonversi grafik ke PDF di aplikasi .NET Anda di masa mendatang. Jangan ragu untuk mencoba fitur-fitur tambahan Aspose.Cells, karena masih banyak lagi yang bisa ditemukan!
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET canggih yang memungkinkan pengembang untuk membuat, memanipulasi, mengonversi, dan merender file Excel secara terprogram.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya! Anda dapat mencoba Aspose.Cells secara gratis dengan mengunduh versi uji coba dari situs web mereka.[lokasi](https://releases.aspose.com/).
### Bagaimana cara memecahkan masalah kesalahan saat menggunakan Aspose.Cells?
 Jika Anda mengalami masalah, Anda dapat mengunjungi[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9) untuk bantuan.
### Apakah Aspose.Cells mendukung format dokumen lain?
Ya, selain XLS/XLSX, Aspose.Cells mendukung berbagai format, termasuk CSV, PDF, HTML, dan banyak lagi.
### Bisakah saya membeli lisensi untuk Aspose.Cells?
 Tentu saja! Kamu bisa[membeli lisensi](https://purchase.aspose.com/buy) di situs web Aspose untuk manfaat versi lengkap.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
