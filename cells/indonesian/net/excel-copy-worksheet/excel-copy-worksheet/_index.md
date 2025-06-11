---
"description": "Pelajari cara menyalin lembar kerja Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah yang mudah diikuti ini. Ideal untuk pengembang .NET yang ingin mengotomatiskan tugas Excel."
"linktitle": "Lembar Kerja Salinan Excel"
"second_title": "Aspose.Cells .NET API-referencia"
"title": "Lembar Kerja Salinan Excel"
"url": "/id/net/excel-copy-worksheet/excel-copy-worksheet/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lembar Kerja Salinan Excel

## Bevezetés

Dalam dunia penanganan data, spreadsheet ada di mana-mana—mulai dari mengelola angka penjualan hingga mengatur data proyek. Namun, bagaimana Anda mengelola file-file ini saat otomatisasi menjadi penting? Nah, jika Anda bekerja di .NET, Aspose.Cells adalah alat yang sangat baik untuk memanipulasi file Excel secara terprogram. Dalam artikel ini, kami akan memandu Anda menyalin lembar kerja dalam file Excel menggunakan Aspose.Cells untuk .NET. Ini adalah tugas umum saat Anda perlu menduplikasi data di lembar baru tanpa memulai dari awal.

Jadi, kencangkan sabuk pengaman Anda! Kita akan menyelami proses ini secara mendalam, tetapi dengan cara yang sederhana, komunikatif, dan jelas.

## Előfeltételek

Sebelum memulai, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai tutorial ini.

### Instal Aspose.Cells untuk .NET
Hal pertama yang harus dilakukan—jika Anda belum menginstal Aspose.Cells for .NET, Anda perlu mengunduh dan menginstalnya. Anda dapat mengunduh versi terbaru dari halaman rilisnya.

