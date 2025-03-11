---
title: Izinkan Pengguna Untuk Mengedit Rentang Di Lembar Kerja Excel
linktitle: Izinkan Pengguna Untuk Mengedit Rentang Di Lembar Kerja Excel
second_title: Referensi API Aspose.Cells untuk .NET
description: Izinkan pengguna untuk mengedit rentang tertentu dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Panduan langkah demi langkah dengan kode sumber dalam C#.
weight: 10
url: /id/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Izinkan Pengguna Untuk Mengedit Rentang Di Lembar Kerja Excel

## Perkenalan

Dalam hal bekerja dengan lembar kerja Excel, fleksibilitas sering kali menjadi kunci—terutama ketika banyak pengguna memerlukan akses untuk mengedit area tertentu tanpa mengorbankan integritas data seluruh lembar. Di sinilah Aspose.Cells for .NET bersinar! Dalam tutorial ini, kita akan membahas cara mengizinkan pengguna mengedit rentang tertentu dalam lembar kerja Excel sambil melindungi bagian dokumen lainnya. Di akhir artikel ini, Anda tidak hanya akan memahami konsepnya tetapi juga memiliki contoh nyata untuk dikerjakan. 

## Prasyarat

Sebelum kita masuk ke inti permasalahan, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai:

1. Lingkungan Pengembangan .NET: Anda harus menyiapkan lingkungan pengembangan .NET yang berfungsi (ini bisa berupa Visual Studio atau IDE lain pilihan Anda).
2.  Pustaka Aspose.Cells untuk .NET: Unduh dan instal pustaka Aspose.Cells. Anda dapat menemukannya[Di Sini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda menavigasi contoh kode dengan mudah.
4. Memahami Dasar-Dasar Excel: Mengetahui cara kerja Excel akan memberikan dasar bagi fungsionalitas yang akan kita bahas.

Setelah prasyarat ini terpenuhi, Anda siap berangkat!

## Paket Impor

Sebelum memulai pengodean, kita perlu memastikan bahwa proyek kita mengenali namespace Aspose.Cells. Berikut cara mengimpor paket yang diperlukan:

```csharp
using System.IO;
using Aspose.Cells;
```

Sekarang setelah kita mengimpor apa yang kita perlukan, mari kita masuk ke tutorial kita langkah demi langkah.

## Langkah 1: Siapkan Direktori Dokumen

Untuk semua operasi berkas, sangat penting untuk memiliki lokasi yang ditentukan di mana dokumen kita akan disimpan. Mari kita atur direktori kerja kita untuk menyimpan berkas Excel.

```csharp
// Jalur ke direktori dokumen.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Pertama, ganti`"YOUR DOCUMENT DIRECTORY"` dengan jalur tempat Anda ingin menyimpan file. Kode ini memeriksa apakah direktori tersebut ada; jika tidak, maka akan dibuatkan direktori.

## Langkah 2: Buat Buku Kerja Baru

Setelah direktori kerja kita siap, waktunya membuat buku kerja Excel. 

```csharp
// Membuat Buku Kerja baru
Workbook book = new Workbook();
```

 Di sini, kita membuat contoh baru dari`Workbook` kelas yang disediakan oleh Aspose.Cells, yang memungkinkan kita memanipulasi file Excel.

## Langkah 3: Akses Lembar Kerja Default

Setiap buku kerja yang baru dibuat dilengkapi dengan setidaknya satu lembar kerja. Mari kita akses lembar kerja tersebut.

```csharp
// Dapatkan lembar kerja pertama (default)
Worksheet sheet = book.Worksheets[0];
```

Dalam potongan kode ini, kita mengakses lembar kerja pertama dari buku kerja kita, yang akan kita manipulasi dalam langkah berikutnya.

## Langkah 4: Dapatkan Izinkan Edit Rentang

 Untuk mengaktifkan rentang tertentu dari lembar kerja untuk pengeditan, kita perlu mengakses`AllowEditRanges` milik.

```csharp
// Dapatkan Izinkan Edit Rentang
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Koleksi ini akan memungkinkan kita untuk mengelola rentang mana yang dapat diedit dalam lembar kerja kita.

## Langkah 5: Tentukan Rentang yang Dilindungi

Berikutnya, mari tentukan bagian lembar kerja mana yang ingin kita lindungi sambil mengizinkan pengeditan pada rentang tertentu.

```csharp
// Definisikan ProtectedRange
ProtectedRange proteced_range;

// Buat rentangnya
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Tentukan kata sandinya
proteced_range.Password = "123";
```

Pada langkah ini, kami menambahkan rentang baru yang dapat diedit yang disebut "r2" yang memungkinkan pengeditan pada sel dari baris 1 kolom 1 hingga baris 3 kolom 3. Selain itu, kami menetapkan kata sandi untuk melindungi rentang ini, memastikan hanya pengguna yang berwenang yang dapat mengubahnya.

## Langkah 6: Lindungi Lembar Kerja

Sekarang setelah kita menyiapkan rentang yang dapat diedit, kita perlu melindungi lembar kerja.

```csharp
// Lindungi lembarannya
sheet.Protect(ProtectionType.All);
```

Kode ini akan melindungi keseluruhan lembar kerja dari perubahan yang tidak diinginkan, kecuali untuk rentang yang baru saja kita tentukan.

## Langkah 7: Simpan File Excel

Mari simpan buku kerja sehingga kita dapat melihat perubahan kita tercermin dalam berkas Excel.

```csharp
// Simpan file Excel
book.Save(dataDir + "protectedrange.out.xls");
```

Pastikan untuk menyesuaikan nama berkas sesuai kebutuhan. Ini akan membuat berkas Excel di direktori yang Anda tentukan dengan pengaturan yang telah kita konfigurasikan.

## Kesimpulan

Nah, itu dia! Anda telah berhasil membuat lembar kerja Excel yang membatasi penyuntingan ke rentang tertentu sekaligus melindungi bagian lembar lainnya. Menggunakan Aspose.Cells untuk .NET membuat pengelolaan tugas semacam ini jauh lebih mudah dan efisien. Baik Anda sedang mengembangkan aplikasi yang rumit atau hanya perlu mengelola data dengan aman, kemampuan ini dapat meningkatkan alur kerja Anda secara signifikan.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang canggih untuk menangani berkas Excel, menawarkan fungsionalitas seperti membuat, mengedit, dan mengonversi lembar kerja secara terprogram.

### Bisakah saya menerapkan beberapa rentang yang dapat diedit?
 Tentu saja! Anda dapat menghubungi`Add` metode pada`allowRanges` koleksi beberapa kali untuk menentukan beberapa rentang yang dapat diedit.

### Apa yang terjadi jika saya lupa kata sandinya?
Sayangnya, jika Anda lupa kata sandi untuk rentang yang dapat diedit, Anda harus menghapus perlindungan atau mengakses file dengan cara yang telah ditentukan sebelumnya yang mungkin melibatkan kredensial.

### Apakah ada versi gratis Aspose.Cells?
Ya, Aspose menyediakan uji coba gratis yang dapat Anda manfaatkan untuk menjelajahi fitur-fiturnya sebelum membeli.

### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells?
 Anda dapat memeriksa[dokumentasi](https://reference.aspose.com/cells/net/)untuk panduan dan referensi terperinci.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
