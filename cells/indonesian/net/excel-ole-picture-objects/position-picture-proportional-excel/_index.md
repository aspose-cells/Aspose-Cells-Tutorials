---
"description": "Pelajari cara memosisikan gambar secara proporsional di Excel menggunakan Aspose.Cells untuk .NET. Jadikan lembar kerja Anda lebih menarik secara visual."
"linktitle": "Posisi Gambar (Proporsional) di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Posisi Gambar (Proporsional) di Excel"
"url": "/id/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Posisi Gambar (Proporsional) di Excel

## Bevezetés
Apakah Anda bosan dengan gambar-gambar berpiksel yang tampaknya tidak pernah pas di lembar kerja Excel Anda? Bayangkan ini: Anda memiliki logo cantik yang perlu ditampilkan dengan jelas di lembar Excel Anda, tetapi akhirnya logo tersebut terjepit, melebar, atau tidak pada tempatnya. Tidak seorang pun menginginkannya! Nah, tunggu sebentar karena hari ini Anda akan mempelajari cara memposisikan gambar secara proporsional di Excel menggunakan pustaka Aspose.Cells untuk .NET. Pustaka canggih ini memudahkan Anda untuk memanipulasi file Excel, baik untuk pelaporan, analisis data, atau sekadar mempercantik presentasi Anda. Mari selami seluk-beluk menyelaraskan gambar Anda dengan sempurna!
## Előfeltételek
Sebelum kita masuk ke pengkodean sebenarnya, ada beberapa hal yang perlu Anda siapkan di komputer Anda:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio karena ini akan menyediakan lingkungan yang nyaman untuk proyek .NET Anda.
2. Pustaka Aspose.Cells: Anda memerlukan pustaka Aspose.Cells. Anda dapat memperoleh uji coba gratis atau membelinya dari [Aspose weboldal](https://purchase.aspose.com/buy).
3. Pengetahuan Dasar C#: Sedikit pengetahuan tentang pemrograman C# akan sangat membantu dalam memahami contoh yang akan kita bahas.
4. Berkas Gambar: Siapkan gambar (seperti logo Anda) yang ingin Anda sisipkan ke dalam lembar Excel.
Sekarang semua sudah siap, mari masuk ke pengkodean!
## Csomagok importálása
Untuk mulai menggunakan Aspose.Cells di proyek Anda, Anda perlu mengimpor namespace tertentu. Berikut cara melakukannya:
### Új projekt létrehozása
Di Visual Studio, buat proyek baru:
- Nyisd meg a Visual Studio-t.
- Klik "Buat proyek baru."
- Pilih "Perpustakaan Kelas (.NET Framework)" atau "Aplikasi Konsol", tergantung pada preferensi Anda.
### Az Aspose.Cells telepítése
Anda dapat menambahkan paket Aspose.Cells ke proyek Anda melalui NuGet. Berikut caranya:
- Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
- Válassza a „NuGet-csomagok kezelése” lehetőséget.
- Keresd meg az „Aspose.Cells” fájlt, és kattints a „Telepítés” gombra.
### Hozzáadás direktívák használatával
Di bagian atas berkas kode Anda, sertakan perintah berikut:
```csharp
using System.IO;
using Aspose.Cells;
```
Arahan ini akan memberi Anda akses ke kelas-kelas yang Anda perlukan untuk memanipulasi berkas Excel Anda.
Sekarang, mari kita uraikan ini ke dalam langkah-langkah terperinci untuk berhasil memposisikan gambar secara proporsional di Excel.
## 1. lépés: Állítsa be a címtárát
Pertama-tama, pastikan Anda memiliki folder khusus untuk dokumen Anda. Berikut cara membuat direktori jika belum ada:
```csharp
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Potongan kode ini membuat direktori baru (jika belum ada) untuk menyimpan file Excel Anda. Cukup ganti `"Your Document Directory"` dengan jalur sebenarnya di mana Anda ingin menyimpan berkas Anda.
## Langkah 2: Buat Instansiasi Buku Kerja
Selanjutnya, mari membuat buku kerja baru:
```csharp
Workbook workbook = new Workbook();
```
Baris ini menginisialisasi objek buku kerja baru, memberi Anda kanvas kosong untuk dikerjakan.
## 3. lépés: Új munkalap hozzáadása
Sekarang setelah buku kerja kita disiapkan, mari tambahkan lembar kerja baru ke dalamnya:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Ini akan menambahkan lembar kerja baru dan mengembalikan indeks lembar tersebut, yang dapat kita gunakan untuk memanipulasinya nanti.
## Langkah 4: Akses Lembar Kerja Baru
Untuk memanipulasi lembar kerja yang baru ditambahkan, Anda perlu mengaksesnya:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Jelenleg, `worksheet` akan memungkinkan kita untuk menambahkan konten dan gambar ke lembar spesifik tersebut.
## Langkah 5: Masukkan Gambar
Sekarang tibalah bagian yang menarik! Mari tambahkan gambar cantik Anda. Ganti `"logo.jpg"` dengan nama berkas gambar Anda:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Baris ini menambahkan gambar di sel F6 (karena baris dan kolom diindeks nol, `5` mengacu pada sel keenam).
## Langkah 6: Akses Gambar yang Ditambahkan
Setelah gambar dimasukkan, Anda dapat mengaksesnya seperti ini:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Ini memungkinkan Anda untuk memanipulasi properti gambar.
## Langkah 7: Posisikan Gambar Secara Proporsional
Sekarang, mari kita posisikan gambar secara proporsional:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
Itt, `UpperDeltaX` és `UpperDeltaY` Sesuaikan posisi gambar relatif terhadap dimensi sel. Anda dapat mengubah nilai-nilai ini untuk mendapatkan gambar yang tepat.
## 8. lépés: Mentse el a módosításokat
Terakhir, simpan buku kerja Anda untuk mempertahankan semua perubahan:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Baris ini menyimpan buku kerja Anda sebagai `book1.out.xls` di direktori yang ditunjuk.
## Következtetés
Nah, itu dia! Anda baru saja mempelajari cara memosisikan gambar secara proporsional di Excel menggunakan Aspose.Cells untuk .NET. Ini bukan sekadar menyisipkan gambar; ini tentang membuatnya tampak sempurna di lembar kerja Anda. Ingat saja: gambar yang ditempatkan dengan baik dapat meningkatkan presentasi data Anda secara signifikan.
Bersenang-senanglah bereksperimen dengan berbagai gambar dan penempatan, dan jangan ragu untuk menyelami lebih dalam berbagai fitur yang ditawarkan Aspose.Cells. Lembar Excel Anda akan segera mengalami perubahan besar!
## GYIK
### Mi az Aspose.Cells?
Aspose.Cells adalah pustaka hebat untuk .NET yang memungkinkan pengguna membuat, memanipulasi, dan mengonversi file Excel tanpa perlu menginstal Microsoft Excel.
### Ingyenesen használhatom az Aspose.Cells-t?
Ya, Aspose.Cells menawarkan uji coba gratis, yang dapat Anda unduh [itt](https://releases.aspose.com/).
### Hol találom a dokumentációt?
Anda dapat mengakses komprehensif [dokumentáció](https://reference.aspose.com/cells/net/) untuk Aspose.Cells.
### Apakah Aspose.Cells mendukung semua format gambar?
Aspose.Cells mendukung berbagai format termasuk JPEG, PNG, BMP, GIF, dan TIFF.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
Untuk pertanyaan apa pun, silakan kunjungi [támogató fórum](https://forum.aspose.com/c/cells/9) tempat Anda dapat mengajukan pertanyaan.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}