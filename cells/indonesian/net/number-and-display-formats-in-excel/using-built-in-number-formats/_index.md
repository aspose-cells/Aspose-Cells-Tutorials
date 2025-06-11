---
"description": "Otomatiskan pemformatan angka di Excel menggunakan Aspose.Cells untuk .NET. Pelajari cara menerapkan format tanggal, persentase, dan mata uang secara terprogram."
"linktitle": "Menggunakan Format Angka Bawaan di Excel Secara Terprogram"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Menggunakan Format Angka Bawaan di Excel Secara Terprogram"
"url": "/id/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Menggunakan Format Angka Bawaan di Excel Secara Terprogram

## Bevezetés
Dalam tutorial ini, kami akan memandu Anda tentang cara menggunakan format angka bawaan di Excel menggunakan Aspose.Cells untuk .NET. Kami akan membahas semuanya mulai dari menyiapkan lingkungan Anda hingga menerapkan berbagai format seperti tanggal, persentase, dan mata uang. Baik Anda seorang profesional berpengalaman atau baru mengenal ekosistem .NET, panduan ini akan membantu Anda memformat sel Excel dengan mudah.
## Előfeltételek
Mielőtt belevágnál, győződj meg róla, hogy a következőkkel rendelkezel:
- Pustaka Aspose.Cells untuk .NET telah terinstal. Anda dapat [töltsd le itt](https://releases.aspose.com/cells/net/).
- Pengetahuan dasar tentang C# dan pemrograman .NET.
- Visual Studio atau IDE .NET apa pun yang terinstal di komputer Anda.
- Lisensi Aspose yang valid atau [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
- .NET framework terpasang (versi 4.0 atau lebih tinggi).
  
Jika Anda tidak memiliki salah satu hal di atas, ikuti tautan yang disediakan untuk mengatur semuanya. Siap? Mari kita mulai bagian yang menyenangkan!
## Csomagok importálása
Sebelum memulai tutorial, pastikan untuk mengimpor namespace yang diperlukan untuk bekerja dengan Aspose.Cells untuk .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Setelah mengimpornya, Anda siap untuk memanipulasi file Excel secara terprogram. Sekarang, mari selami panduan langkah demi langkahnya!
## Langkah 1: Buat atau Akses Buku Kerja Excel Anda
Pada langkah ini, Anda akan membuat buku kerja baru. Anggap saja ini seperti membuka file Excel baru, tetapi Anda melakukannya melalui kode!
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Workbook objektum példányosítása
Workbook workbook = new Workbook();
```
Di sini, kita hanya membuat instance baru `Workbook` objek. Ini berfungsi sebagai berkas Excel Anda, siap untuk manipulasi data. Anda juga dapat memuat berkas yang sudah ada dengan memberikan jalurnya.
## 2. lépés: A munkalap elérése
Buku kerja Excel dapat berisi beberapa lembar kerja. Pada langkah ini, kita akan mengakses lembar kerja pertama di buku kerja Anda:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Kita sekarang mengakses lembar kerja pertama dalam buku kerja. Jika Anda perlu memanipulasi lembar tambahan, Anda dapat merujuknya menggunakan indeks atau nama lembar tersebut.
## 3. lépés: Adatok hozzáadása cellákhoz
Mari kita mulai menambahkan beberapa data ke sel tertentu. Pertama, kita akan memasukkan tanggal sistem saat ini ke dalam sel "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Baris ini menyisipkan tanggal saat ini ke dalam sel A1. Keren, bukan? Bayangkan melakukan ini secara manual untuk ratusan sel—itu akan menjadi mimpi buruk. Sekarang, kita akan beralih ke pemformatan!
## Langkah 4: Format Tanggal di Sel "A1"
Selanjutnya, mari kita format tanggal tersebut dalam format yang lebih mudah dibaca, seperti "15-Okt-24". Di sinilah Aspose.Cells benar-benar unggul:
1. Ambil Gaya Sel:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Di sini, kita mengambil gaya sel A1. Anggap saja ini seperti mengambil "mode" sel sebelum melakukan perubahan apa pun.
2. Atur Format Tanggal:
```csharp
style.Number = 15;
```
Pengaturan `Number` properti ke 15 menerapkan format tanggal yang diinginkan. Ini adalah kode format angka bawaan untuk menampilkan tanggal dalam format "d-mmm-yy".
3. Terapkan Gaya ke Sel:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Baris ini menerapkan perubahan gaya pada sel. Sekarang, alih-alih format tanggal default, Anda akan melihat sesuatu yang jauh lebih mudah digunakan seperti "15-Okt-24."
## Langkah 5: Tambahkan dan Format Persentase di Sel "A2"
Mari beralih ke format persentase. Bayangkan Anda ingin memasukkan nilai dan menampilkannya sebagai persentase. Pada langkah ini, kita akan menambahkan nilai numerik ke sel "A2" dan memformatnya sebagai persentase:
1. Masukkan Nilai Numerik:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Ini memasukkan angka 20 ke dalam sel A2. Anda mungkin berpikir, "Itu hanya angka biasa—bagaimana cara mengubahnya menjadi persentase?" Nah, kita akan membahasnya.
2. Ambil Gaya dan Atur Format Persentase:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Format sebagai persentase
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Di sini, kita menambahkan 2546 ke sel A3. Selanjutnya, kita akan memformat angka ini agar muncul sebagai mata uang.
2. Ambil Gaya dan Atur Format Mata Uang:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Format sebagai mata uang
worksheet.Cells["A3"].SetStyle(style);
```
Pengaturan `Number` properti ke 6 menerapkan format mata uang. Sekarang nilai di sel A3 akan ditampilkan sebagai "2.546,00," lengkap dengan koma dan dua tempat desimal.
## 7. lépés: Mentse el az Excel-fájlt
Sekarang setelah kita menerapkan semua keajaiban pemformatan, saatnya untuk menyimpan berkas:
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Baris ini menyimpan file Excel dalam format Excel 97-2003. Anda dapat mengubah `SaveFormat` sesuai dengan kebutuhan Anda. Dan begitu saja, Anda telah membuat dan memformat file Excel secara terprogram!
## Következtetés
Selamat! Anda telah berhasil mempelajari cara menggunakan Aspose.Cells for .NET untuk menerapkan format angka bawaan ke sel dalam file Excel. Dari tanggal hingga persentase dan mata uang, kami telah membahas beberapa kebutuhan pemformatan paling umum untuk pemrosesan data Excel. Sekarang, alih-alih memformat sel secara manual, Anda dapat mengotomatiskan seluruh proses—menghemat waktu dan mengurangi kesalahan.
## GYIK
### Dapatkah saya menerapkan format angka khusus menggunakan Aspose.Cells untuk .NET?
Ya! Selain format bawaan, Aspose.Cells juga mendukung format angka khusus. Anda dapat membuat format yang sangat spesifik menggunakan `Custom` properti di `Style` osztály.
### Bagaimana cara memformat sel sebagai mata uang dengan simbol tertentu?
Untuk menerapkan simbol mata uang tertentu, Anda dapat menggunakan format khusus dengan mengatur `Style.Custom` ingatlan.
### Bisakah saya memformat seluruh baris atau kolom?
Tentu saja! Anda dapat menerapkan gaya ke seluruh baris atau kolom menggunakan `Rows` vagy `Columns` koleksi di `Worksheet` objektum.
### Bagaimana cara memformat beberapa sel sekaligus?
Használhatod a `Range` objek untuk memilih beberapa sel dan menerapkan gaya ke semuanya sekaligus.
### Telepítenem kell a Microsoft Excelt az Aspose.Cells használatához?
Tidak, Aspose.Cells bekerja secara independen dari Microsoft Excel, jadi Anda tidak perlu menginstal Excel di komputer Anda.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}