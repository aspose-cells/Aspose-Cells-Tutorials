---
category: general
date: 2026-11-22
description: Pelajari cara memperluas rentang di Excel dengan Java, mengotomatisasi
  perhitungan Excel, dan membaca file Excel dengan Java menggunakan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand range
- automate excel calculations
- read excel file java
- use expand function
- how to use expand
language: id
lastmod: 2026-11-22
og_description: Cara memperluas rentang di Excel dengan Java menggunakan fungsi EXPAND.
  Panduan ini menunjukkan cara mengotomatisasi perhitungan Excel, membaca file Excel
  dengan Java, dan menerapkan fungsi expand secara efisien.
og_image_alt: Screenshot showing how to expand range in Excel using Java code
og_title: Cara memperluas rentang di Excel dengan Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to expand range in Excel with Java, automate Excel calculations,
    and read Excel file Java using Aspose.Cells.
  headline: How to expand range in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Cara memperluas rentang di Excel dengan Java
url: /id/java/range-management/how-to-expand-range-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memperluas rentang di Excel dengan Java

Jika Anda perlu **cara memperluas rentang** di lembar kerja Excel dari Java, panduan ini memberikan solusi lengkap yang dapat dijalankan. Anda akan melihat cara mengotomatisasi perhitungan Excel, membaca file Excel dengan Java, dan menerapkan fungsi `EXPAND` tanpa meninggalkan IDE Anda.

Bekerja dengan file Excel secara programatik sering membutuhkan lebih dari referensi sel statis. Fungsi `EXPAND` membuat rentang spill dinamis, yang ideal untuk laporan berbasis data, dasbor, atau skenario apa pun di mana ukuran data sumber berubah. Pada akhir tutorial ini Anda akan memiliki program Java yang berdiri sendiri yang memuat workbook, menetapkan formula `EXPAND`, memaksa perhitungan ulang, dan menulis hasilnya kembali ke disk.

## Prasyarat

* Java 17 atau yang lebih baru terinstal.
* Maven atau Gradle untuk manajemen dependensi.
* Lisensi Aspose.Cells for Java (evaluasi gratis dapat digunakan untuk pengujian).
* File `input.xlsx` sederhana yang ditempatkan di direktori yang diketahui.

Persyaratan ini mencakup langkah **read excel file java** dan memastikan kode berjalan tanpa konfigurasi tambahan.

## Cara memperluas rentang di Excel – menyiapkan proyek

1. **Buat proyek Maven** (atau tambahkan dependensi ke build yang sudah ada).  
   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```
   Menambahkan pustaka memberi Anda akses ke `Workbook`, `Worksheet`, dan kelas lain yang diperlukan untuk **automate excel calculations**.

2. **Tempatkan workbook input** di dekat root proyek.  
   Untuk tutorial ini file bernama `input.xlsx`. File harus berisi setidaknya lima baris data yang dimulai dari sel **A2**, karena contoh ini memperluas rentang tersebut sebanyak lima baris.

## Membaca file Excel dengan Java – memuat workbook

```java
// Load an existing workbook from the file system
Workbook workbook = new Workbook("input.xlsx");
```

Konstruktor `Workbook` membuka file dan mengurai struktur internalnya. Ini adalah langkah pertama dalam alur kerja **read excel file java** apa pun.

## Menggunakan fungsi EXPAND – menetapkan formula

```java
// Access the first worksheet (index 0)
Worksheet ws = workbook.getWorksheets().get(0);

// Set a formula that uses the EXPAND function.
// The formula expands the range starting at A2 to 5 rows and 1 column.
ws.getCells().get("A1").setFormula("=EXPAND(A2,5,1)");
```

Fungsi `EXPAND` berperilaku seperti formula array dinamis: ia mengembalikan rentang spill yang secara otomatis mengisi jumlah baris dan kolom yang diminta. Dalam kasus ini rentang `A2:A6` menjadi hasil formula yang ditempatkan di **A1**. Ini menggambarkan **use expand function** dalam konteks dunia nyata.

## Mengotomatisasi perhitungan Excel – memaksa perhitungan ulang

```java
// Recalculate all formulas in the workbook so the EXPAND formula is evaluated
workbook.calculateFormula();
```

Memanggil `calculateFormula()` memicu mesin untuk **automate excel calculations** yang sebaliknya memerlukan interaksi manual di UI. Metode ini memproses formula `EXPAND` dan menulis nilai spill ke sel yang sesuai.

## Menyimpan workbook yang dimodifikasi – menyelesaikan alur kerja

```java
// Save the workbook with the expanded range applied
workbook.save("output.xlsx");
```

Setelah disimpan, `output.xlsx` berisi data asli plus rentang spill baru yang dihasilkan oleh fungsi `EXPAND`. Membuka file di Excel menampilkan nilai dari **A2:A6** yang secara otomatis terisi di bawah **A1**.

## Contoh lengkap yang berfungsi

Berikut adalah kelas Java lengkap yang berdiri sendiri yang dapat Anda salin, kompilasi, dan jalankan. Kelas ini menunjukkan setiap langkah mulai dari memuat file hingga menyimpan hasil.

```java
import com.aspose.cells.*;

