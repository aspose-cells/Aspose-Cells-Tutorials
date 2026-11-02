---
category: general
date: 2026-06-18
description: Atur format angka Excel menggunakan Java dan pelajari notasi ilmiah Java,
  tulis nilai ke sel, atur digit signifikan, dan ekspor data ke XLSX dalam hitungan
  menit.
draft: false
keywords:
- set number format excel
- scientific notation java
- write value to cell
- set significant digits
- export data to xlsx
language: id
og_description: Atur format angka Excel dengan Java. Pelajari cara menggunakan notasi
  ilmiah di Java, menulis nilai ke sel, mengatur digit signifikan, dan mengekspor
  data ke xlsx secara efisien.
og_title: Mengatur Format Angka Excel di Java – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  headline: Set Number Format Excel in Java – Complete Guide
  type: TechArticle
- description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  name: Set Number Format Excel in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '| A (Formatted) | |---------------| | 1.235E7 |'
  - name: How do I change the number of significant digits?
    text: Just edit the format string. For three digits use `"0.###E0"`; for six digits
      use `"0.######E0"`.
  - name: What if I need a different locale (comma as decimal separator)?
    text: Add a locale‑aware format, e.g., `df.getFormat("0,####E0")`. Excel respects
      the user’s regional settings, so the comma will appear only if the workbook
      is opened on a system that uses it.
  - name: Can I apply the same style to an entire column?
    text: Absolutely. Create the style once (as shown) and then loop through rows,
      applying `cell.setCellStyle(sciStyle)` each time. For large sheets, consider
      using `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – it’s faster and
      keeps the code tidy.
  - name: What if I’m stuck with an older Java version that doesn’t support `var`?
    text: Replace `var` with the explicit type (`Workbook workbook = new XSSFWorkbook();`).
      The rest of the code stays identical.
  type: HowTo
tags:
- Java
- Excel
- Data Export
title: Mengatur Format Angka Excel di Java – Panduan Lengkap
url: /id/java/formatting/set-number-format-excel-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Number Format Excel di Java – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **set number format Excel** dari program Java tanpa membuat rambut rontok? Anda bukan satu-satunya. Baik Anda menghasilkan laporan keuangan atau mengekspor log sensor, menampilkan angka-angka besar dengan rapi dalam file *.xlsx* adalah keterampilan yang wajib dimiliki.

Dalam tutorial ini kita akan membahas solusi praktis end‑to‑end: membuat workbook, mengonfigurasi **scientific notation java**, membatasi **set significant digits**, menulis nilai ke sel, dan akhirnya **export data to xlsx**. Pada akhir tutorial Anda akan memiliki potongan kode mandiri yang dapat langsung dimasukkan ke proyek Anda.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi workbook dengan JExcel‑API (atau Apache POI) di Java.  
- Pemanggilan tepat untuk **set number format excel** agar memaksa notasi ilmiah.  
- Cara **write value to cell** sambil mempertahankan presisi.  
- Menyesuaikan pengaturan workbook untuk **set significant digits** ke jumlah khusus.  
- Menyimpan file sehingga dapat dibuka di aplikasi spreadsheet modern apa pun (**export data to xlsx**).  

Tidak ada layanan eksternal, tidak ada sulap. Hanya Java murni dan beberapa kelas yang terdokumentasi dengan baik.

---

## Prasyarat

- JDK 17 atau lebih baru (kode ini juga berfungsi pada versi lama, tetapi contoh menggunakan sintaks `var` modern untuk singkat).  
- Maven atau Gradle untuk mengambil dependensi `org.apache.poi:poi-ooxml`.  
- Pemahaman dasar tentang koleksi Java – jika Anda pernah menulis loop `for`, Anda sudah cukup.

---

## Langkah 1: Tambahkan Dependensi Apache POI

Jika Anda menggunakan Maven, tempelkan ini ke dalam `pom.xml` Anda. Pengguna Gradle dapat menerjemahkannya ke sintaks `implementation`.

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

> **Pro tip:** Keep POI up‑to‑date. The 5.x line adds better support for number formats and large worksheets.

---

## Langkah 2: Buat Workbook dan Akses Pengaturannya  

Hal pertama yang kita butuhkan adalah objek workbook baru. Apache POI tidak menyediakan kelas `WorkbookSettings` seperti JExcel, tetapi kita dapat mencapai efek yang sama dengan membuat `CellStyle` nanti.

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.Workbook;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise a new workbook (this is where we "set number format excel")
        Workbook workbook = new XSSFWorkbook();   // XSSFWorkbook -> .xlsx format
        // No explicit WorkbookSettings, we'll configure a CellStyle later
```

Mengapa kita memulai dengan **new workbook**? Anggaplah sebagai kanvas kosong; setiap keputusan pemformatan yang kita buat nanti akan diterapkan pada kanvas ini.  

---

## Langkah 3: Definisikan CellStyle untuk Notasi Ilmiah dan Digit Signifikan  

Apache POI memungkinkan Anda membuat string format data. Untuk menegakkan **scientific notation java** dan membatasi jumlah digit, kita menggunakan pola `"0.####E0"` – simbol `#` mengontrol berapa banyak digit signifikan yang muncul.

```java
import org.apache.poi.ss.usermodel.CellStyle;
import org.apache.poi.ss.usermodel.DataFormat;

// Inside main(), after workbook creation:
DataFormat df = workbook.createDataFormat();
CellStyle sciStyle = workbook.createCellStyle();

// "0.####E0" -> 0 before the decimal, up to 4 significant digits after, exponent part
sciStyle.setDataFormat(df.getFormat("0.####E0"));
```

