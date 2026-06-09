---
category: general
date: 2026-06-08
description: Pelajari cara menghasilkan lembar kerja di Java menggunakan smart markers.
  Panduan langkah demi langkah yang mencakup cara menggunakan marker, mengikat koleksi,
  dan mengulang lembar kerja.
draft: false
keywords:
- how to generate worksheets
- how to use markers
- how to expand marker
- how to bind collection
- how to repeat worksheet
language: id
og_description: Cara membuat lembar kerja menggunakan smart markers di Java. Panduan
  ini menunjukkan cara menggunakan marker, mengikat koleksi, memperluas marker, dan
  mengulang lembar kerja dengan mudah.
og_title: Cara membuat lembar kerja dengan Smart Markers – Tutorial Java
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Learn how to generate worksheets in Java using smart markers. Step‑by‑step
    guide covering how to use markers, bind collection and repeat worksheet.
  headline: How to generate worksheets with Smart Markers – Full Java Guide
  type: TechArticle
- description: Learn how to generate worksheets in Java using smart markers. Step‑by‑step
    guide covering how to use markers, bind collection and repeat worksheet.
  name: How to generate worksheets with Smart Markers – Full Java Guide
  steps:
  - name: – Load the template workbook
    text: '> **Why this matters:** The template is your canvas. By keeping the smart
      marker inside the file, you avoid hard‑coding cell addresses in Java. The marker
      `${Employees,RepeatWorksheet}` tells Aspose.Cells to treat the surrounding area
      as a repeatable block.'
  - name: – Bind the collection (how to bind collection)
    text: 'The call `setDataSource("Employees", DataFactory.getEmployees())` does
      two things:'
  - name: – Expand the marker (how to expand marker) and repeat worksheet (how to
      repeat worksheet)
    text: 'Calling `workbook.calculateFormula()` triggers a full evaluation of formulas
      **and** smart markers. During this pass:'
  - name: – Save the workbook
    text: The final `save` call writes everything to disk. The resulting file (`repeating-sheets.xlsx`)
      contains one worksheet per employee, each named automatically (e.g., “Sheet1_JohnDoe”).
      You can rename sheets afterwards via the API if you need a custom naming convention.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara membuat lembar kerja dengan Smart Markers – Panduan Java Lengkap
url: /id/java/templates-reporting/how-to-generate-worksheets-with-smart-markers-full-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menghasilkan lembar kerja dengan Smart Markers – Panduan Lengkap Java

Pernah bertanya-tanya **bagaimana cara menghasilkan lembar kerja** secara otomatis dari satu templat Excel? Anda bukan satu-satunya. Banyak pengembang mengalami kebuntuan ketika mereka membutuhkan lembar terpisah untuk setiap item dalam sebuah daftar—misalnya laporan karyawan, pernyataan bulanan, atau katalog produk. Kabar baik? Smart markers memungkinkan Anda melakukannya dengan hanya beberapa baris kode.

Dalam tutorial ini kami akan menjelaskan **cara menggunakan marker**, mengikat koleksi data, memperluas marker sehingga setiap record mendapatkan lembarnya sendiri, dan akhirnya menyimpan workbook. Pada akhir tutorial Anda akan dapat menjawab pertanyaan “**bagaimana cara menghasilkan lembar kerja**” tanpa menulis loop manual atau melakukan copy‑paste yang rumit.

> **Pro tip:** Jika Anda sudah menggunakan Aspose.Cells untuk Java, pendekatan ini terintegrasi dengan mulus; jika tidak, dapatkan versi percobaan gratis dan ikuti langkah-langkah penyiapan di bagian prasyarat.

## Prasyarat — Apa yang Anda Butuhkan Sebelum Memulai

- **Java 17** (atau JDK terbaru apa pun) – API berfungsi dengan Java 8+ tetapi versi yang lebih baru memberikan kinerja yang lebih baik.
- **Aspose.Cells for Java** (versi terbaru per Juni 2026). Tambahkan dependensi Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the newest release -->
</dependency>
```

- Sebuah **template Excel** (`template-with-marker.xlsx`) yang berisi smart marker seperti `${Employees,RepeatWorksheet}` ditempatkan di mana pun Anda ingin lembar berulang dimulai.
- Sebuah **sumber data** sederhana—dalam contoh ini `DataFactory` statis yang mengembalikan daftar objek `Employee`. Anda dapat menggantinya dengan panggilan basis data nanti.

Jika Anda sudah mencentang semua kotak tersebut, mari kita mulai.

## Cara menghasilkan lembar kerja menggunakan Smart Markers

Berikut adalah program Java lengkap yang dapat dijalankan yang menunjukkan seluruh alur. Kami akan memecahnya langkah demi langkah, menjelaskan **mengapa** setiap baris penting, dan menyisipkan jawaban untuk pertanyaan sekunder seperti **cara mengikat koleksi** dan **cara memperluas marker**.

```java
import com.aspose.cells.*;

