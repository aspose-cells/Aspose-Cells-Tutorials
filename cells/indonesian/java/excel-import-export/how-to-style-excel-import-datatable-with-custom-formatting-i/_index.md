---
category: general
date: 2026-07-03
description: Cara menata file Excel menggunakan Java. Pelajari cara memformat kolom
  tanggal di Excel, menerapkan format angka di Excel, mengekspor DataTable ke XLSX,
  dan mengimpor DataTable ke Excel dengan Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: id
og_description: Cara menata file Excel di Java. Tutorial ini menunjukkan cara memformat
  kolom tanggal di Excel, menerapkan format angka di Excel, mengekspor DataTable ke
  XLSX, dan mengimpor DataTable ke Excel.
og_title: Cara Menata Excel – Panduan Java untuk Pemformatan Kolom Kustom
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Cara Menata Excel – Impor DataTable dengan Pemformatan Kustom di Java
url: /id/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menata Excel – Mengimpor DataTable dengan Pemformatan Kustom di Java

Pernah bertanya-tanya **how to style Excel** lembar kerja secara programatis tanpa membuka file secara manual? Anda tidak sendirian. Banyak pengembang perlu menghasilkan laporan di mana kolom pertama tebal, kolom kedua menampilkan tanggal, dan sisanya mengikuti tata letak bersih. Dalam panduan ini kami akan membahas contoh lengkap yang dapat dijalankan yang **imports a DataTable into Excel**, menerapkan header tebal, memformat kolom tanggal, dan akhirnya **exports DataTable to XLSX**.  

Kami akan menggunakan Aspose.Cells for Java, tetapi konsepnya dapat diterapkan pada pustaka apa pun yang memungkinkan Anda bekerja dengan gaya. Pada akhir tutorial Anda akan memiliki pola yang dapat digunakan kembali untuk **apply number format Excel** sel, **format column date Excel**, dan mengirimkan workbook yang dipoles kepada pengguna Anda.

## Prasyarat

- Java 17 (atau JDK terbaru apa pun)  
- Aspose.Cells for Java 23.9 atau lebih baru (versi percobaan gratis sudah cukup)  
- Struktur mirip `DataTable` (contoh menggunakan mock sederhana)  
- IDE favorit Anda (IntelliJ IDEA, Eclipse, VS Code…)

Tidak diperlukan plugin Maven tambahan; cukup tambahkan JAR Aspose.Cells ke classpath Anda.

---

## Langkah 1: Dapatkan DataTable Sumber – Persiapan “Export DataTable to XLSX”

Sebelum kita dapat **import datatable into excel**, kita membutuhkan objek `DataTable` yang mewakili data yang ingin Anda ekspor. Pada proyek nyata Anda mungkin mengambilnya dari basis data, file CSV, atau API. Untuk tutorial ini kami akan membuat tabel kecil sebagai mock:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Why this matters:** Mendapatkan data dengan benar di awal berarti sisa logika penataan dapat fokus sepenuhnya pada presentasi, bukan pengolahan data.

---

## Langkah 2: Buat Array untuk Menampung Definisi Gaya untuk Setiap Kolom

Aspose.Cells memungkinkan Anda mengirimkan array **Style[]** saat mengimpor `DataTable`. Setiap entri sesuai dengan satu kolom dan menentukan bagaimana kolom tersebut akan terlihat setelah impor. Mari alokasikan array berdasarkan jumlah kolom:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tip:** Jika Anda memiliki banyak kolom, pertimbangkan untuk membangun array dalam loop dan menggunakan kembali satu objek `Style` di mana pemformatannya identik. Ini mengurangi beban memori.

---

## Langkah 3: Definisikan Gaya – Header Tebal & Pemformatan Tanggal

