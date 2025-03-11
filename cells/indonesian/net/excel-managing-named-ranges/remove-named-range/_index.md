---
title: Hapus Rentang Bernama di Excel
linktitle: Hapus Rentang Bernama di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menghapus rentang bernama di Excel menggunakan Aspose.Cells untuk .NET dengan petunjuk langkah demi langkah yang terperinci.
weight: 11
url: /id/net/excel-managing-named-ranges/remove-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hapus Rentang Bernama di Excel

## Perkenalan
Excel telah menjadi bagian penting dalam manajemen dan analisis data bagi banyak individu dan organisasi. Baik Anda seorang analis data berpengalaman atau sekadar seseorang yang senang mengatur data, menguasai Excel sangatlah penting. Hari ini, kita akan membahas fitur yang spesifik namun hebat: menghapus rentang bernama menggunakan Aspose.Cells untuk .NET. Panduan ini akan memandu Anda melalui langkah-langkah untuk mencapainya secara efektif. Jadi, gulung lengan baju Anda, dan mari kita mulai!

## Prasyarat

Sebelum kita masuk ke pengkodean sebenarnya, ada beberapa hal yang perlu Anda siapkan:

### Pengaturan Lingkungan .NET

Untuk bekerja dengan Aspose.Cells for .NET dengan lancar, pastikan Anda memiliki hal berikut:

