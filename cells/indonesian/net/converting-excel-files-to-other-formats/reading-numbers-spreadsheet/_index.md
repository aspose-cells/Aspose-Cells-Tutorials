---
"description": "Pelajari cara membaca lembar kerja Numbers dan mengonversinya ke PDF menggunakan Aspose.Cells untuk .NET dalam tutorial terperinci ini."
"linktitle": "Membaca Lembar Kerja Angka Secara Terprogram di .NET"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Membaca Lembar Kerja Angka Secara Terprogram di .NET"
"url": "/id/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Membaca Lembar Kerja Angka Secara Terprogram di .NET

## Bevezetés
Di dunia digital saat ini, manajemen data merupakan keterampilan yang penting, dan spreadsheet berada di garis depan organisasi data. Namun, bagaimana jika Anda perlu bekerja dengan spreadsheet Numbers—file yang dibuat oleh aplikasi Numbers Apple—menggunakan .NET? Jangan khawatir; Anda tidak sendirian! Dalam tutorial ini, kita akan membahas proses membaca spreadsheet Numbers secara terprogram dengan Aspose.Cells untuk .NET. Anda akan mempelajari cara memuat file Numbers dan mengonversinya ke PDF.
## Előfeltételek
Sebelum kita memulai, ada beberapa hal yang perlu Anda siapkan:
1. Aspose.Cells .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.Cells könyvtár. Letöltheti [itt](https://releases.aspose.com/cells/net/).
2. Visual Studio: Disarankan agar Visual Studio (atau IDE lain yang kompatibel dengan .NET) menginstal di komputer Anda.
3. Pengetahuan Dasar C#: Sedikit pengetahuan dengan pemrograman C# akan membantu Anda mengikutinya dengan lancar.
4. Direktori Dokumen Anda: Anda memerlukan direktori tempat file Numbers Anda disimpan, beserta lokasi untuk menyimpan PDF yang dikonversi.
Setelah Anda memenuhi prasyarat ini, Anda siap untuk memulai!
## Csomagok importálása
Pertama-tama, kita perlu mengimpor paket-paket yang diperlukan ke dalam proyek C# kita. Ini adalah langkah penting karena memungkinkan kita memanfaatkan fungsionalitas yang disediakan oleh pustaka Aspose.Cells.
1. Buka proyek C# Anda di Visual Studio.
2. Tambahkan referensi ke pustaka Aspose.Cells:
   - Jika Anda menggunakan NuGet, jalankan saja perintah berikut di Konsol Manajer Paket:
```
 Install-Package Aspose.Cells
 ```
3. Impor namespace yang diperlukan dalam kode Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Sekarang setelah kita mengimpor paket yang diperlukan, mari beralih ke panduan langkah demi langkah untuk membaca lembar kerja Numbers.
## Langkah 1: Tentukan Direktori Sumber dan Output
Pada langkah ini, kita akan menyiapkan direktori tempat file Numbers sumber Anda berada dan tempat Anda ingin menyimpan PDF keluaran.
```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory"; // Perbarui ini ke direktori Anda yang sebenarnya
// Kimeneti könyvtár
string outputDir = "Your Document Directory"; // Perbarui ini ke direktori Anda yang sebenarnya
```
Di sini, kita mendefinisikan dua variabel string, `sourceDir` és `outputDir`, untuk menentukan lokasi file input dan output. Pastikan untuk mengganti `"Your Document Directory"` dengan jalur sebenarnya pada sistem Anda.
## Langkah 2: Siapkan Opsi Muat untuk Format Angka
Selanjutnya, kita akan menentukan opsi pemuatan untuk membaca lembar kerja Numbers. Langkah ini penting karena memberi tahu Aspose cara menginterpretasikan berkas Numbers.
```csharp
// Tentukan opsi muat; kami ingin memuat spreadsheet Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
Létrehozunk egy `LoadOptions` objek dan tentukan formatnya sebagai `LoadFormat.Numbers`Ini memberi tahu pustaka Aspose.Cells bahwa kita sedang bekerja dengan berkas Numbers. 
## Langkah 3: Muat Lembar Kerja Angka ke dalam Buku Kerja
Sekarang, saatnya untuk memuat spreadsheet Numbers yang sebenarnya ke dalam `Workbook` objektum.
```csharp
// Muat lembar kerja Angka ke dalam buku kerja dengan opsi muat di atas
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
Kami membuat contoh sebuah `Workbook` objek dan berikan jalur file Numbers beserta opsi muat kami. Pastikan nama file (`sampleNumbersByAppleInc.numbers`) cocok dengan nama sebenarnya file Numbers Anda.
## Langkah 4: Simpan Buku Kerja sebagai PDF
Setelah file Numbers berhasil dimuat, langkah berikutnya adalah menyimpannya dalam format lain—khususnya PDF.
```csharp
// Simpan buku kerja ke format PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
Di sini, kami menyebutnya `Save` módszer a `Workbook` objek, menentukan jalur file keluaran dan format tempat kita ingin menyimpannya. Dalam kasus ini, kita menyimpannya sebagai PDF. Pastikan nama file keluaran (`outputNumbersByAppleInc.pdf`) bersifat unik dan tidak menimpa berkas apa pun yang ada.
## 5. lépés: Siker megerősítése
Terakhir, mari tambahkan pesan untuk mengonfirmasi bahwa operasi kita berhasil.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Baris kode ini akan mencetak pesan sukses ke konsol setelah semuanya selesai. Selalu menyenangkan untuk mendapatkan masukan, bukan?
## Következtetés
Nah, itu dia! Anda telah berhasil membaca spreadsheet Numbers dan mengonversinya ke PDF menggunakan Aspose.Cells untuk .NET. Pustaka canggih ini memungkinkan Anda untuk memanipulasi spreadsheet dengan mudah, sehingga memudahkan tugas pengelolaan data Anda. Baik Anda sedang mengembangkan aplikasi atau hanya perlu menangani spreadsheet dengan lebih efisien, Aspose.Cells adalah alat yang fantastis untuk dimiliki dalam perangkat Anda.
## GYIK
### Jenis file apa yang dapat dibaca Aspose.Cells?  
Aspose.Cells dapat membaca berbagai format file, termasuk file XLS, XLSX, CSV, dan Numbers. 
### Bisakah saya mengedit file Numbers menggunakan Aspose.Cells?  
Ya, Anda dapat membaca, memanipulasi, dan menyimpan file Numbers dengan Aspose.Cells.
### Ingyenesen használható az Aspose.Cells?  
Aspose.Cells menawarkan uji coba gratis, tetapi Anda memerlukan lisensi untuk penggunaan lebih lama. Periksa harganya [itt](https://purchase.aspose.com/buy).
### Apa yang harus saya lakukan jika saya mengalami kesalahan saat memuat berkas Numbers?  
Pastikan Anda menggunakan opsi pemuatan yang benar dan jalur berkas akurat. Untuk dukungan lebih lanjut, kunjungi [Aspose Támogatási Fórum](https://forum.aspose.com/c/cells/9).
### Hogyan szerezhetek ideiglenes licencet az Aspose.Cells-hez?  
Ideiglenes jogosítványt lehet igényelni [itt](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}