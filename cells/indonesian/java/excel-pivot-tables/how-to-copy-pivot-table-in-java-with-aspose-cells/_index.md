---
category: general
date: 2026-11-19
description: Pelajari cara menyalin pivot table di Java sambil mempertahankan data
  dan tata letaknya. Panduan langkah demi langkah ini juga menunjukkan cara menyalin
  pivot table Excel secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: id
lastmod: 2026-11-19
og_description: Salin tabel pivot di Java dengan Aspose.Cells. Ikuti panduan ini untuk
  mempelajari cara mempertahankan tabel pivot dan menyalin data pivot Excel dengan
  akurat.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Menyalin tabel pivot di Java – panduan lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Cara menyalin tabel pivot di Java dengan Aspose.Cells
url: /id/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot di Java dengan Aspose.Cells

Jika Anda perlu **menyalin tabel pivot** dari satu workbook ke workbook lain, panduan ini menunjukkan secara tepat cara melakukannya di Java. Baik Anda sedang membangun mesin pelaporan atau memigrasikan data, Anda akan melihat cara yang dapat diandalkan untuk mempertahankan cache, bidang, dan pemformatan pivot.

Menyalin tabel pivot dapat menjadi rumit karena penyalinan rentang sederhana sering kehilangan sumber data yang mendasarinya. Dalam tutorial ini kami akan menggunakan Aspose.Cells untuk **how to copy pivot** sambil menjaga setiap perhitungan tetap utuh, dan kami juga akan membahas **how to preserve pivot** tabel ketika workbook tujuan kosong.

## Prasyarat

* Java 17 atau yang lebih baru terinstal.
* Aspose.Cells untuk Java (versi 23.9 atau lebih baru) ditambahkan ke classpath proyek Anda.
* Dua file Excel: sebuah workbook sumber yang berisi tabel pivot dan sebuah workbook tujuan yang kosong (atau workbook yang ingin Anda gabungkan).

Anda tidak memerlukan lisensi khusus untuk contoh kode ini, tetapi lisensi Aspose.Cells yang valid menghilangkan watermark evaluasi.

## Langkah 1: Muat workbook sumber yang berisi tabel pivot

Langkah pertama adalah membuka workbook yang menyimpan pivot asli. Memuat file memberi Anda akses ke lembar kerja, sel, dan cache pivot.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Mengapa ini penting*: Aspose.Cells membaca seluruh workbook, termasuk data cache tersembunyi yang menggerakkan pivot. Tanpa memuat file secara lengkap, operasi penyalinan akan kehilangan definisi pivot.

## Langkah 2: Siapkan workbook tujuan

Buat workbook baru (atau buka yang sudah ada) dan ambil lembar kerja pertamanya. Di sinilah pivot akan ditempatkan.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Tip*: Jika Anda sudah memiliki workbook target, ganti pemanggilan `new Workbook()` dengan `new Workbook("target.xlsx")`. Ini memungkinkan Anda **copy excel pivot** ke dalam workbook yang sudah terisi sebelumnya.

## Langkah 3: Tentukan area sel yang melingkupi tabel pivot

Anda harus menentukan rentang tepat yang mencakup pivot. Rentang tersebut mencakup tabel pivot, daftar bidang, dan data di sekitarnya yang ingin Anda pertahankan.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Mengapa ini penting*: `CellArea` memberi tahu Aspose.Cells apa yang harus disalin. Jika area terlalu kecil, pivot akan terpotong; jika terlalu besar, Anda akan menyalin data yang tidak diperlukan. Sesuaikan koordinat berdasarkan ukuran pivot sebenarnya.

## Langkah 4: Lakukan operasi penyalinan dengan CopyOptions

Gunakan metode `copy` pada koleksi sel lembar kerja sumber. Mengirimkan objek `CopyOptions()` baru memastikan semua pemformatan, formula, dan cache pivot ditransfer.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Mengapa `CopyOptions` mempertahankan pivot

`CopyOptions` memberi tahu Aspose.Cells untuk memperlakukan rentang sebagai objek *utuh* bukan sekadar kumpulan nilai datar. Inilah kunci untuk **how to preserve pivot** tabel: cache pivot yang mendasarinya digandakan, sehingga workbook tujuan dapat menghitung ulang pivot tanpa intervensi manual.

