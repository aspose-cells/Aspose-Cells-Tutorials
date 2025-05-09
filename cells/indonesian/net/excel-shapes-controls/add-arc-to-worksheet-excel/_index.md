---
"description": "Pelajari cara menambahkan busur ke lembar kerja Excel menggunakan Aspose.Cells for .NET. Ikuti panduan langkah demi langkah kami untuk menyempurnakan desain lembar kerja Anda."
"linktitle": "Menambahkan Arc ke Lembar Kerja di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Menambahkan Arc ke Lembar Kerja di Excel"
"url": "/id/net/excel-shapes-controls/add-arc-to-worksheet-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Arc ke Lembar Kerja di Excel

## Bevezetés
Membuat lembar kerja Excel yang menarik secara visual sangat penting untuk penyajian data, dan pustaka Aspose.Cells menyediakan alat yang tangguh bagi pengembang untuk menyelesaikan tugas ini. Salah satu fitur menarik yang mungkin ingin Anda masukkan ke dalam dokumen Excel adalah kemampuan untuk menambahkan bentuk, seperti busur. Dalam tutorial ini, kami akan memandu langkah demi langkah cara menambahkan busur ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Di akhir artikel ini, Anda tidak hanya akan mempelajari cara menambahkan busur, tetapi juga memperoleh wawasan tentang pengelolaan bentuk secara umum.
## Előfeltételek
Sebelum kita menyelami seluk-beluk penambahan busur ke lembar kerja Anda, penting untuk memastikan Anda memiliki beberapa hal yang diperlukan. Berikut adalah prasyarat yang Anda perlukan untuk memulai:
1. Visual Studio: Anda harus menginstal Visual Studio di komputer Anda karena kita akan menggunakan C# sebagai bahasa pemrograman kita.
2. .NET Framework: Pastikan Anda telah menginstal .NET Framework atau .NET Core. Aspose.Cells mendukung keduanya.
3. Aspose.Cells untuk .NET: Anda harus memiliki pustaka Aspose.Cells. Anda dapat mengunduhnya dari [Aspose.Cells letöltések](https://releases.aspose.com/cells/net/) oldal.
4. Pemahaman Dasar C#: Keakraban dengan C# akan membantu Anda mengikuti potongan kode tanpa banyak kesulitan.
## Csomagok importálása
Untuk mulai bekerja dengan Aspose.Cells di proyek Anda, Anda perlu mengimpor paket yang diperlukan. Berikut cara melakukannya:
### Új projekt létrehozása
- Nyisd meg a Visual Studio-t.
- Pilih "Buat proyek baru."
- Pilih templat yang berfungsi dengan .NET (seperti Aplikasi Konsol).
  
### Aspose.Cells referenciák hozzáadása
- Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
- Válassza a „NuGet-csomagok kezelése” lehetőséget.
- Keresd meg az „Aspose.Cells” fájlt, és telepítsd.
Sekarang Anda siap untuk mulai membuat kode penambahan busur.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Berikut rincian kode langkah demi langkah yang memperagakan cara menambahkan busur ke lembar kerja di Excel.
## Langkah 1: Menyiapkan Direktori
Langkah pertama adalah menyiapkan direktori tempat Anda akan menyimpan berkas Excel. Ini membantu Anda mengelola berkas output dengan mudah.
```csharp
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dalam potongan kode ini, kami menentukan jalur ke direktori dokumen. Kami juga memeriksa apakah direktori tersebut ada; jika tidak, kami membuatnya. Ini menjadi dasar untuk keluaran kami.
## Langkah 2: Buat Instansiasi Buku Kerja
Berikutnya, mari membuat contoh buku kerja baru.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Baris ini membuat buku kerja Excel baru. Anggap ini sebagai kanvas kosong tempat kita dapat menambahkan bentuk, data, dan banyak lagi.
## Langkah 3: Tambahkan Bentuk Busur Pertama
Sekarang, mari tambahkan bentuk busur pertama kita ke lembar kerja.
```csharp
// Tambahkan bentuk busur.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Di sini, kita menambahkan busur ke lembar kerja pertama. Parameter menentukan posisi dan ukuran busur: `(left, top, width, height, startAngle, endAngle)`Ini seperti merencanakan segmen sebuah lingkaran!
## Langkah 4: Kustomisasi Arc Pertama
Setelah menambahkan lengkungan, Anda mungkin ingin menyesuaikan tampilannya.
```csharp
// Mengatur warna bentuk isian
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Mengatur penempatan busur.
arc1.Placement = PlacementType.FreeFloating;           
// Tetapkan ketebalan garis.
arc1.Line.Weight = 1;      
// Mengatur gaya garis putus-putus busur.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Di bagian ini, kita akan menyesuaikan lengkungannya. Kita atur jenis isiannya menjadi warna solid (dalam hal ini biru), tentukan bagaimana lengkungannya ditempatkan, tentukan ketebalan garis, dan pilih gaya garis putus-putus. Pada dasarnya, kita akan mempercantik lengkungan kita agar terlihat menarik!
## Langkah 5: Tambahkan Bentuk Busur Kedua
Mari tambahkan bentuk busur lain untuk memberikan lebih banyak konteks.
```csharp
// Tambahkan bentuk busur lainnya.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Mirip dengan busur pertama, kami menambahkan busur kedua pada lembar kerja yang sama. Koordinat di sini sedikit digeser untuk memposisikannya secara berbeda.
## Langkah 6: Kustomisasi Arc Kedua
Sama seperti yang kita lakukan pada busur pertama, kita akan menyesuaikan busur kedua juga.
```csharp
// Mengatur warna garis
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Mengatur penempatan busur.
arc2.Placement = PlacementType.FreeFloating;          
// Tetapkan ketebalan garis.
arc2.Line.Weight = 1;           
// Mengatur gaya garis putus-putus busur.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Di sini, kami memberikan lengkungan kedua gaya yang sama seperti yang pertama. Anda dapat mengubah warna atau gaya sesuai keinginan untuk tujuan keunikan atau tematik.
## 7. lépés: A munkafüzet mentése
Akhirnya, saatnya untuk menyimpan buku kerja yang baru Anda buat dengan busur.
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
Baris ini berfungsi seperti menekan tombol simpan. Kita menyimpan pekerjaan kita di lokasi yang ditentukan dengan nama berkas yang ditentukan. Pastikan untuk memeriksa direktori Anda untuk melihat karya agung Anda dalam format Excel!
## Következtetés
Dalam tutorial ini, kami telah menjelajahi proses penambahan bentuk lengkung ke lembar kerja Excel menggunakan Aspose.Cells for .NET. Melalui panduan langkah demi langkah yang sederhana, Anda telah mempelajari cara membuat buku kerja baru, menambahkan lengkung, menyesuaikan tampilannya, dan menyimpan dokumen Anda. Kemampuan ini tidak hanya meningkatkan daya tarik visual lembar kerja Anda, tetapi juga membuat presentasi data Anda lebih informatif. Baik Anda membuat bagan, laporan, atau sekadar bereksperimen, penggunaan bentuk seperti lengkung dapat menambahkan sentuhan kreatif pada proyek Anda.
## GYIK
### Mi az Aspose.Cells?
Aspose.Cells adalah pustaka hebat yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel secara terprogram tanpa memerlukan Microsoft Excel.
### Apakah saya perlu menginstal Microsoft Excel untuk menggunakan Aspose.Cells?
Tidak, Aspose.Cells sepenuhnya independen dan tidak memerlukan Microsoft Excel untuk diinstal.
### Kipróbálhatom ingyen az Aspose.Cells-t?
Ya, Anda dapat mencoba Aspose.Cells menggunakan [Ingyenes próbaverzió](https://releases.aspose.com/).
### Milyen programozási nyelveket támogat az Aspose.Cells?
Aspose.Cells mendukung banyak bahasa, termasuk C#, VB.NET, dan banyak lagi.
### Hol kaphatok támogatást az Aspose.Cells-hez?
Anda bisa mendapatkan dukungan melalui [Aspose Fórum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}