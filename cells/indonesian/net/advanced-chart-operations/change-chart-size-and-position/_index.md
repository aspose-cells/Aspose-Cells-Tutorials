---
title: Ubah Ukuran dan Posisi Bagan
linktitle: Ubah Ukuran dan Posisi Bagan
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengubah ukuran dan posisi grafik di Excel menggunakan Aspose.Cells untuk .NET dengan panduan yang mudah diikuti ini.
weight: 11
url: /id/net/advanced-chart-operations/change-chart-size-and-position/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ubah Ukuran dan Posisi Bagan

## Perkenalan

Jika berbicara tentang memanipulasi spreadsheet secara terprogram, sulit untuk mengabaikan fleksibilitas dan kekuatan Aspose.Cells untuk .NET. Pernahkah Anda merasa kesulitan mengubah ukuran atau memposisikan ulang grafik di file Excel Anda? Jika demikian, Anda akan dimanjakan! Panduan ini akan memandu Anda melalui langkah-langkah yang sangat mudah untuk mengubah ukuran dan posisi grafik di spreadsheet Anda menggunakan Aspose.Cells. Bersiaplah, karena kami akan membahas topik ini secara mendalam!

## Prasyarat

Sebelum kita masuk ke inti dari pengkodean dan manipulasi grafik, mari kita perjelas beberapa prasyarat. Fondasi yang kuat akan membuat perjalanan Anda lebih lancar dan lebih menyenangkan.

### Pengetahuan Dasar C#
- Pemahaman terhadap bahasa pemrograman C# sangatlah penting. Jika Anda dapat memahami sintaks C#, Anda sudah selangkah lebih maju!

