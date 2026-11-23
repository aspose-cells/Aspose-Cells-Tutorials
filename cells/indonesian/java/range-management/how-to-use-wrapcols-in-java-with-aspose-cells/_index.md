---
category: general
date: 2026-11-22
description: Pelajari cara menggunakan wrapcols di Java untuk mengonversi rentang
  menjadi kolom menggunakan Aspose.Cells. Panduan ini menjelaskan fungsi wrap columns
  di Excel langkah demi langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: id
lastmod: 2026-11-22
og_description: Cara menggunakan wrapcols di Java untuk mengubah rentang menjadi kolom.
  Ikuti tutorial ini untuk menguasai fungsi wrap columns Excel dengan Aspose.Cells.
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: Cara menggunakan wrapcols di Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Cara menggunakan wrapcols di Java dengan Aspose.Cells
url: /id/java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan wrapcols di Java dengan Aspose.Cells

Jika Anda perlu **how to use wrapcols** untuk mengubah bentuk data dalam workbook Excel, tutorial ini menunjukkan proses lengkapnya. Anda akan melihat bagaimana rumus WRAPCOLS mengubah rentang vertikal menjadi sekumpulan kolom, memudahkan penyajian daftar berdampingan.

Panduan ini mencakup semua yang Anda perlukan: memuat workbook, menerapkan rumus WRAPCOLS, dan menyimpan hasilnya. Tidak ada referensi eksternal yang diperlukan, sehingga Anda dapat menyalin kode dan menjalankannya segera. Sepanjang jalan kami juga menjelaskan *wrap columns excel function* dan mendemonstrasikan cara **convert range to columns** untuk skenario pelaporan umum.

## Apa yang Anda butuhkan

- Java 17 atau lebih baru  
- Aspose.Cells for Java (versi terbaru)  
- IDE Java (IntelliJ IDEA, Eclipse, atau VS Code)  
- File Excel input (`input.xlsx`) yang berisi data di kolom A  

## Cara menggunakan wrapcols di Java dengan Aspose.Cells

Empat langkah berikut menerapkan alur kerja **how to use wrapcols**. Setiap langkah mencakup cuplikan kode, penjelasan mengapa langkah tersebut penting, dan tip untuk menghindari jebakan umum.

### Langkah 1: Muat workbook

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Mengapa langkah ini penting*: `Workbook` adalah titik masuk untuk semua operasi Excel di Aspose.Cells. Memuat file memberi Anda akses ke lembar kerja, sel, dan rumus.  

**Pro tip**: Gunakan path absolut selama pengembangan untuk menghindari `FileNotFoundException`. Beralih ke path relatif setelah proyek dipaketkan.

### Langkah 2: Akses lembar kerja pertama

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Lembar kerja pertama (`index 0`) biasanya berisi data yang ingin Anda ubah. Jika data Anda berada di lembar lain, ubah indeks atau gunakan `get("SheetName")`.  

**Mengapa langkah ini penting**: Bekerja dengan lembar kerja yang tepat memastikan rumus WRAPCOLS merujuk ke rentang yang dimaksud.

