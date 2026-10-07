---
category: general
date: 2026-01-14
description: Cara menyematkan font dalam HTML dan memaksa perhitungan rumus saat mengonversi
  Excel ke HTML. Pelajari cara mengatur area cetak dan mengekspor diagram.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- force formula calculation
- convert excel to html
- how to set print area
language: id
og_description: Cara menyematkan font di HTML, memaksa perhitungan rumus, dan mengonversi
  Excel ke HTML dengan pengaturan area cetak—semua dalam C#.
og_title: Cara Menyematkan Font di HTML – Panduan Lengkap C#
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cara Menyematkan Font di HTML – Panduan Lengkap C#
url: /id/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyematkan Font dalam HTML – Panduan Lengkap C#

Pernah bertanya-tanya **bagaimana cara menyematkan font dalam HTML** saat mengekspor workbook Excel? Anda tidak sendirian. Banyak pengembang mengalami kendala ketika HTML yang dihasilkan terlihat baik di mesin mereka tetapi kehilangan tipografinya di perangkat lain. Kabar baik? Dengan Aspose.Cells untuk .NET Anda dapat menyematkan file font yang tepat langsung ke dalam output HTML—tidak ada lagi glyph yang hilang.

Dalam tutorial ini kami akan membahas contoh full‑stack yang tidak hanya menunjukkan **bagaimana cara menyematkan font dalam HTML**, tetapi juga mendemonstrasikan **memaksa perhitungan formula**, **mengonversi Excel ke HTML**, dan bahkan **cara mengatur area cetak** sebelum mengekspor diagram ke PPTX yang dapat diedit. Pada akhir tutorial Anda akan memiliki satu program C# yang dapat dijalankan dan dapat Anda masukkan ke dalam proyek .NET apa pun.

---

## Apa yang Akan Anda Bangun

- Buat workbook baru, tulis beberapa formula array, dan **memaksa perhitungan formula** sehingga hasilnya tertanam dalam file.
- Simpan workbook sebagai HTML sambil **menyematkan font** dan selector variasinya.
- Muat workbook kedua yang berisi diagram, tentukan **area cetak**, dan ekspor lembar tersebut ke presentasi PowerPoint yang dapat diedit.
- Semua ini menggunakan hanya beberapa baris kode C# yang bersih dan berkomentar baik.

Tidak ada alat eksternal, tidak ada penyalinan manual file font—Aspose.Cells melakukan pekerjaan berat untuk Anda.

---

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 atau lebih baru | Fitur bahasa modern dan kinerja yang lebih baik |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Menyediakan `Workbook`, `HtmlSaveOptions`, `ImageOrPrintOptions`, dll. |
| Beberapa file font TrueType/OpenType (mis., `Arial.ttf`) yang ditempatkan di folder proyek | Diperlukan untuk penyematan; Aspose akan mengambilnya secara otomatis jika font tersebut terpasang di OS host |
| Pengetahuan dasar C# | Untuk mengikuti kode dan menyesuaikannya dengan skenario Anda sendiri |

---

## Langkah 1 – Buat Workbook dan Tulis Formula Array  

Pertama kami membuat instance `Workbook` baru dan menambahkan dua formula array ke sel **A1** dan **A3**. Formula ini (`WRAPCOLS` dan `WRAPROWS`) menghasilkan array kecil 2‑kolom/2‑baris yang nantinya akan kita lihat ter‑render dalam output HTML.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Write WRAPCOLS formula – returns a 2‑column array
            worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4},2)";

            // Write WRAPROWS formula – returns a 2‑row array
            worksheet.Cells[2, 0].Formula = "=WRAPROWS({1;2;3;4},2)";
```

> **Mengapa ini penting:** Dengan menyisipkan formula Anda mendapatkan konten dinamis yang akan dievaluasi ketika kami memaksa perhitungan nanti. Ini juga menunjukkan bahwa ekspor HTML dapat menangani hasil array dengan benar.

---

## Langkah 2 – Paksa Perhitungan Formula  

Aspose.Cells mengevaluasi formula secara malas. Untuk memastikan bahwa HTML kami berisi nilai yang telah dihitung (bukan formula mentah), kami memanggil `CalculateFormula()`.

```csharp
            // Step 2: Force calculation so the formulas are evaluated
            worksheet.CalculateFormula();
