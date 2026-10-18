---
category: general
date: 2026-08-20
description: Pelajari cara mengatur area cetak di Excel, kemudian mengekspor Excel
  ke PPTX dengan Aspose.Cells. Panduan ini akan memandu Anda melalui proses mengonversi
  lembar kerja ke PowerPoint dan menyimpannya sebagai PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: id
lastmod: 2026-08-20
og_description: Atur area cetak di Excel dan kemudian ekspor Excel ke PPTX menggunakan
  Aspose.Cells. Ikuti tutorial langkah demi langkah ini untuk mengonversi lembar kerja
  ke PowerPoint dan menyimpannya sebagai file PPTX.
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: Mengatur area cetak di Excel dan mengekspor ke PowerPoint – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: Cara mengatur area cetak di Excel dan mengekspor ke PowerPoint
url: /id/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengatur area cetak Excel dan mengekspor ke PowerPoint

Jika Anda perlu **set print area excel** sebelum membagikan data dalam sebuah deck slide, tutorial ini menunjukkan secara tepat cara melakukannya. Anda akan melihat cara mengkonfigurasi area cetak, kemudian **export excel to pptx** sambil menjaga kotak teks tetap dapat diedit, sehingga PowerPoint yang dihasilkan siap untuk penyuntingan lebih lanjut.

Kami akan menggunakan Aspose.Cells for Java untuk **convert worksheet to PowerPoint** dan akhirnya **save worksheet as PowerPoint** dalam format PPTX. Tidak ada pustaka tambahan yang diperlukan selain Aspose.Cells JAR. Pada akhir panduan ini Anda dapat menjalankan kode di lingkungan yang kompatibel dengan Java dan menghasilkan presentasi yang mencerminkan rentang Excel yang dipilih.

## Prasyarat

- Java Development Kit 17 atau lebih baru  
- Aspose.Cells for Java (unduh dari situs resmi Aspose)  
- Sebuah workbook Excel yang berisi bentuk (shapes) yang ingin Anda pertahankan dapat diedit (misalnya `BookWithShapes.xlsx`)  

Pastikan Aspose.Cells JAR berada di classpath Anda:

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## Langkah 1: Set print area excel menggunakan Aspose.Cells

Langkah pertama adalah menentukan rentang yang akan diekspor. Menetapkan area cetak membatasi konversi hanya pada sel yang Anda inginkan dan meningkatkan kinerja.

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**Why this matters** – Metode `setPrintArea` memberi tahu Aspose.Cells sel mana yang termasuk dalam halaman yang dapat dicetak. Ketika Anda kemudian **export excel to pptx**, hanya area ini yang dirender, sehingga data yang tidak diperlukan tidak muncul di slide.

### Tips Pro
Jika Anda memerlukan rentang dinamis, Anda dapat menghitung alamat secara programatis:

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## Langkah 2: Export excel to pptx dengan kotak teks yang dapat diedit

Setelah area cetak ditentukan, konfigurasikan opsi ekspor. Mengaktifkan `setExportEditableTextBoxes` mempertahankan teks bentuk sebagai bidang yang dapat diedit di PowerPoint.

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**Why this matters** – Secara default Aspose.Cells merasterisasi kotak teks, menjadikannya bagian dari gambar. Menetapkan `ExportEditableTextBoxes` ke `true` mempertahankan objek bentuk asli, memungkinkan pengguna mengubah teks secara langsung di PowerPoint.

## Langkah 3: Convert worksheet to PowerPoint dan menyimpan file

Sekarang lakukan konversi sebenarnya. Metode `Workbook.save` menerima nama file target dan opsi yang telah dipersiapkan sebelumnya.

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

Setelah kode selesai, `SheetWithEditableShapes.pptx` berisi satu slide yang mencerminkan area cetak yang ditentukan (`A1:G30`). Semua bentuk, termasuk kotak teks, tetap dapat diedit.

### Output yang Diharapkan
Buka PPTX yang dihasilkan di Microsoft PowerPoint:

- Slide menampilkan sel dari **A1 sampai G30** persis seperti yang terlihat di Excel.  
- Semua bentuk yang ada di worksheet asli muncul sebagai bentuk PowerPoint.  
- Teks di dalam bentuk tersebut dapat diedit langsung di PowerPoint (tanpa rasterisasi).

## Langkah 4: Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap. Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

Jalankan program seperti yang dijelaskan pada bagian *Prasyarat*. File PowerPoint yang dihasilkan akan ditempatkan di direktori yang sama yang Anda tentukan.

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Bisakah saya mengekspor beberapa worksheet?** | Ya. Lakukan loop melalui `workbook.getWorksheets()` dan panggil `save` untuk setiap sheet, secara opsional mengubah nama file output. |
| **Bagaimana jika workbook saya berisi chart?** | Chart dirender sebagai gambar secara default. Untuk menjaga mereka dapat diedit, Anda harus mengonversinya menjadi bentuk PowerPoint secara manual, yang berada di luar cakupan panduan ini. |
| **Apakah area cetak diperlukan?** | Tidak. Jika Anda melewatkan `setPrintArea`, Aspose.Cells mengekspor seluruh rentang yang digunakan pada worksheet. Menetapkannya memberi Anda kontrol yang tepat. |
| **Apakah ini bekerja dengan file .xlsx yang dibuat oleh alat lain?** | Tentu saja. Aspose.Cells mendukung semua workbook Office Open XML yang valid, terlepas dari asalnya. |

## Langkah Selanjutnya

- **Save worksheet as PowerPoint** dengan tata letak slide khusus: jelajahi kelas `Presentation` dari Aspose.Slides untuk menggabungkan slide yang diekspor ke dalam dek yang lebih besar.  
- **Export excel to pptx** dengan resolusi gambar yang berbeda: sesuaikan `exportOptions.setResolution(300)` untuk output DPI tinggi.  
- **Automate batch conversions**: gabungkan kode ini dengan file‑watcher untuk memproses banyak file Excel dalam sebuah folder.

Dengan menguasai **set print area excel**, **export excel to pptx**, **convert worksheet to powerpoint**, dan **save worksheet as powerpoint**, Anda dapat mengintegrasikan data Excel ke dalam deck slide secara programatis, menyederhanakan alur pelaporan dan mengurangi pekerjaan salin‑tempel manual.

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengatur Area Cetak di Excel Menggunakan Aspose.Cells untuk .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Atur Area Cetak Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Atur Area Cetak Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}