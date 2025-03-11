---
title: Terapkan Pratinjau Hentian Halaman di Lembar Kerja
linktitle: Terapkan Pratinjau Hentian Halaman di Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Terapkan pratinjau pemisah halaman dengan mudah di Excel menggunakan Aspose.Cells untuk .NET. Tutorial ini memandu Anda langkah demi langkah untuk tata letak pencetakan yang optimal.
weight: 19
url: /id/net/worksheet-display/implement-page-break-preview/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Pratinjau Hentian Halaman di Lembar Kerja

## Perkenalan
Ingin menyempurnakan tata letak lembar kerja Excel Anda sebelum mencetak? Menerapkan pratinjau pemisah halaman adalah jawabannya! Dengan Aspose.Cells untuk .NET, proses ini mudah dan cepat. Tutorial ini akan memandu Anda melalui pengaturan, menunjukkan struktur kode, dan memandu Anda langkah demi langkah, sehingga memudahkan pengaturan pratinjau pemisah halaman di lembar kerja Anda. Mari kita mulai!
## Prasyarat
Sebelum kita masuk ke kode, mari pastikan Anda memiliki semua yang dibutuhkan untuk mengikuti tutorial ini.
1. Pustaka Aspose.Cells untuk .NET  
   Unduh versi terbaru dari[Halaman Unduhan Aspose.Cells untuk .NET](https://releases.aspose.com/cells/net/)Anda juga dapat menginstalnya melalui NuGet di Visual Studio.
2. Lingkungan Pengembangan  
   Lingkungan pengembangan, seperti Visual Studio, sangat penting untuk menjalankan kode.
3. Pengetahuan Dasar tentang C# dan .NET  
   Pemahaman umum tentang C# akan membuatnya lebih mudah untuk diikuti.
4. Lisensi  
    Pertimbangkan untuk menggunakan[Lisensi Sementara](https://purchase.aspose.com/temporary-license/) jika Anda menguji fitur.
## Paket Impor
Sebelum kita masuk ke langkah-langkahnya, pastikan untuk menyertakan pustaka penting guna memastikan kelancaran pengoperasian Aspose.Cells. Berikut pernyataan impornya:
```csharp
using System.IO;
using Aspose.Cells;
```
Sekarang setelah kita melakukan pengaturan, mari kita bahas prosesnya secara rinci dalam langkah-langkah berikut.
## Langkah 1: Siapkan Jalur Direktori
Pertama, kita perlu menentukan jalur direktori tempat file Excel Anda berada. Anggap saja ini sebagai pengaturan "basis" untuk proyek tersebut. Di sinilah file masukan Anda akan berada, dan di sinilah pula file yang dimodifikasi akan disimpan.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Excel Anda berada.
## Langkah 2: Buat Aliran File
Untuk mengakses dan memanipulasi berkas Excel, buatlah FileStream. Anggap FileStream sebagai "jalur" yang membuka saluran ke berkas Anda sehingga Aspose.Cells dapat membaca dan memodifikasinya.
```csharp
// Membuat aliran file yang berisi file Excel yang akan dibuka
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Pada baris ini kita buka`book1.xls` di FileMode.Open, yang memungkinkan kita untuk membaca dan mengubahnya. Pastikan bahwa berkas ini ada di direktori yang ditentukan.
## Langkah 3: Buat Instansiasi Objek Buku Kerja
 Objek Buku Kerja adalah tempat sebagian besar tindakan terjadi. Saat Anda membuat`Workbook` Misalnya, Anda pada dasarnya “membuka” file Excel Anda agar Aspose.Cells dapat melakukan modifikasi.
```csharp
// Membuat instance objek Buku Kerja
// Membuka file Excel melalui aliran file
Workbook workbook = new Workbook(fstream);
```
 Baris ini menginisialisasi buku kerja dari FileStream, yang memungkinkan Aspose.Cells bekerja langsung di`book1.xls`.
## Langkah 4: Akses Lembar Kerja Pertama
Di sebagian besar file Excel, Anda akan bekerja dengan lembar kerja tertentu. Di sini, kita mengakses lembar kerja pertama di buku kerja kita. Lembar kerja ini akan menampilkan pratinjau pemisah halaman.
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Itu`workbook.Worksheets[0]` perintah memilih lembar kerja pertama dalam koleksi. Jika Anda menginginkan lembar kerja yang berbeda, Anda dapat mengubah indeksnya.
## Langkah 5: Aktifkan Mode Pratinjau Hentian Halaman
Di sinilah kita mengaktifkan pratinjau jeda halaman. Pengaturan`IsPageBreakPreview` ke true memungkinkan Anda memvisualisasikan bagaimana lembar kerja akan terlihat saat dicetak, dengan indikator yang jelas mengenai bagian mana dari halaman yang akan rusak.
```csharp
// Menampilkan lembar kerja dalam pratinjau hentian halaman
worksheet.IsPageBreakPreview = true;
```
Saat Anda mengaktifkan fitur ini, lembar kerja Anda beralih ke mode pratinjau hentian halaman, yang memudahkan peninjauan dan penyesuaian tata letak untuk hasil cetak optimal.
## Langkah 6: Simpan Buku Kerja yang Dimodifikasi
Setelah melakukan penyesuaian, Anda perlu menyimpan berkas Anda. Langkah ini merupakan tempat di mana semua kerja keras Anda disatukan, menyimpan modifikasi Anda ke berkas baru.
```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(dataDir + "output.xls");
```
 Dalam contoh ini, kami menyimpan buku kerja yang dimodifikasi sebagai`output.xls` di direktori yang sama dengan berkas asli. Jangan ragu untuk mengubah nama berkas jika diperlukan.
## Langkah 7: Tutup Aliran File
Terakhir, tutup aliran file untuk melepaskan semua sumber daya. Anggap saja seperti menutup "jalur" ke file, memastikan semuanya tersimpan dan terkunci dengan benar.
```csharp
// Menutup aliran file untuk membebaskan semua sumber daya
fstream.Close();
```
Setelah langkah ini, modifikasi berkas Anda selesai. Aliran berkas tidak lagi diperlukan, jadi menutupnya akan mencegah penggunaan memori yang tidak diinginkan.
## Kesimpulan
Nah, itu dia! Dengan Aspose.Cells untuk .NET, pengaturan pratinjau pemisah halaman di Excel menjadi efisien dan mudah dikelola. Setiap langkah yang kami bahas, mulai dari pengaturan direktori hingga penyimpanan file yang dimodifikasi, memastikan bahwa Anda dapat menyesuaikan tata letak lembar kerja dengan yakin untuk dicetak. Baik Anda mengerjakan laporan terperinci atau lembar data sederhana, menguasai pratinjau pemisah halaman dapat membuat proses pencetakan Anda lancar.
## Pertanyaan yang Sering Diajukan
### Apa itu pratinjau hentian halaman?  
Pratinjau hentian halaman memungkinkan Anda melihat di mana halaman akan terputus saat Anda mencetak, sehingga memudahkan penyesuaian tata letak untuk hasil cetak yang optimal.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells untuk .NET?  
 Ya, Anda memerlukan lisensi untuk fungsionalitas penuh. Anda bisa mendapatkannya[Lisensi Sementara](https://purchase.aspose.com/temporary-license/) untuk mencoba fitur.
### Dapatkah saya memilih lembar kerja tertentu untuk menampilkan pratinjau hentian halaman?  
Ya, Anda bisa! Cukup ubah indeks lembar kerja atau gunakan nama lembar kerja untuk memilih lembar tertentu.
### Apakah Aspose.Cells kompatibel dengan .NET Core?  
Ya, Aspose.Cells kompatibel dengan .NET Framework dan .NET Core, membuatnya serbaguna untuk berbagai aplikasi .NET.
### Bagaimana saya bisa mendapatkan dukungan jika saya mengalami masalah?  
Aspose menyediakan[forum dukungan](https://forum.aspose.com/c/cells/9) di mana Anda bisa mendapatkan bantuan untuk masalah atau pertanyaan apa pun.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
