---
category: general
date: 2026-06-30
description: Formula array dinamis di Java memungkinkan Anda membuat lembar Excel
  yang kuat. Pelajari cara membuat workbook Excel dengan Java dan menghitung semua
  formula dengan cepat.
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: id
og_description: Formula array dinamis di Java menyederhanakan otomatisasi Excel. Panduan
  ini menunjukkan cara membuat workbook Excel dengan Java, menggunakan fungsi expand,
  formula lambda, dan menghitung semua formula.
og_title: Formula Array Dinamis di Java – Buat Workbook & Hitung Formula
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: 'Formula Array Dinamis di Java: Membuat Workbook Excel dan Menghitung Semua
  Formula'
url: /id/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formula Array Dinamis di Java: Buat Workbook Excel dan Hitung Semua Formula

Pernah bertanya-tanya bagaimana **dynamic array formulas** bekerja saat Anda mengotomatisasi Excel dari Java? Anda tidak sendirian—banyak pengembang mengalami kebuntuan ketika mereka perlu memasukkan formula canggih seperti `EXPAND` atau `REDUCE` ke dalam workbook tanpa membuka Excel itu sendiri.  

Kabar baiknya? Dengan beberapa baris kode Java Anda dapat **create Excel workbook Java** secara gaya, menambahkan fungsi array modern tersebut, dan kemudian **calculate all formulas** sekaligus. Dalam tutorial ini kami akan membahas setiap langkah, menjelaskan *mengapa* setiap bagian penting, dan memberi Anda contoh lengkap yang dapat dijalankan yang dapat Anda salin‑tempel langsung ke dalam proyek Anda.

## Apa yang Akan Anda Pelajari

- Cara membuat workbook Excel baru menggunakan Java (ya, tanpa UI Excel).  
- Mekanisme di balik fungsi `EXPAND` dan bagaimana ia mengubah rentang sederhana menjadi array dinamis.  
- Cara **use lambda formula** dengan `REDUCE` untuk agregasi khusus.  
- Menambahkan fungsi trigonometri dan hiperbolik (`COT`, `COTH`) yang sering dilupakan ada dalam set formula Excel.  
- Satu baris kode yang Anda perlukan untuk **calculate all formulas** sehingga workbook menampilkan hasil terbaru.  

> **Prerequisites:** Java 8+ (untuk dukungan lambda), pustaka Aspose.Cells for Java, dan pemahaman dasar tentang formula Excel. Tidak ada dependensi lain yang diperlukan.

---

## Formula Array Dinamis: Menyiapkan Workbook

Pertama-tama—mari kita dapatkan objek workbook di meja kerja. Kelas `Workbook` dari Aspose.Cells adalah titik masuk Anda; anggaplah sebagai kanvas kosong tempat setiap formula array dinamis akan hidup.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*Why this matters:* Menginstansiasi workbook secara programatik memberi Anda kontrol penuh atas format file, pengaturan budaya, dan—yang paling penting—evaluasi formula tanpa pernah menyentuh disk.

---

## Menggunakan Fungsi EXPAND untuk Memperluas Rentang

Fungsi `EXPAND` adalah jawaban Excel untuk “spill” sebuah rentang ke area yang lebih besar berdasarkan ukuran yang Anda tentukan. Ini sempurna ketika data sumber dapat berubah panjangnya pada waktu berjalan.

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*Explanation:*  
- `B1:B3` adalah rentang sumber.  
- `5` memberi tahu Excel untuk menghasilkan lima baris, bahkan jika sumbernya lebih pendek.  
- `1` memaksa satu kolom.  

Ketika Anda kemudian **calculate all formulas**, hasil di `A1` akan menjadi spill vertikal lima nilai, menambahkan kosong bila diperlukan.

---

## Menerapkan Formula LAMBDA dengan REDUCE

Jika Anda pernah ingin menjumlahkan sebuah kolom tetapi juga membutuhkan akumulator khusus, `REDUCE` dipasangkan dengan **lambda formula** adalah cara yang tepat. Sintaksnya terlihat agak tidak biasa pada awalnya, tetapi ini hanyalah cara Java menyisipkan fungsi anonim kecil di dalam formula Excel.

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*Why use it?*  
- `0` adalah benih awal (total mulai).  
- `B1:B5` adalah array yang kami proses.  
- `LAMBDA(a,b,a+b)` berarti “ambil akumulator `a` dan elemen berikutnya `b`, kembalikan jumlahnya.”  

