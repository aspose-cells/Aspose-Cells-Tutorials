---
"description": "Manfaatkan Kekuatan Analisis Data di Excel dengan Aspose.Cells untuk Java. Pelajari Pengurutan, Pemfilteran, Perhitungan, dan Tabel Pivot."
"linktitle": "Fungsi Analisis Data Excel"
"second_title": "API Pemrosesan Java Excel Aspose.Cells"
"title": "Fungsi Analisis Data Excel"
"url": "/id/java/excel-data-analysis/data-analysis-functions-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Fungsi Analisis Data Excel


## Pengenalan Fungsi Analisis Data di Excel menggunakan Aspose.Cells untuk Java

Dalam panduan lengkap ini, kita akan membahas cara memanfaatkan Aspose.Cells untuk Java untuk menjalankan fungsi analisis data di Excel. Baik Anda seorang pengembang atau analis data, Aspose.Cells untuk Java menyediakan fitur-fitur canggih untuk memanipulasi dan menganalisis data Excel secara terprogram. Kita akan membahas berbagai tugas analisis data, seperti menyortir, memfilter, menghitung statistik, dan banyak lagi. Mari kita bahas!

## Előfeltételek
Mielőtt belekezdenénk, győződjünk meg arról, hogy a következő előfeltételek teljesülnek:

- [Unduh Aspose.Cells untuk Java](https://releases.aspose.com/cells/java/): Anda memerlukan pustaka Aspose.Cells untuk Java. Ikuti tautan untuk mengunduh dan memasangnya di proyek Anda.

## Excel fájl betöltése
Pertama, Anda memerlukan berkas Excel untuk digunakan. Anda dapat membuat berkas baru atau memuat berkas yang sudah ada menggunakan Aspose.Cells. Berikut cara memuat berkas Excel:

```java
// Meglévő Excel fájl betöltése
Workbook workbook = new Workbook("example.xlsx");
```

## Menyortir Data
Mengurutkan data di Excel merupakan tugas yang umum. Aspose.Cells memungkinkan Anda mengurutkan data dalam urutan menaik atau menurun berdasarkan satu atau beberapa kolom. Berikut cara mengurutkan data:

```java
// Dapatkan lembar kerja tempat data Anda berada
Worksheet worksheet = workbook.getWorksheets().get(0);

// Tentukan rentang penyortiran
CellArea cellArea = new CellArea();
cellArea.startRow = 1; // Mulai dari baris kedua (dengan asumsi baris pertama adalah header)
cellArea.startColumn = 0; // Mulai dari kolom pertama
cellArea.endRow = worksheet.getCells().getMaxDataRow(); // Dapatkan baris terakhir dengan data
cellArea.endColumn = worksheet.getCells().getMaxDataColumn(); // Dapatkan kolom terakhir dengan data

// Buat objek opsi penyortiran
DataSorter sorter = workbook.getDataSorter();
sorter.sort(worksheet, cellArea, 0); // Urutkan berdasarkan kolom pertama dalam urutan menaik
```

## Penyaringan Data
Dengan memfilter data, Anda dapat menampilkan hanya baris yang memenuhi kriteria tertentu. Aspose.Cells menyediakan cara untuk menerapkan filter otomatis ke data Excel Anda. Berikut cara menerapkan filter:

```java
// Aktifkan filter otomatis
worksheet.getAutoFilter().setRange(cellArea);

// Terapkan filter pada kolom tertentu
worksheet.getAutoFilter().filter(0, "Filter Criteria");
```

## Menghitung Statistik
Anda dapat menghitung berbagai statistik pada data Anda, seperti nilai total, rata-rata, minimum, dan maksimum. Aspose.Cells menyederhanakan proses ini. Berikut ini contoh penghitungan jumlah kolom:

```java
// Hitung jumlah kolom
double sum = worksheet.getCells().calculateSum(1, 1, worksheet.getCells().getMaxDataRow(), 1);
```

## Tabel Pivot
Tabel pivot merupakan cara yang ampuh untuk meringkas dan menganalisis kumpulan data besar di Excel. Dengan Aspose.Cells, Anda dapat membuat tabel pivot secara terprogram. Berikut cara membuat tabel pivot:

```java
// Membuat tabel pivot
PivotTableCollection pivotTables = worksheet.getPivotTables();
int index = pivotTables.add("=A1:D11", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables.get(index);
pivotTable.addFieldToArea(PivotFieldType.ROW, 0);
pivotTable.addFieldToArea(PivotFieldType.DATA, 3);
```

## Következtetés
Aspose.Cells untuk Java menyediakan berbagai fitur untuk analisis data di Excel. Dalam panduan ini, kami telah membahas dasar-dasar pengurutan, pemfilteran, penghitungan statistik, dan pembuatan tabel pivot. Kini Anda dapat memanfaatkan kekuatan Aspose.Cells untuk mengotomatiskan dan menyederhanakan tugas analisis data Anda di Excel.

## GYIK

### Bagaimana cara menerapkan beberapa kriteria penyortiran?

Anda dapat menerapkan beberapa kriteria pengurutan dengan menentukan beberapa kolom dalam opsi pengurutan. Misalnya, untuk mengurutkan menurut kolom A dalam urutan menaik dan kemudian menurut kolom B dalam urutan menurun, Anda akan mengubah kode pengurutan seperti ini:

```java
// Buat objek opsi pengurutan dengan beberapa kriteria pengurutan
DataSorter sorter = workbook.getDataSorter();
sorter.sort(worksheet, cellArea, new int[] {0, 1}, new int[] {SortOrder.ASCENDING, SortOrder.DESCENDING});
```

### Dapatkah saya menerapkan filter kompleks menggunakan operator logika?

Ya, Anda dapat menerapkan filter kompleks menggunakan operator logika seperti AND dan OR. Anda dapat menggabungkan kondisi filter untuk membuat ekspresi filter kompleks. Berikut ini contoh penerapan filter dengan operator AND:

```java
// Terapkan filter dengan operator AND
worksheet.getAutoFilter().filter(0, "Filter Condition 1");
worksheet.getAutoFilter().filter(1, "Filter Condition 2");
```

### Bagaimana saya dapat menyesuaikan tampilan tabel pivot saya?

Anda dapat menyesuaikan tampilan tabel pivot dengan memodifikasi berbagai properti dan gaya. Ini termasuk pengaturan format sel, penyesuaian lebar kolom, dan penerapan gaya kustom ke sel tabel pivot. Lihat dokumentasi Aspose.Cells untuk petunjuk terperinci tentang penyesuaian tabel pivot.

### Di mana saya dapat menemukan contoh dan sumber daya yang lebih maju?

Untuk contoh, tutorial, dan sumber daya yang lebih canggih tentang Aspose.Cells untuk Java, silakan kunjungi [Dokumentasi Aspose.Cells untuk Java](https://reference.aspose.com/cells/java/)Anda akan menemukan banyak informasi untuk membantu Anda menguasai analisis data Excel dengan Aspose.Cells.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}