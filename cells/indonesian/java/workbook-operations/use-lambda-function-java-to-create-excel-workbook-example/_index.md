---
category: general
date: 2026-07-17
description: Gunakan fungsi lambda Java untuk membuat workbook Excel, demonstrasikan
  fungsi EXPAND dan REDUCE, serta hitung fungsi array di Excel dengan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use lambda function java
- create excel workbook java
- use reduce function excel
- use expand function excel
- calculate array functions excel
language: id
lastmod: 2026-07-17
og_description: Gunakan fungsi lambda Java untuk membuat workbook Excel, terapkan
  EXPAND dan REDUCE, serta hitung fungsi array di Excel – panduan lengkap langkah
  demi langkah.
og_image_alt: Screenshot of use lambda function java creating Excel workbook with
  formulas
og_title: Gunakan Fungsi Lambda Java – Buat Buku Kerja Excel dengan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: Use lambda function java to create an Excel workbook, demonstrate EXPAND
    and REDUCE functions, and calculate array functions in Excel with Aspose.Cells.
  headline: Use Lambda Function Java to Create Excel Workbook Example
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
- Lambda
title: Gunakan Fungsi Lambda Java untuk Membuat Contoh Workbook Excel
url: /id/java/workbook-operations/use-lambda-function-java-to-create-excel-workbook-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Use Lambda Function Java to Create Excel Workbook Example

Apakah Anda ingin **use lambda function java** untuk membuat sebuah workbook Excel? Dalam tutorial ini kami akan menelusuri contoh lengkap menggunakan Aspose.Cells yang tidak hanya membangun file tetapi juga menunjukkan cara **use expand function excel**, **use reduce function excel**, dan **calculate array functions excel** dalam satu skrip yang mudah diikuti.

Jika Anda pernah menatap spreadsheet dan berpikir, “Harus ada cara programatik untuk memperluas array ini atau mengurangi angka‑angka ini,” Anda berada di tempat yang tepat. Pada akhir panduan ini Anda akan memiliki program Java yang dapat dijalankan yang membuat file Excel, menyisipkan formula untuk EXPAND, REDUCE, COT, dan COTH, serta menyimpan hasil evaluasinya—semua sambil menunjukkan kekuatan pendekatan **lambda function java**.

---

## Prasyarat – Apa yang Anda Butuhkan Sebelum Memulai

- **Java Development Kit (JDK) 8+** – kode menggunakan ekspresi lambda, jadi pastikan Anda menggunakan setidaknya JDK 8.  
- **Aspose.Cells for Java** – pustaka komersial yang memungkinkan Anda memanipulasi file Excel tanpa harus menginstal Office. Unduh JAR terbaru dari situs Aspose dan tambahkan ke classpath proyek Anda.  
- IDE sederhana (IntelliJ IDEA, Eclipse, VS Code) – apa saja dapat digunakan, tetapi IDE dengan dukungan Maven/Gradle memudahkan penanganan dependensi.  

Tidak ada instalasi tambahan yang diperlukan; pustaka ini menangani semua proses berat di balik layar.

---

## Langkah 1: Siapkan Proyek dan Impor Dependensi

Buat proyek Maven baru (atau Gradle, jika Anda lebih suka) dan tambahkan dependensi Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Jika Anda tidak menggunakan Maven, cukup letakkan `aspose-cells-24.10.jar` ke dalam folder `libs` Anda dan tambahkan ke build path.

> **Pro tip:** Jaga dependensi Anda tetap terbaru. Versi yang lebih baru sering membawa peningkatan kinerja dan perbaikan bug untuk fungsi seperti EXPAND dan REDUCE.

---

## Gunakan Lambda Function Java untuk Membuat Workbook Excel

Sekarang lingkungan sudah siap, mari **use lambda function java** untuk menyematkan ekspresi LAMBDA langsung ke dalam formula Excel. Fungsi REDUCE di Excel mengharapkan sebuah lambda, dan penanganan string di Java membuatnya sederhana.

