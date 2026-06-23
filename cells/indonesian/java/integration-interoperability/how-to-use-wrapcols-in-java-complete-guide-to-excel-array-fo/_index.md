---
category: general
date: 2026-06-18
description: Pelajari cara menggunakan WRAPCOLS di Java untuk membungkus daftar menjadi
  kolom, menerapkan formula array ala Excel, dan membuat workbook Excel di Java dengan
  cepat.
draft: false
keywords:
- how to use wrapcols
- apply array formula excel
- list to matrix excel
- wrap list into columns
- create excel workbook java
language: id
og_description: Temukan cara menggunakan WRAPCOLS di Java, membungkus daftar menjadi
  kolom, menerapkan formula array Excel, dan membuat workbook Excel di Java dengan
  contoh lengkap yang dapat dijalankan.
og_title: Cara Menggunakan WRAPCOLS di Java – Panduan Lengkap Formula Array Excel
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Learn how to use WRAPCOLS in Java to wrap a list into columns, apply
    array formula Excel style, and create Excel workbook Java quickly.
  headline: How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas
  type: TechArticle
- questions:
  - answer: The library works in trial mode, which adds a watermark. For production
      you’ll need a commercial license, but the API usage stays the same.
    question: Do I need a license for Aspose.Cells?
  - answer: Absolutely. Replace `{1,2,3}` with a named range like `MyNumbers`. The
      formula becomes `=WRAPCOLS(MyNumbers,3)`.
    question: Can I use WRAPCOLS with named ranges instead of literal arrays?
  - answer: 'POI currently doesn’t evaluate array formulas out of the box, so you’d
      need a custom evaluator or switch to Aspose for full support. --- ## Conclusion
      We’ve covered **how to use WRAPCOLS** in Java, shown you how to **apply array
      formula Excel** techniques, and demonstrated a practical **list to matr'
    question: What if I’m using Apache POI instead of Aspose?
  type: FAQPage
tags:
- Excel
- Java
- Aspose.Cells
- Array Formula
title: Cara Menggunakan WRAPCOLS di Java – Panduan Lengkap Rumus Array Excel
url: /id/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan WRAPCOLS di Java – Panduan Lengkap Rumus Array Excel

Pernah bertanya‑tanya **cara menggunakan WRAPCOLS** saat Anda mengotomatiskan spreadsheet dari Java? Anda tidak sendirian. Baik Anda ingin mengubah daftar nilai datar menjadi tabel 3‑kolom yang rapi atau hanya membutuhkan cara cepat untuk merombak data, fungsi WRAPCOLS adalah penyelamat.  

Dalam tutorial ini kami akan membahas contoh dunia nyata yang menunjukkan **cara menggunakan WRAPCOLS**, cara **menerapkan rumus array Excel**, dan bahkan cara **membuat workbook Excel Java** dari awal. Pada akhir tutorial Anda akan memiliki file `.xlsx` yang berfungsi penuh yang memperlihatkan transformasi **daftar ke matriks Excel**—semua dengan penjelasan jelas dan kode siap‑jalankan.

## Apa yang Akan Anda Pelajari

* Sintaks tepat dari fungsi array `WRAPCOLS` dan kapan fungsi ini paling berguna.  
* Cara **menerapkan rumus array Excel** menggunakan Aspose.Cells untuk Java.  
* Cara **daftar ke matriks Excel** – baik secara kolom maupun baris.  
* Tips untuk **membungkus daftar ke dalam kolom** secara efisien, serta contoh lengkap **membuat workbook Excel Java**.  

Tidak memiliki pengalaman dengan Aspose.Cells? Tidak masalah. Yang Anda perlukan hanyalah lingkungan pengembangan Java dan salinan pustaka Aspose.Cells untuk Java (versi percobaan gratis sudah cukup).

---

## Cara Menggunakan WRAPCOLS – Implementasi Langkah‑demi‑Langkah

> **Tips pro:** WRAPCOLS adalah fungsi *array*, yang berarti Anda harus memasukkannya sebagai rumus yang mengembalikan beberapa sel sekaligus. Di Java, Aspose.Cells menangani evaluasi array untuk Anda setelah Anda memicu perhitungan ulang.