### Langkah 3: Tetapkan rumus WRAPCOLS

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` adalah **wrap columns excel function** yang mendistribusikan nilai dari `range` ke sejumlah kolom yang ditentukan. Dalam contoh ini kami mengambil nilai dari `A1:A10` dan membungkusnya menjadi tiga kolom, mulai dari `A1`.  

**Mengapa langkah ini penting**: Rumus melakukan pekerjaan berat—tidak diperlukan perulangan manual atau penanganan array.  

**Tip untuk convert range to columns**: Sesuaikan argumen kedua (`3`) dengan jumlah kolom yang Anda butuhkan. Jika panjang rentang bukan kelipatan jumlah kolom, kolom terakhir akan berisi item yang tersisa.

### Langkah 4: Simpan workbook

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Menyimpan menulis rumus WRAPCOLS ke dalam `output.xlsx`. Saat Anda membuka file di Excel, rumus akan dievaluasi dan menampilkan data yang dibungkus ke dalam kolom.  

**Mengapa langkah ini penting**: Menyimpan workbook memungkinkan Anda memverifikasi hasil dan membagikan file kepada pengguna non‑Java.

![Rumus Wrapcols diterapkan di Excel](wrapcols-example.png){: .align-center alt="Cara menggunakan wrapcols di screenshot Excel"}

### Output yang Diharapkan

Saat Anda membuka `output.xlsx`, sel `A1:C4` (atau sebanyak baris yang diperlukan) akan berisi daftar asli dari `A1:A10` yang tersebar ke tiga kolom. Tata letaknya seperti ini:

| A | B | C |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
| Item 10 |   |   |

**wrap columns excel function** secara otomatis mengisi sel kosong dengan kosong, sehingga Anda tidak memerlukan kode pembersihan tambahan.

## Memahami wrap columns excel function

Rumus WRAPCOLS merupakan bagian dari fungsi array dinamis Excel yang diperkenalkan di Excel 365. Ia bekerja mirip dengan `TEXTSPLIT` tetapi berfokus pada distribusi per kolom.  

- **Sintaks**: `=WRAPCOLS(source_range, columns)`  
- **Parameter**:  
  - `source_range` – rentang vertikal yang ingin Anda ubah bentuknya.  
  - `columns` – jumlah kolom untuk membungkus data ke dalamnya.  

Saat Anda memanggil `=WRAPCOLS(A1:A10, 3)`, Excel memperlakukan sumber sebagai array satu‑dimensi dan mengisi kolom pertama, kemudian kolom kedua, dan seterusnya, hingga semua nilai ditempatkan. Ini menjadikan **how to use wrapcols** alat yang sempurna untuk mengonversi daftar satu kolom menjadi laporan multi‑kolom tanpa VBA.

## Mengonversi rentang menjadi kolom tanpa rumus (opsional)

Jika Anda lebih suka melakukan operasi **convert range to columns** sepenuhnya di Java—tanpa bergantung pada mesin perhitungan Excel, Anda dapat membaca nilai sumber, membangun array dua‑dimensi, dan menuliskannya kembali secara manual:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

Cuplikan ini menunjukkan cara alternatif untuk **convert range to columns** ketika Anda membutuhkan kontrol penuh atas output (mis., menerapkan pemformatan khusus per kolom). Namun, menggunakan **wrap columns excel function** melalui WRAPCOLS biasanya lebih singkat dan membiarkan Excel menangani perhitungan ulang secara otomatis.

## Kasus tepi dan praktik terbaik

- **Sel kosong**: WRAPCOLS memperlakukan sel kosong sebagai kosong. Jika rentang sumber Anda berisi celah, output akan mempertahankan sel kosong tersebut.  
- **Rentang dinamis**: Gunakan rentang bernama atau referensi tabel (`Table1[Column]`) agar rumus menyesuaikan ketika baris ditambahkan.  
- **Kinerja**: Menerapkan rumus adalah O(1) karena Excel mengevaluasinya secara malas. Konversi programatik yang ditunjukkan di atas adalah O(n) dan mungkin lebih lambat untuk rentang yang sangat besar.  
- **Kompatibilitas versi**: Fungsi WRAPCOLS memerlukan Excel 365 atau yang lebih baru. Jika Anda perlu mendukung versi lama, gunakan metode konversi sisi Java.

## Cara menggunakan wrapcols dalam skenario lain

- **Dashboard pelaporan**: Mengubah daftar vertikal nama KPI menjadi tabel kompak dengan tiga kolom per baris.  
- **Formulir entri data**: Mengonversi kolom masukan pengguna menjadi tata letak berdampingan untuk perbandingan visual yang lebih mudah.  
- **Ekspor ke CSV**: Setelah menerapkan WRAPCOLS, simpan workbook sebagai CSV untuk mendapatkan tampilan terdelimit yang sesuai dengan tata letak kolom.

Setiap kasus ini mengikuti pola **how to use wrapcols** yang sama: muat, referensi, tetapkan rumus, simpan.

## Kesimpulan

Anda kini mengetahui **how to use wrapcols** di Java dengan Aspose.Cells untuk **convert range to columns** secara efisien. Dengan menerapkan rumus `WRAPCOLS` Anda memanfaatkan *wrap columns excel function* bawaan, menjaga kode tetap singkat sambil memberi Excel kontrol penuh atas perhitungan dan tampilan.

Cobalah dengan jumlah kolom yang berbeda, rentang dinamis, atau konversi opsional hanya di Java untuk menyesuaikan kebutuhan proyek Anda. Ketika Anda menguasai teknik ini, mengubah bentuk data di Excel menjadi operasi satu baris bukan tugas manual.

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to use wrapcols to convert a list into multiple columns in Java](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}