Anda dapat mengganti `a+b` dengan logika khusus apa pun—rata‑rata, maksimum, atau bahkan penggabungan string—menjadikan `REDUCE` blok bangunan yang serbaguna.

---

## Menambahkan Fungsi Trigonometri (COT, COTH)

Excel dilengkapi dengan sejumlah fungsi trigonometri yang sering terlewatkan. Berikut cara menambahkan cotangent sederhana dan saudara hiperboliknya ke dalam lembar.

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*Tip:* Fungsi‑fungsi ini secara otomatis menghormati mode perhitungan workbook, jadi Anda tidak memerlukan kode tambahan untuk mengonversi derajat ke radian—`PI()` melakukan pekerjaan beratnya.

---

## Menghitung Semua Formula di Workbook

Sekarang formula sudah berada di tempat, kita perlu **calculate all formulas** agar sel‑sel berisi nilai aktual bukan sekadar teks formula. Aspose.Cells menjadikannya satu pemanggilan metode.

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*What happens under the hood?* Perpustakaan menelusuri setiap sel, menyelesaikan ketergantungan, dan menumpahkan hasil array bila diperlukan. Jika Anda menangani lembar yang sangat besar, Anda dapat menyesuaikan opsi perhitungan untuk kinerja, tetapi pengaturan default sudah sangat baik untuk kebanyakan skenario.

---

## Contoh Lengkap yang Dapat Dijalankan (Siap Salin‑Tempel)

Berikut seluruh program, siap Anda masukkan ke IDE. Ia mencakup impor, metode `main`, dan pemanggilan `save` akhir sehingga Anda dapat membuka file yang dihasilkan di Excel dan melihat spill‑nya.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**Expected output when you open `DynamicArrayDemo.xlsx`:**

| A (Hasil) | B (Sumber) |
|------------|-----------|
| 10         | 10 |
| 20         | 20 |
| 30         | 30 |
| (kosong)    | 40 |
| (kosong)    | 50 |
| 150 (jumlah)  |   |
| 1 (cot)    |   |
| 1.0373… (coth) | |

*Notice how `A1` spills five rows, even though the source only had three values. That’s the power of **dynamic array formulas**.*

---

## Kesalahan Umum & Pro Tips

- **Don’t forget to set calculation mode** jika Anda menonaktifkan perhitungan otomatis di tempat lain; jika tidak `calculateFormula()` tidak akan melakukan apa‑apa.  
- **Array spill collisions:** Jika sel lain sudah menempati rentang spill, Excel akan mengembalikan error `#SPILL!`. Dalam kode, Anda dapat membersihkan area target terlebih dahulu dengan `worksheet.getCells().clear(0, 0, maxRow, maxColumn)`.  
- **Lambda syntax quirks:** Fungsi `LAMBDA` mengharapkan parameter dipisahkan dengan koma, bukan titik koma. Lewatkan koma dan seluruh formula gagal diparse.  
- **Performance tip:** Saat bekerja dengan ribuan baris, panggil `workbook.getSettings().setCalculateFormulaOnOpen(false)` sebelum memasukkan data secara massal, lalu aktifkan kembali sebelum pemanggilan akhir `calculateFormula()`.

---

## Langkah Selanjutnya

Sekarang Anda telah menguasai **dynamic array formulas**, pertimbangkan untuk menjelajahi:

- **`FILTER`** dan **`SORT`** untuk pembentukan data secara langsung.  
- **`SEQUENCE`** untuk menghasilkan array numerik tanpa rentang sumber.  
- Menggunakan **named ranges** bersama `EXPAND` untuk formula yang lebih bersih dan dapat dipakai ulang.  

Semua ini dibangun di atas konsep yang sama yang telah kami bahas—cukup ganti string formula dan biarkan Aspose.Cells melakukan pekerjaan beratnya.

---

## Kesimpulan

Dalam panduan ini kami menunjukkan secara tepat cara **create Excel workbook Java**,

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Calculate Excel Formulas Java: Optimize with Aspose.Cells](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [Master Excel Array Formulas with Aspose.Cells Java: Streamline Calculations and Formatting](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}