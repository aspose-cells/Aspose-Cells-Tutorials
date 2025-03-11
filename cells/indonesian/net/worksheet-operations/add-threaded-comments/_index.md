---
title: Tambahkan Komentar Berulir di Lembar Kerja
linktitle: Tambahkan Komentar Berulir di Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menambahkan komentar berulir di lembar kerja Excel menggunakan Aspose.Cells for .NET dengan tutorial langkah demi langkah ini. Tingkatkan kolaborasi dengan mudah.
weight: 10
url: /id/net/worksheet-operations/add-threaded-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Komentar Berulir di Lembar Kerja

## Perkenalan
Apakah Anda ingin menyempurnakan lembar kerja Excel Anda dengan komentar berulir? Jika Anda seorang pengembang yang menggunakan Aspose.Cells untuk .NET, Anda beruntung! Komentar berulir memungkinkan diskusi yang lebih terorganisasi dalam lembar Excel Anda, sehingga pengguna dapat berkolaborasi secara efektif. Baik Anda sedang mengerjakan proyek yang memerlukan umpan balik atau hanya ingin memberi anotasi pada data, tutorial ini akan memandu Anda melalui proses penambahan komentar berulir di lembar kerja Excel Anda menggunakan Aspose.Cells. 
## Prasyarat
Sebelum kita memulai, pastikan Anda memiliki prasyarat berikut:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda, karena ini adalah IDE paling umum untuk pengembangan .NET.
2.  Aspose.Cells untuk .NET: Anda perlu menginstal pustaka Aspose.Cells untuk .NET. Jika Anda belum menginstalnya, Anda dapat mengunduhnya dari situs tersebut[Di Sini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# sangat penting, karena tutorial ini akan ditulis dalam C#.
4. .NET Framework: Pastikan proyek Anda disiapkan dengan versi .NET Framework yang kompatibel.
## Paket Impor
Untuk bekerja dengan Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan dalam proyek Anda. Berikut cara melakukannya:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ruang nama ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk memanipulasi berkas Excel dan mengelola komentar berulir.
Sekarang setelah prasyarat kita ditetapkan dan paket-paket yang diperlukan diimpor, mari kita uraikan proses penambahan komentar berulir ke dalam beberapa langkah demi kejelasan.
## Langkah 1: Buat Buku Kerja Baru
Hal pertama yang harus dilakukan, kita perlu membuat buku kerja baru di mana kita akan menambahkan komentar berulir.
```csharp
string outDir = "Your Document Directory"; // Atur direktori keluaran Anda
Workbook workbook = new Workbook(); // Buat buku kerja baru
```
 Pada langkah ini, Anda mengatur direktori keluaran tempat file Excel Anda akan disimpan.`Workbook` kelas adalah titik masuk untuk membuat dan memanipulasi file Excel di Aspose.Cells.
## Langkah 2: Tambahkan Penulis untuk Komentar
Sebelum kita dapat menambahkan komentar, kita perlu menentukan penulis. Penulis ini akan dikaitkan dengan komentar yang Anda buat. Sekarang mari tambahkan penulis.
```csharp
int authorIndex = workbook.Worksheets.ThreadedCommentAuthors.Add("Aspose Test", "", ""); // Tambahkan penulis
ThreadedCommentAuthor author = workbook.Worksheets.ThreadedCommentAuthors[authorIndex]; // Dapatkan penulisnya
```
 Di sini, kami menggunakan`Add` metode untuk membuat penulis baru. Anda dapat menentukan nama penulis dan detail opsional lainnya (seperti email) dalam parameter. Penulis ini akan dirujuk nanti saat menambahkan komentar.
## Langkah 3: Tambahkan Komentar Berulir
Setelah kita mengatur penulisnya, saatnya menambahkan komentar berulir ke sel tertentu di lembar kerja. 
```csharp
workbook.Worksheets[0].Comments.AddThreadedComment("A1", "Test Threaded Comment", author); // Tambahkan komentar berulir
```
 Pada langkah ini, kami menambahkan komentar ke sel A1 pada lembar kerja pertama. Anda dapat mengganti`"A1"` dengan referensi sel mana pun tempat Anda ingin menambahkan komentar. Pesan dalam tanda kutip adalah isi komentar.
## Langkah 4: Simpan Buku Kerja
Setelah menambahkan komentar berulir, Anda sebaiknya menyimpan buku kerja Anda sehingga perubahannya tetap ada.
```csharp
workbook.Save(outDir + "AddThreadedComments_out.xlsx"); // Simpan buku kerja
```
 Di sini, buku kerja disimpan di direktori keluaran yang ditentukan dengan nama`AddThreadedComments_out.xlsx`Pastikan direktori tersebut ada, atau Anda akan mengalami kesalahan file tidak ditemukan.
## Langkah 5: Konfirmasikan Keberhasilan
Terakhir, mari kita keluarkan pesan ke konsol yang menunjukkan bahwa operasi kita berhasil.
```csharp
Console.WriteLine("AddThreadedComments executed successfully."); // Pesan konfirmasi
```
Langkah ini bersifat opsional tetapi berguna untuk debugging. Langkah ini memberi tahu Anda bahwa kode tersebut dijalankan tanpa kesalahan.
## Kesimpulan
Nah, itu dia! Anda telah berhasil menambahkan komentar berulir ke lembar kerja Excel Anda menggunakan Aspose.Cells for .NET. Fitur ini dapat meningkatkan kolaborasi secara signifikan dan memberikan kejelasan dalam komunikasi saat beberapa pengguna mengerjakan dokumen yang sama.
Komentar berulir tidak hanya memungkinkan diskusi yang lebih kaya dalam dokumen, tetapi juga menjaga anotasi Anda tetap teratur. Jangan ragu untuk bereksperimen dengan sel, penulis, dan komentar yang berbeda untuk melihat bagaimana semuanya muncul di buku kerja Anda.
## Pertanyaan yang Sering Diajukan
### Apa itu komentar berulir di Excel?  
Komentar berulir adalah komentar yang memungkinkan adanya balasan dan diskusi dalam komentar itu sendiri, sehingga memudahkan kolaborasi.
### Bisakah saya menambahkan beberapa komentar ke satu sel?  
Ya, Anda dapat menambahkan beberapa komentar berulir ke satu sel, yang memungkinkan diskusi yang luas.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?  
 Meskipun Anda dapat mencoba Aspose.Cells dengan uji coba gratis, lisensi diperlukan untuk penggunaan produksi. Anda bisa mendapatkannya[Di Sini](https://purchase.aspose.com/buy).
### Bagaimana cara melihat komentar di Excel?  
Setelah menambahkan komentar, Anda dapat melihatnya dengan mengarahkan kursor ke sel tempat komentar ditempatkan atau melalui panel komentar.
### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells?  
 Anda dapat merujuk ke[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk informasi lebih lanjut dan contoh terperinci.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
