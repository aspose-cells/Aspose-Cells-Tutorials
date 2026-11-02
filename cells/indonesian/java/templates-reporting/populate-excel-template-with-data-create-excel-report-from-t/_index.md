---
category: general
date: 2026-06-30
description: Isi templat Excel dengan data menggunakan SmartMarkerProcessor dan pelajari
  cara membuat laporan Excel dari templat di Java – panduan langkah demi langkah.
draft: false
keywords:
- populate excel template with data
- create excel report from template
- smartmarkerprocessor java
- excel automation java
- java data source excel
language: id
og_description: Isi templat Excel dengan data menggunakan SmartMarkerProcessor. Panduan
  ini menunjukkan cara membuat laporan Excel dari templat di Java, lengkap dengan
  kode.
og_title: Isi Template Excel dengan Data – Buat Laporan Excel dari Template
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  headline: Populate Excel Template with Data – Create Excel Report from Template
  type: TechArticle
- description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  name: Populate Excel Template with Data – Create Excel Report from Template
  steps:
  - name: Instantiate the SmartMarkerProcessor
    text: The processor is the engine that scans your workbook, finds Smart Markers,
      and replaces them with real values.
  - name: '(Optional): Rename the Detail Sheet'
    text: Smart Markers often generate a hidden “detail” sheet that holds intermediate
      data. Renaming it makes the final workbook easier to navigate.
  - name: Load the Template Workbook
    text: This is where you point the processor at the Excel file that contains the
      markers.
  - name: Prepare a Data Source
    text: SmartMarkerProcessor expects an `IDataSource` implementation that knows
      how to fetch values for each marker. Below is a minimal **in‑memory** data source
      that uses a `Map<String, Object>`.
  - name: Apply the Data to the Workbook
    text: Now the magic happens—Smart Markers are replaced with the values from your
      `IDataSource`.
  - name: Save the Processed Workbook
    text: Finally, write the populated workbook to disk (or stream it directly to
      HTTP response if you’re in a web app).
  - name: 'H3: Handling Collections (Tables)'
    text: If your template contains a repeating block like a sales table, replace
      the marker with an array in your data source.
  - name: 'H3: Formatting Dates and Numbers'
    text: 'Smart Markers respect cell formatting. If you pre‑format a cell as *Currency*
      in the template, the numeric value you push through will automatically display
      with the correct symbol and decimal places. No extra code needed—just make sure
      the data type you return (`Double`, `BigDecimal`, `LocalDate`) '
  - name: 'H3: Performance Considerations'
    text: '- **Reuse the processor** if you generate dozens of reports in a batch;
      just call `processor.clear()` between runs. - **Turn off calculation** (`workbook.getSettings().setRecalcOnLoad(false)`)
      when you only need to write values, not recalculate formulas. - **Stream the
      output** to avoid large tempor'
  type: HowTo
tags:
- excel
- java
- reporting
- smartmarker
title: Isi Template Excel dengan Data – Buat Laporan Excel dari Template
url: /id/java/templates-reporting/populate-excel-template-with-data-create-excel-report-from-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Isi Template Excel dengan Data – Buat Laporan Excel dari Template

Pernah perlu **populate Excel template with data** tetapi tidak yakin perpustakaan mana yang dapat menangani pekerjaan berat? Anda tidak sendirian. Ketika Anda membuat dasbor bulanan, faktur, atau spreadsheet berbasis data apa pun, melakukannya secara manual dengan cepat menjadi mimpi buruk.  

Kabar baiknya, SmartMarkerProcessor dari Aspose.Cells membuatnya mudah—cukup beri template dan sumber data, dan Anda akan memiliki laporan Excel yang rapi dalam hitungan detik. Dalam tutorial ini kami juga akan menunjukkan **how to create Excel report from template** menggunakan Java murni, sehingga Anda dapat langsung memasukkan solusi ke dalam proyek Anda.

## Prerequisites (What you’ll need)

- Java 17 atau lebih baru (kode dapat dikompilasi dengan versi lebih lama, tetapi 17 memberikan fitur bahasa terbaru).  
- Aspose.Cells for Java (artefak Maven `com.aspose:aspose-cells` versi 24.9 atau lebih baru).  
- File Excel yang berisi Smart Markers (misalnya, `input.xlsx`).  
- Sumber data sederhana yang mengimplementasikan `IDataSource` (kami akan membuatnya untuk Anda).  