### Pustaka Aspose.Cells untuk .NET
-  Anda perlu menginstal pustaka Aspose.Cells. Jika Anda belum memilikinya, jangan khawatir! Anda dapat mengunduhnya dengan mudah dari[Di Sini](https://releases.aspose.com/cells/net/).

### Lingkungan Pengembangan
- Siapkan lingkungan pengembangan Anda (seperti Visual Studio) tempat Anda dapat menulis dan mengeksekusi kode C# dengan lancar.

### File Excel dengan Bagan
- Akan sangat membantu jika memiliki berkas Excel dengan setidaknya satu bagan di dalamnya yang dapat kita manipulasi untuk tutorial ini.

Setelah Anda memenuhi prasyarat ini dari daftar Anda, Anda siap mempelajari cara mengubah ukuran dan posisi grafik seperti seorang profesional!

## Paket Impor

Setelah semuanya siap, mari impor paket yang diperlukan. Langkah ini penting karena memungkinkan kita mengakses kelas dan metode Aspose.Cells yang diperlukan untuk memanipulasi file Excel.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
```

Pernyataan ini memberi tahu kompiler bahwa kita akan menggunakan kelas dari pustaka Aspose.Cells. Pastikan Anda mencantumkannya di bagian atas kode untuk menghindari jalan yang berliku-liku di kemudian hari!

Sekarang, mari kita bagi prosesnya menjadi beberapa langkah yang mudah dikelola. Kita akan melakukannya selangkah demi selangkah, memastikan semuanya jelas.

## Langkah 1: Tentukan Direktori Sumber dan Output

```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

Pertama-tama, kita perlu menentukan di mana file sumber kita berada dan di mana kita ingin menyimpan file output. Ganti "Direktori Dokumen Anda" dan "Direktori Output Anda" dengan jalur folder Anda yang sebenarnya. Anggap direktori ini sebagai markas dan landasan peluncuran tempat file Anda berada.

## Langkah 2: Muat Buku Kerja

```csharp
Workbook workbook = new Workbook(sourceDir + "sampleChangeChartSizeAndPosition.xlsx");
```

 Di sini, kita membuat contoh baru dari`Workbook` kelas dan muat berkas Excel kita ke dalamnya. Bayangkan buku kerja sebagai buku catatan digital yang berisi semua lembar dan bagan Anda. Parameter yang kita lewati adalah jalur lengkap ke berkas Excel kita, jadi pastikan itu menyertakan nama berkas!

## Langkah 3: Akses Lembar Kerja

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

 Sekarang setelah buku kerja kita dimuat, kita perlu mengakses lembar kerja tertentu yang ingin kita gunakan, yang dalam kasus ini adalah lembar kerja pertama (indeks`[0]`). Seperti membalik halaman yang tepat pada sebuah buku, langkah ini membantu kita fokus pada lembar yang diinginkan untuk suntingan kita.

## Langkah 4: Muat Bagan

```csharp
Chart chart = worksheet.Charts[0];
```

Setelah lembar kerja diambil, kita langsung masuk ke akses grafik! Kita mengambil grafik pertama (sekali lagi, indeks`[0]`). Ini seperti memilih karya seni yang ingin Anda hias. Pastikan diagram Anda ada di lembar kerja itu, atau Anda akan bingung!

## Langkah 5: Ubah Ukuran Bagan

```csharp
chart.ChartObject.Width = 400;
chart.ChartObject.Height = 300;
```

 Saatnya mengubah dimensi grafik! Di sini, kita mengatur lebarnya menjadi`400` piksel dan tingginya`300` piksel. Menyesuaikan ukuran sama halnya dengan memilih bingkai yang sempurna untuk karya seni Anda—terlalu besar atau terlalu kecil, dan bingkai tersebut tidak akan pas dengan ruangan.

## Langkah 6: Ubah Posisi Bagan

```csharp
chart.ChartObject.X = 250;
chart.ChartObject.Y = 150;
```

 Sekarang setelah kita memiliki ukuran yang tepat, mari kita pindahkan grafik! Dengan mengubah`X` Dan`Y` properti, pada dasarnya kita sedang menata ulang bagan pada lembar kerja. Bayangkan seperti menyeret gambar berbingkai Anda ke tempat baru di dinding untuk lebih menonjolkan keindahannya!

## Langkah 7: Simpan Buku Kerja

```csharp
workbook.Save(outputDir + "outputChangeChartSizeAndPosition.xlsx");
```

Terakhir, kami menyimpan perubahan ke file Excel baru. Tentukan nama yang sesuai untuk file yang diekspor agar semuanya tetap teratur. Ini seperti mengambil foto ruangan Anda yang tertata rapi setelah memindahkan perabotan—mempertahankan tata letak baru!

## Langkah 8: Konfirmasikan Keberhasilan

```csharp
Console.WriteLine("ChangeChartSizeAndPosition executed successfully.");
```

Untuk mengakhiri semuanya dengan rapi, kami memberikan umpan balik tentang apakah operasi tersebut berhasil diselesaikan. Ini adalah praktik yang bagus, yang memberi Anda penyelesaian yang jelas dan meyakinkan atas tugas Anda—sama seperti mengagumi hasil kerja Anda setelah menata ulang furnitur!

## Kesimpulan

Selamat! Anda baru saja mempelajari cara mengubah ukuran dan posisi grafik di Excel menggunakan Aspose.Cells for .NET. Dengan langkah-langkah ini, Anda dapat membuat grafik Anda tidak hanya terlihat lebih baik tetapi juga pas dengan spreadsheet Anda, sehingga menghasilkan presentasi data yang lebih profesional. Mengapa tidak mencobanya dan mulai memanipulasi grafik Anda hari ini? 

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells untuk .NET?  
Aspose.Cells untuk .NET adalah pustaka hebat yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel dalam aplikasi .NET.

### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?  
 Meskipun Anda dapat mencoba Aspose.Cells secara gratis, lisensi diperlukan untuk penggunaan berkelanjutan dalam aplikasi produksi. Anda dapat memperolehnya[Di Sini](https://purchase.aspose.com/buy).

### Bisakah saya menggunakan Aspose.Cells tanpa Visual Studio?  
Ya, Anda dapat menggunakan Aspose.Cells di IDE mana pun yang kompatibel dengan .NET, tetapi Visual Studio menyediakan alat yang membuat pengembangan lebih mudah.

### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.Cells?  
 Anda dapat menemukan dukungan di situs khusus mereka[Forum Dukungan](https://forum.aspose.com/c/cells/9).

### Apakah ada lisensi sementara yang tersedia?  
 Ya, Anda dapat memperoleh lisensi sementara untuk mengevaluasi Aspose.Cells untuk jangka waktu pendek, yang tersedia[Di Sini](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
