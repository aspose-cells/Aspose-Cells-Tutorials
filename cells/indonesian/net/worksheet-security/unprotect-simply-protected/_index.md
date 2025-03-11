---
title: Buka Proteksi Lembar Kerja yang Dilindungi Secara Sederhana menggunakan Aspose.Cells
linktitle: Buka Proteksi Lembar Kerja yang Dilindungi Secara Sederhana menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Buka proteksi lembar kerja Excel tanpa kata sandi dengan mudah menggunakan Aspose.Cells untuk .NET. Pelajari pengaturan, langkah-langkah kode, dan simpan output dengan mudah.
weight: 20
url: /id/net/worksheet-security/unprotect-simply-protected/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buka Proteksi Lembar Kerja yang Dilindungi Secara Sederhana menggunakan Aspose.Cells

## Perkenalan
Menghapus proteksi dari lembar kerja Excel dapat menjadi penyelamat saat Anda perlu membuat perubahan pada sel yang terkunci atau memperbarui data. Dengan Aspose.Cells for .NET, Anda dapat melakukannya dengan mudah melalui kode, yang memungkinkan Anda mengotomatiskan lembar kerja yang tidak terproteksi tanpa memerlukan kata sandi jika lembar kerja tersebut hanya diproteksi. Tutorial ini akan memandu Anda melalui setiap langkah, mulai dari menyiapkan prasyarat hingga menulis kode yang diperlukan, semuanya dengan cara yang mudah dipahami sehingga semuanya tetap sederhana namun efektif.
## Prasyarat
Sebelum kita mulai, mari pastikan Anda telah menyiapkan semuanya untuk mulai membuka proteksi lembar kerja dengan Aspose.Cells untuk .NET:
-  Aspose.Cells untuk .NET: Anda memerlukan pustaka ini untuk bekerja dengan file Excel secara terprogram. Anda dapat mengunduhnya dari[Halaman Unduhan Aspose.Cells](https://releases.aspose.com/cells/net/) atau mengaksesnya secara luas[dokumentasi](https://reference.aspose.com/cells/net/).
- Lingkungan Pengembangan: Lingkungan yang cocok untuk aplikasi .NET, seperti Visual Studio.
- Pemahaman Dasar C#: Beberapa pengetahuan dasar tentang pemrograman C# akan membantu untuk mengikuti contoh kode.
## Paket Impor
Untuk menggunakan Aspose.Cells di proyek .NET Anda, pertama-tama Anda perlu mengimpor pustaka Aspose.Cells. Hal ini dapat dilakukan dengan menambahkan paket Aspose.Cells NuGet ke proyek Anda. Berikut panduan singkatnya:
1. Buka proyek Anda di Visual Studio.
2. Di Solution Explorer, klik kanan pada proyek Anda dan pilih "Kelola Paket NuGet."
3. Cari "Aspose.Cells" dan instal versi terbaru.
4. Setelah terinstal, tambahkan impor berikut ke bagian atas berkas kode Anda:
```csharp
using System.IO;
using Aspose.Cells;
```
Sekarang, mari kita masuk ke proses sebenarnya untuk membuka proteksi lembar kerja Excel!
Mari kita uraikan prosesnya menjadi beberapa langkah yang mudah diikuti. Contoh ini mengasumsikan bahwa lembar kerja yang sedang Anda kerjakan tidak memiliki kunci yang dilindungi kata sandi.
## Langkah 1: Mengatur Direktori File
Pada langkah ini, kita tentukan direktori tempat file Excel kita disimpan. Ini akan memudahkan akses ke file input dan penyimpanan file output di lokasi yang diinginkan.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Dengan mengatur jalur direktori di`dataDir`Anda membuat pintasan praktis untuk mengakses dan menyimpan file tanpa perlu mengetikkan path lengkapnya berulang kali.
## Langkah 2: Muat Buku Kerja Excel
 Sekarang, mari kita muat file Excel yang ingin kita gunakan. Di sini, kita membuat file Excel baru.`Workbook` objek, yang mewakili keseluruhan file Excel.
```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook(dataDir + "book1.xls");
   ```
 Itu`Workbook` objek adalah bagian inti dari Aspose.Cells dan memungkinkan Anda untuk melakukan berbagai tindakan pada file Excel. Dengan melewati jalur`"book1.xls"`, baris ini memuat berkas target kita ke dalam program.
## Langkah 3: Akses Lembar Kerja yang Ingin Anda Buka Proteksinya
Setelah buku kerja dimuat, langkah berikutnya adalah menentukan lembar kerja mana yang ingin Anda batalkan proteksinya. Dalam contoh ini, kita akan mengakses lembar kerja pertama dalam buku kerja tersebut.
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Itu`Worksheets` properti memberi kita akses ke semua lembar kerja dalam buku kerja. Dengan menentukan`[0]`, kita mengakses lembar kerja pertama. Anda dapat menyesuaikan indeks ini jika lembar kerja target Anda berada di posisi yang berbeda.
## Langkah 4: Buka Proteksi Lembar Kerja
Sekarang tibalah bagian penting: membuka proteksi lembar kerja. Karena tutorial ini difokuskan pada lembar kerja yang diproteksi secara sederhana (yang tidak memiliki kata sandi), membuka proteksi menjadi mudah.
```csharp
// Membuka proteksi lembar kerja tanpa kata sandi
worksheet.Unprotect();
```
 Di Sini,`Unprotect()` disebut pada`worksheet` objek. Karena kita berurusan dengan lembar yang tidak dilindungi kata sandi, tidak diperlukan parameter tambahan. Lembar kerja sekarang seharusnya tidak dilindungi dan dapat diedit.
## Langkah 5: Simpan Buku Kerja yang Diperbarui
Setelah membuka proteksi lembar kerja, kita perlu menyimpan buku kerja tersebut. Anda dapat memilih untuk menimpa berkas asli atau menyimpannya sebagai berkas baru.
```csharp
// Menyimpan Buku Kerja
workbook.Save(dataDir + "output.xls", SaveFormat.Excel97To2003);
```
 Pada baris ini, kita menyimpan buku kerja menggunakan`Save` metode.`SaveFormat.Excel97To2003` memastikan buku kerja disimpan dalam format Excel yang lebih lama, yang dapat berguna jika kompatibilitas menjadi masalah. Ubah format jika Anda menggunakan versi Excel yang lebih baru.
## Kesimpulan
Selesai! Hanya dengan beberapa baris kode, Anda telah berhasil membuka proteksi lembar kerja yang diproteksi secara sederhana dalam file Excel menggunakan Aspose.Cells for .NET. Pendekatan ini sangat bagus untuk mengotomatisasi tugas dalam file Excel, sehingga menghemat waktu dan tenaga Anda. Ditambah lagi, dengan Aspose.Cells, Anda dilengkapi dengan alat yang hebat untuk mengelola dan memanipulasi file Excel secara terprogram, sehingga membuka banyak kemungkinan untuk mengotomatisasi alur kerja spreadsheet Anda.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells untuk .NET?
Aspose.Cells for .NET adalah pustaka yang hebat untuk bekerja dengan file Excel dalam aplikasi .NET. Pustaka ini memungkinkan Anda membuat, mengedit, mengonversi, dan memanipulasi file Excel tanpa perlu menginstal Microsoft Excel.
### Bisakah saya membuka proteksi lembar kerja yang dilindungi kata sandi dengan metode ini?
 Tidak, metode ini hanya berfungsi untuk lembar kerja yang dilindungi kata sandi. Untuk lembar kerja yang dilindungi kata sandi, Anda harus memberikan kata sandi di`Unprotect()` metode.
### Apakah saya perlu menginstal Microsoft Excel untuk menggunakan Aspose.Cells?
Tidak, Aspose.Cells beroperasi secara independen dari Microsoft Excel, jadi Anda tidak perlu menginstalnya di sistem Anda.
### Bisakah saya menyimpan lembar kerja yang tidak dilindungi dalam format Excel yang lebih baru?
 Ya, Anda bisa. Aspose.Cells mendukung berbagai format, termasuk`XLSX` . Ubah saja format penyimpanan sesuai kebutuhan di`Save` metode.
### Apakah Aspose.Cells tersedia untuk platform selain .NET?
Ya, Aspose.Cells memiliki versi untuk Java dan platform lainnya, yang memungkinkan fungsionalitas serupa di berbagai lingkungan pemrograman.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
