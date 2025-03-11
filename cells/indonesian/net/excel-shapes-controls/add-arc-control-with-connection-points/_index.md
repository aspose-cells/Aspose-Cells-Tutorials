---
title: Tambahkan Kontrol Busur dengan Titik Koneksi
linktitle: Tambahkan Kontrol Busur dengan Titik Koneksi
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara menambahkan kontrol busur dengan titik koneksi menggunakan Aspose.Cells untuk .NET dalam panduan terperinci ini.
weight: 27
url: /id/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Kontrol Busur dengan Titik Koneksi

## Perkenalan
Dalam hal membuat laporan Excel yang menarik secara visual, ilustrasi memegang peranan penting. Baik Anda sedang menyusun laporan keuangan atau uraian proyek, penggunaan bentuk seperti busur dapat menambah kedalaman dan kejelasan pada presentasi data Anda. Hari ini, kita akan membahas secara mendalam cara memanfaatkan Aspose.Cells for .NET untuk menambahkan kontrol busur dengan titik koneksi di lembar kerja Excel Anda. Jadi, jika Anda pernah bertanya-tanya bagaimana cara memperindah lembar kerja atau membuat data Anda menarik, baca terus!
## Prasyarat
Sebelum kita mulai bersenang-senang dalam coding, mari pastikan Anda sudah siap. Berikut ini yang Anda butuhkan:
1. .NET Framework: Pastikan Anda telah menginstal versi yang kompatibel. Aspose.Cells berfungsi dengan beberapa versi, termasuk .NET Core.
2.  Aspose.Cells untuk .NET: Anda perlu mengunduh dan memasang pustaka Aspose.Cells. Anda dapat dengan mudah mengambilnya dari[tautan unduhan](https://releases.aspose.com/cells/net/).
3. IDE yang Bagus: Visual Studio, teman setia setiap pengembang .NET, akan membantu menyederhanakan pengalaman pengkodean Anda.
4. Pengetahuan Dasar C#: Jika Anda menguasai C#, Anda akan mendapati tutorial ini berjalan lancar.
5. Akses ke Direktori Dokumen Anda: Ketahui di mana Anda akan menyimpan file Excel Anda. Ini penting untuk mengatur hasil kerja Anda secara efisien.
## Paket Impor
Langkah selanjutnya adalah memastikan Anda telah mengimpor paket yang tepat ke dalam proyek Anda. Aspose.Cells untuk .NET memiliki berbagai fungsi, jadi kami akan membuatnya tetap sederhana. Berikut ini hal-hal yang perlu Anda sertakan:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ruang nama ini akan memberi Anda akses ke semua fitur gambar dan fungsi manajemen sel yang akan Anda gunakan di seluruh panduan ini.
## Langkah 1: Siapkan Direktori Dokumen Anda
Hal pertama yang harus dilakukan—mari kita buat direktori tempat Anda akan menyimpan file Excel baru yang keren tersebut. Berikut cara melakukannya:
```csharp
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bagian kode ini memeriksa apakah folder yang Anda tentukan ada. Jika tidak, maka akan dibuatkan satu folder. Sederhana, bukan? Sebaiknya Anda memiliki tempat khusus untuk menyimpan berkas-berkas Anda agar tidak berantakan.
## Langkah 2: Buat Instansiasi Buku Kerja
Sekarang setelah direktori kita siap, mari buat buku kerja Excel baru.
```csharp
Workbook excelbook = new Workbook();
```
 Dengan menelepon`Workbook` konstruktor, pada dasarnya Anda berkata, “Hei, mari kita mulai file Excel baru!” Ini akan menjadi kanvas untuk semua bentuk dan data Anda.
## Langkah 3: Menambahkan Bentuk Busur Pertama
Di sinilah keseruan dimulai! Mari tambahkan bentuk lengkung pertama kita.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Baris kode ini menambahkan bentuk lengkung ke lembar kerja pertama. Parameter menentukan koordinat lengkung dan sudut yang menentukan kelengkungannya. 
## Langkah 4: Sesuaikan Tampilan Arc
Bentuk lengkung kosong bagaikan kanvas tanpa cat—perlu sedikit sentuhan!
### Atur Warna Isian Busur
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Ini membuat lengkungan menjadi biru pekat. Anda dapat mengubah warna ke rona apa pun yang Anda suka dengan menukar`Color.Blue` untuk warna lain.
### Atur Penempatan Busur
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Mengatur penempatan ke "FreeFloating" memungkinkan lengkungan bergerak secara independen dari batas sel, memberikan Anda fleksibilitas dalam pemosisian.
### Sesuaikan Berat dan Gaya Garis
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Di sini, Anda menentukan ketebalan dan gaya garis, membuatnya lebih menonjol dan menarik secara visual.
## Langkah 5: Menambahkan Bentuk Lengkung Lainnya
Mengapa berhenti di satu? Mari tambahkan bentuk lengkung lain untuk memperkaya tampilan Excel kita.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Seperti lengkungan pertama, lengkungan ini ditambahkan pada posisi berbeda—di sinilah keajaiban desain terjadi!
## Langkah 6: Kustomisasi Arc Kedua
Ayo berikan sedikit kepribadian pada busur kedua kita juga!
### Ubah Warna Garis Lengkung
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Kami konsisten dengan warna biru, tetapi Anda selalu dapat mencampur dan mencocokkan untuk melihat apa yang paling cocok dengan desain Anda!
### Tetapkan Properti Mirip dengan Arc Pertama
Pastikan untuk meniru pilihan estetika tersebut:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Di sini, Anda hanya perlu memastikan bahwa lengkungan kedua cocok dengan lengkungan pertama, sehingga menciptakan tampilan yang kohesif pada seluruh lembar kerja Anda.
## Langkah 7: Simpan Buku Kerja Anda
Tidak ada karya yang lengkap tanpa disimpan, bukan? Saatnya menulis lengkungan Anda ke dalam berkas Excel.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Baris ini menyimpan busur yang baru Anda buat ke dalam berkas Excel bernama "book1.out.xls" di direktori yang Anda tentukan.
## Kesimpulan
Selamat! Anda baru saja menguasai dasar-dasar penambahan kontrol lengkung dengan titik koneksi di lembar Excel Anda menggunakan Aspose.Cells untuk .NET. Fungsionalitas ini tidak hanya memperindah lembar kerja Anda tetapi juga dapat membuat data yang rumit lebih mudah dicerna. Apakah Anda seorang pengembang berpengalaman atau baru memulai, elemen visual ini dapat mengubah laporan Anda dari hambar menjadi hebat.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET canggih yang memungkinkan pengembang untuk membuat dan memanipulasi file Excel secara terprogram.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya! Anda dapat mencoba uji coba gratis. Kunjungi[tautan ini](https://releases.aspose.com/) untuk memulai.
### Bagaimana cara menambahkan bentuk lain selain busur?
Anda dapat menggunakan berbagai kelas yang tersedia di namespace Aspose.Cells.Drawing untuk menambahkan berbagai bentuk seperti persegi panjang, lingkaran, dan banyak lagi.
### Jenis file apa yang dapat saya buat dengan Aspose.Cells?
Anda dapat membuat dan memanipulasi berbagai format Excel termasuk XLS, XLSX, CSV, dan banyak lagi.
### Apakah dukungan teknis tersedia untuk Aspose.Cells?
 Tentu saja! Anda dapat mengakses[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9) untuk bantuan.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
