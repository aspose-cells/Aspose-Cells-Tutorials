---
date: '2026-10-28'
description: Pelajari cara menempelkan nilai menggunakan Aspose.Cells copy and paste
  options di Java, dengan kode langkah demi langkah, penyiapan dependensi Maven, dan
  tips lisensi.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Pelajari cara menempelkan nilai menggunakan Aspose.Cells copy and
  paste options di Java, dengan kode langkah demi langkah, penyiapan dependensi Maven,
  dan tips lisensi.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Cara menempelkan nilai dengan Aspose.Cells copy and paste options
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Cara menempelkan nilai dengan Aspose.Cells copy and paste options
url: /id/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menempel nilai dengan opsi salin dan tempel Aspose.Cells

Automating Excel reporting in Java means you can generate, consolidate, and format workbooks without ever opening Excel manually. With **Aspose.Cells** you get full control over formulas, hidden rows, and cell values, so your reports stay accurate and lightweight. In this tutorial you’ll learn how to use **CopyOptions.ReferToDestinationSheet** to keep formulas correct and **PasteOptions** to paste only the visible values you need.

## Jawaban cepat
- **Apa yang dilakukan `CopyOptions.ReferToDestinationSheet`?** Itu menulis ulang formula sehingga mengarah ke lembar tujuan setelah operasi salin.  
- **Bagaimana cara menempel hanya sel yang terlihat?** Panggil `PasteOptions.setOnlyVisibleCells(true)` bersama dengan `PasteType.VALUES`.  
- **Versi perpustakaan apa yang diperlukan?** Aspose.Cells 25.3 atau lebih baru.  
- **Apakah saya memerlukan lisensi untuk produksi?** Ya – lisensi permanen atau sementara menghapus batas evaluasi.  
- **Bisakah saya menggunakan Maven atau Gradle?** Kedua-duanya didukung; lihat potongan dependensi di bawah.

## Apa itu “otomatisasi pelaporan Excel”?
Automate Excel reporting means generating and updating Excel workbooks programmatically, allowing you to create, merge, and format reports without manual copy‑paste, which cuts errors and saves hours of repetitive work. This approach is ideal for scheduled batch jobs, data‑driven dashboards, and financial consolidation pipelines.

## Mengapa menggunakan CopyOptions dan PasteOptions untuk pelaporan?
These two classes let you keep formula references intact while copying data **and** extract only the cells that are visible after filtering or hiding rows. Using them together reduces the amount of data transferred by up to 80 % in typical filtered‑table scenarios and guarantees that formulas continue to calculate correctly in the destination sheet.

## Prerequisites
- Java 8 atau lebih tinggi.  
- Maven atau Gradle untuk manajemen dependensi.  
- Aspose.Cells 25.3+ (lisensi percobaan, sementara, atau permanen).  

## Menyiapkan Aspose.Cells untuk java

Add the library to your project with one of the following:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Akuisisi lisensi
- **Free trial** – set fitur lengkap untuk evaluasi.  
- **Temporary license** – menghapus batas percobaan saat Anda menguji.  
- **Permanent license** – direkomendasikan untuk beban kerja produksi.

Initialize Aspose.Cells in your Java code:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Panduan langkah‑demi‑langkah

### 1. copyOptions dengan referToDestinationSheet

#### Ikhtisar
`CopyOptions` is Aspose.Cells' configuration object that controls how formulas and cell references are handled during a copy operation. Setting `CopyOptions.ReferToDestinationSheet` to `true` rewrites formula references so they point to the new sheet after the copy operation.

#### Langkah 1: inisialisasi workbook dan worksheet  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Langkah 2: konfigurasi copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Langkah 3: jalankan operasi copy  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Mengapa ini penting*: Formulas that originally referenced `Sheet1` will now correctly reference `DestSheet`, keeping your automated reports reliable.

