---
"description": "Pelajari cara mudah mengonversi buku kerja Excel ke format CSV dengan Aspose.Cells dalam tutorial komprehensif langkah demi langkah yang dirancang untuk pengembang .NET."
"linktitle": "Simpan Buku Kerja ke Format Teks CSV"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Simpan Buku Kerja ke Format Teks CSV"
"url": "/id/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Simpan Buku Kerja ke Format Teks CSV

## Bevezetés
Saat menangani data, format yang Anda pilih dapat menentukan seberapa mudah Anda dapat mengolahnya. Salah satu format yang paling umum untuk menangani data tabular adalah CSV (Comma-Separated Values). Jika Anda seorang pengembang yang bekerja dengan file Excel dan perlu mengonversi buku kerja ke dalam format CSV, Aspose.Cells for .NET adalah pustaka fantastis yang menyederhanakan tugas ini. Dalam tutorial ini, kami akan menguraikan langkah-langkah untuk mengonversi buku kerja Excel ke format teks CSV dengan mudah.
## Előfeltételek
Sebelum kita mulai, mari pastikan Anda telah menyiapkan semua hal untuk memulai:
1. Pengetahuan Dasar C# dan .NET: Karena kita akan menulis kode dalam C#, pemahaman terhadap bahasa dan kerangka kerja .NET sangatlah penting.
2. Pustaka Aspose.Cells: Pastikan Anda telah memasang pustaka Aspose.Cells for .NET di lingkungan pengembangan Anda. Anda dapat mengunduhnya [itt](https://releases.aspose.com/cells/net/).
3. Visual Studio atau IDE C# apa pun: Anda memerlukan lingkungan pengembangan terintegrasi (IDE) untuk menulis dan menjalankan kode Anda. Visual Studio merupakan pilihan yang populer.
4. Buku Kerja Excel: Siapkan contoh buku kerja Excel (misalnya, "book1.xls") yang berisi beberapa data untuk menguji konversi.
## Csomagok importálása
Setelah prasyarat terpenuhi, langkah pertama dalam proses ini adalah mengimpor paket yang diperlukan. Dalam proyek C#, Anda perlu menyertakan namespace berikut di bagian atas berkas kode:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ruang nama ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk bekerja dengan file Excel dan mengelola aliran memori.
## Langkah 1: Tentukan Jalur ke Direktori Dokumen
Langkah pertama dalam proses kami adalah menentukan tempat penyimpanan dokumen (buku kerja Excel). Hal ini penting karena memungkinkan program kami mengetahui tempat menemukan berkas yang perlu diproses. 
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Mindenképpen cserélje ki `"Your Document Directory"` dengan jalur sebenarnya tempat file "book1.xls" Anda berada. Ini bisa berupa direktori di komputer Anda atau jalur ke server.
## Langkah 2: Muat Buku Kerja Sumber Anda
Berikutnya, kita perlu memuat buku kerja Excel yang akan dikonversi ke format CSV.
```csharp
// Muat buku kerja sumber Anda
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
A `Workbook` kelas dari pustaka Aspose.Cells memungkinkan manipulasi dan akses ke buku kerja Excel. Dengan meneruskan jalur file, kita memuat buku kerja yang ditentukan untuk diproses.
## Langkah 3: Inisialisasi Array Byte untuk Data Buku Kerja
Sebelum kita mulai mengonversi buku kerja ke CSV, kita perlu menginisialisasi array byte kosong yang nantinya akan menampung semua data lembar kerja.
```csharp
// susunan 0-byte
byte[] workbookData = new byte[0];
```
Susunan byte ini akan menggabungkan data dari setiap lembar kerja menjadi satu struktur tunggal yang dapat kita tulis ke dalam berkas nantinya.
## Langkah 4: Siapkan Opsi Penyimpanan Teks
Sekarang, mari kita atur opsi untuk menyimpan format teks. Anda dapat memilih pembatas khusus atau tetap menggunakan tab.
```csharp
// Opsi penyimpanan teks. Anda dapat menggunakan jenis pemisah apa pun
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Mengatur tab sebagai pemisah
```
Dalam contoh ini, kami menggunakan karakter tab sebagai pemisah. Anda dapat mengganti `'\t'` dengan karakter apa pun yang Anda inginkan, seperti koma (`,`), tergantung pada bagaimana Anda ingin CSV diformat.
## Langkah 5: Ulangi Setiap Lembar Kerja
Selanjutnya, kita akan mengulangi semua lembar kerja dalam buku kerja, menyimpan masing-masing ke dalam `workbookData` array, tetapi Anda harus terlebih dahulu memilih lembar kerja mana yang akan dikerjakan.
```csharp
// Salin setiap data lembar kerja dalam format teks di dalam array data buku kerja
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Simpan lembar kerja aktif ke dalam format teks
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
Perulangan berjalan melalui setiap lembar kerja dalam buku kerja. `ActiveSheetIndex` diatur sehingga setiap kali melalui loop, kita menyimpan lembar kerja saat ini. Hasilnya akan disimpan ke dalam memori menggunakan `MemoryStream`.
## Langkah 6: Ambil Data Lembar Kerja
Setelah menyimpan lembar kerja ke aliran memori, langkah selanjutnya adalah mengambil data ini dan menambahkannya ke `workbookData` sor.
```csharp
    // Simpan data lembar kerja ke dalam array data lembar
    ms.Position = 0; // Setel ulang posisi aliran memori
    byte[] sheetData = ms.ToArray(); // Dapatkan array byte
```
`ms.Position = 0;` mengatur ulang posisi untuk membaca setelah menulis. Kemudian, kita menggunakan `ToArray()` untuk mengubah aliran memori menjadi array byte yang menampung data lembar kerja.
## Langkah 7: Gabungkan Data Lembar Kerja
Sekarang, kita akan menggabungkan data dari setiap lembar kerja menjadi satu `workbookData` array diinisialisasi sebelumnya.
```csharp
    // Gabungkan data lembar kerja ini ke dalam array data buku kerja
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Kami membuat array baru yang cukup besar untuk menampung data buku kerja yang ada dan data lembar kerja yang baru. Kemudian kami menyalin data yang ada dan yang baru ke dalam array gabungan ini untuk penggunaan selanjutnya.
## Langkah 8: Simpan Seluruh Data Buku Kerja ke dalam File
Akhirnya, dengan semua data yang digabungkan dalam `workbookData` array, kita dapat menyimpan array ini ke jalur file yang ditentukan.
```csharp
// Simpan seluruh data buku kerja ke dalam file
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` mengambil array byte gabungan dan menuliskannya ke dalam file teks bernama "out.txt" di direktori yang ditentukan.
## Következtetés
Nah, itu dia! Anda telah berhasil mengonversi buku kerja Excel ke format CSV menggunakan Aspose.Cells for .NET. Proses ini tidak hanya efisien, tetapi juga memungkinkan manipulasi data Excel dengan mudah untuk analisis atau pelaporan lebih lanjut. Sekarang Anda dapat mengotomatiskan tugas pemrosesan data atau bahkan mengintegrasikan fungsionalitas ini ke dalam aplikasi yang lebih besar.
## GYIK
### Dapatkah saya menggunakan pembatas yang berbeda untuk file CSV?
Ya, Anda dapat mengubahnya `opts.Separator` ke karakter apa pun yang Anda inginkan, seperti koma atau tanda pipa.
### Ingyenesen használható az Aspose.Cells?
Aspose.Cells tidak gratis, tetapi Anda bisa mendapatkan uji coba gratis [itt](https://releases.aspose.com/).
### Jenis format apa saja yang dapat saya simpan selain CSV?
Aspose.Cells memungkinkan penyimpanan ke berbagai format termasuk XLSX, PDF, dan banyak lagi.
### Bisakah saya memproses berkas Excel berukuran besar menggunakan Aspose.Cells?
Ya, Aspose.Cells dirancang untuk menangani file besar secara efisien, tetapi kinerjanya mungkin bergantung pada sumber daya sistem.
### Di mana saya dapat menemukan dokumentasi yang lebih rinci?
Anda dapat menemukan dokumentasi dan contoh yang lengkap di [situs referensi](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}