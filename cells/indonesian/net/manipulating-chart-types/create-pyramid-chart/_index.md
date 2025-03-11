---
title: Buat Bagan Piramida
linktitle: Buat Bagan Piramida
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mudah membuat bagan piramida di Excel menggunakan Aspose.Cells for .NET dengan panduan langkah demi langkah ini. Sempurna untuk visualisasi data.
weight: 13
url: /id/net/manipulating-chart-types/create-pyramid-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Bagan Piramida

## Perkenalan

Membuat representasi visual data sangat penting dalam banyak bidang, mulai dari analisis data hingga presentasi bisnis. Di antara berbagai jenis bagan, bagan piramida menonjol karena kemampuannya yang unik untuk menyampaikan hubungan hierarkis dan perbandingan proporsional. Tutorial ini akan memandu Anda membuat bagan piramida menggunakan Aspose.Cells untuk .NET. Baik Anda pengembang berpengalaman atau baru mulai menggunakan .NET, panduan ini menyederhanakan prosesnya, memastikan Anda memahami setiap langkah saat menggunakan pustaka yang tangguh ini.

## Prasyarat

Sebelum kita menyelami dunia diagram piramida yang menarik, mari kita siapkan beberapa prasyarat penting untuk memastikan pengalaman yang lancar.

### Pengetahuan Dasar tentang C# dan .NET
Anda harus memiliki pemahaman dasar tentang pengembangan C# dan .NET. Pemahaman terhadap lingkungan Visual Studio juga akan bermanfaat.

