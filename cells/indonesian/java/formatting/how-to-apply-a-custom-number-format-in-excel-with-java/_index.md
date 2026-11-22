---
category: general
date: 2026-11-22
description: Pelajari cara menggunakan format angka khusus untuk memformat kolom sebagai
  mata uang di Excel menggunakan Java. Atur format angka Excel dengan cepat menggunakan
  gaya sederhana.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: id
lastmod: 2026-11-22
og_description: Terapkan format angka khusus di Excel dengan Java. Tutorial ini menunjukkan
  cara mengatur format angka Excel dan memberi gaya pada kolom pertama sebagai mata
  uang.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Terapkan format angka khusus di Excel dengan Java – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Cara menerapkan format angka khusus di Excel dengan Java
url: /id/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menerapkan format angka khusus di Excel dengan Java

Jika Anda perlu **custom number format** sebuah kolom dalam lembar kerja Excel, panduan ini menunjukkan secara tepat cara melakukannya menggunakan Java. Baik Anda membuat laporan keuangan atau mengekspor data akuntansi, memformat kolom pertama sebagai mata uang membuat output langsung dapat dibaca.

Pada contoh di bawah ini kami akan **format column as currency**, menerapkan gaya ke kolom pertama, dan kemudian mengimpor `DataTable` ke dalam lembar kerja. Pendekatan yang sama berlaku untuk format numerik apa pun yang ingin Anda tampilkan.

## Apa yang akan Anda pelajari

* Cara membuat **custom number format** dengan objek `Style` Apache POI.  
* Cara **set Excel number format** untuk kolom tertentu, termasuk kasus **set currency format**.  
* Cara **style first column** saat mengimpor `DataTable`.  
* Cara menyimpan workbook dan memverifikasi bahwa format muncul dengan benar.

### Prasyarat

* Java 17 atau lebih baru.  
* Apache POI 5.x (perpustakaan yang menyediakan `Workbook`, `Worksheet`, dan `Style`).  
* Implementasi `DataTable` yang dapat diiterasi seperti pada contoh kode.  
* Familiaritas dasar dengan konsep Java dan Excel.

---

## Langkah 1: Siapkan proyek dan impor data

Pertama, tambahkan Apache POI ke proyek Anda. Jika Anda menggunakan Maven, sertakan dependensi berikut:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Selanjutnya, dapatkan data sumber sebagai `DataTable`. Dalam skenario dunia nyata ini mungkin berasal dari kueri basis data, file CSV, atau respons API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Pastikan kolom `DataTable` memiliki tipe Java yang tepat (`Integer`, `Double`, dll.) karena format angka hanya memengaruhi sel numerik.

---

## Langkah 2: Buat **custom number format** untuk kolom pertama

Sebuah **custom number format** memberi tahu Excel bagaimana menampilkan nilai numerik. Untuk menampilkan nilai sebagai mata uang kami menggunakan format bawaan `CURRENCY`, tetapi Anda juga dapat mendefinisikan pola seperti `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Mengapa ini berhasil:**  
* `createCellStyle()` mengembalikan objek gaya yang dapat digunakan kembali.  
* `setDataFormat()` menempelkan **set currency format** ke gaya, yang kemudian diterapkan Excel ke setiap sel yang menggunakan gaya ini.  
* Dengan menyimpan gaya di `columnStyles[0]` kami memastikan bahwa hanya kolom pertama yang menerima format mata uang.

---

## Langkah 3: Impor `DataTable` sambil menerapkan gaya kolom

Sekarang kami mengimpor data ke dalam lembar kerja. Metode `importDataTable` menerima array gaya, memungkinkan kami **style first column** dan membiarkan kolom lainnya dengan format default.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Pemanggilan di atas **sets Excel number format** hanya untuk kolom pertama. Semua kolom lain mewarisi gaya default workbook, yang membuat kode tetap sederhana dan efisien.

---

## Langkah 4: Simpan workbook dan verifikasi hasil

Akhirnya, tulis workbook ke file dan buka di Excel untuk memastikan bahwa kolom pertama menampilkan simbol mata uang.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Output yang diharapkan:**  
Saat Anda membuka *FormattedReport.xlsx*, nilai di kolom A muncul dengan simbol mata uang yang sesuai (mis., `$1,234.00`). Semua kolom lain mempertahankan representasi numerik aslinya.

---

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian |
|-----------|------------|
| **Mata uang berbeda** (mis., Euro) | Ganti `Style.CustomNumberFormat.CURRENCY` dengan pola khusus: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Lebih dari satu kolom yang bergaya** | Isi entri tambahan di `columnStyles[]` dengan objek `CellStyle` masing‑masing. |
| **Set data besar** | Gunakan `importDataTable` dalam batch atau alirkan baris untuk menghindari `OutOfMemoryError`. |
| **Pemisah khusus locale** | Gunakan `java.text.NumberFormat` untuk menghasilkan pola yang sadar locale dan berikan ke `setDataFormat`. |

> **Perhatikan:** Menggunakan kembali satu objek `CellStyle` di banyak kolom dapat menyebabkan format yang tidak terduga karena Excel membatasi jumlah gaya berbeda per workbook. Buat gaya terpisah untuk setiap format unik yang Anda butuhkan.

---

## Contoh lengkap yang dapat dijalankan

Berikut adalah program mandiri yang mendemonstrasikan seluruh alur kerja, mulai dari pembuatan data hingga menyimpan workbook yang diformat.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Menjalankan program akan membuat **FormattedReport.xlsx** dimana kolom A (kolom “Amount”) ditampilkan dengan **custom number format** yang menampilkan tanda dolar dan dua tempat desimal.

---

## Kesimpulan

Anda kini tahu cara **custom number format** lembar kerja Excel dari Java, **format column as currency**, dan **style first column** saat mengimpor data. Dengan membuat `CellStyle` yang dapat digunakan kembali dan meneruskannya ke `importDataTable`, Anda dapat **set Excel number format** untuk kolom mana pun tanpa harus melakukan loop pada setiap sel secara manual.

Next, try:

* Menggunakan `setDataFormat` dengan pola khusus locale untuk **set currency format**

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Set Number Format Excel di Java – Panduan Lengkap](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Terapkan Number Format Excel di Java – Panduan Lengkap Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Cara membuat workbook excel dengan format mata uang dan font tebal di Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}