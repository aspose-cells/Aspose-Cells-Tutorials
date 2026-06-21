---
category: general
date: 2026-06-21
description: Pelajari cara menulis lambda di Excel menggunakan Python. Tutorial ini
  juga mencakup cara membuat workbook Excel dengan Python dan cara membaca sel dengan
  Aspose.Cells.
draft: false
keywords:
- how to write lambda
- create excel workbook python
- how to read cells
- how to use byrow
- use lambda function excel
language: id
og_description: Cara menulis lambda di Excel menggunakan Python dijelaskan. Ikuti
  langkah‑langkah jelas kami untuk membuat workbook Excel dengan Python, menerapkan
  BYROW, dan membaca hasil sel.
og_title: Cara Menulis Lambda di Excel dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to write lambda in Excel using Python. This tutorial also
    covers create excel workbook python and how to read cells with Aspose.Cells.
  headline: How to Write Lambda in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: BYROW works on any rectangular range. If you have gaps, just reference
      a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).
    question: What if my data isn’t contiguous?
  - answer: Yes. The first argument is always the row (or column for `BYCOL`). Additional
      arguments can be supplied after the range, like `BYROW(A1:C5, LAMBDA(r, factor,
      AVERAGE(r)*factor), 2)`.
    question: Can I pass more than one argument to the lambda?
  - answer: BYROW and LAMBDA are available starting with Excel 365 (dynamic arrays).
      If you need legacy support, you’d have to emulate the logic with VBA or multiple
      helper columns.
    question: Is this compatible with older Excel versions?
  - answer: Not for this demo, but you can call `workbook.save("output.xlsx")` if
      you want a physical file.
    question: Do I need to save the workbook to disk?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
- Lambda
- BYROW
title: Cara Menulis Lambda di Excel dengan Python – Panduan Langkah demi Langkah
url: /id/python/import-and-export/how-to-write-lambda-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menulis Lambda di Excel dengan Python – Panduan Langkah‑ demi‑Langkah

Pernah bertanya‑tanya **how to write lambda** dalam rumus Excel saat Anda mengotomatiskan spreadsheet dari Python? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mencoba menggabungkan kekuatan fungsi array dinamis baru Excel dengan alur kerja berbasis Python. Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan hal itu — plus kami akan menyentuh **create excel workbook python**, **how to read cells**, dan pola praktis **how to use byrow**.

Pada akhir panduan ini Anda akan memiliki workbook baru, formula BYROW yang memanfaatkan lambda, dan cara sederhana untuk menarik hasil kembali ke skrip Python Anda. Tidak diperlukan add‑in Excel tambahan, hanya Aspose.Cells untuk Python dan sedikit kode.

## Prasyarat

- Python 3.8 atau yang lebih baru terpasang.
- Paket `aspose-cells` (`pip install aspose-cells`).
- Pemahaman dasar tentang list dan fungsi Python.
- (Opsional) IDE atau editor teks yang Anda nyaman gunakan.

Itu saja. Jika ada yang terdengar tidak familiar, berhenti sejenak dan instal paketnya terlebih dahulu; langkah‑langkah selanjutnya akan berfungsi di platform apa pun yang menjalankan Python.

## Membuat Workbook Excel dengan Python

Hal pertama yang kita butuhkan adalah objek workbook yang bersih. Aspose.Cells menyediakan kelas `Workbook` yang mewakili seluruh file Excel dalam memori.

```python
import aspose.cells as cells

# Step 1: Instantiate a new workbook and grab the first worksheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

Mengapa memulai dengan workbook baru? Karena hal itu menjamin lingkungan yang deterministik—tidak ada rumus tersembunyi, tidak ada pemformatan yang tidak diinginkan, hanya kanvas kosong. Ini adalah dasar untuk setiap tutorial **create excel workbook python**.

## Mengisi Worksheet dengan Data

Selanjutnya kami mengisi tabel numerik 5 × 3 yang dimulai dari sel **A1**. Data tersebut sengaja dibuat sederhana agar Anda dapat melihat perhitungannya dengan jelas.

```python
# Step 2: Define a 5x3 table and write it to A1
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]

