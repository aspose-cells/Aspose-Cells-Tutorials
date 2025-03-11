---
title: Atur Format Nilai Kode Seri Bagan
linktitle: Atur Format Nilai Kode Seri Bagan
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengatur kode format nilai rangkaian bagan di Aspose.Cells untuk .NET dengan tutorial langkah demi langkah yang terperinci ini. Sempurna untuk pemula.
weight: 17
url: /id/net/advanced-chart-operations/set-values-format-code-of-chart-series/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur Format Nilai Kode Seri Bagan

## Perkenalan

Dalam dunia yang digerakkan oleh data saat ini, representasi visual dari kumpulan data yang kompleks sangat penting untuk pengambilan keputusan. Bagan berfungsi sebagai alat yang ampuh untuk mengomunikasikan wawasan secara efektif. Aspose.Cells untuk .NET menyederhanakan proses ini, memungkinkan pengembang untuk memanipulasi file Excel dengan mudah dan membuat bagan yang menakjubkan. Dalam panduan ini, kita akan menjelajahi cara mengatur kode format nilai rangkaian bagan menggunakan Aspose.Cells. Jadi, ambil secangkir kopi, dan mari kita mulai perjalanan pengodean ini bersama-sama!

## Prasyarat

Sebelum membahas lebih jauh, mari pastikan Anda siap untuk meraih kesuksesan. Berikut ini yang Anda butuhkan:

1. Pemahaman dasar tentang C#: Keakraban dengan C# akan membantu Anda memahami konsep pemrograman dengan mudah.
2.  Aspose.Cells untuk .NET: Anda memerlukan pustaka Aspose.Cells. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
3. Visual Studio: IDE yang cocok untuk menulis dan mengeksekusi kode C# Anda. Versi apa pun yang mendukung .NET dapat digunakan.
4.  File Excel: Untuk demonstrasi kami, kami akan menggunakan file Excel bernama`sampleSeries_ValuesFormatCode.xlsx`Pastikan Anda telah menyiapkannya di direktori kerja Anda.

## Paket Impor

Pertama-tama, mari impor paket-paket yang diperlukan. Langkah ini penting karena memungkinkan kita memanfaatkan fungsionalitas yang disediakan oleh Aspose.Cells.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells;
using Aspose.Cells.Charts;
```

Dengan impor ini, kita sekarang dapat mengakses kelas penting dari pustaka Aspose yang kita perlukan untuk memanipulasi file Excel.

Sekarang, mari kita uraikan prosesnya menjadi langkah-langkah yang sederhana dan mudah dipahami. Ikuti langkah-langkah yang kami berikan saat kami menguraikan cara mengatur kode format nilai rangkaian bagan di berkas Excel Anda.

## Langkah 1: Siapkan Direktori Sumber dan Output

Sebelum kita dapat memanipulasi berkas Excel, kita perlu menentukan di mana berkas itu berada dan di mana output harus ditempatkan. 

Anggap saja ini sebagai persiapan untuk penampilan kita. Jika Anda tidak tahu di mana input Anda berada dan di mana Anda ingin output Anda, program Anda akan tersesat di labirin direktori file!

```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";

