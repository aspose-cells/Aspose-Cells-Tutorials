---
"description": "Pelajari cara menambahkan kotak grup dan tombol radio di Excel menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah untuk pengembang dari semua tingkatan."
"linktitle": "Tambahkan Kotak Grup ke Lembar Kerja di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Tambahkan Kotak Grup ke Lembar Kerja di Excel"
"url": "/id/net/excel-shapes-controls/add-group-box-to-worksheet-excel/"
"weight": 24
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Kotak Grup ke Lembar Kerja di Excel

## Bevezetés
Dalam hal penyajian data, Excel adalah rajanya. Menambahkan elemen interaktif seperti kotak grup dapat membuat lembar kerja Anda lebih menarik dan mudah digunakan. Hari ini, kita akan menyelami dunia Aspose.Cells untuk .NET, pustaka canggih yang membantu Anda memanipulasi lembar kerja Excel dengan mudah. Namun, jangan khawatir jika Anda bukan ahli dalam pengkodean—panduan ini akan menguraikan semuanya menjadi langkah-langkah sederhana. Apakah Anda siap untuk meningkatkan keterampilan Excel Anda? Mari kita mulai!
## Előfeltételek
Sebelum kita masuk ke kode, ada beberapa hal yang Anda perlukan:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda; di sanalah Anda akan menulis kode .NET.
2. Aspose.Cells untuk .NET: Anda perlu mengunduh pustaka ini. Anda dapat menemukannya [itt](https://releases.aspose.com/cells/net/). 
3. Pengetahuan Dasar C#: Meskipun saya akan menjelaskan semuanya langkah demi langkah, sedikit pemahaman tentang C# akan membantu Anda mengikutinya.
## Csomagok importálása
Untuk proyek apa pun, Anda harus mengimpor paket yang diperlukan terlebih dahulu. Di sini, Aspose.Cells akan menjadi fokus utama Anda. Berikut cara melakukannya:
## Langkah 1: Buka Proyek Anda di Visual Studio
Luncurkan Visual Studio dan buka proyek Anda yang sudah ada atau buat yang baru. 
## Langkah 2: Tambahkan Referensi ke Aspose.Cells
- Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
- Válassza a „NuGet-csomagok kezelése” lehetőséget.
- Cari "Aspose.Cells" dan instal. Ini akan memungkinkan Anda untuk menggunakan semua kelas dan metode yang disediakan oleh pustaka Aspose.Cells.
## Langkah 3: Sertakan Menggunakan Arahan
Di bagian atas file C# Anda, sertakan namespace Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ini memberi Anda akses ke kelas-kelas yang diperlukan untuk bekerja dengan berkas Excel.
Setelah semuanya siap, mari kita bahas inti tutorialnya—menambahkan kotak grup dengan tombol radio ke lembar kerja Excel. Kita akan membagi proses ini menjadi beberapa langkah agar lebih jelas.
## Langkah 1: Siapkan Direktori Dokumen Anda
Sebelum membuat berkas Excel, Anda perlu menentukan lokasi penyimpanannya. Mari buat direktori jika belum ada.
```csharp
// A dokumentumok könyvtárának elérési útja
string dataDir = "Your Document Directory"; // Tentukan jalur yang Anda inginkan
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Kode ini memeriksa apakah direktori tempat file Excel akan disimpan ada. Jika tidak, kode ini akan membuat direktori—ini seperti menyiapkan ruang kerja sebelum memulai proyek!
## Langkah 2: Buat Buku Kerja Baru
Berikutnya, Anda perlu membuat buku kerja Excel tempat Anda akan menambahkan kotak grup.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Baris ini menginisialisasi contoh baru Buku Kerja. Anggap saja ini seperti membuka file Excel kosong yang siap dimodifikasi.
## Langkah 3: Tambahkan Kotak Grup
Sekarang, mari kita tambahkan kotak grup itu. 
```csharp
// Tambahkan kotak grup ke lembar kerja pertama.
GroupBox box = excelbook.Worksheets[0].Shapes.AddGroupBox(1, 0, 1, 0, 300, 250);
```
Di sini, Anda menambahkan kotak grup pada koordinat yang ditentukan di lembar kerja pertama. Parameter menentukan posisi dan ukuran kotak, seperti halnya menempatkan furnitur di dalam ruangan!
## Langkah 4: Mengatur Judul Kotak Grup
Sekarang, beri judul pada kotak grup Anda!
```csharp
// Tetapkan judul kotak grup.
box.Text = "Age Groups";
box.Placement = PlacementType.FreeFloating;
```
String “Kelompok Usia” mengatur label yang muncul pada kotak grup. Mengatur `Placement` sebagai `FreeFloating` memungkinkan kotak tersebut dapat dipindahkan—fleksibilitas adalah kuncinya!
## Langkah 5: Buat Kotak Grup 2-D
Meskipun 3D mungkin terdengar mewah, kami akan menampilkan tampilan klasik di sini.
```csharp
// Jadikan menjadi kotak 2-D.
box.Shadow = false;
```
Kode ini menghilangkan efek bayangan, sehingga kotak tampak datar—seperti selembar kertas sederhana!
## Langkah 6: Tambahkan Tombol Radio
Mari bumbui dengan menambahkan beberapa tombol radio untuk masukan pengguna.
## Langkah 6.1: Tambahkan Tombol Radio Pertama
```csharp
// Tambahkan tombol radio.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
// Tetapkan string teksnya.
radio1.Text = "20-29";
// Tetapkan sel A1 sebagai sel yang ditautkan untuk tombol radio.
radio1.LinkedCell = "A1";
```
Anda membuat tombol radio untuk kelompok usia 20-29 tahun, menautkannya ke sel A1 di lembar kerja. Ini berarti saat tombol ini dipilih, sel A1 mencerminkan pilihan tersebut!
## Langkah 6.2: Kustomisasi Tombol Radio Pertama
Sekarang mari kita beri sedikit gaya.
```csharp
// Jadikan tombol radio 3-D.
radio1.Shadow = true;
// Tetapkan bobot tombol radio.
radio1.Line.Weight = 4;
// Mengatur gaya tanda hubung tombol radio.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Dengan menambahkan bayangan dan menyesuaikan gaya garis, kita meningkatkan visibilitas tombol. Ini seperti menambahkan dekorasi agar tombol menonjol dari halaman!
## Langkah 6.3: Ulangi untuk Tombol Radio Lainnya
Ulangi proses ini untuk kelompok usia tambahan:
```csharp
// Tombol Radio Kedua
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
radio2.Text = "30-39";
radio2.LinkedCell = "A1";
radio2.Shadow = true;
radio2.Line.Weight = 4;
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
// Tombol Radio Ketiga
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
radio3.Text = "40-49";
radio3.LinkedCell = "A1";
radio3.Shadow = true;
radio3.Line.Weight = 4;
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
Setiap tombol radio berfungsi sebagai pilihan untuk rentang usia yang berbeda, yang terhubung kembali ke sel A1 yang sama. Hal ini memungkinkan proses pemilihan yang sederhana dan mudah digunakan.
## Langkah 7: Kelompokkan Bentuknya
Setelah semuanya pada tempatnya, mari rapikan semuanya dengan mengelompokkan bentuk kita. 
```csharp
// Dapatkan bentuknya.
Aspose.Cells.Drawing.Shape[] shapeobjects = new Shape[] { box, radio1, radio2, radio3 };
// Kelompokkan bentuknya.
Aspose.Cells.Drawing.GroupShape group = excelbook.Worksheets[0].Shapes.Group(shapeobjects);
```
Langkah ini menggabungkan semuanya menjadi satu kesatuan yang kohesif. Mirip seperti membingkai koleksi seni Anda—ini menyatukan semuanya dengan indah!
## Langkah 8: Simpan File Excel
Terakhir, mari selamatkan karya agung kita!
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
Baris kode ini menuliskan perubahan Anda ke file Excel baru bernama "book1.out.xls" di direktori yang Anda tentukan. Seperti menyegel amplop, pekerjaan Anda sekarang tersimpan dengan aman!
## Következtetés
Dan itu dia—panduan lengkap untuk menambahkan kotak grup dan tombol radio ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET! Dengan setiap langkah, Anda telah mempelajari cara memanipulasi Excel secara terprogram, membuka pintu ke kemungkinan tak terbatas untuk menyesuaikan laporan, visualisasi data, dan banyak lagi. Keindahan pemrograman adalah Anda dapat mengotomatiskan tugas dan membuat antarmuka yang ramah pengguna dengan relatif mudah—bayangkan potensinya!
## GYIK
### Mi az Aspose.Cells?
Aspose.Cells adalah pustaka .NET untuk mengelola file Excel, mengaktifkan tugas seperti membaca, menulis, dan memanipulasi lembar kerja secara terprogram.
### Apakah saya perlu pengalaman coding untuk menggunakan Aspose.Cells?
Meskipun beberapa pengetahuan coding akan membantu, tutorial ini akan memandu Anda melalui dasar-dasarnya, sehingga dapat diakses oleh pemula!
### Dapatkah saya menyesuaikan tampilan kotak dan tombol grup?
Tentu saja! Aspose.Cells menyediakan berbagai pilihan untuk menata bentuk, termasuk warna, ukuran, dan efek 3D.
### Van ingyenes próbaverzió az Aspose.Cells-hez?
Ya! Anda dapat mencobanya secara gratis dengan mengunjungi [Aspose ingyenes próbaverzió](https://releases.aspose.com/).
### Hol találok további forrásokat vagy támogatást az Aspose.Cells-hez?
A [Aspose Támogatási Fórum](https://forum.aspose.com/c/cells/9) adalah tempat yang sangat baik untuk mencari bantuan dan berbagi pengetahuan dengan masyarakat.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}