```

> **Tip pro:** Jika Anda melewatkan langkah ini, HTML akan menampilkan teks formula (`=WRAPCOLS...`) alih‑alih angka, yang mengalahkan tujuan ekspor yang rapi.

---

## Langkah 3 – Konfigurasikan Opsi Penyimpanan HTML untuk Menyematkan Font  

Sekarang hadir bintang utama: penyematan font. Mengatur `EmbedFonts` ke `true` memberi tahu Aspose untuk menyertakan data font sebagai aliran yang di‑encode Base64 di dalam file HTML yang dihasilkan. Mengaktifkan `EmbedFontVariationSelectors` memastikan bahwa semua selector variasi OpenType (digunakan untuk tipografi lanjutan) juga dipertahankan.

```csharp
            // Step 3: Prepare HTML save options that embed fonts and their variation selectors
            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                EmbedFontVariationSelectors = true
            };
```

> **Cara kerjanya:** Saat HTML ditulis, Aspose menyisipkan blok `<style>` dengan aturan `@font-face` yang merujuk ke data URI yang disematkan. Browser akan merender font yang persis sama terlepas dari font yang terpasang pada klien.

---

## Langkah 4 – Simpan Workbook sebagai HTML  

Kami menyimpan workbook ke file `.xlsx` terlebih dahulu (untuk berjaga‑jaga jika Anda memerlukan sumbernya) dan kemudian mengekspornya ke HTML menggunakan opsi yang baru saja kami definisikan.

```csharp
            // Step 4: Save the workbook as HTML using the configured options
            string outputDir = @"C:\Demo\Output\"; // adjust to your environment
            workbook.Save(Path.Combine(outputDir, "fontDemo.xlsx"));
            workbook.Save(Path.Combine(outputDir, "fontDemo.html"), htmlSaveOptions);
```

> **Hasil:** Buka `fontDemo.html` di browser modern apa pun dan Anda akan melihat nilai array ter‑render dengan font yang disematkan, bahkan jika font tersebut tidak terpasang di mesin Anda.

---

## Langkah 5 – Muat Workbook dengan Diagram dan Atur Area Cetak  

Selanjutnya kami mendemonstrasikan **cara mengatur area cetak** sebelum mengekspor lembar yang berisi diagram. Area cetak membatasi apa yang akan dirender, yang berguna ketika Anda hanya menginginkan rentang tertentu dalam PPTX akhir.

```csharp
            // Step 5: Load a workbook that contains a chart and configure PPTX export options
            Workbook chartWorkbook = new Workbook(Path.Combine(outputDir, "chartEditable.xlsx"));

            // Define the print area (e.g., A1:G20) – this is the SECONDARY keyword in action
            chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:G20";
