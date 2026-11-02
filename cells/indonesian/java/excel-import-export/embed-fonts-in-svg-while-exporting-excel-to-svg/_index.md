---
category: general
date: 2026-08-14
description: Menyematkan font dalam SVG saat mengekspor Excel ke SVG menggunakan Aspose.Cells.
  Pelajari cara mengatur area cetak, mengatur opsi cetak, dan menggunakan fungsi WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: id
lastmod: 2026-08-14
og_description: Sematkan font dalam SVG saat mengekspor Excel ke SVG dengan Aspose.Cells.
  Panduan ini menunjukkan cara mengatur area cetak, mengonfigurasi opsi cetak, dan
  menerapkan fungsi WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Menyematkan font dalam SVG saat mengekspor Excel ke SVG – langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Sematkan font dalam SVG saat mengekspor Excel ke SVG
url: /id/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyematkan font dalam SVG saat mengekspor Excel ke SVG

Jika Anda perlu **menyematkan font dalam SVG saat mengekspor Excel ke SVG**, tutorial ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells for Java. Kami juga akan membahas cara **menetapkan area cetak**, **mengatur opsi cetak**, dan **menggunakan fungsi WRAPCOLS** untuk memformat data tanpa kehilangan tata letak.

Anda akan menjalani contoh lengkap yang dapat dijalankan yang memuat workbook yang ada, menerapkan rumus `WRAPCOLS`, mengonfigurasi opsi gambar khusus SVG, mendefinisikan wilayah cetak, dan akhirnya menyimpan file sebagai SVG dengan font yang disematkan. Tidak diperlukan dokumentasi eksternal—cukup salin kode, jalankan, dan periksa SVG yang dihasilkan.

## Menyematkan font dalam SVG – mengonfigurasi ImageOrPrintOptions

Menyematkan font memastikan bahwa SVG ditampilkan persis seperti di Excel, bahkan pada mesin yang tidak memiliki tipe huruf asli terpasang.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Mengapa ini penting*: Ketika `setEmbedFonts(true)` diaktifkan, Aspose.Cells menulis data font langsung ke dalam bagian `<defs>` SVG. Hasilnya adalah file mandiri yang terlihat identik di semua peramban dan platform.

## Mengekspor Excel ke SVG – alur kerja lengkap

Langkah‑langkah berikut menggambarkan proses end‑to‑end, mulai dari memuat workbook hingga menyimpan file SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Output yang diharapkan**: `output.svg` muncul di `YOUR_DIRECTORY`. Membukanya di peramban menampilkan lembar kerja dengan semua font disematkan, data terbungkus menjadi tiga kolom (berkat `WRAPCOLS`), dan hanya sel dalam `A1:H30` yang dirender.

## Menetapkan area cetak untuk lembar kerja

Mendefinisikan area cetak membatasi SVG yang diekspor ke rentang tertentu, yang mengurangi ukuran file dan memfokuskan penonton pada data yang relevan.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tip*: Rentang mengikuti notasi A1 Excel. Jika Anda memerlukan rentang dinamis, Anda dapat menghitungnya secara programatis dengan `ws.getCells().getMaxDisplayRange()`.

## Mengatur opsi cetak untuk output SVG

Opsi cetak mengontrol bagaimana Aspose.Cells menerjemahkan lembar kerja menjadi gambar. Selain menyematkan font, Anda dapat menyesuaikan resolusi, skala, dan tata letak halaman.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Mengapa Anda harus mengatur opsi cetak*: Tanpa opsi eksplisit, Aspose.Cells menggunakan nilai default yang mungkin tidak menyematkan font atau menerapkan faktor skala yang tidak diinginkan, sehingga menghasilkan SVG yang buram atau bergaya tidak tepat.

## Menggunakan fungsi WRAPCOLS untuk membungkus data kolom

`WRAPCOLS` adalah rumus Excel yang mendistribusikan rentang vertikal ke dalam sejumlah kolom yang ditentukan. Ini berguna ketika Anda ingin menampilkan daftar panjang dalam grid yang kompak.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Saat workbook disimpan, Aspose.Cells mengevaluasi rumus tersebut, menghasilkan tata letak tiga kolom di dalam area cetak yang telah ditentukan. Teknik ini bekerja untuk rentang berukuran apa pun—cukup sesuaikan argumen kedua ke jumlah kolom yang diinginkan.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program Java lengkap yang dapat Anda tempelkan ke IDE mana pun. Pastikan Anda memiliki pustaka Aspose.Cells for Java di classpath Anda.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Langkah verifikasi**

1. Jalankan program.  
2. Buka `output.svg` di peramban web.  
3. Pastikan teks menggunakan tipe huruf yang sama dengan file Excel asli (font disematkan).  
4. Verifikasi bahwa hanya sel dalam `A1:H30` yang muncul dan data dari `A2:A10` ditampilkan dalam tiga kolom.

## Kesalahan umum dan cara menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|---------|----------------|--------|
| Font tidak muncul di SVG | `setEmbedFonts(false)` atau file font tidak dapat diakses | Pastikan `setEmbedFonts(true)` dan bahwa font terpasang pada mesin yang menjalankan kode |
| WRAPCOLS tidak dievaluasi | Mesin perhitungan dinonaktifkan | Panggil `workbook.calculateFormula()` sebelum mengekspor, atau biarkan Aspose.Cells mengevaluasi saat penyimpanan |
| SVG yang diekspor kosong | Area cetak tidak mencakup data apa pun | Periksa kembali rentang yang diberikan ke `setPrintArea` |
| File SVG sangat besar | Tidak ada skala yang diterapkan, resolusi gambar besar | Sesuaikan `imgOptions.setResolution(96)` atau nilai serupa untuk mengontrol DPI |

## Tips pro: gunakan kembali ImageOrPrintOptions untuk beberapa lembar kerja

Jika workbook Anda berisi beberapa sheet yang memerlukan pengaturan SVG identik, buat satu instance `ImageOrPrintOptions` dan tetapkan ke `PageSetup` masing‑masing sheet. Ini mengurangi konsumsi memori dan menjamin penyematan font yang konsisten di semua file yang diekspor.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Langkah selanjutnya

* **Ekspor ke format vektor lain** – Ubah `ImageFormat.SVG` menjadi `ImageFormat.PDF` untuk PDF berkualitas tinggi.  
* **Pemrosesan batch** – Loop melalui folder berisi file `.xlsx` dan hasilkan SVG secara otomatis.  
* **Penanganan font khusus** – Gunakan `FontSettings` untuk memuat font dari direktori tertentu ketika font sistem tidak mencukupi.  

Dengan menguasai **menyematkan font dalam SVG**, **mengekspor excel ke svg**, **menetapkan area cetak**, **mengatur opsi cetak**, dan **menggunakan fungsi WRAPCOLS**, Anda dapat mengotomatiskan pembuatan SVG berkualitas tinggi untuk laporan, dasbor, dan visualisasi web langsung dari data Excel. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}