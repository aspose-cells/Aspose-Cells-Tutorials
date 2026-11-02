---
category: general
date: 2026-06-30
description: Buat pemformatan bersyarat dalam buku kerja Excel menggunakan Aspose.Cells.
  Pelajari cara mengatur latar belakang sel, memberi peringkat sel, dan membuat file
  secara programatis.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: id
og_description: Buat format bersyarat dalam buku kerja Excel menggunakan Aspose.Cells.
  Ikuti tutorial lengkap ini untuk mengatur latar belakang sel, memberi peringkat
  sel, dan mengotomatisasi Excel.
og_title: Buat Pemformatan Bersyarat di Excel dengan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat Pemformatan Bersyarat di Excel dengan Aspose.Cells – Panduan Langkah demi
  Langkah
url: /id/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Pemformatan Bersyarat di Excel dengan Aspose.Cells – Panduan Langkah‑per‑Langkah

Pernah bertanya-tanya bagaimana cara **create conditional formatting** dalam file Excel tanpa membuka UI? Anda tidak sendirian. Banyak pengembang perlu **create excel workbook** secara cepat, dan melakukannya secara programatik menghemat jam kerja manual. Dalam tutorial ini kami akan menunjukkan secara tepat cara **create conditional formatting**, menata sel, dan bahkan memberi peringkat pada nilai tertinggi—semua dengan pustaka Aspose.Cells yang kuat untuk .NET.

Kami akan membahas contoh dunia nyata: menghasilkan lembar skor, menyorot skor tinggi dengan warna hijau muda, dan memberi latar belakang emas pada tiga performer teratas. Pada akhir Anda akan mengetahui **how to set cell background**, **how to rank cells**, dan **how to use Aspose** untuk otomatisasi Excel yang canggih. Tanpa basa‑basi, hanya solusi lengkap yang dapat dijalankan yang dapat Anda sisipkan ke proyek C# mana pun.

## Apa yang Akan Anda Pelajari

- Cara **create excel workbook** menggunakan Aspose.Cells  
- Cara mengisi rentang dengan data acak (skor)  
- Cara **set cell background** dengan warna solid  
- Cara menerapkan aturan berbasis rumus untuk **rank cells** dan menyorot tiga teratas  
- Cara menyimpan hasil sebagai file .xlsx  

