---
title: Ubah Diagram Lingkaran
linktitle: Ubah Diagram Lingkaran
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Manfaatkan kekuatan Aspose.Cells for .NET untuk memodifikasi diagram pai Excel Anda dengan mudah. Ikuti tutorial ini untuk panduan langkah demi langkah.
weight: 16
url: /id/net/manipulating-chart-types/modify-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Diagram Lingkaran

## Perkenalan

Bahasa Indonesia: Pernahkah Anda bertanya-tanya bagaimana Anda dapat merapikan diagram pai tersebut di lembar Excel Anda? Diagram pai dapat menjadi cara yang fantastis untuk memvisualisasikan data, membuat audiens Anda tetap terlibat dan terinformasi. Namun, terkadang diagram tersebut tidak menceritakan kisah yang Anda inginkan langsung dari kotaknya. Di situlah Aspose.Cells untuk .NET berperan. Pustaka yang hebat ini memungkinkan Anda untuk memanipulasi file Excel secara terprogram, memberi Anda alat yang Anda butuhkan untuk menyesuaikan diagram pai Anda hingga ke detail terkecil. Dalam tutorial ini, kita akan menyelami lebih dalam cara memodifikasi diagram pai menggunakan Aspose.Cells. Baik itu mengubah label data atau mengubah estetika diagram.

## Prasyarat

Sebelum kita menyelami seluk-beluk modifikasi diagram lingkaran, ada beberapa prasyarat yang harus Anda penuhi:

