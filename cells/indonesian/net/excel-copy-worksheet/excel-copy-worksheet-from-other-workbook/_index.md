---
title: Salin Lembar Kerja Excel Dari Buku Kerja Lain
linktitle: Salin Lembar Kerja Excel Dari Buku Kerja Lain
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara menyalin lembar kerja dari satu buku kerja Excel ke buku kerja lainnya menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah ini.
weight: 10
url: /id/net/excel-copy-worksheet/excel-copy-worksheet-from-other-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Lembar Kerja Excel Dari Buku Kerja Lain

## Perkenalan

Pernahkah Anda merasa kesulitan dengan beberapa buku kerja Excel, mencoba menjaga data Anda tetap teratur dan mudah diakses? Jika demikian, Anda tidak sendirian! Banyak dari kita yang harus mengelola berbagai file, baik untuk pekerjaan maupun proyek pribadi. Kabar baiknya adalah Anda dapat mempermudah hidup Anda dengan sedikit bantuan dari Aspose.Cells for .NET. Pustaka canggih ini memungkinkan Anda untuk memanipulasi file Excel dengan mudah, termasuk menyalin lembar kerja dari satu buku kerja ke buku kerja lainnya. Dalam panduan ini, kami akan memandu Anda melalui langkah-langkah untuk melakukannya, memastikan Anda dapat menyederhanakan alur kerja dan meningkatkan produktivitas.

## Prasyarat

Sebelum masuk ke bagian pengodean, mari persiapkan semua yang Anda butuhkan. Jangan khawatir; ini bukan ilmu roket! Berikut ini yang Anda perlukan:

