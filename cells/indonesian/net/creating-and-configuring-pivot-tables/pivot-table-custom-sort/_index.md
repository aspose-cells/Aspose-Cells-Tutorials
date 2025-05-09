---
"description": "Pelajari cara mengurutkan Tabel Pivot secara terprogram di .NET menggunakan Aspose.Cells. Panduan langkah demi langkah yang mencakup penyiapan, konfigurasi, pengurutan, dan penyimpanan hasil sebagai file Excel dan PDF."
"linktitle": "Urutkan Kustom Tabel Pivot Secara Terprogram di .NET"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Urutkan Kustom Tabel Pivot Secara Terprogram di .NET"
"url": "/id/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Urutkan Kustom Tabel Pivot Secara Terprogram di .NET

## Bevezetés
Jika berbicara tentang bekerja dengan Excel di lingkungan .NET, satu pustaka menonjol di antara yang lain: Aspose.Cells. Nah, bukankah Anda menyukainya saat sebuah alat memungkinkan Anda memanipulasi spreadsheet secara terprogram? Itulah yang dilakukan Aspose.Cells! Dalam tutorial hari ini, kita akan menyelami dunia Tabel Pivot secara mendalam dan menunjukkan kepada Anda cara menerapkan pengurutan kustom secara terprogram menggunakan pustaka serbaguna ini.
## Előfeltételek
Sebelum kita mulai dan mulai menulis kode, pastikan Anda sudah menyiapkan beberapa hal:
1. Visual Studio: Anda memerlukan versi Visual Studio yang berfungsi. Ini adalah tempat bermain di mana semua keajaiban terjadi.
2. .NET Framework: Keakraban dengan pemrograman .NET sangatlah penting. Baik Anda penggemar .NET Core atau .NET Framework, Anda siap untuk memulai.
3. Pustaka Aspose.Cells: Anda perlu menginstal pustaka Aspose.Cells. Anda bisa mendapatkannya dari [Letöltési link](https://releases.aspose.com/cells/net/) és add hozzá a projektedhez.
4. Pemahaman Dasar tentang Tabel Pivot: Meskipun Anda tidak perlu menjadi seorang ahli, sedikit pengetahuan tentang cara kerja Tabel Pivot akan bermanfaat saat kita mempelajari tutorial ini.
5. Contoh File Excel: Memiliki contoh file Excel bernama `SamplePivotSort.xlsx` siap di direktori kerja Anda untuk pengujian.
## Csomagok importálása
Setelah semua prasyarat terpenuhi, langkah pertama adalah mengimpor paket yang diperlukan. Untuk melakukannya, sertakan baris berikut di bagian atas kode Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Paket ini menyediakan semua fungsionalitas yang Anda perlukan untuk memanipulasi file Excel menggunakan Aspose.Cells.

Baiklah, mari kita masuk ke bagian yang menyenangkan! Kita akan menguraikan proses pembuatan Tabel Pivot dan menerapkan pengurutan khusus ke dalam langkah-langkah yang mudah dikelola.
## Langkah 1: Siapkan Buku Kerja
Untuk memulai, kita perlu menyiapkan buku kerja kita. Berikut cara melakukannya:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
Pada langkah ini, kita menginisialisasi yang baru `Workbook` contoh dengan jalur ke berkas Excel kita. Ini berfungsi sebagai kanvas tempat Tabel Pivot kita akan muncul.
## 2. lépés: A munkalap elérése
Berikutnya, kita perlu mengakses lembar kerja tempat kita akan menambahkan Tabel Pivot.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Di sini, kita ambil lembar kerja pertama di buku kerja kita dan panggil `PivotTableCollection`Koleksi ini memungkinkan kita mengelola semua Tabel Pivot pada lembar kerja ini.
## Langkah 3: Buat Tabel Pivot Pertama Anda
Sekarang saatnya membuat Tabel Pivot kita.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Kita tambahkan Tabel Pivot baru ke lembar kerja kita, tentukan rentang data dan lokasinya. "E3" menunjukkan di mana kita ingin Tabel Pivot kita dimulai. Kita kemudian merujuk Tabel Pivot baru ini menggunakan indeksnya.
## Langkah 4: Konfigurasikan Pengaturan Tabel Pivot
Mari konfigurasikan Tabel Pivot kita! Ini berarti mengendalikan aspek-aspek seperti total keseluruhan dan pengaturan bidang.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Kami memastikan bahwa total keseluruhan untuk baris dan kolom tidak ditampilkan, yang dapat membuat data lebih bersih. Kemudian kami menambahkan kolom pertama ke area baris, mengaktifkan penyortiran otomatis dan pengurutan menaik.
## Langkah 5: Tambahkan Kolom dan Bidang Data
Setelah baris ditetapkan, mari tambahkan kolom dan bidang data.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Kita tambahkan kolom kedua sebagai kolom dan format sebagai tanggal. Sekali lagi, kita aktifkan penyortiran otomatis dan urutan menaik untuk menjaga semuanya tetap teratur. Terakhir, kita perlu menambahkan kolom ketiga ke area data kita:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Langkah 6: Segarkan dan Hitung Tabel Pivot
Setelah menambahkan semua bidang yang diperlukan, mari pastikan Tabel Pivot kita baru dan siap.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Metode ini menyegarkan data dan menghitungnya ulang, memastikan semuanya terkini dan ditampilkan dengan benar di Tabel Pivot kami.
## Langkah 7: Urutkan Kustom Berdasarkan Nilai Bidang Baris
Mari tambahkan sedikit gaya dengan mengurutkan Tabel Pivot berdasarkan nilai tertentu, seperti "Makanan Laut".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Kami mengulangi proses tersebut dengan membuat Tabel Pivot lain dan mengaturnya dengan cara yang sama seperti yang pertama. Sekarang kita dapat menyesuaikannya lebih lanjut:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Langkah 8: Kustomisasi Penyortiran TambahanMari coba metode penyortiran lain berdasarkan tanggal tertentu:
```csharp
// Menambahkan Tabel Pivot lain untuk mengurutkan berdasarkan tanggal
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Ulangi pengaturan baris dan kolom mirip dengan langkah sebelumnya
```
Anda tinggal mengulangi proses yang sama, membuat Tabel Pivot ketiga dengan kriteria pengurutan yang disesuaikan dengan kebutuhan Anda.
## Langkah 9: Simpan Buku KerjaSaatnya menyimpan semua kerja keras yang telah kita lakukan!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Di sini, Anda menyimpan buku kerja sebagai file Excel dan PDF. `PdfSaveOptions` memungkinkan pemformatan yang lebih baik, memastikan setiap lembar muncul pada halaman terpisah saat dikonversi.
## Langkah 10: Akhiri dengan memberi tahu pengguna bahwa semuanya baik-baik saja.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Következtetés
Sekarang, Anda telah mempelajari cara memanfaatkan kekuatan Aspose.Cells untuk membuat dan menyesuaikan Tabel Pivot di aplikasi .NET Anda. Dari pengaturan awal hingga penyortiran khusus, setiap langkah digabungkan untuk memberikan pengalaman yang lancar. Baik Anda perlu menyajikan data penjualan tahunan atau melacak statistik inventaris, keterampilan ini akan sangat membantu Anda!
## GYIK
### Apa itu Tabel Pivot?
Tabel Pivot adalah alat pemrosesan data di Excel yang memungkinkan Anda meringkas dan menganalisis data, menyediakan cara fleksibel untuk mengekstrak wawasan dengan mudah.
### Hogyan telepítsem az Aspose.Cells-t?
Anda dapat menginstalnya melalui NuGet di Visual Studio atau mengunduhnya langsung dari [Letöltési link](https://releases.aspose.com/cells/net/).
### Apakah ada versi uji coba Aspose.Cells?
Ya! Anda dapat mencobanya secara gratis dengan mengunjungi [Ingyenes próbaverzió linkje](https://releases.aspose.com/).
### Bisakah saya mengurutkan beberapa bidang dalam Tabel Pivot?
Tentu saja! Anda dapat menambahkan dan mengurutkan beberapa kolom berdasarkan kebutuhan Anda.
### Hol találok támogatást az Aspose.Cells-hez?
Komunitasnya cukup aktif, dan Anda dapat mengajukan pertanyaan di forum mereka [itt](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}