### Pustaka Aspose.Cells untuk .NET
 Pastikan Anda telah menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya langsung dari[Halaman Rilis Aspose.Cells untuk .NET](https://releases.aspose.com/cells/net/)Ikuti petunjuk instalasi atau gunakan NuGet Package Manager untuk dengan mudah menggabungkannya ke dalam proyek Anda.

### Bahasa Indonesia: Studio Visual
Instalasi Visual Studio yang berfungsi direkomendasikan untuk mengodekan program contoh kita. 

### Lisensi (Opsional)
 Meskipun Anda dapat mencoba uji coba gratis yang tersedia melalui[Tautan Uji Coba Gratis](https://releases.aspose.com/) , untuk penggunaan produksi, pertimbangkan untuk mengunjungi[Tautan pembelian](https://purchase.aspose.com/buy) atau memilih lisensi sementara dari[Tautan Lisensi Sementara](https://purchase.aspose.com/temporary-license/).

Sekarang semuanya sudah siap, mari kita mulai!

## Paket Impor

Sebelum kita mulai membuat kode, mari impor namespace yang diperlukan. Langkah ini penting karena memungkinkan kita untuk memanfaatkan kelas dan metode yang disediakan oleh pustaka Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Ruang nama ini mencakup fungsionalitas inti yang akan kita gunakan dalam tutorial ini, seperti membuat buku kerja, memanipulasi lembar kerja, dan menambahkan bagan.

Baiklah, mari kita uraikan proses pembuatan diagram piramida menjadi beberapa langkah mudah. Di akhir panduan ini, Anda akan memiliki contoh kerja yang lengkap.

## Langkah 1: Tentukan Direktori Output

Pertama-tama, kita perlu menentukan di mana file output kita (file Excel dengan diagram piramida) akan disimpan. Ini seperti memilih ruang kerja sebelum memulai proyek.

```csharp
// Direktori keluaran
string outputDir = "Your Output Directory";
```

 Pastikan untuk mengganti`"Your Output Directory"` dengan jalur yang valid di komputer Anda. Jalur ini adalah tempat penyimpanan berkas Excel yang Anda buat.

## Langkah 2: Membuat Instansi Objek Buku Kerja

Selanjutnya, mari kita buat contoh baru dari sebuah workbook. Bayangkan workbook sebagai kanvas kosong tempat Anda dapat melukis data Anda.

```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
```

Baris ini menginisialisasi buku kerja baru, siap untuk entri data dan visualisasi.

## Langkah 3: Dapatkan Referensi ke Lembar Kerja

Setiap buku kerja berisi setidaknya satu lembar kerja. Di sini kita akan merujuk lembar kerja pertama yang akan digunakan.

```csharp
// Mendapatkan referensi lembar kerja yang baru ditambahkan dengan meneruskan indeks lembar kerjanya
Worksheet worksheet = workbook.Worksheets[0];
```

 Dengan merujuk`Worksheets[0]`, kita berinteraksi langsung dengan lembar pertama, tempat kita menambahkan data dan bagan.

## Langkah 4: Tambahkan Data Sampel ke Sel

Untuk membuat bagan apa pun, Anda memerlukan beberapa data. Mari kita masukkan beberapa contoh nilai di lembar kerja kita.

```csharp
// Menambahkan nilai sampel ke sel
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

Di sini, kita memasukkan nilai ke dalam sel A1 hingga A3 (label atau tingkat piramida) dan B1 hingga B3 (nilai yang sesuai dengan tingkat tersebut).

## Langkah 5: Tambahkan Bagan Piramida ke Lembar Kerja

Sekarang, mari tambahkan diagram piramida kita. Di sinilah keajaiban terjadi!

```csharp
// Menambahkan bagan ke lembar kerja
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pyramid, 5, 0, 25, 10);
```

 Pada baris ini, kami menentukan tipe grafik sebagai`Pyramid` dan tentukan posisinya dalam lembar kerja menggunakan indeks baris dan kolom. Ini sama seperti membingkai gambar di dinding – Anda perlu memilih tempat yang paling cocok untuk meletakkannya!

## Langkah 6: Akses Bagan yang Baru Ditambahkan

Setelah menambahkan bagan, kita perlu mengaksesnya untuk mengaturnya.

```csharp
// Mengakses contoh grafik yang baru ditambahkan
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Baris ini memastikan kita bekerja dengan contoh bagan yang benar yang baru saja kita buat.

## Langkah 7: Tambahkan Seri Data ke Bagan

Agar bagan menampilkan data, kita perlu mengatur sumber data berdasarkan sel yang telah kita isi sebelumnya.

```csharp
// Menambahkan SeriesCollection (sumber data bagan) ke bagan mulai dari sel "A1" hingga "B3"
chart.NSeries.Add("A1:B3", true);
```

Pada bagian ini, kita menghubungkan data dalam sel A1 ke B3, sehingga diagram piramida kita dapat memvisualisasikan informasi ini.

## Langkah 8: Simpan File Excel

Akhirnya, saatnya menyimpan karya agung kita. Mari kita tulis buku kerja Excel ke dalam sebuah file.

```csharp
// Menyimpan file Excel
workbook.Save(outputDir + "outputHowToCreatePyramidChart.xlsx");
```

 Tindakan ini akan membuat file Excel bernama`outputHowToCreatePyramidChart.xlsx` di direktori keluaran yang Anda tentukan.

## Langkah 9: Konfirmasi Konsol

Terakhir namun tidak kalah pentingnya, mari tambahkan beberapa umpan balik di konsol untuk memastikan semuanya berjalan lancar.

```csharp
Console.WriteLine("HowToCreatePyramidChart executed successfully.");
```

Baris ini akan memberitahukan Anda bahwa tugas pembuatan bagan piramida Anda telah selesai tanpa hambatan apa pun.

## Kesimpulan

Membuat bagan piramida dalam file Excel tidak pernah semudah ini dengan Aspose.Cells untuk .NET. Dengan mengikuti langkah-langkah sederhana ini, Anda dapat mengubah data mentah Anda menjadi narasi visual yang menarik yang menarik perhatian dan mengomunikasikan hubungan secara efektif. Sekarang setelah Anda dibekali dengan pengetahuan ini, Anda dapat menjelajahi fitur Aspose.Cells yang lebih kompleks, seperti gaya tingkat lanjut dan berbagai jenis bagan, untuk lebih menyempurnakan laporan Anda.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah API yang canggih untuk memanipulasi file dan bagan Excel dalam aplikasi .NET, yang memungkinkan pengembang untuk membuat, memodifikasi, dan mengonversi dokumen Excel dengan mudah.

### Bisakah saya menggunakan Aspose.Cells secara gratis?
Ya, Aspose.Cells menyediakan uji coba gratis yang memungkinkan Anda menjelajahi fitur-fiturnya. Namun, untuk penggunaan berkelanjutan, pertimbangkan untuk membeli lisensi.

### Jenis bagan apa yang dapat saya buat dengan Aspose.Cells?
Anda dapat membuat berbagai jenis bagan, termasuk bagan batang, garis, pai, area, dan piramida, dan masih banyak lagi.

### Apakah saya perlu menginstal sesuatu selain pustaka Aspose.Cells?
Pastikan Anda telah menyiapkan alat pengembangan .NET seperti Visual Studio di komputer Anda untuk bekerja dengan Aspose.Cells dengan lancar.

### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Untuk dukungan, Anda dapat mengunjungi[Forum Dukungan Aspose.Cells](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
