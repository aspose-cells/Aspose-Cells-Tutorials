---
category: general
date: 2026-06-21
description: Buat array dinamis menggunakan Python dan fungsi SEQUENCE di Excel. Pelajari
  cara membaca hasil formula, menghitung ulang formula Excel, dan lihat contoh SEQUENCE
  di Excel.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: id
og_description: Buat array dinamis di Excel menggunakan Python. Tutorial ini menunjukkan
  cara menggunakan fungsi SEQUENCE, menghitung ulang rumus Excel, dan membaca hasil
  rumus.
og_title: Buat Array Dinamis di Excel dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Buat Array Dinamis di Excel dengan Python – Panduan Langkah demi Langkah
url: /id/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Array Dinamis di Excel dengan Python – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **membuat array dinamis** di Excel tanpa meninggalkan skrip Python Anda? Anda tidak sendirian. Baik Anda mengotomatisasi laporan bulanan atau membangun mesin data ringan, kemampuan untuk menaruh formula `SEQUENCE` ke dalam workbook, menghitung ulang, dan mengambil rentang spill kembali ke Python adalah pengubah permainan.

Dalam tutorial ini kami akan membahas contoh **excel sequence** dunia nyata, menunjukkan cara **membaca hasil formula**, dan menjelaskan cara terbaik untuk **menghitung ulang formula excel** setelah Anda menyuntikkan logika baru. Pada akhir tutorial Anda akan memiliki skrip mandiri yang dapat Anda salin‑tempel, jalankan, dan sesuaikan dengan kebutuhan Anda.

## Apa yang Akan Anda Pelajari

- Cara kerja fungsi `SEQUENCE` dan mengapa fungsi ini sempurna untuk menghasilkan matriks.
- Perbedaan antara nilai sel biasa dan alamat rentang spill.
- Menggunakan `wb.calculate_formula()` (atau yang setara) untuk memaksa Excel mengevaluasi formula baru.
- Mengambil alamat array dinamis dengan `ANCHORARRAY`.
- Contoh Python lengkap yang dapat dijalankan dan dapat Anda masukkan ke proyek mana pun.

Tidak diperlukan pengalaman sebelumnya dengan mesin array‑dinamis baru Excel—hanya pemahaman dasar tentang Python dan perpustakaan seperti **xlwings** yang dapat berkomunikasi dengan Excel.

---

## Cara Membuat Array Dinamis dengan SEQUENCE di Excel Menggunakan Python

Langkah pertama adalah menulis formula **array dinamis** langsung ke sel worksheet. Di Excel modern, fungsi `SEQUENCE` dapat menghasilkan matriks angka secara langsung. Berikut sintaks yang akan kami gunakan:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Mengapa `SEQUENCE`?**  
Anggaplah ini sebagai `range()` bawaan Excel untuk spreadsheet. Ia memungkinkan Anda menentukan baris, kolom, nilai awal, dan kenaikan—semua dalam satu baris yang rapi. Dalam contoh kami kami meminta 3 baris dan 2 kolom, mulai dari 10 dan melangkah 5, yang menghasilkan:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Karena formula berada di `A1`, Excel secara otomatis “spill” hasilnya ke sel‑sel tetangga `A1:B3`. Spill itulah yang nanti akan kami ambil.

---

## Menggunakan Fungsi SEQUENCE di Excel – Contoh Excel Sequence Cepat

Jika Anda membuka Excel secara manual dan mengetik `=SEQUENCE(3,2,10,5)` di sebuah sel, Anda akan langsung melihat matriks yang sama muncul. Fungsi ini merupakan bagian dari mesin **array dinamis** Excel yang diperkenalkan di Office 365, yang berarti:

- Tidak perlu menekan Ctrl+Shift+Enter.
- Hasil dapat memperluas atau menyusut secara otomatis.
- Anda dapat merujuk seluruh rentang spill dengan fungsi seperti `@` atau `#`.

Di Python, satu‑satunya perbedaan adalah kami menetapkan formula sebagai string ke properti `.formula` sel. Perpustakaan yang menangani sisanya.

---

## Mengambil Alamat Rentang Spill dengan ANCHORARRAY

Setelah array dinamis berada di tempat, Anda sering perlu mengetahui di mana Excel menempatkan nilai‑nilai tersebut. Di sinilah `ANCHORARRAY` berperan. Ia mengembalikan alamat sel kiri‑atas dari rentang spill—tepat apa yang kami butuhkan untuk dibaca kembali ke skrip.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Menempatkan formula ini di `C1` memberi kami string teks seperti `"A1:B3"`. Perhatikan bahwa kami **membaca hasil formula** sebagai nilai biasa, bukan sebagai formula lain. Trik kecil ini menghindari kebutuhan untuk mem‑parse worksheet secara manual.