**Troubleshooting tip**: If formulas still reference the old sheet, ensure `setReferToDestinationSheet(true)` is called **before** the copy.

### 2. pasteOptions untuk nilai‑saja dari sel yang terlihat

#### Ikhtisar
`PasteOptions` is Aspose.Cells' settings object that defines what gets pasted. Using `PasteType.VALUES` together with `onlyVisibleCells=true` copies just the displayed values, ignoring hidden rows/columns and formatting.

#### Langkah 1: inisialisasi workbook dan worksheet  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Langkah 2: konfigurasi pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Langkah 3: jalankan operasi tempel  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Mengapa ini penting*: Ideal for extracting filtered data or generating clean reports without hidden rows or formatting noise.

**Troubleshooting tip**: Verify that rows/columns are truly hidden in Excel before copying; otherwise, they will be included.

## Aplikasi praktis
1. **Financial consolidation** – gabungkan lembar bulanan ke dalam workbook utama sambil menjaga semua formula tetap akurat.  
2. **Filtered data export** – ambil hanya baris yang terlihat dari tabel terfilter ke dalam lembar ringkasan.  
3. **Scheduled report generation** – otomatisasi pembuatan laporan Excel setiap malam dengan nilai sel yang tepat dan referensi yang benar.

## Pertimbangan kinerja
- **Dispose of workbooks** ketika selesai (`wb.dispose();`) untuk membebaskan sumber daya native.  
- **Batch operations** – kelompokkan beberapa panggilan copy/paste untuk mengurangi overhead.  
- **Monitor memory** – workbook besar mungkin memerlukan heap yang lebih besar (`-Xmx2g`).  
- Aspose.Cells mendukung **lebih dari 50 format input dan output** dan dapat memproses workbook dengan **hingga 2 juta baris** tanpa memuat seluruh file ke memori, memberikan kinerja throughput tinggi untuk beban kerja perusahaan.

## Pertanyaan yang sering diajukan

**T: Apa kegunaan `CopyOptions.ReferToDestinationSheet`?**  
A: Itu menulis ulang referensi formula sehingga mengarah ke lembar tujuan setelah penyalinan, memastikan formula pelaporan tetap benar.

**T: Bagaimana cara menempel hanya sel yang terlihat?**  
A: Set `PasteOptions.setOnlyVisibleCells(true)` dan pilih `PasteType.VALUES`.

**T: Bisakah saya menggunakan Aspose.Cells tanpa membeli lisensi?**  
A: Ya, uji coba gratis atau lisensi sementara tersedia untuk evaluasi, tetapi lisensi permanen diperlukan untuk produksi.

**T: Mengapa beberapa referensi masih salah setelah menyalin?**  
A: Periksa kembali bahwa `ReferToDestinationSheet` diaktifkan **sebelum** operasi penyalinan dan bahwa formula sumber tidak mengandung tautan workbook eksternal.

**T: Praktik terbaik manajemen memori apa yang harus saya ikuti?**  
A: Dispose of `Workbook` objects when finished, process large files in chunks, and monitor JVM heap usage.

**T: Apakah memungkinkan menggabungkan CopyOptions dan PasteOptions dalam satu operasi?**  
A: Ya, Anda dapat menggabungkannya dengan menyalin terlebih dahulu menggunakan `CopyOptions` dan kemudian menerapkan `PasteOptions` pada rentang target.

## Sumber daya
- **Dokumentasi**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Unduh**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Pembelian**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Uji coba gratis**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Lisensi sementara**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Forum dukungan**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Terakhir diperbarui:** 2026-10-28  
**Diuji dengan:** Aspose.Cells 25.3 for Java  
**Penulis:** Aspose

## Tutorial Terkait

- [Baca File Excel Java – Manipulasi Sel Workbook dengan Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Tambah Data ke Sel di Excel Menggunakan Aspose.Cells untuk Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Konversi Indeks Baris Kolom Sel Excel dengan Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}