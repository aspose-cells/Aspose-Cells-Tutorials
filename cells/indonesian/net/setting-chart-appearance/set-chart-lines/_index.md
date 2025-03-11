---
title: Tetapkan Garis Grafik
linktitle: Tetapkan Garis Grafik
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyesuaikan garis bagan di Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah terperinci kami.
weight: 14
url: /id/net/setting-chart-appearance/set-chart-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tetapkan Garis Grafik

## Perkenalan

Membuat bagan yang menarik secara visual dan informatif sangat penting dalam penyajian data. Baik Anda seorang analis data, manajer bisnis, atau hanya seseorang yang suka mengatur data, bagan dapat meningkatkan cara Anda menyajikan informasi secara signifikan. Tutorial ini akan memandu Anda melalui proses pengaturan garis bagan menggunakan Aspose.Cells for .NET, pustaka yang hebat untuk memanipulasi file Excel. Pada akhirnya, Anda akan mengetahui cara membuat bagan yang memukau yang dilengkapi dengan penyesuaian untuk membuat data Excel Anda menonjol!

## Prasyarat

Sebelum masuk ke bagian pengkodean, pastikan Anda dilengkapi dengan hal berikut:

- Visual Studio: Pastikan Anda telah menginstal Visual Studio. Sangat disarankan untuk menggunakan versi terbaru guna memanfaatkan semua fitur.
- .NET Framework: Proyek Anda harus berbasis pada .NET Framework (atau .NET Core) tempat Anda akan mengimplementasikan Aspose.Cells.
-  Aspose.Cells untuk .NET: Unduh dan instal Aspose.Cells dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
- Pemahaman Dasar C#: Keakraban dengan bahasa pemrograman C# akan membantu saat membuat kode.

## Paket Impor

Untuk memulai dengan Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan ke dalam proyek Anda. Ini akan memungkinkan Anda untuk mengakses semua fitur dan fungsi menarik yang ditawarkan Aspose.Cells. Berikut cara mengimpor paket ke dalam file C# Anda:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Mari kita uraikan prosesnya menjadi beberapa langkah yang dapat dikelola sehingga Anda dapat mengikutinya dengan mudah.

## Langkah 1: Tentukan Direktori Output Anda

Pertama-tama, Anda memerlukan tempat untuk menyimpan berkas Excel yang baru Anda buat. Tentukan direktori output di bagian atas kode Anda seperti ini:

```csharp
// Direktori keluaran
string outputDir = "Your Output Directory";
```

 Penjelasan: Ganti "Direktori Output Anda" dengan jalur tempat Anda ingin Aspose.Cells menyimpan file, seperti`C:\\MyExcelFiles\\`.

## Langkah 2: Membuat Instansi Objek Buku Kerja

Sekarang, kita akan membuat objek buku kerja, yang berfungsi sebagai wadah bagi lembar kerja Anda.

```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
```

 Penjelasan: Baris ini membuat contoh dari`Workbook`kelas dari pustaka Aspose.Cells. Mirip seperti membuka berkas Excel kosong baru tempat Anda dapat mulai menambahkan lembar dan data.

## Langkah 3: Referensi Lembar Kerja

Selanjutnya, Anda perlu bekerja dengan lembar tertentu di buku kerja Anda. Kita akan mengambil lembar kerja pertama.

```csharp
// Mendapatkan referensi lembar kerja yang baru ditambahkan dengan meneruskan indeks lembar kerjanya
Worksheet worksheet = workbook.Worksheets[0];
```

 Penjelasan: Lembar kerja diindeks mulai dari 0, jadi`worksheets[0]` mengacu pada lembar kerja pertama.

## Langkah 4: Tambahkan Nilai Sampel ke Sel

Mari isi beberapa sel dengan data yang nantinya akan kita gunakan untuk membuat bagan kita.

```csharp
// Menambahkan nilai sampel ke sel
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Penjelasan: Di sini kita mengisi sel "A1" hingga "A3" dan "B1" hingga "B3" dengan beberapa nilai numerik. Nilai-nilai ini akan diplot dalam bagan kita nanti.

## Langkah 5: Tambahkan Bagan ke Lembar Kerja

Sekarang, saatnya membuat bagan! Kita akan menambahkan jenis bagan kolom.

```csharp
// Menambahkan bagan ke lembar kerja
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

Penjelasan: Baris ini menambahkan bagan kolom pada koordinat tertentu di lembar kerja. Parameter menentukan di mana bagan akan digambar di grid.

## Langkah 6: Akses Bagan yang Baru Ditambahkan

Sekarang Anda perlu merujuk pada bagan yang baru Anda buat.