- [Aspose.Cells letöltése .NET-hez](https://releases.aspose.com/cells/net/)

Anda dapat menggunakan NuGet di Visual Studio atau mengunduhnya secara manual. Jika Anda lebih suka menggunakan NuGet, jalankan saja perintah ini:

```bash
Install-Package Aspose.Cells
```

### Dapatkan Lisensi
Untuk membuka sepenuhnya fungsionalitas Aspose.Cells, sebaiknya Anda memperoleh lisensi.

- [Licenc vásárlása](https://purchase.aspose.com/buy) vagy [Ideiglenes engedély igénylése](https://purchase.aspose.com/temporary-license/)

Menggunakan perpustakaan tanpa lisensi akan menerapkan tanda air ke berkas keluaran Anda, jadi pastikan Anda menyiapkan lisensi Anda!

### Siapkan Lingkungan Pengembangan Anda
Pastikan Anda telah menginstal hal berikut:
- Visual Studio (atau IDE apa pun yang kompatibel dengan .NET)
- .NET-keretrendszer vagy .NET Core

Setelah semuanya terinstal dan disiapkan, mari mulai membuat kode!

## Csomagok importálása

Untuk bekerja dengan Aspose.Cells, pertama-tama Anda perlu mengimpor namespace yang diperlukan dalam proyek Anda. Berikut cuplikan kode untuk memastikan Anda memiliki referensi yang benar:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Setelah kita selesai dengan urusan tata graha, mari kita masuk ke pekerjaan sebenarnya—menyalin lembar kerja ke dalam buku kerja Excel.

## Langkah 1: Tentukan Jalur Direktori Anda
Hal pertama yang perlu Anda lakukan adalah menentukan direktori tempat file Excel Anda berada. Ini penting untuk memuat file ke dalam proyek Anda dan menyimpan buku kerja yang dimodifikasi.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string InputPath = dataDir + "book1.xls";
```

- A `dataDir` variabel menyimpan jalur direktori tempat file Excel Anda berada. Ubah `"YOUR DOCUMENT DIRECTORY"` ke jalur folder sebenarnya.
- `InputPath` menyimpan lokasi file Excel yang akan kita kerjakan (dalam kasus ini, "book1.xls").

Sebaiknya gunakan jalur dinamis sehingga Anda dapat beralih dengan mudah antar lingkungan (pengembangan, pementasan, produksi).

## Langkah 2: Buka Buku Kerja Excel
Berikutnya, mari muat file Excel menggunakan kelas Workbook, yang mewakili keseluruhan file Excel.

```csharp
Workbook wb = new Workbook(InputPath);
```

- A `Workbook` objek memuat file Excel yang terletak di `InputPath`Aspose.Cells menangani penguraian berkas, jadi Anda tidak perlu khawatir dengan kerumitan format Excel.

## 3. lépés: Hozzáférés a Munkalapgyűjteményhez
Setiap buku kerja memiliki beberapa lembar kerja (anggap saja sebagai tab dalam berkas Excel Anda). Untuk menyalin lembar kerja, pertama-tama Anda perlu mengakses lembar-lembar ini.

```csharp
WorksheetCollection sheets = wb.Worksheets;
```

- `WorksheetCollection` pada dasarnya adalah daftar semua lembar kerja dalam buku kerja. Inilah yang akan kita gunakan untuk menyalin lembar kerja kita.

## Langkah 4: Salin Lembar Kerja yang Ada
Sekarang untuk bagian yang menarik—menduplikasi lembar kerja! Di sini, kita akan menyalin konten "Sheet1" ke lembar baru.

```csharp
sheets.AddCopy("Sheet1");
```

- A `AddCopy` metode menduplikasi lembar kerja yang ada (dalam kasus ini, "Sheet1") dan menambahkan lembar baru ke buku kerja.
- Anda dapat mengganti `"Sheet1"` dengan nama lembar yang ingin Anda salin.

## 5. lépés: A munkafüzet mentése
Terakhir, setelah menyalin lembar kerja, saatnya menyimpan berkas Excel yang telah diperbarui. Kita akan menggunakan metode Simpan untuk menyimpan perubahan ke berkas baru.

```csharp
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```

- A `Save` metode menulis buku kerja yang diperbarui ke file baru (`CopyWithinWorkbook_out.xls`). Anda dapat memilih nama apa pun untuk file keluaran, tetapi ingat untuk menyimpannya dalam format yang sesuai (misalnya, `.xls`, `.xlsx`).

Selesai! Anda telah berhasil menduplikasi lembar kerja dalam file Excel.

## Következtetés

Menyalin lembar kerja di Aspose.Cells untuk .NET tidak hanya mudah tetapi juga sangat efisien. Hanya dengan beberapa baris kode, Anda dapat mengotomatiskan tugas Excel yang berulang, sehingga memudahkan Anda saat menangani kumpulan data besar atau laporan berformat. Baik Anda mengotomatiskan laporan keuangan, log inventaris, atau apa pun yang memerlukan Excel, Aspose.Cells adalah solusi yang tepat untuk Anda.

## GYIK

### Bisakah saya menyalin beberapa lembar kerja sekaligus menggunakan Aspose.Cells untuk .NET?
Tidak, Anda harus menyalinnya satu per satu menggunakan `AddCopy` metode. Namun, Anda dapat dengan mudah mengulang beberapa lembar dan menyalinnya secara berurutan.

### Apakah Aspose.Cells untuk .NET mendukung penyalinan lembar kerja antar buku kerja yang berbeda?
Ya, Anda dapat menyalin lembar kerja antara buku kerja yang berbeda dengan membuka kedua buku kerja dan menggunakan `AddCopy` metode di antara keduanya.

### Milyen Excel formátumokat támogat az Aspose.Cells?
Aspose.Cells mendukung berbagai format Excel, termasuk `.xls`, `.xlsx`, `.csv`, `.html`, és még sok más.

### Szükségem van licencre az Aspose.Cells for .NET használatához?
Ya, untuk menghindari tanda air dan membuka potensi penuh perpustakaan, Anda memerlukan lisensi yang valid. Namun, Anda dapat meminta [ingyenes ideiglenes engedély](https://purchase.aspose.com/temporary-license) untuk mencobanya sebelum membeli.

### Bisakah saya menjalankan Aspose.Cells di .NET Core?
Ya, Aspose.Cells sepenuhnya kompatibel dengan .NET Framework dan .NET Core, membuatnya serbaguna untuk aplikasi lintas-platform.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}