Prasyarat: .NET 6+ (atau .NET Framework 4.6+), Visual Studio (atau IDE C# apa pun), dan referensi ke paket NuGet Aspose.Cells. Jika Anda belum pernah menggunakan Aspose sebelumnya, jangan khawatir—kami akan membahas **how to use Aspose** dari awal.

![Contoh pemformatan bersyarat](https://example.com/images/create-conditional-formatting.png "Tangkapan layar yang menunjukkan pemformatan bersyarat dalam file Excel yang dihasilkan")

*Teks alt gambar: contoh pemformatan bersyarat dalam workbook Excel yang dihasilkan dengan Aspose.Cells.*

## Cara Membuat Workbook Excel dengan Aspose.Cells

Hal pertama yang perlu dilakukan: Anda memerlukan objek workbook untuk bekerja. Aspose.Cells membuat ini menjadi satu baris kode.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Mengapa kita mengganti nama sheet? Nama yang jelas (seperti **Scores**) memudahkan referensi di kemudian hari, terutama saat Anda membagikan file kepada pengguna non‑teknis.  

Setelah workbook ada, mari isi kolom A dengan skor acak.

## Cara Mengisi Data – Membuat Skor Acak

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Catatan singkat: `PutValue` secara otomatis mendeteksi tipe data, jadi Anda tidak perlu meng-cast ke `int`. Loop dimulai pada `i = 0` tetapi menulis ke baris `i + 1` karena baris Excel dimulai dari 1 sementara koleksi `Cells` dimulai dari 0.

## Cara Menetapkan Latar Belakang Sel untuk Skor Tinggi

Sekarang kami akan **create conditional formatting** yang mewarnai setiap skor ≥ 80 dengan nuansa hijau muda.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

Properti `ForegroundColor` mengontrol warna isi, sementara `Pattern = BackgroundType.Solid` memberi tahu Excel untuk menggunakan isian solid bukan gradien atau pola. Ini adalah inti dari **how to set cell background** berdasarkan ambang numerik.

## Cara Memberi Peringkat Sel dan Menyorot Top‑3

Memberi peringkat sedikit lebih rumit karena kita memerlukan rumus yang mengevaluasi setiap sel terhadap seluruh rentang. Aspose.Cells memungkinkan Anda menggunakan sintaks rumus Excel yang sama seperti yang Anda ketik di UI.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Mengapa `A2` dalam rumus? Aspose mengevaluasi rumus relatif terhadap setiap sel dalam rentang, sehingga `A2` otomatis bergeser menjadi `A3`, `A4`, dll., saat aturan diterapkan baris‑per‑baris. Fungsi `RANK` mengembalikan posisi nilai dalam rentang yang ditentukan, dan bagian `<=3` memastikan hanya tiga skor tertinggi yang mendapatkan isian emas.

## Cara Menyimpan Workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif yang dapat ditulis oleh aplikasi Anda. Setelah menjalankan metode, buka file di Excel dan Anda akan melihat:

- Sel hijau muda untuk setiap skor ≥ 80  
- Sel emas untuk tiga skor tertinggi, terlepas apakah mereka juga ≥ 80  

Itulah alur lengkap **create conditional formatting**.

---

## Contoh Lengkap yang Dapat Dijalankan

Berikut seluruh metode lagi, siap untuk disalin‑tempel ke aplikasi konsol atau kelas C# mana pun:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Hasil yang Diharapkan

Saat Anda membuka `Scores_ConditionalFormatting.xlsx`:

- Sel dengan nilai **80** atau lebih bersinar hijau muda.  
- Tiga angka tertinggi (meskipun di bawah 80) muncul dengan latar belakang **gold**.  
- Semua sel lainnya tetap dengan latar belakang putih default.

Petunjuk visual ini langsung memberi tahu manajer siapa performer teratas, tanpa penyortiran manual.

---

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika saya membutuhkan lebih dari tiga skor teratas?**  
Cukup ubah bagian `<=3` pada rumus menjadi `<=5` (atau angka berapa pun yang Anda inginkan). Aturan akan menyesuaikan secara otomatis.

**Apakah saya dapat menerapkan beberapa rentang pemformatan?**  
Tentu saja. Panggil `sheet.ConditionalFormattings.Add` lagi dengan rentang yang berbeda, lalu tambahkan kondisi ke objek `ConditionalFormatting` baru tersebut.

**Bagaimana dengan versi Excel yang lebih lama?**  
Aspose.Cells menyimpan dalam format modern `.xlsx` secara default, yang kompatibel dengan Excel 2007 ke atas. Jika Anda membutuhkan `.xls`, berikan `SaveFormat.Excel97To2003` ke metode `Save`.

**Apakah ada dampak kinerja untuk lembar besar?**  
Pemformatan bersyarat disimpan sebagai metadata, sehingga tidak secara signifikan memengaruhi ukuran file. Namun, menghasilkan ratusan ribu baris dapat meningkatkan penggunaan memori—pertimbangkan pemrosesan dalam batch.

## Langkah Selanjutnya

Sekarang Anda telah menguasai **how to create conditional formatting**, Anda mungkin ingin menjelajahi:

- **How to create Excel charts** secara programatik (fitur Aspose.Cells lainnya)  
- **how to set cell background** berdasarkan nilai teks (mis., “Pass/Fail”)  
- **how to use Aspose.Cells for data validation** dan daftar drop‑down  

## Kesimpulan

Kami baru saja melewati contoh lengkap, end‑to‑end tentang cara **create conditional formatting** dalam workbook Excel menggunakan Aspose.Cells. Dari menginisialisasi workbook, mengisi data, **setting cell background**, memberi peringkat pada performer teratas, hingga akhirnya menyimpan file, setiap langkah dibahas dengan mempertimbangkan **how to rank cells** dan **how to use Aspose**.

Jalankan kode tersebut, sesuaikan ambang batas, dan lihat seberapa cepat Anda dapat menghasilkan laporan yang rapi untuk skenario bisnis apa pun. Memiliki variasi yang ingin Anda bagikan? Tinggalkan komentar di bawah—selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Otomatisasi Pemformatan Bersyarat Excel Menggunakan Aspose.Cells untuk Java: Panduan Lengkap](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Cara Membuat & Memformat Sel Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑per‑Langkah](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Buat Workbook Excel menggunakan Aspose.Cells di Java: Panduan Langkah‑per‑Langkah](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}