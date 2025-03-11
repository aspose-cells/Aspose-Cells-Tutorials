---
title: Membuat Efek Coretan pada Teks di Excel
linktitle: Membuat Efek Coretan pada Teks di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menerapkan efek coretan pada teks di Excel dengan Aspose.Cells untuk .NET dalam tutorial langkah demi langkah terperinci ini.
weight: 15
url: /id/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Efek Coretan pada Teks di Excel

## Perkenalan
Dalam Excel, elemen visual sama pentingnya dengan data itu sendiri. Baik Anda menyorot perubahan penting atau menandai item yang tidak lagi relevan, efek coretan pada teks adalah cara klasik untuk mengelola representasi visual dalam spreadsheet. Dalam panduan ini, kami akan memandu Anda melalui proses penerapan efek coretan pada teks di Excel menggunakan Aspose.Cells for .NET. Tutorial ini tidak hanya akan membahas prasyarat yang diperlukan tetapi juga akan memberikan pendekatan langkah demi langkah untuk memastikan Anda dapat meniru efek ini dengan mudah.
## Prasyarat
Sebelum memulai tutorial, pastikan Anda telah memenuhi prasyarat berikut:
1. Lingkungan Pengembangan: Anda harus menyiapkan lingkungan pengembangan .NET. Ini bisa berupa Visual Studio atau IDE lain yang Anda sukai yang mendukung pengembangan .NET.
2. Aspose.Cells untuk .NET: Pastikan Anda telah menginstal Aspose.Cells di proyek Anda. Anda dapat mengunduhnya dari tautan berikut:[Unduh Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Pemahaman mendasar tentang pemrograman C# sangat membantu karena contoh-contohnya akan dikodekan dalam C#.
4. .NET Framework: Pastikan proyek Anda menargetkan versi .NET Framework yang kompatibel, biasanya .NET Core atau .NET Framework 4.5 dan yang lebih baru.
## Paket Impor
Sebelum Anda menulis kode apa pun, Anda perlu mengimpor namespace yang diperlukan dari Aspose.Cells. Hal ini penting untuk mengakses berbagai fitur yang disediakan oleh pustaka. Berikut ini cara mengimpor namespace yang diperlukan:
```csharp
using System.IO;
using Aspose.Cells;
```
Dengan impor ini, Anda akan memiliki akses ke kelas Buku Kerja, Lembar Kerja, dan Gaya yang akan digunakan di seluruh tutorial ini.
Setelah kita menyiapkan langkah-langkahnya, mari kita bagi prosesnya menjadi beberapa langkah yang mudah dikelola. Setiap langkah akan disertai dengan petunjuk yang jelas untuk memandu Anda dalam membuat efek coretan pada teks di Excel.
## Langkah 1: Tentukan Direktori Dokumen
Mulailah dengan menentukan jalur penyimpanan dokumen Excel Anda. Ini akan menjadi lokasi penyimpanan berkas output Anda.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur direktori aktual tempat Anda ingin menyimpan berkas Excel. Ini akan menyiapkan direktori untuk keluaran Anda.
## Langkah 2: Buat Direktori
Selanjutnya, Anda perlu memastikan bahwa direktori yang Anda tentukan pada langkah sebelumnya ada. Jika tidak ada, Anda dapat membuatnya secara terprogram.
```csharp
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Kode ini memeriksa apakah direktori tersebut ada dan membuatnya jika tidak ada. Ini membantu menghindari kesalahan saat Anda mencoba menyimpan berkas Anda nanti.
## Langkah 3: Membuat Instansi Objek Buku Kerja
Sekarang, saatnya membuat objek Workbook baru. Ini adalah dasar dari file Excel Anda, tempat Anda akan menambahkan data dan menerapkan format.
```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
```
 Itu`Workbook` class merupakan file Excel. Dengan membuat instance dari class ini, pada dasarnya Anda membuat dokumen Excel baru.
## Langkah 4: Tambahkan Lembar Kerja Baru
Setiap buku kerja dapat berisi beberapa lembar kerja. Mari kita lanjutkan dan buat lembar kerja baru di buku kerja Anda.
```csharp
// Menambahkan lembar kerja baru ke objek Excel
int i = workbook.Worksheets.Add();
```
 Itu`Add` metode dari`Worksheets` koleksi menambahkan lembar kerja baru ke buku kerja dan mengembalikan indeksnya. 
## Langkah 5: Dapatkan Referensi Lembar Kerja Baru
Setelah Anda membuat lembar kerja, Anda perlu merujuknya untuk operasi mendatang.
```csharp
// Mendapatkan referensi lembar kerja yang baru ditambahkan dengan meneruskan indeks lembar kerjanya
Worksheet worksheet = workbook.Worksheets[i];
```
Di sini, Anda mengambil lembar kerja yang baru dibuat menggunakan indeksnya (`i`). Ini memberi Anda akses untuk memanipulasi lembar kerja.
## Langkah 6: Akses Sel
 Anda ingin mengakses sel tertentu di lembar kerja Anda tempat Anda akan menerapkan format coretan. Dalam contoh ini, kami menggunakan sel`A1`.
```csharp
// Mengakses sel "A1" dari lembar kerja
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 Di Excel, sel dirujuk dengan pengidentifikasi kolom dan barisnya (misalnya, "A1"). Kita memperoleh referensi ke sel`A1` untuk manipulasi lebih lanjut.
## Langkah 7: Tambahkan Nilai ke Sel
 Selanjutnya, mari masukkan beberapa teks ke dalam sel. Kita akan menulis “Hello Aspose!” di sel`A1`.
```csharp
// Menambahkan beberapa nilai ke sel "A1"
cell.PutValue("Hello Aspose!");
```
 Itu`PutValue` Metode ini digunakan untuk menetapkan nilai string ke sel. Anda dapat mengubah string ini menjadi apa pun yang ingin Anda tampilkan.
## Langkah 8: Dapatkan Gaya Sel
Sekarang setelah kita memiliki teks di sel kita, saatnya mengakses gaya sel untuk menerapkan pemformatan yang kita inginkan, termasuk efek coretan.
```csharp
// Mendapatkan gaya sel
Style style = cell.GetStyle();
```
 Itu`GetStyle` metode mengambil gaya sel saat ini, yang memungkinkan Anda mengubah properti seperti jenis font, ukuran, dan efek.
## Langkah 9: Mengatur Efek Coretan
Mari terapkan efek strikeout pada teks di dalam sel. Kita akan mengubah gaya font sel.
```csharp
// Mulai:AturCoretan
// Mengatur efek coretan pada font
style.Font.IsStrikeout = true;
// ExEnd:TetapkanCoret
```
 Dengan pengaturan`IsStrikeout` menjadi benar, Anda memerintahkan Excel untuk mencoret teks secara visual pada sel yang dipilih - seperti menandai sesuatu secara visual dari daftar.
## Langkah 10: Terapkan Gaya ke Sel
Setelah mengubah gaya, Anda perlu menerapkannya kembali ke sel untuk mencerminkan perubahan.
```csharp
// Menerapkan gaya ke sel
cell.SetStyle(style);
```
 Itu`SetStyle` metode memperbarui sel dengan gaya baru, yang sekarang menyertakan format coretan.
## Langkah 11: Simpan File Excel
 Akhirnya, saatnya untuk menyimpan buku kerja Anda ke direktori yang ditentukan. Dalam contoh ini, kami menyimpan file dengan nama`book1.out.xls`.
```csharp
// Menyimpan file Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Itu`Save`metode ini menulis buku kerja ke disk dalam format Excel 97-2003. Anda dapat menentukan format yang berbeda jika diperlukan.
## Kesimpulan
Membuat efek coretan pada teks di Excel menggunakan Aspose.Cells for .NET merupakan proses yang mudah jika Anda menguraikannya langkah demi langkah. Dengan mengikuti panduan ini, Anda kini memiliki keterampilan untuk menyempurnakan lembar kerja Anda dengan isyarat visual, menjadikan data Anda tidak hanya informatif tetapi juga menarik secara visual.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka yang hebat untuk mengelola file Excel dalam aplikasi .NET, yang memungkinkan Anda membuat, memanipulasi, dan mengonversi dokumen Excel secara terprogram.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Anda dapat menggunakannya secara gratis selama masa uji coba. Uji coba gratis tersedia di[Uji Coba Gratis Aspose.Cells](https://releases.aspose.com/).
### Bagaimana cara membeli Aspose.Cells?
 Anda dapat membeli lisensi untuk Aspose.Cells melalui situs web mereka[Beli Aspose.Cells](https://purchase.aspose.com/buy).
### Apakah ada contoh yang tersedia untuk penggunaan Aspose.Cells?
 Ya, Anda dapat menemukan banyak contoh dan potongan kode di[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/).
### Di mana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Anda bisa mendapatkan dukungan dan bantuan komunitas dari[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
