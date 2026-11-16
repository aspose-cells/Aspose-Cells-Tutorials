---
category: general
date: 2026-11-16
description: Cara menyalin sel antara buku kerja Excel di Java – memuat buku kerja,
  menyalin rentang antara buku kerja (termasuk tabel pivot), dan menyimpan file buku
  kerja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: id
lastmod: 2026-11-16
og_description: Cara menyalin sel antara buku kerja Excel di Java. Pelajari cara memuat
  buku kerja Excel, menyalin rentang (termasuk tabel pivot) antar buku kerja, dan
  menyimpan file buku kerja.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Cara menyalin sel antar buku kerja Excel di Java – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Cara menyalin sel antara buku kerja Excel di Java
url: /id/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin sel antara workbook Excel di Java

Jika Anda perlu **menyalin sel** dari satu workbook Excel ke workbook lain menggunakan Java, panduan ini menunjukkan cara yang dapat diandalkan untuk melakukannya. Anda akan belajar cara **memuat workbook Excel Java**, menyalin rentang yang mungkin berisi tabel pivot, dan akhirnya **menyimpan file workbook** dengan data yang disalin.

Tutorial ini mencakup:

* Memuat workbook sumber dan memilih lembar kerja.  
* Menentukan rentang tepat yang ingin dipindahkan (termasuk tabel pivot).  
* Membuat workbook tujuan dan menyalin rentang.  
* Menyimpan file tujuan.  

Contoh menggunakan pustaka Aspose.Cells untuk Java, yang bekerja dengan file Excel tanpa memerlukan Microsoft Office. Kode berjalan pada Java 8+ dan IDE modern apa pun (IntelliJ IDEA, Eclipse, VS Code, dll.).

---

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

| Persyaratan | Alasan |
|-------------|--------|
| Java Development Kit (JDK) 8 atau yang lebih baru | Diperlukan untuk mengompilasi dan menjalankan kode. |
| Alat build Maven atau Gradle | Mempermudah penambahan dependensi Aspose.Cells. |
| Pustaka Aspose.Cells untuk Java (versi terbaru) | Menyediakan kelas `Workbook`, `Worksheet`, dan `Range` yang digunakan dalam contoh. |
| Dua file Excel (`source.xlsx` dan folder kosong untuk `dest.xlsx`) | File sumber harus berisi data dan, opsional, tabel pivot yang ingin Anda salin. |

Tambahkan dependensi Aspose.Cells ke `pom.xml` (Maven) atau `build.gradle` (Gradle). Contoh untuk Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Cara menyalin sel dengan Aspose.Cells

Langkah‑langkah berikut memandu Anda melalui proses lengkap. Setiap langkah menyertakan kode Java, penjelasan **mengapa** langkah tersebut penting, dan tip untuk menghindari jebakan umum.

### Langkah 1: Muat workbook sumber

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Mengapa?**  
`Workbook` mewakili seluruh file Excel. Memuatnya memberi Anda akses ke semua lembar kerja, sel, dan objek seperti tabel pivot. Menggunakan lembar kerja pertama adalah hal yang umum, tetapi Anda dapat memilih lembar apa pun dengan nama (`srcWb.getWorksheets().get("Sheet2")`).

