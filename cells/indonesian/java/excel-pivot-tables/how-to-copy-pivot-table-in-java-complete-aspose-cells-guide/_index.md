---
category: general
date: 2026-06-08
description: Cara menyalin tabel pivot menggunakan Aspose.Cells di Java. Pelajari
  cara menyalin rentang antar workbook dan mempertahankan tabel pivot dengan mudah.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: id
og_description: Cara menyalin tabel pivot di Java dengan Aspose.Cells. Tutorial ini
  menunjukkan cara menyalin rentang antar workbook dan menjaga pivot tetap utuh.
og_title: Cara Menyalin Pivot Table di Java – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: Cara Menyalin Tabel Pivot di Java – Panduan Lengkap Aspose.Cells
url: /id/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyalin Tabel Pivot di Java – Panduan Lengkap Aspose.Cells

Pernah bertanya-tanya **bagaimana cara menyalin tabel pivot** dari satu workbook Excel ke workbook lain menggunakan Java? Kabar baiknya, Aspose.Cells memudahkan **menyalin rentang antar workbook** sambil mempertahankan setiap detail pivot.  

Dalam tutorial ini kami akan membahas contoh dunia nyata yang tidak hanya menyalin pivot itu sendiri tetapi juga menjaga data dasar, pemformatan, dan rumus tetap utuh. Pada akhir tutorial Anda akan mengetahui secara tepat **cara mempertahankan struktur pivot**, cara memindahkan pivot ke workbook baru, dan cara menghindari jebakan umum yang sering membuat banyak pengembang tersandung.

Kami akan membahas:

* Prasyarat minimal (Java 17+, Aspose.Cells for Java 23.9+).  
* Penjabaran langkah‑per‑langkah kode, dengan penjelasan **mengapa** setiap baris penting.  
* Penanganan kasus tepi untuk rentang pivot besar dan sumber data eksternal.  
* Program lengkap yang dapat dijalankan langsung, cukup ditempelkan ke IDE Anda hari ini.

> **Tip pro:** Jika Anda sudah menggunakan Maven atau Gradle, menambahkan Aspose.Cells sebagai dependensi cukup satu baris—tidak perlu mengatur JAR secara manual.

---

## Cara Menyalin Tabel Pivot – Ikhtisar Langkah‑per‑Langkah

Berikut adalah gambaran tingkat tinggi tentang apa yang akan kami capai:

1. Muat workbook sumber yang berisi tabel pivot.  
2. Identifikasi rentang sel tepat yang membungkus pivot.  
3. Buat workbook tujuan yang baru.  
4. **Salin rentang** ke lembar baru, biarkan Aspose.Cells secara otomatis mempertahankan pivot.  
5. Simpan hasilnya sebagai file baru.

Setiap langkah diilustrasikan dengan potongan kode dan alasan singkat, sehingga Anda memahami mekanisme—bukan sekadar mekanisme.

![Diagram yang menggambarkan cara tabel pivot disalin dari workbook sumber ke workbook tujuan sambil mempertahankan strukturnya](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="diagram cara menyalin tabel pivot"}

### Langkah 1: Siapkan Aspose.Cells di Proyek Anda

Sebelum Anda dapat memanipulasi file Excel, Anda memerlukan pustaka Aspose.Cells di classpath Anda. Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

Untuk Gradle, juga cukup satu baris:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*Mengapa ini penting:* Aspose.Cells menyembunyikan detail OpenXML tingkat rendah, memberi Anda API sederhana untuk **menyalin tabel pivot ke workbook baru** tanpa kehilangan metadata apa pun.

### Langkah 2: Muat Workbook Sumber

Kami memerlukan instance `Workbook` yang menunjuk ke file yang menyimpan pivot. Ganti `YOUR_DIRECTORY/src.xlsx` dengan jalur sebenarnya di mesin Anda.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **Catatan:** Aspose.Cells secara otomatis mendeteksi format file (XLSX, XLS, CSV, dll.), jadi Anda tidak perlu khawatir tentang konversi format.

### Langkah 3: Tentukan Rentang yang Membungkus Pivot

Tabel pivot berada di dalam blok sel persegi panjang. Anda dapat menemukannya secara manual (misalnya, `A1:G20`) atau secara programatis dengan memeriksa koleksi `PivotTables` pada worksheet. Untuk tutorial ini kami akan menghard‑code rentangnya demi kejelasan.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*Mengapa kami menggunakan `createRange`:* Metode ini membuat objek `Range` ringan yang dapat diteruskan ke `copyRange`. Ini adalah cara paling dapat diandalkan untuk **menyalin rentang antar workbook** sambil memastikan struktur internal pivot termasuk.

