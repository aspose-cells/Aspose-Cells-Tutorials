---
title: Mengubah Garis Kisi Utama dalam Bagan
linktitle: Mengubah Garis Kisi Utama dalam Bagan
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengubah garis kisi utama dalam bagan Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah terperinci kami.
weight: 11
url: /id/net/setting-chart-appearance/change-major-gridlines-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengubah Garis Kisi Utama dalam Bagan

## Perkenalan

Membuat bagan yang menarik secara visual di Excel sangat penting untuk penyajian data yang efektif. Baik Anda seorang analis data, manajer proyek, atau hanya seseorang yang tertarik dengan visualisasi data, memahami cara menyesuaikan bagan dapat meningkatkan laporan Anda secara signifikan. Dalam artikel ini, kita akan mempelajari cara mengubah garis kisi utama dalam bagan Excel menggunakan pustaka Aspose.Cells untuk .NET.

## Prasyarat

Sebelum memulai, ada beberapa hal yang perlu Anda siapkan untuk memastikan pengalaman yang lancar saat bekerja dengan Aspose.Cells:

- Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Di sinilah Anda akan menulis dan menjalankan kode Anda.
-  Aspose.Cells untuk .NET: Anda dapat mengunduh versi terbaru Aspose.Cells dari[situs web](https://releases.aspose.com/cells/net/) Jika Anda ingin bereksperimen sebelum membeli, Anda mungkin mempertimbangkan untuk mendaftar[uji coba gratis](https://releases.aspose.com/).
- Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan memudahkan untuk mengikuti contoh-contoh dalam tutorial ini.

Setelah semuanya siap, kita dapat mulai menulis kode!

## Paket Impor

Untuk bekerja dengan Aspose.Cells, langkah pertama adalah mengimpor paket yang diperlukan ke dalam proyek C# Anda. Buka proyek Visual Studio Anda dan sertakan perintah penggunaan berikut di bagian atas file C# Anda:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Paket ini memungkinkan Anda mengakses kelas dan metode yang Anda perlukan untuk membuat dan memodifikasi buku kerja dan bagan Excel.

Sekarang, mari kita uraikan prosesnya menjadi langkah-langkah yang terperinci dan mudah diikuti. Kita akan membuat bagan sederhana dengan beberapa data, lalu mengubah warna garis kisi utamanya.

## Langkah 1: Atur Direktori Output Anda

Hal pertama yang perlu Anda lakukan adalah menentukan tempat penyimpanan file Excel keluaran. Hal ini dilakukan dengan menentukan jalur direktori dalam kode Anda:

```csharp
// Direktori keluaran
string outputDir = "Your Output Directory"; // Perbarui dengan jalur yang Anda inginkan
```

 Mengganti`"Your Output Directory"` dengan jalur sebenarnya di mana Anda ingin menyimpan berkas Anda.

## Langkah 2: Membuat Instansi Objek Buku Kerja

 Selanjutnya, Anda perlu membuat instance baru dari`Workbook` kelas. Objek ini akan mewakili berkas Excel Anda, yang memungkinkan Anda memanipulasi isinya.

```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
```

Baris kode ini menginisialisasi buku kerja baru, yang akan menyediakan kanvas kosong untuk lembar kerja dan bagan kita.

## Langkah 3: Akses Lembar Kerja

 Setelah membuat buku kerja, Anda dapat mengakses lembar kerja default-nya. Lembar kerja di Aspose.Cells diindeks, jadi jika Anda menginginkan lembar kerja pertama, Anda merujuknya dengan indeks`0`.

```csharp
// Mendapatkan referensi lembar kerja yang baru ditambahkan dengan meneruskan indeks lembar kerjanya
Worksheet worksheet = workbook.Worksheets[0];
```

## Langkah 4: Isi Lembar Kerja dengan Data Sampel

Mari tambahkan beberapa contoh nilai ke dalam sel lembar kerja, yang akan berfungsi sebagai data untuk bagan kita. Ini penting karena bagan akan merujuk ke data ini.

```csharp
// Menambahkan nilai sampel ke sel
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Di sini, kita memasukkan beberapa nilai numerik ke dalam sel tertentu. Kolom "A" dan "B" berisi titik data yang akan kita visualisasikan.

## Langkah 5: Tambahkan Bagan ke Lembar Kerja

Setelah data kita tersedia, saatnya membuat bagan. Kita akan menambahkan bagan kolom yang memvisualisasikan kumpulan data kita.

```csharp
// Menambahkan bagan ke lembar kerja
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

Dalam kode ini, kami menentukan jenis bagan (dalam hal ini, bagan kolom) dan posisi di mana kami ingin meletakkannya.

## Langkah 6: Akses Instansi Bagan

 Setelah kita membuat grafik, kita perlu mengakses instansinya untuk mengubah propertinya. Ini dilakukan dengan mengambilnya melalui`Charts`koleksi.

```csharp
// Mengakses contoh grafik yang baru ditambahkan
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

## Langkah 7: Tambahkan Seri Data ke Bagan

Sekarang kita perlu mengikat data kita ke grafik. Ini melibatkan penentuan sel sebagai sumber data untuk grafik.

```csharp
// Menambahkan SeriesCollection (sumber data bagan) ke bagan mulai dari sel "A1" hingga "B3"
chart.NSeries.Add("A1:B3", true);
```

Pada langkah ini, kami menginformasikan bagan tentang rentang data yang harus divisualisasikannya.

## Langkah 8: Sesuaikan Tampilan Bagan

Mari kita percantik diagram kita sedikit dengan mengubah warna area plot, area diagram, dan koleksi seri. Ini akan membantu diagram kita menonjol dan meningkatkan daya tarik visualnya.

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

Dalam kode ini, kami menetapkan berbagai warna untuk berbagai bagian diagram. Menyesuaikan tampilan dapat membuat data Anda jauh lebih menarik!

## Langkah 9: Ubah Warna Garis Kisi Utama

Sekarang, untuk acara utamanya! Untuk meningkatkan keterbacaan, kita akan mengubah warna garis kisi utama di sepanjang kedua sumbu diagram kita.

```csharp
// Mengatur warna garis kisi utama Sumbu Kategori menjadi perak
chart.CategoryAxis.MajorGridLines.Color = Color.Silver;

// Mengatur warna garis kisi utama Sumbu Nilai menjadi merah
chart.ValueAxis.MajorGridLines.Color = Color.Red;
```

Perintah ini mengatur garis kisi utama untuk sumbu kategori dan nilai menjadi perak dan merah. Perbedaan ini memastikan pemirsa Anda dapat mengikuti garis kisi di seluruh diagram dengan mudah.

## Langkah 10: Simpan Buku Kerja

Setelah melakukan semua modifikasi, saatnya menyimpan buku kerja. Ini adalah langkah terakhir yang akan membuahkan hasil.

```csharp
// Menyimpan file Excel
workbook.Save(outputDir + "outputChangingMajorGridlinesInChart.xlsx");
```

Baris ini menyimpan file Excel yang baru Anda buat ke direktori keluaran yang ditentukan dengan nama yang mencerminkan tujuannya.

## Langkah 11: Pesan Konfirmasi

Terakhir, mari tambahkan pesan untuk mengonfirmasi bahwa tugas kita berhasil:

```csharp
Console.WriteLine("Changing Major Gridlines in Chart executed successfully.");
```

Keluaran konsol sederhana ini memberi tahu Anda bahwa program Anda berjalan dengan benar tanpa hambatan apa pun.

## Kesimpulan

Nah, itu dia! Anda telah berhasil mempelajari cara mengubah garis kisi utama dalam bagan menggunakan Aspose.Cells untuk .NET. Dengan mengikuti panduan langkah demi langkah ini, Anda tidak hanya memanipulasi file Excel secara terprogram, tetapi juga meningkatkan daya tarik visualnya dengan kustomisasi warna. Jangan ragu untuk bereksperimen lebih lanjut dengan Aspose.Cells untuk memperdalam keterampilan presentasi data Anda dan membuat bagan Anda lebih dinamis!

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?  
Aspose.Cells adalah pustaka .NET yang dirancang untuk membuat, memanipulasi, dan mengelola file Excel secara terprogram.

### Dapatkah saya mencoba Aspose.Cells secara gratis?  
 Ya, Anda dapat mendaftar untuk uji coba gratis[Di Sini](https://releases.aspose.com/).

### Bagaimana cara mengubah elemen lain dalam bagan menggunakan Aspose.Cells?  
 Anda dapat menyesuaikan berbagai properti bagan dengan cara yang sama dengan mengakses elemen bagan melalui`Chart` kelas, seperti judul, legenda, dan label data.

### Format file apa yang didukung Aspose.Cells?  
Aspose.Cells mendukung berbagai format file, termasuk XLSX, XLS, CSV, dan lainnya.

### Di mana saya dapat menemukan dokumentasi untuk Aspose.Cells?  
 Anda dapat merujuk ke dokumentasi terperinci di[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
