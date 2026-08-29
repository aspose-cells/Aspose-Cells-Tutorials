---
date: '2026-08-16'
description: Pelajari cara menambahkan globalisasi di Java menggunakan Aspose.Cells,
  menyesuaikan pesan kesalahan Excel, dan menyiapkan dependensi Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Pelajari cara menambahkan globalisasi di Java menggunakan Aspose.Cells,
  menyesuaikan pesan kesalahan Excel, dan menyiapkan dependensi Maven. Ikuti panduan
  langkah demi langkah.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Cara menambahkan globalisasi di Java dengan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Cara menambahkan globalisasi di Java dengan Aspose.Cells
url: /id/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan globalisasi di Java dengan Aspose.Cells

## Pendahuluan

Menambahkan globalisasi ke workbook Java Anda memungkinkan Anda menampilkan pesan kesalahan, nilai boolean, dan string lain yang spesifik locale dalam bahasa yang diharapkan pengguna. Dalam tutorial ini Anda akan mempelajari **cara menambahkan globalisasi** untuk bahasa Rusia, tetapi pola yang sama berlaku untuk bahasa apa pun. Pada akhir panduan Anda akan dapat:

- Menimpa teks kesalahan default dan representasi boolean.
- Menerapkan pengaturan khusus Anda ke instance `Workbook` mana pun.
- Mengintegrasikan solusi ke dalam proyek Java berbasis Maven yang umum.

Siap membuat file Excel Anda benar‑benar multibahasa? Mari pertama‑tama pastikan lingkungan pengembangan Anda memenuhi prasyarat.

## Jawaban cepat
- **Apa itu globalisasi di Aspose.Cells?** Itu adalah sekumpulan string yang sadar locale (kesalahan, boolean, dll.) yang dapat Anda ganti dengan teks khusus.  
- **Artifact Maven mana yang diperlukan?** `com.aspose:aspose-cells:25.3`.  
- **Bisakah saya menargetkan bahasa selain Rusia?** Ya – perpanjang `GlobalizationSettings` dan timpa metode yang diperlukan untuk setiap locale.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi permanen menghilangkan watermark evaluasi.  
- **Apakah solusi ini thread‑safe?** Terapkan pengaturan per‑workbook; objek `GlobalizationSettings` sendiri tidak dapat diubah setelah dibuat.

## Apa itu globalisasi di Aspose.Cells?

`GlobalizationSettings` adalah objek konfigurasi Aspose.Cells yang mengontrol string spesifik locale seperti pesan kesalahan, nilai boolean, simbol mata uang, dan pola tanggal. Dengan menyediakan subclass Anda sendiri, Anda memberi tahu pustaka teks apa yang harus ditampilkan untuk setiap budaya, memungkinkan Anda mengganti string bahasa Inggris default dengan terjemahan yang sesuai dengan bahasa dan konvensi regional pengguna akhir.

## Mengapa menambahkan globalisasi khusus?

Aspose.Cells mendukung **lebih dari 50 format input dan output** – termasuk XLSX, CSV, PDF, dan ODS – dan dapat memproses workbook dengan **hingga 200 000 baris** tanpa harus memuat seluruh file ke memori. Menyesuaikan globalisasi memastikan pengguna akhir melihat pesan dalam bahasa mereka, mengurangi tiket dukungan hingga diperkirakan **30 %** untuk penyebaran multinasional.

## Prasyarat

- **Java Development Kit** 8 atau yang lebih baru.
- **IDE** seperti IntelliJ IDEA atau Eclipse.
- **Aspose.Cells for Java** versi 25.3 (atau lebih baru) yang ditambahkan melalui Maven atau Gradle.

### Menyiapkan Aspose.Cells untuk Java