---

## Menghitung Ulang Formula Excel dan Membaca Hasilnya

Excel tidak selalu menghitung ulang secara instan ketika formula baru disuntikkan dari skrip eksternal. Untuk menjamin workbook mencerminkan perubahan terbaru, kami secara eksplisit memicu satu kali perhitungan.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Mengapa memanggil `calculate_formula()`?**  
Jika Anda melewatkan langkah ini, `ws.cells["C1"].value` mungkin masih mengembalikan `None` atau alamat lama karena Excel masih sibuk memperbarui pohon dependensinya. Dengan memaksa perhitungan ulang kami memastikan **membaca hasil formula** selalu up‑to‑date.

---

## Skrip Lengkap – Dari Awal hingga Selesai

Berikut contoh lengkap yang siap dijalankan dan mengikat semua komponen. Skrip ini mengasumsikan Anda telah menginstal **xlwings** (`pip install xlwings`) dan Excel tersedia di mesin Anda.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Output yang Diharapkan

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Menjalankan skrip akan membuka Excel, menyuntikkan formula `SEQUENCE`, menghitung ulang, dan kemudian mencetak baik alamat spill maupun matriks itu sendiri. Tidak ada klik manual yang diperlukan.

---

## Kesalahan Umum dan Pro Tips

- **Kesalahan:** Lupa memanggil `wb.calculate_formula()`.  
  *Hasil:* `C1` tetap kosong atau menampilkan alamat lama.  
  *Solusi:* Selalu jalankan perhitungan setelah menulis formula baru.

- **Kesalahan:** Menggunakan versi Excel yang lebih lama dan tidak memiliki fungsi `SEQUENCE`.  
  *Hasil:* error `#NAME?`.  
  *Solusi:* Pastikan Anda menggunakan Office 365 atau Excel 2021+.

- **Pro tip:** Jika Anda membutuhkan rentang spill untuk pemrosesan lebih lanjut (misalnya, pembuatan grafik), Anda dapat langsung memberi alamat tersebut ke `ws.range(spill_address)` seperti yang ditunjukkan di atas.

- **Pro tip:** `ANCHORARRAY` bekerja dengan semua array dinamis, bukan hanya `SEQUENCE`. Ganti dengan `=SORT(A2:A10)` atau `=FILTER(...)` dan Anda tetap akan mendapatkan alamat spill yang benar.

- **Kasus tepi:** Ketika area target sudah terisi, Excel akan mengembalikan error `#SPILL!`. Dalam situasi ini, bersihkan dulu rentang tujuan atau pindahkan formula ke sel lain.

---

## Memperluas Contoh – Apa Selanjutnya?

Setelah Anda tahu cara **membuat array dinamis**, **membaca hasil formula**, dan **menghitung ulang formula excel**, Anda dapat menjelajahi skenario yang lebih maju:

- **Data dinamis untuk grafik** – beri rentang spill ke sumber data grafik dan biarkan grafik tumbuh otomatis.
- **Pemformatan bersyarat** – terapkan aturan ke rentang spill menggunakan alamatnya.
- **Referensi lintas workbook** – tulis array dinamis di satu workbook dan tarik data ke workbook lain melalui tautan `xlwings`.

Masing‑masing poin ini dibangun di atas konsep inti yang dibahas di sini, jadi silakan bereksperimen. Satu‑satunya batas adalah imajinasi Anda (dan mungkin batas maksimum baris/kolom Excel).

---

## Kesimpulan

Kami baru saja menelusuri alur kerja lengkap untuk **membuat array dinamis** di Excel dari Python, menggunakan **fungsi SEQUENCE excel**, mengambil rentang spill dengan **ANCHORARRAY**, **menghitung ulang formula excel**, dan akhirnya **membaca hasil formula** kembali ke skrip Anda. Contoh singkat ini menunjukkan betapa kuatnya mesin array‑dinamis baru Excel ketika dipadukan dengan alat otomasi seperti **xlwings**.

Cobalah dalam proyek Anda sendiri, ubah dimensi matriks, atau ganti `SEQUENCE` dengan fungsi dinamis lain. Seiring Anda semakin nyaman, Anda akan menemukan bahwa mengotomatisasi Excel tidak hanya memungkinkan tetapi juga sangat mudah.

Punya pertanyaan atau ingin berbagi bagaimana Anda memperluas pola ini? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}