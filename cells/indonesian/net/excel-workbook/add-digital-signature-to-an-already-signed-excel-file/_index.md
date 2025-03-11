---
title: Tambahkan Tanda Tangan Digital ke File Excel yang Sudah Ditandatangani
linktitle: Tambahkan Tanda Tangan Digital ke File Excel yang Sudah Ditandatangani
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara menambahkan tanda tangan digital ke file Excel yang sudah ditandatangani menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah terperinci ini.
weight: 30
url: /id/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Tanda Tangan Digital ke File Excel yang Sudah Ditandatangani

## Perkenalan

Di dunia digital saat ini, pengamanan dokumen menjadi lebih penting dari sebelumnya. Tanda tangan digital menyediakan cara untuk memastikan keaslian dan integritas berkas Anda, terutama saat menangani informasi sensitif. Jika Anda bekerja dengan berkas Excel dan ingin menambahkan tanda tangan digital baru ke buku kerja yang telah ditandatangani, Anda berada di tempat yang tepat! Dalam panduan ini, kami akan memandu Anda melalui proses penambahan tanda tangan digital ke berkas Excel yang telah ditandatangani menggunakan Aspose.Cells for .NET. Jadi, mari kita mulai!

## Prasyarat

Sebelum kita masuk ke inti pengkodean, ada beberapa hal yang perlu Anda siapkan:

1.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells di proyek .NET Anda. Anda dapat mengunduhnya dari[lokasi](https://releases.aspose.com/cells/net/).
2.  File Sertifikat: Anda memerlukan file sertifikat yang valid (biasanya`.pfx`file) yang berisi sertifikat digital Anda. Pastikan Anda mengetahui kata sandi untuk file ini.
3. Lingkungan Pengembangan: Siapkan lingkungan pengembangan Anda dengan Visual Studio atau IDE lain yang mendukung .NET.
4. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda mengikutinya dengan lancar.
5. File Contoh: Miliki file Excel contoh yang sudah ditandatangani secara digital. Ini akan menjadi file tempat Anda akan menambahkan tanda tangan baru.

Sekarang setelah semuanya siap, mari kita mulai membuat kode!

## Paket Impor

Untuk memulai, Anda perlu mengimpor paket yang diperlukan ke dalam berkas C# Anda. Berikut cara melakukannya:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ruang nama ini akan memungkinkan Anda bekerja dengan berkas Excel dan menangani tanda tangan digital dengan lancar.

## Langkah 1: Siapkan Direktori Sumber dan Output Anda

Sebelum Anda dapat memanipulasi file Excel, Anda perlu menentukan lokasi file sumber dan lokasi penyimpanan file output. Berikut cara melakukannya:

```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Document Directory";
```

Pada langkah ini, kami menggunakan metode untuk mendapatkan jalur bagi direktori sumber dan keluaran. Pastikan direktori ini ada dan berisi file yang diperlukan.

## Langkah 2: Muat Buku Kerja yang Sudah Ditandatangani

 Selanjutnya, Anda perlu memuat buku kerja Excel yang ingin Anda ubah. Hal ini dilakukan dengan membuat contoh`Workbook` kelas dan meneruskan jalur file yang ditandatangani.

```csharp
// Muat buku kerja yang sudah ditandatangani secara digital
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

 Di sini, kita memuat buku kerja bernama`sampleDigitallySignedByCells.xlsx`Pastikan berkas ini sudah ditandatangani.

## Langkah 3: Buat Koleksi Tanda Tangan Digital

Sekarang, mari buat koleksi tanda tangan digital. Koleksi ini akan menampung semua tanda tangan digital yang ingin Anda tambahkan ke buku kerja.

```csharp
// Buat koleksi tanda tangan digital
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Langkah ini penting karena memungkinkan Anda mengelola beberapa tanda tangan jika diperlukan.

## Langkah 4: Buat Sertifikat Baru

 Anda perlu memuat berkas sertifikat Anda untuk membuat tanda tangan digital baru. Di sinilah Anda menentukan jalur ke`.pfx` file dan kata sandinya.

```csharp
// File sertifikat dan kata sandinya
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Buat sertifikat baru
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

 Pastikan untuk mengganti`AsposeDemo.pfx`dan kata sandi dengan nama file sertifikat dan kata sandi Anda yang sebenarnya.

## Langkah 5: Buat Tanda Tangan Digital

Dengan sertifikat di tangan, Anda sekarang dapat membuat tanda tangan digital. Anda juga perlu memberikan alasan untuk tanda tangan tersebut serta tanggal dan waktu saat ini.

```csharp
// Buat tanda tangan digital baru dan tambahkan ke koleksi tanda tangan digital
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Langkah ini menambahkan tanda tangan baru ke koleksi Anda, yang nantinya akan Anda terapkan ke buku kerja.

## Langkah 6: Tambahkan Koleksi Tanda Tangan Digital ke Buku Kerja

Sekarang saatnya menambahkan koleksi tanda tangan digital ke buku kerja. Di sinilah keajaiban terjadi!

```csharp
// Tambahkan koleksi tanda tangan digital di dalam buku kerja
workbook.AddDigitalSignature(dsCollection);
```

Dengan mengeksekusi baris ini, Anda secara efektif melampirkan tanda tangan digital baru ke buku kerja yang telah ditandatangani.

## Langkah 7: Simpan dan Buang Buku Kerja

Terakhir, Anda ingin menyimpan buku kerja yang dimodifikasi ke direktori keluaran dan melepaskan sumber daya apa pun yang sedang digunakan.

```csharp
//Simpan buku kerja dan buang.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Langkah ini memastikan bahwa perubahan Anda disimpan, dan buku kerja dibuang dengan benar untuk mengosongkan sumber daya.

## Langkah 8: Konfirmasi Eksekusi

Sebagai penutup, sebaiknya Anda mengonfirmasi bahwa kode Anda berhasil dijalankan. Anda dapat melakukannya dengan pesan konsol sederhana.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Ini memberikan umpan balik bahwa operasi Anda berhasil, dan itu selalu menyenangkan untuk dilihat!

## Kesimpulan

Nah, itu dia! Anda telah berhasil menambahkan tanda tangan digital baru ke berkas Excel yang sudah ditandatangani menggunakan Aspose.Cells for .NET. Tanda tangan digital adalah cara yang ampuh untuk memastikan keaslian dokumen Anda, dan kini Anda tahu cara mengelolanya secara terprogram. Baik Anda sedang mengerjakan dokumen keuangan, kontrak, atau informasi sensitif lainnya, penerapan tanda tangan digital dapat meningkatkan keamanan dan kepercayaan.

## Pertanyaan yang Sering Diajukan

### Apa itu tanda tangan digital?
Tanda tangan digital adalah metode kriptografi yang digunakan untuk memvalidasi keaslian dan integritas suatu pesan atau dokumen.

### Bisakah saya menambahkan beberapa tanda tangan digital ke file Excel yang sama?
Ya, Anda dapat membuat koleksi tanda tangan digital dan menambahkan beberapa tanda tangan ke buku kerja yang sama.

### Format apa yang didukung Aspose.Cells untuk tanda tangan digital?
 Aspose.Cells mendukung berbagai format, termasuk`.pfx` untuk sertifikat.

### Apakah saya memerlukan versi .NET tertentu untuk menggunakan Aspose.Cells?
 Periksa[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk kompatibilitas dengan versi .NET Anda.

### Bagaimana cara mendapatkan lisensi sementara untuk Aspose.Cells?
 Anda dapat meminta lisensi sementara dari[Halaman pembelian Aspose](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
