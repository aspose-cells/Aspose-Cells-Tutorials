---
category: general
date: 2026-08-20
description: Pelajari cara mengekspor Excel ke TXT sambil membatasi angka desimal,
  mempertahankan digit signifikan, dan menyimpan buku kerja sebagai TXT menggunakan
  Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: id
lastmod: 2026-08-20
og_description: Ekspor Excel ke TXT dengan Aspose.Cells. Panduan ini menunjukkan cara
  membatasi angka desimal, mempertahankan digit signifikan, dan menyimpan workbook
  sebagai TXT di Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Ekspor Excel ke TXT dalam Java – kontrol tempat desimal dan digit signifikan
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Cara mengekspor Excel ke TXT dengan Aspose.Cells dan mengontrol presisi desimal
url: /id/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor Excel ke TXT dengan Aspose.Cells dan mengontrol presisi desimal

Jika Anda perlu **mengekspor Excel ke TXT** dan memastikan output menghormati jumlah tempat desimal tertentu, panduan ini menyediakan solusi lengkap. Anda akan melihat cara membatasi tempat desimal, mempertahankan digit signifikan, dan **menyimpan workbook sebagai TXT** menggunakan pustaka Aspose.Cells untuk Java.

Tutorial ini menjelaskan langkah demi langkah membuat workbook, menyisipkan nilai presisi tinggi, mengonfigurasi opsi penyimpanan TXT, dan menulis file ke disk. Pada akhir tutorial Anda dapat menghasilkan file teks yang berisi presisi tepat yang Anda butuhkan, tanpa pemrosesan manual setelahnya.

## Apa yang Anda perlukan

- Java 17 (atau JDK yang didukung)
- Aspose.Cells untuk Java 23.10 atau yang lebih baru
- IDE atau alat build (Maven/Gradle) untuk mengelola dependensi
- Izin menulis ke direktori output

## Langkah 1: Buat workbook dan akses lembar kerja pertama

Membuat workbook adalah langkah pertama ketika Anda ingin **mengekspor Excel ke TXT**. Kelas `Workbook` mewakili seluruh file Excel, dan `Worksheet` memberi Anda akses ke sel-selnya.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Mengapa ini penting*: Objek workbook menyimpan semua data, gaya, dan metadata. Memulai dengan workbook baru memastikan tidak ada pemformatan tersembunyi yang mengganggu ekspor teks.

## Langkah 2: Tambahkan nilai numerik dan batasi tempat desimal

Sisipkan angka yang memiliki banyak tempat desimal sehingga Anda dapat mendemonstrasikan cara **membatasi tempat desimal** saat mengekspor.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Mengapa ini penting*: Excel menyimpan presisi penuh, tetapi ketika Anda mengekspor nanti, Anda mungkin ingin memotong atau membulatkan nilai tersebut. Pengaturan `limit decimal places` akan menangani ini secara otomatis.

## Langkah 3: Konfigurasikan opsi penyimpanan TXT untuk mempertahankan digit signifikan

Aspose.Cells menyediakan `TxtSaveOptions`. Menetapkan `significantDigits` memberi tahu exporter untuk menyimpan hanya jumlah digit bermakna yang diperlukan, mengabaikan nol di depan.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Mengapa ini penting*: Opsi **keep significant digits** memastikan file output berisi jumlah presisi yang dapat diprediksi, yang penting bagi sistem hilir yang mengharapkan format numerik lebar tetap.

## Langkah 4: Simpan workbook sebagai TXT

Akhirnya, tulis workbook ke file teks. Metode `save` menghormati opsi yang telah Anda konfigurasikan, sehingga file yang dihasilkan akan berisi representasi desimal yang telah dibatasi.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Mengapa ini penting*: Menggunakan **save workbook as txt** dengan `TxtSaveOptions` yang telah dipersiapkan menjamin file yang diekspor sesuai dengan batasan presisi yang Anda tetapkan pada langkah sebelumnya.

### Konten yang diharapkan dari `SignificantDigits.txt`

```
0.00012346
```

Nilai tersebut menunjukkan lima digit signifikan (`12346`) setelah pembulatan, dan nol di depan dipertahankan sesuai format TXT.

## Variasi dan kasus tepi

| Skenario | Penyesuaian |
|----------|------------|
| **Jumlah digit signifikan yang berbeda** | Panggil `txtOptions.setSignificantDigits(n)` dimana `n` antara 1‑15. |
| **Mengekspor rentang alih-alih seluruh lembar** | Gunakan `txtOptions.setExportRange("A1:B10")` sebelum menyimpan. |
| **Mempertahankan pemisah kolom** | Atur `txtOptions.setSeparator('\t')` untuk output berpisah tab. |
| **Lembar kerja besar** | Tingkatkan `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` untuk menghindari `OutOfMemoryError`. |

## Kesalahan umum dan tips profesional

- **Jangan bingungkan digit signifikan dengan tempat desimal**. Nol di depan tidak dihitung sebagai signifikan; gunakan `setSignificantDigits` untuk presisi bermakna dan `setDecimalPlaces` jika Anda memerlukan jumlah digit tetap setelah titik desimal.
- **Selalu tentukan jalur output absolut** saat menjalankan dari IDE untuk menghindari kesalahan izin.
- **Validasi file yang dihasilkan** dengan panggilan sederhana `java.nio.file.Files.readAllLines(Paths.get(outputPath))` untuk memastikan kontennya sesuai harapan sebelum diteruskan ke proses hilir.

## Kode sumber lengkap untuk referensi

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Menjalankan program menghasilkan `SignificantDigits.txt` yang berisi satu baris `0.00012346`, menunjukkan bahwa proses **export excel to txt** menghormati baik persyaratan **limit decimal places** maupun **keep significant digits**.

## Kesimpulan

Anda kini tahu cara **mengekspor Excel ke TXT** menggunakan Aspose.Cells untuk Java sambil mengontrol presisi numerik. Dengan mengonfigurasi `TxtSaveOptions` Anda dapat **membatasi tempat desimal**, **mempertahankan digit signifikan**, dan secara andal **menyimpan workbook sebagai txt** tanpa pemrosesan tambahan.

Selanjutnya, Anda dapat menjelajahi:

- Mengekspor beberapa lembar ke file TXT terpisah (`save workbook as txt` per lembar)
- Menggunakan `setSeparator` untuk membuat output yang kompatibel CSV
- Mengotomatiskan konversi batch untuk kumpulan data besar

Silakan bereksperimen dengan jumlah digit dan pemisah yang berbeda untuk menyesuaikan kebutuhan proyek Anda secara tepat. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat dan Mengekspor Excel ke HTML Menggunakan Aspose.Cells Java | Panduan Operasi Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Simpan Excel sebagai Teks – Panduan Lengkap C# untuk Mengekspor Excel ke TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Ekspor Workbook Excel sebagai Gambar Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}