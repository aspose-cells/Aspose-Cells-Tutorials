---
category: general
date: 2026-06-21
description: Pelajari cara menggunakan expand di Java untuk memperluas array menjadi
  baris, menulis kode rumus Excel, dan menyimpan file Excel gaya Java—semua dalam
  satu tutorial.
draft: false
keywords:
- how to use expand
- expand array to rows
- write excel formula code
- save excel file java
language: id
og_description: Cara menggunakan expand di Java untuk memanipulasi data Excel, memperluas
  array menjadi baris, menulis kode rumus Excel, dan menyimpan file Excel dengan Java.
og_title: Cara Menggunakan Expand di Java – Panduan Lengkap Excel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  headline: How to Use Expand in Java – Complete Excel Guide
  type: TechArticle
- description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  name: How to Use Expand in Java – Complete Excel Guide
  steps:
  - name: Why This Works
    text: '- **`Workbook`**: Represents the entire Excel file. Creating a new one
      gives you a clean canvas; loading an existing file lets you augment a pre‑existing
      template. - **`Worksheet`**: Think of it as a single tab. We grab the first
      one because that’s where we’ll demonstrate the formula. - **`setFormul'
  - name: Real‑World Use Cases
    text: '| Scenario | How EXPAND Helps | |----------|------------------| | Generating
      a month‑long schedule from a short list of tasks | `=EXPAND(taskList,30)` |
      | Padding a matrix for a statistical model | `=EXPAND(matrix,10,10,0)` | | Creating
      placeholder rows for user input | `=EXPAND({""},20)` |'
  - name: Expected Output
    text: 'When you open `output.xlsx`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Formulas
title: Cara Menggunakan Expand di Java – Panduan Lengkap Excel
url: /id/java/spreadsheet-automation/how-to-use-expand-in-java-complete-excel-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Expand di Java – Panduan Lengkap Excel

Pernah bertanya-tanya **bagaimana cara menggunakan expand** saat Anda mengotomatisasi Excel dengan Java? Anda bukan satu-satunya—para pengembang terus menanyakan cara memperluas array menjadi baris tanpa menulis loop yang tak berujung. Kabar baiknya, Anda dapat melakukannya dengan satu rumus, dan kode Java untuk menempatkan rumus itu ke dalam workbook ternyata sangat singkat.

Dalam tutorial ini kami akan membimbing Anda melalui contoh praktis yang menunjukkan secara tepat cara menggunakan expand, cara menulis kode rumus Excel di Java, dan cara menyimpan file Excel dengan gaya Java sehingga Anda dapat memeriksa hasilnya secara langsung. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan, yang memuat workbook yang sudah ada, menaruh fungsi `EXPAND` ke dalam sebuah sel, dan menulis kembali file ke disk.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Java 17 (atau JDK terbaru apa pun) terpasang.
- Maven atau Gradle untuk mengelola dependensi.
- Perpustakaan **Aspose.Cells for Java** (cara termudah untuk memanipulasi Excel dari Java). Anda dapat mengambilnya dari Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
```

Tidak diperlukan instalasi Excel tambahan; perpustakaan ini menangani format file secara internal. Jika Anda lebih suka Gradle, cukup ganti blok dependensi sesuai kebutuhan.

Setelah dasar‑dasarnya selesai, mari kita mulai mengutak‑atik.

## Cara Menggunakan Expand di Java

Fungsi `EXPAND` merupakan bagian dari keluarga array dinamis Excel. Fungsi ini mengambil sebuah array sumber dan memperluasnya ke ukuran yang ditentukan, mengisi sel kosong dengan `#N/A` secara default. Dalam contoh kami, kami akan memberi array satu‑dimensi sederhana `{1,2,3}` dan meminta Excel memperluasnya menjadi **5 baris**.

