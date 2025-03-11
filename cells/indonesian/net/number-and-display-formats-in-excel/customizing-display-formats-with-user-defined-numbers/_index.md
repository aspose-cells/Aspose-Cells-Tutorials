---
title: Menyesuaikan Format Tampilan dengan Angka yang Ditentukan Pengguna
linktitle: Menyesuaikan Format Tampilan dengan Angka yang Ditentukan Pengguna
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyesuaikan format tampilan dengan Aspose.Cells untuk .NET. Format tanggal, persentase, dan mata uang menggunakan panduan langkah demi langkah ini.
weight: 11
url: /id/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyesuaikan Format Tampilan dengan Angka yang Ditentukan Pengguna

## Perkenalan
Bekerja dengan file Excel sering kali memerlukan pemformatan sel khusus untuk menyajikan data dengan cara yang lebih bermakna dan mudah digunakan. Bayangkan Anda sedang membuat file Excel untuk sebuah laporan. Anda tidak hanya menginginkan angka mentah. Anda ingin tanggal, persentase, dan mata uang terlihat ramping dan profesional, bukan? Di situlah format tampilan khusus berperan. Dalam tutorial ini, kami akan membahas secara mendalam Aspose.Cells for .NET untuk menunjukkan kepada Anda cara menyesuaikan format tampilan angka menggunakan pengaturan yang ditentukan pengguna.
## Prasyarat
Sebelum memulai, pastikan Anda telah menyiapkan semua yang dibutuhkan untuk mengikuti tutorial ini. Berikut ini yang Anda perlukan:
-  Aspose.Cells untuk .NET terinstal.[Unduh di sini](https://releases.aspose.com/cells/net/).
- Pengetahuan dasar tentang C# dan kerangka kerja .NET.
-  Lisensi yang valid untuk Aspose.Cells. Jika Anda belum memilikinya, dapatkan lisensi[uji coba gratis](https://releases.aspose.com/) atau meminta[lisensi sementara](https://purchase.aspose.com/temporary-license/).
- IDE seperti Visual Studio.
- .NET Framework 4.0 atau lebih tinggi.
 Jika Anda kehilangan sesuatu, jangan khawatir. Anda selalu dapat mengunjungi kembali tautan ini untuk mengunduh file yang diperlukan atau mencari bantuan dari[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9).
## Mengimpor Ruang Nama
Sebelum masuk ke kode, Anda perlu mengimpor namespace yang diperlukan untuk mengakses semua fungsi Aspose.Cells yang diperlukan.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Kedua namespace ini akan menjadi alat inti Anda dalam tutorial ini. Sekarang, mari beralih ke bagian yang menyenangkan:
## Langkah 1: Menyiapkan Direktori Proyek
Pertama, Anda perlu tempat untuk menyimpan file, bukan? Mari buat direktori untuk menyimpan file Excel keluaran. Pada langkah ini, kita juga akan memastikan direktori tersebut ada sebelum menyimpan apa pun.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Kami sedang mendefinisikan`dataDir` variabel untuk menyimpan jalur tempat file Excel keluaran akan disimpan.
-  Kami kemudian memeriksa apakah direktori tersebut ada menggunakan`System.IO.Directory.Exists()`.
-  Jika direktori tidak ada, maka akan dibuat menggunakan`System.IO.Directory.CreateDirectory()`.
## Langkah 2: Buat Buku Kerja Baru dan Tambahkan Lembar Kerja
Sekarang setelah kita memiliki direktori, mari buat buku kerja Excel baru dan tambahkan lembar kerja ke dalamnya.
```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
// Menambahkan lembar kerja baru ke objek Excel
int i = workbook.Worksheets.Add();
// Mendapatkan referensi lembar kerja yang baru ditambahkan dengan meneruskan indeks lembar kerjanya
Worksheet worksheet = workbook.Worksheets[i];
```
-  Pertama, kita membuat yang baru`Workbook` objek. Anggap saja ini sebagai berkas Excel Anda.
-  Kami menambahkan lembar kerja baru ke buku kerja ini menggunakan`Add()`metode dan simpan indeks dalam variabel`i`.
-  Kami merujuk lembar kerja ini menggunakan`workbook.Worksheets[i]`.
## Langkah 3: Menambahkan Tanggal ke Sel dan Menyesuaikan Formatnya
 Sekarang, mari masukkan tanggal saat ini ke dalam sel dan format agar ditampilkan dengan cara khusus. Alih-alih format tanggal default, kita akan menetapkan format khusus seperti`d-mmm-yy`.
```csharp
// Menambahkan tanggal sistem saat ini ke sel "A1"
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Mendapatkan gaya sel A1
Style style = worksheet.Cells["A1"].GetStyle();
// Mengatur format tampilan khusus untuk menampilkan tanggal sebagai "d-mmm-yy"
style.Custom = "d-mmm-yy";
// Menerapkan gaya ke sel A1
worksheet.Cells["A1"].SetStyle(style);
```
-  Kami menambahkan tanggal sistem saat ini ke sel`A1` menggunakan`PutValue(DateTime.Now)`.
-  Kami mengambil gaya sel saat ini`A1` menggunakan`GetStyle()`.
-  Kami mengubah gaya sel dengan mengatur`style.Custom = "d-mmm-yy"`, yang memformat tanggal untuk menampilkan hari, bulan singkat, dan tahun.
-  Terakhir, kami menerapkan gaya baru ke sel dengan`SetStyle()`.
## Langkah 4: Memformat Sel sebagai Persentase
 Selanjutnya, mari kita bekerja dengan angka. Kita akan menambahkan nilai numerik ke sel lain, misalnya`A2`, dan memformatnya sebagai persentase.
```csharp
//Menambahkan nilai numerik ke sel "A2"
worksheet.Cells["A2"].PutValue(20);
// Mendapatkan gaya sel A2
style = worksheet.Cells["A2"].GetStyle();
// Mengatur format tampilan kustom untuk menampilkan nilai sebagai persentase
style.Custom = "0.0%";
// Menerapkan gaya ke sel A2
worksheet.Cells["A2"].SetStyle(style);
```
-  Kami menambahkan nilai`20` ke sel`A2`.
-  Kami mengambil gaya sel`A2` dan atur format khusus ke`0.0%` untuk menampilkan nilai sebagai persentase (misalnya, 20%).
-  Terakhir, kita menerapkan gaya ke sel menggunakan`SetStyle()`.
## Langkah 5: Memformat Sel sebagai Mata Uang
 Mari tambahkan nilai lain, katakanlah ke sel`A3`, dan memformatnya untuk ditampilkan sebagai mata uang. Agar lebih menarik, kami akan menggunakan format yang menampilkan nilai positif sebagai mata uang dalam pound dan nilai negatif dalam dolar.
```csharp
// Menambahkan nilai numerik ke sel "A3"
worksheet.Cells["A3"].PutValue(2546);
// Mendapatkan gaya sel A3
style = worksheet.Cells["A3"].GetStyle();
// Mengatur format tampilan khusus untuk menampilkan nilai sebagai mata uang
style.Custom = "£#,##0;[Red]$-#,##0";
// Menerapkan gaya ke sel A3
worksheet.Cells["A3"].SetStyle(style);
```
-  Kami menambahkan nilai`2546` ke sel`A3`.
-  Kami menetapkan format khusus`£#,##0;[Red]$-#,##0`, yang menampilkan nilai positif dengan tanda pound dan nilai negatif berwarna merah dengan tanda dolar.
- Kami menerapkan gaya ke sel menggunakan`SetStyle()`.
## Langkah 6: Menyimpan Buku Kerja
Langkah terakhir adalah menyimpan buku kerja sebagai file Excel. Kami akan menggunakan format Excel 97-2003 untuk tutorial ini.
```csharp
// Menyimpan file Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  Itu`Save()` metode menyimpan buku kerja dalam direktori yang ditentukan.
-  Kami memilih`SaveFormat.Excel97To2003` untuk memastikan kompatibilitas dengan versi Excel yang lebih lama.
## Kesimpulan
Nah, itu dia! Kita baru saja membuat file Excel, menambahkan format tanggal, persentase, dan mata uang khusus ke sel tertentu menggunakan Aspose.Cells for .NET, dan menyimpan file tersebut. Pemformatan khusus membuat file Excel Anda jauh lebih mudah dibaca dan profesional. Jangan lupa untuk menjelajahi opsi pemformatan lain di Aspose.Cells, seperti pemformatan bersyarat, untuk kontrol yang lebih baik atas tampilan data Anda.
## Pertanyaan yang Sering Diajukan
### Bagaimana saya dapat menerapkan opsi pemformatan yang lebih kompleks di Aspose.Cells?
Anda dapat menggabungkan berbagai gaya pemformatan, seperti warna font, batas, dan warna latar belakang, dengan format angka kustom.
### Dapatkah saya menerapkan format angka khusus ke serangkaian sel?
Ya, Aspose.Cells memungkinkan Anda menerapkan gaya ke rentang sel menggunakan`Range.SetStyle()` metode.
### Format file apa lagi yang dapat saya gunakan untuk menyimpan buku kerja?
 Aspose.Cells mendukung banyak format, termasuk XLSX, CSV, dan PDF. Cukup ubah`SaveFormat` di dalam`Save()` metode.
### Bisakah saya memformat angka negatif secara berbeda?
Tentu saja! Anda dapat menggunakan format angka khusus untuk menampilkan angka negatif dengan warna atau simbol yang berbeda.
### Apakah Aspose.Cells untuk .NET gratis?
 Aspose.Cells menawarkan uji coba gratis, tetapi untuk fungsionalitas penuh, Anda memerlukan lisensi yang valid. Anda bisa mendapatkannya[lisensi sementara di sini](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
