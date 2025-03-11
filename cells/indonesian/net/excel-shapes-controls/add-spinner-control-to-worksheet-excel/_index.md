---
title: Tambahkan Kontrol Pemutar ke Lembar Kerja di Excel
linktitle: Tambahkan Kontrol Pemutar ke Lembar Kerja di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menambahkan kontrol Spinner ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET dalam tutorial langkah demi langkah ini.
weight: 23
url: /id/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Kontrol Pemutar ke Lembar Kerja di Excel

## Perkenalan
Jika Anda mendalami dunia otomatisasi Excel menggunakan .NET, Anda mungkin menemukan kebutuhan akan kontrol yang lebih interaktif dalam lembar kerja Anda. Salah satu kontrol tersebut adalah Spinner, yang memungkinkan pengguna untuk menambah atau mengurangi nilai dengan mudah. Dalam tutorial ini, kita akan menjelajahi cara menambahkan kontrol Spinner ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Kita akan menguraikannya menjadi beberapa langkah yang mudah dipahami sehingga Anda dapat mengikutinya dengan lancar. 
## Prasyarat
Sebelum kita masuk ke kode, mari pastikan Anda telah menyiapkan semuanya agar pengalaman Anda lancar:
1.  Aspose.Cells untuk .NET: Pastikan Anda memiliki pustaka Aspose.Cells. Jika Anda belum menginstalnya, Anda dapat mengunduh versi terbaru dari[tautan unduhan](https://releases.aspose.com/cells/net/).
2. Visual Studio: Anda harus memiliki instalasi Visual Studio atau IDE .NET lain yang Anda sukai.
3. Pengetahuan Dasar tentang C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan mudah. Jika Anda baru memulai, jangan khawatir! Saya akan memandu Anda melalui setiap bagian.
## Paket Impor
Untuk menggunakan Aspose.Cells di proyek Anda, Anda perlu mengimpor namespace yang diperlukan. Berikut cara menyiapkan lingkungan Anda:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ruang nama ini memungkinkan Anda mengakses fungsionalitas inti Aspose.Cells, termasuk manipulasi buku kerja dan kemampuan menggambar bentuk seperti Spinner.
Setelah kita membahas prasyarat dan mengimpor paket yang diperlukan, mari kita mulai panduan langkah demi langkah. Setiap langkah dirancang agar jelas dan ringkas sehingga Anda dapat menerapkannya dengan mudah.
## Langkah 1: Siapkan Direktori Proyek Anda
Sebelum Anda mulai membuat kode, ada baiknya Anda mengatur berkas-berkas Anda. Mari kita buat direktori untuk berkas-berkas Excel kita.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Di sini, kami menentukan jalur untuk direktori dokumen kami. Jika direktori tersebut tidak ada, kami membuatnya. Ini memastikan bahwa semua file yang kami hasilkan memiliki lokasi yang ditentukan.
## Langkah 2: Buat Buku Kerja Baru
Sekarang saatnya membuat buku kerja Excel tempat kita akan menambahkan kontrol Spinner.
```csharp
// Buat Buku Kerja baru.
Workbook excelbook = new Workbook();
```
 Itu`Workbook` class merupakan file Excel. Dengan membuatnya, kita membuat buku kerja baru yang siap untuk dimodifikasi.
## Langkah 3: Akses Lembar Kerja Pertama
Kita akan menambahkan Spinner ke lembar kerja pertama dalam buku kerja.
```csharp
// Dapatkan lembar kerja pertama.
Worksheet worksheet = excelbook.Worksheets[0];
```
Baris ini mengakses lembar kerja pertama (indeks 0) dari buku kerja kita. Anda dapat memiliki beberapa lembar kerja, tetapi untuk contoh ini, kita akan membuatnya tetap sederhana.
## Langkah 4: Bekerja dengan Sel
Selanjutnya, mari kita bekerja dengan sel-sel di lembar kerja kita. Kita akan menetapkan beberapa nilai dan gaya.
```csharp
// Dapatkan sel lembar kerja.
Cells cells = worksheet.Cells;
// Masukkan nilai string ke dalam sel A1.
cells["A1"].PutValue("Select Value:");
// Mengatur warna font sel.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Mengatur teks font menjadi tebal.
cells["A1"].GetStyle().Font.IsBold = true;
// Masukkan nilai ke sel A2.
cells["A2"].PutValue(0);
```
Di sini, kita mengisi sel A1 dengan perintah, menerapkan warna merah, dan menebalkan teks. Kita juga menetapkan sel A2 ke nilai awal 0, yang akan ditautkan ke Spinner kita.
## Langkah 5: Gaya Sel A2
Berikutnya, mari terapkan beberapa gaya ke sel A2 untuk membuatnya lebih menarik secara visual.
```csharp
// Atur warna bayangan menjadi hitam dengan latar belakang solid.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Mengatur warna font sel.
cells["A2"].GetStyle().Font.Color = Color.White;
// Mengatur teks font menjadi tebal.
cells["A2"].GetStyle().Font.IsBold = true;
```
Kami menambahkan latar belakang hitam dengan pola solid ke sel A2 dan mengatur warna font menjadi putih. Kontras ini akan membuatnya menonjol di lembar kerja.
## Langkah 6: Tambahkan Kontrol Pemintal
Sekarang, kita siap menambahkan kontrol Spinner ke lembar kerja kita.
```csharp
// Tambahkan kontrol pemutar.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Baris ini menambahkan kontrol Spinner ke lembar kerja. Parameter menentukan posisi dan ukuran Spinner (baris, kolom, lebar, tinggi).
## Langkah 7: Konfigurasikan Properti Spinner
Mari sesuaikan perilaku Spinner agar sesuai dengan kebutuhan kita.
```csharp
// Mengatur jenis penempatan pemutar.
spinner.Placement = PlacementType.FreeFloating;
// Tetapkan sel yang ditautkan untuk kontrol.
spinner.LinkedCell = "A2";
// Tetapkan nilai maksimum.
spinner.Max = 10;
//Tetapkan nilai minimum.
spinner.Min = 0;
// Tetapkan perubahan kenaikan untuk kontrol.
spinner.IncrementalChange = 2;
// Atur ke bayangan 3-D.
spinner.Shadow = true;
```
Di sini, kami menetapkan properti Spinner. Kami menautkannya ke sel A2, yang memungkinkannya mengontrol nilai yang ditampilkan di sana. Nilai minimum dan maksimum menentukan rentang yang dapat digunakan Spinner, sementara perubahan inkremental menetapkan seberapa banyak nilai berubah dengan setiap klik. Menambahkan bayangan 3-D memberikan tampilan yang halus.
## Langkah 8: Simpan File Excel
Terakhir, mari simpan buku kerja Excel kita dengan Spinner yang disertakan.
```csharp
// Simpan berkas excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Perintah ini menyimpan buku kerja ke direktori yang ditentukan. Anda dapat mengubah nama berkas sesuai kebutuhan.
## Kesimpulan
Nah, itu dia! Anda telah berhasil menambahkan kontrol Spinner ke lembar kerja Excel menggunakan Aspose.Cells for .NET. Elemen interaktif ini meningkatkan pengalaman pengguna dengan memungkinkan penyesuaian cepat pada nilai. Baik Anda membuat alat pelaporan dinamis atau formulir entri data, kontrol Spinner dapat menjadi tambahan yang berharga. 
## Pertanyaan yang Sering Diajukan
### Apa itu kontrol Spinner di Excel?
Kontrol Spinner memungkinkan pengguna untuk menambah atau mengurangi nilai numerik dengan mudah, menyediakan cara intuitif untuk membuat pilihan.
### Bisakah saya menyesuaikan tampilan Spinner?
Ya, Anda dapat mengubah ukuran, posisi, dan bahkan bayangan 3-D untuk tampilan yang lebih halus.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?
 Aspose.Cells menawarkan uji coba gratis, tetapi lisensi berbayar diperlukan untuk penggunaan produksi. Lihat[opsi pembelian](https://purchase.aspose.com/buy).
### Bagaimana saya bisa mendapatkan bantuan dengan Aspose.Cells?
 Untuk dukungan, kunjungi[Forum Aspose](https://forum.aspose.com/c/cells/9) tempat Anda dapat mengajukan pertanyaan dan mendapatkan jawaban.
### Apakah mungkin untuk menambahkan beberapa Spinner ke lembar kerja yang sama?
Tentu saja! Anda dapat menambahkan Spinner sebanyak yang dibutuhkan dengan mengikuti langkah yang sama untuk setiap kontrol.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