```java
// Import statements
import com.aspose.cells.*;

public class ExpandDemo {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load or create a workbook
            Workbook wb = new Workbook(); // creates a blank workbook
            // Optionally, load an existing file:
            // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // 3️⃣ Apply the EXPAND function in cell A1
            // This is where we **write excel formula code** from Java.
            ws.getCells().get("A1").setFormula("=EXPAND({1,2,3},5)");

            // 4️⃣ Save the workbook — **save excel file java** style.
            wb.save("YOUR_DIRECTORY/output.xlsx");
            System.out.println("Workbook saved successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Mengapa Ini Berfungsi

- **`Workbook`**: Mewakili seluruh file Excel. Membuat yang baru memberi Anda kanvas bersih; memuat file yang sudah ada memungkinkan Anda menambah pada templat yang sudah ada.
- **`Worksheet`**: Anggap sebagai satu tab. Kami mengambil yang pertama karena di situlah kami akan mendemonstrasikan rumus.
- **`setFormula`**: Metode ini menyuntikkan rumus Excel yang valid dalam bentuk string. Di sini kami memberi fungsi `EXPAND`, yang memberi tahu Excel untuk **memperluas array ke baris** (dan kolom, bila Anda memintanya).
- **`save`**: Menyimpan perubahan ke disk. Inilah langkah **save excel file java** yang memastikan Anda dapat membuka file di Excel atau penampil apa pun setelahnya.

Jalankan program, buka `output.xlsx`, dan Anda akan melihat kolom A terisi dengan `1, 2, 3, #N/A, #N/A`. Ubah argumen kedua `EXPAND` menjadi `3` dan Anda hanya akan mendapatkan tiga baris—sempurna untuk laporan dinamis.

## Memperluas Array ke Baris dengan Fungsi EXPAND

Jika Anda berasal dari latar belakang di mana Anda harus melakukan loop manual pada baris, fungsi `EXPAND` dapat menggantikan boilerplate tersebut. Berikut penjelasan singkat tentang sintaksnya:

```
EXPAND(source, rows, columns, fill)
```

- **source** – Array yang ingin Anda perluas. Dalam contoh kami `{1,2,3}`.
- **rows** – Jumlah baris yang diinginkan. Kami menggunakan `5`.
- **columns** – Opsional; secara default menggunakan jumlah kolom dari sumber.
- **fill** – Apa yang ditempatkan di sel kosong (`#N/A` secara default).

### Contoh Kasus Penggunaan di Dunia Nyata

| Skenario | Bagaimana EXPAND Membantu |
|----------|---------------------------|
| Membuat jadwal sebulan penuh dari daftar tugas singkat | `=EXPAND(taskList,30)` |
| Menambahkan padding pada matriks untuk model statistik | `=EXPAND(matrix,10,10,0)` |
| Membuat baris placeholder untuk input pengguna | `=EXPAND({""},20)` |

Dengan membiarkan Excel melakukan pekerjaan berat, Anda menjaga kode Java tetap rapi dan menghindari loop yang tidak perlu.

## Menulis Kode Rumus Excel di Java

Anda mungkin bertanya, “Apakah saya bisa membangun string rumus secara dinamis?” Tentu saja. Berikut cuplikan yang membangun pemanggilan `EXPAND` berdasarkan variabel:

```java
int[] numbers = {4, 5, 6};
int targetRows = 7;

// Convert int array to Excel‑style literal: {4,5,6}
StringBuilder sb = new StringBuilder("{");
for (int i = 0; i < numbers.length; i++) {
    sb.append(numbers[i]);
    if (i < numbers.length - 1) sb.append(",");
}
sb.append("}");

String formula = String.format("=EXPAND(%s,%d)", sb.toString(), targetRows);
ws.getCells().get("B2").setFormula(formula);
```

Perhatikan bagaimana kami **write excel formula code** secara programatis, lalu menaruhnya ke sel `B2`. Pendekatan ini skalabel ketika Anda perlu menghasilkan rumus secara dinamis—misalnya, menarik data dari basis data dan mengubahnya menjadi laporan Excel yang dinamis.

## Save Excel File Java – Menyimpan Perubahan

Menyimpan workbook adalah bagian akhir dari puzzle. Aspose.Cells memberi Anda beberapa opsi:

