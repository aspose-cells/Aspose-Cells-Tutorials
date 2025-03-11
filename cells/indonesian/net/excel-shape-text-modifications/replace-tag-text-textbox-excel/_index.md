---
title: Ganti Tag dengan Teks di TextBox di Excel
linktitle: Ganti Tag dengan Teks di TextBox di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Ganti teks dalam kotak teks di lembar Excel Anda dengan mudah menggunakan Aspose.Cells for .NET. Panduan langkah demi langkah untuk otomatisasi Excel.
weight: 11
url: /id/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ganti Tag dengan Teks di TextBox di Excel

## Perkenalan
Dalam artikel ini, kita akan menyelami tugas tertentu: mengganti tag dengan teks di dalam kotak teks dalam lembar Excel menggunakan Aspose.Cells. Kami akan memandu Anda melalui seluruh proses langkah demi langkah, memastikan Anda memahami setiap detailnya. Di akhir tutorial ini, Anda tidak hanya akan meningkatkan pemahaman Anda tentang Aspose.Cells tetapi juga menyederhanakan tugas-tugas terkait Excel Anda!
## Prasyarat
Sebelum Anda dapat memulai, Anda perlu menyiapkan beberapa hal:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio. Ini adalah IDE fleksibel yang memudahkan pengodean dalam C#.
2.  Pustaka Aspose.Cells: Jika Anda belum melakukannya, unduh pustaka Aspose.Cells untuk .NET dari[halaman](https://releases.aspose.com/cells/net/)Anda juga bisa mendapatkan versi uji coba gratis untuk mencoba fitur-fiturnya.
3. Pengetahuan Dasar C#: Pemahaman dasar tentang pemrograman C# akan sangat membantu Anda mengikuti panduan ini dengan mudah.
Sekarang Anda sudah siap, mari beralih ke bagian yang menyenangkan—menulis kode!
## Paket Impor
Hal pertama yang harus dilakukan—mari impor paket yang diperlukan. Ini penting karena tanpa impor yang tepat, kode Anda tidak akan mengenali kelas dan metode yang akan kita gunakan.
## Mulai Proyek C# Anda
Buka Visual Studio dan buat proyek C# baru, sebaiknya Aplikasi Konsol, karena ini akan memudahkan Anda melihat hasilnya.
## Tambahkan Referensi Aspose.Cells
- Klik kanan pada proyek Anda di Solution Explorer.
- Pilih “Tambah” > “Referensi”.
- Telusuri lokasi tempat Anda mengunduh pustaka Aspose.Cells dan sertakan dalam proyek Anda.
## Impor Namespace yang Diperlukan
 Setelah Anda menambahkan referensi, tambahkan yang berikut ini`using` direktif di bagian atas file utama Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Ini memberi Anda akses ke kelas dalam namespace Aspose.Cells.
Sekarang setelah kita menyiapkan lingkungan kita, mari masuk ke bagian yang menarik—pengodean! Tujuan kita adalah menemukan tag tertentu dalam kotak teks dalam file Excel dan menggantinya dengan teks yang disediakan.
## Langkah 1: Tentukan Direktori Sumber dan Output
Pertama, kita perlu menentukan di mana file Excel sumber kita berada dan di mana kita ingin menyimpan versi yang dimodifikasi.
```csharp
// Direktori Sumber dan Keluaran
string sourceDir = "Your Document Directory"; // Ubah ke Direktori Anda
string outputDir = "Your Document Directory"; // Ubah ke Direktori Anda
```
## Langkah 2: Muat Buku Kerja
Di sinilah kita akan memuat buku kerja Excel kita. Jika file tidak ada, maka akan muncul kesalahan. Jadi, pastikan jalur file Anda benar!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Di sini, kami memuat file Excel yang ada yang disebut`sampleReplaceTagWithText.xlsx`.
## Langkah 3: Tentukan Tag dan Teks Pengganti
Berikutnya, kita perlu menentukan tag yang kita cari dan tag apa yang ingin kita ganti.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 Dalam contoh ini, tag dibagi menggunakan`$`Anda dapat menggantinya dengan pembatas apa pun yang Anda sukai.
## Langkah 4: Ulangi Tag dan Ganti
Kita akan membuat loop untuk menelusuri setiap tag yang ingin kita ganti. Di sinilah keajaiban terjadi!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Langkah 5: Simpan Buku Kerja
Setelah kita melakukan penggantian, sekarang saatnya menyimpan buku kerja yang dimodifikasi ke dalam format yang diinginkan. Berikut cara mengonversinya ke PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Anda juga dapat menyimpannya dalam berbagai format lain, termasuk XLSX.
## Langkah 6: Terapkan Logika Penggantian
 Di sinilah inti fungsionalitas kami berada.`sheetReplace` metode ini akan menangani penggantian sebenarnya dalam lembar kerja Excel.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Pertama, kita mengulang setiap lembar kerja dalam buku kerja.
- Kami mengganti tag utama tidak hanya di konten sel tetapi juga di header dan footer (jika ada).
- Terakhir, kami memeriksa setiap kotak teks pada lembar dan mengganti teks di dalamnya, berdasarkan tag yang kami cari.
## Kesimpulan
Dan voila! Anda sekarang telah mempelajari cara mengganti tag dengan teks dalam kotak teks di seluruh dokumen Excel Anda menggunakan Aspose.Cells for .NET. Ini dapat menghemat waktu, terutama saat menangani tugas berulang dalam spreadsheet.
## Pertanyaan yang Sering Diajukan
### Bisakah saya mengganti tag di beberapa file Excel sekaligus?
Ya, dengan melakukan pengulangan melalui daftar file, Anda dapat menerapkan logika yang sama ke beberapa file Excel.
### Apakah saya memerlukan lisensi berbayar untuk menggunakan Aspose.Cells?
 Anda dapat memulai dengan uji coba gratis, tetapi untuk fungsionalitas penuh, Anda perlu membeli lisensi. Lihat[Opsi pembelian Aspose](https://purchase.aspose.com/buy).
### Bisakah saya mengganti gambar dalam kotak teks menggunakan Aspose.Cells?
Aspose.Cells utamanya menangani teks. Namun, Anda dapat memanipulasi gambar secara terpisah jika diperlukan.
### Dalam format apa saya dapat menyimpan file Excel yang dimodifikasi?
Anda dapat menyimpannya dalam berbagai format termasuk XLSX, PDF, CSV, dll.
### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?
 Anda dapat menemukan dukungan dan mengajukan pertanyaan di[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
