---
category: general
date: 2026-11-25
description: Pelajari cara membuat workbook Excel, memformat sel secara umum, menerapkan
  gaya sel Excel, dan menyimpan workbook XLSX menggunakan Java dan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- format cell general
- apply style excel cell
- save workbook xlsx
language: id
lastmod: 2026-11-25
og_description: Buat workbook Excel dengan Java, format sel sebagai umum, terapkan
  gaya sel Excel, dan simpan workbook XLSX sambil menangani tanggal era Jepang.
og_image_alt: Screenshot of a Java IDE showing code that creates an Excel workbook
  with a formatted date cell
og_title: Buat workbook Excel dengan tanggal era Jepang – panduan Java langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create Excel workbook, format cell general, apply style
    Excel cell, and save workbook XLSX using Java and Aspose.Cells.
  headline: How to create Excel workbook with Japanese era dates in Java
  type: TechArticle
tags:
- Java
- Excel automation
- Aspose.Cells
title: Cara membuat workbook Excel dengan tanggal era Jepang di Java
url: /id/java/formatting/how-to-create-excel-workbook-with-japanese-era-dates-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat workbook Excel dengan tanggal era Jepang di Java

Jika Anda perlu **membuat workbook Excel** yang menyimpan tanggal era Jepang, panduan ini menunjukkan langkah‑langkah tepatnya. Anda akan melihat cara memformat sel sebagai General, menerapkan gaya pada sel Excel, dan akhirnya **menyimpan workbook XLSX** sehingga tanggal diinterpretasikan dengan benar.

Bekerja dengan string era Jepang (seperti “R3‑04‑01”) dapat menjadi rumit karena Excel mengharapkan nilai `DateTime` yang sebenarnya, bukan sekadar teks. Pada akhir tutorial ini Anda akan memiliki file `.xlsx` yang berfungsi penuh yang menampilkan tanggal Gregorian yang tepat sambil mempertahankan notasi era asli.

## Prasyarat

- Java 17 atau lebih baru (kode dapat dikompilasi dengan versi sebelumnya juga)
- Pustaka Aspose.Cells untuk Java (`aspose-cells-xx.x.jar`) – pustaka ini gratis untuk evaluasi dan memiliki semua fitur untuk produksi
- Pengetahuan dasar tentang Java dan Maven/Gradle (atau kemampuan menambahkan JAR ke classpath Anda)
- IDE seperti IntelliJ IDEA, Eclipse, atau VS Code (semua dapat digunakan)

## Langkah 1 – Membuat workbook Excel

Operasi pertama adalah menginstansiasi objek workbook baru. Objek ini mewakili seluruh file Excel dalam memori dan memberi Anda akses ke lembar kerja, sel, dan gaya.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (an empty .xlsx file in memory)
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Mengapa ini penting:**  
Membuat workbook secara programatik menghilangkan kebutuhan akan file templat dan menjamin bahwa file yang dihasilkan dimulai dengan keadaan bersih. Konstruktor `Workbook` secara otomatis membuat lembar default, yang kami ambil untuk manipulasi lebih lanjut.

## Langkah 2 – Memformat sel sebagai General

Excel menyimpan angka dengan berbagai format. Untuk tanggal yang nanti akan kami konversi dari string era Jepang, pertama-tama kami mengatur format nomor sel menjadi *General* sehingga Excel tidak mencoba menginterpretasikan teks terlalu awal.

```java
        // Step 2: Get the target cell (A1) where the era date will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Write the raw Japanese era string (e.g., "R3-04-01")
        targetCell.putValue("R3-04-01");

        // Ensure the cell uses the General number format
        Style cellStyle = targetCell.getStyle();
        cellStyle.setNumber(0); // 0 = General format in Aspose.Cells
        targetCell.setStyle(cellStyle);
```

**Mengapa ini penting:**  
Mengatur **format cell general** mencegah Excel secara otomatis memformat string era sebagai teks dengan format khusus, yang akan menghalangi konversi selanjutnya menjadi `DateTime` yang sebenarnya. Pemanggilan `setNumber(0)` adalah ekuivalen Aspose.Cells dari format “General” di Excel.

## Langkah 3 – Menerapkan gaya pada sel Excel

Meskipun tujuan utama adalah menyimpan tanggal, Anda mungkin ingin sel terlihat konsisten dengan bagian lain lembar—misalnya border tipis atau font tertentu. Menerapkan gaya juga menunjukkan cara memanipulasi estetika sel secara programatik.

```java
        // Step 3: Apply additional styling (optional but common)
        // Example: add a thin border around the cell
        cellStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN);

        // Set a light gray background to highlight the date cell
        cellStyle.setPattern(BackgroundType.SOLID);
        cellStyle.setBackgroundColor(Color.getGray());

        // Apply the updated style back to the cell
        targetCell.setStyle(cellStyle);
```

**Mengapa ini penting:**  
Langkah **apply style excel cell** menunjukkan cara memperkaya tampilan visual tanpa memengaruhi data dasar. Border dan warna latar disimpan sebagai bagian dari objek style sel, memastikan workbook akhir terlihat rapi saat dibuka di Excel.

## Langkah 4 – Mengonversi string era Jepang menjadi objek DateTime

Sekarang kami mengganti teks mentah dengan nilai `DateTime` yang tepat. Aspose.Cells dapat mengurai string menggunakan `CultureInfo` tertentu. Dengan memberikan budaya Jepang (`ja-JP`), pustaka ini secara tepat menginterpretasikan “R3‑04‑01” sebagai tahun ke‑3 era Reiwa, yang berkorespondensi dengan 2021‑04‑01 dalam kalender Gregorian.

