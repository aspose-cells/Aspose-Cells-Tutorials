---
title: Gabungkan Sel dalam Rentang Bernama di Excel
linktitle: Gabungkan Sel dalam Rentang Bernama di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menggabungkan sel dalam rentang bernama menggunakan Aspose.Cells for .NET dalam tutorial langkah demi langkah ini. Temukan cara memformat, memberi gaya, dan mengotomatiskan laporan Excel.
weight: 11
url: /id/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gabungkan Sel dalam Rentang Bernama di Excel

## Perkenalan

Saat bekerja dengan file Excel secara terprogram, salah satu tugas umum yang mungkin Anda hadapi adalah menggabungkan sel dalam rentang bernama. Baik Anda mengotomatiskan pembuatan laporan, membuat dasbor, atau sekadar mengelola kumpulan data besar, menggabungkan sel merupakan teknik penting. Dalam tutorial ini, kita akan menjelajahi cara menggabungkan sel dalam rentang bernama menggunakan Aspose.Cells for .NET—pustaka canggih yang memungkinkan pengembang untuk memanipulasi file Excel tanpa perlu menginstal Microsoft Excel.

## Prasyarat

Sebelum kita mulai, pastikan Anda telah menyiapkan hal-hal berikut:

-  Aspose.Cells untuk .NET: Anda dapat mengunduhnya dari[Aspose.Cells merilis halaman](https://releases.aspose.com/cells/net/).
- .NET Framework terinstal di komputer Anda.
- Pemahaman dasar tentang C#: Keakraban dengan konsep seperti kelas, metode, dan objek akan membantu.

## Paket Impor

Sebelum kita mulai membuat kode, Anda perlu mengimpor namespace yang diperlukan. Namespace ini akan memberi Anda akses ke fungsionalitas pustaka Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Setelah prasyarat dan paket-paket selesai, mari beralih ke bagian yang menyenangkan: pengkodean!

Berikut rincian cara menggabungkan sel dalam rentang bernama di lembar Excel menggunakan Aspose.Cells for .NET.

## Langkah 1: Buat Buku Kerja Baru

Hal pertama yang kita butuhkan adalah buku kerja. Buku kerja dalam istilah Excel setara dengan berkas Excel. Mari kita buat satu.

```csharp
// Buat Buku Kerja baru.
Workbook wb1 = new Workbook();
```

Dengan menginisialisasi buku kerja baru, kita sekarang memiliki berkas Excel kosong yang siap dimanipulasi. Ini seperti memulai dengan kanvas kosong!

## Langkah 2: Akses Lembar Kerja Pertama

Setiap buku kerja berisi lembar kerja, dan dalam kasus ini, kita ingin bekerja dengan lembar kerja pertama. Mari kita ambil lembar kerja tersebut!

```csharp
// Dapatkan lembar kerja pertama dalam buku kerja.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Bayangkan lembar kerja sebagai tab-tab individual dalam berkas Excel tempat data sebenarnya berada. Secara default, kita mengakses tab pertama.

## Langkah 3: Buat Rentang Sel

Sekarang setelah kita memiliki lembar kerja, saatnya membuat rentang. Rentang mengacu pada blok sel, yang dapat mencakup beberapa baris dan kolom.

```csharp
//Buat rentang.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Di sini, kami memilih sel dari D6 hingga I12—blok yang mencakup beberapa baris dan kolom. Kami akan segera menggabungkan rentang ini!

## Langkah 4: Beri Nama Rentangnya

Memberi nama suatu rentang akan memudahkan referensinya nanti, terutama saat menangani kumpulan data besar.

```csharp
// Sebutkan rentangnya.
mrange.Name = "TestRange";
```

Dengan memberi nama rentang ini "TestRange", kita dapat dengan cepat mengambilnya nanti dalam kode, tanpa perlu menentukan koordinat sel lagi.

## Langkah 5: Gabungkan Rentang Sel

Sekarang untuk keajaibannya—menggabungkan sel-sel dalam rentang yang baru saja kita buat!

```csharp
// Gabungkan sel-sel rentang.
mrange.Merge();
```

Langkah ini menggabungkan semua sel dari D6 hingga I12 menjadi satu sel tunggal. Sempurna untuk hal-hal seperti judul atau ringkasan!

## Langkah 6: Ambil Rentang Bernama

Setelah sel-sel digabungkan, kita mungkin ingin menerapkan beberapa pemformatan. Pertama-tama mari kita ambil rentang bernama kita.

```csharp
// Dapatkan jangkauannya.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Mengambil rentang berdasarkan nama memungkinkan kita melakukan operasi lebih lanjut, seperti menambahkan gaya atau memasukkan data.

## Langkah 7: Tentukan Gaya untuk Sel yang Digabungkan

Apa gunanya sel gabungan jika tampilannya tidak rapi? Mari buat objek gaya untuk menyelaraskan teks dan menerapkan warna latar belakang.

```csharp
// Tentukan objek gaya.
Style style = wb1.CreateStyle();

// Mengatur perataan.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Di sini, kita meratakan teks secara horizontal dan vertikal di bagian tengah, dan menetapkan warna latar belakang biru muda (aqua). Bergaya, bukan?

## Langkah 8: Terapkan Gaya ke Rentang

Setelah menentukan gaya, saatnya menerapkannya ke rentang gabungan.

```csharp
// Buat objek StyleFlag.
StyleFlag flag = new StyleFlag();

// Jadikan atribut gaya relatif AKTIF.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Terapkan gaya ke rentang.
range1.ApplyStyle(style, flag);
```

 Itu`StyleFlag` memberi tahu Aspose.Cells properti gaya mana yang akan diterapkan—penyelarasan, bayangan, dsb. Ini memberi Anda kontrol terperinci atas cara gaya diterapkan.

## Langkah 9: Masukkan Data ke dalam Rentang Gabungan

Apa itu rentang yang diformat tanpa konten? Mari tambahkan beberapa teks.

```csharp
// Masukkan data ke dalam rentang.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Ini menempatkan teks "Selamat Datang di Aspose API" ke dalam sel pertama dari rentang gabungan kita. Dengan penggabungan sel, teks ini akan menjangkau semua sel dari D6 hingga I12.

## Langkah 10: Simpan File Excel

Terakhir, mari simpan buku kerja sebagai berkas Excel.

```csharp
// Simpan berkas Excel.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Di sini, buku kerja disimpan dengan nama "outputMergeCellsInNamedRange.xlsx" di direktori yang Anda tentukan.

## Kesimpulan

Nah, itu dia! Anda telah berhasil menggabungkan sel dalam rentang bernama, menerapkan beberapa format yang cantik, dan bahkan memasukkan beberapa data—semuanya dengan Aspose.Cells untuk .NET. Baik Anda sedang mengerjakan otomatisasi laporan, memanipulasi file Excel, atau sekadar mempelajari teknik baru, panduan langkah demi langkah ini akan memberi Anda dasar yang Anda butuhkan.

## Pertanyaan yang Sering Diajukan

### Bisakah saya menggabungkan beberapa rentang yang tidak bersebelahan di Aspose.Cells?  
Tidak, Anda hanya dapat menggabungkan sel yang bersebelahan di Aspose.Cells.

### Bisakah saya membatalkan operasi penggabungan secara terprogram?  
 Setelah sel digabungkan, Anda dapat memisahkannya menggunakan`UnMerge()` metode di Aspose.Cells.

### Apakah penggabungan sel menghapus data di dalamnya?  
Jika ada data dalam sel sebelum penggabungan, maka data dari sel pertama dalam rentang akan dipertahankan.

### Dapatkah saya menerapkan gaya yang berbeda pada sel individual dalam rentang gabungan?  
Tidak, rentang gabungan berfungsi sebagai satu sel tunggal. Jadi, Anda tidak dapat menerapkan gaya berbeda ke sel individual di dalamnya.

### Bagaimana cara mengakses sel yang digabungkan setelah penggabungan?  
Setelah penggabungan, Anda masih dapat mengakses sel yang digabungkan menggunakan koordinat sudut kiri atasnya.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
