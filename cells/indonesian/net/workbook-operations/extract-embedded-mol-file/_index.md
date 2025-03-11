---
title: Ekstrak File Mol Tertanam dari Buku Kerja
linktitle: Ekstrak File Mol Tertanam dari Buku Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengekstrak file MOL tertanam dari buku kerja Excel menggunakan Aspose.Cells untuk .NET dalam tutorial langkah demi langkah terperinci ini.
weight: 18
url: /id/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak File Mol Tertanam dari Buku Kerja

## Perkenalan
Saat mengelola data dalam buku kerja Excel, terkadang Anda menemukan berbagai objek tertanam yang tidak dalam format standar. Salah satu format tersebut adalah MOL (Molecular Structure File), yang umumnya digunakan dalam kimia untuk merepresentasikan informasi molekuler. Jika Anda ingin mengekstrak file MOL ini dari buku kerja Excel menggunakan Aspose.Cells for .NET, Anda telah menemukan panduan yang tepat. Dalam artikel ini, kami akan memandu Anda melalui proses tersebut langkah demi langkah, mengungkap setiap bagian di sepanjang jalan.
## Prasyarat
Sebelum mempelajari kode, penting untuk memastikan bahwa Anda memiliki keterampilan dan alat yang diperlukan. Berikut ini yang Anda perlukan:
1. Pemahaman Dasar tentang Pemrograman .NET: Anda harus terbiasa dengan C# dan kerangka kerja .NET.
2.  Aspose.Cells untuk .NET: Pastikan Anda memiliki pustaka Aspose.Cells. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/).
3. IDE: Anda dapat menggunakan Visual Studio atau IDE lain yang kompatibel dengan .NET.
4. Buku Kerja Excel dengan File MOL Tertanam: Untuk tutorial ini, Anda memerlukan file Excel yang berisi objek MOL. Anda dapat membuatnya sendiri atau menggunakan file contoh apa pun.
## Paket Impor
Untuk memulai, Anda perlu mengimpor namespace yang diperlukan dalam proyek Anda. Hal ini penting untuk mengakses fungsi Aspose.Cells. Berikut cara melakukannya:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Ruang nama ini akan memungkinkan Anda untuk memanipulasi buku kerja, mengakses lembar kerja, dan bekerja dengan berkas secara umum.
Sekarang setelah prasyarat kita terpenuhi, mari selami kodenya dan pahami setiap langkah yang terlibat dalam mengekstrak file MOL yang tertanam dari buku kerja Excel. 
## Langkah 1: Menyiapkan Direktori Anda
Langkah pertama adalah menentukan lokasi dokumen sumber dan lokasi penyimpanan file MOL yang diekstrak. Mari kita atur direktori tersebut.
```csharp
string SourceDir = "Your Document Directory"; // Ganti dengan jalur direktori Anda
string outputDir = "Your Document Directory"; // Ganti dengan jalur keluaran Anda
```
 Di sini, Anda mengganti`"Your Document Directory"`dengan jalur ke direktori Anda yang sebenarnya. Penting agar direktori sumber dan keluaran dapat diakses oleh aplikasi Anda.
## Langkah 2: Memuat Buku Kerja
Setelah Anda menyiapkan direktori, tugas berikutnya adalah memuat buku kerja Excel. Mari kita lakukan sekarang.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Kami sedang membuat sebuah contoh dari`Workbook` kelas dan meneruskan jalur ke file Excel kita yang bernama`EmbeddedMolSample.xlsx`Langkah ini menginisialisasi buku kerja, yang memungkinkan Anda mengakses isinya.
## Langkah 3: Mengulangi Lembar Kerja
Sekarang setelah buku kerja Anda dimuat, Anda perlu melakukan pengulangan pada setiap lembar kerja di dalam buku kerja tersebut. Ini memungkinkan Anda memeriksa setiap lembar untuk objek yang disematkan.

```csharp
var index = 1; // Digunakan untuk memberi nama file MOL yang diekstraksi
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Logika ekstraksi lebih lanjut ada di sini
}
```

 Di sini, Anda menggunakan`foreach` loop untuk menavigasi melalui lembar kerja. Untuk setiap lembar kerja, Anda mengakses`OleObjects` koleksi yang berisi semua objek yang tertanam.
## Langkah 4: Mengekstrak File MOL
Sekarang tibalah bagian yang penting—mengekstrak file MOL dari objek OLE. Ini memerlukan loop lain di dalam loop lembar kerja.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Untuk setiap objek OLE yang Anda temukan, Anda membuat file baru di direktori output.`ObjectData` milik`OleObject` menyimpan data objek tertanam, yang Anda tulis ke file yang baru dibuat menggunakan`FileStream`File diberi nama secara berurutan (`OleObject1.mol`, `OleObject2.mol` , dll.) berdasarkan`index` variabel.
## Langkah 5: Konfirmasi Penyelesaian Proses
Terakhir, setelah semua file MOL diekstraksi, ada baiknya untuk memberi tahu pengguna bahwa prosesnya telah berhasil diselesaikan.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Baris ini hanya mencetak pesan ke konsol yang memberi tahu Anda bahwa ekstraksi berhasil. Ini adalah sentuhan yang bagus untuk umpan balik pengguna.
## Kesimpulan
Nah, itu dia! Anda telah berhasil mengekstrak file MOL yang disematkan dari buku kerja Excel menggunakan Aspose.Cells for .NET. Proses ini mengintegrasikan beberapa langkah inti, yang memastikan pendekatan terstruktur untuk menangani objek yang disematkan. Baik Anda melakukan penelitian ilmiah, analisis kimia, atau sekadar menangani kumpulan data yang kompleks, kemampuan untuk mengekstrak dan memanipulasi jenis file ini dapat membuat perbedaan yang signifikan dalam cara Anda mengelola informasi. 
## Pertanyaan yang Sering Diajukan
### Bisakah saya mengekstrak tipe file lain selain MOL dari Excel?
Ya, Anda dapat mengekstrak berbagai jenis file tertanam lainnya dengan teknik serupa.
### Apakah Aspose.Cells gratis untuk digunakan?
 Aspose.Cells adalah pustaka komersial, tetapi Anda dapat[cobalah gratis untuk jangka waktu terbatas](https://releases.aspose.com/).
### Apakah metode ini berfungsi dengan semua versi Excel?
Ya, selama format file didukung oleh Aspose.Cells.
### Bisakah saya mengotomatiskan proses ekstraksi ini?
Tentu saja! Anda dapat mengotomatiskan proses ini dengan menempatkan kode dalam tugas terjadwal atau skrip.
### Di mana saya dapat menemukan dokumentasi lebih lanjut tentang Aspose.Cells?
 Anda dapat memeriksa[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk rincian dan contoh lebih lanjut.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
