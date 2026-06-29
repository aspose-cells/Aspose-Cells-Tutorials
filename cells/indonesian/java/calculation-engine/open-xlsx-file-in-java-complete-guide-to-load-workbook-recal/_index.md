---
category: general
date: 2026-06-27
description: Buka file XLSX di Java dengan cepat. Pelajari cara membaca file Excel
  di Java, memuat workbook Excel, dan menghitung ulang semua rumus menggunakan Apache
  POI.
draft: false
keywords:
- open xlsx file
- recalculate all formulas
- read excel file in java
- how to recalculate excel formulas
- load excel workbook
language: id
og_description: Buka file XLSX di Java dan pelajari cara membaca file Excel di Java,
  memuat workbook Excel, lalu menghitung ulang semua formula dengan contoh yang jelas
  dan dapat dijalankan.
og_title: Buka File XLSX di Java – Memuat Workbook Langkah demi Langkah & Menghitung
  Ulang Formula
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Open XLSX file in Java quickly. Learn how to read Excel file in Java,
    load Excel workbook, and recalculate all formulas using Apache POI.
  headline: Open XLSX File in Java – Complete Guide to Load Workbook & Recalculate
    Formulas
  type: TechArticle
- questions:
  - answer: Not directly. For older binary formats you’d use `HSSFWorkbook` instead
      of `XSSFWorkbook`. The rest of the code (evaluator, saving) stays the same.
    question: Does this work with `.xls` files?
  - answer: POI does not execute VBA macros, but it can preserve them when you write
      the file back. The formulas will still be recalculated.
    question: What if the workbook contains macros?
  - answer: 'Yes—call `evaluator.evaluateAll()` on the sheet object: `evaluator.evaluateAll(sheet);`.
      ## Wrap‑Up We’ve just shown you how to **open XLSX file in Java**, **load Excel
      workbook**, and **recalculate all formulas** in a clean, production‑ready way.
      The example covers *how to recalculate Excel formula'
    question: Can I recalculate only a single sheet?
  type: FAQPage
tags:
- java
- excel
- apache-poi
title: Buka File XLSX di Java – Panduan Lengkap untuk Memuat Workbook & Menghitung
  Ulang Rumus
url: /id/java/calculation-engine/open-xlsx-file-in-java-complete-guide-to-load-workbook-recal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buka File XLSX di Java – Panduan Lengkap Memuat Workbook & Menghitung Ulang Rumus

Pernah perlu **open XLSX file** di Java tapi tidak yakin pustaka mana yang harus dipilih atau bagaimana membuat rumus‑rumus memperbarui secara otomatis? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ini ketika mereka mencoba *read Excel file in Java* untuk tugas pelaporan atau migrasi data.

Dalam tutorial ini kami akan membahas solusi dunia nyata: memuat workbook Excel, **menghitung ulang semua rumus**, dan menyimpan hasilnya—tanpa spreadsheet yang harus dibuka secara manual. Pada akhir tutorial Anda akan tahu persis *how to recalculate Excel formulas* secara programatis dan memiliki contoh kode yang siap dijalankan.

## Apa yang Anda Butuhkan

- Java 8 atau lebih baru (kode ini bekerja pada Java 11, 17, dll.)  
- Apache POI 5.x (pustaka de‑facto untuk penanganan Excel di Java)  
- File `dynamic.xlsx` sederhana yang ditempatkan di suatu tempat yang dapat Anda referensikan dari proyek Anda  
- IDE favorit Anda atau editor teks biasa—tidak masalah, kode ini sederhana  

Jika Anda sudah memiliki semuanya, bagus—mari kita mulai.

## Buka File XLSX di Java – Memuat Workbook Excel

Langkah pertama adalah **load excel workbook** dari disk. Anggap ini seperti membuka pintu ke spreadsheet; tanpa itu Anda tidak dapat melihat sel atau rumus apa pun di dalamnya.

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/**
 * Demonstrates opening an XLSX file, recalculating formulas, and saving the result.
 */
public class ExcelFormulaRecalc {

