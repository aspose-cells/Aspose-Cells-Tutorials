---
title: Membuat Diagram Lingkaran
linktitle: Membuat Diagram Lingkaran
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara membuat diagram pai di Excel menggunakan Aspose.Cells for .NET dengan panduan langkah demi langkah ini. Visualisasikan data Anda dengan mudah.
weight: 12
url: /id/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Diagram Lingkaran

## Perkenalan

Membuat bagan sangat penting untuk merepresentasikan data secara visual, dan bagan pai adalah salah satu cara paling populer untuk mengilustrasikan bagaimana bagian-bagian membentuk keseluruhan. Dengan Aspose.Cells for .NET, Anda dapat dengan mudah mengotomatiskan pembuatan bagan pai dalam file Excel. Dalam tutorial ini, kita akan membahas cara membuat bagan pai dari awal menggunakan Aspose.Cells for .NET, dengan panduan langkah demi langkah untuk mempermudah dan mempercepat prosesnya. Baik Anda baru menggunakan alat ini atau ingin meningkatkan keterampilan otomatisasi Excel, panduan ini akan membantu Anda!

## Prasyarat

Sebelum menyelami kode, pastikan Anda telah menyiapkan hal berikut:

1.  Aspose.Cells untuk Pustaka .NET: Pastikan Anda telah menginstal Aspose.Cells di proyek Anda. Jika Anda belum menginstalnya, Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/cells/net/).
2. Lingkungan Pengembangan .NET: Pastikan proyek Anda diatur untuk menggunakan .NET Framework atau .NET Core.
3. Pengetahuan Dasar C#: Anda harus nyaman dengan pemrograman C#, khususnya pemrograman berorientasi objek (OOP).

 Untuk pengguna tingkat lanjut, lisensi sementara dapat diterapkan untuk membuka semua fitur Aspose.Cells. Anda dapat meminta satu dari[Di Sini](https://purchase.aspose.com/temporary-license/).

## Paket Impor

Untuk memulai, impor namespace dan paket yang diperlukan untuk tutorial ini. Ini termasuk operasi I/O dasar dan paket Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Langkah 1: Buat Buku Kerja Baru

 Pertama, kita perlu membuat sebuah instance dari`Workbook` kelas, yang mewakili berkas Excel. Buku kerja berisi beberapa lembar, dan untuk contoh kita, kita akan bekerja dengan dua lembar—satu untuk data dan satu untuk diagram pai.

```csharp
Workbook workbook = new Workbook();
```

Ini menginisialisasi buku kerja Excel yang baru. Namun, ke mana data tersebut akan disimpan? Mari kita bahas hal itu di langkah berikutnya.

## Langkah 2: Tambahkan Data ke Lembar Kerja

Setelah buku kerja dibuat, kita perlu mengakses lembar kerja pertama dan memberinya nama. Di sinilah kita akan memasukkan data yang diperlukan untuk diagram pai.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Sekarang, kita dapat memasukkan beberapa data penjualan dummy yang mewakili berbagai wilayah:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Di sini, kami menambahkan dua kolom: satu untuk wilayah dan satu lagi untuk angka penjualan. Data ini akan ditampilkan dalam diagram lingkaran.

## Langkah 3: Tambahkan Lembar Bagan

Berikutnya, mari tambahkan lembar kerja terpisah untuk menampung diagram lingkaran.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Lembar baru ini akan menjadi tempat diagram pai. Memberinya nama seperti "Diagram" memastikan bahwa pengguna mengetahui apa yang diharapkan saat mereka membuka berkas tersebut.

## Langkah 4: Buat Diagram Lingkaran

Sekarang saatnya membuat diagram yang sebenarnya. Kita akan tentukan bahwa kita menginginkan diagram pai, dan kita akan tentukan posisinya pada lembar tersebut.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 Metode`Add()`menerima parameter untuk jenis grafik (dalam kasus ini,`ChartType.Pie`), dan lokasinya pada lembar kerja. Angka-angka tersebut mewakili posisi baris dan kolom.

## Langkah 5: Sesuaikan Tampilan Bagan

Bagan pai tidak akan lengkap tanpa beberapa penyesuaian! Mari buat bagan kita menarik secara visual dengan mengubah warna, label, dan judul.

### Tetapkan Judul Bagan
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Sesuaikan Luas Plot
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Kami mengatur isian gradien untuk area plot dan menyembunyikan batas agar terlihat lebih rapi.

## Langkah 6: Tentukan Data Bagan

 Saatnya untuk menghubungkan grafik ke data kita.`NSeries` properti bagan mengikat angka penjualan dan wilayah ke bagan pai.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 Baris pertama menentukan bahwa kita menggunakan data penjualan dari sel`B2:B8` Kami juga memberi tahu grafik untuk menggunakan nama wilayah dari`A2:A8` sebagai label kategori.

## Langkah 7: Tambahkan Label Data

Menambahkan label langsung ke segmen diagram dapat mempermudah pemahaman. Mari sertakan nama wilayah dan nilai penjualan dalam irisan diagram lingkaran.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Langkah 8: Sesuaikan Area dan Legenda Bagan

Terakhir, mari kita berikan sentuhan akhir pada area grafik dan legenda. Ini akan menyempurnakan tampilan grafik secara keseluruhan.

### Area Bagan
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legenda
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Langkah 9: Simpan Buku Kerja

Terakhir, kita simpan buku kerja ke dalam file Excel. Anda dapat menentukan direktori output dan nama file sesuai kebutuhan.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Kesimpulan

Membuat diagram lingkaran dengan Aspose.Cells untuk .NET adalah proses yang mudah dan dapat disesuaikan. Dengan mengikuti panduan ini, Anda dapat membuat diagram yang tampak profesional yang menyampaikan wawasan berharga hanya dalam beberapa langkah. Baik untuk pelaporan bisnis maupun tujuan pendidikan, menguasai pembuatan diagram akan meningkatkan keterampilan otomatisasi Excel Anda. Ingat, Aspose.Cells menyediakan fleksibilitas yang Anda butuhkan untuk membuat file Excel yang menakjubkan dan berbasis data dengan mudah.

## Pertanyaan yang Sering Diajukan

### Bisakah saya membuat jenis bagan lain menggunakan Aspose.Cells untuk .NET?
Ya! Aspose.Cells mendukung berbagai jenis bagan, termasuk bagan batang, bagan garis, dan diagram sebar.

### Apakah saya memerlukan lisensi berbayar untuk menggunakan Aspose.Cells untuk .NET?
Anda dapat menggunakan versi gratis dengan beberapa batasan. Untuk fitur lengkap, Anda memerlukan lisensi, yang dapat Anda beli[Di Sini](https://purchase.aspose.com/buy).

### Bisakah saya mengekspor bagan ke format seperti PDF atau gambar?
Tentu saja! Aspose.Cells memungkinkan Anda mengekspor grafik ke berbagai format, termasuk PDF dan PNG.

### Apakah mungkin untuk menata setiap irisan pai dengan warna yang berbeda?
 Ya, Anda dapat menerapkan warna yang berbeda pada setiap irisan dengan mengatur`IsColorVaried` properti untuk`true`, seperti yang ditunjukkan dalam tutorial.

### Bisakah saya mengotomatiskan pembuatan beberapa bagan dalam satu buku kerja?
Ya, Anda dapat membuat dan menyesuaikan bagan sebanyak yang diperlukan dalam satu file Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