Tambahkan dependensi Maven ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Atau, jika Anda lebih suka Gradle, sisipkan berikut ini ke dalam `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Akuisisi lisensi

Aspose menawarkan beberapa opsi lisensi:

- **Free trial** – evaluasi penuh fitur selama 30 hari.  
- **Temporary license** – evaluasi tak terbatas tanpa watermark.  
- **Commercial license** – siap produksi, dengan dukungan prioritas.

Setelah memperoleh file lisensi, atur sekali pada saat aplikasi dimulai:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Cara menambahkan globalisasi untuk bahasa Rusia?

Objek `Workbook` mewakili file Excel yang dimuat ke memori, memberikan akses ke sheet, sel, dan pengaturannya. Muat workbook Anda, buat subclass dari `GlobalizationSettings`, dan lampirkan ke workbook. Jawaban langsungnya: **instansiasi kelas `GlobalizationSettings` khusus, timpa `getErrorValueString` dan `getBooleanValueString`, lalu panggil `workbook.setGlobalizationSettings(customSettings)`**. Pendekatan dua langkah ini menggantikan string bahasa Rusia default dengan milik Anda.

### Mendefinisikan pengaturan khusus

Untuk pertama kalinya Anda menyebut `GlobalizationSettings` dalam panduan ini, perhatikan definisinya:

`GlobalizationSettings` adalah kelas dasar yang digunakan Aspose.Cells untuk mengambil string spesifik locale.  

Sekarang buat subclass yang mengembalikan teks khusus bahasa Rusia:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Menerapkan pengaturan ke workbook

Setelah mendefinisikan subclass, lampirkan ke instance `Workbook` mana pun:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Aplikasi praktis

- **Pelaporan keuangan** – menampilkan kode kesalahan dalam bahasa akuntan, mengurangi kesalahpahaman.  
- **Alat tingkat perusahaan** – menyematkan logika globalisasi yang sama di puluhan utilitas internal berbasis Excel.  
- **Pipeline data otomatis** – memastikan sistem hilir menerima nilai yang sadar locale tanpa langkah terjemahan tambahan.

## Pertimbangan kinerja

Saat Anda mengaktifkan globalisasi khusus, Aspose.Cells tetap memproses formula dan I/O dengan kinerja tinggi yang sama. Untuk menjaga penggunaan memori tetap rendah:

- Lepaskan referensi workbook (`wb.dispose()`) setelah menyimpan.  
- Gunakan `CalculationOptions.setEnableIterativeCalculation(true)` hanya bila diperlukan.  
- Sesuaikan heap JVM (`-Xmx2g`) untuk workbook yang lebih besar dari 100 MB.

## Pertanyaan yang sering diajukan

**Q: Bisakah saya menerapkan pengaturan globalisasi yang sama ke beberapa workbook sekaligus?**  
A: Ya. Buat satu instance `RussianGlobalization` dan berikan ke setiap workbook melalui `setGlobalizationSettings`.

**Q: Bagaimana jika saya perlu mendukung bahasa yang menggunakan skrip kanan‑ke‑kiri?**  
A: Timpa metode tambahan seperti `getCurrencySymbol` dan `getDatePattern` di subclass Anda untuk mengembalikan simbol RTL yang sesuai.

**Q: Apakah lisensi diperlukan untuk versi percobaan agar dapat menggunakan globalisasi khusus?**  
A: Tidak. Versi percobaan sepenuhnya mendukung `GlobalizationSettings`; hanya watermark evaluasi yang muncul pada format output tertentu.

**Q: Bagaimana cara men-debug string kesalahan yang tidak tepat?**  
A: Sisipkan pernyataan `System.out.println` di dalam metode yang Anda timpa untuk memverifikasi nilai `err` yang masuk cocok dengan kasus switch Anda.

**Q: Apakah ini memengaruhi kecepatan perhitungan formula?**  
A: Sangat sedikit. Pustaka hanya mencari string saat merender nilai sel, bukan selama langkah perhitungan menengah.

## Sumber daya tambahan

- **Documentation**: Jelajahi panduan detail di [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Download**: Akses rilis terbaru di [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Purchase**: Beli lisensi untuk penggunaan komersial di [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Free trial**: Mulai dengan percobaan gratis dari [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary license**: Dapatkan lisensi sementara melalui [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support**: Dapatkan bantuan dari komunitas di [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Terakhir diperbarui:** 2026-08-16  
**Diuji dengan:** Aspose.Cells 25.3 untuk Java  
**Penulis:** Aspose

## Tutorial Terkait

- [Aspose.Cells Java: Custom Calculation Engine Guide](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [How to Use Aspose Cells – Excel Engine Tutorials for Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven Dependency – Manage Excel Data Connections with Aspose.Cells in Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}