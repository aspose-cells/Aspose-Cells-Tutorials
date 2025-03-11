---
title: Sisipkan Kotak Centang di Lembar Bagan
linktitle: Sisipkan Kotak Centang di Lembar Bagan
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mudah menyisipkan kotak centang di lembar bagan Excel menggunakan Aspose.Cells untuk .NET dengan tutorial langkah demi langkah ini.
weight: 13
url: /id/net/inserting-controls-in-charts/insert-checkbox-in-chart-sheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sisipkan Kotak Centang di Lembar Bagan

## Perkenalan

Jika Anda pernah membuat bagan di Excel, Anda tahu bahwa bagan dapat sangat berguna untuk memvisualisasikan data. Namun, bagaimana jika Anda dapat meningkatkan interaktivitas tersebut lebih jauh dengan menambahkan kotak centang langsung di bagan? Meskipun ini mungkin terdengar agak rumit, sebenarnya cukup mudah dilakukan dengan pustaka Aspose.Cells untuk .NET. Dalam tutorial ini, saya akan memandu Anda melalui proses ini langkah demi langkah, membuatnya sederhana dan mudah diikuti.

## Prasyarat

Sebelum memulai tutorial, pastikan Anda telah menyiapkan semuanya. Berikut ini yang Anda perlukan:

### Visual Studio Terpasang
- Pertama dan terutama, Anda memerlukan Visual Studio. Jika Anda belum menginstalnya, Anda dapat mengunduhnya dari situs Microsoft.