1. Visual Studio (atau IDE .NET apa pun): Anda harus menyiapkan lingkungan pengembangan .NET di komputer Anda.
2.  Aspose.Cells untuk .NET: Anda perlu mengunduh dan menginstal Aspose.Cells. Jika Anda belum memilikinya, Anda bisa mendapatkannya[Di Sini](https://releases.aspose.com/cells/net/).
3. Pemahaman Dasar tentang C#: Sedikit pengetahuan dengan pemrograman C# akan membuat perjalanan ini lebih lancar, tetapi jangan stres jika Anda baru memulai!
4. .NET Framework: Pastikan proyek Anda menargetkan versi .NET Framework yang kompatibel.
5. Pengaturan Sistem: Pastikan Anda dapat menjalankan dan menguji aplikasi Anda tanpa batasan apa pun.

Sekarang setelah semuanya siap, mari kita mulai membuat kode!

## Paket Impor

Sebelum kita mulai menerapkan fungsionalitasnya, kita perlu mengimpor paket-paket yang diperlukan. Dengan cara ini, Anda akan memiliki akses ke semua fitur yang ditawarkan Aspose.Cells. Berikut panduan langkah demi langkahnya:

### Tambahkan Pernyataan Penggunaan

Buka berkas C# Anda dan tambahkan perintah berikut di bagian atas:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Paket ini adalah inti dari pustaka Aspose dan akan memberi Anda akses ke semua kelas dan metodenya.

Sekarang setelah semuanya siap, mari kita masuk ke bagian yang menarik—menyalin lembar kerja dari satu buku kerja ke buku kerja lainnya! Kita akan membaginya menjadi beberapa langkah yang jelas.

## Langkah 1: Siapkan Direktori Dokumen

Pertama, kita perlu menentukan di mana file Excel akan disimpan. Tentukan jalur direktori dokumen Anda:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";  // Perbarui ini ke direktori Anda yang sebenarnya
```
 Itu`dataDir` variabel akan menyimpan jalur tempat Anda menyimpan berkas Excel akhir. Pastikan Anda mengganti "DIREKTORI DOKUMEN ANDA" dengan jalur sebenarnya di sistem Anda.

## Langkah 2: Buat Buku Kerja Baru dan Isi dengan Data

Selanjutnya, mari buat buku kerja pertama kita dan tambahkan beberapa contoh data ke dalamnya. Berikut caranya:

```csharp
// Buat Buku Kerja baru
Workbook excelWorkbook0 = new Workbook();
// Dapatkan lembar kerja pertama di buku
Worksheet ws0 = excelWorkbook0.Worksheets[0];

// Taruh beberapa data ke dalam baris header (A1:A4)
for (int i = 0; i < 5; i++)
{
    ws0.Cells[i, 0].PutValue(string.Format("Header Row {0}", i));
}

// Taruh beberapa data detail (A5:A999)
for (int i = 5; i < 1000; i++)
{
    ws0.Cells[i, 0].PutValue(string.Format("Detail Row {0}", i));
}
```
Di sini, kita membuat buku kerja pertama dan mengisi lembar kerja pertama (`ws0`) dengan tajuk dan baris detail. Data simulasi ini akan membantu Anda memvisualisasikan proses penyalinan nanti.

## Langkah 3: Siapkan Pengaturan Halaman untuk Pencetakan

Mari konfigurasikan pengaturan halaman untuk mengulang baris tajuk saat mencetak, supaya kita dapat melihat fitur tersebut beraksi:

```csharp
// Tentukan objek pagesetup berdasarkan lembar kerja pertama
PageSetup pagesetup = ws0.PageSetup;
//Lima baris pertama diulang di setiap halaman
pagesetup.PrintTitleRows = "$1:$5";
```
 Bagian ini menentukan bagaimana dokumen Anda akan dicetak. Dengan mengatur`PrintTitleRows`, kami memastikan bahwa lima baris pertama akan muncul pada setiap halaman yang dicetak, yang sangat berguna untuk keterbacaan.

## Langkah 4: Buat Buku Kerja Kedua

Sekarang, kita perlu membuat buku kerja lain tempat kita akan menyalin lembar kerja pertama:

```csharp
// Buat Buku Kerja lainnya
Workbook excelWorkbook1 = new Workbook();
// Dapatkan lembar kerja pertama di buku
Worksheet ws1 = excelWorkbook1.Worksheets[0];
// Beri nama lembar kerja
ws1.Name = "MySheet";
```
Kami telah membuat buku kerja baru (`excelWorkbook1`) dan mengganti nama lembar kerja pertama menjadi "MySheet". Sebaiknya Anda memberi nama yang bermakna pada lembar kerja Anda agar lebih mudah diakses nanti.

## Langkah 5: Salin Lembar Kerja

Mari salin konten dari lembar kerja buku kerja pertama ke buku kerja kedua:

```csharp
// Salin data dari lembar kerja pertama buku kerja pertama ke dalam
// lembar kerja pertama dari buku kerja kedua
ws1.Copy(ws0);
```
 Itu`Copy` metode mengambil semua konten dari lembar kerja sumber (`ws0`) dan menduplikasinya ke lembar kerja tujuan (`ws1`). Sederhana sekali, bukan?

## Langkah 6: Simpan Buku Kerja Baru

Terakhir, mari simpan buku kerja yang baru kita buat:

```csharp
// Simpan file excel
excelWorkbook1.Save(dataDir + "CopyWorksheetFromWorkbookToOther_out.xls");
```
Baris ini akan menyimpan buku kerja kedua Anda di jalur yang ditentukan. Jangan lupa untuk memeriksa apakah semuanya terlihat baik setelah Anda menjalankan kode Anda!

## Kesimpulan

Nah, itu dia! Anda telah berhasil mempelajari cara menyalin lembar kerja dari satu buku kerja ke buku kerja lain menggunakan Aspose.Cells for .NET. Ini adalah keterampilan yang sangat berguna, terutama saat menangani sejumlah besar data yang tersebar di berbagai berkas. Hanya dengan beberapa baris kode, Anda dapat mengatur, mengelola, dan mengakses data Excel dengan lebih mudah.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?  
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat, memanipulasi, mengonversi, dan merender file Excel dalam berbagai format.

### Bisakah saya menggunakan Aspose.Cells secara gratis?  
 Ya, Aspose.Cells menawarkan uji coba gratis, yang dapat Anda akses[Di Sini](https://releases.aspose.com/).

### Bagaimana cara mendapatkan lisensi sementara untuk Aspose.Cells?  
 Anda dapat meminta lisensi sementara dengan mengunjungi[tautan ini](https://purchase.aspose.com/temporary-license/).

### Di mana saya dapat menemukan dokumentasi lebih lanjut tentang Aspose.Cells?  
 Anda dapat menemukan dokumentasi terperinci[Di Sini](https://reference.aspose.com/cells/net/).

### Apakah ada dukungan yang tersedia untuk pengguna Aspose.Cells?  
 Tentu saja! Anda bisa mendapatkan dukungan melalui[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