- Pengetahuan Dasar C#: Pemahaman mendasar tentang pemrograman C# akan membantu Anda mengikutinya dengan mudah.
- Aspose.Cells untuk .NET: Anda harus menginstal pustaka Aspose.Cells. Apakah Anda memutuskan untuk menggunakan versi lengkap atau memilih uji coba gratis, pastikan pustaka tersebut siap digunakan.
- Visual Studio atau IDE C# apa pun: Anda memerlukan lingkungan untuk menulis dan mengeksekusi kode C# Anda.
-  File Contoh Excel: Untuk tutorial ini, file Excel contoh bernama`sampleModifyPieChart.xlsx` akan digunakan.

 Anda dapat mengunduh pustaka Aspose.Cells[Di Sini](https://releases.aspose.com/cells/net/).

## Paket Impor

Langkah pertama dalam perjalanan kita adalah mengimpor paket-paket yang diperlukan ke dalam proyek C# kita. Berikut ini cara melakukannya:

## Siapkan Proyek Anda

Untuk memulai, buka IDE C# Anda (Visual Studio sangat disarankan) dan buat proyek baru:

1. Buka Visual Studio.
2. Pilih "Buat proyek baru."
3. Pilih aplikasi konsol C#.
4.  Beri nama proyek Anda (misalnya,`ModifyPieChartDemo`).
5. Klik Buat.

## Instal Aspose.Cells

Setelah proyek Anda siap, saatnya menambahkan pustaka Aspose.Cells. Anda dapat menginstalnya menggunakan NuGet:

1. Di “Solution Explorer” klik kanan pada proyek Anda.
2. Pilih Kelola Paket NuGet.
3. Navigasi ke tab Telusuri.
4. Cari Aspose.Cells.
5. Klik Instal dan terima semua perjanjian lisensi.

Sekarang setelah Anda menginstal pustaka, mari impor namespace yang diperlukan dalam kode Anda.

## Mengimpor Ruang Nama

 Di bagian atas Anda`Program.cs` file, impor namespace berikut:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Setelah itu selesai, sekarang kita siap beralih ke kode sebenarnya!

## Langkah 1: Tentukan Direktori Input dan Output

Mari kita mulai dengan menentukan direktori untuk file input dan output Anda. Di sinilah Anda menentukan lokasi file Excel dan tempat Anda ingin menyimpan file yang dimodifikasi.

 Di dalam kamu`Main` metode, ketik kode berikut:

```csharp
// Direktori keluaran
string outputDir = "Your Output Directory Path";

// Direktori sumber
string sourceDir = "Your Document Directory Path";
```

 Pastikan untuk mengganti`Your Output Directory Path` Dan`Your Document Directory Path` dengan jalur sebenarnya pada sistem Anda.

## Langkah 2: Buka Buku Kerja yang Ada

 Selanjutnya, kita perlu membuka file Excel yang berisi diagram lingkaran yang ingin Anda ubah. Untuk melakukan ini, gunakan`Workbook` kelas:

```csharp
// Buka berkas yang ada.
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

 Dalam cuplikan ini, kami membuat yang baru`Workbook` objek dan memuat berkas Excel kita ke dalamnya.

## Langkah 3: Akses Lembar Kerja

Sekarang, mari kita bahas lembar kerja tertentu yang berisi diagram pai. Kita akan menganggap diagram pai ada di lembar kerja kedua (indeks 1):

```csharp
// Dapatkan bagan desainer di lembar kedua.
Worksheet sheet = workbook.Worksheets[1];
```

 Dengan mengakses`Worksheets` koleksi, kita bisa mendapatkan lembar spesifik yang kita butuhkan.

## Langkah 4: Dapatkan Bagannya

Sekarang, kita siap untuk mengakses diagram itu sendiri. Dengan asumsi hanya ada satu diagram pada lembar kerja itu, kita dapat mengambilnya secara langsung:

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Di sini, kita mengambil bagan pertama dari lembar kerja yang ditentukan.

## Langkah 5: Akses Label Data

Sekarang tibalah bagian yang menarik—memodifikasi label data pada diagram pai. Mari kita akses label data dari rangkaian data:

```csharp
// Dapatkan label data dalam rangkaian data titik data ketiga.
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

Dengan baris ini, kami menargetkan label data secara khusus untuk titik ketiga seri data kami. 

## Langkah 6: Ubah Teks Label

Selanjutnya, saatnya mengubah apa yang tertulis pada label tersebut. Untuk contoh kita, kita akan memperbaruinya menjadi "United Kingdom, 400K":

```csharp
// Ubah teks label.
datalabels.Text = "United Kingdom, 400K";
```

Seperti itu saja, kami telah memperbarui labelnya! 

## Langkah 7: Simpan Buku Kerja

Sekarang setelah kita membuat perubahan, mari simpan buku kerja yang telah dimodifikasi. 

```csharp
// Simpan berkas excel.
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

Baris ini menyimpan buku kerja ke direktori keluaran yang ditentukan. 

## Langkah 8: Konfirmasi Eksekusi

Terakhir, mari kita keluarkan pesan konfirmasi untuk memastikan semuanya berjalan lancar:

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

Ini memberi Anda sedikit kepastian bahwa perubahan Anda telah dibuat seperti yang diharapkan.

# Kesimpulan

Nah, itu dia! Hanya dengan beberapa langkah sederhana, Anda telah berhasil memodifikasi diagram pai menggunakan Aspose.Cells untuk .NET. Pustaka canggih ini tidak hanya memudahkan Anda memanipulasi file Excel, tetapi juga memungkinkan Anda untuk mempersonalisasi visualisasi data Anda untuk dampak yang maksimal. Jika Anda menangani presentasi data dalam pekerjaan Anda, meluangkan waktu untuk mempelajari cara menggunakan Aspose.Cells pasti akan membuahkan hasil. Jadi, silakan, bereksperimenlah dengan diagram tersebut, dan lihat bagaimana Anda dapat menghidupkan data Anda!

# Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells untuk .NET?  
Aspose.Cells untuk .NET adalah pustaka hebat yang dirancang untuk membuat, memanipulasi, dan mengonversi file Excel secara terprogram tanpa memerlukan Microsoft Excel.

### Bisakah saya memodifikasi bagan selain bagan pai?  
Tentu saja! Aspose.Cells mendukung berbagai jenis bagan, termasuk bagan batang, garis, dan area, yang memungkinkan visualisasi data yang fleksibel.

### Apakah ada versi gratis Aspose.Cells?  
Ya! Aspose menawarkan versi uji coba gratis yang memungkinkan Anda menguji pustaka sebelum membeli.

### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?  
Anda dapat menemukan dukungan di forum Aspose, tempat anggota komunitas dan staf Aspose dapat membantu Anda.

### Apakah saya perlu menginstal Microsoft Excel untuk menggunakan Aspose.Cells?  
Tidak, Aspose.Cells bekerja secara independen dari Microsoft Excel. Anda tidak perlu menginstalnya di sistem Anda.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
