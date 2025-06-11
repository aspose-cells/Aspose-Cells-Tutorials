---
"description": "Temukan cara menerapkan validasi data desimal di Excel menggunakan Aspose.Cells for .NET dengan panduan kami yang mudah diikuti. Tingkatkan integritas data dengan mudah."
"linktitle": "Validasi Data Desimal di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Validasi Data Desimal di Excel"
"url": "/id/net/excel-autofilter-validation/decimal-data-validation-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Validasi Data Desimal di Excel

## Bevezetés

Membuat lembar kerja dengan data yang akurat sangat penting untuk komunikasi yang jelas dalam bisnis apa pun. Salah satu cara untuk memastikan keakuratan data adalah melalui penggunaan validasi data di Excel. Dalam tutorial ini, kita akan memanfaatkan kekuatan Aspose.Cells untuk .NET untuk membuat mekanisme validasi data desimal yang menjaga data Anda tetap andal dan bersih. Jika Anda ingin meningkatkan kemampuan Excel Anda, Anda berada di tempat yang tepat!

## Előfeltételek

Sebelum menyelami kode, pastikan Anda telah menyiapkan semuanya agar pengalaman Anda berjalan lancar:

1. Visual Studio: Unduh dan instal Visual Studio jika Anda belum melakukannya. Ini adalah lingkungan yang sempurna untuk mengembangkan aplikasi .NET.
2. Aspose.Cells untuk .NET: Anda perlu menambahkan pustaka Aspose.Cells ke proyek Anda. Anda dapat mengunduhnya melalui [ezt a linket](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Meskipun kami akan menjelaskan semuanya langkah demi langkah, memiliki pemahaman mendasar tentang pemrograman C# akan memberi Anda pemahaman yang lebih baik tentang konsep tersebut.
4. .NET Framework: Pastikan Anda telah menginstal .NET Framework yang diperlukan yang kompatibel dengan Aspose.Cells.
5. Pustaka: Rujuk pustaka Aspose.Cells dalam proyek Anda untuk menghindari kesalahan kompilasi.

Sekarang setelah kita membahas dasar-dasarnya, mari masuk ke bagian yang menarik: pengkodean.

## Csomagok importálása

Untuk memulai, Anda perlu mengimpor paket yang diperlukan ke dalam berkas C# Anda. Ini memungkinkan Anda untuk mengakses fungsi Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Dengan menyertakan baris ini di bagian atas berkas Anda, Anda memberi tahu C# untuk mencari fungsionalitas Aspose.Cells yang memungkinkan Anda memanipulasi berkas Excel.

Sekarang setelah kita menyiapkan bahannya, mari kita bahas langkah-langkah yang diperlukan untuk membuat validasi data desimal dalam lembar kerja Excel.

## 1. lépés: Dokumentumkönyvtár beállítása

Sebelum Anda dapat menyimpan file apa pun, Anda perlu memastikan bahwa direktori dokumen Anda telah disiapkan dengan benar:

```csharp
string dataDir = "Your Document Directory";
```

Csere `"Your Document Directory"` dengan jalur tempat Anda ingin menyimpan file Excel Anda.

## Langkah 2: Periksa Keberadaan Direktori

Potongan kode ini memeriksa apakah direktori tersebut ada dan membuat direktori tersebut jika tidak ada:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Langkah ini seperti memastikan ruang kerja Anda siap sebelum memulai proyek baru. Tidak berantakan, tidak stres!

## Langkah 3: Buat Objek Buku Kerja

Berikutnya, mari buat objek buku kerja baru, yang pada dasarnya adalah file Excel:

```csharp
Workbook workbook = new Workbook();
```

Bayangkan buku kerja sebagai kanvas kosong untuk data Anda. Pada titik ini, tidak ada konten yang tersedia tetapi siap untuk diwarnai.

## Langkah 4: Membuat dan Mengakses Lembar Kerja


Sekarang, mari buat lembar kerja dan akses lembar pertama di buku kerja:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Sama seperti buku yang memiliki beberapa halaman, buku kerja dapat memiliki beberapa lembar kerja. Saat ini kami fokus pada yang pertama.

## Langkah 5: Dapatkan Koleksi Validasi

Sekarang, mari tarik koleksi validasi dari lembar kerja karena di sinilah kita akan mengelola aturan validasi data kita:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Langkah ini sama halnya dengan memeriksa kotak peralatan sebelum Anda memulai suatu proyek.

## Langkah 6: Tentukan Area Sel untuk Validasi

Kita perlu menentukan area di mana validasi berlaku:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Di sini, kami menetapkan bahwa validasi data akan diterapkan pada satu sel—khususnya, sel pertama di lembar kerja (A1).

## Langkah 7: Buat dan Tambahkan Validasi

Mari buat objek validasi kita dan tambahkan ke koleksi validasi:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Sekarang kita memiliki objek validasi yang akan kita konfigurasikan untuk menegakkan kondisi desimal kita.

## Langkah 8: Tetapkan Jenis Validasi

Berikutnya, kami akan menentukan jenis validasi yang kami inginkan:

```csharp
validation.Type = ValidationType.Decimal;
```

Dengan menetapkan jenis ke Desimal, kita menginstruksikan Excel untuk mengharapkan nilai desimal dalam sel yang divalidasi.

## Langkah 9: Tentukan Operator

Sekarang, kita akan menentukan kondisi untuk nilai yang diizinkan. Kita ingin memastikan data yang dimasukkan berada di antara dua rentang:

```csharp
validation.Operator = OperatorType.Between;
```

Anggap saja seperti menggambar garis batas. Angka apa pun di luar rentang ini akan ditolak, sehingga data Anda tetap bersih!

## Langkah 10: Tetapkan Batasan untuk Validasi

Berikutnya, kami akan menetapkan batas bawah dan atas untuk validasi kami:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Dengan batasan ini, setiap angka desimal, tidak peduli seberapa besar atau kecil, diterima, asalkan valid!

## Langkah 11: Menyesuaikan Pesan Kesalahan

Mari pastikan bahwa pengguna mengetahui mengapa masukan mereka ditolak dengan menambahkan pesan kesalahan:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Hal ini memberikan pengalaman yang mudah digunakan, karena menyediakan panduan tentang apa yang harus dimasukkan.

## Langkah 12: Tentukan Area Validasi

Sekarang, mari tentukan sel yang akan menerima validasi ini:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

Dalam konfigurasi ini, kami mengatakan bahwa validasi berlaku dari sel A1 hingga A10.

## Langkah 13: Tambahkan Area Validasi

Sekarang setelah kita mendefinisikan area validasi kita, mari terapkan:

```csharp
validation.AddArea(area);
```

Validasi Anda kini sudah pada tempatnya, siap untuk menangkap masukan apa pun yang tidak pantas!

## Langkah 14: Simpan Buku Kerja

Terakhir, mari simpan buku kerja dengan validasi data desimal yang sudah ada:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Nah, itu dia! Anda telah berhasil membuat buku kerja dengan validasi data desimal menggunakan Aspose.Cells for .NET.

## Következtetés

Menerapkan validasi data desimal di Excel menggunakan Aspose.Cells for .NET mudah dilakukan jika Anda mengikuti langkah-langkah mudah berikut. Anda tidak hanya memastikan bahwa data tetap bersih dan terstruktur, tetapi juga meningkatkan integritas data secara keseluruhan di lembar kerja Anda, sehingga lembar kerja tersebut andal dan mudah digunakan.
Baik Anda berkecimpung di bidang keuangan, manajemen proyek, atau bidang apa pun yang memanfaatkan pelaporan data, menguasai keterampilan ini akan meningkatkan produktivitas Anda secara signifikan. Jadi, cobalah! Lembar kerja Anda akan berterima kasih karenanya.

## GYIK

### Apa itu validasi data di Excel?
Validasi data di Excel adalah fitur yang membatasi jenis data yang dapat dimasukkan dalam sel atau rentang tertentu, guna memastikan integritas data.

### Dapatkah saya menyesuaikan pesan kesalahan dalam validasi data?
Ya! Anda dapat memberikan pesan kesalahan khusus untuk memandu pengguna saat entri data yang salah dibuat.

### Ingyenesen használható az Aspose.Cells?
Aspose.Cells menawarkan uji coba gratis, tetapi Anda memerlukan lisensi untuk penggunaan jangka panjang. Anda dapat menemukan informasi lebih lanjut tentang cara memperoleh lisensi sementara [itt](https://purchase.aspose.com/temporary-license/).

### Tipe data apa yang dapat saya validasi di Excel?
Dengan Aspose.Cells, Anda dapat memvalidasi berbagai tipe data termasuk bilangan bulat, desimal, tanggal, daftar, dan rumus khusus.

### Di mana saya dapat menemukan lebih banyak dokumentasi Aspose.Cells?
Anda dapat menjelajahi dokumentasi yang luas [itt](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}