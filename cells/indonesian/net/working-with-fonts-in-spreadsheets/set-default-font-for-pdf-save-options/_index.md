---
title: Tetapkan Font Default untuk Opsi Penyimpanan PDF
linktitle: Tetapkan Font Default untuk Opsi Penyimpanan PDF
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengatur font default untuk opsi penyimpanan PDF menggunakan Aspose.Cells untuk .NET, yang memastikan dokumen Anda terlihat sempurna setiap saat.
weight: 11
url: /id/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tetapkan Font Default untuk Opsi Penyimpanan PDF

## Perkenalan
Saat membuat laporan, faktur, atau dokumen lain dalam format PDF, memastikan konten Anda terlihat tepat adalah yang terpenting. Font memainkan peran penting dalam menjaga daya tarik visual dan keterbacaan dokumen Anda. Namun, apa yang terjadi jika font yang Anda gunakan dalam file Excel tidak tersedia di sistem tempat Anda membuat PDF? Di sinilah Aspose.Cells for .NET berguna. Pustaka canggih ini memungkinkan Anda menyetel font default untuk opsi penyimpanan PDF, memastikan dokumen Anda terlihat profesional dan konsisten, di mana pun dokumen dibuka.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki hal berikut:
1. Visual Studio: Anda memerlukan lingkungan pengembangan seperti Visual Studio untuk menulis dan mengeksekusi kode Anda.
2.  Aspose.Cells untuk .NET: Anda dapat mengunduh versi terbaru dari[tautan ini](https://releases.aspose.com/cells/net/)Atau, Anda dapat menginstalnya melalui NuGet Package Manager di Visual Studio.
3. Pengetahuan Dasar C#: Memahami dasar-dasar C# akan membantu Anda mengikuti contoh kode.
4. Contoh Berkas Excel: Siapkan contoh berkas Excel untuk pengujian. Anda dapat membuat berkas dengan berbagai fon dan gaya untuk melihat bagaimana Aspose.Cells menangani fon yang hilang.
## Paket Impor
Sebelum Anda dapat menggunakan Aspose.Cells dalam proyek Anda, Anda perlu mengimpor paket yang diperlukan. Berikut cara melakukannya:
1. Buka Proyek Anda: Luncurkan Visual Studio dan buka proyek Anda yang ada atau buat yang baru.
2. Tambahkan Referensi: Klik kanan pada proyek Anda di Solution Explorer dan pilih "Kelola Paket NuGet."
3. Instal Aspose.Cells: Cari "Aspose.Cells" dan klik tombol "Instal".
4. Tambahkan Petunjuk Penggunaan: Di bagian atas file C# Anda, sertakan namespace berikut:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Langkah 1: Siapkan Direktori Anda
Sebelum bekerja dengan file, penting untuk menentukan direktori sumber dan output. Ini akan memudahkan Anda menemukan file Excel input dan menyimpan file output yang dihasilkan.
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya ke direktori Anda.
## Langkah 2: Buka File Excel
 Sekarang setelah kita menyiapkan direktori kita, mari kita buka file Excel yang ingin Anda gunakan.`Workbook` kelas di Aspose.Cells digunakan untuk memuat dokumen Excel.
```csharp
// Buka file Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Pastikan untuk mengganti nama berkas dengan nama berkas Anda yang sebenarnya.
## Langkah 3: Siapkan Opsi Rendering Gambar
Selanjutnya, kita perlu mengonfigurasi opsi rendering untuk mengonversi lembar Excel kita ke format gambar. Kita akan membuat contoh`ImageOrPrintOptions`, menentukan jenis gambar dan font default.
```csharp
// Merender ke format file PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 Dalam potongan kode ini, kami mengatur`CheckWorkbookDefaultFont` properti untuk`false`, yang berarti jika ada font yang hilang, font default yang ditentukan (“Times New Roman”) akan digunakan sebagai gantinya.
## Langkah 4: Render Lembar sebagai Gambar
 Sekarang, mari kita render lembar pertama buku kerja sebagai gambar PNG. Kita akan menggunakan`SheetRender` kelas untuk menyelesaikan hal ini.
```csharp
// Render lembar kerja pertama menjadi gambar
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Langkah 5: Ubah Jenis Gambar dan Render ke TIFF
 Jika Anda ingin merender lembar yang sama ke format gambar yang berbeda, seperti TIFF, Anda cukup mengubah`ImageType` properti dan ulangi proses rendering.
```csharp
// Diatur ke format TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Langkah 6: Konfigurasikan Opsi Penyimpanan PDF
 Selanjutnya, mari kita atur opsi penyimpanan PDF. Kita akan membuat contoh`PdfSaveOptions`menetapkan font default, dan menentukan bahwa kita ingin memeriksa font yang hilang.
```csharp
// Konfigurasikan opsi penyimpanan PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Langkah 7: Simpan Buku Kerja sebagai PDF
Setelah opsi penyimpanan dikonfigurasi, saatnya menyimpan buku kerja Excel kita sebagai berkas PDF. 
```csharp
// Simpan buku kerja ke PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Langkah 8: Konfirmasi Eksekusi
Terakhir, sebaiknya Anda memberi tahu pengguna bahwa proses telah berhasil diselesaikan. Anda dapat melakukannya dengan menggunakan pesan konsol sederhana.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Kesimpulan
Aspose.Cells menyediakan cara yang fleksibel dan tangguh untuk menangani manipulasi file Excel, sehingga memudahkan pengembang untuk membuat dokumen yang menarik secara visual dengan format yang tetap terjaga. Baik Anda mengerjakan laporan, dokumen keuangan, atau bentuk presentasi data lainnya, memiliki kendali atas tampilan font dapat meningkatkan kualitas output secara signifikan.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang canggih yang memungkinkan pengembang untuk memanipulasi berkas Excel tanpa perlu menginstal Microsoft Excel. Pustaka ini mendukung berbagai format berkas dan menawarkan fitur-fitur lengkap untuk bekerja dengan lembar kerja.
### Bagaimana cara mengatur font default untuk file Excel saya?
 Anda dapat mengatur font default menggunakan`PdfSaveOptions` class dan tentukan nama font yang diinginkan. Ini memastikan bahwa meskipun font tidak ada, dokumen Anda akan menggunakan font default yang telah Anda tentukan.
### Bisakah saya mengonversi file Excel ke format selain PDF?
Tentu saja! Aspose.Cells memungkinkan Anda mengonversi file Excel ke berbagai format, termasuk gambar (PNG, TIFF), HTML, CSV, dan banyak lagi.
### Apakah Aspose.Cells gratis untuk digunakan?
Aspose.Cells adalah produk komersial, tetapi Anda dapat mencobanya secara gratis dengan versi uji coba terbatas. Untuk fungsionalitas penuh, Anda perlu membeli lisensi.
### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?
 Anda dapat menemukan dukungan untuk Aspose.Cells dengan mengunjungi[Forum Aspose](https://forum.aspose.com/c/cells/9), tempat Anda dapat mengajukan pertanyaan dan berbagi wawasan dengan pengguna dan pengembang lain.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
