---
title: Mengubah Teks ke Kolom di Aspose.Cells .NET
linktitle: Mengubah Teks ke Kolom di Aspose.Cells .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengubah teks menjadi kolom dengan mudah menggunakan Aspose.Cells untuk .NET dalam tutorial langkah demi langkah terperinci ini.
weight: 15
url: /id/net/row-column-autofit-conversion/convert-text-to-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengubah Teks ke Kolom di Aspose.Cells .NET

## Perkenalan
Dalam dunia manajemen data yang serba cepat saat ini, efisiensi adalah kuncinya. Baik Anda seorang analis yang mengolah angka atau profesional bisnis yang menyiapkan laporan, Anda sering kali merasa perlu memanipulasi data dengan cepat dan akurat. Jika Anda pernah harus berurusan dengan nama-nama dalam satu sel yang perlu Anda bagi menjadi beberapa kolom, Anda tahu betapa membosankannya hal itu. Untungnya, Aspose.Cells untuk .NET menyediakan solusi elegan untuk membagi teks menjadi beberapa kolom. Dalam panduan ini, kita akan membahas proses mengubah teks menjadi kolom menggunakan Aspose.Cells.
## Prasyarat
Sebelum kita mulai, mari kita pastikan Anda sudah siap. Berikut ini yang Anda perlukan:
1.  Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Jika Anda belum memilikinya, Anda dapat mengunduhnya dari[Situs Microsoft](https://visualstudio.microsoft.com/downloads/).
2. .NET Framework: Pastikan Anda bekerja dalam proyek yang menargetkan versi .NET Framework yang kompatibel. Aspose.Cells kompatibel dengan .NET Core, .NET Framework, dan platform lainnya.
3.  Pustaka Aspose.Cells: Anda perlu mengunduh dan merujuk pustaka Aspose.Cells ke dalam proyek Anda. Anda bisa mendapatkannya dari[Halaman Unduhan Aspose](https://releases.aspose.com/cells/net/).
4. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami tutorial ini dengan mudah.
## Paket Impor
Agar semuanya berjalan lancar, kita perlu mengimpor paket Aspose.Cells yang diperlukan. Berikut cara melakukannya:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Ini memungkinkan Anda mengakses semua fungsionalitas Aspose.Cells yang diperlukan untuk memanipulasi data Anda.
Sekarang setelah semuanya siap, mari kita mulai dengan memecah konversi teks menjadi kolom menjadi beberapa langkah yang mudah diikuti.
## Langkah 1: Siapkan Direktori Dokumen
Pertama, Anda perlu mengonfigurasi direktori tempat Anda akan menyimpan berkas output. Sebaiknya Anda selalu menyusun berkas dengan rapi; hal ini memudahkan pengelolaannya.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
-  Mengganti`"Your Document Directory"`dengan jalur sebenarnya tempat Anda ingin menyimpan berkas Anda. Misalnya, Anda dapat menggunakan`C:\\Documents\\AsposeOutput\\`.
## Langkah 2: Buat Contoh Buku Kerja
Selanjutnya, mari kita buat buku kerja kita. Ini pada dasarnya adalah berkas tempat semua data Anda akan diproses.
```csharp
// Membuat contoh buku kerja.
Workbook wb = new Workbook();
```
- Anggap buku kerja sebagai kanvas kosong. Anda dapat melukis sesuka hati!
## Langkah 3: Akses Lembar Kerja Pertama
Sekarang setelah kita memiliki buku kerja, kita perlu mengakses lembar kerja pertama untuk mulai menambahkan data kita.
```csharp
// Akses lembar kerja pertama.
Worksheet ws = wb.Worksheets[0];
```
- Lembar kerja itu seperti halaman dalam buku kerja Anda. Anda dapat memiliki beberapa halaman, tetapi kami akan fokus pada halaman pertama demi kesederhanaan.
## Langkah 4: Tambahkan Data ke Lembar Kerja
Mari kita isi lembar kerja kita dengan beberapa nama. Kita akan memasukkan daftar nama yang nama depan dan belakangnya dipisahkan oleh spasi.
```csharp
// Tambahkan nama orang di kolom A. Nama depan dan Nama belakang dipisahkan dengan spasi.
ws.Cells["A1"].PutValue("John Teal");
ws.Cells["A2"].PutValue("Peter Graham");
ws.Cells["A3"].PutValue("Brady Cortez");
ws.Cells["A4"].PutValue("Mack Nick");
ws.Cells["A5"].PutValue("Hsu Lee");
```
- Anda mungkin ingin menyesuaikan nama Anda seperlunya; mungkin Anda ingin mengujinya dengan daftar nama Anda sendiri atau membuat set yang lebih beragam.
## Langkah 5: Buat Opsi Pemuatan Teks
Sebelum memisahkan nama, kita harus menentukan bagaimana kita ingin memisahkan teks. Dalam kasus ini, kita akan menggunakan spasi sebagai pemisah.
```csharp
// Buat opsi pemuatan teks dengan spasi sebagai pemisah.
TxtLoadOptions opts = new TxtLoadOptions();
opts.Separator = ' ';
```
- Dengan mendefinisikan spasi sebagai pemisah, kita memberi tahu Aspose bahwa di sinilah nama harus dipisahkan.
## Langkah 6: Membagi Kolom menjadi Beberapa Kolom
 Di sinilah keajaibannya! Sekarang kita akan membagi isi kolom A menjadi dua kolom terpisah (nama depan di kolom A dan nama belakang di kolom B) menggunakan`TextToColumns` metode.
```csharp
// Memisahkan kolom A menjadi dua kolom menggunakan metode TextToColumns()
// Sekarang kolom A akan berisi nama depan dan kolom B akan berisi nama belakang.
ws.Cells.TextToColumns(0, 0, 5, opts);
```
- Langkah ini akan meringankan semua kerja keras Anda. Seperti memiliki pembantu kecil yang tekun dan tahu persis apa yang harus dilakukan!
## Langkah 7: Simpan Buku Kerja
Terakhir, mari simpan buku kerja kita dengan perubahan yang kita buat. Senang rasanya melihat pekerjaan Anda tersimpan dengan rapi!
```csharp
// Simpan buku kerja dalam format xlsx.
wb.Save(dataDir + "outputTextToColumns.xlsx");
```
- Pastikan Anda memberi nama yang bermakna pada file tersebut. Dalam kasus ini, kita menyimpannya sebagai`outputTextToColumns.xlsx`, tetapi Anda bebas mengganti namanya menjadi apa pun yang Anda inginkan.
## Kesimpulan
 Nah, itu dia! Anda baru saja mempelajari cara mengonversi teks ke kolom menggunakan Aspose.Cells untuk .NET. Ini adalah alat hebat yang menyederhanakan penanganan data, memungkinkan Anda melakukan operasi yang dulunya memerlukan waktu berjam-jam hanya dengan beberapa baris kode sederhana. Sekarang, lain kali Anda perlu memisahkan nama atau teks lain, Anda dapat melakukannya dengan mudah. Jangan lupa untuk menjelajahi[Dokumentasi Aspose](https://reference.aspose.com/cells/net/) untuk fitur dan penyesuaian lebih canggih yang dapat meningkatkan keterampilan pemrosesan data Anda!
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET tangguh yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi lembar kerja Excel secara efisien tanpa perlu menginstal Microsoft Excel.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya! Anda dapat memulai dengan uji coba gratis yang tersedia dari[Halaman percobaan Aspose](https://releases.aspose.com/).
### Di mana saya dapat menemukan dukungan untuk Aspose.Cells?
 Untuk pertanyaan atau permasalahan apa pun, Anda dapat mengunjungi[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9).
### Apakah mudah untuk mempelajari Aspose.Cells?
Tentu saja! Dengan contoh-contoh yang mudah dipahami dan dokumentasi yang lengkap, bahkan pemula pun dapat memahaminya dengan cepat.
### Fitur apa lagi yang ditawarkan Aspose.Cells?
Selain manipulasi teks, Aspose.Cells mendukung pembuatan bagan, validasi data, perhitungan rumus, dan banyak lagi!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
