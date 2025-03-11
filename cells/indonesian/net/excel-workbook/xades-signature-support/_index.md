---
title: Dukungan Tanda Tangan Xades
linktitle: Dukungan Tanda Tangan Xades
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara menambahkan tanda tangan Xades ke berkas Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah ini. Amankan dokumen Anda.
weight: 190
url: /id/net/excel-workbook/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dukungan Tanda Tangan Xades

## Perkenalan

Di dunia digital saat ini, pengamanan dokumen menjadi lebih penting dari sebelumnya. Baik Anda berurusan dengan informasi bisnis yang sensitif maupun data pribadi, memastikan integritas dan keaslian berkas Anda adalah yang terpenting. Salah satu cara untuk mencapainya adalah melalui tanda tangan digital, khususnya, tanda tangan Xades. Jika Anda seorang pengembang .NET yang ingin menerapkan dukungan tanda tangan Xades di aplikasi Anda, Anda berada di tempat yang tepat! Dalam panduan ini, kami akan memandu Anda melalui proses penambahan tanda tangan Xades ke berkas Excel menggunakan Aspose.Cells untuk .NET. Jadi, mari kita langsung mulai!

## Prasyarat

Sebelum kita memulai, ada beberapa hal yang perlu Anda siapkan:

1.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya dengan mudah dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
2. Lingkungan Pengembangan: Lingkungan pengembangan .NET yang berfungsi (seperti Visual Studio) tempat Anda dapat menulis dan mengeksekusi kode Anda.
3. Sertifikat Digital: Anda memerlukan sertifikat digital yang valid (file PFX) beserta kata sandinya. Sertifikat ini penting untuk membuat tanda tangan digital.
4. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami contoh-contohnya dengan lebih baik.

Setelah prasyarat ini terpenuhi, Anda siap untuk mulai menerapkan tanda tangan Xades di file Excel Anda!

## Paket Impor

Untuk bekerja dengan Aspose.Cells for .NET, Anda perlu mengimpor namespace yang diperlukan. Berikut cara melakukannya:

```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```

Ruang nama ini menyediakan akses ke kelas dan metode yang diperlukan untuk bekerja dengan file Excel dan mengelola tanda tangan digital.

Sekarang setelah semuanya disiapkan, mari kita uraikan proses penambahan tanda tangan Xades ke berkas Excel menjadi beberapa langkah yang jelas dan mudah dikelola.

## Langkah 1: Siapkan Direktori Sumber dan Output Anda

Pertama, kita perlu menentukan di mana file Excel sumber kita berada dan di mana kita ingin menyimpan file output yang sudah ditandatangani. Ini adalah langkah penting karena membantu dalam mengatur file Anda secara efisien.

```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Output Directory";
```

## Langkah 2: Muat Buku Kerja

Selanjutnya, mari kita muat buku kerja Excel yang ingin kita tandatangani. Di sinilah Anda akan memuat berkas Excel yang sudah ada.

```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```

 Di sini, kita membuat contoh baru dari`Workbook` class, dengan meneruskan jalur file Excel sumber. Pastikan nama file sesuai dengan yang ada di direktori sumber.

## Langkah 3: Siapkan Sertifikat Digital Anda

Untuk membuat tanda tangan digital, Anda perlu memuat sertifikat digital Anda. Ini melibatkan pembacaan berkas PFX dan pemberian kata sandi untuk berkas tersebut.

```csharp
string password = "pfxPassword"; // Ganti dengan kata sandi PFX Anda
string pfx = "pfxFile"; // Ganti dengan jalur ke file PFX Anda
```

 Pada langkah ini, ganti`pfxPassword` dengan kata sandi Anda yang sebenarnya dan`pfxFile` dengan jalur ke berkas PFX Anda. Ini adalah kunci untuk menandatangani dokumen Anda!

## Langkah 4: Buat Tanda Tangan Digital

 Sekarang, mari kita membuat tanda tangan digital menggunakan`DigitalSignature` kelas. Di sinilah keajaiban terjadi!

```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```

 Dalam potongan kode ini, kita membaca file PFX ke dalam array byte dan membuat array baru.`DigitalSignature` objek. Kami juga mengatur`XAdESType` ke`XAdES`, yang penting untuk tanda tangan kita.

## Langkah 5: Tambahkan Tanda Tangan ke Buku Kerja

Setelah tanda tangan digital dibuat, langkah berikutnya adalah menambahkannya ke buku kerja.

```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
workbook.SetDigitalSignature(dsCollection);
```

 Di sini, kita membuat`DigitalSignatureCollection`, tambahkan tanda tangan kita ke dalamnya, lalu tetapkan koleksi ini ke buku kerja. Beginilah cara kita melampirkan tanda tangan ke berkas Excel.

## Langkah 6: Simpan Buku Kerja yang Telah Ditandatangani

Akhirnya, saatnya menyimpan buku kerja yang telah ditandatangani ke direktori keluaran. Langkah ini mengakhiri proses.

```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```

 Dalam kode ini, kita menyimpan buku kerja dengan nama baru,`XAdESSignatureSupport_out.xlsx`, di direktori output. Anda akan melihat pesan sukses di konsol setelah langkah ini selesai.

## Kesimpulan

Nah, itu dia! Anda telah berhasil menambahkan tanda tangan Xades ke berkas Excel Anda menggunakan Aspose.Cells for .NET. Proses ini tidak hanya meningkatkan keamanan dokumen Anda, tetapi juga membangun kepercayaan dengan pengguna Anda dengan memastikan keaslian berkas Anda. 
Tanda tangan digital merupakan bagian penting dari manajemen dokumen modern, dan dengan kekuatan Aspose.Cells, Anda dapat menerapkannya dengan mudah dalam aplikasi Anda.

## Pertanyaan yang Sering Diajukan

### Apa tanda tangan Xades?
Xades (XML Advanced Electronic Signatures) adalah standar tanda tangan digital yang menyediakan fitur tambahan untuk memastikan integritas dan keaslian dokumen elektronik.

### Apakah saya memerlukan sertifikat digital untuk membuat tanda tangan Xades?
Ya, Anda memerlukan sertifikat digital yang valid (file PFX) untuk membuat tanda tangan Xades.

### Dapatkah saya menguji Aspose.Cells untuk .NET sebelum membeli?
 Tentu saja! Anda bisa mendapatkan uji coba gratis dari[Situs web Aspose](https://releases.aspose.com/).

### Apakah Aspose.Cells kompatibel dengan semua versi .NET?
 Aspose.Cells mendukung berbagai versi kerangka kerja .NET. Periksa[dokumentasi](https://reference.aspose.com/cells/net/) untuk detail kompatibilitas.

### Di mana saya bisa mendapatkan dukungan jika saya mengalami masalah?
 Anda dapat mengunjungi[Forum Aspose](https://forum.aspose.com/c/cells/9) untuk dukungan dan bantuan masyarakat.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
