---
category: general
date: 2026-10-16
description: Aspose.Cells mengatur formula di Java menggunakan fungsi EXPAND. Pelajari
  contoh langkah demi langkah dan lihat cara menggunakan expand untuk rentang dinamis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells set formula
- how to use expand
- expand function example
- Java Excel automation
- dynamic range formula
language: id
lastmod: 2026-10-16
og_description: Aspose.Cells mengatur formula di Java menggunakan fungsi EXPAND. Ikuti
  contoh lengkap untuk memperluas rentang secara dinamis dalam workbook Excel.
og_image_alt: Spreadsheet screenshot showing the EXPAND formula applied to cell B2
  via Aspose.Cells
og_title: Aspose.Cells mengatur formula dengan EXPAND – Tutorial Java
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Aspose.Cells set formula in Java using the EXPAND function. Learn a
    step‑by‑step example and see how to use expand for dynamic ranges.
  headline: Aspose.Cells set formula with EXPAND function – complete Java guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel formulas
- Spreadsheet automation
title: Aspose.Cells mengatur formula dengan fungsi EXPAND – panduan lengkap Java
url: /id/java/formulas-functions/aspose-cells-set-formula-with-expand-function-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Panduan Lengkap Java Aspose.Cells set formula dengan fungsi EXPAND

Jika Anda perlu **aspose cells set formula** secara programatis, tutorial ini menunjukkan secara tepat caranya. Anda akan belajar cara menggunakan fungsi EXPAND untuk membuat rentang dinamis yang berkembang lima baris dan lima kolom dari sel awal, semuanya dari kode Java.

Bekerja dengan rumus Excel dari Java sering terasa canggung, tetapi Aspose.Cells menyederhanakan kompleksitasnya. Pada bagian di bawah ini kami akan menelusuri contoh lengkap yang dapat dijalankan, membahas mengapa setiap baris penting, dan mengeksplorasi variasi umum seperti sel awal yang berbeda atau ukuran ekspansi variabel.

## Apa yang dibahas dalam tutorial ini

* Memuat workbook yang sudah ada dengan Aspose.Cells  
* Mengakses worksheet dan koleksi selnya  
* **aspose cells set formula** menggunakan fungsi `EXPAND`  
* Menghitung ulang workbook sehingga rumus dievaluasi  
* Menyimpan hasil dan memverifikasi output  

Tidak diperlukan pustaka eksternal selain Aspose.Cells, dan kode dapat dijalankan pada runtime Java 8+ mana pun. Pada akhir tutorial Anda akan dapat mengadaptasi pola ini untuk rumus dinamis lainnya.

## Prasyarat