- **`wb.save("path.xlsx")`** – Menyimpan dalam format XLSX default.
- **`wb.save("path.xls", SaveFormat.EXCEL_97_TO_2003)`** – Untuk kompatibilitas legacy.
- **`wb.save(outputStream, SaveFormat.XLSX)`** – Saat Anda perlu men-stream file (misalnya, dalam aplikasi web).

Berikut contoh yang menulis ke `ByteArrayOutputStream` sehingga Anda dapat mengembalikan byte‑nya dari endpoint REST:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
wb.save(baos, SaveFormat.XLSX);
byte[] excelBytes = baos.toByteArray();
// Now you can send `excelBytes` as a response payload.
```

Itulah pola **save excel file java** yang banyak layanan perusahaan andalkan.

## Kesalahan Umum & Tips Profesional

- **Timing Evaluasi Rumus** – Aspose.Cells **tidak** mengevaluasi rumus secara otomatis pada saat `save`. Jika Anda memerlukan nilai yang dihitung, panggil `wb.calculateFormula()` sebelum menyimpan.
- **Dukungan Array Dinamis** – Fungsi `EXPAND` hanya tersedia di Excel 365 / 2021+. Membuka file di versi Excel yang lebih lama akan menampilkan `#NAME?`. Jika Anda harus mendukung klien legacy, pertimbangkan fallback ke ekspansi manual.
- **Masalah Lokal** – Gunakan nama fungsi dalam bahasa Inggris (`EXPAND`) terlepas dari lokal workbook; Aspose.Cells mengikuti sintaks bahasa Inggris.
- **Array Besar** – Memperluas ke ribuan baris dapat memperbesar ukuran file. Pantau penggunaan memori dan pertimbangkan streaming dataset besar.

## Contoh Lengkap yang Berfungsi

Berikut program lengkap yang dapat Anda salin‑tempel ke IDE. Program ini mencakup semua impor, penanganan error, dan komentar untuk memandu Anda.

```java
import com.aspose.cells.*;

public class ExpandDemoFull {
    public static void main(String[] args) {
        // Adjust these paths as needed
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/output.xlsx";

        try {
            // Step 1: Load an existing workbook or create a new one
            Workbook wb;
            if (new java.io.File(inputPath).exists()) {
                wb = new Workbook(inputPath);
                System.out.println("Loaded existing workbook.");
            } else {
                wb = new Workbook(); // brand‑new workbook
                System.out.println("Created a new workbook.");
            }

            // Step 2: Access the first worksheet
            Worksheet ws = wb.getWorksheets().get(0);

            // Step 3: Build a dynamic EXPAND formula (expand array to rows)
            int[] sourceArray = {1, 2, 3};
            int rowsDesired = 5;

            // Convert Java array to Excel literal syntax
            StringBuilder literal = new StringBuilder("{");
            for (int i = 0; i < sourceArray.length; i++) {
                literal.append(sourceArray[i]);
                if (i < sourceArray.length - 1) literal.append(",");
            }
            literal.append("}");

            String formula = String.format("=EXPAND(%s,%d)", literal, rowsDesired);
            ws.getCells().get("A1").setFormula(formula);
            System.out.println("Inserted formula: " + formula);

            // Optional: force calculation so the file contains values, not just formulas
            wb.calculateFormula();

            // Step 4: Save the workbook – **save excel file java** style
            wb.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error occurred: " + ex.getMessage());
            ex.printStackTrace();
        }
    }
}
```

### Output yang Diharapkan

Saat Anda membuka `output.xlsx`:

| A   |
|-----|
| 1   |
| 2   |
| 3   |
| #N/A |
| #N/A |

Jika Anda mengubah `rowsDesired` menjadi `3`, kolom akan berhenti setelah baris ketiga. Placeholder `#N/A` adalah cara Excel mengatakan “tidak ada data di sini”—Anda dapat menggantinya dengan memberikan argumen keempat ke `EXPAND`, misalnya, `=EXPAND({1,

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Delete Rows in Excel Using Aspose.Cells for Java | Guide & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}