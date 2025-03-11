---
title: Melindungi Sel dan Rentang di Lembar Kerja menggunakan Aspose.Cells
linktitle: Melindungi Sel dan Rentang di Lembar Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara melindungi sel dan rentang dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Ikuti panduan langkah demi langkah ini untuk mengamankan lembar kerja Anda.
weight: 11
url: /id/net/worksheet-security/protect-cells-and-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Melindungi Sel dan Rentang di Lembar Kerja menggunakan Aspose.Cells

## Perkenalan
Bekerja dengan spreadsheet sering kali melibatkan perlindungan bagian-bagian tertentu dari lembar kerja dari modifikasi yang tidak diinginkan, terutama dalam lingkungan kolaboratif. Dalam tutorial ini, kita akan menjelajahi cara melindungi sel dan rentang tertentu dalam lembar kerja menggunakan Aspose.Cells untuk .NET. Kami akan memandu Anda melalui proses menyiapkan lembar kerja yang dilindungi, menentukan rentang mana yang dapat diedit, dan menyimpan file. Ini dapat menjadi fitur yang sangat berguna ketika Anda ingin membatasi akses ke data sensitif sambil mengizinkan bagian-bagian tertentu untuk dimodifikasi oleh orang lain.
## Prasyarat
Sebelum memulai tutorial, pastikan Anda memiliki prasyarat berikut:
1. Aspose.Cells untuk .NET: Anda perlu menginstal pustaka Aspose.Cells di proyek Anda. Jika belum, Anda dapat mengunduhnya dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: Panduan ini mengasumsikan Anda menggunakan Visual Studio atau IDE serupa yang mendukung pengembangan C#.
3. Pengetahuan dasar C#: Anda harus memahami dasar-dasar pemrograman C# dan cara menyiapkan proyek di Visual Studio.
4.  Lisensi Aspose.Cells: Meskipun Aspose menawarkan uji coba gratis, lisensi yang valid akan memungkinkan Anda untuk menggunakan set fitur lengkap dari pustaka tersebut. Jika Anda tidak memilikinya, Anda dapat memperoleh lisensi[lisensi sementara di sini](https://purchase.aspose.com/temporary-license/).
Setelah Anda memastikan semua hal di atas telah siap, kita dapat beralih ke bagian pengkodean.
## Paket Impor
Agar dapat bekerja dengan Aspose.Cells, Anda harus mengimpor namespace yang diperlukan ke dalam file C# terlebih dahulu. Berikut cara mengimpornya:
```csharp
using System.IO;
using Aspose.Cells;
```
 Itu`Aspose.Cells` namespace memberi Anda akses ke fungsi inti untuk memanipulasi file Excel, dan`System.IO` digunakan untuk operasi file seperti menyimpan buku kerja.
Sekarang, mari kita uraikan langkah-langkah untuk melindungi sel dan rentang dalam lembar kerja menggunakan Aspose.Cells.
## Langkah 1: Siapkan Lingkungan Anda
Pertama, buat direktori tempat Anda ingin menyimpan file Excel. Jika direktori tersebut belum ada, kami akan membuatnya. Ini membantu memastikan bahwa Anda memiliki tempat untuk menyimpan file output.
```csharp
// Tentukan jalur ke direktori dokumen Anda
string dataDir = "Your Document Directory";
// Periksa apakah direktori tersebut ada, jika tidak, buatlah
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
 Di sini, kami menggunakan`System.IO.Directory.Exists()` untuk memeriksa apakah folder tersebut ada, dan jika tidak, kita membuatnya menggunakan`Directory.CreateDirectory()`.
## Langkah 2: Buat Buku Kerja Baru
Sekarang, mari kita buat objek Workbook baru. Ini akan berfungsi sebagai file Excel tempat kita akan mendefinisikan sel dan rentang.
```csharp
// Membuat instance objek Buku Kerja baru
Workbook book = new Workbook();
```
 Itu`Workbook` class adalah titik masuk untuk bekerja dengan file Excel di Aspose.Cells. Class mewakili dokumen Excel.
## Langkah 3: Akses Lembar Kerja Default
Setiap buku kerja yang baru dibuat memiliki lembar kerja default. Kita akan mengambilnya untuk bekerja dengan isinya.
```csharp
// Dapatkan lembar kerja pertama (default) di buku kerja
Worksheet sheet = book.Worksheets[0];
```
 Di Sini,`Worksheets[0]` memberi kita lembar pertama dalam buku kerja (pengindeksan dimulai dari 0).
## Langkah 4: Tentukan Rentang yang Dapat Diedit
Untuk melindungi bagian tertentu dari lembar kerja sekaligus mengizinkan pengguna untuk mengedit sel tertentu, kita perlu menentukan rentang yang dapat diedit. Kita akan membuat rentang yang dapat diedit dan menambahkannya ke koleksi AllowEditRanges pada lembar kerja.
```csharp
// Dapatkan koleksi AllowEditRanges
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// Tentukan ProtectedRange dan tambahkan ke koleksi
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
Dalam kode di atas:
- `"r2"` adalah nama rentang yang dapat diedit.
-  Angka-angka`1, 1, 3, 3` mewakili indeks baris dan kolom awal dan akhir untuk rentang (yaitu, dari sel B2 hingga D4).
## Langkah 5: Tetapkan Kata Sandi untuk Rentang yang Dilindungi
Setelah kita menentukan rentang yang dapat diedit, mari tambahkan kata sandi untuk melindunginya. Ini berarti pengguna akan memerlukan kata sandi untuk mengedit rentang khusus ini.
```csharp
// Tentukan kata sandi untuk rentang yang dapat diedit
protectedRange.Password = "123";
```
 Di sini, kami telah menetapkan kata sandi sebagai`"123"`, tetapi Anda dapat memilih kata sandi aman apa pun. Langkah ini penting untuk mengendalikan akses ke area yang dapat diedit.
## Langkah 6: Lindungi Seluruh Lembar
Pada tahap ini, kita akan melindungi seluruh lembar kerja. Melindungi lembar kerja memastikan bahwa bagian lain dari lembar kerja, kecuali rentang yang diizinkan, tidak dapat diedit.
```csharp
// Lindungi lembaran dengan jenis perlindungan yang ditentukan (Semua)
sheet.Protect(ProtectionType.All);
```
Ini memastikan semua sel pada lembar terkunci, kecuali sel yang berada dalam rentang yang dapat diedit.
## Langkah 7: Simpan Buku Kerja
Terakhir, kita simpan buku kerja ke dalam sebuah file. Lembar yang diproteksi akan disimpan dengan nama yang Anda tentukan.
```csharp
// Simpan file Excel ke direktori yang ditentukan
book.Save(dataDir + "protectedrange.out.xls");
```
 Di sini, file Excel akan disimpan sebagai`protectedrange.out.xls` di direktori yang telah kita tentukan sebelumnya. Jika Anda ingin menyimpannya dengan nama atau format yang berbeda, Anda dapat mengubah nama dan ekstensi file.
## Kesimpulan
Dengan mengikuti tutorial ini, Anda telah mempelajari cara melindungi sel dan rentang dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Pendekatan ini memberi Anda fleksibilitas dalam mengendalikan area mana dalam lembar kerja Anda yang dapat diedit dan mana yang tidak. Kini Anda dapat menerapkan keterampilan ini dalam proyek Anda sendiri, memastikan data sensitif Anda tetap aman sekaligus menyediakan area yang dapat diedit bagi pengguna.
Ingat, Aspose.Cells menawarkan serangkaian alat tangguh untuk bekerja dengan file Excel, dan ini hanyalah salah satu dari banyak hal yang dapat Anda lakukan dengannya. 
## Pertanyaan yang Sering Diajukan
### Bisakah saya hanya melindungi sel tertentu dalam lembar kerja?
 Ya, dengan menggunakan`AllowEditRanges` properti, Anda dapat menentukan sel atau rentang mana yang dapat diedit sementara sisa lembar kerja tetap dilindungi.
### Bisakah saya menghapus perlindungannya nanti?
 Ya, Anda dapat membuka proteksi lembar kerja dengan menggunakan`Unprotect()` metode, dan jika kata sandi telah ditetapkan, Anda harus memberikannya.
### Bagaimana cara melindungi seluruh lembar dengan kata sandi?
 Untuk melindungi seluruh lembaran, Anda cukup menggunakan`Protect()` metode dengan atau tanpa kata sandi. Misalnya,`sheet.Protect("password")`.
### Bisakah saya menambahkan beberapa rentang yang dapat diedit?
 Tentu saja! Anda dapat menambahkan rentang yang dapat diedit sebanyak yang Anda perlukan dengan memanggil`allowRanges.Add()` beberapa kali.
### Fitur keamanan apa lagi yang ditawarkan Aspose.Cells?
Aspose.Cells mendukung berbagai fitur keamanan seperti enkripsi buku kerja, pengaturan kata sandi file, dan melindungi sel dan lembar.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
