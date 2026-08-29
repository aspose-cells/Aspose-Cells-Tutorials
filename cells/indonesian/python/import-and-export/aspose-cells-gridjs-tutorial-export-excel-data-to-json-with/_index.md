---
category: general
date: 2026-07-03
description: Tutorial Aspose Cells GridJs yang menunjukkan cara mengekspor data Excel
  ke JSON dan mengekspor lembar kerja ke JSON secara efisien menggunakan lazy loading.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: id
og_description: Tutorial Aspose Cells GridJs menjelaskan cara mengekspor data Excel
  ke JSON dan mengekspor lembar kerja ke JSON dengan pemuatan malas untuk spreadsheet
  besar.
og_title: Tutorial Aspose Cells GridJs – Ekspor data Excel ke JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Tutorial Aspose Cells GridJs – Ekspor data Excel ke JSON dengan pemuatan malas
url: /id/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial Aspose Cells GridJs – Ekspor Data Excel JSON dengan lazy loading

Pernah bertanya-tanya bagaimana cara **mengekspor Excel data JSON** dari spreadsheet yang sangat besar tanpa membuat browser melambat? Dalam tutorial Aspose Cells GridJs ini kami akan membahas solusi lengkap yang siap dijalankan yang memungkinkan Anda **mengekspor worksheet ke JSON** menggunakan lazy loading, sehingga hanya baris yang Anda butuhkan yang diambil sesuai permintaan.

Jika Anda telah berjuang dengan file `.xlsx` yang sangat besar dan sisi klien terus membeku, Anda tidak sendirian. Kabar baiknya? Pendekatan yang kami bahas di sini ringan dan skalabel, serta dapat Anda sisipkan ke proyek Python apa pun yang sudah menggunakan library Aspose.Cells.

## Apa yang dibahas dalam panduan ini

Dalam beberapa menit ke depan Anda akan belajar cara:

1. Memuat workbook besar dengan Aspose.Cells.
2. Mengaktifkan lazy loading GridJs sehingga server mengalirkan baris dalam potongan.
3. Mengekspor konfigurasi GridJs ke file JSON yang dapat dikonsumsi front‑end.
4. Menyesuaikan ukuran chunk untuk kinerja optimal.
5. Memverifikasi output dan mengintegrasikannya dengan halaman HTML sederhana.

Tidak ada layanan eksternal, tidak ada sihir tersembunyi—hanya Python murni dan API Aspose.Cells. Pada akhir tutorial Anda akan memiliki pipeline **ekspor worksheet ke JSON** yang lengkap yang dapat Anda sesuaikan untuk dashboard, alat pelaporan, atau komponen data‑grid apa pun.

### Prasyarat

- Python 3.8+ terinstal secara lokal.
- Paket `asposecells` (Anda dapat `pip install aspose-cells`).
- File Excel berukuran besar (misalnya `large-data.xlsx`) yang ditempatkan di direktori yang diketahui.
- Familiaritas dasar dengan Python dan konsep pengembangan web.

Jika ada yang terdengar tidak familiar, jangan panik—setiap langkah menyertakan penjelasan singkat “mengapa” sehingga Anda akan memahami alasan di balik kode.

---

## Langkah 1: Instal dan impor Aspose.Cells

Pertama-tama, kita memerlukan library Aspose.Cells. Ini adalah produk komersial, tetapi trial gratis dapat digunakan untuk pengembangan.

```bash
pip install aspose-cells
```

Sekarang impor kelas yang diperlukan dalam skrip Anda.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Mengapa ini penting:** Mengimpor `Workbook` memberi Anda akses ke mesin berperforma tinggi yang membaca file Excel langsung ke memori, melewati pendekatan `openpyxl` yang lebih lambat.

## Langkah 2: Muat workbook yang berisi dataset besar

Dengan library siap, arahkan ke file Excel Anda. Path dapat berupa absolut atau relatif; pastikan file tersebut ada.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Tips pro:** Jika workbook Anda lebih besar dari beberapa ratus megabyte, pertimbangkan meningkatkan batas memori proses Python atau menggunakan interpreter 64‑bit untuk menghindari `MemoryError`.

## Langkah 3: Aktifkan lazy loading GridJs

GridJs adalah komponen grid JavaScript milik Aspose. Lazy loading memberi tahu server untuk mengirim hanya sebagian baris—sempurna untuk lembar besar.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Mengapa lazy loading?** Tanpa itu, seluruh worksheet akan diserialisasi menjadi JSON sekaligus, yang dapat dengan mudah melampaui batas memori browser. Dengan mengatur `LazyLoadingChunkSize` menjadi 500, setiap permintaan membawa payload yang dapat dikelola.

