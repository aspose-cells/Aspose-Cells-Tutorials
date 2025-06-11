---
"description": "Pelajari cara menambahkan kotak daftar ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Ikuti panduan langkah demi langkah kami yang mudah dan buat lembar Excel Anda interaktif."
"linktitle": "Tambahkan Kotak Daftar ke Lembar Kerja di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Tambahkan Kotak Daftar ke Lembar Kerja di Excel"
"url": "/id/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Kotak Daftar ke Lembar Kerja di Excel

## Bevezetés
Menambahkan elemen interaktif ke lembar kerja Excel Anda, seperti kotak daftar, dapat meningkatkan manajemen dan presentasi data secara signifikan. Baik Anda membuat formulir interaktif atau alat entri data kustom, kemampuan untuk mengontrol input pengguna dengan kotak daftar sangatlah berharga. Aspose.Cells untuk .NET menyediakan cara yang efisien untuk menambahkan dan mengelola kontrol ini di file Excel Anda. Dalam panduan ini, kami akan memandu Anda melalui proses menambahkan kotak daftar ke lembar kerja menggunakan Aspose.Cells untuk .NET.
## Előfeltételek
Sebelum menyelami pengkodean, pastikan Anda memiliki alat dan sumber daya berikut:
- Pustaka Aspose.Cells untuk .NET: Anda dapat mengunduhnya dari [Aspose.Cells .NET letöltési oldal](https://releases.aspose.com/cells/net/).
- Lingkungan Pengembangan: Setiap IDE yang mendukung pengembangan .NET, seperti Visual Studio.
- .NET Framework: Pastikan proyek Anda menargetkan versi .NET Framework yang didukung.
Pertimbangkan juga untuk mendapatkan [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) jika Anda ingin menjelajahi semua fitur tanpa batasan.
## Csomagok importálása
Sebelum memulai, pastikan Anda telah mengimpor namespace Aspose.Cells yang diperlukan. Berikut cara melakukannya:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Dalam tutorial ini, kami akan menguraikan proses penambahan kotak daftar menjadi beberapa langkah sederhana. Ikuti setiap langkah dengan saksama untuk memastikan semuanya berjalan sesuai harapan.
## 1. lépés: A dokumentumkönyvtár beállítása
Sebelum Anda membuat file Excel, Anda memerlukan lokasi untuk menyimpannya. Berikut cara mengatur direktori:
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Pada langkah ini, Anda menentukan di mana berkas Anda akan disimpan. Kode tersebut memeriksa apakah direktori tersebut ada, dan jika tidak ada, kode tersebut akan membuatkannya untuk Anda. Ini memastikan bahwa Anda tidak akan mengalami kesalahan "berkas tidak ditemukan" di kemudian hari.
## 2. lépés: Új munkafüzet létrehozása és az első munkalap elérése
Berikutnya, kita akan membuat buku kerja baru dan mengakses lembar kerja pertama tempat kita akan menambahkan kotak daftar.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook workbook = new Workbook();
// Szerezd meg az első munkalapot.
Worksheet sheet = workbook.Worksheets[0];
```
Buku kerja pada dasarnya adalah berkas Excel Anda. Di sini, kita membuat buku kerja baru dan mengakses lembar kerja pertama, yang merupakan tempat kita akan meletakkan kotak daftar. Anggap ini sebagai pembuatan kanvas kosong tempat Anda akan melukis kontrol.
## Langkah 3: Masukkan Data untuk Kotak Daftar
Sebelum kita menambahkan kotak daftar, kita perlu mengisi beberapa data yang akan dirujuk oleh kotak daftar tersebut.
```csharp
// Dapatkan koleksi sel lembar kerja.
Cells cells = sheet.Cells;
// Masukkan nilai untuk label.
cells["B3"].PutValue("Choose Dept:");
// Atur label menjadi tebal.
cells["B3"].GetStyle().Font.IsBold = true;
// Masukkan nilai untuk kotak daftar.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Di sini, kami menambahkan beberapa teks ke dalam lembar kerja. Label "Pilih Dept:" ditempatkan di sel B3, dan fonnya diatur menjadi tebal. Di kolom A, kami memasukkan nilai yang akan berfungsi sebagai rentang input untuk kotak daftar kami, yang mewakili berbagai departemen. Rentang input ini adalah apa yang akan dipilih pengguna saat berinteraksi dengan kotak daftar.
## Langkah 4: Tambahkan Kotak Daftar ke Lembar Kerja
Sekarang setelah kita menyiapkan data, mari tambahkan kontrol kotak daftar itu sendiri.
```csharp
// Tambahkan kotak daftar baru.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Kode ini menambahkan kotak daftar ke lembar kerja. Parameter menentukan posisi dan ukuran kotak daftar. Kotak daftar ditempatkan pada baris 2, kolom 0 dengan lebar 122 dan tinggi 100. Koordinat dan ukuran inilah yang menentukan di mana kotak daftar akan muncul di lembar kerja.
## Langkah 5: Mengatur Properti Kotak Daftar
Berikutnya, kita akan mengatur berbagai properti untuk kotak daftar tersebut agar berfungsi sepenuhnya.
```csharp
// Tetapkan jenis penempatan.
listBox.Placement = PlacementType.FreeFloating;
// Mengatur sel yang ditautkan.
listBox.LinkedCell = "A1";
// Mengatur rentang masukan.
listBox.InputRange = "A2:A7";
// Tetapkan jenis pilihan.
listBox.SelectionType = SelectionType.Single;
// Atur kotak daftar dengan bayangan 3-D.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Properti ini memastikan kotak daftar tetap pada posisinya terlepas dari bagaimana lembar kerja dimodifikasi.
- LinkedCell: Ini menetapkan sel (dalam kasus ini, A1) tempat nilai yang dipilih dari kotak daftar akan ditampilkan.
- InputRange: Ini memberi tahu kotak daftar tempat mencari daftar opsinya (A2 hingga A7, yang telah kita atur sebelumnya).
- SelectionType.Single: Ini membatasi pengguna untuk memilih hanya satu item dari kotak daftar.
- Bayangan: Efek bayangan memberi kotak daftar tampilan yang lebih tiga dimensi, sehingga menarik secara visual.
## 6. lépés: Mentse el az Excel-fájlt
Terakhir, mari simpan buku kerja kita dengan kotak daftar yang disertakan.
```csharp
// Simpan buku kerja.
workbook.Save(dataDir + "book1.out.xls");
```
Baris kode ini menyimpan buku kerja ke direktori yang telah kita buat sebelumnya. File tersebut diberi nama "book1.out.xls", tetapi Anda dapat memilih nama apa pun yang sesuai dengan proyek Anda.
## Következtetés
Nah, itu dia! Anda telah berhasil menambahkan kotak daftar ke lembar kerja Excel menggunakan Aspose.Cells for .NET. Hanya dengan beberapa baris kode, kami telah membuat kotak daftar yang berfungsi penuh, yang membuat lembar kerja lebih interaktif dan dinamis. Tutorial ini akan memberi Anda dasar yang kuat untuk menjelajahi kontrol dan fitur lain di Aspose.Cells for .NET. Teruslah bereksperimen, dan Anda akan segera menguasai fungsionalitas pustaka yang luas!
## GYIK
### Bisakah saya mengizinkan beberapa pilihan dalam kotak daftar?  
Ya, Anda dapat mengubahnya `SelectionType` hogy `SelectionType.Multi` untuk memperbolehkan beberapa pilihan.
### Bisakah saya mengubah tampilan kotak daftar?  
Tentu saja! Aspose.Cells memungkinkan Anda untuk menyesuaikan tampilan kotak daftar, termasuk ukuran, font, dan bahkan warnanya.
### Bagaimana jika saya perlu menghapus kotak daftar tersebut nanti?  
Anda dapat mengakses dan menghapus kotak daftar dari `Shapes` koleksi menggunakan `sheet.Shapes.RemoveAt(index)`.
### Bisakah saya menautkan kotak daftar ke sel yang berbeda?  
Ya, cukup ubah `LinkedCell` properti ke sel lain tempat Anda ingin menampilkan nilai yang dipilih.
### Bagaimana cara menambahkan lebih banyak item ke kotak daftar?  
Cukup perbarui rentang input dengan memasukkan lebih banyak nilai ke dalam sel yang ditentukan, dan kotak daftar akan otomatis diperbarui.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}