Tidak diperlukan IDE khusus—editor apa pun yang dapat mengompilasi Java sudah cukup.  

---

## Isi Template Excel dengan Data – Langkah‑per‑Langkah

Di bawah ini kami membagi proses menjadi enam langkah logis. Setiap langkah mencakup **why** mengapa penting, bukan hanya **what** yang harus diketik.

### Step 1: Instantiate the SmartMarkerProcessor  

Processor adalah mesin yang memindai workbook Anda, menemukan Smart Markers, dan menggantinya dengan nilai sebenarnya.

```java
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Mengapa?*  
Membuat processor baru memastikan Anda memulai dengan keadaan bersih. Jika Anda menggunakan kembali instance lama, pengaturan yang tersisa dapat memengaruhi run berikutnya—sesuatu yang pasti ingin Anda hindari dalam pekerjaan produksi.

### Step 2 (Optional): Rename the Detail Sheet  

Smart Markers sering menghasilkan sheet “detail” tersembunyi yang menyimpan data menengah. Mengganti namanya membuat workbook akhir lebih mudah dinavigasi.

```java
// Step 2: (Optional) Set a new name for the detail sheet that will be generated
processor.setDetailSheetNewName("CopyOfDetail");
```

*Tips Pro:*  
Jika template Anda sudah berisi sheet bernama “Detail”, beri sheet yang dihasilkan suffix unik (misalnya, `CopyOfDetail_2024`) untuk mencegah bentrok nama.

### Step 3: Load the Template Workbook  

Di sinilah Anda mengarahkan processor ke file Excel yang berisi marker.

```java
// Step 3: Load the workbook that contains Smart Markers
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Mengapa?*  
Memuat workbook ke memori memungkinkan Aspose.Cells memanipulasinya tanpa menyentuh file asli di disk. Anda dapat dengan aman menggunakan kembali file template yang sama untuk banyak laporan.

### Step 4: Prepare a Data Source  

SmartMarkerProcessor mengharapkan implementasi `IDataSource` yang tahu cara mengambil nilai untuk setiap marker. Di bawah ini adalah sumber data **in‑memory** minimal yang menggunakan `Map<String, Object>`.

```java
// Step 4: Prepare the data source that provides values for the markers
class MapDataSource implements IDataSource {
    private final Map<String, Object> data;

    public MapDataSource(Map<String, Object> data) {
        this.data = data;
    }

    @Override
    public Object getValue(String key) {
        return data.get(key);
    }

    @Override
    public boolean isArray(String key) {
        // For this simple example we never return arrays
        return false;
    }

    @Override
    public int getLength(String key) {
        return 0; // not an array
    }

    @Override
    public Object getValue(String key, int index) {
        return null; // not an array
    }
}

// Example data that matches the markers in input.xlsx
Map<String, Object> values = new HashMap<>();
values.put("EmployeeName", "Jane Doe");
values.put("Department", "Engineering");
values.put("Salary", 95000);
values.put("ReportDate", LocalDate.now().toString());

IDataSource dataSource = new MapDataSource(values);
```

*Mengapa implementasi ini?*  
Ini ringan, tidak memerlukan basis data eksternal, dan sempurna untuk demo atau unit test. Dalam skenario dunia nyata Anda akan mengganti `MapDataSource` dengan sesuatu yang mengambil data dari result set JDBC, REST API, atau entitas ORM.

### Step 5: Apply the Data to the Workbook  

Sekarang keajaiban terjadi—Smart Markers digantikan dengan nilai dari `IDataSource` Anda.

```java
// Step 5: Apply the data to the workbook, generating the detail sheet
processor.apply(workbook, dataSource);
```

*Apa yang terjadi di balik layar?*  
Aspose.Cells mengiterasi setiap sel yang berisi marker seperti `${EmployeeName}`. Untuk setiap marker, ia memanggil `IDataSource.getValue("EmployeeName")` dan menulis nilai yang dikembalikan ke sel. Jika Anda memiliki marker tabel (`${Employees}`), processor secara otomatis akan memperluas baris berdasarkan panjang array.

### Step 6: Save the Processed Workbook  

Akhirnya, tulis workbook yang telah diisi ke disk (atau streaming langsung ke respons HTTP jika Anda berada dalam aplikasi web).

