---
title: Menerapkan Pemformatan Bersyarat saat Runtime di Excel
linktitle: Menerapkan Pemformatan Bersyarat saat Runtime di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menerapkan pemformatan bersyarat saat runtime di Excel dengan Aspose.Cells untuk .NET dalam panduan langkah demi langkah yang komprehensif ini.
weight: 11
url: /id/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menerapkan Pemformatan Bersyarat saat Runtime di Excel

## Perkenalan

mereka adalah alat yang hebat untuk analisis dan visualisasi data. Salah satu fitur Excel yang menonjol adalah pemformatan bersyarat, yang memungkinkan pengguna menerapkan gaya pemformatan tertentu ke sel berdasarkan nilainya. Ini dapat mempermudah identifikasi tren, menyorot poin data penting, atau sekadar membuat data lebih mudah dibaca. Jika Anda ingin menerapkan pemformatan bersyarat dalam file Excel Anda secara terprogram, Anda berada di tempat yang tepat! Dalam panduan ini, kami akan memandu cara menerapkan pemformatan bersyarat saat runtime menggunakan Aspose.Cells untuk .NET.

## Prasyarat
Sebelum menyelami kodenya, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Anda dapat menggunakan versi apa pun yang mendukung pengembangan .NET.
2.  Aspose.Cells untuk .NET: Anda harus menginstal Aspose.Cells untuk .NET. Anda dapat mengunduhnya dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
4. .NET Framework: Pastikan proyek Anda menargetkan versi .NET Framework yang kompatibel.

Sekarang setelah prasyaratnya terpenuhi, mari masuk ke bagian yang menyenangkan!

## Paket Impor
Untuk memulai dengan Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan dalam proyek C# Anda. Berikut cara melakukannya:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ruang nama ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk memanipulasi file Excel dan menerapkan pemformatan bersyarat.

Sekarang, mari kita uraikan proses penerapan pemformatan bersyarat ke dalam langkah-langkah yang lebih mudah dikelola.

## Langkah 1: Siapkan Proyek Anda
Pertama-tama, Anda perlu membuat proyek C# baru di Visual Studio. Berikut caranya:

1. Buka Visual Studio dan pilih File > Baru > Proyek.
2. Pilih Aplikasi Konsol (.NET Framework) dan beri nama proyek Anda.
3. Klik Buat.

## Langkah 2: Tambahkan Referensi Aspose.Cells
Setelah proyek Anda disiapkan, Anda perlu menambahkan referensi ke pustaka Aspose.Cells:

1. Klik kanan pada proyek Anda di Solution Explorer.
2. Pilih Kelola Paket NuGet.
3. Cari Aspose.Cells dan instal.

Ini akan memungkinkan Anda untuk menggunakan semua fungsionalitas yang disediakan oleh pustaka Aspose.Cells.

## Langkah 3: Buat Objek Buku Kerja
Selanjutnya, mari buat buku kerja dan lembar kerja baru. Di sinilah semua keajaiban terjadi:

```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

Pada langkah ini, kita menentukan direktori tempat file Excel akan disimpan, membuat buku kerja baru, dan mengakses lembar kerja pertama.

## Langkah 4: Tambahkan Pemformatan Bersyarat
Sekarang, mari tambahkan beberapa format bersyarat. Kita akan mulai dengan membuat objek format bersyarat yang kosong:

```csharp
// Menambahkan format kondisional kosong
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Di sini, kami menambahkan koleksi pemformatan bersyarat baru ke lembar kerja kami, yang akan menampung aturan pemformatan kami.

## Langkah 5: Tentukan Rentang Format
Selanjutnya, kita perlu menentukan rentang sel yang akan menerapkan pemformatan bersyarat. Misalnya, kita ingin memformat baris pertama dan kolom kedua:

```csharp
// Mengatur rentang format bersyarat.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

Dalam kode ini, kami mendefinisikan dua area untuk pemformatan bersyarat. Area pertama adalah untuk sel di (0,0) dan yang kedua untuk (1,1). Jangan ragu untuk menyesuaikan rentang ini berdasarkan kebutuhan spesifik Anda!

## Langkah 6: Tambahkan Kondisi Pemformatan Bersyarat
Sekarang saatnya menentukan kondisi untuk pemformatan kita. Katakanlah kita ingin menyorot sel berdasarkan nilainya:

```csharp
// Menambahkan kondisi.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Menambahkan kondisi.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 Pada langkah ini, kami menambahkan dua kondisi: satu untuk nilai antara`A2` Dan`100` , dan satu lagi untuk nilai antara`50` Dan`100`Fitur ini memungkinkan Anda menyorot sel secara dinamis berdasarkan nilainya.

## Langkah 7: Mengatur Gaya Pemformatan
Setelah kondisi kita terpenuhi, kita sekarang dapat mengatur gaya pemformatan. Mari ubah warna latar belakang untuk kondisi kita:

```csharp
// Mengatur warna latar belakang.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Di sini, kita akan menyetel warna latar belakang kondisi pertama menjadi merah. Anda dapat menyesuaikannya lebih lanjut dengan mengubah warna font, batas, dan gaya lainnya sesuai kebutuhan!

## Langkah 8: Simpan File Excel
Akhirnya, saatnya menyimpan pekerjaan kita! Kita akan menyimpan buku kerja ke direktori yang ditentukan:

```csharp
// Menyimpan file Excel
workbook.Save(dataDir + "output.xls");
```

Baris kode ini menyimpan berkas Excel dengan format bersyarat yang diterapkan. Pastikan untuk memeriksa direktori yang ditentukan untuk berkas keluaran Anda!

## Kesimpulan
Nah, itu dia! Anda telah berhasil menerapkan pemformatan bersyarat saat runtime di Excel menggunakan Aspose.Cells untuk .NET. Pustaka canggih ini memudahkan Anda memanipulasi file Excel secara terprogram, sehingga Anda dapat mengotomatiskan tugas-tugas yang membosankan dan menyempurnakan presentasi data Anda. Baik Anda mengerjakan proyek kecil atau aplikasi berskala besar, Aspose.Cells dapat membantu Anda menyederhanakan alur kerja dan meningkatkan produktivitas Anda.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel secara terprogram.

### Bisakah saya menggunakan Aspose.Cells dengan bahasa pemrograman lain?
Ya, Aspose.Cells tersedia untuk berbagai bahasa pemrograman, termasuk Java, Python, dan lainnya.

### Apakah ada uji coba gratis yang tersedia untuk Aspose.Cells?
 Ya, Anda dapat mengunduh uji coba gratis dari[Situs web Aspose](https://releases.aspose.com/).

### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Anda bisa mendapatkan dukungan dengan mengunjungi[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9).

### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?
 Ya, lisensi diperlukan untuk penggunaan komersial, tetapi Anda dapat meminta lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
