---
"description": "Pelajari cara memisahkan baris dan kolom di Excel menggunakan Aspose.Cells for .NET dengan panduan lengkap ini. Sederhanakan manipulasi data Excel Anda."
"linktitle": "Memisahkan Baris dan Kolom di Excel dengan Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Memisahkan Baris dan Kolom di Excel dengan Aspose.Cells"
"url": "/id/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Memisahkan Baris dan Kolom di Excel dengan Aspose.Cells

## Bevezetés
Saat menangani file Excel, Anda mungkin menemukan diri Anda dalam situasi di mana Anda perlu memisahkan baris dan kolom. Baik Anda sedang membersihkan spreadsheet atau memformat ulang data untuk presentasi yang lebih baik, Aspose.Cells untuk .NET adalah alat fantastis yang menyederhanakan proses tersebut. Dalam tutorial ini, saya akan memandu Anda melalui langkah-langkah untuk memisahkan baris dan kolom di Excel menggunakan Aspose.Cells. Pada akhirnya, Anda akan memiliki pemahaman yang kuat tentang cara bekerja dengan file Excel secara terprogram.
## Előfeltételek
Sebelum mulai menggunakan kode, pastikan Anda telah menyiapkan semuanya. Berikut ini yang Anda perlukan:
1. Visual Studio: Anda harus memiliki versi Visual Studio yang berfungsi yang terpasang di komputer Anda. Jika Anda belum memilikinya, Anda dapat mengunduhnya dari [Situs Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells untuk .NET: Anda perlu mengunduh pustaka Aspose.Cells. Anda dapat mengunduhnya dari [Aspose Kiadások oldal](https://releases.aspose.com/cells/net/)Pastikan Anda memiliki lisensi yang diperlukan, yang dapat dibeli atau diperoleh melalui [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
3. Pengetahuan Dasar C#: Pemahaman mendasar tentang pemrograman C# akan membantu Anda mengikutinya dengan lebih mudah.
Setelah semuanya siap, kita dapat masuk ke bagian yang menyenangkan: kode!
## Csomagok importálása
Untuk memulai, Anda perlu mengimpor paket yang diperlukan ke dalam proyek C# Anda. Berikut cara melakukannya:
1. Nyisd meg a projektedet a Visual Studioban.
2. Tambahkan referensi ke pustaka Aspose.Cells. Anda dapat melakukannya dengan mengklik kanan pada Referensi di proyek Anda dan memilih Tambahkan Referensi. Telusuri lokasi tempat Anda menyimpan Aspose.Cells DLL.
3. Di bagian atas file C# Anda, tambahkan perintah penggunaan berikut:
```csharp
using System.IO;
using Aspose.Cells;
```
Sekarang semuanya sudah disiapkan, mari kita ikuti langkah-langkah untuk memisahkan baris dan kolom di lembar Excel Anda. 
## 1. lépés: A dokumentumkönyvtár meghatározása
Pertama, Anda perlu menentukan direktori tempat file Excel Anda berada. Anda dapat mengaturnya sebagai berikut:
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Csere `"Your Document Directory"` dengan jalur sebenarnya di komputer Anda tempat file Excel disimpan. 
## 2. lépés: Fájlfolyam létrehozása
Selanjutnya, Anda perlu membuat aliran file untuk membuka file Excel. Berikut cara melakukannya:
```csharp
// Létrehoz egy fájlfolyamot, amely tartalmazza a megnyitni kívánt Excel-fájlt.
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Di sini, Anda membuka file bernama `book1.xls`Pastikan berkas ini ada di direktori yang Anda tentukan, atau Anda akan mengalami kesalahan berkas tidak ditemukan.
## 3. lépés: Munkafüzet-objektum példányosítása
Sekarang, mari kita muat berkas Excel ke dalam objek Buku Kerja. Ini memungkinkan Anda untuk memanipulasi buku kerja secara terprogram:
```csharp
// Workbook objektum példányosítása
// Az Excel fájl megnyitása a fájlfolyamon keresztül
Workbook workbook = new Workbook(fstream);
```
Dengan baris kode ini, Anda telah berhasil memuat file Excel ke dalam memori dan siap untuk bekerja dengannya.
## 4. lépés: A munkalap elérése
Setelah Anda memiliki buku kerja, langkah berikutnya adalah mengakses lembar kerja tertentu tempat Anda ingin memisahkan baris dan kolom. Berikut cara melakukannya:
```csharp
// Az Excel fájl első munkalapjának elérése
Worksheet worksheet = workbook.Worksheets[0];
```
Dalam kasus ini, kita mengakses lembar kerja pertama. Jika data Anda ada di lembar lain, Anda dapat mengubah indeksnya.
## Langkah 5: Pisahkan Baris
Sekarang tibalah bagian yang menarik! Mari kita pisahkan enam baris pertama (dari baris 0 hingga baris 5). Gunakan kode berikut:
```csharp
// Első hat sor csoportosításának felbontása (0-tól 5-ig)
worksheet.Cells.UngroupRows(0, 5);
```
Metode ini menghapus pengelompokan apa pun yang telah diterapkan pada baris yang ditentukan. Semudah itu!
## Langkah 6: Pisahkan Kolom
Sama seperti baris, Anda juga dapat memisahkan kolom. Berikut cara memisahkan tiga kolom pertama (dari kolom 0 hingga kolom 2):
```csharp
// Első három oszlop csoportosításának felbontása (0-tól 2-ig)
worksheet.Cells.UngroupColumns(0, 2);
```
## 7. lépés: Mentse el a módosított Excel-fájlt
Setelah Anda memisahkan baris dan kolom, langkah selanjutnya adalah menyimpan perubahan kembali ke file Excel. Anda dapat melakukannya dengan menggunakan `Save` metode:
```csharp
// A módosított Excel fájl mentése
workbook.Save(dataDir + "output.xls");
```
Dalam contoh ini, kami menyimpan file yang dimodifikasi sebagai `output.xls`Anda dapat mengubah nama berkas sesuai keinginan Anda.
## 8. lépés: Zárja be a fájlfolyamot
Terakhir, untuk mengosongkan sumber daya, Anda harus menutup aliran file:
```csharp
// A fájlfolyam bezárása az összes erőforrás felszabadításához
fstream.Close();
```
Ini merupakan praktik yang baik untuk memastikan bahwa aplikasi Anda tidak menahan pegangan berkas lebih lama dari yang diperlukan.
## Következtetés
Nah, itu dia! Anda telah berhasil mempelajari cara memisahkan baris dan kolom dalam file Excel menggunakan Aspose.Cells for .NET. Hanya dengan beberapa baris kode, Anda dapat membuat perubahan signifikan pada file Excel secara terprogram. Baik Anda mengotomatiskan laporan atau menyiapkan data untuk analisis, menguasai teknik ini dapat menghemat banyak waktu.
## GYIK
### Mi az Aspose.Cells?
Aspose.Cells adalah pustaka yang hebat untuk bekerja dengan file Excel dalam aplikasi .NET, yang memungkinkan manipulasi, konversi, dan pembuatan lembar kerja dengan mudah.
### Bisakah saya memisahkan baris dan kolom di Excel menggunakan pustaka lain?
Ya, ada pustaka lain yang tersedia untuk manipulasi Excel di .NET, tetapi Aspose.Cells menawarkan fitur yang luas dan kemudahan penggunaan.
### Apakah ada cara untuk membatalkan perubahan setelah menyimpan?
Setelah Anda menyimpan berkas Excel, keadaan sebelumnya tidak dapat dipulihkan kecuali Anda memiliki cadangan berkas asli.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
Anda dapat menemukan dukungan dengan mengunjungi [Forum Dukungan Aspose](https://forum.aspose.com/c/cells/9), tempat Anda dapat mengajukan pertanyaan dan menemukan solusi.
### Használhatom az Aspose.Cells-t licenc nélkül?
Ya, Anda dapat menggunakan Aspose.Cells secara gratis dengan batasan tertentu, dan Anda dapat memulai dengan [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) untuk fungsionalitas penuh.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}