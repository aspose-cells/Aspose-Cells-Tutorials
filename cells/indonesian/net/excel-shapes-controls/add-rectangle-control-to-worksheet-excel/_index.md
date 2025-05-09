---
"description": "Pelajari cara menambahkan kontrol persegi panjang ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah yang terperinci."
"linktitle": "Tambahkan Kontrol Persegi Panjang ke Lembar Kerja di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Tambahkan Kontrol Persegi Panjang ke Lembar Kerja di Excel"
"url": "/id/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Kontrol Persegi Panjang ke Lembar Kerja di Excel

## Bevezetés
Jika berbicara tentang mengotomatiskan tugas Excel, Aspose.Cells for .NET adalah alat yang hebat yang dapat membantu Anda mencapai berbagai tujuan, salah satunya adalah menambahkan bentuk seperti persegi panjang ke lembar kerja Anda. Dalam panduan ini, kita akan membahas cara menambahkan kontrol persegi panjang ke lembar kerja Excel menggunakan Aspose.Cells for .NET. Pada akhirnya, Anda akan dapat membuat, menyesuaikan, dan menyimpan lembar kerja dengan kontrol persegi panjang yang tertanam di dalamnya.
Namun sebelum membahasnya, mari kita bahas prasyaratnya.
## Előfeltételek
Untuk mengikuti tutorial ini, pastikan Anda memiliki prasyarat berikut:
1. Aspose.Cells untuk pustaka .NET: Jika Anda belum melakukannya, [unduh perpustakaan](https://releases.aspose.com/cells/net/) atau menginstalnya menggunakan NuGet di Visual Studio.
2. .NET Framework: Anda perlu menyiapkan lingkungan pengembangan .NET di komputer Anda.
3. Pengetahuan dasar C#: Meskipun kami akan memandu Anda langkah demi langkah, pengetahuan dasar tentang C# dan pemrograman berorientasi objek akan bermanfaat.
4. Lisensi: Menggunakan Aspose.Cells dalam mode evaluasi berfungsi dengan baik untuk tugas-tugas dasar, tetapi untuk fungsionalitas penuh, pertimbangkan untuk mendapatkan [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) atau membeli satu dari [itt](https://purchase.aspose.com/buy).
Sekarang, mari selami kodenya!
## Csomagok importálása
Untuk memulai dengan Aspose.Cells, pastikan Anda telah mengimpor namespace yang diperlukan ke dalam proyek Anda. Impor ini akan memungkinkan akses ke berbagai kelas dan metode yang Anda perlukan untuk berinteraksi dengan file Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Baris ini memastikan bahwa proyek Anda dapat berinteraksi dengan direktori file (`System.IO`), buku kerja Excel (`Aspose.Cells`), dan menggambar bentuk (`Aspose.Cells.Drawing`).
Sekarang, mari kita uraikan prosesnya ke dalam beberapa langkah sederhana sehingga Anda dapat dengan mudah mengikuti dan mengulanginya dalam proyek Anda sendiri.
## Langkah 1: Menyiapkan Jalur Direktori
Hal pertama yang perlu Anda lakukan adalah menentukan direktori tempat file Excel akan disimpan. Langkah ini memastikan bahwa proyek Anda mengetahui tempat untuk membuat dan menyimpan file output.
### Mendefinisikan Direktori Data
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Di sini, Anda menentukan jalur direktori tempat file Excel akan disimpan. Anda dapat mengganti `"Your Document Directory"` dengan jalur sebenarnya di komputer Anda, atau membuat folder secara dinamis jika belum ada.
### Memeriksa dan Membuat Direktori
```csharp
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Blok ini memeriksa apakah direktori tersebut ada. Jika tidak, maka akan dibuatkan direktori baru. Anggap saja seperti menyiapkan lemari arsip sebelum menyimpan dokumen apa pun.
## Langkah 2: Membuat Instansiasi Buku Kerja Baru
Pada langkah ini, Anda membuat buku kerja Excel baru menggunakan `Aspose.Cells.Workbook` kelas. Ini akan berfungsi sebagai wadah untuk lembar kerja dan bentuk Anda.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Dengan menelepon `Workbook` konstruktor, Anda sekarang memiliki buku kerja Excel kosong yang siap untuk kustomisasi.
## Langkah 3: Menambahkan Kontrol Persegi Panjang
Di sinilah keajaiban terjadi. Anda akan menambahkan bentuk persegi panjang ke lembar kerja pertama buku kerja Anda.
```csharp
// Tambahkan kontrol persegi panjang.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Mari kita uraikan ini:
- `excelbook.Worksheets[0]`Ini mengakses lembar kerja pertama dalam buku kerja Anda.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Ini menambahkan bentuk persegi panjang ke lembar kerja. Parameter di sini menentukan posisi (baris dan kolom), serta lebar dan tinggi persegi panjang.
## Langkah 4: Menyesuaikan Persegi Panjang
Menambahkan persegi panjang saja tidak cukup—Anda perlu menyesuaikannya. Pada langkah ini, kita akan mengatur penempatan, ketebalan garis, dan gaya garis putus-putus persegi panjang.
### Mengatur Penempatan
```csharp
// Mengatur penempatan persegi panjang.
rectangle.Placement = PlacementType.FreeFloating;
```
Ini menetapkan bahwa persegi panjang tersebut mengambang bebas, artinya tidak akan dibatasi oleh dimensi sel.
### Mengatur Berat Garis
```csharp
// Tetapkan ketebalan garis.
rectangle.Line.Weight = 4;
```
Di sini, kita atur ketebalan garis persegi panjang menjadi 4 poin. Semakin tinggi angkanya, semakin tebal garisnya.
### Mengatur Gaya Tanda Hubung
```csharp
// Mengatur gaya garis putus-putus pada persegi panjang.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Baris ini mengatur gaya garis putus-putus batas persegi panjang menjadi padat. Anda dapat bereksperimen dengan gaya yang berbeda seperti `Dash` vagy `Dot` Tergantung pada kebutuhan Anda.
## 5. lépés: A munkafüzet mentése
Setelah persegi panjang ditambahkan dan disesuaikan, langkah terakhir adalah menyimpan buku kerja ke direktori yang ditentukan.
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
Ini menyimpan buku kerja sebagai `.xls` file di folder yang Anda tentukan sebelumnya. Anda dapat mengubah format file dengan mengubah ekstensi, seperti `.xlsx` jika Anda lebih suka format Excel yang lebih baru.
## Következtetés
Nah, itu dia! Menambahkan kontrol persegi panjang ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET adalah proses yang mudah setelah Anda menguraikannya langkah demi langkah. Apakah Anda perlu menambahkan bentuk untuk tampilan visual, menyorot bagian data, atau menyesuaikan laporan, Aspose.Cells memberi Anda fleksibilitas untuk melakukannya secara terprogram.
Panduan ini akan membekali Anda dengan semua pengetahuan yang Anda butuhkan untuk mulai menambahkan bentuk seperti persegi panjang ke lembar Excel Anda dengan Aspose.Cells. Sekarang saatnya bereksperimen dan melihat apa lagi yang dapat Anda capai dengan pustaka hebat ini!
## GYIK
### Bisakah saya menambahkan bentuk lain seperti lingkaran atau garis menggunakan Aspose.Cells untuk .NET?  
Ya, Aspose.Cells memungkinkan Anda menambahkan berbagai bentuk, termasuk lingkaran, garis, panah, dan banyak lagi.
### Properti apa lagi yang dapat saya atur untuk kontrol persegi panjang?  
Anda dapat menyesuaikan warna isian, warna garis, transparansi, dan bahkan menambahkan teks di dalam persegi panjang.
### Az Aspose.Cells kompatibilis a .NET Core-ral?  
Ya, Aspose.Cells mendukung .NET Core, serta .NET Framework dan platform berbasis .NET lainnya.
### Dapatkah saya memposisikan persegi panjang relatif terhadap sel tertentu?  
Ya, Anda dapat menempatkan persegi panjang dalam baris dan kolom tertentu, atau menggunakan `PlacementType` untuk mengontrol bagaimana ia dijangkarkan.
### Van ingyenes próbaverzió az Aspose.Cells-hez?  
Igen, kaphatsz egy [ingyenes próba](https://releases.aspose.com/) dari situs web untuk menguji fitur perpustakaan sebelum membeli.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}