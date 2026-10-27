---
category: general
date: 2026-07-03
description: Sertakan ekspor rumus dalam Java untuk mengonversi sel Excel menjadi
  teks menggunakan Aspose.Cells. Pelajari cara mencetak rentang Excel dan mendapatkan
  string nilai sel secara efisien.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: id
og_description: Sertakan ekspor formula dalam Java untuk mengonversi sel Excel menjadi
  teks. Panduan langkah demi langkah yang menunjukkan cara mencetak rentang Excel
  dan mengambil nilai sel sebagai string.
og_title: Sertakan Ekspor Rumus di Java – Ubah Sel Excel menjadi Teks
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Sertakan Ekspor Rumus di Java – Konversi Sel Excel ke Teks
url: /id/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sertakan Ekspor Rumus di Java – Mengonversi Sel Excel ke Teks

Pernah membutuhkan **include formulas export** saat mengambil data dari workbook Excel? Mungkin Anda sedang membangun layanan pelaporan yang harus mempertahankan rumus asli sambil tetap memberikan teks yang rapi. Jika demikian, Anda berada di tempat yang tepat. Panduan ini akan memandu Anda mengonversi sel Excel menjadi teks biasa—*termasuk* rumus yang tertanam—menggunakan Aspose.Cells untuk Java.

Kami juga akan membahas cara **print Excel range**, menyesuaikan **export table options**, dan akhirnya **get cell values string** yang dapat Anda log, kirim melalui API, atau simpan di basis data. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dijalankan sepenuhnya dan pemahaman yang kuat tentang alasan di balik setiap pemanggilan.

## Apa yang Akan Anda Dapatkan

- Program Java lengkap yang siap disalin‑tempel yang membaca file `.xlsx`, memilih rentang, dan mengekspornya sebagai string terformat.
- Pemahaman tentang kelas `ExportTableOptions` dan mengapa mengaktifkan `setExportAsString` dan `setIncludeFormula` penting.
- Tips untuk menangani lembar kerja besar, mengelola berbagai tipe data, dan menyesuaikan format output.
- Daftar periksa cepat untuk jebakan umum (misalnya sel yang digabung, baris tersembunyi, dan format angka spesifik locale).

### Prasyarat

- Java 17 atau lebih baru (kode dapat dikompilasi dengan versi lebih lama tetapi kami akan menggunakan LTS terbaru).
- Aspose.Cells untuk Java 23.10 (atau rilis terbaru lainnya)—Anda dapat mengunduhnya dari Maven Central.
- Sebuah contoh `input.xlsx` yang ditempatkan di folder yang Anda kontrol (jalur di‑hard‑code dalam contoh untuk kejelasan).

Jika Anda sudah memiliki semuanya, mari kita mulai.

## Langkah 1: Siapkan Proyek dan Tambahkan Dependensi

Pertama, buat proyek Maven (atau Gradle, jika Anda lebih suka). Tambahkan dependensi Aspose.Cells ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** Jika Anda menggunakan proxy perusahaan, pastikan repositori dapat dijangkau; jika tidak, proses build akan gagal dengan error “Could not resolve dependencies”.

Setelah Maven selesai mengunduh, Anda siap menulis kode Java.

## Langkah 2: Muat Workbook dan Ambil Worksheet yang Diinginkan

Baris pertama contoh kode menunjukkan cara membuka workbook yang sudah ada:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif ke file Anda. Konstruktor `Workbook` secara otomatis mendeteksi format file (XLS, XLSX, CSV, dll.), jadi Anda tidak perlu menyebutkannya.

Selanjutnya, kami mengambil sheet pertama:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Mengapa sheet pertama? Pada banyak templat data berada di tab pertama, tetapi Anda dapat memberikan indeks apa pun atau bahkan menggunakan `get("SheetName")` jika Anda lebih suka pendekatan berbasis nama.

## Langkah 3: Tentukan Rentang yang Ingin Anda Ekspor

