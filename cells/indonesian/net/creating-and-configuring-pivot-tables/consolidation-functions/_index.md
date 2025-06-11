---
"description": "Pelajari cara menggunakan Aspose.Cells for .NET untuk menerapkan fungsi konsolidasi secara terprogram. Otomatiskan tugas analisis data Anda secara efisien."
"linktitle": "Fungsi Konsolidasi Secara Terprogram di .NET"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Fungsi Konsolidasi Secara Terprogram di .NET"
"url": "/id/net/creating-and-configuring-pivot-tables/consolidation-functions/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Fungsi Konsolidasi Secara Terprogram di .NET

## Bevezetés
Apakah Anda ingin memanfaatkan kekuatan Excel untuk analisis data, tetapi ingin mengotomatiskan proses-proses yang membosankan yang terlibat? Nah, Anda berada di tempat yang tepat! Dalam artikel ini, kita akan menyelami dunia Aspose.Cells untuk .NET, dengan fokus khusus pada fungsi konsolidasinya. Bayangkan dapat dengan mudah menganalisis dan meringkas data Anda tanpa menghabiskan waktu berjam-jam untuk tugas-tugas yang berulang.
## Előfeltételek
Sebelum kita memulai perjalanan analisis data, mari pastikan Anda telah menyiapkan semuanya. Berikut ini yang Anda perlukan:
1. Lingkungan .NET: Anda harus memiliki lingkungan .NET yang berfungsi. Baik Anda menggunakan .NET Core atau .NET Framework, langkah-langkahnya sebagian besar akan tetap sama.
2. Pustaka Aspose.Cells: Anda harus menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya dengan mudah dari [Aspose kiadási oldal](https://releases.aspose.com/cells/net/).
3. Pemahaman Dasar tentang C#: Sedikit pengetahuan tentang pemrograman C# akan bermanfaat. Jika Anda sudah membuat kode dalam C#, Anda sudah siap!
4. Contoh File Excel: Untuk contoh kita, pastikan Anda memiliki file Excel bernama `Book.xlsx` siap di direktori dokumen Anda.
## Csomagok importálása
Untuk memulai pengodean, pertama-tama Anda perlu mengimpor paket yang diperlukan. Pustaka Aspose.Cells perlu dirujuk dalam proyek Anda. Berikut cara melakukannya:
1. Instal Paket NuGet: Buka proyek Anda di Visual Studio, klik kanan pada Solusi dan pilih "Kelola Paket NuGet". Cari `Aspose.Cells` dan tekan instal.
2. Menggunakan Arahan: Di bagian atas file C# Anda, Anda harus menyertakan namespace berikut untuk mengakses kelas yang kita perlukan:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Mari kita lanjutkan ke penerapan fungsi konsolidasi kita!
Sekarang, kita akan membagi program utama kita menjadi beberapa langkah yang jelas dan mudah dipahami. Siap? Mari kita mulai!
## 1. lépés: Dokumentumkönyvtár beállítása
Pertama, kita perlu membuat jalur untuk dokumen kita. Ini merujuk pada folder tempat file Excel Anda disimpan.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Mindenképpen cserélje ki `"Your Document Directory"` dengan jalur sebenarnya ke tempat Anda `Book.xlsx` berkas berada.
## 2. lépés: Munkafüzet-példány létrehozása
Selanjutnya, mari kita buat contoh buku kerja dari file Excel sumber kita. Objek ini akan memungkinkan kita berinteraksi dengan data di dalamnya `Book.xlsx`.
```csharp
// Buat buku kerja dari file excel sumber
Workbook workbook = new Workbook(dataDir + "Book.xlsx");
```
Di sini, kita memuat buku kerja sehingga kita dapat mengakses lembar dan datanya.
## 3. lépés: Az első munkalap elérése
Setelah kita memiliki buku kerja, kita perlu mengakses lembar kerja tempat tabel pivot berada. Di sini, kita berasumsi bahwa itu adalah lembar kerja pertama.
```csharp
// Mengakses lembar kerja pertama dari buku kerja
Worksheet worksheet = workbook.Worksheets[0];
```
Baris kode ini mengambil lembar pertama, sehingga memungkinkan kita mengerjakannya secara langsung.
## Langkah 4: Akses Tabel Pivot
Bagus! Sekarang kita perlu menemukan tabel pivot yang ingin kita gunakan. Untuk contoh ini, kita akan mengakses tabel pivot pertama dari lembar kerja kita.
```csharp
// Akses tabel pivot pertama dari lembar kerja
PivotTable pivotTable = worksheet.PivotTables[0];
```
Pastikan file Excel Anda benar-benar berisi tabel pivot agar langkah ini berhasil.
## Langkah 5: Terapkan Fungsi Konsolidasi
Sekarang saatnya menerapkan fungsi konsolidasi! Mari hitung rata-rata untuk bidang data pertama dan hitung entri yang berbeda untuk bidang data kedua.
```csharp
// Terapkan fungsi konsolidasi Rata-rata ke bidang data pertama
pivotTable.DataFields[0].Function = ConsolidationFunction.Average;
// Terapkan fungsi konsolidasi DistinctCount ke bidang data kedua
pivotTable.DataFields[1].Function = ConsolidationFunction.DistinctCount;
```
Cobalah mencampur fungsi-fungsi ini dengan bidang-bidang yang berbeda untuk melihat bagaimana hasilnya berubah.
## Langkah 6: Hitung Perubahannya
Setelah menyiapkan fungsi, penting untuk menghitung data guna mencerminkan perubahan yang telah kita buat. Ini seperti menekan tombol 'refresh' pada lembar kerja Excel Anda.
```csharp
// Hitung data untuk membuat perubahan yang mempengaruhi
pivotTable.CalculateData();
```
Anggap saja langkah ini seperti memastikan kopi Anda sudah diseduh sebelum diminum. Anda tentu tidak ingin melewatkan hasilnya!
## Langkah 7: Simpan Perubahan Anda
Akhirnya, saatnya untuk menyimpan pekerjaan kita. Kita akan menyimpan buku kerja yang dimodifikasi ke dalam file Excel baru yang disebut `output.xlsx`.
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "output.xlsx");
```
Dan voila! Anda telah berhasil menggabungkan data menggunakan pustaka Aspose.Cells di .NET.
## Következtetés
Anda telah sampai di akhir tutorial kami tentang menggabungkan fungsi menggunakan Aspose.Cells untuk .NET! Proses ini tidak hanya menghemat waktu Anda tetapi juga meningkatkan produktivitas Anda. Anda dapat menggunakan pengetahuan baru ini dan menjelajahi berbagai penggunaan fungsi penggabungan dalam tugas analisis data Anda. Jangan lupa untuk berbagi wawasan Anda di kolom komentar, dan jangan ragu untuk menghubungi kami jika Anda memiliki pertanyaan.
## GYIK
### Mi az Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengelola file Excel secara terprogram dalam aplikasi mereka.
### Ingyenesen használhatom az Aspose.Cells-t?
Ya, Aspose menawarkan uji coba gratis yang dapat Anda temukan [itt](https://releases.aspose.com).
### Bagaimana cara mengakses dokumentasi Aspose.Cells?
Anda dapat mengakses dokumentasi yang komprehensif [itt](https://reference.aspose.com/cells/net/).
### Van támogatás az Aspose.Cells-hez?
Tentu saja! Anda dapat mencari bantuan di [támogató fórum](https://forum.aspose.com/c/cells/9).
### Di mana saya dapat membeli lisensi Aspose.Cells?
Anda dapat membeli lisensi [itt](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}