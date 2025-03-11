---
title: Pemformatan dan Tampilan Tabel Pivot Secara Terprogram di .NET
linktitle: Pemformatan dan Tampilan Tabel Pivot Secara Terprogram di .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Sempurnakan tabel pivot Excel Anda dengan Aspose.Cells untuk .NET. Pelajari cara memformat, menyesuaikan, dan mengotomatiskan presentasi data Anda dengan mudah.
weight: 16
url: /id/net/creating-and-configuring-pivot-tables/formatting-and-look/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pemformatan dan Tampilan Tabel Pivot Secara Terprogram di .NET

## Perkenalan
Tabel pivot merupakan alat yang fantastis di Excel yang memungkinkan pengguna untuk meringkas dan menganalisis kumpulan data yang kompleks. Tabel pivot dapat mengubah data yang biasa menjadi laporan yang menarik secara visual dan informatif, sehingga pengguna dapat memperoleh wawasan dengan cepat. Dalam tutorial ini, kita akan membahas cara memanipulasi gaya tabel pivot menggunakan Aspose.Cells for .NET, yang memungkinkan Anda untuk mengotomatiskan dan menyesuaikan laporan Excel dengan mudah. Apakah Anda siap untuk meningkatkan keterampilan presentasi data Anda? Mari kita mulai!
## Prasyarat
Sebelum kita memulai perjalanan ini, ada beberapa hal penting yang perlu Anda siapkan:
1. Visual Studio: Ini akan menjadi lingkungan utama kita untuk pengkodean dan pengujian.
2.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka ini. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/).
3. Pemahaman Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda mengikutinya dengan mudah.
4. File Excel: Anda memerlukan file Excel yang berisi tabel pivot. Jika tidak memilikinya, Anda dapat membuat tabel pivot sederhana menggunakan Microsoft Excel.
Setelah Anda menyiapkan semuanya, mari lanjutkan dengan mengimpor paket yang diperlukan!
## Paket Impor
Untuk memulai, kita perlu mengimpor pustaka yang diperlukan ke dalam proyek C# kita. Berikut cara melakukannya:
### Buat Proyek C# Baru
Pertama, buka Visual Studio dan buat proyek Aplikasi Konsol baru. Ini akan memudahkan kita menjalankan kode.
### Tambahkan Referensi
Setelah proyek Anda disiapkan, Anda perlu menambahkan referensi ke pustaka Aspose.Cells:
- Klik kanan pada proyek Anda di Solution Explorer.
- Pilih "Kelola Paket NuGet."
- Cari "Aspose.Cells" dan instal paketnya.
Setelah itu, Anda siap mengimpor namespace Aspose.Cells. Berikut ini adalah kode untuk mengimpor paket yang diperlukan:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Sekarang setelah kita mengimpor paket kita, mari kita lihat lebih dekat cara memanipulasi format tabel pivot di Excel.
## Langkah 1: Siapkan Direktori Dokumen Anda
Pertama-tama, kita akan menentukan jalur ke berkas Excel kita. Berikut cara melakukannya:
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Pastikan untuk mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Excel Anda disimpan.
## Langkah 2: Muat Buku Kerja
 Selanjutnya, kita perlu memuat berkas Excel yang sudah ada. Pada langkah ini, kita akan menggunakan`Workbook` kelas yang disediakan oleh Aspose.Cells.