Sekarang tiba pada inti operasi **convert excel cells text**. Anda memberi tahu Aspose.Cells sel mana yang akan diambil dengan membuat objek `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

String `"A1:C3"` adalah alamat gaya A1 klasik. Itu juga dapat dibangun secara programatis:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Fleksibilitas itu membantu ketika ukuran rentang bersifat dinamis—misalnya, Anda membaca baris terakhir yang digunakan dengan `ws.getCells().getMaxDataRow()`.

## Langkah 4: Konfigurasikan Export Table Options untuk Menyertakan Rumus

Di sinilah keajaiban **include formulas export** berada. Secara default, Aspose.Cells mengembalikan nilai *yang ditampilkan*. Jika sebuah sel berisi `=SUM(A1:A3)`, Anda akan mendapatkan angka yang dihitung, bukan teks rumus. Untuk mengubahnya, siapkan `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Mengapa kedua flag? `setExportAsString(true)` memberi tahu API untuk menggabungkan sel menggunakan pemisah default (tab untuk kolom, baris baru untuk baris). `setIncludeFormula(true)` mengubah sumber nilai dari “nilai yang ditampilkan” menjadi “rumus mentah”. Jika Anda hanya menginginkan nilai, biarkan `false`.

### Penyesuaian Opsional

- `eto.setExportHiddenRows(true);` – sertakan baris yang disembunyikan di Excel.
- `eto.setExportHiddenColumns(true);` – sama untuk kolom.
- `eto.setExportAsHTML(true);` – dapatkan HTML alih-alih teks biasa.

Silakan bereksperimen; kelas opsi ini adalah **export table options** playground.

## Langkah 5: Ambil Rentang sebagai String Terformat

Sekarang kami mengambil data:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

String `txt` yang dikembalikan terlihat seperti ini (asumsi A1:C3 berisi campuran nilai dan rumus):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Perhatikan tab (`\t`) yang memisahkan kolom dan baris baru (`\n`) yang memisahkan baris. Anda dapat memisahkan string nanti jika membutuhkan array 2‑D:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Langkah 6: Cetak Hasil – “Print Excel Range” Jadi Sederhana

Akhirnya, kami menuliskan string ke konsol:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Menjalankan program mencetak output persis seperti yang ditunjukkan di atas. Dari sini Anda dapat menulis string ke file log, mengirimnya lewat HTTP, atau menyimpannya dalam dokumen NoSQL.

## Contoh Lengkap yang Siap Dijalan

Menggabungkan semuanya, berikut program lengkapnya. Salin, tempel, dan tekan **Run**—tanpa impor yang hilang.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Output yang Diharapkan (contoh)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Jika workbook Anda berisi angka yang diformat sebagai tanggal, mereka akan muncul dalam format spesifik locale (mis., `2026‑07‑03`). Untuk memaksa tanggal ISO, Anda dapat menyesuaikan `ExportTableOptions` dengan `NumberFormat` khusus.

## Menangani Kasus Edge dan Pertanyaan Umum

### Jika rentang berisi sel yang digabung?

Sel yang digabung diperlakukan sebagai nilai sel paling kiri atas. Sisa area yang digabung akan muncul sebagai string kosong. Jika Anda membutuhkan alamat wilayah yang digabung, query `Cell.getMergedRange()` sebelum mengekspor.

### Bisakah saya mengekspor sheet besar (ratusan ribu baris)?

Ya, tetapi perhatikan konsumsi memori. Gunakan `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` agar Aspose.Cells mengalirkan data ke disk. Juga, pertimbangkan mengekspor dalam potongan (mis., 10 000 baris sekaligus) agar string tetap dapat dikelola.

### Bagaimana cara mengubah pemisah kolom?

`ExportTableOptions` menyediakan `setSeparator(char separator)`. Untuk output gaya CSV, setel menjadi `','`:

```java
eto.setSeparator(',');
```

### Apakah rumus menghormati referensi eksternal?

Jika sebuah rumus mengacu ke workbook lain, Aspose.Cells akan mempertahankan teks referensi (`='[Other.xlsx]Sheet1'!A1`). Ia tidak akan mengevaluasi nilai eksternal kecuali Anda memuat workbook tersebut juga.

## Pro Tips untuk Kode Siap Produksi

- **Cache workbook** jika Anda membaca the

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat dan Mengekspor Excel ke HTML Menggunakan Aspose.Cells Java \| Panduan Operasi Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Cara Mengonversi Excel ke PDF di Java Menggunakan Aspose.Cells: Panduan Langkah demi Langkah](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Ekspor Workbook Excel sebagai Gambar Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}