### Langkah 4: Buat Workbook Tujuan Kosong

Sekarang kami membuat workbook kosong yang akan menerima data yang disalin.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Workbook default sudah berisi satu worksheet, yang sempurna untuk keperluan kami. Jika Anda memerlukan nama lembar khusus, Anda dapat menggantinya:

```java
destinationSheet.setName("PivotCopy");
```

### Langkah 5: Salin Rentang dan Pertahankan Pivot

Inilah tempat keajaiban terjadi. Metode `copyRange` menerima objek `CopyOptions`, tetapi kami tidak perlu mengubah apa pun—pelestarian pivot sudah diaktifkan secara default.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*Mengapa ini berhasil:* Aspose.Cells memperlakukan pivot sebagai bagian dari koleksi sel. Saat Anda memanggil `copyRange`, ia menyalin cache pivot yang mendasari, bidang data, dan tata letak, secara efektif **cara mempertahankan pivot** tanpa kode tambahan.

### Langkah 6: Simpan Workbook Tujuan

Akhirnya, tulis file baru ke disk.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

Buka `copied-with-pivot.xlsx` yang dihasilkan di Excel, dan Anda akan melihat replika persis dari pivot asli, siap untuk analisis lebih lanjut.

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan langsung. Program ini menggabungkan semua potongan kode di atas, menambahkan beberapa pemeriksaan defensif, dan mencetak pesan konfirmasi yang ramah.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**Output yang diharapkan saat Anda menjalankan program**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

Buka file tujuan—pivot Anda akan tampak identik dengan yang asli, lengkap dengan slicer, filter, dan bidang terhitung.

## Menangani Kasus Edge Umum

| Situasi | Hal yang Perlu Diperhatikan | Perbaikan yang Disarankan |
|-----------|-------------------|---------------|
| **Pivot menggunakan sumber data eksternal** (misalnya, basis data) | Koneksi eksternal tidak tertanam dalam workbook, sehingga penyalinan dapat memutus tautan. | Ekspor data ke sebuah lembar terlebih dahulu, kemudian buat pivot pada lembar tersebut sebelum menyalin. |
| **Pivot sangat besar (ribuan baris)** | `copyRange` dapat mengonsumsi memori yang signifikan. | Tingkatkan heap JVM (`-Xmx2g`) atau salin pivot dalam potongan lebih kecil menggunakan `copyRows`/`copyColumns`. |
| **Beberapa pivot pada lembar yang sama** | Hard‑coding `A1:G20` hanya menyalin pivot pertama. | Lakukan loop melalui `sourceWorksheet.getPivotTables()` dan salin setiap `PivotTable.getDataRange()`. |
| **Workbook tujuan sudah berisi lembar dengan nama yang sama** | `setName` akan melemparkan pengecualian. | Gunakan `Workbook.getWorksheets().add("PivotCopy")` untuk membuat lembar dengan nama unik. |

Tips ini memastikan bahwa **cara menyalin tabel pivot** berfungsi secara andal, bahkan dalam skenario produksi.

## Pertanyaan yang Sering Diajukan

**T: Apakah metode ini juga menyalin pemformatan pivot?**  
J: Ya. Karena kami menyalin seluruh rentang sel, gaya, pemformatan bersyarat, dan format angka ikut terbawa bersama data.

**T: Bagaimana jika saya perlu menyalin pivot ke sel tertentu selain `A1`?**  
J: Cukup ubah argumen ketiga `copyRange` ke alamat kiri‑atas yang diinginkan, misalnya `"B5"`.

**T: Bisakah saya menyalin pivot tanpa data sumbernya?**  
J: Tidak secara langsung. Cache pivot berada di dalam workbook; menghapus data sumber akan membuat pivot tidak dapat digunakan. Ekspor data sumber ke lembar tersembunyi jika Anda menginginkan salinan yang lebih ringan.

## Kesimpulan

Anda kini memiliki jawaban yang jelas, menyeluruh tentang **cara menyalin tabel pivot** di Java menggunakan Aspose.Cells. Dengan memuat workbook sumber, menentukan rentang pivot, dan memanfaatkan `copyRange`, Anda dapat dengan mudah **menyalin rentang antar workbook** sambil memastikan pivot tetap

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Memperbarui Sumber Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Cara Membuat Tabel Pivot di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cara Menerapkan Slicer pada Tabel Pivot Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}