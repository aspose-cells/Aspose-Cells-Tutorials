---
title: Mengonversi ke XPS dalam .NET
linktitle: Mengonversi ke XPS dalam .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengonversi file Excel ke format XPS menggunakan Aspose.Cells for .NET hanya dalam beberapa langkah mudah, dipandu dengan contoh kode praktis.
weight: 10
url: /id/net/xps-and-pdf-operations/converting-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi ke XPS dalam .NET

## Perkenalan
Saat harus mengonversi file Excel ke format XPS, Anda mungkin merasa sedikit kewalahan, terutama jika Anda baru mengenal dunia pemrograman atau baru saja terjun ke pengembangan .NET. Namun, jangan khawatir! Dalam panduan ini, kami akan menguraikan proses penggunaan Aspose.Cells untuk .NET seperti seorang profesional. Setelah selesai membaca, Anda tidak hanya akan memiliki pemahaman yang jelas tentang cara melakukannya, tetapi juga memperoleh beberapa wawasan praktis yang dapat meningkatkan keterampilan pengodean Anda. Jadi, mari kita mulai!
## Prasyarat
Sebelum Anda menyelami seluk-beluk konversi, pastikan Anda memiliki semua yang Anda butuhkan. Berikut ini yang Anda perlukan:
1. Visual Studio: Ini adalah IDE tempat Anda akan menulis kode. Pastikan Anda telah menginstalnya.
2.  Pustaka Aspose.Cells: Anda memerlukan pustaka ini untuk menangani file Excel secara efisien. Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar tentang .NET: Keakraban dengan C# atau VB.NET akan membantu Anda memahami contoh kami dengan lebih baik.
4. File Excel: Siapkan contoh file Excel (untuk tutorial ini, kita akan menggunakan "Book1.xls") di direktori kerja Anda.

## Paket Impor
Setelah kita membahas prasyaratnya, mari kita lanjutkan dengan mengimpor paket yang diperlukan. Mengimpor namespace yang tepat sangat penting, karena ini memberi tahu kompiler di mana menemukan kelas dan metode yang akan kita gunakan.
### Siapkan Proyek Anda
Hal pertama yang harus dilakukan! Buka Visual Studio dan buat proyek baru. Pilih aplikasi konsol karena mudah dan cocok untuk tugas semacam ini.
### Tambahkan Aspose.Cells ke Proyek Anda
Untuk memulai Aspose.Cells, Anda perlu menambahkan pustaka. Untuk melakukannya:
1. Klik kanan pada proyek Anda di Solution Explorer.
2. Klik “Kelola Paket NuGet.”
3. Cari “Aspose.Cells” dan klik “Instal.”
### Impor Namespace yang Diperlukan
Di awal berkas C#, Anda perlu mengimpor Aspose.Cells. Ini melibatkan penambahan perintah penggunaan berikut:
```csharp
using System.IO;
using Aspose.Cells;
```
Mari kita uraikan proses mengonversi berkas Excel ke format XPS menjadi langkah-langkah sederhana dan mudah dikelola. 
## Langkah 1: Tentukan Direktori Dokumen Anda
Di sinilah Anda menentukan jalur tempat file Excel Anda berada. Ini penting karena kode perlu mengetahui lokasi file tersebut.
```csharp
string dataDir = "Your Document Directory"; // Pastikan untuk mengganti dengan jalur Anda yang sebenarnya
```
## Langkah 2: Buka File Excel
Sekarang, mari muat berkas Excel Anda ke objek Aspose Workbook. Tindakan ini memberi program Anda akses ke data di dalam berkas Excel tersebut.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Di sini, kita membuat contoh baru dari`Workbook` kelas dan memuat "Book1.xls" ke dalamnya.
## Langkah 3: Akses Lembar Kerja Pertama
Selanjutnya, kita perlu mendapatkan lembar kerja yang ingin kita kerjakan. Karena kita menggunakan lembar kerja pertama, kode kita akan terlihat seperti ini:
```csharp
Worksheet sheet = workbook.Worksheets[0]; // Mengakses lembar kerja pertama
```
Baris kode ini memungkinkan Anda mengakses lembar kerja pertama untuk perintah selanjutnya.
## Langkah 4: Konfigurasikan Opsi Gambar dan Cetak
 Sekarang kita perlu menentukan bagaimana kita ingin menampilkan output kita. Ini melibatkan pembuatan instance dari`ImageOrPrintOptions` dan mengatur format keluaran yang diinginkan.