// Direktori keluaran
string outputDir = "Your Output Directory";
```

## Langkah 2: Muat File Excel Sumber

Setelah kita menetapkan direktori, saatnya memuat berkas Excel yang ingin kita gunakan.

Memuat berkas Excel sama halnya dengan membuka buku sebelum membaca. Tanpa membukanya, Anda tidak dapat menyelami isinya. 

```csharp
// Muat file Excel sumber
Workbook wb = new Workbook(sourceDir + "sampleSeries_ValuesFormatCode.xlsx");
```

## Langkah 3: Akses Lembar Kerja

Setelah buku kerja kita dimuat, mari masuk ke lembar kerja pertama.

Setiap lembar kerja dalam file Excel berfungsi seperti halaman dalam buku. Anda ingin mengakses halaman yang tepat untuk menemukan data yang Anda minati!

```csharp
// Akses lembar kerja pertama
Worksheet worksheet = wb.Worksheets[0];
```

## Langkah 4: Akses Bagan

Berikutnya, kita perlu mengakses bagan di mana kita ingin mengubah format serinya.

Bayangkan bagan tersebut sebagai kanvas tempat karya visualisasi data Anda dilukis. Dengan mengaksesnya, kita dapat memanfaatkan kekuatannya!

```csharp
// Akses bagan pertama
Chart ch = worksheet.Charts[0];
```

## Langkah 5: Tambahkan Seri Data

Setelah bagan siap, mari tambahkan beberapa rangkaian data untuk divisualisasikan.

Menambahkan rangkaian seperti menambahkan warna pada lukisan Anda. Semakin berwarna, semakin menarik karya seni tersebut!

```csharp
// Tambahkan seri menggunakan array nilai
ch.NSeries.Add("{10000, 20000, 30000, 40000}", true);
```

## Langkah 6: Tetapkan Kode Format Nilai

Di sinilah keajaiban terjadi. Kami akan menetapkan kode format untuk seri yang baru ditambahkan.

Menetapkan kode format mengubah angka mentah menjadi sesuatu yang lebih mudah dibaca, seperti menerapkan filter untuk menyempurnakan foto Anda sebelum menunjukkannya kepada dunia!

```csharp
// Akses seri dan atur kode format nilainya
Series srs = ch.NSeries[0];
srs.ValuesFormatCode = "$#,##0"; //Ini mengaturnya ke format mata uang
```

## Langkah 7: Simpan File Excel Output

Terakhir, kita perlu menyimpan perubahan yang telah kita buat pada berkas Excel baru.

Menyimpan hasil kerja keras Anda terasa memuaskan, bukan? Ini menjaga usaha Anda dan memungkinkan Anda untuk membagikan atau mengulas hasil kerja Anda kapan saja!

```csharp
// Simpan file Excel keluaran
wb.Save(outputDir + "outputSeries_ValuesFormatCode.xlsx");
```

## Langkah 8: Pesan Konfirmasi

Untuk menyelesaikan semuanya, kita dapat mencetak pesan sukses.

Sama seperti menerima tepuk tangan di akhir pertunjukan, konfirmasi ini memberi Anda perasaan hangat dan gembira atas pencapaian.

```csharp
Console.WriteLine("SetValuesFormatCodeOfChartSeries executed successfully.");
```

## Kesimpulan

Dalam tutorial ini, kita telah menjelajahi proses pengaturan kode format nilai dari rangkaian bagan menggunakan Aspose.Cells untuk .NET. Dari memuat berkas Excel hingga menyimpan produk akhir, setiap langkah membawa kita lebih dekat ke visualisasi data yang efektif dengan cara yang bermakna dan berdampak. Sekarang, Anda dapat mengambil keterampilan ini dan menerapkannya pada proyek Anda yang sedang berjalan.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells untuk .NET?
Aspose.Cells untuk .NET adalah pustaka hebat yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel menggunakan aplikasi .NET.

### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?
Ya, Aspose.Cells memerlukan lisensi untuk digunakan dalam lingkungan produksi. Anda dapat memilih lisensi sementara untuk tujuan pengujian.

### Bisakah saya membuat bagan dari awal menggunakan Aspose.Cells?
Tentu saja! Aspose.Cells menyediakan fungsionalitas yang tangguh untuk membuat dan menyesuaikan grafik dari awal.

### Di mana saya dapat menemukan dokumentasi lebih lanjut tentang Aspose.Cells?
 Anda dapat mengakses[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk panduan terperinci dan referensi API.

### Format apa yang didukung saat menyimpan file Excel?
Aspose.Cells mendukung berbagai format, termasuk XLSX, XLS, CSV, PDF, dan banyak lagi.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
