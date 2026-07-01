---
category: general
date: 2026-06-30
description: Urutkan nilai unik di Excel menggunakan Java. Pelajari cara mengatur
  rumus, menghitung ulang rumus, dan menghasilkan daftar unik di Excel dengan Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: id
og_description: Urutkan nilai unik di Excel dengan Java. Panduan ini menunjukkan cara
  mengatur formula, menghitung ulang formula, dan menghasilkan daftar unik di Excel
  dalam hitungan menit.
og_title: Urutkan Nilai Unik di Excel – Tutorial Java untuk Rumus Array
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Mengurutkan Nilai Unik di Excel – Panduan Lengkap Java untuk Menetapkan Rumus
  Array
url: /id/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurutkan Nilai Unik di Excel – Panduan Java Lengkap untuk Menetapkan Formula Array

Pernah bertanya-tanya bagaimana cara **sort unique values Excel** tanpa menyeret formula? Anda bukan satu-satunya. Dalam banyak skenario pelaporan Anda memerlukan daftar bersih yang diurutkan secara alfabetik dari entri yang unik, dan melakukannya secara manual sangat merepotkan.  

Berita baik? Dengan beberapa baris kode Java Anda dapat **set array formula** pada lembar kerja, lalu **recalculate formulas** sehingga rentang yang spill terisi secara otomatis. Dalam tutorial ini kami akan membahas semuanya—dari membuat workbook hingga menghasilkan daftar unik gaya Excel—sehingga Anda dapat menyematkan solusi langsung ke dalam aplikasi Anda.

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan proyek Java dengan Aspose.Cells (perpustakaan yang mendukung potongan kode).  
- Menggunakan fungsi `SORT` dan `UNIQUE` bersama-sama untuk **menghasilkan daftar unik Excel**.  
- Menerapkan **array formula** ke sebuah sel secara programatis.  
- Memicu proses perhitungan sehingga langkah **how to recalculate formulas** terjadi secara instan.  
- Memverifikasi output dan menyesuaikan solusi untuk kasus tepi seperti sel kosong atau rentang yang tidak bersebelahan.

By the end of this guide you’ll be able to drop a ready‑to‑use method into any Java service that needs to export clean Excel sheets.

> **Pro tip:** Jika Anda sudah menggunakan Maven, menambahkan Aspose.Cells sebagai dependensi menghemat Anda dari menangani file JAR secara manual.

---

## Prasyarat

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 or newer | Aspose.Cells menargetkan Java 8+. |
| Maven (or Gradle) | Mempermudah manajemen dependensi. |
| Aspose.Cells for Java | Menyediakan `Workbook`, `Worksheet`, dan API formula yang akan kami gunakan. |
| Basic familiarity with Excel functions | Memahami `SORT` dan `UNIQUE` membantu Anda menyesuaikan kode. |

> *Jika Anda belum memiliki Aspose.Cells, tambahkan ini ke `pom.xml` Anda*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Langkah 1: Buat Workbook Baru (How to Set Formula Begins Here)