    public static void main(String[] args) throws Exception {
        // Path to the file you want to open
        String inputPath = "dynamic.xlsx";

        // Step 1: Load the workbook (open xlsx file)
        try (FileInputStream fis = new FileInputStream(inputPath);
             Workbook workbook = new XSSFWorkbook(fis)) {

            // The workbook is now in memory – ready for further actions
            System.out.println("Workbook loaded successfully.");
```

> **Mengapa XSSFWorkbook?**  
> `XSSFWorkbook` menangani format OOXML modern `.xlsx`, sementara `HSSFWorkbook` untuk format lama `.xls`. Menggunakan kelas yang tepat memastikan Anda benar‑benar **open XLSX file** tanpa menemui `InvalidFormatException`.

## Hitung Ulang Semua Rumus dalam Workbook

Setelah file terbuka, pertanyaan logis berikutnya adalah *“how to recalculate Excel formulas?”* Jawabannya ada di `FormulaEvaluator` milik POI. Ia menelusuri seluruh grafik sheet, mengevaluasi setiap sel yang berisi rumus.

```java
            // Step 2: Create a FormulaEvaluator (how to recalculate excel formulas)
            FormulaEvaluator evaluator = workbook.getCreationHelper().createFormulaEvaluator();

            // Step 3: Force POI to evaluate every formula cell (recalculate all formulas)
            evaluator.evaluateAll();

            System.out.println("All formulas have been recalculated.");
```

> **Pro tip:** Jika Anda hanya perlu memperbarui satu sheet, panggil `evaluator.evaluateAll()` pada sheet tersebut alih‑alih seluruh workbook. Ini dapat menghemat memori pada file yang sangat besar.

### Kasus Tepi & Jebakan Umum

| Situasi | Hal yang Perlu Diperhatikan | Solusi yang Disarankan |
|-----------|-------------------|---------------|
| Workbook sangat besar (ratusan MB) | POI dapat kehabisan memori heap | Gunakan `SXSSFWorkbook` untuk penulisan streaming, atau tingkatkan `-Xmx` |
| Sel berisi referensi eksternal | POI tidak dapat menyelesaikannya secara otomatis | Isi data yang diperlukan terlebih dahulu atau hindari tautan eksternal |
| Fungsi khusus (UDFs) | POI tidak tahu cara mengevaluasinya | Implementasikan `UDFFinder` atau lewati sel‑sel tersebut |

## Verifikasi dan Simpan Workbook yang Diperbarui

Penghitungan ulang hanya berguna jika Anda dapat melihat hasilnya. Mari menulis workbook yang diperbarui kembali ke disk. Anda dapat menimpa file asli, tetapi contoh di bawah menulis ke file baru untuk menjaga keamanan.

```java
            // Step 4: Write the updated workbook to a new file
            String outputPath = "dynamic_updated.xlsx";
            try (FileOutputStream fos = new FileOutputStream(outputPath)) {
                workbook.write(fos);
            }

            System.out.println("Updated workbook saved as " + outputPath);
        }
    }
}
```

Menjalankan program akan mencetak:

```
Workbook loaded successfully.
All formulas have been recalculated.
Updated workbook saved as dynamic_updated.xlsx
```

Buka `dynamic_updated.xlsx` di Excel dan Anda akan melihat bahwa setiap rumus kini mencerminkan data terbaru—tepat seperti yang Anda harapkan setelah operasi **recalculate all formulas** manual.

## Membaca Sel‑sel Spesifik (Opsional)

Jika tujuan Anda adalah *read Excel file in Java* setelah penghitungan ulang, Anda dapat mengambil nilai sel seperti ini:

```java
Sheet sheet = workbook.getSheetAt(0); // first sheet
Row row = sheet.getRow(1); // second row (0‑based)
Cell cell = row.getCell(2); // third column

