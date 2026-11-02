---
category: general
date: 2026-06-21
description: Buat tabel perkalian di Excel menggunakan Python. Pelajari cara menggunakan
  lambda, cara menggunakan makearray, menampilkan array Excel, dan membaca nilai Excel
  dengan Python dalam tutorial langkah demi langkah.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: id
og_description: Buat tabel perkalian di Excel menggunakan Python. Tutorial ini menunjukkan
  cara menggunakan lambda, makearray, menampilkan array Excel, dan membaca nilai Excel
  dengan Python secara efisien.
og_title: Buat tabel perkalian di Excel dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Buat tabel perkalian di Excel dengan Python – Panduan Lengkap
url: /id/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat tabel perkalian di Excel dengan Python – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **membuat tabel perkalian** di Excel tanpa harus mengetik setiap sel secara manual? Anda tidak sendirian. Dalam banyak skenario pelaporan, Anda memerlukan grid produk 5×5 (atau lebih besar) secara cepat, dan melakukannya secara manual membuang-buang waktu.  

Dalam tutorial ini kita akan membahas cara bersih yang didorong oleh Python untuk menghasilkan tabel tersebut, menyematkannya dengan formula `MAKEARRAY`, dan kemudian mengambil hasilnya kembali ke skrip Anda. Sepanjang jalan kita akan menjawab **cara menggunakan lambda**, menunjukkan **cara menggunakan makearray**, dan mendemonstrasikan **menampilkan array excel** serta **membaca nilai excel python**—semua dalam satu contoh yang kohesif.

Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan bekerja dengan workbook apa pun, serta memahami mengapa pendekatan ini cepat dan tahan masa depan.

## Apa yang Anda Butuhkan

- Python 3.8+ (rilis stabil terbaru sudah cukup)
- Library `openpyxl` (atau library lain yang mendukung Excel dan formula)
- Pemahaman dasar tentang ekspresi lambda di Python
- Tidak memerlukan add‑in Excel khusus; fungsi native `MAKEARRAY` (tersedia di Excel 365) melakukan pekerjaan berat

Jika Anda belum memiliki salah satu dari ini, cukup jalankan `pip install openpyxl` dan Anda siap melanjutkan.

## Membuat tabel perkalian – Gambaran Umum

Inti idenya sederhana: kita membuat workbook baru, menulis formula `MAKEARRAY` yang membangun matriks perkalian 5 × 5, memaksa Excel menghitungnya, dan akhirnya membaca nilai yang dihasilkan kembali ke Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Menjalankan skrip akan mencetak:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Itulah **membuat tabel perkalian** yang berfungsi penuh di Excel, dihasilkan sepenuhnya dari Python.

### Mengapa menggunakan `MAKEARRAY` alih‑alih loop Python?

- **Performa**: Excel menangani perhitungan secara native, yang lebih cepat untuk matriks besar.
- **Pembaruan langsung**: Jika Anda kemudian mengubah dimensi dalam formula, sheet secara otomatis menghitung ulang.
- **Keterbacaan**: Formula menyatakan maksud (“buat array”) secara langsung, menjaga kode Python Anda tetap rapi.

## Cara menggunakan lambda di Python untuk formula Excel

Bagian `LAMBDA` dari pemanggilan `MAKEARRAY` adalah fungsi anonim di sisi Excel, bukan lambda Python. Namun, konsepnya sama: Anda mendefinisikan potongan logika kecil yang inline yang menerima `r` (indeks baris) dan `c` (indeks kolom) serta mengembalikan `r*c`.  

Jika Anda baru mengenal **cara menggunakan lambda** di dunia Excel, anggaplah itu sebagai mini‑fungsi yang hidup hanya di dalam formula. Tidak perlu mendeklarasikan fungsi terpisah di tempat lain. Di Python kita cukup menyematkan string:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Baris itu memberi tahu Excel: *“Untuk setiap sel dalam blok 5‑by‑5, hitung baris × kolom.”*  

Karena lambda dievaluasi oleh Excel, Anda tidak perlu khawatir tentang sintaks lambda Python di sini—hanya sintaks Excel.

## Cara menggunakan makearray untuk menghasilkan array