## Langkah 4: Ekspor konfigurasi GridJs ke JSON

Sekarang kami meminta Aspose menghasilkan JSON yang diharapkan oleh komponen GridJs front‑end. Ini adalah inti dari operasi **export excel data json**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

Metode `ExportGridJsJson` mengembalikan objek `bytes` yang berisi representasi JSON dari worksheet, siap untuk disimpan atau di-stream.

## Langkah 5: Tulis JSON ke file (atau stream)

Untuk pengujian cepat, tulis JSON ke disk. Pada API produksi Anda akan mengembalikannya langsung dari endpoint Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Apa yang akan Anda lihat:** Membuka `lazygrid.json` memperlihatkan struktur dengan `columns`, `rows`, dan metadata paginasi. Array `rows` pada awalnya akan kosong; GridJs akan meminta chunk pertama saat halaman dimuat.

## Langkah 6: Sambungkan JSON ke halaman HTML sederhana (opsional)

Jika Anda ingin melihat grid beraksi, buat file HTML kecil yang memuat GridJs dari CDN dan menunjuk ke JSON yang dihasilkan.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Mengapa menyertakan ini?** Ini mendemonstrasikan siklus lengkap: Python membuat JSON, browser mengambilnya, dan GridJs merender data chunk‑by‑chunk. Anda kini dapat bereksperimen dengan nilai `LazyLoadingChunkSize` yang berbeda untuk menemukan titik optimal bagi jaringan Anda.

## Langkah 7: Verifikasi dan pemecahan masalah

Jalankan skrip Python:

```bash
python export_lazy_grid.py
```

Anda harus melihat pesan sukses dan file `lazygrid.json`. Buka file HTML di browser; grid harus menampilkan 500 baris pertama secara instan, dengan kontrol paginasi untuk memuat lebih banyak.

Jika grid muncul kosong:

- **Periksa ukuran file JSON** – file berukuran nol byte biasanya berarti path workbook salah.
- **Pastikan lazy loading diaktifkan** – flag `LazyLoading` harus `True`.
- **Periksa konsol browser** – kesalahan CORS atau 404 menunjukkan JSON tidak disajikan dengan benar.

---

## Variasi umum dan kasus tepi

### Mengekspor worksheet tertentu

Contoh di atas selalu menggunakan worksheet pertama (`Worksheets[0]`). Untuk mengekspor sheet lain, cukup ubah indeks atau gunakan nama sheet:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Mengubah ukuran chunk untuk file besar

Untuk file dengan jutaan baris, ukuran chunk 500 mungkin masih terlalu kecil, menyebabkan banyak round‑trip. Anda dapat meningkatkannya menjadi 2000 atau lebih, tetapi ingat bahwa chunk yang lebih besar mengonsumsi lebih banyak bandwidth per permintaan.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Mengekspor ke stream alih-alih file

Jika API Anda mengembalikan JSON secara langsung, Anda tidak perlu menulis ke disk:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Menangani formula dan format

Secara default, `ExportGridJsJson` menyertakan nilai hasil perhitungan formula. Jika Anda memerlukan formula mentah, atur:

```python
grid_options.ExportFormulas = True
```

---

## Kesimpulan

Dalam **tutorial Aspose Cells GridJs** ini kami membahas semua yang Anda perlukan untuk **mengekspor Excel data JSON** dan **mengekspor worksheet ke JSON** dengan lazy loading. Dari menginstal Aspose.Cells, mengaktifkan lazy loading, menghasilkan JSON, hingga menghubungkannya dengan halaman HTML sederhana, Anda kini memiliki pola full‑stack yang skalabel dengan mulus untuk spreadsheet besar.

Cobalah—sesuaikan ukuran chunk, arahkan ke worksheet yang berbeda, atau integrasikan endpoint ke aplikasi Flask atau Django. Kemungkinannya tak terbatas, dan peningkatan performa terasa langsung.

Siap melangkah ke tahap berikutnya? Coba tambahkan penyortiran kolom, renderer sel khusus, atau bahkan filter sisi server untuk membuat grid GridJs Anda benar‑benar interaktif. Jika mengalami kendala, tinggalkan komentar di bawah; selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Impor Data JSON ke Excel Menggunakan Aspose.Cells Java: Panduan Komprehensif](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Muat CSV & Ekspor ke JSON Menggunakan Aspose.Cells untuk .NET: Panduan Komprehensif](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Ekspor Data Excel Menggunakan Aspose.Cells .NET: Panduan Lengkap untuk Ekspor Data Tanpa Hambatan](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}