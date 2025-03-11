---
title: Tambahkan Oval ke Lembar Kerja di Excel
linktitle: Tambahkan Oval ke Lembar Kerja di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menambahkan oval ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah dengan penjelasan kode terperinci.
weight: 17
url: /id/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Oval ke Lembar Kerja di Excel

## Perkenalan
Membuat file Excel yang memukau dan interaktif dapat melibatkan lebih dari sekadar angka dan rumus. Bentuk seperti oval dapat menambah daya tarik visual atau menyediakan elemen fungsional di lembar kerja Anda. Dalam tutorial ini, kita akan menjelajahi cara menggunakan Aspose.Cells for .NET untuk menambahkan oval ke lembar kerja Excel secara terprogram. Baik Anda ingin menambahkan sedikit gaya atau fungsionalitas, kami menyediakan panduan langkah demi langkah yang menguraikan semuanya.
## Prasyarat
Sebelum menyelami kode, ada beberapa hal yang perlu Anda siapkan:
1.  Pustaka Aspose.Cells untuk .NET: Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/cells/net/) atau menginstalnya menggunakan NuGet di Visual Studio.
2. Lingkungan Pengembangan: AC# IDE seperti Visual Studio.
3. Pemahaman Dasar C#: Anda harus terbiasa dengan konsep dasar pengkodean dalam C#.
 Selain itu, ingatlah untuk menyiapkan proyek Anda dengan menginstal pustaka Aspose.Cells for .NET. Jika Anda belum memiliki lisensi, Anda dapat mengajukan permohonan[lisensi sementara](https://purchase.aspose.com/temporary-license/) atau gunakan[uji coba gratis](https://releases.aspose.com/) versi.
## Paket Impor
Sebelum menulis kode apa pun, pastikan Anda telah menyertakan namespace yang diperlukan. Berikut cuplikan kode C# untuk memastikan Anda menggunakan pustaka yang tepat:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Langkah 1: Siapkan Direktori Anda
Langkah pertama dalam menambahkan oval ke lembar Excel adalah menentukan tempat penyimpanan file Excel Anda. Mari tentukan jalur direktori dan pastikan direktori tersebut ada sebelum menyimpan pekerjaan kita.

Kita akan membuat jalur direktori dan memverifikasi apakah jalur tersebut ada. Jika folder tersebut tidak ada, maka folder tersebut akan dibuat.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Langkah ini penting karena memastikan berkas Anda disimpan di lokasi yang tepat, dan Anda tidak mengalami masalah jalur berkas di kemudian hari.
## Langkah 2: Inisialisasi Buku Kerja Baru
Selanjutnya, kita perlu membuat buku kerja baru yang akan kita gunakan untuk menambahkan bentuk oval. Buku kerja tersebut merupakan berkas Excel, dan kita dapat menambahkan konten atau bentuk ke dalamnya.

 Pada langkah ini, kita membuat instance baru`Workbook` objek yang akan berfungsi sebagai wadah berkas Excel kita.
```csharp
// Buat Buku Kerja baru.
Workbook excelbook = new Workbook();
```
## Langkah 3: Tambahkan Bentuk Oval Pertama
Sekarang tibalah bagian yang menyenangkan—menambahkan bentuk oval ke lembar kerja. Bentuk oval ini dapat mewakili elemen visual seperti tombol atau sorotan. Kita akan mulai dengan menambahkan bentuk oval pertama ke lembar kerja pertama buku kerja kita.

 Di sini, kami menggunakan`Shapes.AddOval()` metode untuk membuat oval pada lembar kerja pada baris dan kolom tertentu.
```csharp
// Tambahkan bentuk oval.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
 Parameter di dalam`AddOval()` adalah sebagai berikut:
- Dua angka pertama mewakili baris dan kolom untuk sudut kiri atas oval.
- Dua angka berikutnya mewakili tinggi dan lebar oval.
## Langkah 4: Atur Penempatan dan Gaya Oval
 Setelah oval dibuat, kita dapat mengatur posisinya, ketebalan garis, dan gaya garis putus-putus.`Placement` Properti menentukan bagaimana oval berperilaku saat Anda mengubah ukuran atau memindahkan sel di lembar kerja.

Kita buat oval mengambang bebas dan menyesuaikan penampilannya.
```csharp
// Mengatur penempatan oval.
oval1.Placement = PlacementType.FreeFloating;
// Tetapkan ketebalan garis.
oval1.Line.Weight = 1;
// Mengatur gaya garis putus-putus oval.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ini memungkinkan oval bergerak bebas dalam lembar kerja, dan ketebalan garis serta gayanya diatur untuk konsistensi visual.
## Langkah 5: Tambahkan Bentuk Oval (Lingkaran) Lainnya
Mengapa berhenti di satu? Pada langkah ini, kita akan menambahkan bentuk oval lain, kali ini membuat lingkaran sempurna dengan menyamakan tinggi dan lebarnya.

Kita membuat oval lain, meletakkannya di lokasi berbeda, dan memastikan bentuknya melingkar dengan mengatur tinggi dan lebar yang sama.
```csharp
// Tambahkan bentuk oval (lingkaran) lainnya.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Langkah 6: Tata Rambut Oval Kedua
Sama seperti sebelumnya, kita akan menyesuaikan penempatan, bobot, dan gaya garis oval (atau lingkaran) kedua ini.

Kami menerapkan properti serupa pada oval kedua agar sesuai dengan gaya oval pertama.
```csharp
// Mengatur penempatan oval.
oval2.Placement = PlacementType.FreeFloating;
// Tetapkan ketebalan garis.
oval2.Line.Weight = 1;
// Mengatur gaya garis putus-putus oval.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Langkah 7: Simpan Buku Kerja
Terakhir, kita perlu menyimpan buku kerja dengan oval yang baru saja kita tambahkan. Menyimpan file memastikan bahwa semua perubahan kita tersimpan.

Kami menyimpan buku kerja ke jalur direktori yang telah kami tentukan sebelumnya.
```csharp
// Simpan berkas excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Selesai! Anda telah berhasil menambahkan oval ke lembar kerja Excel dan menyimpan berkasnya.
## Kesimpulan
Menambahkan bentuk seperti oval ke lembar Excel menggunakan Aspose.Cells for .NET tidak hanya mudah, tetapi juga merupakan cara yang menyenangkan untuk menyempurnakan lembar kerja Anda dengan elemen visual tambahan. Baik untuk tujuan desain atau menambahkan elemen yang dapat diklik, bentuk dapat memainkan peran penting dalam tampilan dan fungsi file Excel Anda. Jadi, lain kali Anda mengerjakan proyek yang memerlukan lembar Excel yang interaktif atau menarik secara visual, Anda tahu persis cara menambahkan oval yang sempurna itu!
## Pertanyaan yang Sering Diajukan
### Bisakah saya menambahkan bentuk lain seperti persegi panjang atau garis menggunakan Aspose.Cells untuk .NET?
 Ya, Anda dapat menambahkan berbagai bentuk seperti persegi panjang, garis, dan panah menggunakan`Shapes` koleksi di Aspose.Cells.
### Apakah mungkin untuk mengubah ukuran oval setelah menambahkannya?
Tentu saja! Anda dapat mengubah properti tinggi dan lebar oval setelah menambahkannya.
### Dalam format file apa saya dapat menyimpan buku kerja selain XLS?
Aspose.Cells mendukung berbagai format seperti XLSX, CSV, dan PDF, antara lain.
### Bisakah saya mengubah warna garis luar oval?
 Ya, Anda dapat mengubah warna garis oval menggunakan`Line.Color` milik.
### Apakah perlu memiliki lisensi untuk Aspose.Cells?
 Meskipun Anda dapat mencoba Aspose.Cells dengan uji coba gratis, Anda memerlukan[lisensi](https://purchase.aspose.com/buy) untuk penggunaan jangka panjang atau untuk mengakses fitur-fitur lanjutan.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
