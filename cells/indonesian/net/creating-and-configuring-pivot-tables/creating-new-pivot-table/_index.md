---
"description": "Pelajari cara membuat tabel pivot secara terprogram di .NET menggunakan Aspose.Cells dengan panduan langkah demi langkah kami. Analisis data Anda secara efisien."
"linktitle": "Membuat Tabel Pivot Baru Secara Terprogram di .NET"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Membuat Tabel Pivot Baru Secara Terprogram di .NET"
"url": "/id/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Tabel Pivot Baru Secara Terprogram di .NET

## Bevezetés
Membuat tabel pivot mungkin tampak seperti tugas yang menakutkan, terutama saat Anda melakukannya secara terprogram. Namun, jangan khawatir! Dengan Aspose.Cells untuk .NET, menyusun tabel pivot tidak hanya mudah tetapi juga cukup ampuh untuk analisis data. Dalam tutorial ini, kami akan memandu Anda langkah demi langkah tentang cara membuat tabel pivot baru dalam aplikasi .NET. Baik Anda menambahkan data untuk penjualan, olahraga, atau metrik bisnis lainnya, panduan ini akan membantu Anda menyiapkan dan menjalankan tabel pivot dalam waktu singkat.

## Előfeltételek
Sebelum memulai, pastikan Anda telah menyiapkan semuanya. Berikut ini yang perlu Anda lakukan:

1. Instal .NET Framework: Pastikan Anda telah menginstal .NET Framework di komputer Anda. Aspose.Cells mendukung berbagai versi, tetapi sebaiknya gunakan versi terbaru.
2. Pustaka Aspose.Cells: Anda perlu memiliki pustaka Aspose.Cells. Anda dapat [töltsd le itt](https://releases.aspose.com/cells/net/) vagy szerezz egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) untuk evaluasi.
3. Penyiapan IDE: Siapkan IDE yang kompatibel dengan C#, seperti Visual Studio, tempat Anda dapat memulai proyek baru.
4. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda mengikutinya tanpa terlalu terjebak.

Sudah siap? Bagus! Mari kita mulai mengimpor paket-paket yang diperlukan.

## Csomagok importálása
Pertama-tama, Anda perlu mengimpor namespace yang diperlukan ke dalam proyek C# Anda. Buka file C# Anda dan tambahkan perintah berikut:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ruang nama ini memberi Anda akses ke fungsionalitas buku kerja, lembar kerja, dan tabel pivot yang akan kita gunakan sepanjang tutorial ini.

## 1. lépés: Munkafüzet-objektum létrehozása
Membuat buku kerja adalah awal perjalanan Anda. Mari kita mulai dengan membuat buku kerja baru dan mengakses lembar kerja pertama.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Workbook objektum példányosítása
Workbook workbook = new Workbook();

// Az újonnan hozzáadott munkalap hivatkozásának beszerzése
Worksheet sheet = workbook.Worksheets[0];
```

Pada langkah ini, kita membuat `Workbook` contoh yang merepresentasikan file Excel kita dan ambil lembar kerja pertama, yang akan menjadi tempat bermain bagi tabel pivot.

## Langkah 2: Masukkan Data ke dalam Sel
Selanjutnya, mari kita isi lembar kerja kita dengan beberapa contoh data. Kita akan memasukkan baris untuk berbagai cabang olahraga, kuartal, dan angka penjualan untuk memberikan sesuatu yang dapat diringkas pada tabel pivot kita.

```csharp
Cells cells = sheet.Cells;

// Mengatur nilai ke sel
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Mengisi datacell = sel["A2"];
cell.PutValue("Golf");
// ... Entri data lebih lanjut
```

Di sini, kita mendefinisikan tajuk kolom dan memasukkan nilai di bawah setiap tajuk. Data ini akan bertindak sebagai sumber untuk tabel pivot kita, jadi pastikan tabel tersebut terorganisasi! Ikuti blok ini, dan Anda akan membuat kumpulan data yang komprehensif.

## Langkah 3: Menambahkan Tabel Pivot
Setelah data kita siap, saatnya membuat tabel pivot. Kita akan menggunakan kumpulan tabel pivot dari lembar kerja untuk menambahkan tabel pivot baru.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Menambahkan PivotTable ke lembar kerja
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Dalam cuplikan ini, kami menambahkan tabel pivot ke lembar kerja yang merujuk ke rentang data kami (dalam kasus ini, sel A1 hingga C8). Kami menempatkan tabel pivot mulai dari sel E3, dan menamainya "PivotTable2". Cukup mudah, bukan?

## Langkah 4: Sesuaikan Tabel Pivot
Sekarang setelah kita memiliki tabel pivot, mari kita sesuaikan tabel tersebut untuk menampilkan ringkasan yang bermakna. Kita dapat mengontrol apa yang muncul di baris, kolom, dan area data tabel pivot.

```csharp
// Mengakses contoh PivotTable yang baru ditambahkan
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Tidak menampilkan total keseluruhan untuk baris.
pivotTable.RowGrand = false;

// Menyeret bidang pertama ke area baris.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Menyeret bidang kedua ke area kolom.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Menyeret bidang ketiga ke area data.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

Pada langkah ini, kami memberi tahu tabel pivot untuk menyembunyikan total keseluruhan untuk baris lalu menentukan kolom mana yang masuk ke dalam baris, kolom, dan area data. Nama cabang olahraga akan mengisi baris, kuartal akan mengisi kolom, dan angka penjualan akan memberikan ringkasan.

## 5. lépés: A munkafüzet mentése
Terakhir, kami ingin menyimpan buku kerja yang baru kami buat untuk melihat hasil kerja kami.

```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Cukup berikan jalur yang tepat, dan output tabel pivot Anda akan tersimpan ke dalam berkas Excel yang bisa Anda buka dan tinjau.

## Következtetés
Membuat tabel pivot secara terprogram menggunakan Aspose.Cells untuk .NET dapat menghemat waktu Anda secara signifikan, terutama saat menangani kumpulan data besar. Anda telah mempelajari cara menyiapkan proyek, mengimpor paket yang diperlukan, mengisi data, dan membuat tabel pivot yang dapat disesuaikan dari awal. Jadi, lain kali Anda kewalahan dengan angka, ingat tutorial ini dan biarkan Aspose.Cells melakukan pekerjaan berat untuk Anda.

## GYIK
### Mi az Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang canggih untuk membuat dan mengelola lembar kerja Excel secara terprogram.

### Van ingyenes próbaverzió az Aspose.Cells-hez?
Ya, Anda bisa mendapatkan uji coba gratis [itt](https://releases.aspose.com/).

### Bisakah saya menyesuaikan tampilan tabel pivot?
Tentu saja! Anda dapat menyesuaikan format, tata letak, dan bahkan gaya tabel pivot sesuai kebutuhan Anda.

### Di mana saya dapat menemukan lebih banyak contoh dan dokumentasi tentang Aspose.Cells?
Ellenőrizheti a [dokumentáció](https://reference.aspose.com/cells/net/) átfogó útmutatókért és példákért.

### Hogyan kaphatok támogatást az Aspose.Cells-hez?
Anda bisa mendapatkan dukungan melalui [Aspose fórum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}