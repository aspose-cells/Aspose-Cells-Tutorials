---
category: general
date: 2026-03-01
description: Cara membuat PDF dan menyimpan workbook sebagai PDF, mengekspor Excel
  ke HTML, serta menggunakan fungsi expand dengan Aspose.Cells untuk Java. Kode langkah
  demi langkah disertakan.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: id
og_description: Cara membuat PDF dari workbook menggunakan Aspose.Cells untuk Java.
  Pelajari cara menyimpan workbook sebagai PDF, mengekspor Excel ke HTML, dan menggunakan
  fungsi EXPAND.
og_title: Cara Membuat PDF dari Workbook – Tutorial Java
tags:
- Aspose.Cells
- Java
- PDF generation
title: Cara Membuat PDF dari Workbook – Panduan Java Lengkap
url: /id/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat PDF dari Workbook – Panduan Java Lengkap

Pernah bertanya-tanya **how to create PDF** langsung dari workbook Excel tanpa harus menggunakan konverter pihak ketiga? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mereka membutuhkan ekspor PDF cepat, pratinjau HTML, atau rumus array canggih—semuanya dalam satu langkah.  

Dalam tutorial ini kami akan membahas satu program Java yang berdiri sendiri dan melakukan hal tersebut. Kami akan **save workbook as PDF**, menunjukkan cara **export Excel to HTML** sambil mempertahankan baris beku, dan mendemonstrasikan **use expand function** di dalam lembar kerja. Pada akhir tutorial Anda akan memiliki proyek yang dapat dijalankan dan dapat dimasukkan ke dalam build Maven atau Gradle mana pun.

> **Pro tip:** Semua kode di bawah ini bekerja dengan Aspose.Cells 23.10 (atau lebih baru). Jika Anda menggunakan versi yang lebih lama, beberapa nama metode mungkin sedikit berbeda.

---

## Prasyarat

- **Java 17** (atau versi LTS apa pun) terinstal dan dikonfigurasi.
- **Aspose.Cells for Java** library. Tambahkan dependensi Maven berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- IDE atau editor teks pilihan Anda (IntelliJ IDEA, VS Code, Eclipse…).

Tidak ada API eksternal, tidak ada layanan web—hanya Java murni dan SDK Aspose.Cells.

---

## Gambaran Umum Solusi

Kami akan membagi implementasi menjadi **tujuh langkah logis**:

1. Buat sebuah workbook dan demonstrasikan fungsi **EXPAND**.  
2. Aktifkan font variation selectors dan **save the workbook as PDF**.  
3. Ekspor workbook yang sama ke HTML sambil mempertahankan baris beku.  
4. Gunakan Smart Marker dengan parameter `IF` untuk menyisipkan teks bersyarat.  
5. Terapkan master‑detail Smart Marker untuk data hierarkis.  
6. Muat file Markdown yang berisi gambar Base‑64‑encoded.  
7. Konfigurasikan opsi GridJs untuk perataan dan border, lalu sisipkan data.

Setiap langkah dibungkus dalam metode masing‑masing untuk menjaga metode `main` tetap rapi dan untuk mengilustrasikan **mengapa** kita melakukan apa yang kita lakukan, bukan hanya **apa** yang kita ketik.

---

## Langkah 1 – Buat Workbook dan Gunakan Fungsi EXPAND

Fungsi **EXPAND** adalah rumus dynamic‑array baru yang diperkenalkan di Office 365. Fungsi ini memungkinkan Anda menumpahkan rentang ke area yang lebih besar tanpa menyalin sel secara manual.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Mengapa ini penting:**  
- `EXPAND` secara otomatis menambahkan spasi kosong pada hasil, yang sempurna ketika Anda kemudian **save workbook as PDF**—PDF akan menampilkan tabel bersih dan berbentuk persegi panjang.  
- Memanggil `calculateFormula()` memastikan mesin rumus dijalankan sebelum kami mengekspor apa pun.

---

## Langkah 2 – Aktifkan Font Variation Selectors dan **Save Workbook as PDF**

Jika Anda perlu mendukung tipografi lanjutan (misalnya emoji atau CJK variation selectors), Anda harus mengaktifkan fitur ini **sebelum** menyimpan.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Poin penting:** Kata kunci utama **how to create pdf** dijawab di sini—dengan memanggil `workbook.save(..., SaveFormat.PDF)` setelah mengonfigurasi pengaturan.

---

## Langkah 3 – **Export Excel to HTML** Sambil Mempertahankan Baris Beku

Seringkali pemangku kepentingan meminta pratinjau web cepat. Aspose.Cells dapat mengekspor ke HTML, dan dengan `setPreserveFrozenRows(true)` kami mempertahankan pengalaman menggulir yang sama seperti di Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Mengapa ini penting:** Baris beku merupakan fitur kenyamanan penggunaan; tanpa mereka, baris header akan menghilang ketika pengguna menggulir ke bawah halaman.

---

## Langkah 4 – Smart Marker dengan Parameter IF

Smart Markers memungkinkan Anda menggabungkan data ke dalam template tanpa menulis loop. Parameter `if` menambahkan logika bersyarat langsung di dalam marker.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

PDF output akan menampilkan **“VIP Customer: Acme Corp”** karena `IsVIP` bernilai `true`. Ubah flag menjadi `false` dan Anda akan mendapatkan **“Regular Customer: Acme Corp”**—tanpa kode tambahan.

---

## Langkah 5 – Master‑Detail Smart Marker Menggunakan Rentang Hierarkis

Ketika Anda memiliki data induk‑anak (misalnya, pesanan dan item baris), marker master‑detail menghemat Anda dari penyisipan baris manual.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**Apa yang Anda dapatkan:** Mesin memperluas baris master untuk setiap pesanan dan secara otomatis menempatkan baris detail di bawahnya—sempurna untuk faktur atau laporan pembelian.

---

## Langkah 6 – Muat Dokumen Markdown dengan Gambar Base‑64 yang Disematkan

Jika data sumber Anda berada dalam Markdown (umum dalam alur kerja dokumentasi), Aspose.Cells dapat merendernya langsung ke dalam workbook.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Catatan kasus tepi:** Jika string Base‑64 tidak valid, Aspose akan melewatkan gambar tetapi tetap memproses sisa dokumen—tanpa crash.

---

## Langkah 7 – Konfigurasikan Opsi GridJs dan Sisipkan Data

GridJs adalah grid JavaScript ringan yang dapat dirender oleh Aspose ke dalam HTML. Menyelaraskan angka dan menerapkan border meningkatkan keterbacaan.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Mengapa ini penting:** Penyelarasan yang tepat dan border membuat HTML yang dihasilkan tampak seperti spreadsheet yang rapi—berguna untuk dasbor.

---

## Menggabungkan Semua – Metode `main`

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}