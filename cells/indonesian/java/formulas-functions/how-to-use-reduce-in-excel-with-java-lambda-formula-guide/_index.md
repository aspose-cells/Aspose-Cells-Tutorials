---
category: general
date: 2026-06-08
description: Cara menggunakan reduce di Excel dengan Java menggunakan Aspose.Cells.
  Pelajari formula lambda Excel, array dinamis Java, cara menulis lambda, dan penjumlahan
  dengan reduce dalam tutorial langkah demi langkah yang jelas.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: id
og_description: Cara menggunakan reduce di Excel dengan Java. Menguasai formula lambda
  Excel, array dinamis Java, dan penjumlahan dengan reduce menggunakan contoh lengkap
  yang dapat dijalankan.
og_title: Cara Menggunakan Reduce di Excel dengan Java – Panduan Formula Lambda
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Cara Menggunakan Reduce di Excel dengan Java – Panduan Rumus Lambda
url: /id/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Reduce di Excel dengan Java – Panduan Formula Lambda

Pernah bertanya-tanya **how to use reduce** di Excel ketika Anda menulis kode Java? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan saat mencoba menggabungkan fungsi array dinamis baru Excel dengan otomatisasi berbasis Java, dan jawabannya tidak serumit yang terlihat pada awalnya.

Dalam tutorial ini kami akan membahas contoh konkret yang menunjukkan **how to use reduce** bersama dengan ekspresi **lambda formula Excel**, semuanya didukung oleh pustaka Aspose.Cells for Java. Pada akhir tutorial Anda akan dapat menghasilkan array dinamis di Java, menulis fungsi lambda, dan menghitung **sum with reduce**—tanpa perlu mengutak‑atik spreadsheet secara manual.

---

## Apa yang Akan Anda Bangun

- Workbook baru yang dibuat sepenuhnya dari Java.  
- Array dinamis **EXPAND** yang mengisi sel A1:A5 dengan angka 1‑5.  
- Formula **REDUCE** yang menjumlahkan angka-angka tersebut menggunakan **lambda formula Excel**.  
- File `.xlsx` yang disimpan yang dapat Anda buka di program spreadsheet apa pun untuk memverifikasi hasilnya.

Tanpa makro eksternal, tanpa VBA—hanya kode Java murni dan fungsi modern Excel.

---

## Prasyarat

- Java 17 (atau JDK terbaru lainnya) – versi lama masih dapat digunakan tetapi Anda akan kehilangan kemudahan `var`.  
- Aspose.Cells for Java (versi percobaan gratis sudah cukup untuk demo ini).  
- Pemahaman dasar tentang sintaks Java dan formula Excel.

Jika Anda baru dengan **dynamic arrays java**, jangan khawatir—panduan ini menjelaskan setiap bagiannya.

---

## Langkah 1: Siapkan Proyek Anda dan Impor Aspose.Cells

Pertama-tama, tambahkan dependensi Aspose.Cells Maven ke `pom.xml` Anda (atau unduh JAR secara manual).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Pro tip:** Jaga dependensi Anda tetap terbaru; versi yang lebih baru meningkatkan kecepatan evaluasi formula, yang penting ketika Anda **how to use reduce** pada lembar kerja besar.

---

## Langkah 2: Buat Workbook dan Akses Worksheet Pertama

Sekarang kita akan membuat workbook baru. Ini adalah fondasi untuk mempelajari **how to use reduce** karena objek workbook memberi kita sandbox untuk menaruh formula.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Mengapa ini penting:* Kelas `Workbook` mengabstraksi seluruh file Excel, sementara `Worksheet` mewakili satu tab. Nanti Anda akan melihat bagaimana **dynamic arrays java** dapat mengisi banyak sel dari satu formula yang ditempatkan di A1.

---

## Langkah 3: Hasilkan Array Vertikal dengan EXPAND

Fungsi `EXPAND` Excel dapat menumpahkan nilai ke dalam rentang. Kita akan menggunakannya untuk membuat angka 1 sampai 5 di kolom A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Jika Anda membuka workbook yang dihasilkan, sel A1:A5 akan berisi 1, 2, 3, 4, 5. Ini adalah bagian **dynamic arrays java**—satu formula mengisi seluruh rentang.

---

## Langkah 4: Tulis Lambda REDUCE untuk Menjumlahkan Array

Di sinilah kami menjawab pertanyaan inti: **how to use reduce** di Excel dari Java. Fungsi `REDUCE` mengiterasi sebuah array, menerapkan lambda yang Anda berikan. Dalam kasus kami, kami akan menjumlahkan angka-angka tersebut.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Mari kita uraikan:

- `0` – nilai akumulator awal (`acc`).  
- `A1:A5` – array yang kami hasilkan dengan **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – **lambda formula Excel** yang menambahkan setiap elemen (`x`) ke akumulator (`acc`).  

Saat formula dijalankan, `B1` berisi **15**, yaitu **sum with reduce** dari angka 1‑5.

> **How to write lambda** di Excel? Anggaplah sebagai fungsi anonim di mana argumen pertama adalah parameter, dan ekspresi akhir adalah nilai kembali. Di Java kami hanya menyisipkan teks; mesin Excel yang melakukan pekerjaan berat.

---

## Langkah 5: Simpan Workbook

Akhirnya, kami menyimpan workbook ke disk sehingga Anda dapat membukanya di Excel, Google Sheets, atau penampil apa pun yang mendukung `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Open the file and you’ll see:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

**sum with reduce** muncul di B1, mengonfirmasi bahwa kami telah berhasil mendemonstrasikan **how to use reduce** bersama dengan **lambda formula Excel** dari Java.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program Java lengkap yang siap dijalankan. Salin‑tempel ke IDE Anda, sesuaikan direktori output, dan tekan **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Output yang diharapkan** saat Anda membuka `new-functions.xlsx`:

- Sel **A1:A5** berisi `1, 2, 3, 4, 5`.  
- Sel **B1** menampilkan `15`, mengonfirmasi **sum with reduce**.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan array horizontal bukan vertikal?

Swap the column/row arguments in `EXPAND`. For a horizontal spill across B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Bisakah saya menggunakan REDUCE untuk perkalian alih-alih penjumlahan?

Absolutely. Just change the lambda body:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Sekarang B1 akan menampilkan `120` (5 ! = 120).

### Apakah Aspose.Cells mendukung fungsi LAMBDA khusus?

Ya, Anda dapat mendefinisikan fungsi LAMBDA bernama melalui koleksi `Names` workbook, lalu memanggilnya seperti formula bawaan apa pun. Itu akan dibahas lebih mendalam pada tutorial selanjutnya tentang **how to write lambda** yang hidup di luar satu sel.

### Bagaimana dengan versi Excel lama yang tidak mengenali REDUCE?

Jika Anda menargetkan Excel 2019 atau sebelumnya, mesin akan mengembalikan `#NAME?`. Dalam kasus seperti itu

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}