## Langkah 5: Simpan workbook tujuan

Akhirnya, tulis file tujuan ke disk. File yang disimpan akan berisi salinan fungsional penuh dari pivot asli.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Hasil yang diharapkan*: Membuka `copied_with_pivot.xlsx` di Excel menampilkan tabel pivot yang identik, lengkap dengan slicer, filter, dan bidang terhitung. Anda dapat menyegarkannya, dan sumber data akan mengarah ke rentang yang disalin di dalam workbook yang sama.

---

![Diagram showing copy pivot table process](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagram illustrating the copy pivot table workflow from source to destination workbook"}

## Cara menyalin tabel pivot di beberapa lembar kerja

Jika Anda perlu **copy excel pivot** tabel dari beberapa lembar, ulangi Langkah 3‑4 untuk setiap lembar kerja sumber. Anda juga dapat melakukan loop melalui `srcWb.getWorksheets()` dan menyalin setiap pivot ke lembar yang sesuai di `destWb`. Berikut contoh loop yang ringkas:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro tip*: Gunakan `srcWs.getPivotTables().getCount()` untuk mendeteksi apakah sebuah lembar benar‑benar berisi pivot sebelum menyalin. Ini menghindari penyalinan data yang tidak relevan.

## Kesalahan umum dan cara menghindarinya

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivot loses its cache** | Menggunakan `Worksheet.copy()` tanpa `CopyOptions` hanya menyalin nilai sel. | Selalu gunakan `srcWs.getCells().copy(..., new CopyOptions())`. |
| **Destination shows #REF! errors** | Pivot yang disalin masih merujuk ke sumber data eksternal workbook asli. | Setelah menyalin, panggil `destWs.getPivotTables().get(0).refresh();` untuk mengikat kembali cache ke rentang baru. |
| **Slicers disappear** | Slicer disimpan di luar area sel utama. | Perluas `CellArea` untuk mencakup rentang slicer, atau salin seluruh lembar kerja (`srcWs.copy(destWs, new CopyOptions())`). |
| **Performance slowdown on large pivots** | Menyalin rentang besar dengan pemformatan dapat memperlambat. | Gunakan `CopyOptions.setOnlyData(true)` jika Anda tidak memerlukan pemformatan, lalu terapkan kembali gaya secara manual. |

## Cara mempertahankan pemformatan tabel pivot saat memperbarui data

Terkadang Anda perlu **how to preserve pivot** tata letak setelah data sumber berubah. Setelah menyalin, Anda dapat mengunci gaya pivot:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Menetapkan `PreserveFormatting` memastikan bahwa semua gaya khusus yang Anda terapkan di sumber tetap ada setelah penyalinan.

## Memverifikasi penyalinan

Cara cepat untuk memastikan penyalinan berhasil adalah membandingkan definisi pivot:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Jika jumlahnya cocok dan tujuan terbuka tanpa error, Anda telah berhasil **copy pivot table**.

## Kesimpulan

Anda sekarang tahu cara **copy pivot table** dari satu workbook Excel ke workbook lain menggunakan Aspose.Cells untuk Java, dan Anda telah melihat langkah‑langkah tepat untuk **how to copy pivot** sambil memastikan cache, pemformatan, dan slicer pivot tetap utuh. Pola yang sama berlaku untuk skenario **copy excel pivot** di beberapa lembar, dan Anda dapat menyesuaikan kode untuk menangani kasus khusus seperti mempertahankan pemformatan pivot atau menangani set data besar.

### Langkah selanjutnya

* Jelajahi opsi **preserve pivot table** seperti `setPreserveFormatting` dan `refresh` untuk sumber data dinamis.  
* Coba menyalin tabel pivot antara workbook dengan urutan kolom yang berbeda—sesuaikan `CellArea` sesuai.  
* Gabungkan teknik ini dengan Aspose.Slides untuk menyematkan snapshot pivot ke dalam presentasi PowerPoint.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara menyalin rentang dan mempertahankan tabel pivot di Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Cara menyalin tabel pivot antara lembar kerja di Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [Cara menyalin tabel pivot ke workbook baru di Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}