1.  Visual Studio: Unduh dan instal Visual Studio (Community Edition juga bagus) yang dapat Anda temukan di[Situs web Visual Studio](https://visualstudio.microsoft.com/).
2. .NET Framework: Pastikan Anda menggunakan versi .NET Framework yang sesuai. Aspose.Cells mendukung .NET Framework 4.0 dan yang lebih baru.
3. Pustaka Aspose.Cells: Anda perlu mengunduh dan merujuk pustaka Aspose.Cells for .NET di aplikasi Anda. Anda dapat menemukan paket yang dapat diunduh[Di Sini](https://releases.aspose.com/cells/net/).

### Pemahaman Dasar C#

Anda memerlukan pemahaman dasar tentang pemrograman C#. Ini akan membantu Anda memahami potongan kode yang akan kita bahas.

### Akses ke File Excel

Pastikan Anda memiliki berkas Excel untuk bereksperimen. Jika tidak, Anda dapat membuatnya dengan cepat menggunakan Microsoft Excel.

## Paket Impor

Setelah prasyarat terpenuhi, mari impor paket yang akan dibutuhkan dalam proyek kita. Buka Visual Studio dan buat aplikasi konsol baru. Lalu, sertakan namespace berikut dalam program Anda:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Pengaturan ini memungkinkan Anda memanfaatkan fungsionalitas yang disediakan oleh Aspose.Cells untuk memanipulasi lembar Excel dengan mudah.

## Langkah 1: Menyiapkan Direktori Output

Pertama-tama, kita perlu menentukan di mana file output kita akan disimpan. Hal ini penting untuk menghindari kebingungan di kemudian hari tentang di mana file Anda berada.

```csharp
// Direktori keluaran
string outputDir = "Your Document Directory Here\\";
```

 Mengganti`"Your Document Directory Here\\"`dengan jalur di komputer Anda di mana Anda ingin menyimpan berkas Anda.

## Langkah 2: Membuat Instansiasi Buku Kerja Baru

Bagaimana cara memulai dengan lembaran baru? Tentu saja dengan membuat buku kerja baru! Buku kerja ini akan berfungsi sebagai kanvas kosong kita.

```csharp
// Buat Buku Kerja baru.
Workbook workbook = new Workbook();
```

Baris kode ini menciptakan buku kerja baru yang dapat kita manipulasi.

## Langkah 3: Mengakses Koleksi Lembar Kerja

Setiap buku kerja terdiri dari satu atau beberapa lembar kerja. Untuk bekerja dalam lembar kerja tertentu, kita perlu mengakses koleksi ini.

```csharp
// Dapatkan semua lembar kerja dalam buku.
WorksheetCollection worksheets = workbook.Worksheets;
```

Di sini, kami telah mengambil semua lembar kerja yang tersedia di buku kerja baru kami.

## Langkah 4: Memilih Lembar Kerja Pertama

Berikutnya, kita ingin beroperasi dalam lembar kerja pertama—titik awal default dalam banyak kasus.

```csharp
// Dapatkan lembar kerja pertama dalam koleksi lembar kerja.
Worksheet worksheet = workbook.Worksheets[0];
```

Potongan kode ini memungkinkan kita memilih lembar kerja pertama dengan mudah.

## Langkah 5: Membuat Rentang Bernama

Sekarang, mari kita buat rentang bernama, yang merupakan bagian penting dari tutorial ini. Ini akan memungkinkan kita untuk mengilustrasikan cara menghapus rentang bernama nanti.

```csharp
// Membuat rentang sel.
Range range1 = worksheet.Cells.CreateRange("E12", "I12");

// Sebutkan rentangnya.
range1.Name = "FirstRange";
```

Di sini, kita mendefinisikan rentang dari sel E12 hingga I12 dan menamainya “FirstRange.”

## Langkah 6: Memformat Rentang Bernama

Untuk menunjukkan betapa serbagunanya Aspose.Cells, mari tambahkan beberapa pemformatan ke rentang bernama kita.

```csharp
// Tetapkan batas garis luar ke rentang.
range1.SetOutlineBorder(BorderType.TopBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.BottomBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.LeftBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.RightBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
```

Kami menambahkan batas sedang berwarna biru tua di sekeliling jangkauan kami untuk membuatnya menarik secara visual.

## Langkah 7: Memasukkan Data ke dalam Rentang

Berikutnya, kita dapat mengisi sel kita dengan sejumlah data untuk membuatnya berfungsi.

```csharp
// Masukkan beberapa data dengan beberapa format ke dalam beberapa sel dalam rentang.
range1[0, 0].PutValue("Test");            
range1[0, 4].PutValue(123);
```

Pada langkah ini, kami menempatkan kata "Tes" di sel E12 dan angka 123 di sel I12.

## Langkah 8: Membuat Rentang Bernama Lainnya

Untuk mengilustrasikan maksud kami lebih jauh, kami akan membuat rentang bernama lain yang mirip dengan yang pertama.

```csharp
//Buat rentang sel lainnya.
Range range2 = worksheet.Cells.CreateRange("B3", "F3");

// Sebutkan rentangnya.
range2.Name = "SecondRange";
```

Sekarang kami memiliki rentang bernama lain yang disebut "SecondRange" yang tersedia untuk digunakan.

## Langkah 9: Menyalin Rentang Pertama ke Rentang Kedua

Mari kita tunjukkan cara menggunakan rentang kedua dengan menyalin data dari rentang pertama.

```csharp
// Salin rentang pertama ke rentang kedua.
range2.Copy(range1);
```

Dengan langkah ini, kita telah secara efektif menduplikasi data dari "FirstRange" ke "SecondRange."

## Langkah 10: Menghapus Rentang Bernama

Sekarang untuk inti dari tutorial kita: menghapus rentang bernama. Di sinilah semuanya menyatu.

```csharp
// Hapus rentang bernama sebelumnya (range1) beserta isinya.
worksheet.Cells.ClearRange(range1.FirstRow, range1.FirstColumn, range1.FirstRow + range1.RowCount - 1, range1.FirstColumn + range1.ColumnCount - 1);
```

Baris ini menghapus konten rentang yang ingin kita hapus, memastikan bahwa kita tidak meninggalkan jejak!

## Langkah 11: Menghapus Rentang Bernama dari Lembar Kerja

Langkah terakhir yang penting adalah menghapus rentang bernama dari koleksi nama lembar kerja.

```csharp
worksheets.Names.RemoveAt(0);
```

Ini secara efektif akan menghapus rentang bernama “FirstRange” dari buku kerja.

## Langkah 12: Menyimpan Buku Kerja

Terakhir namun tidak kalah pentingnya, mari kita simpan pekerjaan kita. 

```csharp
// Simpan berkas Excel.
workbook.Save(outputDir + "outputRemoveNamedRange.xlsx");
```

Perintah ini menyimpan buku kerja Anda dengan perubahan yang kita buat—di sinilah semua kerja keras Anda disimpan!

## Langkah 13: Konfirmasi Eksekusi Berhasil

Untuk menyelesaikan semuanya dengan rapi, Anda mungkin ingin menampilkan pesan sukses pada konsol.

```csharp
Console.WriteLine("RemoveNamedRange executed successfully.");
```

Ini memberitahukan Anda bahwa seluruh operasi telah selesai tanpa hambatan!

## Kesimpulan

Dengan mengikuti panduan ini, Anda telah mempelajari cara memanipulasi rentang bernama di Excel menggunakan Aspose.Cells for .NET. Anda telah membuat rentang, mengisinya dengan data, menyalin isinya, dan akhirnya menghapusnya sambil memastikan file Excel Anda tetap teratur dan bersih. Excel, seperti kafe yang ramai, berkembang pesat karena keteraturan. Jadi, apakah Anda mengelola data untuk laporan atau merapikan lembar anggaran pribadi Anda, menguasai rentang bernama dapat membantu Anda menghasilkan beberapa solusi yang efisien. 

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang dirancang untuk memanipulasi file Excel secara terprogram.

### Bisakah saya menghapus beberapa rentang bernama sekaligus?
Ya, Anda dapat melakukan pengulangan pada kumpulan rentang bernama dan menghapusnya bila diperlukan.

### Apakah ada versi uji coba yang tersedia?
 Ya, Anda dapat mengunduh uji coba gratis Aspose.Cells[Di Sini](https://releases.aspose.com/).

### Bahasa pemrograman apa yang didukung Aspose.Cells?
Aplikasi ini terutama mendukung bahasa .NET seperti C# dan VB.NET, antara lain.

### Di mana saya dapat mencari dukungan jika saya menghadapi masalah?
 Anda dapat mengunjungi[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9) untuk bantuan atas pertanyaan apa pun.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
