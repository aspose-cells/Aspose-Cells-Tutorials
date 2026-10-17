---
category: general
date: 2026-03-01
description: Salin tabel pivot di Java sambil mempertahankan pivot, kemudian ekspor
  Excel ke PPTX, nonaktifkan AutoFilter Excel, dan gunakan Smart Marker untuk array
  JSON – panduan langkah demi langkah lengkap.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: id
og_description: Salin tabel pivot di Java, pertahankan definisi pivot, ekspor ke PPTX,
  nonaktifkan AutoFilter, dan gunakan Smart Marker – panduan lengkap untuk pengembang.
og_title: Salin Tabel Pivot di Java – Pertahankan, Ekspor ke PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Salin Tabel Pivot di Java – Pertahankan, Ekspor ke PPTX
url: /id/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Tabel Pivot di Java – Pertahankan, Ekspor ke PPTX

Pernahkah Anda perlu **menyalin tabel pivot** dari satu workbook ke workbook lain tanpa kehilangan definisi pivot yang mendasarinya? Anda bukan satu-satunya yang kebingungan tentang hal ini. Dalam banyak proyek dunia nyata, Anda akan menemukan diri Anda memindahkan data, dan hal terakhir yang Anda inginkan adalah pivot yang rusak yang menghasilkan error saat runtime.  

Dalam tutorial ini kami akan membahas solusi lengkap yang tidak hanya **menyalin tabel pivot** tetapi juga menunjukkan cara **mempertahankan tabel pivot** saat menyalin, **mengekspor Excel ke PPTX**, **menonaktifkan Excel AutoFilter**, dan **menggunakan smart marker** untuk menempatkan array JSON ke dalam satu sel. Pada akhir tutorial Anda akan memiliki satu program Java yang dapat dijalankan yang mencakup keempat skenario.

## Prasyarat

- Java 8 atau lebih baru (kode ini juga bekerja dengan Java 11)  
- Perpustakaan Aspose.Cells untuk Java (versi 23.9 atau lebih baru) – Anda dapat mengunduhnya dari Maven Central  
- Familiaritas dasar dengan konsep Excel seperti tabel pivot, tabel, dan kotak teks  

Jika Anda belum memiliki JAR Aspose.Cells, tambahkan ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Sekarang, mari kita mulai.

## Langkah 1: Salin Tabel Pivot – Mempertahankan Definisi Pivot

Ketika Anda hanya menyalin rentang sel yang berisi tabel pivot, metadata pivot sering tertinggal. Aspose.Cells memberikan cara yang rapi untuk mempertahankan definisi tetap dengan menggunakan `copyRange` dengan instance `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Mengapa ini berhasil:** `CopyOptions` memberi tahu Aspose.Cells untuk membawa semua, termasuk cache pivot dan pengaturan field. Tanpa itu, Anda akan mendapatkan nilai biasa dan kehilangan kemampuan untuk menyegarkan pivot.

**Kasus khusus:** Jika pivot sumber Anda mencakup lebih dari `A1:G20` yang dikodekan secara tetap, sesuaikan rentangnya atau gunakan `sourceSheet.getPivotTables().get(0).getDataRange()` untuk mengambilnya secara dinamis.

![Contoh menyalin tabel pivot](image.png "Menyalin tabel pivot di Java")

*Teks alt gambar: diagram menyalin tabel pivot di Java*

## Langkah 2: Ekspor Worksheet dengan TextBox yang Dapat Diedit ke PPTX

Seringkali Anda perlu mengubah lembar Excel menjadi slide PowerPoint—pikirkan dasbor mingguan yang harus dipresentasikan. Aspose.Cells dapat langsung menyimpan worksheet sebagai file PPTX sambil mempertahankan bentuk seperti text box.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Apa yang terjadi:** Metode `save` dengan `SaveFormat.PPTX` mengonversi seluruh sheet, termasuk TextBox yang dapat diedit, menjadi slide PowerPoint. Teks di dalam kotak tetap dapat diedit saat Anda membuka PPTX di PowerPoint.

**Tip:** Jika Anda memiliki beberapa sheet dan hanya menginginkan satu sheet tertentu, panggil `wb.getWorksheets().removeAt(index)` untuk yang lainnya sebelum menyimpan.

## Langkah 3: Nonaktifkan Excel AutoFilter dari Tabel

AutoFilter berguna bagi pengguna akhir, tetapi terkadang Anda perlu mematikannya secara programatis—mungkin sebelum mengekspor data atau saat menghasilkan laporan bersih. Berikut cara **menonaktifkan excel autofilter** pada tabel Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Mengapa Anda mungkin memerlukannya:** Mengekspor ke format yang tidak mendukung AutoFilter (seperti CSV atau PDF) dapat menyebabkan ikon filter muncul. Menonaktifkannya memastikan output yang bersih.

**Kesalahan umum:** Jika sheet tidak memiliki tabel, `getTables().get(0)` akan melempar `IndexOutOfBoundsException`. Selalu periksa `sheet.getTables().size()` terlebih dahulu dalam kode produksi.

## Langkah 4: Gunakan Smart Marker – Sisipkan Array JSON sebagai Nilai Sel Tunggal

Smart Marker adalah mesin templating Aspose. Salah satu trik berguna adalah memperlakukan seluruh array JSON sebagai nilai sel tunggal, yang sempurna untuk pencatatan atau mengirim data terstruktur ke downstream. Mari **gunakan smart marker** untuk mencapai ini.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Cara kerjanya:** Penanda `${json}` dalam workbook digantikan oleh seluruh string JSON karena kami mengatur `ArrayAsSingle`. Tanpa opsi ini, Aspose akan mencoba memperluas setiap elemen array ke baris terpisah.

**Variasi:** Jika Anda membutuhkan array dibagi ke beberapa baris, cukup hilangkan `ArrayAsSingle` dan biarkan Smart Marker menangani ekspansi secara otomatis.

## Contoh Kerja Lengkap – Semua Langkah Digabungkan

Berikut adalah satu kelas Java yang menggabungkan semua operasi yang telah kami bahas. Jalankan sebagai metode `main` biasa; cukup sesuaikan jalur file agar sesuai dengan lingkungan Anda.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}