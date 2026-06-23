---
category: general
date: 2026-06-21
description: Cara menerapkan gaya saat mengonversi DataTable ke Excel dalam Java.
  Pelajari cara mengimpor DataTable ke Excel, menambahkan gaya khusus ke Excel, dan
  menyimpan workbook ke file dalam hitungan menit.
draft: false
keywords:
- how to apply styles
- convert datatable to excel
- save workbook to file
- add custom styles excel
- import datatable to excel
language: id
og_description: Cara menerapkan gaya saat mengonversi DataTable ke Excel dalam Java.
  Panduan ini menunjukkan cara mengimpor DataTable ke Excel, menambahkan gaya khusus
  ke Excel, dan menyimpan workbook ke file.
og_title: Cara Menerapkan Gaya Saat Mengonversi DataTable ke Excel – Tutorial Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  headline: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  type: TechArticle
- description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  name: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  steps:
  - name: 5.1 Conditional Formatting Instead of Fixed Styles
    text: If you need to highlight rows where `Score > 90`, you can add a `ConditionalFormattingCollection`
      after the import. This gives you dynamic coloring without hard‑coding extra
      styles.
  - name: 5.2 Merging Cells for Titles
    text: Sometimes a report needs a big title spanning multiple columns. Use `worksheet.getCells().merge(0,
      0, 1, 3)` and then apply a distinct style to that merged region.
  - name: 5.3 Large DataSets – Performance Considerations
    text: When dealing with >100k rows, set `ImportDataTableOptions` to `ImportDataTableOptions.NO_FORMATTING`
      first, then apply styles in a second pass. This avoids the overhead of styling
      each cell during import.
  - name: 5.4 Multi‑Sheet Export
    text: If you have several `DataTable`s, just create additional worksheets via
      `workbook.getWorksheets().add("Sheet2")` and repeat the **import datatable to
      excel** step for each sheet.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- DataTable
title: Cara Menerapkan Gaya Saat Mengonversi DataTable ke Excel – Panduan Java Lengkap
url: /id/java/formatting/how-to-apply-styles-when-converting-datatable-to-excel-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menerapkan Gaya Saat Mengonversi DataTable ke Excel – Panduan Lengkap Java

Pernah bertanya-tanya **bagaimana cara menerapkan gaya** ketika Anda perlu **mengonversi DataTable ke Excel**? Anda bukan satu-satunya. Dalam banyak alat internal kami mengambil data dari basis data, menaruhnya ke dalam `DataTable`, dan kemudian mengharapkan spreadsheet yang tampak cantik tanpa pekerjaan tambahan. Spoiler: Anda harus memberi tahu perpustakaan *tepat* apa arti “cantik”.

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan **bagaimana cara menerapkan gaya** menggunakan Aspose.Cells untuk Java, mengimpor `DataTable` ke Excel, **menambahkan gaya khusus ala excel**, dan akhirnya **menyimpan workbook ke file**. Pada akhir tutorial, Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek mana pun.

---

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru apa pun) – kode ini juga berfungsi pada Java 8+.  
- **Aspose.Cells for Java** JAR (versi percobaan gratis cukup untuk pengujian).  
- Sumber `DataTable` – kami akan membuat contoh sederhana, tetapi Anda dapat menggantinya dengan hasil kueri nyata apa pun.  
- IDE pilihan Anda (IntelliJ, Eclipse, VS Code… silakan pilih).

Tidak diperlukan alat build tambahan; sebuah `pom.xml` Maven sederhana sudah cukup, tetapi Anda juga dapat menambahkan JAR secara manual.

---

## Langkah 1: Siapkan Proyek dan Dependensi

Pertama-tama—mari kita menambahkan pustaka ke classpath.

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- check the latest version -->
    </dependency>
</dependencies>
```

Jika Anda tidak menggunakan Maven, cukup letakkan `aspose-cells-24.9.jar` ke dalam folder `libs` Anda dan tambahkan ke path build.

> **Pro tip:** Aspose menyediakan kelas `License`. Daftarkan lisensi Anda lebih awal, atau Anda akan melihat watermark pada file output.

```java
import com.aspose.cells.*;

