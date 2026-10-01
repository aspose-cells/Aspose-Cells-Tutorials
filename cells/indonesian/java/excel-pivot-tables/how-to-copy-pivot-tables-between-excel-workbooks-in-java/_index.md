---
category: general
date: 2026-10-01
description: Pelajari cara menyalin tabel pivot antar workbook Excel menggunakan Java.
  Panduan langkah demi langkah ini juga menunjukkan cara menyalin rentang antar workbook
  dan menggandakan rentang Excel dengan aman.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: id
lastmod: 2026-10-01
og_description: Cara menyalin tabel pivot antar workbook Excel menggunakan Java. Ikuti
  panduan ini untuk menyalin rentang ke workbook, menggandakan rentang Excel, dan
  mempertahankan data pivot.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Cara menyalin tabel pivot antar workbook Excel di Java – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Cara menyalin tabel pivot antar workbook Excel di Java
url: /id/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot antara workbook Excel di Java

Jika Anda perlu **how to copy pivot** tabel dari satu file Excel ke file lainnya, panduan ini memberikan solusi siap‑jalankan. Pada akhir dua kalimat pertama Anda akan tahu persis panggilan API mana yang mempertahankan definisi pivot saat menyalin rentang data.

Anda juga akan belajar cara **copy range between workbooks**, **duplicate Excel range** objek, dan dengan aman **copy range to workbook** tanpa kehilangan formula atau pemformatan. Tidak diperlukan skrip eksternal—hanya satu proyek Java yang menggunakan Aspose.Cells for Java.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Java Development Kit 17 atau lebih baru.
* Maven atau Gradle untuk mengelola dependensi.
* Lisensi Aspose.Cells for Java yang valid (evaluasi gratis dapat digunakan untuk pengujian).
* Dua file Excel: `source.xlsx` (mengandung tabel pivot) dan `destination.xlsx` yang kosong (atau biarkan kode membuatnya).

## Langkah 1: Siapkan proyek Maven

Buat sebuah `pom.xml` yang menyertakan Aspose.Cells. Dependensi ini memberikan Anda kelas `Workbook`, `Worksheet`, dan `Range` yang digunakan dalam contoh.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Jaga versi Aspose.Cells tetap terbaru; rilis yang lebih baru menambahkan dukungan yang lebih baik untuk struktur cache pivot yang kompleks.

## Langkah 2: Muat workbook sumber yang berisi tabel pivot

Blok kode pertama menunjukkan **how to copy excel** data dengan memuat file sumber. Konstruktor `Workbook` membaca seluruh file ke memori, mempertahankan semua objek lembar, termasuk pivot.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Mengapa ini penting:* Aspose.Cells menyimpan tabel pivot sebagai bagian dari model internal worksheet. Memuat workbook memastikan cache pivot tersedia untuk penyalinan selanjutnya.

## Langkah 3: Tentukan rentang yang mencakup tabel pivot

Sebuah tabel pivot dapat meluas ke beberapa baris dan kolom. Dalam kebanyakan kasus Anda dapat menyalin seluruh rentang yang digunakan pada lembar. Metode `createRange` membangun objek `Range` yang akan ditangani oleh operasi penyalinan.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Jika pivot meluas melampaui `H20`, cukup ubah string alamatnya. Langkah ini merupakan inti dari penanganan **duplicate excel range**; objek rentang mengetahui formula, gaya, dan baris tersembunyi.

## Langkah 4: Buat workbook baru yang akan menerima rentang yang disalin

Anda dapat memulai dengan workbook kosong atau memuat file tujuan yang sudah ada. Di sini kami membuat workbook baru, yang merupakan cara paling bersih untuk **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Catatan:** Jika Anda perlu menyalin pivot ke nama lembar tertentu, ubah nama `destWs` dengan `destWs.setName("Report")` sebelum menempel.

## Langkah 5: Salin rentang – Aspose.Cells secara otomatis mempertahankan pivot

