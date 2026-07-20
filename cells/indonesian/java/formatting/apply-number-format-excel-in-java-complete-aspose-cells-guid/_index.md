---
category: general
date: 2026-07-20
description: Terapkan format angka Excel menggunakan Java dan Aspose.Cells. Pelajari
  cara menerapkan gaya mata uang di Excel, membuat workbook Excel dengan Java, dan
  mengimpor DataTable ke Excel secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: id
lastmod: 2026-07-20
og_description: Terapkan format angka Excel dengan Java. Panduan ini menunjukkan cara
  menerapkan gaya mata uang di Excel, membuat workbook Excel dengan Java, dan mengimpor
  datatable ke Excel langkah demi langkah.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Terapkan Format Angka Excel di Java – Tutorial Lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Menerapkan Format Angka Excel di Java – Panduan Lengkap Aspose.Cells
url: /id/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Format Angka Excel di Java – Panduan Lengkap Aspose.Cells

Pernah bertanya-tanya bagaimana cara **apply number format excel** langsung dari kode Java? Mungkin Anda sedang membuat laporan keuangan atau membutuhkan cara cepat untuk menata kolom jumlah tanpa membuka Excel secara manual. Kabar baiknya? Dengan Aspose.Cells Anda dapat melakukannya dalam beberapa baris kode, dan Anda juga akan belajar cara **apply currency style excel**, **create excel workbook java**, serta **import datatable to excel** dalam satu rangkaian yang rapi.

Dalam tutorial ini kita akan membahas contoh dunia nyata: daftar jumlah yang disimpan dalam `List<Map<String,Object>>` Java diimpor ke dalam workbook baru, kolom pertama menerima format mata uang bawaan, dan file disimpan siap didistribusikan. Siap melihat betapa mudahnya? Mari kita mulai.

## Prasyarat – Apa yang Anda Butuhkan

Sebelum memulai, pastikan Anda memiliki:

- **Java Development Kit (JDK) 8+** – kode dapat dijalankan pada JDK terbaru apa pun.
- **Aspose.Cells for Java** library (artifact Maven `com.aspose:aspose-cells`) – ini adalah mesin yang memungkinkan kita memanipulasi file Excel tanpa harus menginstal Office.
- Sebuah **IDE favorit** (IntelliJ IDEA, Eclipse, VS Code…) – editor apa saja dapat digunakan, namun IDE mempercepat proses debugging.
- Familiaritas dasar dengan **Java collections** – kita akan menggunakan `List` of `Map` untuk meniru DataTable.

Itu saja. Tidak ada layanan eksternal, tidak perlu instalasi Excel, hanya Java murni.

## Langkah 1: Buat Excel Workbook Java – Menginstansiasi Workbook

Hal pertama yang kita perlukan adalah objek workbook. Anggap saja ini sebagai kanvas kosong tempat semua hal akan ditempatkan.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Mengapa membuat workbook terlebih dahulu? Aspose.Cells bekerja sepenuhnya di memori, sehingga Anda dapat menambahkan sheet, style, dan data sebelum menyentuh disk. Pendekatan ini cepat dan membuat kode Anda mudah diuji.

## Langkah 2: Siapkan Data – Import Datatable to Excel Menggunakan List of Maps

Di banyak aplikasi perusahaan, data berasal dari basis data dalam bentuk tabel. Di sini kami mensimulasikannya dengan `List<Map<String,Object>>`. Setiap map mewakili satu baris, dan kunci `"Amount"` berisi nilai numerik.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Anda mungkin bertanya, “Mengapa tidak menggunakan `ResultSet` atau POJO?” Metode `importDataTable` menerima koleksi apa pun yang berperilaku seperti DataTable, dan list of maps adalah cara paling sederhana untuk menunjukkan konsep tanpa menambahkan dependensi tambahan.

## Langkah 3: Definisikan Format Angka – Apply Currency Style Excel

