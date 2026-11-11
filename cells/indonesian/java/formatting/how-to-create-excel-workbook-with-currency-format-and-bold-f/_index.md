---
category: general
date: 2026-08-20
description: Buat workbook Excel di Java menggunakan Aspose.Cells, atur format mata
  uang, tambahkan font tebal, dan impor array gaya untuk sel yang bergaya.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: id
lastmod: 2026-08-20
og_description: Buat buku kerja Excel di Java, atur format mata uang, tambahkan huruf
  tebal, dan pelajari cara mengimpor gaya menggunakan Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Buat workbook Excel dengan sel mata uang yang bergaya di Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Cara membuat workbook Excel dengan format mata uang dan huruf tebal di Java
url: /id/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat workbook Excel dengan format mata uang dan huruf tebal di Java

Jika Anda perlu **membuat workbook excel** secara programatis, panduan ini menunjukkan secara tepat cara melakukannya. Kami akan menjelaskan cara membuat workbook, menerapkan format mata uang, menambahkan huruf tebal, dan menggunakan fitur **how to import style** Aspose.Cells sehingga setiap sel yang diimpor terlihat konsisten.

Anda akan selesai dengan file `DataTableWithStyleArray.xlsx` siap pakai yang menampilkan angka sebagai dolar dan menyorotnya dengan huruf tebal. Tidak diperlukan pemformatan manual di Excel.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

- Java 17 atau yang lebih baru terpasang.
- Lisensi Aspose.Cells untuk Java (atau kunci evaluasi gratis).
- Maven atau Gradle untuk mengelola dependensi `aspose-cells`.
- Pemahaman dasar tentang koleksi Java dan `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Tip pro:** Jika Anda mengalami `LicenseException`, letakkan file lisensi Anda di classpath dan panggil `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` sebelum membuat workbook.

## Cara membuat workbook excel dengan sel mata uang bergaya

Bagian ini berisi langkah‑langkah inti. Setiap langkah menjelaskan **mengapa** itu penting, bukan hanya **apa** yang harus diketik.

### Langkah 1: Inisialisasi workbook dan worksheet

Membuat workbook baru memberi Anda wadah bersih untuk semua pemformatan selanjutnya.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Mengapa:** Objek `Workbook` mewakili seluruh file Excel. Mengakses `Worksheet` pertama memungkinkan Anda mulai mengisi data secara langsung.

### Langkah 2: Bangun DataTable dengan data numerik

`DataTable` meniru tabel basis data, memudahkan impor baris secara massal.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Mengapa:** Menggunakan `DOUBLE` menjamin nilai mempertahankan presisi desimal, yang penting ketika Anda kemudian **format cells currency**.

### Langkah 3: Definisikan gaya – format mata uang dan huruf tebal

Di sini kami **menetapkan format mata uang** dan **menambahkan huruf tebal** ke objek `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Mengapa:** String format `Number` `$#,##0.00` memberi tahu Excel untuk memperlakukan sel sebagai nilai moneter, sementara `setBold(true)` menonjolkan angka. Menempatkan gaya dalam array mempersiapkan kami untuk langkah **how to import style**.

### Langkah 4: Konfigurasikan opsi impor untuk menggunakan array gaya

Aspose.Cells memungkinkan Anda mengirim `Style[]` melalui `ImportTableOptions`. Ini adalah metode resmi **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Mengapa:** Tanpa `ImportTableOptions`, sel yang diimpor akan mewarisi gaya default, kehilangan format mata uang dan ketebalan huruf yang telah kami definisikan.

### Langkah 5: Impor DataTable ke worksheet

Sekarang kami memasukkan data ke lembar pada sel `A1`, secara otomatis menerapkan array gaya.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` menunjukkan bahwa baris pertama `DataTable` berisi header kolom.
- `"A1"` adalah sudut kiri‑atas tempat impor dimulai.

> **Mengapa:** Mengimpor dengan array gaya menjamin setiap sel yang diimpor menerima gaya **format cells currency** yang telah kami siapkan sebelumnya.

### Langkah 6: Simpan workbook ke disk

Akhirnya, tulis workbook yang berada di memori ke file fisik.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Mengapa:** Menyimpan mempertahankan pemformatan, memungkinkan Anda atau proses selanjutnya membuka file di Excel dengan tampilan yang diinginkan.

## Kode sumber lengkap

Berikut adalah kelas Java lengkap yang siap dijalankan. Salin ke IDE Anda, ganti `YOUR_DIRECTORY` dengan folder yang ada, dan jalankan.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Output yang diharapkan

Saat Anda membuka `DataTableWithStyleArray.xlsx` di Microsoft Excel, Anda akan melihat:

| Amount |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Angka ditampilkan dengan **format mata uang** (simbol `$`, dua tempat desimal).
- Font untuk kedua sel adalah **tebal**, sehingga menonjol.

## Variasi umum dan kasus tepi

| Skenario | Apa yang diubah | Alasan |
|----------|----------------|--------|
| **Mata uang berbeda** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Gunakan simbol Euro atau format spesifik locale apa pun. |
| **Beberapa kolom dengan gaya berbeda** | Buat beberapa objek `Style`, isi `styleArray` dalam urutan yang sama dengan kolom. | Setiap kolom dapat memiliki format angka, font, latar belakang, dll. masing‑masing. |
| **Set data besar** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Meningkatkan kinerja dengan melewatkan baris header atau metadata yang tidak diperlukan. |
| **Menerapkan gaya setelah impor** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | Berguna ketika hanya sebagian baris yang memerlukan pemformatan khusus. |

## Tips untuk penggunaan produksi

- **Lisensi lebih awal**: Daftarkan lisensi Aspose.Cells Anda sebelum membuat workbook untuk menghindari watermark evaluasi.
- **Keamanan thread**: Instance `Workbook` **tidak** thread‑safe. Buat instance terpisah per thread jika Anda menghasilkan banyak file secara bersamaan.
- **Manajemen memori**: Untuk lembar sangat besar, pertimbangkan menggunakan API streaming `Workbook` (`Workbook` → `WorkbookDesigner`) untuk menjaga penggunaan memori tetap rendah.
- **Pengujian**: Sertakan unit test yang membuka file yang disimpan dengan Apache POI dan memastikan format nomor gaya sel cocok dengan `"$#,##0.00"`.

## Kesimpulan

Anda sekarang tahu cara **membuat workbook excel** di Java, **menetapkan format mata uang**, **menambahkan huruf tebal**, dan dengan benar **how to import style** menggunakan `ImportTableOptions` Aspose.Cells. Solusi menyeluruh ini menghilangkan langkah manual di Excel dan menjamin setiap sel yang diimpor mengikuti gaya **format cells currency** yang sama.

Siap untuk tantangan berikutnya? Coba tambahkan pemformatan bersyarat, menyematkan diagram, atau mengekspor workbook ke PDF—semua sambil kembali menggunakan teknik style‑array yang sama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Excel menggunakan Aspose.Cells di Java: Panduan Langkah demi Langkah](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Cara Membuat & Memformat Sel Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Cara Menata Sel Excel dan Menambahkan Hyperlink Menggunakan Aspose.Cells untuk Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}