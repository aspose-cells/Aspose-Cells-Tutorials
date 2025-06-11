---
"description": "Pelajari cara menambahkan tautan internal ke sel dalam lembar Excel menggunakan Aspose.Cells for .NET. Sempurnakan navigasi di lembar kerja Anda dengan mudah."
"linktitle": "Menambahkan Tautan ke Sel Lembar Lain di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Menambahkan Tautan ke Sel Lembar Lain di Excel"
"url": "/id/net/excel-working-with-hyperlinks/add-link-to-other-sheet-cell/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan Tautan ke Sel Lembar Lain di Excel

## Bevezetés
Bayangkan Anda sedang berjalan di bandara yang sibuk; Anda tidak ingin membuang waktu mencari gerbang Anda. Sebaliknya, rambu-rambu yang jelas dan tautan yang membantu memandu Anda dengan lancar ke tujuan Anda. Demikian pula, dalam perangkat lunak spreadsheet seperti Excel, menambahkan hyperlink dapat menyederhanakan navigasi dan membuat data Anda lebih mudah digunakan. Apakah Anda mengelola anggaran yang rumit, melacak penjualan, atau menangani kumpulan data besar, kemampuan untuk menautkan ke lembar lain dapat menghemat banyak waktu dan kebingungan. Hari ini, kita akan membahas cara menambahkan tautan ke sel di lembar lain menggunakan Aspose.Cells untuk .NET. Panduan ini akan memandu Anda langkah demi langkah melalui proses tersebut, memastikan Anda dapat menerapkan fitur hebat ini di spreadsheet Excel Anda.
## Előfeltételek
Mielőtt belekezdenénk, van néhány dolog, amire szükséged lesz:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Ini adalah alat yang berguna untuk pengembangan .NET.
2. Pustaka Aspose.Cells: Anda perlu mengunduh dan memasang pustaka Aspose.Cells untuk .NET. Anda dapat mengunduhnya dari [Halaman unduhan Aspose Cells](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Pemahaman dasar tentang pemrograman C# akan sangat membantu. Panduan ini mengasumsikan Anda cukup familier dengan sintaksis C#.
4. Microsoft Excel: Memiliki Excel di komputer Anda membantu memvisualisasikan hasil dari apa yang akan Anda buat.
5. .NET Framework: Pastikan Anda bekerja dalam versi .NET Framework yang kompatibel yang mendukung pustaka Aspose.Cells.
## Csomagok importálása
Untuk memulai proyek Anda, Anda perlu mengimpor namespace yang diperlukan. Berikut cara melakukannya di file C# Anda:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Dengan impor ini, Anda siap menggunakan fitur-fitur Aspose.Cells yang canggih. 
Sekarang, mari kita uraikan tugas inti—menambahkan hyperlink ke sel di lembar lain dalam file Excel yang sama! 
## Langkah 1: Siapkan Lingkungan Proyek Anda
Sebelum menulis kode apa pun, kita perlu membuat proyek C# baru. 
1. Nyisd meg a Visual Studio-t.
2. Buat proyek Aplikasi Konsol C# baru. 
3. Beri nama proyek Anda sesuatu yang deskriptif seperti "ExcelLinkDemo".
4. Tambahkan referensi ke Aspose.Cells.dll. Anda dapat melakukannya dengan mengklik kanan pada "References" di Solution Explorer, memilih "Add Reference", dan menavigasi ke tempat Anda menginstal Aspose.Cells.
## Langkah 2: Tentukan Direktori Output Anda
Selanjutnya, Anda perlu menentukan di mana Anda ingin menyimpan file Excel keluaran Anda. Berikut ini cara Anda dapat menentukannya dalam kode Anda:
```csharp
// Direktori keluaran untuk file Excel Anda
string outputDir = "Your Document Directory"; // Ganti dengan direktori Anda
```
Mindenképpen cserélje ki `"Your Document Directory"` dengan jalur tempat Anda ingin menyimpan berkas keluaran.
## 3. lépés: A munkafüzet objektum példányosítása
Sekarang Anda siap membuat buku kerja Excel! Di sinilah semua lembar dan data Anda akan berada.
```csharp
// Workbook objektum példányosítása
Workbook workbook = new Workbook();
```
Baris ini menginisialisasi buku kerja baru dalam memori, memberi Anda kanvas kosong untuk dikerjakan.
## Langkah 4: Menambahkan Lembar Kerja Baru
Di Excel, setiap buku kerja dapat berisi beberapa lembar. Mari tambahkan satu lembar ke buku kerja kita.
```csharp
// Új munkalap hozzáadása a Munkafüzet objektumhoz
workbook.Worksheets.Add(); // Menambahkan lembar kerja kosong baru secara default
```
Perintah ini menambahkan lembar kerja baru, dan sekarang buku kerja Anda berisi setidaknya satu lembar untuk Anda manipulasi.
## Langkah 5: Mengakses Lembar Kerja Pertama
Untuk bekerja dengan lembar kerja pertama (dikenal sebagai lembar default), Anda perlu mereferensikannya.
```csharp
// Mendapatkan referensi lembar kerja pertama (default)
Worksheet worksheet = workbook.Worksheets[0];
```
Jelenleg, `worksheet` adalah referensi ke lembar pertama di mana kita akan menambahkan hyperlink.
## Langkah 6: Menambahkan Hyperlink Internal
Inilah bagian yang menarik! Kita akan membuat hyperlink di sel “B3” yang mengarah ke sel “B9” di lembar kerja yang berbeda.
```csharp
// Menambahkan hyperlink internal ke sel "B9" di lembar kerja lain "Sheet2"
worksheet.Hyperlinks.Add("B3", 1, 1, "Sheet2!B9");
```
Dalam perintah ini, kita memberi tahu Excel untuk menjadikan sel “B3” sebagai tautan. Parameternya adalah:
- Lokasi sel untuk hyperlink (“B3”).
- Indeks lembar yang kami tautkan (1, yang merujuk ke lembar kedua).
- Sel target yang ingin kita tautkan (sel di "Sheet2").
## Langkah 7: Menambahkan Teks Tampilan untuk Hyperlink
Saat Anda mengeklik hyperlink, Anda ingin teks tampilan menjelaskan ke mana tautan itu mengarah. Di situlah baris berikutnya muncul.
```csharp
worksheet.Hyperlinks[0].TextToDisplay = "Link To Other Sheet Cell";
```
Ini akan membuat “Link To Other Sheet Cell” muncul di sel “B3,” dan akan memandu siapa saja yang menggunakan spreadsheet tersebut.
## 8. lépés: Mentse el a munkafüzetét
Setelah semuanya diatur, saatnya menyimpan buku kerja yang baru Anda buat dengan hyperlink yang tertanam.
```csharp
// Menyimpan file Excel dengan hyperlink
workbook.Save(outputDir + "outputAddingLinkToOtherSheetCell.xlsx");
```
Pastikan untuk menentukan jalur yang benar di `outputDir` agar berkas Excel Anda tersimpan dengan benar.
## Langkah 9: Konfirmasikan Operasi
Terakhir, mari beri tahu pengguna bahwa operasinya berhasil diselesaikan.
```csharp
Console.WriteLine("AddingLinkToOtherSheetCell executed successfully.");
```
Nah, itu dia! Anda telah membuat program C# dasar yang menambahkan hyperlink internal ke buku kerja Excel menggunakan Aspose.Cells for .NET.
## Következtetés
Dalam tutorial ini, kami menelusuri langkah-langkah yang diperlukan untuk menambahkan hyperlink ke lembar lain dalam buku kerja Excel dengan Aspose.Cells untuk .NET. Tautan dalam lembar kerja Anda dapat berfungsi sebagai penanda di lautan data, sehingga memudahkan navigasi. Bayangkan betapa lebih efisiennya alur kerja Anda dengan lembar kerja yang ditautkan dengan benar! Sekarang setelah Anda memiliki alat canggih ini di ujung jari Anda, jangan ragu untuk bereksperimen lebih lanjut dengan kemampuan Aspose.Cells untuk meningkatkan produktivitas Anda.
## GYIK
### Mi az Aspose.Cells?  
Aspose.Cells adalah pustaka .NET yang canggih untuk membuat dan memanipulasi file Excel tanpa menggunakan Microsoft Excel.
### Ingyenesen használhatom az Aspose.Cells-t?  
Ya! Anda dapat mengunduh uji coba gratis dari [itt](https://releases.aspose.com/).
### Apakah saya perlu menginstal Microsoft Excel untuk menggunakan Aspose.Cells?  
Tidak, Aspose.Cells beroperasi secara independen dari Microsoft Excel.
### Apakah mungkin untuk menautkan ke beberapa lembar?  
Tentu saja! Anda dapat membuat beberapa hyperlink yang mengarah ke lembar yang berbeda menggunakan pendekatan yang sama.
### Hol kaphatok támogatást az Aspose.Cells-hez?  
Anda dapat menghubungi komunitas Aspose untuk mendapatkan dukungan [itt](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}