public class ExpandRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook (read excel file java)
        Workbook workbook = new Workbook("input.xlsx");

        // 2️⃣ Get the first worksheet
        Worksheet ws = workbook.getWorksheets().get(0);

        // 3️⃣ Apply the EXPAND formula (use expand function)
        // The formula expands the range starting at A2 to 5 rows and 1 column
        ws.getCells().get("A1").setFormula("=EXPAND(A2,5,1)");

        // 4️⃣ Recalculate so the formula is evaluated (automate excel calculations)
        workbook.calculateFormula();

        // 5️⃣ Save the updated workbook
        workbook.save("output.xlsx");

        System.out.println("Workbook saved as output.xlsx with expanded range.");
    }
}
```

### Output yang diharapkan

Saat Anda membuka `output.xlsx` setelah program selesai, Anda akan melihat:

| A   | B | … |
|-----|---|---|
| **A1** | *(value from A2)* |
| **A2** | *(value from A3)* |
| **A3** | *(value from A4)* |
| **A4** | *(value from A5)* |
| **A5** | *(value from A6)* |

Nilai di kolom **A** adalah hasil spill dari formula `EXPAND`. Tidak diperlukan penyalinan‑tempel manual, yang menunjukkan cara **automate excel calculations** secara efektif.

## Kasus tepi dan tips praktik terbaik

* **Empty source cells** – Jika `A2` kosong, rentang spill juga akan kosong. Pertimbangkan membungkus formula dengan `IFERROR` jika Anda memerlukan nilai cadangan.
* **Large ranges** – Fungsi `EXPAND` dapat menangani ribuan baris, tetapi menghitung ulang lembar yang sangat besar dapat memengaruhi kinerja. Gunakan `Workbook.calculateFormula(FormulaCalculationOptions)` untuk menyesuaikan pengaturan perhitungan.
* **License enforcement** – Tanpa lisensi Aspose.Cells yang valid, pustaka akan menambahkan watermark pada file output. Daftarkan lisensi Anda di awal metode `main` untuk menghindari hal ini.
* **Thread safety** – Instansi `Workbook` tidak thread‑safe. Buat instansi terpisah per thread saat **automate excel calculations** dalam pekerjaan paralel.

## Kesimpulan

Anda sekarang tahu **cara memperluas rentang** di Excel dengan Java dengan menggunakan fungsi `EXPAND`, memuat workbook, memaksa perhitungan ulang, dan menyimpan hasilnya. Contoh end‑to‑end ini mencakup **read excel file java**, menunjukkan **use expand function**, dan memperlihatkan cara **automate excel calculations** secara siap produksi.

### Apa selanjutnya?

* Jelajahi fungsi array dinamis lainnya seperti `FILTER`, `SORT`, dan `UNIQUE` untuk membangun spreadsheet yang lebih canggih.
* Gabungkan **read excel file java** dengan API streaming untuk memproses file besar tanpa memuat seluruh workbook ke memori.
* Gunakan kemampuan charting Aspose.Cells untuk memvisualisasikan data yang diperluas langsung dari Java.

Silakan bereksperimen dengan rentang sumber yang berbeda, jumlah kolom, atau bahkan workbook multi‑sheet. Pola yang sama berlaku: tetapkan formula, panggil `calculateFormula()`, dan simpan. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara menggunakan fungsi expand dalam pemrosesan Excel Java](/cells/english/java/range-management/how-to-use-expand-function-in-java-excel-processing/)
- [Cara Menggunakan Expand di Java – Panduan Excel Lengkap](/cells/english/java/spreadsheet-automation/how-to-use-expand-in-java-complete-excel-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}