---
title: Salin Baris menggunakan Aspose.Cells untuk .NET
linktitle: Salin Baris menggunakan Aspose.Cells untuk .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyalin baris dalam file Excel secara efisien menggunakan Aspose.Cells for .NET. Panduan langkah demi langkah ini menyederhanakan penyalinan baris untuk kebutuhan manajemen data Anda.
weight: 11
url: /id/net/row-and-column-management/copying-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Baris menggunakan Aspose.Cells untuk .NET

## Perkenalan
Jika Anda bekerja dengan file Excel di lingkungan .NET, Aspose.Cells untuk .NET adalah alat hebat yang perlu Anda ketahui. Dengan alat ini, Anda dapat mengotomatiskan tugas-tugas seperti membuat lembar kerja baru, memformat sel, dan bahkan menyalin baris dengan mudah. Bayangkan menangani kumpulan data besar atau mengulang baris templat dengan mudah—Aspose.Cells untuk .NET membuat tugas-tugas ini mudah! Dalam tutorial ini, kami akan fokus pada satu tugas khusus: menyalin baris dalam file Excel. Kami akan membahas prasyarat, mengimpor paket yang diperlukan, dan panduan langkah demi langkah untuk mempermudah proses ini. Jadi, mari kita mulai!
## Prasyarat
Sebelum kita masuk ke kode, berikut ini yang Anda perlukan:
1.  Aspose.Cells untuk .NET: Pastikan Anda memiliki versi terbaru. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/) atau[dapatkan uji coba gratis](https://releases.aspose.com/).
2. Lingkungan Pengembangan: Lingkungan apa pun yang kompatibel dengan .NET seperti Visual Studio.
3. Pengetahuan Dasar C#: Meskipun panduan ini ramah bagi pemula, keakraban dengan C# akan membantu Anda memahami setiap langkah dengan lebih baik.
4.  Lisensi: Untuk akses penuh, dapatkan[lisensi sementara](https://purchase.aspose.com/temporary-license/) jika diperlukan.
## Paket Impor
Untuk memulai, pastikan untuk mengimpor namespace yang diperlukan dalam kode Anda. Pustaka ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk menangani file Excel.
```csharp
using System.IO;
using Aspose.Cells;
```
Mari kita uraikan kode tersebut menjadi beberapa langkah sederhana. Setiap langkah akan memandu Anda melalui proses tersebut, mulai dari membuka buku kerja Excel hingga menyimpan berkas yang diperbarui dengan baris yang disalin.
## Langkah 1: Atur Jalur ke Direktori Anda
Pertama-tama, kita perlu mengatur jalur direktori tempat file Excel Anda berada. Anggap saja ini seperti menyiapkan ruang kerja sehingga program mengetahui di mana menemukan file untuk dikerjakan.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya di mesin Anda tempat file Excel Anda (`book1.xls`) disimpan.
## Langkah 2: Buka File Excel yang Ada
 Sekarang setelah jalur sudah ditetapkan, mari kita muat file Excel ke dalam program kita. Menggunakan`Workbook` kelas dari Aspose.Cells, kita dapat dengan mudah membuka dan mengakses file Excel kita.
```csharp
// Buka berkas Excel yang ada.
Workbook excelWorkbook1 = new Workbook(dataDir + "book1.xls");
```
 Di Sini,`excelWorkbook1` adalah objek buku kerja Anda yang sekarang berisi semua data dari`book1.xls`Ini memungkinkan kita untuk bekerja dengan lembar kerja, sel, dan baris dalam berkas ini.
## Langkah 3: Akses Lembar Kerja yang Diinginkan
Dengan buku kerja yang terbuka, langkah berikutnya adalah memilih lembar kerja tempat Anda ingin menyalin baris. Dalam contoh ini, kita akan bekerja dengan lembar kerja pertama dalam buku kerja.
```csharp
// Dapatkan lembar kerja pertama dalam buku kerja.
Worksheet wsTemplate = excelWorkbook1.Worksheets[0];
```
 Itu`Worksheets[0]` indeks memilih lembar kerja pertama. Jika data Anda ada di lembar kerja lain, sesuaikan indeks sebagaimana mestinya.
## Langkah 4: Salin Baris Target
Sekarang tibalah bagian inti dari tutorial kita: menyalin baris. Di sini, kita akan menyalin data dari baris 2 (indeks 1, karena baris diindeks nol) ke baris 16 (indeks 15) dalam lembar kerja yang sama.
```csharp
// Salin baris kedua dengan data, format, gambar, dan objek gambar ke baris ke-16.
wsTemplate.Cells.CopyRow(wsTemplate.Cells, 1, 15);
```
Dalam perintah ini:
- Baris Sumber (1): Ini adalah baris yang kita salin, yang sesuai dengan baris 2 di Excel.
- Baris Tujuan (15): Di sinilah kita ingin baris yang disalin ditempel, sesuai dengan baris 16 di Excel.
 Itu`CopyRow` metode ini efisien—tidak hanya menyalin data tetapi juga format, gambar, atau objek apa pun di baris tersebut.
## Langkah 5: Simpan File Excel yang Diperbarui
Setelah salinan baris selesai, saatnya untuk menyimpan file Excel yang dimodifikasi. Ini memastikan bahwa semua perubahan yang dibuat`excelWorkbook1` dilestarikan.
```csharp
// Simpan berkas Excel.
excelWorkbook1.Save(dataDir + "output.xls");
```
 Di sini, kami menyimpan buku kerja yang diperbarui sebagai`output.xls` di direktori yang sama dengan berkas asli. Anda dapat mengubah nama dan lokasi berkas jika diperlukan.
## Kesimpulan
Nah, itu dia! Hanya dengan beberapa baris kode, Anda telah berhasil menyalin baris di Excel menggunakan Aspose.Cells untuk .NET. Tutorial ini mencakup langkah-langkah penting, mulai dari menyiapkan jalur dokumen hingga menyimpan file yang telah diperbarui. Aspose.Cells membuat manipulasi Excel menjadi mudah, baik saat Anda menyalin baris, memformat sel, atau menangani kumpulan data besar. Jadi, lain kali Anda perlu mereplikasi data di seluruh baris, Anda akan tahu persis cara melakukannya.
## Pertanyaan yang Sering Diajukan
### Bisakah saya menyalin beberapa baris sekaligus menggunakan Aspose.Cells untuk .NET?  
 Ya, Anda dapat mengulang baris dan menggunakan`CopyRow` metode dalam satu loop untuk menyalin beberapa baris.
### Bagaimana cara menyalin baris antar lembar kerja yang berbeda?  
Cukup tentukan lembar kerja sumber dan tujuan di`CopyRow` metode. Metode ini bekerja di beberapa lembar kerja dalam buku kerja yang sama.
### Apakah Aspose.Cells untuk .NET mempertahankan format baris saat menyalin?  
 Tentu saja!`CopyRow` metode menyalin data, pemformatan, gambar, dan bahkan objek gambar.
### Apakah Aspose.Cells untuk .NET kompatibel dengan .NET Core?  
Ya, Aspose.Cells mendukung .NET Framework, .NET Core, dan .NET Standard, memberikan fleksibilitas di berbagai lingkungan .NET.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells untuk .NET?  
 Meskipun ada uji coba gratis yang tersedia,[lisensi sementara atau penuh](https://purchase.aspose.com/buy) direkomendasikan untuk fungsionalitas penuh dan menghilangkan segala batasan.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
