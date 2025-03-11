---
title: Buat Garis dengan Bagan Penanda Data
linktitle: Buat Garis dengan Bagan Penanda Data
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara membuat bagan Garis dengan Penanda Data di Excel menggunakan Aspose.Cells for .NET. Ikuti panduan langkah demi langkah ini untuk membuat dan menyesuaikan bagan dengan mudah.
weight: 10
url: /id/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Garis dengan Bagan Penanda Data

## Perkenalan

Pernahkah Anda bertanya-tanya bagaimana cara membuat grafik yang memukau di Excel secara terprogram? Nah, bersiaplah, karena hari ini kita akan membahas cara membuat Grafik Garis dengan Penanda Data menggunakan Aspose.Cells untuk .NET. Tutorial ini akan memandu Anda di setiap langkah, memastikan Anda memiliki pemahaman yang baik tentang pembuatan grafik, bahkan jika Anda baru saja memulai dengan Aspose.Cells.

## Prasyarat

Sebelum kita mulai, pastikan Anda telah menyiapkan semua hal agar dapat mengikutinya dengan lancar.

1. Aspose.Cells untuk Pustaka .NET – Anda perlu menginstal ini. Anda dapat mengambilnya[Di Sini](https://releases.aspose.com/cells/net/).
2. .NET Framework – Pastikan lingkungan pengembangan Anda disiapkan dengan versi .NET terbaru.
3. IDE (Integrated Development Environment) – Visual Studio direkomendasikan.
4.  Lisensi Aspose.Cells yang valid – Jika Anda belum memilikinya, Anda dapat meminta[lisensi sementara](https://purchase.aspose.com/temporary-license/) atau lihat mereka[uji coba gratis](https://releases.aspose.com/).

Siap untuk memulai? Mari kita bahas!

## Mengimpor Paket yang Diperlukan

Untuk memulai, pastikan Anda mengimpor namespace berikut ke dalam proyek Anda. Namespace ini akan menyediakan kelas dan metode yang diperlukan untuk membuat bagan Anda.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Setelah Anda menguasainya, kita dapat mulai membuat kode!

## Langkah 1: Siapkan Buku Kerja dan Lembar Kerja Anda

Hal pertama yang harus dilakukan, Anda perlu membuat buku kerja baru dan mengakses lembar kerja pertama.

```csharp
//Direktori keluaran
static string outputDir = "Your Document Directory";
		
// Membuat contoh buku kerja
Workbook workbook = new Workbook();

// Akses lembar kerja pertama
Worksheet worksheet = workbook.Worksheets[0];
```

Anggap buku kerja sebagai berkas Excel dan lembar kerja sebagai lembar tertentu di dalamnya. Dalam kasus ini, kita bekerja dengan lembar pertama.

## Langkah 2: Isi Lembar Kerja dengan Data

Sekarang setelah kita memiliki lembar kerja, mari kita isi dengan beberapa data. Kita akan membuat titik data acak untuk dua rangkaian nilai.

```csharp
// Tetapkan judul kolom
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Data acak untuk membuat grafik
Random R = new Random();

// Buat data acak dan simpan di sel
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Di sini, kami menggunakan angka acak untuk mensimulasikan data, tetapi dalam aplikasi kehidupan nyata, Anda dapat mengisinya dengan nilai sebenarnya dari kumpulan data Anda.

## Langkah 3: Tambahkan Bagan ke Lembar Kerja

Berikutnya, kita tambahkan bagan tersebut ke lembar kerja dan pilih jenisnya – dalam kasus ini, Bagan Garis dengan Penanda Data.

```csharp
// Tambahkan bagan ke lembar kerja
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Akses grafik yang baru dibuat
Chart chart = worksheet.Charts[idx];
```

Potongan kode ini menambahkan diagram garis dengan penanda data ke lembar kerja, menempatkannya dalam rentang tertentu (1,3 hingga 20,20). Cukup mudah, bukan?

## Langkah 4: Sesuaikan Tampilan Bagan

Setelah diagram dibuat, Anda dapat menatanya sesuai keinginan. Mari ubah latar belakang, judul, dan gaya diagram.

```csharp
// Mengatur gaya grafik
chart.Style = 3;

// Tetapkan nilai penskalaan otomatis ke benar
chart.AutoScaling = true;

// Atur warna latar depan menjadi putih
chart.PlotArea.Area.ForegroundColor = Color.White;

//Tetapkan properti judul bagan
chart.Title.Text = "Sample Chart";

// Tetapkan jenis grafik
chart.Type = ChartType.LineWithDataMarkers;
```

Di sini, kami memberikan bagan tampilan yang bersih dengan menetapkan latar belakang putih, penskalaan otomatis, dan memberinya judul yang bermakna.

## Langkah 5: Tentukan Seri dan Plot Titik Data

Sekarang setelah bagan kita tampak bagus, kita perlu menentukan rangkaian data yang akan diplot.

```csharp
// Tetapkan Properti judul sumbu kategori
chart.CategoryAxis.Title.Text = "Units";

// Tentukan dua seri untuk grafik tersebut
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Seri ini sesuai dengan rentang titik data yang telah kita isi sebelumnya.

## Langkah 6: Tambahkan Warna dan Sesuaikan Penanda Seri

Mari buat bagan ini lebih menarik dengan menambahkan warna khusus ke penanda data kita.

```csharp
// Sesuaikan seri pertama
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Sesuaikan seri kedua
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Dengan menyesuaikan warna, Anda membuat bagan tidak hanya fungsional tetapi juga menarik secara visual!

## Langkah 7: Tetapkan Nilai X dan Y untuk Setiap Seri

Terakhir, mari kita tetapkan nilai X dan Y untuk setiap seri kita.

```csharp
// Tetapkan nilai X dan Y dari seri pertama
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Tetapkan nilai X dan Y dari seri kedua
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Nilainya berdasarkan pada data yang kita isi pada langkah 2.

## Langkah 8: Simpan Buku Kerja

Sekarang semuanya sudah diatur, mari simpan buku kerja, sehingga kita dapat melihat bagan tersebut dalam aksi.

```csharp
// Simpan buku kerja
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Selesai! Anda baru saja membuat diagram garis dengan penanda data menggunakan Aspose.Cells for .NET.

## Kesimpulan

Membuat bagan secara terprogram di Excel mungkin tampak sulit, tetapi dengan Aspose.Cells untuk .NET, semudah mengikuti resep langkah demi langkah. Dari menyiapkan buku kerja hingga menyesuaikan tampilan bagan, pustaka canggih ini menangani semuanya. Baik Anda membuat laporan, dasbor, atau visualisasi data, Aspose.Cells memungkinkan Anda melakukannya dengan mudah.

## Pertanyaan yang Sering Diajukan

### Bisakah saya menyesuaikan grafik lebih lanjut?  
Tentu saja! Aspose.Cells menawarkan banyak sekali opsi penyesuaian, mulai dari font hingga garis kisi dan masih banyak lagi.

### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?  
 Ya, lisensi diperlukan untuk fungsionalitas penuh. Anda bisa mendapatkannya[lisensi sementara](https://purchase.aspose.com/temporary-license/) atau mulai dengan[uji coba gratis](https://releases.aspose.com/).

### Bagaimana cara menambahkan lebih banyak seri data?  
 Cukup tambahkan seri tambahan menggunakan`NSeries.Add` metode, menentukan rentang sel untuk data baru.

### Bisakah saya mengekspor bagan sebagai gambar?  
 Ya, Anda dapat mengekspor grafik secara langsung sebagai gambar menggunakan`Chart.ToImage` metode.

### Apakah Aspose.Cells mendukung grafik 3D?  
Ya, Aspose.Cells mendukung berbagai jenis bagan, termasuk bagan 3D.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