```csharp
Aspose.Cells.Rendering.ImageOrPrintOptions options = new Aspose.Cells.Rendering.ImageOrPrintOptions();
options.SaveFormat = SaveFormat.Xps; // Mengatur format keluaran ke XPS
```
Langkah ini memberi tahu Aspose bahwa kita ingin mengonversi konten Excel ke format XPS.
## Langkah 5: Render Lembaran
Setelah opsi ditetapkan, saatnya untuk merender lembar tertentu:
```csharp
Aspose.Cells.Rendering.SheetRender sr = new Aspose.Cells.Rendering.SheetRender(sheet, options);
sr.ToImage(0, dataDir + "out_printingxps.out.xps");
```
 Di sini, kami telah membuat`SheetRender` objek, yang mengurus proses rendering. Metode`ToImage` menangani konversi aktual dan menyimpan output yang ditampilkan sebagai "out_printingxps.out.xps".
## Langkah 6: Ekspor Seluruh Buku Kerja ke XPS
Jika Anda ingin mengonversi seluruh buku kerja, bukan hanya satu lembar, Anda dapat mengikuti langkah tambahan ini:
```csharp
WorkbookRender wr = new WorkbookRender(workbook, options);
wr.ToImage(dataDir + "out_whole_printingxps.out.xps");
```
Cuplikan kode ini memungkinkan Anda mengekspor keseluruhan buku kerja sekaligus, menjadikannya efisien jika Anda memiliki beberapa lembar kerja yang akan dikonversi.
## Kesimpulan
Selamat! Anda telah berhasil mengonversi file Excel ke format XPS menggunakan pustaka Aspose.Cells di .NET. Mungkin tampak seperti banyak langkah, tetapi masing-masing langkah memainkan peran penting dalam proses tersebut. Dengan pengetahuan ini, Anda diperlengkapi dengan baik untuk menangani file Excel dalam aplikasi Anda dan mengoptimalkannya untuk berbagai format. Jadi, lain kali seseorang bertanya kepada Anda cara mengonversi spreadsheet yang menyebalkan itu, Anda akan tahu persis apa yang harus dilakukan!
## Pertanyaan yang Sering Diajukan
### Apa itu format XPS?
XPS (XML Paper Specification) adalah format dokumen tetap yang mempertahankan tata letak dan tampilan dokumen.
### Apakah saya perlu membeli Aspose.Cells untuk menggunakannya?
 Anda dapat mencoba uji coba gratis Aspose.Cells yang tersedia[Di Sini](https://releases.aspose.com/)Setelah itu, Anda mungkin perlu membeli lisensi untuk fungsionalitas penuh.
### Bisakah saya mengonversi beberapa file Excel sekaligus?
Ya, Anda dapat mengadaptasi kode untuk mengulang beberapa file dalam direktori dan menerapkan logika konversi yang sama untuk setiap file.
### Bagaimana jika saya hanya perlu mengonversi lembar tertentu?
 Anda dapat menentukan indeks lembar yang Anda inginkan di`SheetRender` objek seperti yang ditunjukkan dalam langkah kita.
### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells?
 Anda dapat menjelajahi[dokumentasi](https://reference.aspose.com/cells/net/) untuk fitur dan pilihan lebih lanjut yang tersedia di perpustakaan.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