```java
import com.aspose.cells.*;

public class Office365FunctionsDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create a new workbook and obtain the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Demonstrate the EXPAND function – expands a seed array to a larger size
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3},5,1)");
        // Explanation: EXPAND turns the 3‑element seed into a 5‑row, 1‑column array.

        // Step 4: Demonstrate the REDUCE function – aggregates an array into a single value
        // Here we **use lambda function java** inside the Excel formula.
        sheet.getCells().get("A2").setFormula(
            "=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))"
        );
        // Explanation: Starting at 0, the lambda (a,b) → a+b adds each element together.

        // Step 5: Use the COT function to calculate the cotangent of π/4
        sheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 6: Use the COTH function to calculate the hyperbolic cotangent of 1
        sheet.getCells().get("A4").setFormula("=COTH(1)");

        // Step 7: Recalculate all formulas so the results are stored in the cells
        workbook.calculateFormula();

        // Step 8: Save the workbook with the evaluated results
        workbook.save("Office365Funcs.xlsx");
    }
}
```

### Mengapa Ini Berfungsi

- **`Workbook`** adalah titik masuk untuk tugas **create excel workbook java**. Ia mewakili seluruh file dalam memori.  
- **`Worksheet`** memberi kita lembar kerja; workbook default sudah berisi satu lembar.  
- **`setFormula`** menyisipkan string formula Excel mentah. Perhatikan bagaimana baris REDUCE berisi segmen `LAMBDA(a,b,a+b)` – di situlah kami **use lambda function java** untuk memberi tahu Excel cara menggabungkan nilai.  
- **`calculateFormula()`** memaksa Aspose.Cells untuk mengevaluasi setiap formula, sehingga angka hasil disimpan langsung di file. Tanpa pemanggilan ini sel akan berisi teks formula saja.  

---

## Cara Menggunakan Expand Function Excel – Memperluas Array Secara Dinamis

Contoh **use expand function excel** berada di sel `A1`. Mari kita uraikan apa yang dilakukan formula tersebut:

```excel
=EXPAND({1,2,3},5,1)
```

- `{1,2,3}` adalah array awal (tiga angka).  
- `5` memberi tahu Excel untuk memperluas hasil menjadi lima baris.  
- `1` menentukan jumlah kolom (hanya satu kolom).  

Saat workbook dibuka di Excel, `A1:A5` akan menampilkan:

| A |
|---|
| 1 |
| 2 |
| 3 |
| 0 |
| 0 |

> **Kesalahan umum:** Lupa memanggil `workbook.calculateFormula()` akan membuat Anda hanya melihat teks mentah `=EXPAND(...)` alih‑alih angka yang telah diperluas.

---

## Cara Menggunakan Reduce Function Excel – Menjumlahkan dengan Lambda

Baris **use reduce function excel** berada di sel `A2`. Bentuknya seperti ini:

```excel
=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))
```

- `0` adalah nilai akumulator awal.  
- `{1,2,3,4}` adalah array yang ingin kita reduksi.  
- `LAMBDA(a,b,a+b)` memberi tahu Excel untuk menambahkan setiap elemen (`b`) ke total berjalan (`a`).  

Setelah perhitungan, `A2` berisi **10**. Jika Anda menginginkan produk alih‑alih jumlah, cukup ganti `a+b` dengan `a*b` – pola **use lambda function java** yang sama tetap berlaku.

---

## Menghitung Fungsi Array Excel – COT dan COTH

While not strictly array‑based, the COT

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Use Aspose Cells – Excel Engine Tutorials for Java](/cells/english/java/calculation-engine/)
- [Custom SUM Function in Excel using Aspose.Cells Java&#58; Enhance Your Calculations](/cells/english/java/formulas-functions/custom-sum-function-excel-aspose-cells-java/)
- [How to Use Aspose.Cells for Excel Slicer Automation in Java](/cells/english/java/advanced-features/excel-slicer-modifications-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}