if (cell.getCellType() == CellType.NUMERIC) {
    double value = cell.getNumericCellValue();
    System.out.println("Recalculated value: " + value);
}
```

Potongan kode ini menunjukkan cara mengambil satu nilai yang baru‑dihitung dari workbook—berguna untuk memasukkan data ke komponen Java lainnya.

## Ringkasan Contoh Kerja Lengkap

Menggabungkan semuanya, berikut program lengkap yang berdiri sendiri yang dapat Anda salin‑tempel ke `ExcelFormulaRecalc.java` dan jalankan:

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

public class ExcelFormulaRecalc {
    public static void main(String[] args) throws Exception {
        String inputPath = "dynamic.xlsx";
        String outputPath = "dynamic_updated.xlsx";

        try (FileInputStream fis = new FileInputStream(inputPath);
             Workbook workbook = new XSSFWorkbook(fis)) {

            // Load the workbook (open xlsx file)
            System.out.println("Workbook loaded successfully.");

            // Recalculate all formulas (how to recalculate excel formulas)
            FormulaEvaluator evaluator = workbook.getCreationHelper().createFormulaEvaluator();
            evaluator.evaluateAll();
            System.out.println("All formulas have been recalculated.");

            // Optional: read a specific cell after recalculation
            Sheet sheet = workbook.getSheetAt(0);
            Row row = sheet.getRow(1);
            Cell cell = row.getCell(2);
            if (cell != null && cell.getCellType() == CellType.NUMERIC) {
                System.out.println("Recalculated cell value: " + cell.getNumericCellValue());
            }

            // Save the updated workbook
            try (FileOutputStream fos = new FileOutputStream(outputPath)) {
                workbook.write(fos);
            }
            System.out.println("Updated workbook saved as " + outputPath);
        }
    }
}
```

Simpan file, tambahkan Apache POI ke classpath proyek Anda (pengguna Maven dapat menambahkan dependensi `poi‑ooxml`), dan jalankan `java ExcelFormulaRecalc`. Itu saja—Anda telah **opened an XLSX file**, **recalculated all formulas**, dan **saved the changes**.

![Contoh membuka file XLSX di Java](/images/open-xlsx-java.png "buka file xlsx")

*Teks alt gambar: contoh membuka file xlsx di Java yang menampilkan editor kode dan output konsol.*

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan file `.xls`?**  
A: Tidak secara langsung. Untuk format biner lama Anda harus menggunakan `HSSFWorkbook` alih‑alih `XSSFWorkbook`. Sisanya (evaluator, penyimpanan) tetap sama.

**Q: Bagaimana jika workbook berisi makro?**  
A: POI tidak mengeksekusi makro VBA, tetapi dapat mempertahankannya saat Anda menulis file kembali. Rumus tetap akan dihitung ulang.

**Q: Bisakah saya menghitung ulang hanya satu sheet?**  
A: Ya—panggil `evaluator.evaluateAll()` pada objek sheet: `evaluator.evaluateAll(sheet);`.

## Kesimpulan

Kami baru saja menunjukkan cara **open XLSX file in Java**, **load Excel workbook**, dan **recalculate all formulas** dengan cara yang bersih dan siap produksi. Contoh ini mencakup *how to recalculate Excel formulas*, mendemonstrasikan *reading Excel file in Java*, dan menyoroti nuansa *load excel workbook* untuk file kecil maupun besar.

Selanjutnya, Anda mungkin ingin menjelajahi:

- Menambahkan gaya atau diagram dengan kelas `XSSF` milik POI  
- Streaming workbook besar dengan `SXSSFWorkbook` untuk penulisan bermemori rendah  
- Mengintegrasikan solusi ke layanan Spring Boot yang memproses unggahan secara langsung  

Cobalah hal‑hal tersebut, dan Anda akan segera mengotomatisasi alur kerja berat Excel seperti seorang profesional. Ada pertanyaan lain? Tinggalkan komentar, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Menguasai Manipulasi File Excel Menggunakan Aspose.Cells untuk Java \| Panduan Operasi Workbook](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Menguasai Operasi File Excel di Java Menggunakan Aspose.Cells](/cells/english/java/workbook-operations/excel-file-operations-aspose-cells-java/)
- [Menguasai Manajemen File XLSB Excel di Java dengan Aspose.Cells: Memuat dan Memodifikasi Koneksi DB](/cells/english/java/workbook-operations/excel-xlsb-management-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}