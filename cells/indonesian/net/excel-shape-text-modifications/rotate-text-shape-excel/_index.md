---
title: Memutar Teks dengan Bentuk di Excel
linktitle: Memutar Teks dengan Bentuk di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara memutar teks dengan bentuk di Excel menggunakan Aspose.Cells for .NET. Ikuti panduan langkah demi langkah ini untuk presentasi Excel yang sempurna.
weight: 12
url: /id/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memutar Teks dengan Bentuk di Excel

## Perkenalan
Dalam dunia Excel, representasi visual sama pentingnya dengan data itu sendiri. Baik Anda sedang menyusun laporan atau mendesain dasbor dinamis, cara informasi ditata dapat memengaruhi keterbacaan dan tampilan keseluruhannya secara drastis. Jadi, pernahkah Anda ingin memutar teks untuk menyelaraskannya dengan bentuk secara bergaya? Anda beruntung! Dalam tutorial ini, kita akan mendalami cara memutar teks dengan bentuk menggunakan Aspose.Cells untuk .NET, memastikan spreadsheet Anda tidak hanya memberikan informasi tetapi juga mengesankan.
## Prasyarat
Sebelum kita mulai, mari pastikan Anda memiliki semua yang Anda butuhkan:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda, karena di sanalah kita akan menulis kode.
2.  Aspose.Cells untuk .NET: Anda memerlukan pustaka Aspose.Cells. Anda dapat[unduh versi terbaru di sini](https://releases.aspose.com/cells/net/) atau mencobanya secara gratis dengan[uji coba gratis](https://releases.aspose.com/).
3. Pengetahuan Dasar C#: Keakraban dengan C# dan lingkungan .NET akan sangat membantu, meskipun kami akan memandu Anda di setiap langkah.
4.  File Excel: Contoh file Excel, sebut saja`sampleRotateTextWithShapeInsideWorksheet.xlsx`, diperlukan untuk menguji kode kita. Anda harus meletakkan berkas ini di direktori yang mudah diakses.
Sudah siap? Luar biasa! Mari kita masuk ke bagian yang menyenangkan.
## Paket Impor
Untuk memulai, kita perlu mengimpor paket-paket yang diperlukan ke dalam proyek kita. Berikut cara melakukannya:
### Buat Proyek Baru
1. Buka Visual Studio.
2. Pilih "Buat proyek baru."
3. Pilih "Aplikasi Konsol" dan pilih C# sebagai bahasa pemrograman pilihan Anda.
### Instal Aspose.Cells
Sekarang, mari tambahkan Aspose.Cells ke proyek Anda. Anda dapat melakukannya menggunakan NuGet Package Manager:
1. Buka "Alat" di menu atas.
2. Pilih "NuGet Package Manager" dan kemudian "Kelola Paket NuGet untuk Solusi."
3. Cari "Aspose.Cells."
4. Klik "Instal" untuk menambahkannya ke proyek Anda.
### Tambahkan Menggunakan Arahan
Di bagian atas file C# utama Anda, Anda perlu menambahkan perintah berikut:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Sekarang, kita siap untuk memulai coding!
Mari kita uraikan prosesnya menjadi beberapa langkah yang mudah dipahami. Berikut cara memutar teks dengan bentuk dalam file Excel:
## Langkah 1: Siapkan Jalur Direktori Anda
Pertama, Anda perlu menyiapkan direktori sumber dan keluaran tempat file Excel akan disimpan. Berikut caranya:
```csharp
//Direktori sumber
string sourceDir = "Your Document Directory"; // Atur direktori dokumen Anda
//Direktori keluaran
string outputDir = "Your Document Directory"; // Atur direktori keluaran Anda
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat Anda`sampleRotateTextWithShapeInsideWorksheet.xlsx` berkas berada.
## Langkah 2: Muat File Excel Sampel
Sekarang, mari kita muat contoh berkas Excel. Ini penting, karena kita ingin memanipulasi data yang ada.
```csharp
//Muat contoh file Excel.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Langkah 3: Akses Lembar Kerja
Setelah berkas dimuat, kita perlu mengakses lembar kerja tertentu yang ingin kita ubah. Dalam kasus kita, ini adalah lembar kerja pertama.
```csharp
//Akses lembar kerja pertama.
Worksheet ws = wb.Worksheets[0];
```
## Langkah 4: Memodifikasi Sel
Selanjutnya, kita akan mengubah sel tertentu untuk menampilkan pesan. Dalam contoh kita, kita akan menggunakan sel B4.
```csharp
//Akses sel B4 dan tambahkan pesan di dalamnya.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Langkah ini adalah tentang komunikasi—memastikan siapa pun yang membuka lembar ini mengerti apa yang sedang kita ubah.
## Langkah 5: Akses Bentuk Pertama
Untuk memutar teks, kita memerlukan bentuk untuk bekerja. Di sini, kita akan mengakses bentuk pertama di lembar kerja.
```csharp
//Akses bentuk pertama.
Shape sh = ws.Shapes[0];
```
## Langkah 6: Sesuaikan Penyelarasan Teks Bentuk
Di sinilah keajaiban terjadi. Kita akan menyesuaikan properti perataan teks pada bentuk tersebut.
```csharp
//Akses perataan teks bentuk.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Jangan memutar teks dengan bentuk dengan menyetel RotateTextWithShape sebagai salah.
shapeTextAlignment.RotateTextWithShape = false;
```
 Dengan pengaturan`RotateTextWithShape` ke false, kami memastikan bahwa teks tetap tegak dan tidak berputar mengikuti bentuknya, sehingga menjaga semuanya tetap rapi dan teratur.
## Langkah 7: Simpan File Excel Output
Terakhir, mari simpan perubahan kita ke berkas Excel baru. Ini memastikan kita tidak kehilangan suntingan kita dan memiliki keluaran yang rapi.
```csharp
//Simpan berkas Excel keluaran.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Selesai! File output Anda kini telah disimpan, termasuk teks di sel B4 dan penyesuaian yang dilakukan pada bentuknya.
## Langkah 8: Jalankan Kode
 Di dalam kamu`Main` metode, bungkus semua potongan kode di atas, dan jalankan proyek Anda. Lihat perubahan yang tercermin dalam berkas keluaran Anda!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Kesimpulan
Memutar teks dengan bentuk di Excel menggunakan Aspose.Cells untuk .NET mungkin tampak seperti proses yang rumit pada awalnya, tetapi cukup mudah setelah Anda menguraikannya. Dengan mengikuti langkah-langkah sederhana ini, Anda dapat menyesuaikan lembar kerja Anda agar terlihat lebih profesional dan menarik secara visual. Sekarang, baik Anda melakukan ini untuk klien atau proyek pribadi Anda, semua orang akan memuji kualitas pekerjaan Anda!
## Pertanyaan yang Sering Diajukan
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya! Anda dapat menggunakan[uji coba gratis](https://releases.aspose.com/) untuk mencoba perpustakaan.
### Versi Excel apa yang didukung Aspose.Cells?
Aspose.Cells mendukung berbagai format Excel, termasuk XLS, XLSX, CSV, dan banyak lagi.
### Apakah mungkin untuk memutar teks dengan bentuk di versi Excel yang lebih lama?
Ya, fungsionalitas ini dapat diterapkan ke format lama yang didukung oleh Aspose.Cells.
### Di mana saya dapat menemukan dokumentasi lebih lanjut tentang Aspose.Cells?
 Anda dapat menjelajahi komprehensif[dokumentasi](https://reference.aspose.com/cells/net/) untuk wawasan lebih dalam.
### Bagaimana cara mendapatkan dukungan untuk Aspose.Cells?
 Anda dapat meminta dukungan dengan mengunjungi[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
