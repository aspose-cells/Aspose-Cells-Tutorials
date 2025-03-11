---
title: Bagan Render
linktitle: Bagan Render
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara membuat grafik dalam .NET menggunakan Aspose.Cells. Ikuti tutorial langkah demi langkah kami untuk membuat visual yang memukau dengan mudah.
weight: 10
url: /id/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bagan Render

## Perkenalan

Bagan merupakan elemen penting dalam penyajian dan analisis data, yang membuat informasi yang rumit menjadi mudah dicerna. Jika Anda bekerja dengan .NET dan perlu membuat bagan secara terprogram, Aspose.Cells adalah pustaka canggih yang menyediakan fitur intuitif dan canggih untuk menangani file dan bagan Excel. Dalam panduan ini, kami akan memandu Anda melalui proses pembuatan bagan menggunakan Aspose.Cells untuk .NET. Bersiaplah untuk menyelami tutorial terperinci ini, yang dirancang agar menarik dan mudah diikuti!

## Prasyarat

Sebelum kita mulai membuat kode, pastikan Anda telah menyiapkan semuanya. Berikut ini yang Anda perlukan:

1. Lingkungan .NET: Pastikan Anda telah menyiapkan lingkungan pengembangan .NET. Anda dapat menggunakan Visual Studio atau IDE lain yang mendukung .NET.
2.  Aspose.Cells untuk .NET: Anda perlu menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya dari[Halaman rilis Aspose](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami contoh dengan lebih baik, tetapi jangan khawatir jika Anda baru—panduan ini akan menjelaskan semuanya langkah demi langkah!

## Paket Impor

Langkah pertama dalam perjalanan coding Anda adalah mengimpor paket-paket yang diperlukan. Buka proyek Anda di IDE dan tambahkan namespace berikut:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Ruang nama ini akan memberi Anda akses ke fungsionalitas yang ditawarkan oleh pustaka Aspose.Cells, yang memungkinkan Anda membuat dan memanipulasi bagan dengan mudah.


Sekarang setelah kita membahas prasyarat dan impor, mari selami seluk-beluk pembuatan bagan! Kita akan menguraikannya menjadi langkah-langkah yang jelas dan mudah dikelola.

## Langkah 1: Siapkan Direktori Output Anda

Sebelum membuat buku kerja dan bagan, kita perlu menentukan di mana output akan disimpan. Dengan demikian, saat bagan dibuat, Anda akan tahu persis di mana menemukannya.

```csharp
string outputDir = "Your Output Directory"; // Tentukan direktori keluaran di sini.
```

Pastikan untuk mengganti "Direktori Keluaran Anda" dengan jalur tempat Anda ingin menyimpan gambar bagan Anda.

## Langkah 2: Buat Buku Kerja

Selanjutnya, kita akan membuat buku kerja baru. Di sinilah semua keajaiban terjadi!

```csharp
Workbook workbook = new Workbook();
```

 Baris ini membuat contoh baru dari`Workbook` kelas, yang memungkinkan kita bekerja dengan lembaran dan bagan.

## Langkah 3: Tambahkan Lembar Kerja Baru

Sekarang setelah kita memiliki buku kerja, saatnya untuk menambahkan lembar kerja baru. Bayangkan lembar kerja sebagai halaman-halaman berbeda dalam buku catatan, tempat Anda dapat menyimpan data secara teratur.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Di sini, kita menambahkan lembar kerja baru dan memperoleh referensi ke lembar kerja tersebut. Anda akan bekerja dengan lembar kerja ini untuk memasukkan data dan diagram Anda.

## Langkah 4: Masukkan Nilai Sampel

Setelah lembar kerja kita dibuat, mari tambahkan beberapa contoh data ke dalam sel. Data ini akan menjadi dasar bagan Anda, jadi pilihlah nilai yang sesuai dengan jenis bagan Anda!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

Dalam cuplikan ini, kita mengisi sel "A1" hingga "A3" dengan beberapa nilai numerik dan sel "B1" hingga "B3" dengan serangkaian nilai lainnya. Jangan ragu untuk menyesuaikan angka-angka ini agar sesuai dengan kebutuhan Anda!

## Langkah 5: Buat Bagan

Sekarang, saatnya membuat bagan Anda. Kita akan menambahkan jenis bagan kolom, yang sangat bagus untuk membandingkan nilai.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Di sini, kami menambahkan bagan di lokasi yang ditentukan dengan mendefinisikan tata letaknya: rangkaian angka pertama mewakili posisi bagan pada kisi.

## Langkah 6: Menambahkan Seri Data ke Bagan

Setelah bagan dibuat, sekarang kita perlu mengikatnya ke data yang kita masukkan pada langkah sebelumnya.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Garis ini menghubungkan rangkaian data grafik dengan nilai dalam sel "A1" hingga "B3". Ini berarti grafik Anda akan secara visual menyajikan data sebagaimana yang dimaksudkan.

## Langkah 7: Simpan Bagan sebagai Gambar

Sekarang mari ubah bagan kita ke dalam format gambar, sehingga dapat dibagikan dan dilihat dengan mudah.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

Pada langkah ini, kami menyimpan grafik sebagai gambar EMF (Enhanced Metafile) di direktori keluaran yang ditentukan. Anda juga dapat menyimpannya dalam format lain seperti BMP atau PNG.

## Langkah 8: Ubah Grafik ke Bitmap

Jika Anda lebih suka bekerja dengan bitmap, berikut ini cara mengonversi bagan Anda ke format Bitmap.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Ini akan menyimpan diagram Anda sebagai gambar BMP. Ingat, file BMP cenderung lebih besar tetapi kualitasnya sangat tinggi!

## Langkah 9: Rendering dengan Opsi Lanjutan

Kita juga dapat menyajikan grafik dengan beberapa opsi gambar tingkat lanjut untuk kualitas dan resolusi yang lebih baik. Mari kita atur beberapa opsi:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Opsi ini membantu meningkatkan kualitas visual gambar yang Anda hasilkan, terutama berguna untuk presentasi atau publikasi.

## Langkah 10: Ubah Bagan menjadi Gambar dengan Opsi Lanjutan

Sekarang mari kita konversi grafik menggunakan opsi lanjutan yang baru saja kita atur.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Ini menyimpan bagan Anda sebagai berkas PNG dengan pengaturan kualitas yang ditingkatkan.

## Langkah 11: Mengekspor Bagan ke PDF

Terakhir, jika Anda menginginkan dokumen yang bagus dan mudah dibagikan, Anda dapat mengekspor bagan Anda langsung ke format PDF.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Langkah ini akan membuat PDF yang berisi bagan Anda, membuatnya sempurna untuk laporan digital atau dibagikan dengan kolega.

## Kesimpulan 

Selamat! Anda telah berhasil membuat bagan menggunakan Aspose.Cells for .NET. Pustaka canggih ini menyederhanakan pembuatan dan manipulasi file Excel dan bagan, membuat data Anda jauh lebih mudah diakses dan menarik secara visual. Baik Anda sedang mempersiapkan laporan, analisis, atau presentasi, bagan memberikan dampak yang signifikan, dan dengan Aspose, Anda dapat membuatnya secara terprogram dengan mudah.

## Pertanyaan yang Sering Diajukan

### Jenis bagan apa yang dapat saya buat dengan Aspose.Cells untuk .NET?
Anda dapat membuat berbagai macam bagan, termasuk bagan kolom, garis, pai, dan batang, antara lain.

### Bisakah saya menyesuaikan tampilan grafik?
Ya, Aspose.Cells memungkinkan kustomisasi yang luas, termasuk warna, gaya, dan elemen bagan.

### Apakah ada uji coba gratis yang tersedia?
Tentu saja! Anda dapat mengunduh versi uji coba gratis dari[Di Sini](https://releases.aspose.com/).

### Di mana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Anda dapat menemukan dukungan dan sumber daya komunitas di[Forum Dukungan Aspose](https://forum.aspose.com/c/cells/9).

### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?
 Ya, lisensi diperlukan untuk penggunaan lanjutan setelah masa uji coba, tetapi Anda dapat mengajukan lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