```csharp
// Memuat file template
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Ketika Anda mengganti`"Book1.xls"` dengan nama file Anda yang sebenarnya,`workbook` Objek sekarang akan berisi data Excel.
## Langkah 3: Akses Lembar Kerja dan Tabel Pivot
Sekarang, kita ingin mengambil lembar dan tabel pivot yang akan kita gunakan:
```csharp
// Dapatkan lembar kerja pertama
Worksheet worksheet = workbook.Worksheets[0];
var pivot = workbook.Worksheets[0].PivotTables[0];
```
Dalam kasus ini, kita menggunakan lembar kerja pertama dan tabel pivot pertama. Jika berkas Excel Anda memiliki beberapa lembar atau tabel pivot, pastikan untuk menyesuaikan nilai indeks sebagaimana mestinya.

Sekarang setelah kita memiliki akses ke tabel pivot, saatnya untuk membuatnya menarik secara visual! Kita dapat mengatur gaya dan memformat seluruh tabel pivot. Berikut caranya:
## Langkah 4: Mengatur Gaya Tabel Pivot
Mari terapkan gaya yang telah ditentukan sebelumnya ke tabel pivot kita:
```csharp
pivot.PivotTableStyleType = PivotTableStyleType.PivotTableStyleDark1;
```
Baris kode ini mengubah gaya tabel pivot menjadi tema gelap. Anda dapat menjelajahi berbagai gaya yang tersedia di pustaka Aspose.Cells untuk menemukan gaya yang sesuai dengan kebutuhan Anda.
## Langkah 5: Sesuaikan Gaya Tabel Pivot
Untuk kustomisasi lebih lanjut, kita dapat membuat gaya kita sendiri. Keren, bukan? Berikut cara melakukannya:
```csharp
Style style = workbook.CreateStyle();
style.Font.Name = "Arial Black";
style.ForegroundColor = Color.Yellow;
style.Pattern = BackgroundType.Solid;
```
Dalam cuplikan ini:
- Kami tentukan fontnya sebagai "Arial Black".
- Warna latar depan diatur menjadi kuning.
- Kami mengatur pola menjadi padat.
## Langkah 6: Terapkan Gaya Kustom ke Tabel Pivot
Terakhir, mari terapkan gaya yang baru dibuat ini untuk memformat seluruh tabel pivot:
```csharp
pivot.FormatAll(style);
```
Baris ini menerapkan gaya kustom Anda ke semua data dalam tabel pivot. Sekarang tabel Anda akan tampak fantastis!
## Langkah 7: Simpan Perubahan Anda
Setelah Anda selesai memformat tabel pivot, jangan lupa untuk menyimpan perubahannya. Berikut cara menyimpan dokumen:
```csharp
// Menyimpan file Excel
workbook.Save(dataDir + "output.xls");
```
 Mengganti`"output.xls"` dengan nama apa pun yang Anda inginkan untuk berkas Excel yang baru diformat. Dan voilà! Anda telah berhasil memformat tabel pivot menggunakan Aspose.Cells untuk .NET.
## Kesimpulan
Singkatnya, kami telah memulai perjalanan untuk memformat tabel pivot secara terprogram di Excel menggunakan Aspose.Cells for .NET. Kami mulai dengan mengimpor paket yang diperlukan, memuat buku kerja Excel yang ada, menyesuaikan gaya tabel pivot, dan akhirnya menyimpan output yang telah diformat. Dengan mengintegrasikan keterampilan tersebut ke dalam alur kerja Anda, Anda dapat mengotomatiskan tugas pemformatan yang membosankan yang dapat menghabiskan waktu Anda yang berharga. Jadi, mengapa tidak mencobanya? Cobalah sendiri dan tingkatkan kemampuan Excel Anda!
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka yang hebat untuk memanipulasi file Excel dalam aplikasi .NET, yang memungkinkan tugas otomatis dan terprogram diselesaikan dengan mudah.
### Dapatkah saya mencoba Aspose.Cells secara gratis?
 Ya! Anda dapat memulai dengan uji coba gratis dengan mengklik[Di Sini](https://releases.aspose.com).
### Jenis gaya tabel pivot apa yang tersedia?
 Aspose.Cells menyediakan berbagai gaya yang telah ditentukan sebelumnya, yang dapat diakses melalui`PivotTableStyleType`.
### Bagaimana cara membuat tabel pivot di Excel?
Anda dapat membuat tabel pivot di Excel menggunakan tab "Sisipkan" pada bilah alat dan memilih "Tabel Pivot" dari opsi yang tersedia.
### Di mana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Anda dapat menemukan bantuan di forum Aspose[Di Sini](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