Metode `copy` memindahkan semua yang ada di dalam rentang sumber, termasuk definisi pivot, cache, dan pemformatan. Tidak diperlukan kode tambahan untuk menjaga pivot tetap berfungsi.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Mengapa ini berhasil:* Aspose.Cells memperlakukan pivot sebagai kumpulan sel tersembunyi dan metadata yang terlampir pada rentang. Saat Anda memanggil `copy`, perpustakaan menyalin metadata tersebut ke workbook target.

## Langkah 6: Simpan workbook tujuan

Akhirnya, tulis hasilnya ke disk. File yang disimpan berisi tabel pivot yang identik yang dapat Anda segarkan atau modifikasi seperti aslinya.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Menjalankan program mencetak konfirmasi dan menghasilkan `destination.xlsx` dengan pivot yang berfungsi penuh.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah, kelas Java lengkapnya terlihat seperti ini:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Output yang diharapkan

* Konsol: `Pivot table copied successfully.`
* `destination.xlsx` dibuka di Excel dengan tabel pivot yang identik dengan yang ada di `source.xlsx`. Menyegarkan pivot menunjukkan sumber data yang sama, membuktikan bahwa **how to copy pivot** berfungsi sebagaimana mestinya.

## Menangani variasi umum

### Menyalin beberapa lembar kerja

Jika proyek Anda memerlukan penyalinan beberapa lembar, lakukan loop melalui worksheet workbook dan ulangi langkah 2‑4 untuk setiap lembar. Pivot di setiap lembar akan dipertahankan secara independen.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Mempertahankan koneksi data eksternal

Tabel pivot yang bergantung pada sumber data eksternal mempertahankan string koneksi setelah disalin. Namun, file tujuan harus memiliki akses ke sumber data yang sama. Verifikasi koneksi dengan membuka pivot dan memeriksa tab **Data**.

### Menangani sel yang digabung

Jika rentang sumber berisi sel yang digabung, Aspose.Cells menyalin tata letak penggabungan secara otomatis. Namun, validasi hasilnya jika workbook tujuan menggunakan lebar kolom default yang berbeda.

## Praktik terbaik untuk penyalinan yang andal

| Praktik | Alasan |
|----------|--------|
| Gunakan rentang yang tepat digunakan (`srcWs.getCells().getMaxDisplayRange()`) alih-alih alamat yang ditulis keras | Menjamin seluruh pivot dan data sumbernya termasuk. |
| Terapkan lisensi sebelum operasi berat | Mencegah watermark evaluasi dan meningkatkan kinerja. |
| Segarkan pivot setelah menyalin (`pivotTable.refresh()`) jika data sumber berubah | Memastikan tujuan mencerminkan nilai terbaru. |
| Tuliskan unit test yang membuka workbook tujuan dan memastikan `pivotTable.getPivotFields().size()` cocok dengan sumber | Mendeteksi kehilangan bidang secara tidak sengaja selama perubahan kode di masa mendatang. |

## Kesimpulan

Anda kini tahu **how to copy pivot** tabel antara workbook Excel di Java, serta cara **copy range between workbooks**, **duplicate excel range**, dan **copy range to workbook** sambil mempertahankan semua pemformatan dan formula. Contoh ini menggunakan Aspose.Cells, yang menyederhanakan penanganan XML tingkat rendah yang diperlukan oleh OpenXML SDK.

Selanjutnya, jelajahi topik terkait seperti **updating pivot cache programmatically**, **exporting pivot data to CSV**, atau **creating pivot tables from scratch**. Masing‑masing topik tersebut dibangun di atas konsep yang sama yang ditunjukkan di sini.

Selamat coding, dan silakan bereksperimen dengan rentang yang lebih besar, beberapa pivot, atau gaya khusus – pola yang sama berlaku untuk semua skenario.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat Tabel Pivot di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cara Menyalin Beberapa Kolom di Excel Menggunakan Aspose.Cells Java: Panduan Lengkap](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Menyalin Gambar Antara Lembar di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}