**Pro tip:**  
Jika file sumber besar, pertimbangkan memuatnya dalam mode *memory‑efficient*: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }})`

### Langkah 2: Tentukan rentang yang mencakup tabel pivot

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Mengapa?**  
Objek `Range` mengabstraksi blok persegi panjang sel. Dengan menentukan `"A1:G20"` Anda memberi tahu Aspose.Cells sel‑sel mana—termasuk tabel pivot yang tertanam—yang akan disalin. Pustaka secara otomatis menyalin data dasar, gaya, dan definisi pivot.

**Kasus tepi:**  
Jika tabel pivot meluas di luar rentang yang ditentukan, perluas alamatnya (misalnya, `"A1:Z100"`). Anda juga dapat menggunakan `srcWs.getCells().getMaxDataColumn()` dan `getMaxDataRow()` untuk menghitung area yang digunakan secara dinamis.

### Langkah 3: Buat workbook tujuan

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Mengapa?**  
Workbook baru memastikan tidak ada format yang tidak diinginkan atau lembar tersembunyi yang mengganggu konten yang disalin. Workbook default sudah berisi satu lembar kerja, yang akan kita gunakan sebagai target.

### Langkah 4: Salin rentang ke workbook tujuan

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Mengapa?**  
`copyRange` menangani semua atribut sel: nilai, formula, format, dan bahkan cache pivot. Dengan menyalin ke `"A1"` Anda menempatkan rentang di sudut kiri‑atas lembar tujuan, mempertahankan tata letak asli.

**Pertanyaan umum:** *Apakah tabel pivot tetap berfungsi?*  
Ya. Aspose.Cells menyalin definisi tabel pivot dan cache‑nya, sehingga pivot bekerja persis seperti di workbook sumber.

### Langkah 5: Simpan workbook tujuan

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Mengapa?**  
Pemanggilan `save` menulis workbook yang berada di memori ke file fisik `.xlsx`. Anda juga dapat menyimpan ke format lain (`.xls`, `.csv`, `.pdf`) dengan mengubah ekstensi file atau menggunakan `SaveOptions`.

**Tip:**  
Jika Anda perlu mengalirkan file ke respons web, gunakan `destWb.save(OutputStream, SaveFormat.XLSX);` alih‑alih jalur file.

---

## Salin rentang antara workbook – kode sumber lengkap

Berikut adalah kelas Java lengkap yang siap dijalankan. Ganti `YOUR_DIRECTORY` dengan folder sebenarnya di mesin Anda.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Hasil yang diharapkan:**  
`dest.xlsx` berisi replika tepat dari rentang `A1:G20` dari `source.xlsx`. Jika rentang sumber berisi tabel pivot, file tujuan menampilkan pivot yang sama dengan sumber data yang terhubung ke sel‑sel yang disalin.

Anda dapat membuka `dest.xlsx` di Excel, LibreOffice, atau penampil apa pun yang mendukung `.xlsx` untuk memverifikasi bahwa nilai, format, dan fungsi pivot tetap terjaga.

---

## Salin workbook tabel pivot – hal yang perlu Anda ketahui

* **Cache pivot disalin secara otomatis.** Pustaka mentransfer cache yang mendasari, sehingga pivot tidak perlu disegarkan secara manual.
* **Sumber data eksternal tidak dipindahkan.** Jika pivot mengambil data dari basis data eksternal, Anda harus memastikan workbook tujuan dapat mengakses sumber yang sama, atau membuat ulang cache secara lokal.
* **Tabel pivot besar dapat meningkatkan penggunaan memori.** Untuk workbook yang sangat besar, pertimbangkan meningkatkan heap JVM (`-Xmx2g`) untuk menghindari `OutOfMemoryError`.

---

## Simpan file workbook dalam format berbeda

Aspose.Cells memungkinkan Anda menyimpan hasil ke banyak format tanpa perubahan kode tambahan:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Pilih format yang sesuai dengan proses hilir Anda. Logika `copyRange` yang sama bekerja terlepas dari format akhir.

---

## Memuat workbook Excel Java – tips tambahan

* **Memuat file terenkripsi:** Gunakan `LoadOptions` dengan kata sandi:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Membaca hanya lembar kerja tertentu:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Opsi‑opsi ini dapat mempercepat langkah **load excel workbook java**, terutama untuk file besar.

---

## Kesimpulan

Anda kini tahu **cara menyalin sel** antara workbook Excel di Java, cara **menyalin rentang antara workbook** yang berisi **tabel pivot**, dan cara **menyimpan file workbook** dalam format yang Anda butuhkan. Dengan mengikuti langkah‑langkah di atas, Anda dapat mengintegrasikan manipulasi data Excel ke dalam aplikasi Java apa pun—baik Anda membangun mesin pelaporan, pipeline ETL, atau utilitas konversi file sederhana.

**Langkah selanjutnya** yang dapat Anda jelajahi:

* Gunakan **copy range between workbooks** untuk menggabungkan beberapa laporan menjadi


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}