Pertama-tama kita memerlukan workbook kosong. Anggaplah itu sebagai kanvas kosong dimana nanti kita akan **set array formula** pada sel `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Mengapa membuat workbook baru?*  
> Itu menjamin lingkungan yang bersih, menghindari formula tersembunyi yang dapat mengganggu data uji kami.

---

## Langkah 2: Isi Data Contoh (Opsional tapi Membantu)

Untuk melihat hasil dengan jelas, mari isi kolom **B** dengan beberapa entri duplikat.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Mengapa menggunakan kolom B?*  
> Formula yang akan kami tulis merujuk ke `B1:B10`, jadi menempatkan data di sana mencerminkan contoh klasik Excel.

---

## Langkah 3: Tetapkan Array Formula yang **Sort Unique Values Excel**

Sekarang keajaiban terjadi. Kami menggabungkan `UNIQUE` (untuk menghapus duplikat) dengan `SORT` (untuk mengurutkannya secara alfabetik). Ekspresi yang dihasilkan adalah **array formula**, yang berarti ia akan spill ke sel-sel tetangga secara otomatis.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Cara Kerjanya

- `UNIQUE(B1:B10)` memindai rentang dan mengembalikan array vertikal dari string yang berbeda.  
- `SORT(...)` mengambil array tersebut dan mengurutkannya dalam urutan naik.  
- Membungkus semuanya dengan `=` dan memanggil `setFormulaArray` memberi tahu Aspose.Cells untuk memperlakukan hasil sebagai **spilled array**, seperti yang dilakukan Excel.

> **Catatan:** Jika Anda menggunakan versi Excel yang lebih lama dan tidak memiliki `SORT` atau `UNIQUE`, Anda dapat kembali ke `SORT(UNIQUE(...))` dengan fungsi **LET** atau menggunakan formula array legacy (`=INDEX(...)`). Tutorial ini fokus pada pendekatan array dinamis modern karena ini cara paling bersih untuk **generate unique list Excel** saat ini.

---

## Langkah 4: Hitung Ulang Formula Agar Rentang yang Spill Terisi

Setelah formula ditempatkan, workbook tidak secara otomatis mengevaluasinya. Di sinilah langkah **how to recalculate formulas** berperan.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Memanggil `calculateFormula()` memaksa Aspose.Cells menjalankan mesin Excel, mengisi sel `A1`, `A2`, … dengan nilai unik yang sudah diurutkan.

> *Mengapa tidak mengandalkan evaluasi malas?*  
> Dalam konteks sisi‑server Anda sering memerlukan data siap untuk diekspor (CSV, PDF, dll.) segera setelah perhitungan, sehingga panggilan eksplisit menjamin konsistensi.

---

## Langkah 5: Verifikasi Hasil (Debugging Opsional)

Selalu merupakan ide yang baik untuk mencetak nilai yang spill ke konsol—terutama ketika Anda belajar API baru.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Menjalankan program mencetak:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Buka `SortedUniqueValues.xlsx` dan Anda akan melihat data yang sama spill dari `A1` ke bawah.

---

## Menangani Kasus Tepi

### Sel Kosong dalam Rentang Sumber

Jika `B1:B10` berisi sel kosong, `UNIQUE` akan memperlakukannya sebagai entri terpisah. Untuk mengabaikan sel kosong, bungkus rentang dengan `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Data Tidak Kontigu

Ketika data Anda berada di beberapa kolom, Anda dapat menggabungkannya dengan `CHOOSE` atau `TEXTJOIN` sebelum menerapkan `UNIQUE`. Misalnya:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Penyesuaian ini menunjukkan fleksibilitas **how to set formula** untuk skenario yang lebih kompleks.

---

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabungkan)

Berikut adalah program Java lengkap yang dapat dijalankan. Salin‑tempel ke IDE Anda, tambahkan dependensi Aspose.Cells, dan tekan *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Output yang diharapkan** (ditampilkan di konsol) cocok dengan daftar yang diurutkan dan deduplikasi yang kami bahas sebelumnya. Membuka file Excel yang dihasilkan memperlihatkan nilai yang sama spill dari `A1` ke bawah.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan versi Excel yang lebih lama (sebelum Office 365)?**  
A: Fungsi `SORT` dan `UNIQUE` merupakan bagian dari mesin Dynamic Array yang diperkenalkan di Excel 365. Untuk file legacy Anda perlu menggunakan formula array klasik seperti `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells masih dapat mengevaluasinya, tetapi sintaksnya lebih panjang.

**Q: Bisakah saya menetapkan array formula pada rentang selain `A1`?**  
A: Tentu saja. Cukup ubah alamat di `cells.get("A1")`. Array yang spill akan selalu mulai dari sel yang Anda tentukan dan memperluas ke kanan‑dan‑bawah sesuai kebutuhan.

**Q: Bagaimana jika data sumber saya lebih besar dari `B1:B10`?**  
A: Ganti rentang statis dengan rentang dinamis, misalnya `B:B` atau named range. Formula menjadi `=SORT(UNIQUE(B:B))`. Hati-hati dengan referensi seluruh kolom pada lembar yang sangat besar; hal itu dapat memengaruhi kinerja.

---

## Kesimpulan

Kami baru saja membahas **how to set formula** dalam Java untuk **sort unique values Excel**, cara **recalculate formulas**, dan cara **generate unique list Excel** menggunakan API kuat Aspose.Cells. Langkah‑langkahnya sederhana: buat workbook, isi data, terapkan array formula, jalankan perhitungan, dan verifikasi hasil.  

Dari sini Anda dapat memperluas—menambahkan conditional formatting, mengekspor ke PDF, atau mengintegrasikan metode ke layanan web yang menyediakan laporan siap pakai. Ide dasarnya tetap sama: biarkan fungsi Excel melakukan pekerjaan berat, dan biarkan Java mengatur prosesnya.  

Siap meningkatkan otomatisasi Excel Anda? Coba ganti `SORT` dengan `SORTBY` untuk mengurutkan berdasarkan kolom sekunder, atau bereksperimen dengan `FILTER` untuk mengecualikan baris yang tidak memenuhi aturan bisnis. Kemungkinannya hampir tak terbatas.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}