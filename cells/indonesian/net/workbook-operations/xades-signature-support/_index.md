---
title: Dukungan XAdESSignature di Buku Kerja menggunakan Aspose.Cells
linktitle: Dukungan XAdESSignature di Buku Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menerapkan dukungan tanda tangan XAdES di buku kerja Excel menggunakan Aspose.Cells untuk .NET. Ikuti panduan langkah demi langkah kami untuk penandatanganan dokumen yang aman.
weight: 29
url: /id/net/workbook-operations/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dukungan XAdESSignature di Buku Kerja menggunakan Aspose.Cells

## Perkenalan
Di dunia digital saat ini, integritas dan keaslian data adalah yang terpenting. Bayangkan Anda sedang mengirim dokumen Excel yang penting, dan Anda ingin memastikan bahwa penerima tahu bahwa dokumen tersebut tidak dirusak. Di sinilah tanda tangan digital berperan! Dengan Aspose.Cells untuk .NET, Anda dapat dengan mudah menambahkan tanda tangan XAdES ke buku kerja Excel Anda, memastikan bahwa data Anda tetap aman dan tepercaya. Dalam tutorial ini, kami akan memandu Anda melalui proses penerapan dukungan tanda tangan XAdES di file Excel Anda langkah demi langkah. Mari kita mulai!
## Prasyarat
Sebelum kita memulai, ada beberapa hal yang perlu Anda siapkan untuk mengikuti tutorial ini:
1. Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
2. Lingkungan Pengembangan: IDE yang cocok untuk pengembangan .NET, seperti Visual Studio.
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
4. Sertifikat Digital: Berkas PFX (pertukaran informasi pribadi) yang valid yang berisi sertifikat digital Anda dan kata sandi untuk mengaksesnya.
Sudah mendapatkan semuanya? Bagus! Mari kita lanjutkan ke langkah berikutnya.
## Paket Impor
Untuk memulai dengan Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan dalam proyek C# Anda. Ini akan memungkinkan Anda mengakses kelas dan metode yang diperlukan untuk menambahkan tanda tangan digital. Berikut cara melakukannya:
### Buat Proyek C# Baru
1. Buka Visual Studio.
2. Buat proyek Aplikasi Konsol baru.
3.  Beri nama proyek Anda sesuatu yang dapat dikenali, seperti`XAdESSignatureExample`.
### Tambahkan Referensi Aspose.Cells
1.  Klik kanan pada proyek Anda di Solution Explorer dan pilih`Manage NuGet Packages`.
2.  Pencarian untuk`Aspose.Cells` dan instal versi terbaru.
### Impor Namespace yang Diperlukan
 Di bagian atas Anda`Program.cs` file, tambahkan perintah berikut menggunakan perintah:
```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```
Ini akan memungkinkan Anda untuk menggunakan kelas dan metode Aspose.Cells dalam proyek Anda.
Sekarang setelah Anda menyiapkan semuanya, mari kita uraikan proses penambahan tanda tangan XAdES ke buku kerja Anda ke dalam langkah-langkah yang dapat dikelola.
## Langkah 1: Siapkan Direktori Sumber dan Output Anda
Sebelum Anda mulai bekerja dengan berkas Excel Anda, Anda perlu menentukan di mana berkas sumber Anda berada dan di mana Anda ingin menyimpan berkas keluaran.
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"`dengan jalur sebenarnya tempat file Excel Anda disimpan dan tempat Anda ingin menyimpan file yang ditandatangani.
## Langkah 2: Muat Buku Kerja
 Selanjutnya, Anda akan memuat buku kerja Excel yang ingin Anda tandatangani. Ini dilakukan dengan menggunakan`Workbook` kelas dari Aspose.Cells.
```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```
 Pastikan untuk mengganti`"sourceFile.xlsx"` dengan nama berkas Excel Anda sebenarnya.
## Langkah 3: Siapkan Sertifikat Digital Anda
Untuk menambahkan tanda tangan digital, Anda perlu memuat berkas PFX dan memberikan kata sandinya. Berikut cara melakukannya:
```csharp
string password = "pfxPassword"; // Ganti dengan kata sandi PFX Anda
string pfx = "pfxFile"; // Jalur ke file PFX Anda
```
 Pastikan untuk mengganti`"pfxPassword"` dengan kata sandi Anda yang sebenarnya dan`"pfxFile"` dengan jalur ke berkas PFX Anda.
## Langkah 4: Buat Tanda Tangan Digital
 Sekarang saatnya membuat tanda tangan digital menggunakan`DigitalSignature` kelas. Anda perlu membaca berkas PFX ke dalam array byte dan kemudian membuat tanda tangan.
```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```
 Di Sini,`"testXAdES"` adalah alasan untuk menandatangani, dan`DateTime.Now` menunjukkan waktu penandatanganan.
## Langkah 5: Tambahkan Tanda Tangan ke Buku Kerja
 Untuk menambahkan tanda tangan ke buku kerja Anda, Anda perlu membuat`DigitalSignatureCollection` dan tambahkan tanda tangan Anda di dalamnya.
```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
```
## Langkah 6: Mengatur Tanda Tangan Digital ke Buku Kerja
Sekarang setelah koleksi tanda tangan Anda siap, waktunya untuk mengaturnya ke dalam buku kerja.
```csharp
workbook.SetDigitalSignature(dsCollection);
```
## Langkah 7: Simpan Buku Kerja
Terakhir, simpan buku kerja Anda dengan tanda tangan digital yang diterapkan.
```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
```
 Mengganti`"XAdESSignatureSupport_out.xlsx"` dengan nama file keluaran yang Anda inginkan.
## Langkah 8: Konfirmasikan Keberhasilan
Untuk memastikan semuanya berjalan lancar, Anda dapat mencetak pesan sukses ke konsol.
```csharp
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```
## Kesimpulan
 Nah, itu dia! Anda telah berhasil menambahkan dukungan tanda tangan XAdES ke buku kerja Excel Anda menggunakan Aspose.Cells for .NET. Fitur hebat ini tidak hanya meningkatkan keamanan dokumen Anda, tetapi juga membantu menjaga integritas data Anda. Jika Anda memiliki pertanyaan atau mengalami masalah, silakan periksa[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) atau kunjungi[forum dukungan](https://forum.aspose.com/c/cells/9) untuk bantuan.
## Pertanyaan yang Sering Diajukan
### Apa itu XAdES?
XAdES (XML Advanced Electronic Signatures) adalah standar tanda tangan elektronik yang memastikan integritas dan keaslian dokumen elektronik.
### Apakah saya memerlukan sertifikat digital untuk menggunakan tanda tangan XAdES?
Ya, Anda memerlukan sertifikat digital yang valid dalam format PFX untuk membuat tanda tangan XAdES.
### Dapatkah saya menggunakan Aspose.Cells untuk format file lain?
Ya, Aspose.Cells terutama berfungsi dengan berkas Excel, tetapi juga mendukung berbagai format lembar kerja lainnya.
### Apakah ada uji coba gratis yang tersedia untuk Aspose.Cells?
Tentu saja! Anda bisa mendapatkan uji coba gratis[Di Sini](https://releases.aspose.com/).
### Di mana saya dapat menemukan lebih banyak contoh dan tutorial?
 Anda dapat menjelajahi lebih banyak contoh dan dokumentasi terperinci di[Situs web Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