```java
// ---------------------------------------------------------------------
// 1️⃣  Import the Aspose.Cells library
// ---------------------------------------------------------------------
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {

        // -----------------------------------------------------------------
        // 2️⃣  Create a new workbook – this is the foundation of any Java‑Excel task
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook();               // create excel workbook java

        // -----------------------------------------------------------------
        // 3️⃣  Grab the first worksheet (index 0) – the default sheet is ready
        // -----------------------------------------------------------------
        Worksheet sheet = workbook.getWorksheets().get(0);

        // -----------------------------------------------------------------
        // 4️⃣  Set a WRAPCOLS formula that turns a simple list into a 3‑column matrix
        // -----------------------------------------------------------------
        // The array {1,2,3,4,5,6} will be laid out column‑wise, three columns wide.
        sheet.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3,4,5,6},3)"); // how to use wrapcols

        // -----------------------------------------------------------------
        // 5️⃣  Set a WRAPROWS formula – just for comparison, creates a 2‑row matrix
        // -----------------------------------------------------------------
        sheet.getCells().get("B1").setFormula("=WRAPROWS({1,2,3,4,5,6},2)"); // apply array formula excel

        // -----------------------------------------------------------------
        // 6️⃣  Recalculate all formulas so the array results become actual cell values
        // -----------------------------------------------------------------
        workbook.calculateFormula();                     // forces evaluation of array formulas

        // -----------------------------------------------------------------
        // 7️⃣  Save the workbook to disk – you now have a real Excel file
        // -----------------------------------------------------------------
        workbook.save("wrap_demo.xlsx");                 // create excel workbook java
        System.out.println("Workbook saved successfully!");
    }
}
```

**Mengapa ini berhasil:**  
* `Workbook` adalah titik masuk untuk setiap manipulasi Excel di Java.  
* `WRAPCOLS` menerima dua argumen – array sumber dan jumlah kolom yang diinginkan.  
* Dengan memanggil `calculateFormula()`, Aspose.Cells mengevaluasi rumus array dan menuliskan matriks hasil ke dalam lembar, secara efektif **membungkus daftar ke dalam kolom**.  

> **Bagaimana jika Anda memerlukan jumlah kolom yang dinamis?** Cukup ganti angka `3` yang ditulis keras dengan referensi sel atau variabel yang Anda hitung pada waktu berjalan.

---

## Menerapkan Rumus Array di Excel dengan Java

Jika Anda belum pernah menangani rumus array secara programatis, konsepnya bisa terasa agak misterius. Di UI Excel Anda menekan `Ctrl+Shift+Enter` untuk mengunci rumus; di Java pustaka melakukan pekerjaan berat untuk Anda.  

* **Setel rumus** – seperti yang ditunjukkan di atas, Anda menggunakan `setFormula()` pada sebuah sel.  
* **Picu perhitungan ulang** – `workbook.calculateFormula()` memaksa mesin mengevaluasi setiap rumus, termasuk array.  

Pendekatan ini adalah cara yang direkomendasikan untuk **menerapkan rumus array Excel** saat Anda menghasilkan workbook di sisi server. Ini menjamin sel‑sel hasil berisi nilai yang sudah dihitung, bukan sekadar string rumus.

---

## Mengubah Daftar menjadi Matriks di Excel

Fungsi `WRAPCOLS` dan `WRAPROWS` sangat cocok untuk mengubah daftar satu‑dimensi menjadi tata letak dua‑dimensi. Berikut perbandingan singkat:

| Fungsi      | Bentuk yang Diinginkan | Contoh Pemanggilan                         | Hasil (beberapa sel pertama) |
|-------------|------------------------|--------------------------------------------|------------------------------|
| `WRAPCOLS`  | 3 kolom                | `=WRAPCOLS({1,2,3,4,5,6},3)`               | A1=1, A2=2, A3=3, B1=4…      |
| `WRAPROWS`  | 2 baris                | `=WRAPROWS({1,2,3,4,5,6},2)`               | A1=1, B1=2, C1=3, A2=4…      |

Perhatikan bagaimana daftar datar yang sama dapat divisualisasikan dalam dua cara yang sangat berbeda. Ketika Anda memerlukan transformasi **daftar ke matriks Excel**, pilih saja fungsi yang sesuai dengan orientasi yang Anda inginkan.

### Kasus Tepi yang Perlu Diingat