### Pustaka Aspose.Cells
-  Alat penting berikutnya adalah pustaka Aspose.Cells untuk .NET. Anda dapat dengan mudah mendapatkannya dari[Situs web Aspose](https://releases.aspose.com/cells/net/) untuk diunduh. Jika Anda lebih suka menguji sebelum membeli, ada juga[uji coba gratis tersedia](https://releases.aspose.com/).

### Pemahaman Dasar C#
- Karena kita akan menulis beberapa kode, pemahaman dasar tentang C# akan bermanfaat. Jangan khawatir; saya akan menjelaskannya sambil jalan!

### Direktori Keluaran
- Anda akan memerlukan direktori tempat file Excel keluaran Anda akan disimpan. Pastikan Anda memiliki direktori ini.

Jika prasyarat ini telah terpenuhi dalam daftar Anda, kita siap untuk beraksi!

## Paket Impor

Untuk memulai, mari kita siapkan proyek kita di Visual Studio dan impor paket-paket yang diperlukan. Berikut panduan langkah demi langkah yang mudah dipahami:

### Buat Proyek Baru

Buka Visual Studio dan buat proyek Aplikasi Konsol baru. Cukup ikuti langkah-langkah sederhana berikut:
- Klik “Buat proyek baru.”
- Pilih “Aplikasi Konsol (.NET Framework)” dari pilihan yang ada.
- Beri nama proyek Anda seperti "CheckboxInChart".

### Instal Aspose.Cells melalui NuGet

Setelah proyek Anda disiapkan, saatnya menambahkan pustaka Aspose.Cells. Anda dapat melakukannya melalui Pengelola Paket NuGet:
- Klik kanan pada proyek Anda di Solution Explorer dan pilih “Kelola Paket NuGet.”
- Cari “Aspose.Cells” dan klik “Install.”
- Ini akan menarik semua dependensi yang Anda perlukan, membuatnya mudah untuk mulai menggunakan pustaka.

### Tambahkan Petunjuk Penggunaan yang Diperlukan

 Di bagian atas Anda`Program.cs` file, tambahkan arahan berikut menggunakan untuk membuat fungsionalitas Aspose.Cells tersedia:
```csharp
using Aspose.Cells.Charts;
using System;
using Aspose.Cells.Drawing;
```

Sekarang Anda telah menyelesaikan pengaturan! Ini seperti meletakkan fondasi yang kokoh sebelum membangun rumah — penting untuk struktur yang stabil.

Sekarang setelah semuanya siap, mari kita mulai bagian pengkodean! Berikut adalah uraian terperinci tentang cara memasukkan kotak centang ke dalam lembar bagan menggunakan Aspose.Cells.

## Langkah 1: Tentukan Direktori Output Anda

Sebelum kita masuk ke bagian yang menarik, kita perlu menentukan di mana kita ingin menyimpan berkas kita. Anda perlu memberikan jalur direktori keluaran.
```csharp
string outputDir = "C:\\YourOutputDirectory\\"; // Beralih ke direktori yang Anda tentukan
```
 Pastikan untuk mengganti`"C:\\YourOutputDirectory\\"`dengan jalur tempat Anda ingin menyimpan berkas Anda. Anggap ini seperti menyiapkan ruang kerja Anda; Anda perlu tahu di mana Anda meletakkan alat-alat Anda (atau dalam hal ini, berkas Excel Anda).

## Langkah 2: Membuat Instansiasi Objek Buku Kerja

 Berikutnya, kita membuat sebuah instance dari`Workbook` kelas. Di sinilah semua pekerjaan kita akan dilakukan.
```csharp
Workbook workbook = new Workbook();
```
Baris kode ini seperti membuka kanvas kosong. Anda siap untuk mulai melukis (atau dalam kasus kami, membuat kode)!

## Langkah 3: Menambahkan Bagan ke Lembar Kerja

Sekarang, saatnya menambahkan bagan ke buku kerja Anda. Berikut cara melakukannya:
```csharp
int index = workbook.Worksheets.Add(SheetType.Chart);
Worksheet sheet = workbook.Worksheets[index];
sheet.Charts.AddFloatingChart(ChartType.Column, 0, 0, 1024, 960);
```
Dalam kode ini, Anda:
- Menambahkan lembar bagan baru ke buku kerja.
- Memilih jenis bagan. Di sini, kita akan menggunakan bagan kolom sederhana.
- Menentukan dimensi bagan Anda.

Anggap langkah ini sebagai pemilihan jenis bingkai foto yang Anda inginkan sebelum menempatkan karya seni Anda di dalamnya.

## Langkah 4: Menambahkan Seri Data ke Bagan Anda

Pada titik ini, mari kita isi diagram dengan beberapa seri data. Untuk menambahkan data sampel:
```csharp
sheet.Charts[0].NSeries.Add("{1,2,3}", false);
```
Baris ini penting! Seperti mengoleskan cat pada kanvas. Angka-angka tersebut mewakili beberapa contoh titik data untuk diagram Anda.

## Langkah 5: Menambahkan Kotak Centang ke Bagan

Sekarang, kita akan masuk ke bagian yang menyenangkan — menambahkan kotak centang ke diagram kita. Berikut caranya:
```csharp
sheet.Charts[0].Shapes.AddShapeInChart(MsoDrawingType.CheckBox, PlacementType.Move, 400, 400, 1000, 600);
sheet.Charts[0].Shapes[0].Text = "CheckBox 1";
```
Dalam kode ini:
- Kami menentukan jenis bentuk yang ingin kami tambahkan — dalam hal ini, kotak centang.
- `PlacementType.Move` artinya jika grafik bergerak, kotak centang pun akan bergerak.
- Kami juga mengatur posisi dan ukuran kotak centang dalam area bagan, dan terakhir, kami mengatur label teks kotak centang.

Menambahkan kotak centang seperti menaruh ceri di atas es krim Anda; ia menyempurnakan keseluruhan presentasi!

## Langkah 6: Menyimpan File Excel

Terakhir, mari kita simpan pekerjaan kita. Berikut bagian terakhir dari teka-teki tersebut:
```csharp
workbook.Save(outputDir + "InsertCheckboxInChartSheet_out.xlsx");
```
Baris ini menyimpan berkas Excel yang baru Anda buat dengan kotak centang di direktori keluaran yang ditentukan. Ini sama saja dengan menyegel karya seni Anda dalam kotak pelindung!

## Kesimpulan

Nah, itu dia! Anda telah berhasil menambahkan kotak centang ke lembar bagan dalam file Excel menggunakan Aspose.Cells for .NET. Dengan mengikuti langkah-langkah ini, Anda dapat membuat lembar Excel yang interaktif dan dinamis yang menawarkan fungsionalitas hebat, membuat visualisasi data Anda semakin menarik.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?  
Aspose.Cells adalah pustaka yang hebat untuk membuat dan memanipulasi file Excel dalam aplikasi .NET.

### Bisakah saya menggunakan Aspose.Cells secara gratis?  
 Ya, Aspose menawarkan uji coba gratis. Anda dapat memulai dengan versi uji coba yang tersedia[Di Sini](https://releases.aspose.com/).

### Apakah menambahkan kotak centang ke lembar bagan rumit?  
Sama sekali tidak! Seperti yang ditunjukkan dalam tutorial ini, hal itu dapat dilakukan hanya dengan beberapa baris kode sederhana.

### Di mana saya dapat membeli Aspose.Cells?  
 Anda dapat membeli Aspose.Cells dari mereka[tautan pembelian](https://purchase.aspose.com/buy).

### Bagaimana saya bisa mendapatkan dukungan jika saya mengalami masalah?  
 Aspose menyediakan forum dukungan tempat Anda dapat mengajukan pertanyaan dan menemukan solusi. Lihat forum mereka[halaman dukungan](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
