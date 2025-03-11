---
title: Mengontrol Sumber Daya Eksternal di Excel ke PDF di Aspose.Cells
linktitle: Mengontrol Sumber Daya Eksternal di Excel ke PDF di Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara mengontrol sumber daya eksternal dalam konversi Excel ke PDF menggunakan Aspose.Cells untuk .NET dengan panduan kami yang mudah diikuti.
weight: 12
url: /id/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengontrol Sumber Daya Eksternal di Excel ke PDF di Aspose.Cells

## Perkenalan
Di era digital saat ini, mengonversi lembar kerja Excel ke dokumen PDF merupakan tugas yang umum. Baik itu menyiapkan laporan, data keuangan, atau materi presentasi, Anda ingin memastikan bahwa PDF Anda terlihat persis seperti yang Anda inginkan. Aspose.Cells untuk .NET adalah pustaka tangguh yang memungkinkan Anda mengendalikan proses konversi ini hingga ke detail terakhir, terutama saat menangani sumber daya eksternal seperti gambar yang menyertai file Excel Anda. Dalam panduan ini, kami akan membahas cara mengendalikan sumber daya eksternal selama proses konversi Excel ke PDF menggunakan Aspose.Cells. Jadi, ambil minuman favorit Anda, dan mari kita mulai!
## Prasyarat
Sebelum kita masuk ke inti permasalahan, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai. Berikut daftar periksa singkatnya:
1. Visual Studio atau IDE apa pun yang kompatibel dengan .NET: Anda memerlukan lingkungan untuk menulis dan menguji kode Anda.
2.  Aspose.Cells untuk .NET: Jika Anda belum menginstalnya, kunjungi[Unduhan Aspose](https://releases.aspose.com/cells/net/) halaman dan ambil versi terbaru.
3. Pengetahuan Dasar tentang C#: Pemahaman terhadap bahasa pemrograman C# akan sangat membantu. Jika Anda tidak yakin tentang konsep apa pun, jangan ragu untuk mencarinya.
4. Contoh Berkas Excel: Siapkan berkas Excel dengan sumber daya eksternal yang ingin Anda konversi. Anda dapat menggunakan berkas contoh yang disediakan "samplePdfSaveOptions_StreamProvider.xlsx".
5. Berkas Gambar untuk Pengujian: Ini akan digunakan sebagai sumber daya eksternal selama konversi. Berkas gambar "newPdfSaveOptions_StreamProvider.png" adalah tempat penampung yang baik.
## Paket Impor
Untuk memulai, Anda perlu mengimpor namespace yang diperlukan dari pustaka Aspose.Cells. Ini penting untuk mengakses fungsinya. Pastikan untuk menambahkan perintah berikut di bagian atas berkas Anda:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Paket-paket ini akan menyediakan semua kelas dan metode penting yang Anda perlukan untuk menjalankan tugas Anda.
## Langkah 1: Buat Kelas Penyedia Aliran Anda
 Tugas pertama adalah membuat kelas penyedia aliran yang mengimplementasikan`IStreamProvider` antarmuka. Kelas ini akan memungkinkan Anda untuk mengontrol bagaimana sumber daya eksternal dimuat.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Baca gambar baru dalam aliran memori dan tetapkan ke properti Stream
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
Di kelas ini:
- CloseStream: Metode ini akan dipanggil saat aliran ditutup. Untuk saat ini, kami hanya menulis pesan debug untuk pelacakan.
-  InitStream: Di sinilah keajaiban dimulai. Di sini, Anda akan membaca gambar eksternal Anda sebagai array byte, mengubahnya menjadi aliran memori, dan menetapkannya ke`options.Stream` milik.
## Langkah 2: Siapkan Direktori Sumber dan Output
Sekarang penyedia streaming Anda sudah siap, saatnya menentukan di mana file Excel Anda berada dan di mana Anda ingin menyimpan PDF Anda.
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Document Directory";
```
 Cukup ganti`"Your Document Directory"` dengan jalur sebenarnya di komputer tempat file Anda berada. Menjaga file Anda tetap teratur adalah kuncinya!
## Langkah 3: Muat File Excel Anda
Berikutnya, Anda akan memuat berkas Excel yang ingin Anda gunakan untuk membuat PDF.
```csharp
// Muat file Excel sumber yang berisi gambar eksternal
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
 Kami menggunakan`Workbook` kelas dari Aspose.Cells, yang mewakili berkas Excel Anda. Berkas tersebut dapat mencakup berbagai sumber daya eksternal seperti gambar yang ingin Anda kendalikan selama konversi.
## Langkah 4: Atur Opsi Penyimpanan PDF
Sebelum Anda menyimpan buku kerja sebagai PDF, mari tentukan bagaimana Anda ingin menyimpannya. Anda dapat menyesuaikan opsi ini sesuai kebutuhan Anda.
```csharp
// Tentukan Opsi Penyimpanan Pdf - Penyedia Aliran
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Simpan setiap lembar di halaman baru
```
 Di sini, kita membuat contoh baru`PdfSaveOptions` , yang memungkinkan Anda menyesuaikan bagaimana format PDF Anda.`OnePagePerSheet`opsi ini berguna untuk memastikan bahwa setiap lembar Excel mendapatkan halamannya sendiri dalam PDF final.
## Langkah 5: Tetapkan Penyedia Streaming Anda
Dengan opsi PDF yang Anda tetapkan, Anda perlu memberi tahu Aspose untuk menggunakan penyedia aliran kustom Anda untuk sumber daya eksternal.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
 Garis ini menghubungkan Anda`Workbook` contoh dengan`MyStreamProvider` kelas yang Anda buat sebelumnya. Ini berarti bahwa setiap kali sumber daya eksternal ditemukan selama konversi, penyedia Anda akan menanganinya sebagaimana ditentukan.
## Langkah 6: Simpan Buku Kerja sebagai PDF
Setelah semuanya siap, saatnya menyimpan buku kerja Excel Anda sebagai PDF.
```csharp
// Simpan buku kerja ke Pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
 Dengan menelepon`Save` metode pada objek buku kerja dan meneruskan direktori keluaran Anda beserta opsi PDF, Anda mengonversi file Excel menjadi PDF yang diformat dengan indah.
## Langkah 7: Konfirmasikan Eksekusi yang Berhasil
Sebagai penutup, alangkah baiknya untuk mengonfirmasi bahwa proses Anda telah berhasil!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Mencetak pesan sukses ke konsol membantu Anda tetap terinformasi tentang status operasi Anda. Merupakan kebiasaan yang baik untuk menyertakan konfirmasi kecil ini dalam kode Anda.
## Kesimpulan
Nah, itu dia! Dengan mengikuti langkah-langkah mudah ini, Anda dapat mengontrol secara ahli bagaimana sumber daya eksternal ditangani selama konversi Excel ke PDF menggunakan Aspose.Cells. Ini berarti bahwa dokumen Anda sekarang dapat menyertakan gambar dan elemen eksternal lainnya secara akurat, memastikan produk akhir yang sempurna setiap saat.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?  
Aspose.Cells adalah pustaka hebat untuk pengembang .NET yang memungkinkan Anda membuat, memanipulasi, mengonversi, dan merender file Excel dalam berbagai format.
### Bagaimana cara mengunduh Aspose.Cells?  
 Anda dapat mengunduh versi terbaru Aspose.Cells dari[Tautan unduhan](https://releases.aspose.com/cells/net/).
### Dapatkah saya mencoba Aspose.Cells secara gratis?  
 Ya! Anda bisa mendapatkan uji coba gratis dengan mengunjungi[Halaman uji coba gratis](https://releases.aspose.com/).
### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?  
 Untuk pertanyaan terkait dukungan, Anda dapat mengunjungi[Forum Dukungan Aspose](https://forum.aspose.com/c/cells/9).
### Bagaimana cara memperoleh lisensi sementara untuk Aspose.Cells?  
 Anda dapat mengajukan permohonan lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
