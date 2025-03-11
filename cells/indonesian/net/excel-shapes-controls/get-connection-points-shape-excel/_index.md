---
title: Mendapatkan Titik Koneksi Bentuk di Excel
linktitle: Mendapatkan Titik Koneksi Bentuk di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mendapatkan titik koneksi bentuk di Excel dengan Aspose.Cells untuk .NET. Ikuti panduan langkah demi langkah kami untuk mengekstrak dan menampilkan titik bentuk secara terprogram dengan mudah.
weight: 11
url: /id/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mendapatkan Titik Koneksi Bentuk di Excel

## Perkenalan
Saat bekerja dengan file Excel secara terprogram, kita sering kali perlu berinteraksi dengan bentuk yang tertanam di lembar kerja. Salah satu tugas yang lebih canggih yang dapat Anda lakukan adalah mengekstrak titik koneksi dari suatu bentuk. Titik koneksi digunakan untuk melampirkan bentuk dengan konektor dan mengelola tata letaknya dengan lebih tepat. Jika Anda ingin mendapatkan titik koneksi suatu bentuk di Excel, Aspose.Cells for .NET adalah alat yang Anda butuhkan. Dalam tutorial ini, kami akan memandu Anda melalui proses langkah demi langkah untuk mencapainya.
## Prasyarat
Sebelum menyelami kode, pastikan Anda memiliki prasyarat berikut:
- Aspose.Cells untuk .NET: Anda perlu menginstal Aspose.Cells di lingkungan pengembangan Anda. Jika Anda belum memilikinya, Anda dapat[unduh versi terbaru di sini](https://releases.aspose.com/cells/net/).
- Lingkungan Pengembangan: Pastikan Anda memiliki instalasi Visual Studio atau IDE lain yang kompatibel dengan .NET.
- Pengetahuan Dasar C#: Tutorial ini mengasumsikan bahwa Anda memiliki pemahaman dasar tentang pemrograman C# dan prinsip berorientasi objek.
 Anda juga dapat mendaftar untuk[uji coba gratis Aspose.Cells](https://releases.aspose.com/) Jika Anda belum melakukannya. Ini akan memberi Anda akses ke semua fitur yang diperlukan untuk panduan ini.

## Paket Impor
Untuk bekerja dengan Aspose.Cells dalam proyek Anda, Anda perlu menyertakan namespace yang diperlukan. Pernyataan impor berikut harus ditempatkan di bagian atas kode Anda:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ruang nama ini memberi Anda akses ke fungsionalitas inti Aspose.Cells dan memungkinkan Anda memanipulasi lembar kerja dan bentuk.

## Panduan Langkah demi Langkah untuk Mendapatkan Titik Koneksi Bentuk
Di bagian ini, kami akan memandu Anda untuk mengekstrak titik koneksi suatu bentuk dalam lembar kerja Excel. Ikuti setiap langkah dengan saksama agar Anda memperoleh pemahaman yang jelas.
## Langkah 1: Buat Buku Kerja Baru
 Hal pertama yang harus dilakukan adalah membuat instance dari`Workbook` class. Ini merupakan file Excel di Aspose.Cells. Jika Anda tidak memiliki file tersebut, tidak masalah—Anda dapat memulai dengan buku kerja kosong.
```csharp
// Membuat Buku Kerja baru
Workbook workbook = new Workbook();
```
 Pada langkah ini, kami telah membuat buku kerja Excel kosong, tetapi Anda juga dapat memuat buku kerja yang sudah ada dengan meneruskan jalur file ke`Workbook` konstruktor.
## Langkah 2: Akses Lembar Kerja Pertama
Selanjutnya, kita perlu mengakses lembar kerja tempat kita ingin bekerja dengan bentuk. Dalam kasus ini, kita akan menggunakan lembar kerja pertama dari buku kerja.
```csharp
// Dapatkan lembar kerja pertama di buku kerja
Worksheet worksheet = workbook.Worksheets[0];
```
 Baris ini mengakses lembar kerja pertama dari kumpulan lembar kerja dalam buku kerja. Jika Anda bekerja dengan lembar tertentu, Anda dapat mengganti indeks`0` dengan indeks yang diinginkan.
## Langkah 3: Tambahkan Kotak Teks Baru (Bentuk)
Sekarang, mari tambahkan bentuk baru ke lembar kerja. Kita akan membuat kotak teks, yang merupakan jenis bentuk. Anda juga dapat menambahkan jenis bentuk lainnya, tetapi demi kesederhanaan, kita akan tetap menggunakan kotak teks dalam tutorial ini.
```csharp
// Tambahkan kotak teks baru ke koleksi
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Inilah yang telah kami lakukan:
-  Menambahkan kotak teks di baris`2` , kolom`1`.
-  Atur dimensi kotak teks ke`160` satuan lebar dan`200` satuan tinggi.
## Langkah 4: Akses Bentuk dari Koleksi Bentuk
 Setelah kita menambahkan kotak teks, kotak teks tersebut menjadi bagian dari koleksi bentuk lembar kerja. Sekarang kita akan mengakses bentuk tersebut menggunakan`Shapes`koleksi.
```csharp
// Akses bentuk (kotak teks) dari koleksi bentuk
Shape shape = workbook.Worksheets[0].Shapes[0];
```
Pada langkah ini, kita mengambil bentuk pertama (kotak teks kita) dari koleksi. Jika Anda memiliki beberapa bentuk, Anda dapat menentukan indeks atau bahkan menemukan bentuk tersebut berdasarkan nama.
## Langkah 5: Ambil Titik Koneksi
Sekarang setelah kita memiliki bentuk, mari kita ekstrak titik-titik koneksinya. Titik-titik ini digunakan untuk memasang konektor ke bentuk.`ConnectionPoints` properti bentuk mengembalikan semua titik koneksi yang tersedia.
```csharp
// Dapatkan semua titik koneksi dalam bentuk ini
var connectionPoints = shape.ConnectionPoints;
```
Ini memberi kita kumpulan semua titik koneksi yang tersedia untuk bentuk itu.
## Langkah 6: Menampilkan Titik Koneksi
Terakhir, kami ingin menampilkan koordinat setiap titik koneksi. Di sinilah kami mengulang titik koneksi dan mencetaknya ke konsol.
```csharp
// Menampilkan semua titik bentuk
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Loop ini mengulangi setiap titik koneksi dan mencetak`X` Dan`Y` koordinat. Ini dapat berguna untuk men-debug atau mengonfirmasi secara visual titik koneksi suatu bentuk.
## Langkah 7: Jalankan dan Selesaikan
Setelah Anda menyiapkan semua langkah di atas, Anda dapat menjalankan kodenya. Berikut baris terakhir yang memastikan proses berhasil diselesaikan:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Baris ini hanya mencatat pesan ke konsol yang menunjukkan bahwa proses telah selesai.

## Kesimpulan
Dalam tutorial ini, kami membahas cara mengambil titik koneksi suatu bentuk di Excel menggunakan Aspose.Cells for .NET. Dengan membagi tugas menjadi langkah-langkah kecil yang mudah dipahami, kami mengeksplorasi proses pembuatan buku kerja, menambahkan bentuk, dan mengekstrak titik koneksi.
Dengan memahami cara memanipulasi bentuk secara terprogram, Anda membuka kemungkinan untuk membuat lembar Excel yang dinamis dan interaktif. Baik Anda membuat laporan, mendesain dasbor, atau membuat diagram, pengetahuan ini akan berguna.
## Pertanyaan yang Sering Diajukan
### Apa yang dimaksud dengan titik koneksi dalam suatu bentuk?
Titik koneksi adalah titik tertentu pada suatu bentuk tempat Anda dapat memasang konektor atau menautkannya ke bentuk lain.
### Bisakah saya mengambil titik koneksi untuk semua bentuk di lembar kerja?
Ya, Aspose.Cells memungkinkan Anda mengambil titik koneksi untuk bentuk apa pun yang mendukungnya. Cukup lakukan pengulangan melalui koleksi bentuk di lembar kerja.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?
Ya, meskipun Anda dapat mencobanya secara gratis, lisensi diperlukan untuk mendapatkan fitur lengkap. Anda dapat[beli lisensi di sini](https://purchase.aspose.com/buy)atau dapatkan[lisensi sementara](https://purchase.aspose.com/temporary-license/).
### Bagaimana cara menambahkan berbagai jenis bentuk di Aspose.Cells?
Anda dapat menggunakan`Add` metode untuk bentuk seperti persegi panjang, elips, dan lainnya. Setiap bentuk memiliki parameter khusus yang dapat Anda sesuaikan.
### Bagaimana cara memuat berkas Excel yang sudah ada alih-alih membuat yang baru?
 Untuk memuat file yang sudah ada, berikan jalur file ke`Workbook` konstruktor, seperti ini:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
