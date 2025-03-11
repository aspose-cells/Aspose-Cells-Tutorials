---
title: Mengekspor Lembar Kerja CSS Secara Terpisah dalam Output HTML
linktitle: Mengekspor Lembar Kerja CSS Secara Terpisah dalam Output HTML
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengekspor lembar kerja Excel ke HTML secara efektif dengan CSS terpisah menggunakan Aspose.Cells untuk .NET dalam tutorial langkah demi langkah yang komprehensif ini.
weight: 14
url: /id/net/exporting-excel-to-html-with-advanced-options/exporting-worksheet-css-separately/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengekspor Lembar Kerja CSS Secara Terpisah dalam Output HTML

## Perkenalan
Dalam panduan ini, Anda akan mempelajari cara mengekspor lembar kerja Excel ke HTML, dengan fokus khusus pada pengeksporan CSS secara terpisah. Hal ini tidak hanya meningkatkan kemudahan pemeliharaan gaya Anda, tetapi juga meningkatkan efisiensi alur kerja Anda. Sekarang, mari kita bahas prasyaratnya dan langsung mulai!
## Prasyarat
Sebelum kita masuk ke kode, berikut ini yang Anda perlukan agar tutorial ini berjalan lancar:
1. Lisensi Aspose.Cells untuk .NET: Anda memerlukan lisensi untuk memanfaatkan sepenuhnya fitur Aspose.Cells. Anda dapat[unduh versi terbaru](https://releases.aspose.com/cells/net/)atau dapatkan[lisensi sementara](https://purchase.aspose.com/temporary-license/) Jika Anda hanya menguji air.
2. Lingkungan Pengembangan: Idealnya, Anda harus menginstal Visual Studio untuk menjalankan proyek .NET Anda dengan lancar.
3. Pengetahuan Dasar C#: Memiliki sedikit dasar dalam pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
4.  Dokumentasi Referensi: Biasakan diri Anda dengan[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk fitur dan kemampuan tambahan.
Setelah Anda memenuhi prasyarat ini, kita siap untuk memasuki bagian yang seru!
## Paket Impor
Untuk memulai, Anda perlu mengimpor namespace yang relevan dari Aspose.Cells. Berikut cara mengaturnya:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Drawing;
```
Pengaturan ini akan memberi Anda semua alat yang diperlukan untuk membuat buku kerja, memanipulasi lembar kerja, dan mengelola gaya.

Mari kita uraikan ini ke dalam bagian-bagian yang lebih mudah dikelola, setiap langkah akan membawa Anda lebih dekat ke tujuan Anda untuk mengekspor lembar kerja Excel yang menarik itu langsung ke dalam berkas HTML dengan semua isi CSS terpisah!
## Langkah 1: Mengatur Direktori Output
Hal pertama yang perlu Anda lakukan adalah memutuskan di mana Anda ingin menyimpan berkas HTML yang diekspor. Ini penting karena jika Anda salah, Anda mungkin akan mencari dokumen Anda di mana-mana!
```csharp
string outputDir = "Your Document Directory";
```
 Cukup ganti`"Your Document Directory"` dengan jalur tempat Anda ingin menyimpan berkas. Misalnya:`string outputDir = @"C:\MyExports\";`.
## Langkah 2: Buat Objek Buku Kerja
Selanjutnya, kita perlu membuat objek buku kerja baru. Bayangkan buku kerja sebagai kanvas kosong tempat semua keajaiban terjadi!
```csharp
Workbook wb = new Workbook();
```
 Dengan melakukan ini, kita telah menginisialisasi instance baru dari kelas Workbook. Variabel ini`wb` sekarang akan menampung seluruh lembar kerja Excel kita.
## Langkah 3: Akses Lembar Kerja Pertama
Sekarang saatnya untuk menyelami kanvas Anda dan mengambil lembar kerja pertama. Bagian ini mudah, karena kita hanya memerlukan lembar pertama untuk tutorial ini.
```csharp
Worksheet ws = wb.Worksheets[0];
```
Baris ini mengambil lembar kerja pertama dalam buku kerja Anda, siap untuk dimanipulasi.
## Langkah 4: Memanipulasi Nilai Sel
Sekarang ke bagian yang menyenangkan—mari masukkan beberapa data ke dalam sel! Anda dapat memilih sel mana saja, tetapi untuk contoh ini, kita akan menggunakan sel “B5”.
```csharp
Cell cell = ws.Cells["B5"];
cell.PutValue("This is some text.");
```
Dengan baris ini, kita telah memasukkan teks "Ini adalah teks." ke dalam sel B5. Sederhana, bukan? 
## Langkah 5: Mengatur Gaya Sel
Mari tambahkan sedikit gaya! Kita akan menata teks kita dengan mengubah warna font menjadi merah. 
```csharp
Style st = cell.GetStyle();
st.Font.Color = Color.Red;
cell.SetStyle(st);
```
Langkah ini mengambil gaya sel B5 yang ada, mengubah warna font menjadi merah, lalu menerapkan kembali gaya baru. Sekarang sel Anda bukan sekadar kotak teks biasa!
## Langkah 6: Tentukan Opsi Penyimpanan HTML
Pada tahap ini, kami akan menyiapkan opsi penyimpanan HTML. Ini penting untuk memastikan bahwa CSS Anda diekspor secara terpisah.
```csharp
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.ExportWorksheetCSSSeparately = true;
```
 Dengan`ExportWorksheetCSSSeparately` Jika opsi disetel ke benar, Anda memberi tahu perpustakaan untuk menangani gaya CSS secara berbeda, bukan menanamkannya langsung ke dalam berkas HTML.
## Langkah 7: Simpan Buku Kerja sebagai HTML
Akhirnya, saatnya menyimpan semua kerja keras! Baris ini menyimpan buku kerja Anda di direktori keluaran yang ditentukan sebagai berkas HTML.
```csharp
wb.Save(outputDir + "outputExportWorksheetCSSSeparately.html", opts);
```
Di sini, kami memberi nama file output kami`outputExportWorksheetCSSSeparately.html`Dan voilà—Anda berhasil!
## Langkah 8: Konfirmasi Eksekusi
Untuk mengetahui semuanya berjalan lancar, sebaiknya selalu tampilkan pesan konfirmasi.
```csharp
Console.WriteLine("ExportWorksheetCSSSeparatelyInOutputHTML executed successfully.");
```
Sekarang Anda dapat menjalankan kode Anda, dan jika Anda melihat pesan konfirmasi, selamat—Anda telah berhasil mengekspor lembar kerja Excel Anda dengan CSS terpisah!
## Kesimpulan
Dan itu dia—panduan Anda sendiri untuk mengekspor lembar kerja Excel ke HTML sambil tetap memisahkan CSS, berkat Aspose.Cells untuk .NET. Ini tidak hanya menjaga gaya Anda tetap teratur tetapi juga memberi Anda lebih banyak fleksibilitas kapan pun Anda perlu membuat perubahan di masa mendatang. 
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET canggih yang memungkinkan Anda membuat, memodifikasi, dan mengonversi lembar kerja Excel tanpa memerlukan Microsoft Excel.
### Bagaimana saya bisa mendapatkan uji coba Aspose.Cells gratis?
 Anda dapat mengunduh uji coba gratis dari[Aspose.Cells merilis halaman](https://releases.aspose.com/).
### Bisakah saya menyesuaikan keluaran HTML lebih lanjut?
Ya, Aspose.Cells menyediakan berbagai opsi untuk menyesuaikan keluaran HTML sesuai kebutuhan Anda.
### Apakah mungkin untuk memanipulasi elemen lembar lainnya menggunakan Aspose.Cells?
Tentu saja! Aspose.Cells memungkinkan Anda untuk memanipulasi grafik, gambar, dan banyak elemen lainnya dalam spreadsheet.
### Di mana saya dapat menemukan sumber daya tambahan?
 Lihat di sini[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk panduan terperinci dan referensi API.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