```csharp
// Mengakses contoh grafik yang baru ditambahkan
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Penjelasan: Ini memberi Anda kendali atas contoh bagan yang memungkinkan Anda menyesuaikan dan memberi gaya lebih lanjut.

## Langkah 7: Tambahkan Seri Data ke Bagan

Mari tambahkan rangkaian data untuk bagan kita.

```csharp
// Menambahkan SeriesCollection (sumber data bagan) ke bagan mulai dari sel "A1" hingga "B3"
chart.NSeries.Add("A1:B3", true);
```

Penjelasan: Baris ini memerintahkan bagan untuk menarik data dari rentang yang ditentukan. Parameter kedua menentukan apakah rentang data mencakup kategori.

## Langkah 8: Sesuaikan Tampilan Bagan

Sekarang saatnya bagian yang menyenangkan - menyesuaikan grafik Anda! Mari kita ubah beberapa warna.

```csharp
// Mengatur warna latar depan area plot
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// Mengatur warna latar depan area grafik
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// Mengatur warna latar depan area Koleksi Seri ke-1
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// Mengatur warna latar depan area titik Koleksi Seri ke-1
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// Mengisi area Koleksi Seri ke-2 dengan gradien
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

Penjelasan: Di sini, Anda menyesuaikan warna berbagai komponen diagram agar tampak mencolok. Setiap garis menargetkan area diagram yang berbeda.

## Langkah 9: Terapkan Gaya Garis

Berikutnya, Anda dapat mengubah gaya garis untuk rangkaian data Anda agar bagan Anda tidak hanya cantik, tetapi juga profesional.

```csharp
// Menerapkan gaya garis putus-putus pada garis SeriesCollection
chart.NSeries[0].Border.Style = Aspose.Cells.Drawing.LineType.Dot;

// Menerapkan gaya penanda segitiga pada penanda data SeriesCollection
chart.NSeries[0].Marker.MarkerStyle = Aspose.Cells.Charts.ChartMarkerType.Triangle;

// Mengatur bobot semua baris dalam SeriesCollection ke sedang
chart.NSeries[1].Border.Weight = Aspose.Cells.Drawing.WeightType.MediumLine;
```

Penjelasan: Kode di atas menyesuaikan batas rangkaian grafik, memberinya garis putus-putus dan bahkan mengubah penanda titik data menjadi segitiga. Semuanya tentang sentuhan pribadi!

## Langkah 10: Simpan Buku Kerja Anda

Sekarang, mari simpan kerja keras Anda ke dalam berkas Excel.

```csharp
// Menyimpan file Excel
workbook.Save(outputDir + "outputSettingChartLines.xlsx");
```

Penjelasan: Baris ini menyimpan buku kerja Anda dengan nama yang ditentukan di direktori keluaran yang Anda tentukan. Sekarang Anda dapat membukanya dan melihat bagan keren Anda!

## Langkah 11: Konfirmasi Eksekusi

Akhirnya, mari kita pastikan bahwa semuanya berjalan lancar.

```csharp
Console.WriteLine("SettingChartLines executed successfully.");
```

Penjelasan: Pesan sederhana untuk menginformasikan bahwa kode Anda dijalankan tanpa masalah.

## Kesimpulan

Selamat! Anda kini telah menguasai dasar-dasar pembuatan dan penyesuaian diagram menggunakan Aspose.Cells for .NET. Hanya dengan beberapa langkah sederhana, Anda dapat meningkatkan penyajian data, membuatnya lebih mudah dipahami dan menarik secara visual. Saat Anda bereksperimen dengan opsi penyesuaian lainnya, ingatlah bahwa diagram yang bagus tidak hanya menceritakan sebuah kisah, tetapi juga menarik perhatian audiens Anda.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells untuk .NET?  
Aspose.Cells untuk .NET adalah pustaka yang hebat untuk memanipulasi lembar kerja Excel dalam aplikasi .NET.

### Bisakah saya menggunakan Aspose.Cells secara gratis?  
 Ya, Aspose menyediakan uji coba gratis untuk menguji fungsionalitasnya. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/).

### Apakah ada dukungan yang tersedia untuk Aspose.Cells?  
 Tentu saja! Anda bisa mendapatkan dukungan melalui[Forum Aspose](https://forum.aspose.com/c/cells/9).

### Bisakah saya membuat jenis bagan lain menggunakan Aspose.Cells?  
Ya, Aspose mendukung berbagai jenis bagan termasuk bagan garis, bagan pai, dan bagan area.

### Bagaimana cara mendapatkan lisensi sementara untuk Aspose.Cells?  
 Anda dapat mengajukan permohonan[lisensi sementara](https://purchase.aspose.com/temporary-license/) melalui situs web Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
