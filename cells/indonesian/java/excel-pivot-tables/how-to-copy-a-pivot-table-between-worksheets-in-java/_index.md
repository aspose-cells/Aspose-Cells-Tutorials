---
category: general
date: 2026-10-16
description: Cara menyalin tabel pivot di Java dengan Aspose.Cells – pelajari cara
  menyalin rentang ke lembar lain dan menyalin rentang antar lembar kerja secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: id
lastmod: 2026-10-16
og_description: Cara menyalin tabel pivot di Java menggunakan Aspose.Cells. Tutorial
  ini menunjukkan cara menyalin rentang ke lembar lain dan menyalin rentang antar
  lembar kerja dengan kode lengkap.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Cara menyalin tabel pivot antar lembar kerja di Java – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Cara menyalin tabel pivot antar lembar kerja di Java
url: /id/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot antar lembar kerja di Java

Jika Anda perlu **menyalin tabel pivot** dari satu lembar ke lembar lain dalam buku kerja yang sama, panduan ini menyediakan solusi lengkap yang siap dijalankan. Anda akan melihat cara menyalin rentang sumber yang berisi tabel pivot, mempertahankan fungsionalitasnya, dan memverifikasi hasilnya—semua menggunakan Aspose.Cells untuk Java.

Menyalin tabel pivot adalah tugas umum ketika Anda menghasilkan laporan secara programatik, dan melakukannya dengan benar menghindari kehilangan cache pivot atau merusak formula. Pada akhir tutorial ini Anda akan dapat **menyalin rentang ke lembar lain** dan **menyalin rentang antar lembar kerja** tanpa langkah manual apa pun.

## Apa yang akan Anda pelajari

* Muat file Excel yang sudah ada dengan tabel pivot.
* Tentukan rentang sumber yang berisi tabel pivot.
* Tentukan rentang tujuan pada lembar kerja yang berbeda.
* Gunakan `CopyOptions` untuk menjaga tabel pivot tetap utuh.
* Verifikasi bahwa tabel pivot yang disalin berfungsi seperti yang diharapkan.

**Prasyarat**

* Java 17 atau lebih baru.
* Aspose.Cells untuk Java (versi 23.12 atau lebih baru).  
* File Excel (`input.xlsx`) yang berisi tabel pivot pada lembar pertama.

---

## Cara menyalin tabel pivot dengan Aspose.Cells

Inti dari operasi ini adalah proses empat langkah: memuat buku kerja, menemukan rentang sumber, menentukan rentang tujuan, dan melakukan penyalinan. Di bawah ini setiap langkah dijelaskan secara detail.

### Langkah 1: Muat buku kerja

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Mengapa langkah ini?*  
Memuat buku kerja membawa seluruh file ke dalam memori, memberi Anda akses ke lembar kerja, sel, dan cache pivot. Aspose.Cells membaca format file secara otomatis, jadi Anda tidak perlu khawatir tentang `.xls` vs `.xlsx`.

### Langkah 2: Temukan rentang sumber yang berisi tabel pivot

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Mengapa langkah ini?*  
Tabel pivot disimpan dalam blok sel yang juga merujuk ke cache tersembunyi. Dengan memilih rentang yang tepat (`A1:G20` dalam contoh ini), Anda memastikan cache tetap terhubung saat rentang disalin.

### Langkah 3: Tentukan rentang tujuan pada lembar lain

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Mengapa langkah ini?*  
Memilih tujuan pada lembar kerja yang berbeda memungkinkan Anda **menyalin rentang ke lembar lain**. Sel paling kiri atas (`A1`) adalah titik awal yang umum, namun Anda dapat menempatkannya di mana saja dengan mengubah alamat.

### Langkah 4: Salin rentang sumber sambil mempertahankan tabel pivot

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Mengapa langkah ini?*  
`CopyOptions` mengontrol apa yang ditransfer. Menggunakan `PasteType.PASTE_ALL` menjamin bahwa tabel pivot, formatnya, dan formula dasar disalin. Tanpa opsi ini, hanya nilai mentah yang mungkin disalin, yang dapat merusak fungsi pivot.