Sekarang kami menjawab pertanyaan klasik **format column date excel** dan juga mendemonstrasikan **apply number format excel** untuk kolom lain.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Apa yang terjadi di sini?**  
- `StyleNumberFormat.DATE` memberi tahu Excel untuk memperlakukan nilai sel sebagai tanggal singkat (mis., *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` secara otomatis menambahkan simbol `$` dan dua tempat desimal.  
- Menetapkan font menjadi tebal pada kolom pertama membuat header menonjol, yang merupakan kebutuhan umum ketika Anda **how to style excel** spreadsheet untuk keterbacaan.

> **Edge case:** Jika data sumber Anda sudah berisi string yang diformat, Anda mungkin perlu mengonversinya menjadi objek `java.util.Date` sebelum impor; jika tidak, Excel akan memperlakukan mereka sebagai teks biasa.

---

## Langkah 4: Buat Workbook Baru dan Akses Worksheet Pertamanya

Workbook baru memberi kita kanvas bersih. Kami akan mengambil worksheet pertama, tempat impor akan ditempatkan.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Why a new workbook?** Memulai dari awal menjamin tidak ada gaya yang tersisa atau baris tersembunyi yang mengganggu output akhir—penting ketika Anda **how to style excel** file secara konsisten di banyak run.

---

## Langkah 5: Impor DataTable dengan Gaya Kolom

Berikut inti dari operasi: memasukkan `DataTable` ke dalam sheet sambil menerapkan array gaya yang telah kami buat.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Penjelasan:**  
- `importDataTable` menyalin baik baris header maupun baris data.  
- Array `columnStyles` selaras dengan setiap kolom, sehingga header kolom pertama menjadi tebal, kolom kedua menampilkan tanggal, dan kolom ketiga muncul sebagai mata uang.  
- Baris tunggal ini menggantikan puluhan langkah pemformatan sel‑per‑sel manual, menunjukkan cara bersih untuk **apply number format excel** secara programatis.

---

## Langkah 6: Simpan Workbook yang Ditetapkan – Menyelesaikan “Export DataTable to XLSX”

Akhirnya kami menyimpan workbook ke disk. Sesuaikan path ke folder yang dapat ditulisi pada mesin Anda.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Buka file di Excel dan Anda akan melihat:

- Header kolom **ID** dalam huruf tebal.  
- Kolom **OrderDate** diformat sebagai tanggal (mis., *04/27/2024*).  
- Kolom **Total** ditampilkan dengan simbol dolar dan dua desimal.

> **Pro tip:** Jika Anda perlu mendukung versi Excel yang lebih lama, panggil `workbook.save(outputPath, SaveFormat.XLS)` alih-alih default XLSX.

---

## Langkah 7: Verifikasi Hasil & Penyesuaian Opsional

Sangat baik untuk memeriksa kembali file yang dihasilkan, terutama saat mengotomatisasi laporan untuk pemangku kepentingan.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Jika `isBold` mencetak `true`, rutinitas **how to style excel** Anda berhasil seperti yang diharapkan. Dari sini Anda dapat:

- Menambahkan pemformatan bersyarat (mis., menyorot total > $200).  
- Membekukan baris atas untuk memudahkan scroll.  
- Menyisipkan diagram yang merujuk pada data yang diimpor.

Semua ekstensi ini mengikuti pola yang sama: definisikan `Style`, terapkan, dan simpan.

---

## Pertanyaan Umum & Kasus Edge

| Question | Answer |
|----------|--------|
| **Bisakah saya menata lebih dari satu kolom dengan cara yang sama?** | Ya—gunakan kembali satu instance `Style` untuk semua kolom yang berbagi pemformatan. |
| **Bagaimana jika DataTable saya memiliki lebih banyak kolom daripada gaya?** | Setiap kolom tanpa entri yang sesuai di `columnStyles` akan menggunakan gaya default. |
| **Bagaimana cara mengubah format tanggal menjadi “dd‑MMM‑yyyy”?** | Gunakan `columnStyles[1].setCustom("#dd-MMM-yyyy#");` alih-alih `DATE` bawaan. |
| **Apakah ada cara untuk mengubah ukuran kolom secara otomatis setelah impor?** | Panggil `worksheet.autoFitColumns();` setelah `importDataTable`. |
| **Apakah ini akan bekerja di Linux/macOS?** | Tentu—Aspose.Cells bersifat platform‑agnostic selama Anda memiliki JDK yang kompatibel. |

---

## Kesimpulan

Anda kini memiliki contoh lengkap, ujung‑ke‑ujung tentang **how to style Excel** workbook dengan **importing datatable into excel**, **format column date excel**, dan **apply number format excel** menggunakan Java. Kode tersebut menunjukkan alur penuh dari **export datatable to xlsx** hingga membuka file di Excel, mencakup baik *apa* maupun *mengapa* di balik setiap langkah.  

Cobalah: sesuaikan array gaya, tambahkan lebih banyak kolom, atau sambungkan kueri basis data nyata. Pola yang sama akan memungkinkan Anda menghasilkan laporan tampak profesional dengan satu klik tombol, tanpa perlu pemformatan manual.

![Worksheet Excel yang ditata oleh kode tutorial](https://example.com/images/styled-worksheet.png "Tangkapan layar worksheet Excel yang ditata menggunakan Java dan Aspose.Cells")

*Teks alt gambar: “Worksheet Excel yang ditata menggunakan Java dan Aspose.Cells, menampilkan header tebal dan kolom tanggal yang diformat.”*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat & Memformat Sel Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑Demi‑Langkah](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Cara Menata Sel Excel dan Menambahkan Hyperlink Menggunakan Aspose.Cells untuk Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells untuk Java: Cara Membuat dan Memformat Workbook Excel Secara Efisien](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}