*Apa yang terjadi di sini?* Format tersebut memberi tahu Excel: “Tampilkan angka dalam notasi ilmiah, tetapi hanya pertahankan hingga empat digit signifikan.” Jika Anda membutuhkan presisi berbeda, cukup tambahkan atau hapus simbol `#`.  

---

## Langkah 4: Tulis Angka Besar ke Sel  

Sekarang kita akan **write value to cell** *A1* menggunakan gaya yang baru saja kita buat. Objek `Sheet` dan `Row` ringan, jadi membuatnya secara dinamis tidak memakan biaya.

```java
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Cell;

// Continue inside main():
Sheet sheet = workbook.createSheet("Numbers");

// Row 0 (first row), Cell 0 (column A)
Row row = sheet.createRow(0);
Cell cell = row.createCell(0);
cell.setCellValue(12345678.9);   // The raw value we want to store
cell.setCellStyle(sciStyle);    // Apply our scientific notation style
```

Perhatikan bahwa kita tidak perlu meng-cast angka; POI menangani `double` secara otomatis. Dengan melampirkan `sciStyle`, kita menjamin bahwa ketika pengguna membuka file, Excel akan menampilkan `1.235E7` (dibulatkan ke empat digit signifikan) alih‑alih string mentah 8‑digit.

---

## Langkah 5: Simpan Workbook – Export Data ke XLSX  

Langkah terakhir adalah **export data to xlsx**. Kami akan menulis workbook ke file di direktori saat ini, tetapi Anda dapat menujuk ke lokasi mana pun yang Anda inginkan.

```java
import java.io.FileOutputStream;

// Still inside main():
try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
    workbook.write(out);
}
workbook.close();   // Free resources
System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Saat Anda double‑click `sigDigits.xlsx`, Anda akan melihat kolom **A** menampilkan `1.235E7` – persis seperti yang kami minta.

### Expected Output

| A (Formatted) |
|---------------|
| 1.235E7       |

Jika Anda membuka file dan mengubah format sel secara manual, Anda akan melihat nilai dasar tetap `12345678.9`. Itulah keajaiban **set number format excel**: tampilan berubah, data tetap murni.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana cara mengubah jumlah digit signifikan?

Cukup edit string format. Untuk tiga digit gunakan `"0.###E0"`; untuk enam digit gunakan `"0.######E0"`.

### Bagaimana jika saya membutuhkan locale berbeda (koma sebagai pemisah desimal)?

Tambahkan format yang sadar locale, mis., `df.getFormat("0,####E0")`. Excel menghormati pengaturan regional pengguna, sehingga koma akan muncul hanya jika workbook dibuka pada sistem yang menggunakannya.

### Bisakah saya menerapkan gaya yang sama ke seluruh kolom?

Tentu saja. Buat gaya sekali (seperti yang ditunjukkan) lalu loop melalui baris, menerapkan `cell.setCellStyle(sciStyle)` setiap kali. Untuk lembar besar, pertimbangkan menggunakan `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – lebih cepat dan menjaga kode tetap rapi.

### Bagaimana jika saya terpaksa menggunakan versi Java lama yang tidak mendukung `var`?

Ganti `var` dengan tipe eksplisit (`Workbook workbook = new XSSFWorkbook();`). Sisanya tetap identik.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.*;

import java.io.FileOutputStream;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (set number format excel)
        Workbook workbook = new XSSFWorkbook();

        // Define a style for scientific notation with 4 significant digits
        DataFormat df = workbook.createDataFormat();
        CellStyle sciStyle = workbook.createCellStyle();
        sciStyle.setDataFormat(df.getFormat("0.####E0")); // set significant digits

        // Access the first worksheet and write a large number into cell A1
        Sheet sheet = workbook.createSheet("Numbers");
        Row row = sheet.createRow(0);
        Cell cell = row.createCell(0);
        cell.setCellValue(12345678.9);   // write value to cell
        cell.setCellStyle(sciStyle);    // apply scientific notation

        // Save the workbook – export data to xlsx
        try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
            workbook.write(out);
        }
        workbook.close();

        System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Jalankan kelas, buka `sigDigits.xlsx`, dan Anda akan melihat angka ditampilkan dalam notasi ilmiah dengan tepat empat digit signifikan. Itulah seluruh alur kerja **set number format excel** di Java.

---

## Kesimpulan

Kami baru saja membahas semua yang Anda perlukan untuk **set number format excel** dari Java: membuat workbook, merancang gaya notasi ilmiah yang **set significant digits**, **write value to cell**, dan akhirnya **export data to xlsx**. Pendekatannya ringan, hanya menggunakan Apache POI, dan berfungsi di platform apa pun yang mendukung Java.

Selanjutnya, Anda mungkin ingin:

- Tambahkan pemformatan bersyarat untuk menyoroti nilai di luar rentang.  
- Hasilkan beberapa lembar dengan gaya numerik berbeda (mis., mata uang vs. ilmiah).  
- Stream dataset besar dengan `SXSSFWorkbook` untuk ekspor yang efisien memori.

Cobalah itu, dan Anda akan menjadi orang yang diandalkan untuk otomatisasi Excel di tim Anda. Ada pertanyaan atau kasus penggunaan yang unik? Tinggalkan komentar di bawah—selamat coding! 

*Gambar yang menggambarkan alur kerja (alt text: “set number format excel workflow diagram showing Java code, scientific notation, and export to xlsx”)*


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/german/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/french/java/cell-operations/aspose-cells-java-set-active-cell-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}