worksheet.cells["A1"].put_value(table_data)
```

Perhatikan bagaimana kami menggunakan `put_value` dengan list Python bersarang; Aspose.Cells secara otomatis memetakan baris dan kolom untuk kami. Jika Anda perlu mengimpor data dari CSV atau basis data, Anda cukup mengganti `table_data` dengan sumber tersebut—tidak ada yang berubah.

## Cara Menulis Lambda dalam Formula BYROW (Python)

Sekarang bagian yang menarik: **how to write lambda** yang akan dievaluasi oleh mesin Excel. Fungsi `BYROW` Excel mengiterasi setiap baris dalam suatu rentang, memasukkan baris tersebut ke dalam `LAMBDA` yang Anda berikan. Dalam kasus kami, kami menginginkan rata‑rata setiap baris.

```python
# Step 3: Insert a BYROW formula that uses a lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"
```

Mari kita uraikan:

- `BYROW(A1:C5, …)` memberi tahu Excel untuk melihat setiap baris dalam rentang A1:C5.
- `LAMBDA(r, AVERAGE(r))` mendefinisikan fungsi anonim (`r` adalah array baris) yang mengembalikan rata‑rata baris tersebut.
- Hasilnya secara otomatis mengalir ke D1:D5 karena BYROW mengembalikan sebuah array.

Baris tunggal itu adalah jawaban untuk **how to write lambda** dalam perhitungan per‑baris. Anda dapat mengganti `AVERAGE` dengan `SUM`, `MAX`, atau agregat lain—cukup ubah isi lambda.

## Memaksa Perhitungan Rumus

Aspose.Cells tidak mengevaluasi rumus secara otomatis saat Anda menetapkannya, jadi kita harus memintanya untuk menghitung ulang.

```python
# Step 4: Force the workbook to evaluate all formulas
workbook.calculate_formula()
```

Jika Anda melewatkan langkah ini, sel di kolom D masih akan berisi teks rumus, bukan angka yang dihitung. Ini adalah jebakan umum ketika orang **how to use byrow** tanpa memicu proses perhitungan.

## Cara Membaca Sel Setelah Perhitungan

Akhirnya, mari tarik hasilnya kembali ke Python. Ini menggambarkan **how to read cells** dengan cara yang bekerja untuk output rumus apa pun.

```python
# Step 5: Retrieve the average values from D1:D5
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print(row_averages)  # Expected output: [20.0, 15.0, 12.0, 0.0, 200.0]
```

Sebuah list‑comprehension cepat mengulangi lima baris, mengambil nilai `.value` tiap sel, dan menyimpannya dalam `row_averages`. Daftar yang dicetak mengonfirmasi bahwa lambda kami bekerja persis seperti yang diharapkan.

### Tips Pro
Jika Anda perlu membaca blok hasil yang besar, gunakan `worksheet.cells.get_range("D1:D5").value` untuk mengambil seluruh array dalam satu panggilan—jauh lebih cepat untuk lembar besar.

## Menggunakan Fungsi Lambda Excel untuk Rata‑Rata Baris (Script Lengkap)

Menggabungkan semuanya, berikut script lengkap yang siap dijalankan:

```python
import aspose.cells as cells

# Create a new workbook
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]

# Populate the table
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]
worksheet.cells["A1"].put_value(table_data)

# Write BYROW with lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"

# Recalculate so the formula resolves
workbook.calculate_formula()

# Read the results back into Python
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print("Row averages:", row_averages)
```

Menjalankan script ini akan mencetak:

```
Row averages: [20.0, 15.0, 12.0, 0.0, 200.0]
```

Itulah seluruh siklus: **create excel workbook python**, mengisi data, **how to use byrow**, **how to write lambda**, dan akhirnya **how to read cells**.

## Kasus Pojok & Pertanyaan Umum

- **Bagaimana jika data saya tidak berurutan?**  
  BYROW bekerja pada rentang persegi apa pun. Jika ada celah, cukup referensikan rentang yang lebih besar dan biarkan lambda mengabaikan sel kosong (`AVERAGEIF(r, "<>")`).

- **Apakah saya dapat memberikan lebih dari satu argumen ke lambda?**  
  Ya. Argumen pertama selalu baris (atau kolom untuk `BYCOL`). Argumen tambahan dapat diberikan setelah rentang, seperti `BYROW(A1:C5, LAMBDA(r, factor, AVERAGE(r)*factor), 2)`.

- **Apakah ini kompatibel dengan versi Excel yang lebih lama?**  
  BYROW dan LAMBDA tersedia mulai Excel 365 (array dinamis). Jika Anda membutuhkan dukungan versi lama, Anda harus meniru logika tersebut dengan VBA atau beberapa kolom bantu.

- **Apakah saya perlu menyimpan workbook ke disk?**  
  Tidak untuk demo ini, tetapi Anda dapat memanggil `workbook.save("output.xlsx")` jika menginginkan file fisik.

## Kesimpulan

Kami telah membahas **how to write lambda** dalam formula Excel BYROW dari Python, mendemonstrasikan alur kerja lengkap **create excel workbook python**, dan menunjukkan cara paling sederhana untuk **how to read cells** setelah perhitungan. Dengan memanfaatkan Aspose.Cells Anda menghindari masalah COM interop, dan pola yang sama dapat diskalakan ke ribuan baris dengan perubahan kode minimal.

Siap untuk tantangan berikutnya? Cobalah mengganti `AVERAGE` dengan `MEDIAN`, tambahkan logika bersyarat di dalam lambda, atau hasilkan seluruh deck laporan secara otomatis. Kombinasi Python dan fungsi modern Excel membuka dunia kemungkinan untuk otomatisasi berbasis data.

Ada pertanyaan atau ingin berbagi trik lambda Anda? Tinggalkan komentar di bawah, dan selamat coding!  

![cara menulis lambda di Excel menggunakan Python](image.png){alt="cara menulis lambda di Excel menggunakan Python"}

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cara Memuat Workbook Excel Tanpa Nama yang Didefinisikan Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)
- [Cara Membuat Named Ranges yang Berskala Workbook di Excel Menggunakan Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}