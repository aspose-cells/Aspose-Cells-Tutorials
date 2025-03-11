---
title: Edit Rentang Dalam Lembar Kerja Excel
linktitle: Edit Rentang Dalam Lembar Kerja Excel
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara mengedit rentang dalam lembar kerja Excel menggunakan Aspose.Cells untuk .NET dengan panduan komprehensif ini yang menampilkan petunjuk langkah demi langkah.
weight: 20
url: /id/net/protect-excel-file/edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Edit Rentang Dalam Lembar Kerja Excel

## Perkenalan

Dalam hal mengedit lembar kerja Excel, salah satu fitur paling canggih yang berguna adalah kemampuan untuk melindungi area tertentu sekaligus mengizinkan pengeditan di area lain. Ini bisa sangat berguna dalam lingkungan kolaboratif di mana banyak pengguna memerlukan akses tetapi hanya boleh mengubah sel yang ditentukan. Hari ini, kita akan membahas cara memanfaatkan Aspose.Cells for .NET untuk mengelola rentang yang dapat diedit dalam lembar kerja Excel. Jadi, ambil minuman pengodean favorit Anda dan mari kita mulai!

## Prasyarat

Sebelum kita mulai membuat kode, pastikan Anda sudah menyiapkan semuanya. Berikut ini yang Anda perlukan:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio. Edisi komunitas berfungsi dengan baik.
2.  Pustaka Aspose.Cells: Anda memerlukan pustaka Aspose.Cells untuk .NET. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Pemahaman mendasar tentang C# akan sangat membantu.
4. Pengaturan Proyek: Buat aplikasi konsol C# baru di Visual Studio.

Sempurna—Anda sudah siap! Sekarang, mari selami inti kode.

## Paket Impor

Setelah Anda menyiapkan proyek, langkah awal melibatkan pengimporan namespace Aspose.Cells yang diperlukan. Untuk melakukannya, cukup sertakan baris berikut di bagian atas berkas kode Anda:

```csharp
using Aspose.Cells;
```

Ini akan memungkinkan Anda untuk mengakses semua fungsi yang disediakan oleh Aspose.Cells dalam proyek Anda.

## Langkah 1: Siapkan Direktori

Sebelum Anda mulai bekerja dengan file Excel, ada baiknya Anda membuat direktori tempat file Anda akan berada. Langkah ini memastikan bahwa aplikasi Anda mengetahui tempat untuk membaca dan menulis data.

Mari kita buat kode untuk membuat direktori (jika belum ada):

```csharp
// Jalur ke direktori dokumen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Mengganti`"YOUR DOCUMENT DIRECTORY"` dengan jalur tempat Anda ingin menyimpan file Anda. Ini bisa berupa sesuatu seperti`@"C:\ExcelFiles\"`.

## Langkah 2: Buat Buku Kerja Baru

Sekarang direktori Anda sudah siap, mari buat buku kerja Excel baru. Ini sama seperti membuka kanvas kosong sebelum mulai melukis.

```csharp
// Membuat Buku Kerja baru
Workbook book = new Workbook();
```

Dengan ini, buku kerja kosong Anda sudah siap digunakan!

## Langkah 3: Dapatkan Lembar Kerja Pertama

Setiap buku kerja berisi setidaknya satu lembar kerja secara default. Anda perlu mengambil lembar kerja tersebut untuk melakukan operasi pada lembar kerja tersebut.

```csharp
// Dapatkan lembar kerja pertama (default)
Worksheet sheet = book.Worksheets[0];
```

Di sini, kita mengakses lembar kerja pertama, yang mirip dengan membuka selembar kertas baru di buku catatan Anda.

## Langkah 4: Dapatkan Izinkan Edit Rentang

Sebelum kita dapat mengatur rentang yang dapat diedit, kita perlu mengambil kumpulan rentang yang dilindungi dari lembar kerja kita.

```csharp
// Dapatkan Izinkan Edit Rentang
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Baris ini mengambil koleksi tempat Anda akan mengelola rentang yang dilindungi. Ada baiknya mengetahui apa yang tersedia di balik layar!

## Langkah 5: Tentukan dan Buat Rentang Terlindungi

Pada titik ini, kita siap menentukan rentang yang ingin Anda izinkan untuk melakukan pengeditan. Mari buat rentang ini.

```csharp
// Definisikan ProtectedRange
ProtectedRange proteced_range;

// Buat rentangnya
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];
```

Dalam kode di atas, kita membuat rentang terproteksi bernama "r2" yang memungkinkan pengeditan di sel dari baris 1, kolom 1 hingga baris 3, kolom 3 (yang dalam istilah Excel diterjemahkan menjadi blok A1 hingga C3). Anda dapat menyesuaikan indeks ini sesuai kebutuhan.

## Langkah 6: Tetapkan Kata Sandi 

Menetapkan kata sandi untuk rentang yang dilindungi memastikan bahwa hanya mereka yang memiliki kata sandi yang dapat mengubah area yang ditentukan. Langkah ini meningkatkan keamanan spreadsheet Anda.

```csharp
// Tentukan kata sandinya
proteced_range.Password = "YOUR_PASSWORD";
```

 Mengganti`"YOUR_PASSWORD"` dengan kata sandi pilihan Anda. Ingat saja, jangan membuatnya terlalu sederhana—anggap saja seperti mengunci peti harta karun Anda!

## Langkah 7: Lindungi Lembaran

Sekarang setelah rentang yang dapat diedit telah ditentukan dan diamankan dengan kata sandi, saatnya untuk melindungi seluruh lembar kerja.

```csharp
// Lindungi lembarannya
sheet.Protect(ProtectionType.All);
```

Dengan menerapkan metode ini, pada dasarnya Anda mengunci seluruh lembar kerja. Hanya rentang yang ditetapkan untuk pengeditan yang dapat diubah.

## Langkah 8: Simpan File Excel

Kita akhirnya mencapai langkah terakhir dalam tutorial kita—menyimpan buku kerja ke direktori yang Anda tentukan!

```csharp
// Simpan file Excel
book.Save(dataDir + "protectedrange.out.xls");
```

Ini akan menyimpan buku kerja Anda yang dilindungi sebagai`protectedrange.out.xls` di direktori yang Anda tentukan.

## Kesimpulan

Nah, itu dia! Anda telah berhasil membuat lembar kerja Excel menggunakan Aspose.Cells for .NET, menentukan rentang yang dapat diedit, menetapkan kata sandi, dan melindungi lembar kerja—semuanya dalam beberapa langkah mudah. Sekarang Anda dapat berbagi buku kerja dengan rekan kerja, meningkatkan kolaborasi sekaligus menjaga keamanan data penting.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?  
Aspose.Cells adalah pustaka .NET canggih yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel secara terprogram.

### Bisakah saya melindungi sel tertentu dalam lembar kerja Excel?  
Ya, dengan menggunakan Aspose.Cells, Anda dapat menentukan rentang tertentu yang dapat diedit dan melindungi sisa lembar kerja.

### Apakah ada versi uji coba yang tersedia untuk Aspose.Cells?  
 Tentu saja! Anda dapat mengunduh uji coba gratis[Di Sini](https://releases.aspose.com/).

### Bisakah saya menggunakan Aspose.Cells dengan bahasa pemrograman lain?  
Meskipun tutorial ini berfokus pada .NET, Aspose.Cells tersedia untuk beberapa bahasa pemrograman, termasuk Java dan Cloud API.

### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells?  
 Anda dapat menjelajahi dokumentasi lengkapnya[Di Sini](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