```

> **Mengapa mengatur area cetak?** Tanpanya, Aspose akan mengekspor seluruh lembar, berpotensi menarik baris/kolom kosong dan memperbesar ukuran file PPTX.

---

## Langkah 6 – Ekspor Worksheet ke PPTX yang Dapat Diedit  

Akhirnya kami mengekspor worksheet ke file PowerPoint yang dapat diedit. Dengan mengatur `ExportChartAsEditable = true`, diagram disimpan sebagai bentuk native PowerPoint, memungkinkan pengguna akhir untuk memodifikasinya langsung di PowerPoint.

```csharp
            // Step 6: Configure PPTX export options
            ImageOrPrintOptions pptSaveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartAsEditable = true
            };

            // Step 7: Save as editable PPTX
            chartWorkbook.Save(Path.Combine(outputDir, "editableChart.pptx"), pptSaveOptions);
        }
    }
}
```

> **Apa yang Anda dapatkan:** `editableChart.pptx` berisi diagram dari `chartEditable.xlsx` sebagai objek PowerPoint yang dapat diedit, terbatas pada rentang `A1:G20`.

---

## Ikhtisar Output yang Diharapkan  

| File | Deskripsi |
|------|-----------|
| `fontDemo.xlsx` | Workbook asli dengan formula array yang telah dihitung. |
| `fontDemo.html` | File HTML yang **menyematkan font**, menampilkan hasil array, dan dapat bekerja offline. |
| `editableChart.pptx` | Presentasi PowerPoint dengan diagram yang dapat diedit, menghormati **area cetak** yang Anda atur. |

Buka `fontDemo.html` di Chrome atau Edge; Anda akan melihat teks menggunakan font persis yang Anda sematkan (misalnya Arial) bahkan jika sistem Anda tidak memilikinya. Diagram dalam `editableChart.pptx` dapat diklik dua kali dan diedit seperti diagram native PowerPoint mana pun.

---

## Pertanyaan Umum & Kasus Tepi  

### Bagaimana jika font saya tidak terpasang di server?  
Aspose.Cells hanya akan menyematkan font yang *tersedia* untuk runtime. Jika file font tertentu hilang, HTML akan kembali ke font default browser. Untuk menjamin penyematan, salin file `.ttf`/`.otf` yang diperlukan ke folder aplikasi Anda dan referensikan mereka melalui `FontInfo` (skenario lanjutan).

### Bisakah saya menyematkan hanya subset karakter untuk mengurangi ukuran file?  
Ya. Gunakan `HtmlSaveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`. Ini memberi tahu Aspose untuk menyertakan hanya glyph yang benar‑benar digunakan dalam workbook, secara dramatis mengecilkan payload HTML.

### Apakah **paksa perhitungan formula** juga bekerja untuk fungsi volatile seperti `NOW()`?  
Tentu saja. `CalculateFormula()` mengevaluasi semua formula, termasuk yang volatile, pada saat Anda memanggilnya. Jika Anda memerlukan perhitungan yang mencerminkan tanggal/waktu tertentu, atur `CalculationOptions` workbook sebelumnya.

### Bagaimana dengan workbook besar – apakah penyematan font akan membuat HTML menjadi besar?  
Penyematan font menambahkan sekitar 100‑200 KB per font (tergantung ukuran). Untuk laporan besar, pertimbangkan untuk menautkan ke font yang di‑host di web alih‑alih menyematkan, atau gunakan mode subset yang disebutkan sebelumnya.

---

## Tips Pro & Praktik Terbaik  

- **Simpan batch:** Jika Anda menghasilkan puluhan file HTML, gunakan kembali satu instance `HtmlSaveOptions` untuk menghindari alokasi yang tidak perlu.  
- **Cache area cetak:** Saat mengekspor banyak lembar, simpan area cetak yang diinginkan dalam file konfigurasi untuk menjaga kode Anda tetap DRY.  
- **Validasi output:** Setelah menyimpan HTML, jalankan pemeriksaan cepat dengan browser headless (mis., Puppeteer) untuk memastikan font dirender dengan benar sebelum dikirim ke pengguna.  
- **Kunci versi:** Kode di atas menargetkan Aspose.Cells 23.12+. Versi yang lebih baru mungkin memperkenalkan opsi tambahan seperti `FontEmbeddingMode`. Selalu periksa catatan rilis.

---

## Kesimpulan  

Kami telah membahas **cara menyematkan font dalam HTML** menggunakan Aspose.Cells, menunjukkan pentingnya **paksa perhitungan formula**, mendemonstrasikan alur kerja **mengonversi Excel ke HTML** yang bersih, dan menjelaskan **cara mengatur area cetak** sebelum mengekspor diagram ke PPTX yang dapat diedit. Contoh lengkap yang dapat dijalankan berada dalam satu file `Program.cs`, sehingga Anda dapat menyalin‑tempel, menyesuaikan jalur, dan menjalankannya hari ini.

Siap untuk langkah selanjutnya? Cobalah mengganti font yang disematkan dengan tipe huruf khusus merek, atau bereksperimen dengan mode penyematan `Subset` untuk menjaga HTML tetap ringan. Pola yang sama bekerja untuk PDF, gambar, bahkan ekspor CSV—cukup ubah kelas `SaveOptions`.

Ada pertanyaan lebih lanjut tentang penyematan font, penanganan formula, atau trik area cetak? Tinggalkan komentar di bawah atau hubungi saya di forum komunitas Aspose. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}