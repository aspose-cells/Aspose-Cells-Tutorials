---
title: Pengelompokan Data dalam Tabel Pivot
linktitle: Pengelompokan Data dalam Tabel Pivot
second_title: API Pemrosesan Java Excel Aspose.Cells
description: Pelajari cara membuat tabel pivot di Excel menggunakan Aspose.Cells untuk Java. Otomatiskan pengelompokan dan analisis data dengan contoh kode sumber.
weight: 14
url: /id/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pengelompokan Data dalam Tabel Pivot


Tabel pivot merupakan alat yang ampuh untuk menganalisis dan meringkas data dalam spreadsheet. Tabel pivot memungkinkan Anda mengelompokkan dan mengkategorikan data untuk mendapatkan wawasan yang berharga. Dalam artikel ini, kita akan membahas cara mengelompokkan data secara efektif dalam tabel pivot menggunakan Aspose.Cells untuk Java, beserta contoh kode sumbernya.

## Perkenalan

Tabel pivot menyediakan cara yang fleksibel untuk mengatur dan meringkas data dari kumpulan data yang besar. Tabel pivot memungkinkan Anda membuat tampilan khusus data dengan mengelompokkannya ke dalam kategori atau hierarki. Ini dapat membantu Anda mengidentifikasi tren, pola, dan outlier dalam data dengan lebih mudah.

## Langkah 1: Buat Tabel Pivot

Mari kita mulai dengan membuat tabel pivot menggunakan Aspose.Cells untuk Java. Berikut adalah contoh cara membuat tabel pivot dari contoh file Excel.

```java
// Memuat file Excel
Workbook workbook = new Workbook("sample.xlsx");

// Akses lembar kerja yang berisi data
Worksheet worksheet = workbook.getWorksheets().get(0);

// Tentukan rentang data
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Dengan asumsi 20 baris data
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Dengan asumsi 4 kolom data

// Membuat tabel pivot berdasarkan rentang data
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Dapatkan tabel pivot berdasarkan indeks
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Tambahkan bidang ke baris dan kolom
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Tambahkan nilai dan terapkan agregasi
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Simpan file Excel yang telah dimodifikasi
workbook.save("output.xlsx");
```

## Langkah 2: Kelompokkan Data

 Di Aspose.Cells untuk Java, Anda dapat mengelompokkan data dalam tabel pivot menggunakan`PivotField` kelas. Berikut ini contoh cara mengelompokkan bidang dalam tabel pivot:

```java
// Akses bidang "Produk" di tabel pivot
PivotField productField = pivotTable.getPivotFields().get("Product");

//Kelompokkan bidang "Produk" berdasarkan kriteria tertentu, misalnya, dengan huruf awal
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Simpan file Excel yang dimodifikasi dengan data yang dikelompokkan
workbook.save("output_grouped.xlsx");
```

## Langkah 3: Sesuaikan Pengelompokan

Anda dapat menyesuaikan pengaturan pengelompokan lebih lanjut, seperti menentukan interval pengelompokan berdasarkan tanggal atau aturan pengelompokan khusus. Berikut ini contoh penyesuaian pengelompokan berdasarkan tanggal:

```java
// Mengakses bidang "Tanggal" di tabel pivot (dengan asumsi itu adalah bidang tanggal)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Kelompokkan tanggal berdasarkan bulan
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Simpan file Excel yang dimodifikasi dengan pengelompokan tanggal khusus
workbook.save("output_custom_grouping.xlsx");
```

## Kesimpulan

Pengelompokan data dalam tabel pivot merupakan teknik yang berharga untuk menganalisis dan meringkas data di Excel, dan Aspose.Cells untuk Java memudahkan untuk mengotomatiskan proses ini. Dengan contoh kode sumber yang disediakan, Anda dapat membuat tabel pivot, menyesuaikan pengelompokan, dan memperoleh wawasan dari data Anda secara efisien.

## Tanya Jawab Umum

### 1. Apa tujuan tabel pivot di Excel?

Tabel pivot di Excel digunakan untuk meringkas dan menganalisis kumpulan data besar. Tabel pivot memungkinkan Anda membuat tampilan data khusus, sehingga memudahkan identifikasi pola dan tren.

### 2. Bagaimana cara menyesuaikan pengelompokan data dalam tabel pivot?

 Anda dapat menyesuaikan pengelompokan data dalam tabel pivot menggunakan`PivotField` kelas di Aspose.Cells untuk Java. Ini memungkinkan Anda menentukan kriteria pengelompokan, seperti interval berbasis tanggal atau aturan khusus.

### 3. Dapatkah saya mengotomatiskan pembuatan tabel pivot menggunakan Aspose.Cells untuk Java?

Ya, Anda dapat mengotomatiskan pembuatan tabel pivot di Excel menggunakan Aspose.Cells untuk Java, seperti yang ditunjukkan dalam contoh kode sumber yang disediakan.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
