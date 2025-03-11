---
title: Tambahkan Tanda Tangan Digital ke File Excel yang Ditandatangani
linktitle: Tambahkan Tanda Tangan Digital ke File Excel yang Ditandatangani
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menambahkan tanda tangan digital ke berkas Excel yang sudah ditandatangani menggunakan Aspose.Cells for .NET dalam panduan langkah demi langkah ini. Amankan dokumen Anda.
weight: 12
url: /id/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Tanda Tangan Digital ke File Excel yang Ditandatangani

## Perkenalan
Di dunia digital saat ini, memastikan keaslian dan integritas dokumen sangatlah penting. Tanda tangan digital berfungsi sebagai cara yang kuat untuk memverifikasi bahwa dokumen belum diubah dan berasal dari sumber yang sah. Jika Anda bekerja dengan file Excel dalam .NET dan ingin menambahkan tanda tangan digital ke file yang sudah ditandatangani, Anda berada di tempat yang tepat! Dalam panduan ini, kami akan memandu Anda melalui proses penambahan tanda tangan digital baru ke file Excel yang sudah ditandatangani menggunakan Aspose.Cells untuk .NET. 
## Prasyarat
Sebelum kita masuk ke inti pembahasan, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai:
1.  Aspose.Cells untuk .NET: Pertama dan terutama, Anda harus menginstal Aspose.Cells di lingkungan .NET Anda. Anda dapat mengunduhnya dari[halaman rilis](https://releases.aspose.com/cells/net/).
2. .NET Framework: Pastikan Anda telah menginstal .NET Framework di komputer Anda. Panduan ini mengasumsikan bahwa Anda sudah familier dengan konsep dasar pemrograman .NET.
3. Sertifikat Digital: Anda memerlukan sertifikat digital yang valid (dalam format .pfx) untuk membuat tanda tangan digital. Jika Anda tidak memilikinya, Anda dapat membuat sertifikat yang ditandatangani sendiri untuk tujuan pengujian.
4. Lingkungan Pengembangan: Editor kode atau IDE seperti Visual Studio tempat Anda dapat menulis dan mengeksekusi kode C# Anda.
5. Contoh Berkas Excel: Anda harus memiliki berkas Excel yang sudah ditandatangani secara digital. Ini akan menjadi berkas yang akan kami tambahkan tanda tangan lainnya.
Setelah semua prasyarat ini terpenuhi, mari masuk ke kodenya!
## Paket Impor
Sebelum Anda mulai membuat kode, pastikan untuk mengimpor namespace yang diperlukan. Berikut ini yang perlu Anda sertakan di bagian atas berkas C# Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ruang nama ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk memanipulasi file Excel dan menangani tanda tangan digital.
Sekarang, mari kita uraikan prosesnya menjadi beberapa langkah yang mudah dikelola. Kita akan membahas setiap langkah untuk memastikan Anda memahami cara menambahkan tanda tangan digital ke berkas Excel yang sudah ditandatangani.
## Langkah 1: Tentukan Direktori Anda
Pertama, Anda perlu menentukan di mana file sumber Anda berada dan di mana akan menyimpan file output. Ini mudah tetapi penting:
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory"; // Ganti dengan direktori Anda yang sebenarnya
// Direktori keluaran
string outputDir = "Your Document Directory"; // Ganti dengan direktori Anda yang sebenarnya
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Anda disimpan. Ini mengatur tahapan untuk operasi file Anda.
## Langkah 2: Muat Buku Kerja yang Sudah Ditandatangani
Berikutnya, Anda akan memuat buku kerja Excel yang sudah ditandatangani. Di sinilah keajaiban dimulai:
```csharp
// Muat buku kerja yang sudah ditandatangani secara digital untuk menambahkan tanda tangan digital baru
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
 Baris ini menginisialisasi yang baru`Workbook` objek dengan file yang ditentukan. Pastikan nama file sesuai dengan file Excel yang sudah ditandatangani.
## Langkah 3: Buat Koleksi Tanda Tangan Digital
Untuk mengelola tanda tangan digital Anda, Anda perlu membuat koleksi. Koleksi ini memungkinkan Anda menyimpan beberapa tanda tangan jika diperlukan:
```csharp
// Buat koleksi tanda tangan digital
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
Koleksi ini akan menjadi tempat Anda menambahkan tanda tangan digital baru sebelum menerapkannya ke buku kerja.
## Langkah 4: Muat Sertifikat Anda
Sekarang saatnya memuat sertifikat digital Anda. Sertifikat ini akan digunakan untuk membuat tanda tangan baru:
```csharp
// File sertifikat dan kata sandinya
string certFileName = sourceDir + "AsposeDemo.pfx"; // File sertifikat Anda
string password = "aspose"; //Kata sandi sertifikat Anda
// Buat sertifikat baru
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
 Pastikan untuk mengganti`AsposeDemo.pfx` dengan nama berkas sertifikat Anda dan perbarui kata sandinya. Langkah ini penting karena tanpa sertifikat yang benar, Anda tidak akan dapat membuat tanda tangan yang valid.
## Langkah 5: Buat Tanda Tangan Digital Baru
Setelah sertifikat Anda dimuat, kini Anda dapat membuat tanda tangan digital baru. Tanda tangan ini akan ditambahkan ke koleksi Anda:
```csharp
// Buat tanda tangan digital baru dan tambahkan ke koleksi tanda tangan digital
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
Di sini, Anda memberikan pesan yang menjelaskan tanda tangan, yang dapat membantu pencatatan. Stempel waktu memastikan bahwa tanda tangan dikaitkan dengan momen waktu yang tepat.
## Langkah 6: Tambahkan Koleksi Tanda Tangan ke Buku Kerja
Setelah membuat tanda tangan, saatnya menambahkan seluruh koleksi ke buku kerja:
```csharp
// Tambahkan koleksi tanda tangan digital di dalam buku kerja
workbook.AddDigitalSignature(dsCollection);
```
Langkah ini secara efektif menerapkan tanda tangan digital baru Anda ke buku kerja, menandainya dengan keaslian tambahan.
## Langkah 7: Simpan Buku Kerja
Terakhir, simpan buku kerja dengan menyertakan tanda tangan digital baru. Inilah saatnya semua kerja keras Anda terbayar:
```csharp
//Simpan buku kerja dan buang.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
Pastikan untuk menentukan nama untuk berkas keluaran Anda. Ini akan menjadi versi baru berkas Excel Anda, lengkap dengan tanda tangan digital tambahan.
## Langkah 8: Konfirmasikan Keberhasilan
Sebagai penutup, ada baiknya memberikan umpan balik setelah operasi selesai dengan sukses:
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
Baris ini akan mencetak pesan konfirmasi ke konsol, memberi tahu Anda bahwa semuanya berjalan lancar.
## Kesimpulan
Nah, itu dia! Anda telah berhasil menambahkan tanda tangan digital baru ke berkas Excel yang sudah ditandatangani menggunakan Aspose.Cells for .NET. Proses ini tidak hanya meningkatkan keamanan dokumen Anda, tetapi juga memastikan bahwa dokumen tersebut dapat dipercaya dan diverifikasi. 
Tanda tangan digital sangat penting dalam lanskap digital saat ini, terutama bagi bisnis dan profesional yang perlu menjaga integritas dokumen mereka. Dengan mengikuti panduan ini, Anda dapat dengan mudah mengelola tanda tangan digital dalam file Excel Anda, memastikan bahwa data Anda tetap aman dan autentik.
## Pertanyaan yang Sering Diajukan
### Apa itu tanda tangan digital?
Tanda tangan digital adalah skema matematika untuk memverifikasi keaslian dan integritas pesan atau dokumen digital. Skema ini memastikan bahwa dokumen tersebut tidak diubah dan mengonfirmasi identitas penanda tangan.
### Apakah saya memerlukan sertifikat khusus untuk membuat tanda tangan digital?
Ya, Anda memerlukan sertifikat digital yang diterbitkan oleh otoritas sertifikat (CA) tepercaya untuk membuat tanda tangan digital yang valid.
### Dapatkah saya menggunakan sertifikat yang ditandatangani sendiri untuk pengujian?
Tentu saja! Anda dapat membuat sertifikat yang ditandatangani sendiri untuk tujuan pengembangan dan pengujian, tetapi untuk produksi, sebaiknya gunakan sertifikat dari CA tepercaya.
### Apa yang terjadi jika saya mencoba menambahkan tanda tangan ke dokumen yang tidak ditandatangani?
Jika Anda mencoba menambahkan tanda tangan digital ke dokumen yang belum ditandatangani, prosesnya akan berfungsi tanpa masalah, tetapi tanda tangan asli tidak akan ada.
### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells?
 Anda dapat memeriksa[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk panduan terperinci dan referensi API.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
