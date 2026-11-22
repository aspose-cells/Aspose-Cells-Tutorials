---
category: general
date: 2026-11-22
description: Pelajari cara menyajikan Excel dalam aplikasi web menggunakan Flask.
  Panduan ini menunjukkan cara memuat workbook Excel dan menampilkan Excel di web
  dengan GridJs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: id
lastmod: 2026-11-22
og_description: Cara menyajikan file Excel menggunakan Flask dan GridJs. Ikuti tutorial
  lengkap ini untuk memuat workbook Excel dan menampilkannya di web.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: Cara menyajikan Excel dengan Flask – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: Cara menyajikan file Excel dengan Flask dan GridJs
url: /id/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyajikan File Excel dengan Flask dan GridJs

Jika Anda perlu **cara menyajikan excel** dalam aplikasi web Python, tutorial ini menunjukkan solusi lengkap. Anda akan belajar cara **memuat workbook excel** dengan pustaka `cells`, mengeksposnya melalui endpoint Flask, dan memungkinkan pengguna **menampilkan excel di web** menggunakan GridJs.

Kami akan menelusuri setiap baris kode, menjelaskan mengapa setiap bagian penting, dan memberikan contoh yang siap dijalankan. Pada akhir panduan, Anda dapat menyematkan file `.xlsx` apa pun ke dalam grid responsif di sisi klien tanpa menulis parser data JavaScript khusus.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- Python 3.9+ terpasang  
- Paket `flask` dan `cells` (`pip install flask cells`)  
- File Excel contoh (misalnya, `sample.xlsx`) di direktori yang diketahui  

Tidak diperlukan kerangka kerja front‑end tambahan; GridJs menangani UI secara otomatis.

## Gambaran Solusi

Ide dasarnya sederhana:

1. **Muat** workbook Excel di server.  
2. **Buat** sebuah `GridJsHandler` yang menerjemahkan data lembar kerja ke format JSON yang diharapkan GridJs.  
3. **Ekspos** route Flask yang mengembalikan tampilan JSON dan menerima perubahan dari klien.  
4. **Jalankan** server Flask sehingga browser dapat mengambil data dan merender grid.

Sekarang mari implementasikan setiap langkah.

## Cara Menyajikan Excel dengan Flask dan GridJs

### Langkah 1: Muat workbook Excel

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Mengapa ini penting:**  
`cells.Workbook` mem-parsing file `.xlsx` menjadi representasi dalam memori. Memuat workbook sekali saat startup membuat server cepat karena permintaan berikutnya menggunakan objek yang sama alih‑alih mengakses sistem file berulang kali.

### Langkah 2: Buat handler sisi‑server GridJs

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Mengapa ini penting:**  
`GridJsHandler` mengabstraksi konversi dari baris/kolom Excel ke skema JSON yang dikonsumsi GridJs. Ia juga melacak perubahan di sisi klien, memungkinkan Anda menyimpan perubahan kembali ke workbook nanti jika diperlukan.

### Langkah 3: Aktifkan fitur opsional (lazy loading)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Mengapa ini penting:**  
Ketika lembar kerja berisi ribuan baris, mengirim seluruh dataset sekaligus dapat membebani browser. Lazy loading mengalirkan data halaman demi halaman, meningkatkan kinerja untuk skenario **menampilkan excel di web**.

### Langkah 4: Siapkan aplikasi Flask minimal

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Mengapa ini penting:**  
Flask menyediakan server HTTP ringan yang dapat menyajikan endpoint JSON dan file statis. Menjaga aplikasi Flask minimal mengurangi permukaan serangan dan membuat contoh mudah diadaptasi.

### Langkah 5: Definisikan endpoint GridJs

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**Mengapa ini penting:**  

- **GET** – Browser mengambil tampilan lembar kerja awal.  
- **POST** – Saat pengguna mengedit sel, GridJs mengirim payload JSON; `apply_changes` menggabungkan perubahan tersebut kembali ke status internal handler.  

Mengembalikan `grid_handler.get_view()` memastikan klien selalu menerima data terbaru, yang esensial untuk pengalaman **menampilkan excel di web** yang mulus.

### Langkah 6: Jalankan server Flask

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Mengapa ini penting:**  
Menjalankan pada port 5000 adalah default Flask, sehingga mudah diuji secara lokal (`http://localhost:5000/gridjs`). Di produksi Anda akan menempatkan Flask di belakang server WSGI (misalnya, Gunicorn) dan mungkin mengaktifkan HTTPS.

## Output JSON yang Diharapkan

Saat Anda mengunjungi `http://localhost:5000/gridjs` dengan permintaan GET, responsnya akan terlihat seperti:

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

GridJs secara otomatis mengonsumsi payload ini, merender tabel yang dapat dicari dan diurutkan di browser.

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah skrip lengkap yang dapat Anda salin ke `app.py` dan jalankan:

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

Jalankan skrip dengan:

```bash
python app.py
```

Buka browser dan arahkan ke halaman HTML sederhana yang memuat GridJs (lihat dokumentasi GridJs untuk tag `<script>`). Grid akan menampilkan konten Excel secara langsung.

## Variasi Umum dan Kasus Edge

| Situasi | Cara menyesuaikan |
|-----------|--------------|
| **Beberapa lembar kerja** | Buat `GridJsHandler` terpisah untuk setiap sheet dan ekspos endpoint berbeda (`/gridjs/sheet1`, `/gridjs/sheet2`). |
| **File besar (>10 MB)** | Tingkatkan batas ukuran permintaan Flask (`app.config['MAX_CONTENT_LENGTH']`) dan tetap aktifkan `lazy_load`. |
| **Menyimpan perubahan kembali ke file** | Setelah `apply_changes`, panggil `workbook.save("output.xlsx")` untuk menulis perubahan ke disk. |
| **Autentikasi** | Bungkus endpoint dengan Flask‑Login atau pemeriksaan token API sebelum mengembalikan data. |
| **CORS untuk front‑end eksternal** | Tambahkan `from flask_cors import CORS; CORS(app)` untuk mengizinkan permintaan lintas asal. |

Penyesuaian ini memungkinkan Anda menskalakan proses **memuat workbook excel** ke beban kerja produksi.

## Tips Pro

- **Cache tampilan JSON** jika workbook jarang berubah; gunakan `functools.lru_cache` di sekitar `grid_handler.get_view()` untuk mengurangi beban serialisasi.  
- **Validasi edit yang masuk** (`request.json`) untuk mencegah data yang tidak valid merusak workbook.  
- Saat menyajikan lewat HTTPS, setel `app.run(ssl_context=('cert.pem', 'key.pem'))` untuk mengenkripsi lalu lintas.

## Kesimpulan

Anda kini tahu **cara menyajikan excel** menggunakan Flask dan GridJs, mulai dari memuat workbook hingga mengembalikan tampilan JSON yang dapat dirender browser. Contoh ini mencakup seluruh siklus hidup: **memuat workbook excel**, mengaktifkan lazy loading, mengekspos endpoint REST, dan menjalankan server siap produksi.

Selanjutnya, jelajahi topik terkait seperti **menampilkan excel di web** dalam front‑end React, atau perpanjang handler untuk **memuat workbook excel** dari penyimpanan cloud (misalnya AWS S3). Bereksperimenlah dengan styling kolom GridJs, menambahkan paginasi, atau menyimpan edit pengguna kembali ke spreadsheet asli.

Selamat coding, dan nikmati mengubah file Excel statis menjadi tabel web interaktif!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}