---
category: general
date: 2026-08-20
description: Buat smart marker lembar kerja di Java menggunakan Aspose.Cells dan kontrol
  penamaan lembar detail dengan SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: id
lastmod: 2026-08-20
og_description: Buat smart marker lembar kerja di Java dengan Aspose.Cells. Pelajari
  cara memberi nama lembar detail secara dinamis menggunakan SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Buat smart markers lembar kerja – Panduan Java dengan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Cara membuat smart marker pada lembar kerja dengan Aspose.Cells
url: /id/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat smart markers pada lembar kerja dengan Aspose.Cells

Jika Anda perlu **membuat smart markers pada lembar kerja** dalam workbook Java, panduan ini menunjukkan langkah‑langkah tepat untuk melakukannya dengan Aspose.Cells. Anda akan melihat cara mengonfigurasi `SmartMarkerOptions` sehingga setiap lembar detail mendapatkan nama yang unik dan dapat diprediksi.

Membuat laporan Excel yang memperluas templat master‑detail merupakan kebutuhan umum dalam sistem keuangan, inventaris, dan pelaporan. Menggunakan smart markers menghilangkan duplikasi lembar secara manual dan memungkinkan Anda fokus pada data alih‑alih infrastruktur.

## Apa yang akan Anda pelajari

* Cara memuat workbook master yang berisi smart markers.  
* Cara mengatur `SmartMarkerOptions` untuk mengendalikan penamaan lembar detail yang dihasilkan.  
* Cara menyediakan `DataTable` dengan data contoh dan menerapkannya pada smart markers.  
* Cara menyimpan hasil sehingga setiap lembar kerja detail memiliki nama yang berbeda, menghindari duplikat nama lembar.

**Prasyarat**  
* Java 17 atau lebih baru (kode juga dapat dikompilasi dengan JDK 8+).  
* Aspose.Cells for Java 23.9 atau yang lebih baru – perpustakaan menyediakan kelas `Workbook`, `SmartMarkerOptions`, dan kelas terkait lainnya.  
* Sebuah IDE seperti IntelliJ IDEA, Eclipse, atau VS Code.

Konsep sekunder yang akan Anda temui meliputi **Aspose.Cells Java**, **smart marker options**, dan penanganan **duplicate sheet names** ketika templat diperluas.

## Membuat smart markers pada lembar kerja – panduan langkah‑demi‑langkah

Bagian‑bagian berikut membagi proses menjadi langkah‑langkah terpisah yang dapat digunakan kembali. Setiap langkah mencakup cuplikan kode, penjelasan mengapa langkah tersebut penting, dan tip praktis untuk menghindari jebakan umum.

### Langkah 1: Siapkan proyek Maven dan tambahkan Aspose.Cells

Buat modul Maven baru (atau proyek Gradle) dan tambahkan dependensi Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Mengapa langkah ini penting** – Perpustakaan menyediakan kelas `Workbook` yang membaca dan menulis file Excel, serta mesin smart‑marker yang memperluas templat Anda secara otomatis. Tanpa dependensi yang tepat, kompiler tidak dapat menemukan panggilan API yang digunakan nanti.

> **Pro tip:** Jika Anda bekerja di belakang proxy perusahaan, konfigurasikan `settings.xml` Maven untuk mengambil repositori Aspose secara aman.

### Langkah 2: Muat workbook master yang berisi smart markers

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Mengapa langkah ini penting** – Workbook master mendefinisikan tata letak, formula, dan tag placeholder (`«SmartMarker»`) yang akan digantikan oleh mesin. Memuat file sekali saja menjaga penggunaan memori tetap rendah dan memungkinkan Anda menggunakan kembali workbook yang sama untuk beberapa set data.

### Langkah 3: Konfigurasikan SmartMarkerOptions untuk nama lembar detail khusus

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Mengapa langkah ini penting** – Secara default Aspose.Cells membuat lembar detail dengan nama generik seperti “DetailSheet”. Ketika templat diperluas untuk banyak baris, nama‑nama tersebut bentrok, menyebabkan **duplicate sheet names** dan pengecualian runtime. Pola `"DetailSheet_{0}"` menjamin nama unik per baris, menyelesaikan masalah duplikasi.

### Langkah 4: Bangun DataTable yang cocok dengan bidang smart marker

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Mengapa langkah ini penting** – `DataTable` menyediakan nilai sebenarnya yang menggantikan placeholder smart marker. Nama kolom harus cocok dengan nama marker dalam templat; jika tidak, mesin akan melewatkan penggantian secara diam‑diam.

> **Kesalahan umum:** Menggunakan nama kolom yang berbeda huruf kapital (misalnya “id” vs “Id”) menyebabkan data hilang pada lembar yang dihasilkan.

### Langkah 5: Terapkan data ke smart markers dengan opsi penamaan

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Mengapa langkah ini penting** – Metode `apply` memicu mesin smart‑marker. Ia membaca setiap baris, membuat lembar detail baru menggunakan pola penamaan dari `SmartMarkerOptions`, dan mengisi lembar dengan data baris tersebut. Panggilan tunggal ini menggantikan puluhan baris kode kloning lembar manual dan pengisian sel.

### Langkah 6: Simpan workbook dan verifikasi hasilnya

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Setelah dijalankan, buka `MasterDetailDuplicatedNames.xlsx`. Anda akan melihat:

* Lembar master asli tidak berubah.  
* Dua lembar kerja baru bernama `DetailSheet_1` dan `DetailSheet_2`.  
* Setiap lembar detail berisi nilai dari baris yang bersesuaian dalam `DataTable`.

**Mengapa langkah ini penting** – Menyimpan workbook menyelesaikan proses ekspansi smart‑marker. File kini dapat dikirim ke sistem hilir, dilampirkan pada email, atau dibuka di Excel untuk analisis lebih lanjut.

## Menangani kasus tepi dan variasi

### Beberapa lembar master

Jika templat Anda berisi lebih dari satu lembar master, iterasi setiap smart marker pada tiap lembar:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Penamaan khusus di luar indeks baris

Anda dapat menyisipkan kolom data apa pun ke dalam nama lembar dengan menggunakan placeholder seperti `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Pastikan kolom `OrderId` ada dalam `DataTable` yang diberikan.

### Mencegah nama lembar yang terlalu panjang

Excel membatasi nama lembar hingga 31 karakter. Jika pola penamaan Anda berisiko melebihi batas ini, potong atau hash nilai tersebut:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Kemudian proses nama yang dihasilkan dengan `StringUtils.abbreviate` sebelum mengirimkannya ke Aspose.

## Contoh lengkap yang dapat dijalankan

Berikut adalah file sumber lengkap yang dapat Anda salin, sesuaikan jalur file, dan jalankan langsung:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Output yang diharapkan**

* `MasterDetailDuplicatedNames.xlsx` berisi:

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mastering Aspose.Cells Java: Utilize Smart Markers for Dynamic Data in Worksheets](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Create Dynamic Charts with Smart Markers in Aspose.Cells for Java | Step-by-Step Guide](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}