```java
// Step 6: Save the processed workbook
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

*Tips:*  
Gunakan overload `workbook.save(OutputStream, SaveFormat.XLSX)` ketika Anda perlu mengirim file ke klien tanpa menyentuh sistem file.

---

## Create Excel Report from Template – Advanced Tips

Sekarang alur dasar sudah berfungsi, mari jelajahi beberapa peningkatan umum yang membuat **Excel report from template** siap produksi.

### H3: Handling Collections (Tables)

Jika template Anda berisi blok berulang seperti tabel penjualan, gantilah marker dengan array di sumber data Anda.

```java
class ListDataSource implements IDataSource {
    private final Map<String, List<Map<String, Object>>> tables = new HashMap<>();

    public void addTable(String name, List<Map<String, Object>> rows) {
        tables.put(name, rows);
    }

    @Override
    public boolean isArray(String key) {
        return tables.containsKey(key);
    }

    @Override
    public int getLength(String key) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows == null ? 0 : rows.size();
    }

    @Override
    public Object getValue(String key, int index) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows != null ? rows.get(index) : null;
    }

    @Override
    public Object getValue(String key) {
        // Not used for arrays
        return null;
    }
}

// Sample table data
List<Map<String, Object>> sales = new ArrayList<>();
sales.add(Map.of("Product", "Widget A", "Qty", 120, "Revenue", 4800));
sales.add(Map.of("Product", "Widget B", "Qty", 75,  "Revenue", 3375));

ListDataSource listSource = new ListDataSource();
listSource.addTable("SalesData", sales);

// Apply as before
processor.apply(workbook, listSource);
```

Di template Anda akan memiliki marker seperti `${SalesData.Product}`, `${SalesData.Qty}`, dll., di dalam baris yang akan direplikasi Aspose untuk setiap entri.

### H3: Formatting Dates and Numbers

Smart Markers menghormati pemformatan sel. Jika Anda memformat sel sebagai *Currency* di template, nilai numerik yang Anda masukkan akan otomatis ditampilkan dengan simbol dan tempat desimal yang tepat. Tidak perlu kode tambahan—pastikan tipe data yang Anda kembalikan (`Double`, `BigDecimal`, `LocalDate`) sesuai dengan format yang diharapkan.

### H3: Performance Considerations

- **Reuse the processor** jika Anda menghasilkan puluhan laporan dalam satu batch; cukup panggil `processor.clear()` di antara run.  
- **Turn off calculation** (`workbook.getSettings().setRecalcOnLoad(false)`) ketika Anda hanya perlu menulis nilai, bukan menghitung ulang formula.  
- **Stream the output** untuk menghindari file sementara besar saat dijalankan di lingkungan terbatas.

## Expected Output

Setelah menjalankan contoh enam‑langkah, `output.xlsx` akan berisi:

| A               | B          | C            |
|-----------------|------------|--------------|
| EmployeeName    | Jane Doe   |              |
| Department      | Engineering|              |
| Salary          | 95,000     |              |
| ReportDate      | 2026‑06‑30 |              |
| …               | …          | …            |

Jika Anda menambahkan contoh tabel, Anda akan melihat tabel penjualan yang terisi penuh tepat di bawah baris header. Semua pemformatan yang Anda terapkan di `input.xlsx` (simbol mata uang, pola tanggal, header tebal) tetap utuh.

---

## Conclusion

Kami baru saja menjelaskan cara **populate Excel template with data** menggunakan `SmartMarkerProcessor` dari Aspose.Cells, dan Anda sekarang mengetahui langkah‑langkah tepat untuk **create Excel report from template** dalam Java. Ide dasarnya sederhana: definisikan Smart Markers dalam workbook yang dapat digunakan kembali, berikan `IDataSource` yang sesuai, dan biarkan perpustakaan menangani pekerjaan berat.

Dari sini Anda dapat:
- Menghubungkan basis data nyata menggantikan `MapDataSource`.  
- Menambahkan chart yang secara otomatis mencerminkan data baru.  
- Menyebarkan kode sebagai microservice yang mengembalikan file Excel yang dihasilkan sesuai permintaan.  

Cobalah, sesuaikan marker, dan saksikan alur kerja pelaporan Anda menyusut secara dramatis. Ada pertanyaan atau skenario marker yang rumit? Tinggalkan komentar di bawah—selamat coding!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Isi Excel dengan Data Bersarang Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Ekspor Data XML dari Excel menggunakan Aspose.Cells di Java: Panduan Langkah‑per‑Langkah](/cells/english/java/import-export/export-excel-xml-data-aspose-cells-java/)
- [Cara Membuat & Memformat Sel Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑per‑Langkah](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}