public class ExcelExporter {
    static {
        try {
            License license = new License();
            license.setLicense("Aspose.Cells.lic"); // place your license file in resources
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
    }
    // …rest of the class
}
```

Sekarang kami siap membahas **bagaimana cara menerapkan gaya**.

---

## Langkah 2: Buat Gaya Kustom untuk Excel

Keajaiban spreadsheet yang rapi terletak pada gaya selnya. Aspose memungkinkan Anda mendefinisikan objek `Style`, menyesuaikan font, warna, border, dan kemudian menggunakannya kembali di mana saja. Di bawah ini adalah cara ringkas untuk **menambahkan gaya khusus secara keseluruhan di excel**.

```java
/**
 * Builds an array of two custom styles:
 * 1. Header style – bold, gray background, centered.
 * 2. Data style   – thin borders, left‑aligned.
 */
private static Style[] buildImportStyles(Workbook workbook) {
    // Header style
    Style headerStyle = workbook.createStyle();
    Font headerFont = headerStyle.getFont();
    headerFont.setBold(true);
    headerFont.setColor(Color.getWhite());
    headerStyle.setPattern(BackgroundType.SOLID);
    headerStyle.setBackgroundColor(Color.getGray25());
    headerStyle.setHorizontalAlignment(TextAlignmentType.CENTER);
    headerStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    // Data style
    Style dataStyle = workbook.createStyle();
    dataStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setHorizontalAlignment(TextAlignmentType.LEFT);
    dataStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    return new Style[] { headerStyle, dataStyle };
}
```

Perhatikan bagaimana kami membuat **dua gaya berbeda**—satu untuk judul kolom dan satu untuk baris data. Anda dapat memperluas array ini dengan sebanyak mungkin gaya yang Anda perlukan; Aspose akan menerapkannya secara berurutan ketika Anda memanggil `importDataTable`.

---

## Langkah 3: Impor DataTable ke Worksheet

Sekarang bagian yang sebenarnya **mengimpor datatable ke excel**. Metode `importDataTable` menerima `DataTable` sumber, sebuah flag untuk judul kolom, baris/kolom mulai, dan array gaya yang baru saja kami buat.

```java
public static void exportDataTableToExcel(DataTable dataTable, String outputPath) throws Exception {
    // 1️⃣ Create a new workbook and grab the first worksheet
    Workbook workbook = new Workbook();
    Worksheet worksheet = workbook.getWorksheets().get(0);

    // 2️⃣ Build the custom styles (header + data)
    Style[] importStyles = buildImportStyles(workbook);

    // 3️⃣ Import the DataTable – start at A1 (0,0), keep column names, apply styles
    worksheet.getCells().importDataTable(dataTable, true, 0, 0, importStyles);

    // 4️⃣ Auto‑fit columns for a tidy look
    worksheet.autoFitColumns();

    // 5️⃣ Finally, **save workbook to file**
    workbook.save(outputPath);
}
```

Catatan singkat: argumen `true` memberi tahu Aspose untuk **mempertahankan judul kolom**—itu adalah kasus umum ketika Anda menginginkan laporan yang dapat dibaca. Jika Anda mengaturnya ke `false`, baris data pertama akan menjadi header.

---

## Langkah 4: Sambungkan Semua – Contoh Minimal yang Berfungsi

Di bawah ini adalah metode `main` yang berdiri sendiri yang membuat `DataTable` tiruan, memanggil prosedur ekspor, dan menulis `output.xlsx` ke folder `./results`.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExporter {

    // (License block omitted for brevity – see Step 1)

    public static void main(String[] args) throws Exception {
        // Mock a DataTable – replace this with your real DB call
        DataTable dataTable = createSampleDataTable();

        // Define where the Excel file should land
        String outputPath = "results/output.xlsx";

        // Perform the conversion and styling
        exportDataTableToExcel(dataTable, outputPath);

        System.out.println("Excel file generated at: " + outputPath);
    }

    /** Helper that builds a simple DataTable with three columns */
    private static DataTable createSampleDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", CellValueType.INTEGER);
        dt.getColumns().add("Name", CellValueType.STRING);
        dt.getColumns().add("Score", CellValueType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[] {1, "Alice", 85.5});
        dt.getRows().add(new Object[] {2, "Bob", 92.0});
        dt.getRows().add(new Object[] {3, "Charlie", 78.3});
        return dt;
    }

    // (Style builder and export method from Steps 2‑3 go here)
}
```

**Output yang diharapkan:** Buka `output.xlsx` dan Anda akan melihat baris header tebal berwarna abu-abu, sel data dengan border tipis, dan kolom yang secara otomatis disesuaikan ukurannya agar cocok dengan konten. Itulah tepatnya **bagaimana cara menerapkan gaya** untuk membuat lembar terlihat profesional.

![Cara menerapkan gaya di workbook Excel](/images/excel-styles.png){alt="cara menerapkan gaya di workbook Excel"}

*(Tangkapan layar menunjukkan header berwarna abu-abu tebal dan baris data dengan border tipis.)*

---

## Langkah 5: Tips Lanjutan & Kasus Tepi

### 5.1 Pemformatan Bersyarat Alih-alih Gaya Tetap  
Jika Anda perlu menyorot baris di mana `Score > 90`, Anda dapat menambahkan `ConditionalFormattingCollection` setelah impor. Ini memberi Anda pewarnaan dinamis tanpa harus menulis gaya tambahan secara manual.

```java
FormatConditionCollection fcc = worksheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
fc.getStyle().setBackgroundColor(Color.getLightGreen());
```

### 5.2 Menggabungkan Sel untuk Judul  
Kadang-kadang laporan memerlukan judul besar yang membentang beberapa kolom. Gunakan `worksheet.getCells().merge(0, 0, 1, 3)` lalu terapkan gaya berbeda pada wilayah yang digabungkan tersebut.

### 5.3 Dataset Besar – Pertimbangan Kinerja  
Saat menangani >100k baris, setel `ImportDataTableOptions` ke `ImportDataTableOptions.NO_FORMATTING` terlebih dahulu, kemudian terapkan gaya pada proses kedua. Ini menghindari beban tambahan styling setiap sel selama impor.

### 5.4 Ekspor Multi‑Sheet  
Jika Anda memiliki beberapa `DataTable`, cukup buat worksheet tambahan melalui `workbook.getWorksheets().add("Sheet2")` dan ulangi langkah **import datatable to excel** untuk setiap sheet.

---

## Kesimpulan

Kami telah membahas **bagaimana cara menerapkan gaya** dari awal hingga akhir: menyiapkan Aspose.Cells, membangun **gaya khusus excel**, **mengimpor datatable ke excel**, dan akhirnya **menyimpan workbook ke file**. Contoh kode lengkap siap untuk disalin‑tempel, dan tips tambahan memberikan Anda panduan untuk laporan yang lebih canggih.

Selanjutnya, Anda mungkin ingin menjelajahi **menambahkan gaya khusus excel** untuk chart, atau bereksperimen dengan **mengonversi datatable ke excel** dalam endpoint REST Spring Boot. Bagaimanapun, Anda kini memiliki fondasi yang kuat untuk mengubah tabel mentah menjadi spreadsheet yang rapi—tanpa perlu format manual.

Ada pertanyaan

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menerapkan Gaya ke Sel Excel Menggunakan Aspose.Cells untuk Java - Panduan Lengkap](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Menggabungkan Sel & Menerapkan Gaya di Excel menggunakan Aspose.Cells untuk Java - Panduan Lengkap](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Cara Mengimpor DataTable ke Excel Menggunakan Aspose.Cells untuk .NET (Panduan Langkah demi Langkah)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}