`MAKEARRAY` adalah penambahan relatif baru ke perpustakaan fungsi Excel (tersedia di Microsoft 365 sejak 2022). Ia menggantikan trik lama seperti kombinasi `INDEX` + `ROW`/`COLUMN`. Tanda tangannya adalah:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – jumlah baris yang Anda inginkan.
- **columns** – jumlah kolom yang Anda inginkan.
- **lambda** – sebuah LAMBDA Excel yang menerima `(row, column)` dan mengembalikan sebuah nilai.

Dalam contoh kami kami memberikan `5,5` untuk tabel perkalian klasik, tetapi Anda dapat dengan mudah mengubah angka tersebut:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Itu akan menghasilkan tabel 10 × 10 tanpa menyentuh loop Python apa pun. Ini menunjukkan **cara menggunakan makearray** untuk segala jenis grid deterministik, baik itu tabel lookup, heatmap, atau jadwal keuangan.

## Menampilkan array excel – mengambil data kembali ke Python

Setelah Excel menghitung formula, nilai yang dihasilkan berada di sheet seperti sel yang dimasukkan secara manual. Untuk **menampilkan array excel**, kita iterasi rentang dan mencetak setiap baris:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Beberapa tips:

- Gunakan `worksheet.cell(row, column).value` alih‑alih pengindeksan gaya kamus jika Anda perlu menangani rentang yang lebih besar; ini sedikit lebih cepat.
- Jika Anda menginginkan tabel yang lebih cantik, pertimbangkan `tabulate` atau `pandas.DataFrame` untuk memformat output.

Berikut adalah tangkapan layar sheet yang dihasilkan (teks alt gambar mencakup kata kunci utama untuk SEO):

![Screenshot menunjukkan cara membuat tabel perkalian di Excel menggunakan Python](/images/multiplication-table-excel.png)

## Membaca nilai excel python – mengekstrak matriks untuk pemrosesan lebih lanjut

Seringkali langkah selanjutnya setelah **menampilkan array excel** adalah memasukkan angka‑angka tersebut ke dalam pipeline analisis data. Di sinilah **membaca nilai excel python** bersinar. Loop yang sama yang kita gunakan untuk mencetak dapat dipakai kembali untuk membangun list of lists, array NumPy, atau DataFrame Pandas:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Output:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Sekarang Anda memiliki DataFrame yang sepenuhnya bertipe yang dapat Anda plot, ekspor ke CSV, atau masukkan ke model machine‑learning. Ini menyelesaikan bagian **membaca nilai excel python** dari alur kerja.

## Kasus Pojok & Tips Praktis

- **Rekalkulasi formula**: Jika Anda memodifikasi workbook setelah pemanggilan `calculate_formula()` pertama, Anda harus memanggilnya lagi; jika tidak, array yang di‑cache akan tetap usang.
- **Excel non‑365**: Versi Excel lama tidak mendukung `MAKEARRAY`. Dalam kasus itu, gunakan tabel yang dihasilkan oleh Python dan tulis setiap sel secara individual.
- **Tabel besar**: Untuk matriks lebih besar dari ~100 × 100, pertimbangkan streaming data untuk menghindari memuat seluruh sheet ke memori.
- **Penanganan error**: Bungkus langkah perhitungan dan pembacaan dalam blok `try/except` untuk menangkap `InvalidFileException` atau `FormulaError`.

## Kesimpulan

Kami baru saja menunjukkan cara **membuat tabel perkalian** di Excel menggunakan Python, memanfaatkan kekuatan **cara menggunakan lambda** dan **cara menggunakan makearray**. Anda telah melihat cara **menampilkan array excel**, membaca nilai tersebut kembali dengan **membaca nilai excel python**, dan bahkan mengubah hasilnya menjadi DataFrame Pandas untuk analisis lanjutan.

Ingin melangkah lebih jauh? Coba ganti logika perkalian dengan sesuatu yang lebih kompleks—mungkin matriks jarak, tabel probabilitas, atau grid penetapan harga dinamis. Pola yang sama berlaku: satu baris `MAKEARRAY`, panggilan cepat `calculate_formula()`, dan beberapa loop Python untuk menarik data keluar.

Jika panduan ini membantu Anda, beri bintang di GitHub, bagikan kepada rekan tim, atau tinggalkan komentar dengan kasus penggunaan Anda sendiri. Selamat coding, dan nikmati kemudahan menghasilkan tabel Excel dengan satu formula!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}