```java
        // Step 4: Convert the era string to a DateTime using Japanese culture
        // The fromString method respects the culture’s calendar (Japanese Imperial)
        DateTime japaneseDate = DateTime.fromString(
                "R3-04-01", // era string
                CultureInfo.createSpecificCulture("ja-JP") // Japanese locale
        );

        // Overwrite the cell value with the parsed DateTime
        targetCell.setValue(japaneseDate);
```

**Mengapa ini penting:**  
Tanpa menentukan budaya, “R3‑04‑01” akan diperlakukan sebagai teks biasa, kehilangan makna tanggalnya. Objek `CultureInfo` memberi tahu Aspose.Cells untuk menggunakan sistem kalender Jepang, secara otomatis menangani konversi era. Sel yang dihasilkan kini berisi tanggal Excel yang sebenarnya, memungkinkan penyortiran, penyaringan, dan operasi aritmetika tanggal.

## Langkah 5 – Menyimpan workbook sebagai XLSX

Akhirnya, kami menulis workbook yang berada di memori ke file fisik. Menggunakan format `.xlsx` menjamin kompatibilitas dengan versi Excel modern, Google Sheets, dan alat spreadsheet lainnya.

```java
        // Step 5: Save the workbook to the desired location
        String outputPath = "JapaneseEra.xlsx"; // adjust the path as needed
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved successfully to " + outputPath);
    }
}
```

**Mengapa ini penting:**  
Operasi **save workbook xlsx** menyelesaikan semua perubahan. Aspose.Cells menulis workbook dalam format Open XML, mempertahankan baik data maupun gaya yang diterapkan pada langkah sebelumnya. File yang dihasilkan dapat dibuka langsung di Excel, di mana sel akan menampilkan `2021‑04‑01` (setara Gregorian) tetapi string era asli masih dapat dipulihkan melalui “Format Cells → Number → Custom” di Excel jika diperlukan.

## Output yang Diharapkan

Saat Anda membuka `JapaneseEra.xlsx` di Microsoft Excel:

- Sel **A1** menampilkan tanggal `2021‑04‑01` (format tanggal default Excel).  
- Sel tersebut memiliki border abu‑abu tipis dan latar belakang abu‑abu muda, mengonfirmasi bahwa langkah **apply style excel cell** berhasil.  
- Jika Anda mengubah format sel menjadi “General,” nilai dasarnya tetap berupa tanggal yang sebenarnya, bukan string asli.

Konsol akan mencetak:

```
Workbook saved successfully to JapaneseEra.xlsx
```

## Variasi umum dan kasus tepi

| Situasi | Apa yang harus diubah |
|-----------|----------------|
| **Era berbeda (mis., Heisei)** | Gunakan awalan era yang sesuai (`H` untuk Heisei) dalam string input. `CultureInfo` yang sama akan menangani konversi. |
| **Beberapa tanggal** | Lakukan loop pada rentang sel, menerapkan logika konversi yang sama pada setiap sel. |
| **Format tanggal khusus** | Setelah `setValue(japaneseDate)`, panggil `cellStyle.setNumber(14)` (atau ID format nomor Excel apa pun) untuk menampilkan tanggal sebagai `yyyy/MM/dd`. |
| **Workbook besar** | Gunakan kembali satu objek `Style` untuk kinerja, atau gunakan `StyleFlag` untuk memodifikasi hanya atribut yang diperlukan. |
| **Menyimpan ke stream** | Ganti `workbook.save(outputPath, SaveFormat.XLSX)` dengan `workbook.save(outputStream, SaveFormat.XLSX)` saat mengirim file melalui HTTP. |

## Tips dari lapangan

- **Pro tip:** Selalu atur format nomor sel *sebelum* menetapkan `DateTime`. Mengubah format setelahnya dapat menyebabkan Excel menampilkan representasi visual yang salah.
- **Waspada:** Menggunakan `CultureInfo("ja-JP")` tanpa `createSpecificCulture` dapat kembali ke kalender Gregorian, menghasilkan tanggal yang tidak tepat.
- **Catatan kinerja:** Saat membuat banyak sel bergaya, kloning `Style` yang ada alih-alih memanggil `getStyle()` untuk setiap sel; ini mengurangi beban penyalinan internal.

## Kesimpulan

Dalam tutorial ini Anda belajar cara **membuat workbook Excel** di Java, **memformat sel general**, **menerapkan gaya sel Excel**, dan **menyimpan workbook XLSX** sambil menangani tanggal era Jepang dengan benar. Contoh kode lengkap siap untuk disalin, ditempel, dan dijalankan, memberikan fondasi yang dapat diandalkan untuk otomatisasi Excel apa pun yang melibatkan kalender non‑Gregorian.

Selanjutnya, Anda mungkin ingin menjelajahi:

- Menambahkan rumus yang merujuk pada tanggal yang telah dikonversi (mis., `=YEAR(A1)`).
- Mengekspor workbook ke PDF menggunakan `workbook.save("output.pdf", SaveFormat.PDF)`.
- Mengintegrasikan logika ini ke endpoint REST Spring Boot untuk menghasilkan laporan sesuai permintaan.

Silakan bereksperimen dengan budaya yang berbeda, format nomor khusus, atau impor data massal. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Inisialisasi Workbook Excel & Penataan Sel menggunakan Aspose.Cells Java: Panduan Komprehensif](/cells/english/java/formatting/excel-workbook-initialization-cell-styling-aspose-cells-java/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai SVG menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}