public class WorksheetGenerator {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the template workbook that already contains the smart marker
        Workbook workbook = new Workbook("YOUR_DIRECTORY/template-with-marker.xlsx");

        // 2️⃣ Bind the "Employees" collection to the smart marker
        // This answers “how to bind collection” – we simply give the marker a data source
        workbook.getSmartMarkers().setDataSource(
                "Employees",               // marker name used in the template
                DataFactory.getEmployees() // returns List<Employee>
        );

        // 3️⃣ Recalculate formulas – this expands the ${Employees,RepeatWorksheet} marker
        // Here we answer “how to expand marker” and “how to repeat worksheet”
        workbook.calculateFormula();

        // 4️⃣ Save the resulting workbook with each employee on its own sheet
        workbook.save("YOUR_DIRECTORY/repeating-sheets.xlsx");
    }
}
```

### Langkah 1 – Muat workbook templat

> **Mengapa ini penting:** Templat adalah kanvas Anda. Dengan menjaga smart marker di dalam file, Anda menghindari hard‑coding alamat sel di Java. Marker `${Employees,RepeatWorksheet}` memberi tahu Aspose.Cells untuk memperlakukan area di sekitarnya sebagai blok yang dapat diulang.

Jika Anda membuka `template-with-marker.xlsx`, Anda akan melihat sesuatu seperti:

```
${Employees,RepeatWorksheet}
Name: ${Employees.Name}
Dept: ${Employees.Department}
```

Ketika mesin memproses marker, ia akan menggandakan seluruh lembar kerja untuk setiap karyawan dalam koleksi yang terikat.

### Langkah 2 – Mengikat koleksi (cara mengikat koleksi)

Pemanggilan `setDataSource("Employees", DataFactory.getEmployees())` melakukan dua hal:

1. **Mengaitkan** nama marker (`Employees`) dengan koleksi Java.
2. **Memberi** mesin marker data yang diperlukan untuk mengisi setiap lembar yang diulang.

Anda juga dapat melewatkan `DataTable`, `ArrayList<Map<String,Object>>`, atau iterable apa pun yang dapat diintrospeksi oleh Aspose. Kuncinya adalah nama marker dalam templat harus cocok dengan argumen pertama `setDataSource`.

### Langkah 3 – Memperluas marker (cara memperluas marker) dan mengulang lembar kerja (cara mengulang lembar kerja)

Memanggil `workbook.calculateFormula()` memicu evaluasi penuh formula **dan** smart markers. Selama proses ini:

- Token `${Employees,RepeatWorksheet}` dikenali.
- Aspose membuat **lembar kerja baru** untuk setiap entri dalam koleksi `Employees`.
- Semua referensi sel di dalam marker diganti dengan nilai bidang yang sesuai (misalnya, `${Employees.Name}` → “John Doe”).

> **Catatan kasus tepi:** Jika koleksi Anda kosong, Aspose akan membiarkan lembar kerja asli tidak tersentuh. Untuk menghindari file kosong, Anda mungkin ingin memeriksa `DataFactory.getEmployees().isEmpty()` terlebih dahulu.

### Langkah 4 – Simpan workbook

Pemanggilan `save` akhir menulis semuanya ke disk. File yang dihasilkan (`repeating-sheets.xlsx`) berisi satu lembar kerja per karyawan, masing‑masing diberi nama secara otomatis (misalnya, “Sheet1_JohnDoe”). Anda dapat mengganti nama lembar setelahnya melalui API jika memerlukan konvensi penamaan khusus.

#### Output yang Diharapkan

Buka `repeating-sheets.xlsx` dan Anda akan melihat serangkaian tab:

- **Employee_1** – terisi dengan data John.
- **Employee_2** – terisi dengan data Mary.
- …dan seterusnya untuk setiap entri dalam koleksi.

Setiap lembar mencerminkan tata letak yang didefinisikan dalam `template-with-marker.xlsx`, tetapi dengan placeholder diganti oleh nilai nyata.

## Cara menggunakan marker untuk lebih dari sekadar lembar kerja

Smart markers tidak terbatas pada pengulangan lembar. Mereka juga dapat:

- **Mengisi tabel** dalam satu lembar (`${Orders,Repeat}`).
- **Menyisipkan gambar** (`${Employees.Photo}`) ketika sumber data menyimpan aliran biner.
- **Menerapkan pemformatan bersyarat** berdasarkan nilai marker.

Jika Anda pernah perlu menghasilkan laporan multi‑lembar yang menggabungkan halaman ringkasan statis dengan halaman detail dinamis, cukup letakkan marker yang berbeda pada lembar yang berbeda dan ulangi langkah `calculateFormula()` yang sama. Mesin akan menangani setiap marker secara independen.

## Kesalahan umum & cara menghindarinya

- **Kesalahan sintaks marker:** Lupa menambahkan koma atau salah eja nama marker akan menyebabkan mesin mengabaikan token. Periksa kembali string tepat di dalam `${…}`.
- **Ketidaksesuaian tipe data:** Aspose mengharapkan nama properti yang cocok dengan placeholder secara case‑sensitive. Jika kelas `Employee` Anda memiliki `firstName` tetapi marker menulis `${Employees.FirstName}`, sel akan tetap kosong.
- **Koleksi besar:** Menghasilkan ribuan lembar kerja dapat mengonsumsi memori. Pertimbangkan streaming output atau membagi data menjadi batch jika Anda mengalami `OutOfMemoryError`.

## Bonus: Menyesuaikan nama lembar (cara mengulang lembar kerja dengan nama khusus)

Jika Anda ingin setiap lembar memiliki nama yang bermakna (misalnya, ID karyawan), Anda dapat mengganti nama mereka setelah ekspansi marker:

```java
int sheetIndex = 0;
for (Worksheet ws : workbook.getWorksheets()) {
    // Skip the original template sheet if you don't need it
    if (ws.getName().startsWith("Template")) continue;

    // Assume the first cell A1 now holds the employee's ID after expansion
    String employeeId = ws.getCells().get("A1").getStringValue();
    ws.setName("Emp_" + employeeId);
    sheetIndex++;
}
```

Potongan kode ini menunjukkan **cara mengulang lembar kerja** sambil memberikan setiap lembar nama khusus yang diambil dari data itu sendiri.

## Ringkasan – Apa yang Kami Bahas

- **Cara menghasilkan lembar kerja** di Java menggunakan smart markers Aspose.Cells.
- **Cara menggunakan marker** dengan menempatkan `${Collection,RepeatWorksheet}` dalam templat.
- **Cara mengikat koleksi** dengan `setDataSource`.
- **Cara memperluas marker** melalui `calculateFormula`.
- **Cara mengulang lembar kerja** secara otomatis untuk setiap baris data.
- Tips untuk menyesuaikan nama lembar dan menangani kasus tepi.

## Apa Selanjutnya?

Sekarang Anda telah menguasai pembuatan lembar kerja, Anda mungkin ingin menjelajahi:

- **Cara menghasilkan diagram** per lembar (sematkan marker `${ChartData}`).
- **Cara mengekspor ke PDF** setelah lembar kerja dibuat (`workbook.save("output.pdf", SaveFormat.PDF)`).
- **Cara mengintegrasikan dengan Spring Boot** untuk pembuatan laporan secara langsung dalam layanan web.

Silakan bereksperimen—ganti daftar `Employee` dengan pelanggan, pesanan, atau objek domain apa pun. Pola yang sama bekerja di semua kasus.

---

*Siap menerapkan ini ke produksi? Dapatkan Aspose.Cells for Java terbaru, jalankan kode, dan saksikan lembar kerja muncul seperti sulap. Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi resmi Aspose untuk penjelasan lebih mendalam. Selamat coding!*

<img src="how-to-generate-worksheets.png" alt="how to generate worksheets diagram">

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengotomatisasi Excel Smart Markers dengan Aspose.Cells untuk Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Cara Menambahkan Worksheet di Excel Menggunakan Aspose.Cells untuk Java: Panduan Lengkap](/cells/english/java/worksheet-management/add-spreadsheets-excel-aspose-cells-java/)
- [Cara Mengonversi Excel ke PDF di Java Menggunakan Aspose.Cells: Panduan Langkah demi Langkah](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}