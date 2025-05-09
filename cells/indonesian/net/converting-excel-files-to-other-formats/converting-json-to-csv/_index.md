---
"description": "Pelajari cara mengonversi JSON ke CSV secara terprogram di .NET menggunakan Aspose.Cells. Ikuti panduan langkah demi langkah kami untuk memastikan transformasi data yang lancar."
"linktitle": "Mengonversi JSON ke CSV secara Terprogram di .NET"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Mengonversi JSON ke CSV secara Terprogram di .NET"
"url": "/id/net/converting-excel-files-to-other-formats/converting-json-to-csv/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi JSON ke CSV secara Terprogram di .NET

## Bevezetés
Di dunia digital saat ini, penanganan data dalam berbagai format telah menjadi hal yang lumrah, dan JSON (JavaScript Object Notation) adalah salah satu format yang paling banyak digunakan untuk pertukaran data. Namun, apa yang terjadi jika Anda perlu mengubah JSON tersebut menjadi format yang lebih mudah diakses untuk analisis, seperti CSV (Comma Separated Values)? Tutorial ini akan memandu Anda melalui proses konversi JSON ke CSV secara terprogram menggunakan Aspose.Cells for .NET—API manipulasi spreadsheet yang mudah digunakan namun canggih. 
## Előfeltételek
Sebelum kita menyelami kodenya, penting untuk memastikan Anda memiliki semua komponen yang diperlukan dan pemahaman dasar tentang alat yang akan kita gunakan. Mari kita uraikan apa yang Anda butuhkan:
- Aspose.Cells untuk .NET: Ini adalah pustaka utama yang akan kita gunakan untuk mengonversi JSON ke CSV. Anda dapat [töltsd le itt](https://releases.aspose.com/cells/net/).
- Visual Studio: Anda memerlukan lingkungan pengembangan terintegrasi (IDE) seperti Visual Studio untuk menulis dan mengeksekusi kode .NET.
- .NET Framework: Pastikan Anda telah menginstal .NET Framework. Aspose.Cells kompatibel dengan .NET Core dan .NET Framework.
- Pengetahuan Dasar C#: Meskipun panduan ini akan menguraikan setiap bagian kode, panduan ini akan membantu jika Anda sudah cukup familier dengan C#.
## Csomagok importálása
Untuk menggunakan Aspose.Cells di proyek .NET Anda, pertama-tama Anda perlu menginstal pustaka tersebut. Anda dapat melakukannya melalui NuGet Package Manager:
1. Nyisd meg a Visual Studio-t.
2. Buka Alat > Manajer Paket NuGet > Kelola Paket NuGet untuk Solusi.
3. Cari Aspose.Cells dan instal versi terbaru.
Setelah terinstal, pastikan Anda menyertakan namespace berikut dalam kode Anda:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Sekarang semuanya sudah disiapkan, mari kita urai kodenya langkah demi langkah sehingga Anda dapat melihat betapa mudahnya mengonversi file JSON ke CSV menggunakan Aspose.Cells.
## Langkah 1: Baca File JSON
Hal pertama yang perlu kita lakukan adalah membaca data JSON dari sebuah file. Kita asumsikan Anda sudah memiliki file JSON (sebut saja `SampleJson.json`) yang disimpan dalam direktori di sistem Anda.
Használhatod a `File.ReadAllText()` metode dalam C# untuk membaca isi file JSON menjadi sebuah string.
```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory";
// Membaca file JSON
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Langkah ini penting karena Anda memerlukan data JSON mentah untuk memulai proses konversi. Dengan membacanya sebagai string, Anda mempersiapkannya untuk diproses oleh Aspose.Cells.
## 2. lépés: Üres munkafüzet létrehozása
Aspose.Cells beroperasi terutama pada buku kerja (file Excel). Untuk mulai mengimpor data JSON, pertama-tama Anda perlu membuat buku kerja kosong tempat data ini akan disisipkan.
```csharp
// Üres munkafüzet létrehozása
Workbook workbook = new Workbook();
```
Di sini, Anda menginisialisasi buku kerja kosong yang nantinya akan menampung data berformat CSV. Anggap saja seperti membuat lembar kerja kosong di Excel yang akan segera diisi dengan data JSON Anda.
## Langkah 3: Mengakses Sel di Buku Kerja
Sekarang kita memiliki buku kerja kosong, kita perlu mendapatkan akses ke sel-selnya. `Cells` koleksi di Aspose.Cells mewakili semua sel dalam lembar kerja, tempat Anda akan meletakkan data JSON Anda.
```csharp
// Dapatkan Sel
Cells cells = workbook.Worksheets[0].Cells;
```
Potongan kode ini memilih lembar kerja pertama (lembar kerja pada indeks 0) dan mendapatkannya `Cells` koleksi. Sel-sel ini seperti kisi-kisi lembar kerja tempat data akan ditambahkan.
## Langkah 4: Tetapkan JsonLayoutOptions
Aspose.Cells menyediakan beberapa opsi penyesuaian untuk cara mengimpor data JSON Anda. Di sini, kami mendefinisikan `JsonLayoutOptions` untuk menentukan bagaimana Aspose harus menangani array, data numerik, dan judul objek.
```csharp
// Mengatur Opsi Tata Letak JSON
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: Secara otomatis mengonversi nilai string yang berupa nilai numerik atau tanggal.
- ArrayAsTable: Memperlakukan array dalam JSON sebagai tabel dalam buku kerja.
- IgnoreArrayTitle dan IgnoreObjectTitle: Opsi ini mengabaikan judul untuk array dan objek, memastikan bahwa hanya data mentah yang diimpor.
## Langkah 5: Impor Data JSON
Setelah opsi tata letak ditetapkan, saatnya memasukkan data JSON. `JsonUtility.ImportData()` metode ini melakukan pekerjaan berat di sini, memasukkan data JSON ke dalam sel buku kerja.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Metode ini membutuhkan beberapa parameter:
- `str`: String JSON yang kita baca pada Langkah 1.
- `cells`: Kumpulan sel tempat data akan ditempatkan.
- `0, 0`: Ini adalah indeks baris dan kolom yang menunjukkan di mana data harus dimulai (misalnya, sudut kiri atas).
- `importOptions`: Opsi tata letak yang kami atur pada Langkah 4.
## Langkah 6: Simpan Buku Kerja sebagai CSV
Sekarang data JSON ada di buku kerja, kita dapat dengan mudah menyimpan buku kerja sebagai file CSV. CSV adalah format yang sederhana dan ringan untuk menyimpan data tabular, yang membuatnya sempurna untuk analisis data.
```csharp
// Kimeneti könyvtár
string outputDir = "Your Document Directory";
// Munkafüzet mentése
workbook.Save(outputDir + @"SampleJson_out.csv");
```
Pada langkah ini, kita menyimpan buku kerja sebagai file CSV. Anda menentukan jalur dan nama file (`SampleJson_out.csv`) di mana CSV akan disimpan.
## Langkah 7: Konfirmasikan Prosesnya
Untuk memastikan semuanya bekerja seperti yang diharapkan, kita dapat mencetak pesan konfirmasi di konsol.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Pesan sukses yang sederhana membantu mengonfirmasi bahwa proses berjalan lancar.
## Következtetés
Mengonversi JSON ke CSV menggunakan Aspose.Cells untuk .NET merupakan proses yang mudah namun ampuh. Hanya dengan beberapa baris kode, Anda dapat mengubah data JSON yang kompleks menjadi format CSV yang lebih mudah diakses. Baik Anda berurusan dengan array, objek, atau data numerik, Aspose.Cells memudahkan konfigurasi proses konversi agar sesuai dengan kebutuhan Anda.
## GYIK
### Bisakah Aspose.Cells menangani file JSON berukuran besar?
Ya, Aspose.Cells dirancang untuk menangani kumpulan data besar secara efisien, membuatnya cocok untuk memproses file JSON besar tanpa masalah kinerja.
### Bagaimana saya dapat menyesuaikan keluaran CSV?
Anda dapat menyesuaikan keluaran CSV dengan menyesuaikan `JsonLayoutOptions` atau memanipulasi format buku kerja sebelum menyimpannya sebagai CSV.
### Apakah ada cara untuk mengecualikan data tertentu dari JSON selama konversi?
Ya, dengan mengubah JSON atau menggunakan logika kode khusus sebelum mengimpor, Anda dapat mengecualikan atau memfilter bidang data tertentu.
### Apakah Aspose.Cells mendukung format file lain selain CSV?
Tentu saja! Aspose.Cells mendukung berbagai format termasuk Excel (XLS, XLSX), PDF, HTML, dan masih banyak lagi.
### Bagaimana saya bisa mencoba Aspose.Cells secara gratis?
Kamu bisa [unduh uji coba gratis di sini](https://releases.aspose.com/) untuk menguji semua fitur sebelum membeli.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}