* **Pembagian tidak merata** – Jika panjang daftar bukan kelipatan sempurna dari jumlah kolom/baris, kolom/baris terakhir akan berisi sisa item. Tidak ada error yang dilempar.  
* **Array sumber kosong** – Menggunakan `{}` akan menghasilkan error #VALUE!; hindari dengan memeriksa ukuran daftar sebelum menyetel rumus.  
* **Set data besar** – Untuk ribuan item, pertimbangkan memecah operasi menjadi beberapa bagian untuk menghindari lonjakan memori saat `calculateFormula()` dijalankan.

---

## Membungkus Daftar ke Kolom vs. Baris – Kapan Memilih yang Mana?

* **Bungkus ke kolom (`WRAPCOLS`)** ketika Anda menginginkan penyebaran vertikal melintasi sejumlah kolom tetap – cocok untuk laporan yang menuliskan item ke bawah tiap kolom.  
* **Bungkus ke baris (`WRAPROWS`)** ketika Anda lebih suka penyebaran horizontal – berguna untuk dasbor di mana setiap baris mewakili sebuah kategori.  

Kedua fungsi termasuk dalam keluarga **rumus array** Excel, artinya mereka mengembalikan array nilai. Pilihan tergantung pada tata letak visual yang diharapkan pemangku kepentingan.

---

## Membuat Workbook Excel di Java – Contoh Lengkap

Berikut adalah program mandiri yang mendemonstrasikan semua yang telah dibahas. Salin, tempel, dan jalankan; Anda akan mendapatkan `wrap_demo.xlsx` di folder proyek Anda.

```java
import com.aspose.cells.*;

public class FullWrapExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣  Instantiate a new workbook – the starting point for create excel workbook java
        Workbook wb = new Workbook();

        // 2️⃣  Access the default worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣  Demonstrate WRAPCOLS – turning a simple list into a 3‑column matrix
        ws.getCells().get("A1").setFormula("=WRAPCOLS({10,20,30,40,50,60,70,80,90},3)"); // how to use wrapcols

        // 4️⃣  Demonstrate WRAPROWS – turning the same list into a 2‑row matrix
        ws.getCells().get("E1").setFormula("=WRAPROWS({10,20,30,40,50,60,70,80,90},2)"); // apply array formula excel

        // 5️⃣  Force calculation so the array results are materialized
        wb.calculateFormula();

        // 6️⃣  Save the file – you’ve now created an Excel workbook Java can open
        wb.save("full_wrap_demo.xlsx"); // create excel workbook java

        System.out.println("Excel file generated: full_wrap_demo.xlsx");
    }
}
```

**Output yang diharapkan:**  

* Sel `A1:C3` akan berisi angka 10‑90 yang disusun secara kolom (3 kolom).  
* Sel `E1:M2` akan memuat angka yang sama yang disusun secara baris (2 baris).  

Buka file tersebut di Excel, dan Anda akan melihat matriks bersih tanpa penyalinan manual—hanya kekuatan **membungkus daftar ke dalam kolom** (dan baris) yang digerakkan oleh Java.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah saya memerlukan lisensi untuk Aspose.Cells?**  
J: Pustaka dapat dijalankan dalam mode percobaan, yang menambahkan watermark. Untuk produksi Anda memerlukan lisensi komersial, tetapi penggunaan API tetap sama.

**T: Bisakah saya menggunakan WRAPCOLS dengan named range alih‑alih array literal?**  
J: Tentu saja. Ganti `{1,2,3}` dengan named range seperti `MyNumbers`. Rumusnya menjadi `=WRAPCOLS(MyNumbers,3)`.

**T: Bagaimana jika saya menggunakan Apache POI alih‑alih Aspose?**  
J: POI saat ini tidak mengevaluasi rumus array secara otomatis, sehingga Anda memerlukan evaluator khusus atau beralih ke Aspose untuk dukungan penuh.

---

## Kesimpulan

Kami telah membahas **cara menggunakan WRAPCOLS** di Java, menunjukkan cara **menerapkan teknik rumus array Excel**, dan mendemonstrasikan konversi praktis **daftar ke matriks Excel**. Potongan kode yang dapat dijalankan juga menggambarkan proses lengkap **

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Aspose.Cells untuk Java: Cara Membuat dan Memformat Workbook Excel Secara Efisien](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Cara Membuat Daftar Validasi Data Excel dengan Aspose.Cells untuk Java: Panduan Langkah‑demi‑Langkah](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Cara Menerapkan Gaya pada Sel Excel Menggunakan Aspose.Cells untuk Java - Panduan Lengkap](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}