### Langkah 5: Simpan buku kerja dan verifikasi hasil

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Buka `output.xlsx` di Excel dan pastikan bahwa:

* Lembar kedua berisi tabel pivot yang berfungsi penuh dan identik dengan yang asli.
* Menyegarkan tabel pivot memperbarui data, membuktikan cache tetap utuh.

## Menyalin rentang ke lembar lain menggunakan Java

Jika tujuan Anda hanya **menyalin rentang ke lembar lain** tanpa tabel pivot, kode yang sama dapat digunakan dengan rentang sel biasa. Satu-satunya perubahan adalah alamat sumber. Konfigurasi `CopyOptions` tetap sama, memastikan formula dan format dipertahankan.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Potongan kode ini menunjukkan fleksibilitas API untuk skenario pivot maupun non‑pivot.

## Menyalin rentang antar lembar kerja tanpa kehilangan formula

Saat Anda **menyalin rentang antar lembar kerja**, formula yang merujuk ke lembar lain dapat menjadi rusak jika referensi relatif berubah. Untuk menghindarinya:

1. Gunakan `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` jika Anda hanya membutuhkan formula.
2. Pertahankan lembar tujuan dalam buku kerja yang sama sehingga referensi internal tetap valid.
3. Setelah menyalin, panggil `workbook.calculateFormula();` untuk memaksa perhitungan ulang.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Langkah tambahan ini memastikan bahwa rentang yang disalin berperilaku persis seperti aslinya, bahkan ketika mencakup beberapa lembar kerja.

## Tips profesional dan jebakan umum

| Situasi | Tips |
|-----------|-----|
| **Cache pivot tidak memperbarui** | Setelah menyalin, panggil `destSheet.getPivotTables().get(0).refresh();` untuk memperbarui cache. |
| **Menyalin ke buku kerja yang berbeda** | Gunakan `Workbook destWorkbook = new Workbook();` dan kemudian `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Ingat untuk menyalin cache pivot secara terpisah jika diperlukan. |
| **Tabel pivot besar** | Tingkatkan ukuran heap Java (`-Xmx2g`) untuk menghindari `OutOfMemoryError` selama penyalinan. |
| **Mempertahankan gaya** | Setel `copyOptions.setPasteType(PasteType.PASTE_ALL)`; jika tidak, hanya nilai yang disalin. |

## Output yang diharapkan

Menjalankan program lengkap menghasilkan `output.xlsx`. Saat dibuka di Excel:

* **Sheet2!A1:G20** menampilkan tabel pivot yang sama dengan **Sheet1!A1:G20**.
* Daftar bidang pivot, label baris/kolom, dan nilai data cocok dengan sumber.
* Menyegarkan pivot memperbarui angka, mengonfirmasi cache berfungsi.

Konsol akan mencetak:

```
Pivot table copied successfully.
```

## Kesimpulan

Dalam tutorial ini Anda belajar **cara menyalin tabel pivot** dari satu lembar kerja ke lembar lain menggunakan Aspose.Cells untuk Java. Dengan memuat buku kerja, memilih rentang sumber yang tepat, menentukan tujuan, dan mengonfigurasi `CopyOptions`, Anda dapat dengan andal **menyalin rentang ke lembar lain** dan **menyalin rentang antar lembar kerja** sambil mempertahankan semua fungsi pivot.  

Selanjutnya, Anda mungkin ingin menjelajahi:

* Mengekspor tabel pivot yang disalin ke PDF atau HTML.
* Mengotomatiskan penyegaran tabel pivot di banyak buku kerja.
* Menggunakan `CopyOptions` untuk menyalin hanya elemen tertentu (mis., nilai, format).

Silakan bereksperimen dengan alamat rentang yang berbeda, struktur buku kerja, atau bahkan penyalinan antar buku kerja. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara menyalin rentang di Java – Salin Tabel Pivot dengan Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Cara Menyalin Tabel Pivot di Java – Panduan Lengkap Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Salin Tabel Pivot Excel – Panduan Langkah‑per‑Langkah Menggunakan Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}