* Java Development Kit (JDK) 8 atau yang lebih baru  
* Aspose.Cells untuk Java (unduh dari [situs resmi](https://downloads.aspose.com/cells/java))  
* File Excel input (`input.xlsx`) yang ditempatkan di direktori yang diketahui  
* Familiaritas dasar dengan sintaks Java serta Maven/Gradle untuk manajemen dependensi  

## Langkah 1: Siapkan proyek dan tambahkan Aspose.Cells

Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

Untuk Gradle, setaraannya adalah:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Selalu gunakan versi stabil terbaru; rilis yang lebih baru menyertakan perbaikan performa untuk perhitungan rumus.

## Langkah 2: Muat workbook

Baris pertama solusi kami membuka workbook yang sudah ada. Ganti `YOUR_DIRECTORY` dengan path absolut tempat `input.xlsx` berada.

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Mengapa ini penting*: Memuat workbook membuat representasi dalam memori yang memungkinkan Anda memanipulasi worksheet, sel, dan rumus tanpa harus menyentuh sistem file lagi.

## Langkah 3: Akses worksheet target dan koleksi sel

Kami bekerja dengan worksheet pertama (indeks 0). Objek `Cells` memberikan akses langsung ke sel individual berdasarkan alamat.

```java
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
```

Jika Anda memerlukan sheet yang berbeda, ubah indeks atau gunakan `get("SheetName")`.

## Langkah 4: **aspose cells set formula** – terapkan fungsi EXPAND

Sekarang kami menetapkan rumus pada sel **B2**. Fungsi `EXPAND` menerima tiga argumen: sel referensi, jumlah baris yang akan diperluas, dan jumlah kolom yang akan diperluas.

```java
        // Apply the EXPAND function to B2, expanding 5 rows and 5 columns from A2
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");
```

### Cara menggunakan expand

* **Sel referensi (`A2`)** – titik awal rentang dinamis.  
* **Baris (`5`)** – berapa banyak baris rentang harus tumbuh ke bawah.  
* **Kolom (`5`)** – berapa banyak kolom rentang harus tumbuh ke kanan.

Anda dapat mengganti nilai‑nilai ini dengan variabel jika memerlukan solusi yang fleksibel:

```java
int rows = 10;
int cols = 3;
cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));
```

## Langkah 5: Hitung ulang workbook

Setelah menetapkan rumus, Anda harus memberi tahu Aspose.Cells untuk mengevaluasinya. Metode `calculateFormula()` memproses semua rumus dalam workbook.

```java
        // Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();
```

> **Mengapa harus menghitung ulang?**  
> Tanpa pemanggilan ini, rumus tetap tidak dievaluasi dan file output akan menampilkan string mentah `=EXPAND(...)` alih‑alih array yang telah diperluas.

## Langkah 6: Simpan workbook yang telah diperbarui

Akhirnya, tulis perubahan ke file baru. Ini menjaga workbook asli tetap tersedia untuk perbandingan.

```java
        // Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Saat Anda membuka `output.xlsx` di Excel, sel **B2** akan menampilkan blok 5 × 5 nilai yang disalin dari area yang dimulai pada **A2**. Jika **A2** berisi angka `1`, blok tersebut akan menampilkan `1` di setiap sel karena `EXPAND` mereplikasi nilai sumber ke seluruh rentang yang diperluas.

## Kode sumber lengkap yang dapat dijalankan

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet and its cells collection
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Step 3: Apply the EXPAND function to cell B2, referencing A2 and expanding 5 rows and 5 columns
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");

        // Step 4: Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();

        // Step 5: Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Output yang diharapkan

| B2 | C2 | D2 | E2 | F2 |
|----|----|----|----|----|
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |

(Nilai sebenarnya tergantung pada apa yang ada di `A2` dalam file sumber Anda.)

## Variasi umum dan kasus tepi

| Skenario | Perubahan kode | Alasan |
|----------|----------------|--------|
| **Sel awal yang berbeda** | `cells.get("C3").setFormula("=EXPAND(D3,3,2)");` | Gunakan sel mana pun sebagai referensi; rumus akan memperluas relatif terhadap sel tersebut. |
| **Ukuran ekspansi variabel** | `int rows = 8; int cols = 4; cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));` | Memungkinkan rentang yang ditentukan pada waktu berjalan, berguna dalam laporan berbasis data. |
| **Ekspansi ukuran nol** | `=EXPAND(A2,0,0)` | Mengembalikan hanya nilai sel asli; berguna untuk logika kondisional di mana ukuran mungkin ditambah kemudian. |
| **Menggunakan named range** | `cells.get("B2").setFormula("=EXPAND(MyRange,5,5)");` | Berfungsi ketika `MyRange` didefinisikan dalam workbook; membuat rumus lebih mudah dibaca. |

> **Waspadai:** Batas maksimum array Excel (16.384 kolom × 1.048.576 baris). Mencoba memperluas melampaui batas ini akan menghasilkan error perhitungan.

## Tips debugging

* **Rumus tidak dievaluasi?** Pastikan `workbook.calculateFormula();` dipanggil setelah setiap `setFormula`.  
* **Nilai tidak sesuai harapan?** Verifikasi bahwa sel referensi (`A2` dalam contoh) berisi data yang ingin Anda propagasikan.  
* **Kekhawatiran performa** – Ekspansi besar dapat memakan biaya tinggi. Jika Anda hanya membutuhkan sebagian, kurangi argumen baris/kolom.

## Kesimpulan

Anda kini memiliki contoh lengkap **aspose cells set formula** yang menunjukkan **cara menggunakan expand** dalam Java. Dengan memuat workbook, menetapkan rumus `EXPAND`, menghitung ulang, dan menyimpan, Anda dapat menghasilkan rentang dinamis tanpa interaksi manual dengan Excel.

Dari sini Anda dapat mengeksplorasi:

* Menggunakan fungsi dinamis lain seperti `FILTER` atau `SEQUENCE` dengan Aspose.Cells.  
* Menyematkan logika ini dalam layanan web yang menghasilkan laporan secara on‑demand.  
* Menggabungkan `EXPAND` dengan pemformatan bersyarat melalui API Aspose.Cells.

Silakan bereksperimen dengan sel awal yang berbeda, ukuran variabel, atau named range untuk menyesuaikan skenario otomasi Anda. Jika contoh **expand function** ini membantu, bagikan kepada tim Anda atau kontribusikan perbaikan di GitHub. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mastering Aspose.Cells Java: How to interrupt formula calculation in Excel](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Convert Excel Tables to Ranges Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/english/java/tables-structured-references/convert-excel-tables-ranges-aspose-cells-java/)
- [How to Set Excel Document Version Using Aspose.Cells for Java](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}