Sekarang masuk ke inti tutorial: **apply number format excel**. Aspose.Cells menyediakan format angka bawaan; format mata uang berada pada indeks 5. Kami mengambil style default dari worksheet pertama, menyesuaikan format angkanya, dan menyimpannya untuk penggunaan selanjutnya.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Mengapa menggunakan style default sebagai dasar? Style tersebut sudah berisi font default workbook, perataan, dan pengaturan lainnya, sehingga Anda hanya perlu mengubah hal yang penting—dalam hal ini, format angka. Jika Anda memerlukan format khusus (misalnya “€#,##0.00”), Anda dapat memanggil `currencyStyle.setCustom("#,##0.00 €")` sebagai gantinya.

## Langkah 4: Siapkan Opsi Impor – Menghubungkan Array Style

Aspose.Cells memungkinkan Anda mengirimkan array objek `Style` yang berkorespondensi dengan kolom yang diimpor. Karena data kami hanya memiliki satu kolom, kami menyediakan array satu elemen yang berisi style mata uang.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Jika Anda perlu menata beberapa kolom secara berbeda, cukup perbesar array: `new Style[] { styleForCol1, styleForCol2, … }`. Urutan style harus sesuai dengan urutan kolom pada data sumber.

## Langkah 5: Impor Data – Membawa Datatable ke Worksheet

Dengan workbook siap, data telah dipersiapkan, dan style telah didefinisikan, kini kita **import datatable to excel**. Kami memulai dari sel `A1`, menyertakan header kolom (`true`), dan menyerahkan `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Perhatikan flag `true`—Aspose.Cells akan secara otomatis menghasilkan baris header berdasarkan kunci map (`"Amount"`). Jika Anda mengatur menjadi `false`, header tidak akan dibuat, memberi Anda kontrol lebih besar atas tata letak akhir.

## Langkah 6: Simpan File – Create Excel Workbook Java ke Disk

Potongan terakhir dari puzzle adalah menyimpan workbook yang berada di memori ke file fisik. Anda dapat memilih format apa pun yang didukung Aspose (`.xlsx`, `.xls`, `.csv`, …). Di sini kami menyimpan sebagai file XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Setelah menjalankan program, buka file yang dihasilkan. Anda akan melihat kolom `"Amount"` diformat dengan tanda dolar, dua angka desimal, dan pemisah ribuan yang tepat—tepat seperti yang Anda harapkan ketika **apply number format excel** untuk nilai mata uang.

## Hasil yang Diharapkan

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

Header “Amount” muncul dengan huruf tebal (style default), dan setiap sel di bawahnya menampilkan format mata uang yang telah kami atur. Tidak ada penataan manual di Excel yang diperlukan.

## Tips Pro dan Kesalahan Umum

- **Gunakan Kembali Styles Secara Bijak** – Styles ringan, namun membuat `Style` baru untuk setiap sel dapat menurunkan kinerja. Selalu gunakan kembali objek style ketika menerapkan format yang sama pada banyak sel, seperti yang kami lakukan dengan `currencyStyle`.
- **Format Khusus** – Jika locale Anda menggunakan simbol mata uang berbeda, ganti `currencyStyle.setNumber(5)` dengan `currencyStyle.setCustom("€#,##0.00")`. Uji format tersebut di Excel untuk memastikan perilakunya sesuai harapan.
- **Dataset Besar** – Untuk ribuan baris, pertimbangkan menggunakan `importDataTable` dengan flag `ImportTableOptions.setImportDataOnly(true)` untuk melewatkan pembuatan header dan mempercepat proses impor.
- **Keamanan Thread** – Objek Aspose.Cells **tidak** thread‑safe. Buat `Workbook` terpisah per thread jika Anda menghasilkan laporan secara paralel.

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menerapkan format angka pada workbook yang sudah ada?**  
J: Tentu saja. Buka workbook dengan `new Workbook("Existing.xlsx")`, ambil worksheet target, dan ikuti langkah 3‑5 untuk menerapkan array style pada data baru.

**T: Bagaimana jika saya perlu memformat tanggal bukan mata uang?**  
J: Gunakan indeks angka bawaan yang berbeda (`14` untuk tanggal singkat, `22` untuk tanggal panjang) atau format khusus seperti `yyyy‑mm‑dd`. Alur kerja tetap sama.

**T: Apakah ini bekerja dengan versi Excel lama (.xls)?**  
J: Ya. Cukup ubah ekstensi file di `workbook.save("MyFile.xls")`. Aspose secara otomatis beralih ke format biner.

## Kesimpulan – Apa yang Telah Kita Capai

Kami telah **apply number format excel** pada kolom nilai moneter, mendemonstrasikan cara **apply currency style excel**, menunjukkan cara termudah untuk **create excel workbook java**, dan menggunakan Aspose.Cells untuk **import datatable to excel** tanpa menyentuh UI. Semua ini dilakukan dalam program singkat yang dapat Anda salin, tempel, dan jalankan.

Apa selanjutnya? Cobalah memperluas contoh ini:

- Tambahkan lebih banyak kolom (misalnya “Date”, “Description”) dan tetapkan style berbeda per kolom.
- Ekspor data yang sama ke CSV dan bandingkan bagaimana format angka hilang.
- Integrasikan kode ke dalam layanan Spring Boot yang mengembalikan workbook sebagai respons HTTP yang dapat diunduh.

Silakan bereksperimen, dan jika menemukan kendala, tinggalkan komentar di bawah. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menerapkan Style pada Sel Excel Menggunakan Aspose.Cells untuk Java - Panduan Lengkap](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Menggabungkan Sel & Menerapkan Style di Excel menggunakan Aspose.Cells untuk Java - Panduan Lengkap](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells untuk Java: Cara Membuat dan Memformat Workbook Excel secara Efisien](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}