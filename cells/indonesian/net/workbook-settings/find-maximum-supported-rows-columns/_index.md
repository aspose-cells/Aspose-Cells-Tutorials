---
title: Temukan Jumlah Baris dan Kolom Maksimum yang Didukung oleh Format XLS dan XLSX
linktitle: Temukan Jumlah Baris dan Kolom Maksimum yang Didukung oleh Format XLS dan XLSX
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan jumlah baris dan kolom maksimum yang didukung oleh format XLS dan XLSX menggunakan Aspose.Cells untuk .NET. Maksimalkan pengelolaan data Excel Anda dengan tutorial lengkap ini.
weight: 11
url: /id/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Temukan Jumlah Baris dan Kolom Maksimum yang Didukung oleh Format XLS dan XLSX

## Perkenalan
Dalam dunia Excel, mengelola kumpulan data besar bisa menjadi tugas yang berat, terutama saat menangani jumlah baris dan kolom maksimum yang didukung oleh berbagai format file. Tutorial ini akan memandu Anda melalui proses menemukan jumlah baris dan kolom maksimum yang didukung oleh format XLS dan XLSX menggunakan pustaka Aspose.Cells for .NET. Di akhir artikel ini, Anda akan memiliki pemahaman menyeluruh tentang cara memanfaatkan alat canggih ini untuk menangani tugas-tugas terkait Excel secara efisien.
## Prasyarat
Sebelum kita masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:
1. [Kerangka .NET](https://dotnet.microsoft.com/en-us/download) atau[Inti .NET](https://dotnet.microsoft.com/en-us/download) terinstal pada sistem Anda.
2. [Aspose.Cells untuk .NET](https://releases.aspose.com/cells/net/) pustaka yang diunduh dan dirujuk dalam proyek Anda.
 Jika Anda belum melakukannya, Anda dapat mengunduh pustaka Aspose.Cells untuk .NET dari[situs web](https://releases.aspose.com/cells/net/) atau menginstalnya melalui[Bahasa Inggris NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Paket Impor
Untuk memulai, Anda perlu mengimpor paket yang diperlukan dari pustaka Aspose.Cells for .NET. Tambahkan pernyataan berikut di bagian atas berkas C# Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Langkah 1: Temukan Jumlah Baris dan Kolom Maksimum yang Didukung oleh Format XLS
Mari kita mulai dengan menjelajahi jumlah baris dan kolom maksimum yang didukung oleh format XLS (Excel 97-2003).
```csharp
// Cetak pesan tentang format XLS.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Membuat buku kerja dalam format XLS.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Cetak baris dan kolom maksimum yang didukung oleh format XLS.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
Pada langkah ini, kita:
1. Cetak pesan untuk menunjukkan bahwa kami sedang bekerja dengan format XLS.
2.  Buat yang baru`Workbook` contoh menggunakan`FileFormatType.Excel97To2003` enum, yang mewakili format XLS.
3.  Ambil baris dan kolom maksimum yang didukung oleh format XLS menggunakan`Workbook.Settings.MaxRow` Dan`Workbook.Settings.MaxColumn`properti, masing-masing. Kami menambahkan 1 ke nilai-nilai ini untuk mendapatkan jumlah baris dan kolom maksimum yang sebenarnya (karena keduanya berbasis nol).
4. Cetak baris dan kolom maksimum ke konsol.
## Langkah 2: Temukan Jumlah Baris dan Kolom Maksimum yang Didukung oleh Format XLSX
Selanjutnya, mari kita jelajahi jumlah baris dan kolom maksimum yang didukung oleh format XLSX (Excel 2007 dan yang lebih baru).
```csharp
// Cetak pesan tentang format XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Buat buku kerja dalam format XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Cetak baris dan kolom maksimum yang didukung oleh format XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
Pada langkah ini, kita:
1. Cetak pesan untuk menunjukkan bahwa kami sedang bekerja dengan format XLSX.
2.  Buat yang baru`Workbook` contoh menggunakan`FileFormatType.Xlsx` enum, yang mewakili format XLSX.
3.  Ambil baris dan kolom maksimum yang didukung oleh format XLSX menggunakan`Workbook.Settings.MaxRow` Dan`Workbook.Settings.MaxColumn`properti, masing-masing. Kami menambahkan 1 ke nilai-nilai ini untuk mendapatkan jumlah baris dan kolom maksimum yang sebenarnya (karena keduanya berbasis nol).
4. Cetak baris dan kolom maksimum ke konsol.
## Langkah 3: Menampilkan Pesan Sukses
Terakhir, mari tampilkan pesan sukses untuk menunjukkan bahwa contoh "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" telah berhasil dijalankan.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Langkah ini hanya mencetak pesan sukses ke konsol.
## Kesimpulan
Dalam tutorial ini, Anda telah mempelajari cara menggunakan pustaka Aspose.Cells for .NET untuk menemukan baris dan kolom maksimum yang didukung oleh format file XLS dan XLSX. Dengan memahami keterbatasan format ini, Anda dapat merencanakan dan mengelola proyek berbasis Excel dengan lebih baik, memastikan bahwa data Anda sesuai dengan rentang yang didukung.
## Pertanyaan yang Sering Diajukan
### Berapa jumlah baris maksimum yang didukung oleh format XLS?
Jumlah baris maksimum yang didukung oleh format XLS (Excel 97-2003) adalah 65.536.
### Berapa jumlah maksimum kolom yang didukung oleh format XLS?
Jumlah maksimum kolom yang didukung oleh format XLS (Excel 97-2003) adalah 256.
### Berapa jumlah baris maksimum yang didukung oleh format XLSX?
Jumlah baris maksimum yang didukung oleh format XLSX (Excel 2007 dan yang lebih baru) adalah 1.048.576.
### Berapa jumlah maksimum kolom yang didukung oleh format XLSX?
Jumlah maksimum kolom yang didukung oleh format XLSX (Excel 2007 dan yang lebih baru) adalah 16.384.
### Dapatkah saya menggunakan pustaka Aspose.Cells untuk .NET untuk bekerja dengan format file Excel lainnya?
 Ya, pustaka Aspose.Cells untuk .NET mendukung berbagai format file Excel, termasuk XLS, XLSX, ODS, dan lainnya. Anda dapat menjelajahi[dokumentasi](https://reference.aspose.com/cells/net/) untuk mempelajari fitur dan fungsi yang tersedia.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
