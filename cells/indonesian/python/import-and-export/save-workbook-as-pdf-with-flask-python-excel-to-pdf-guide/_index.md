---
category: general
date: 2026-06-21
description: Simpan workbook sebagai PDF menggunakan Flask dan Aspose.Cells di Python
  – pelajari cara mengonversi XLSX ke PDF, menyesuaikan lebar kolom Excel secara otomatis,
  dan mengembalikan file dengan flask send_file pdf.
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: id
og_description: Simpan workbook sebagai PDF di Python menggunakan Flask. Tutorial
  langkah demi langkah ini menunjukkan cara mengonversi XLSX ke PDF, menyesuaikan
  lebar kolom Excel secara otomatis, dan menyajikan hasilnya dengan flask send_file
  pdf.
og_title: Simpan Workbook sebagai PDF dengan Flask – Panduan Python Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  headline: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  type: TechArticle
- description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  name: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  steps:
  - name: Why Each Piece Matters
    text: '- **`request.files.get("file")`** – Safely fetches the uploaded file; using
      `.get` avoids a `KeyError` if the field is missing. - **`io.BytesIO`** – Keeps
      everything in RAM, so we never write temporary files to disk. This is crucial
      for scalability. - **`auto_fit_columns()`** – Without this, column '
  - name: Manual Test with cURL
    text: '```bash curl -X POST http://localhost:5000/convert  -F "file=@sample.xlsx"  -o
      result.pdf ```'
  - name: Automated Test with Python’s `requests`
    text: '```python import requests'
  type: HowTo
tags:
- flask
- python
- excel
- pdf
- aspose-cells
title: Simpan Workbook sebagai PDF dengan Flask – Panduan Python Excel ke PDF
url: /id/python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan Workbook sebagai PDF dengan Flask – Panduan Python Excel ke PDF

Perlu **save workbook as PDF** dari layanan web? Anda bukan satu-satunya yang bertanya-tanya bagaimana mengubah file Excel yang diunggah menjadi PDF yang rapi secara langsung. Dalam panduan ini kami akan menjelaskan cara menyimpan workbook sebagai PDF menggunakan Flask dan Aspose.Cells, sekaligus membahas cara **convert XLSX to PDF**, auto‑fit kolom Excel, dan akhirnya mengirimkan hasilnya dengan `flask send_file pdf`.

Kami akan memulai dengan proyek Flask baru, menambahkan beberapa tips praktik terbaik, dan menghasilkan endpoint yang sepenuhnya berfungsi yang dapat dipanggil oleh klien mana pun. Pada saat Anda selesai, Anda akan dapat mengubah spreadsheet apa pun menjadi PDF hanya dengan beberapa baris kode Python.

## Apa yang Anda Butuhkan

- **Python 3.8+** (kode ini bekerja pada 3.9, 3.10, dan yang lebih baru)
- **Flask** (`pip install flask`) – kerangka kerja web ringan yang menjalankan API kami
- **Aspose.Cells for Python via .NET** (`pip install aspose-cells`) – pustaka yang benar‑benar membaca XLSX dan menulis PDF
- Pemahaman dasar tentang permintaan HTTP `POST` (tidak rumit)

Jika Anda sudah memiliki semua ini, bagus—mari kita mulai. Jika belum, langkah “Install Dependencies” akan menyiapkan semuanya.

## Langkah 1 – Siapkan Proyek Flask

Pertama, buat folder baru untuk proyek dan buat lingkungan virtual. Ini menjaga dependensi tetap rapi.

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

Sekarang buat file bernama `app.py`. File ini akan menampung seluruh logika **save workbook as pdf**.

## Langkah 2 – Inisialisasi Aplikasi Flask

Kami mulai dengan mengimpor komponen yang diperlukan dan membuat objek Flask app. Perhatikan betapa singkatnya blok impor—tidak ada modul yang tidak terpakai, yang menjaga waktu startup tetap rendah.

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **Pro tip:** Simpan `app = Flask(__name__)` di bagian atas file; ini memudahkan pengujian selanjutnya dengan alat seperti `pytest-flask`.

## Langkah 3 – Bangun Endpoint Konversi (convert xlsx to pdf)

Berikut inti tutorial: sebuah endpoint yang menerima spreadsheet melalui `POST`, memuatnya ke dalam workbook Aspose.Cells, dan menyiapkannya untuk ekspor PDF.

```python
@app.route("/convert", methods=["POST"])
def convert():
    # 1️⃣ Grab the uploaded file from the request
    uploaded = request.files.get("file")
    if not uploaded:
        return {"error": "No file provided"}, 400

    # 2️⃣ Read the file into memory (binary)
    file_bytes = uploaded.read()

    # 3️⃣ Load the spreadsheet into a workbook object
    workbook = cells.Workbook(io.BytesIO(file_bytes))

    # 4️⃣ Auto‑fit all columns in the first sheet (auto fit excel columns)
    workbook.worksheets[0].auto_fit_columns()

    # 5️⃣ Save the workbook as PDF into an in‑memory stream
    pdf_stream = io.BytesIO()
    workbook.save(pdf_stream, cells.SaveFormat.PDF)
    pdf_stream.seek(0)

    # 6️⃣ Return the PDF using flask send_file pdf
    return send_file(
        pdf_stream,
        mimetype="application/pdf",
        as_attachment=True,
        download_name="output.pdf"
    )
```

### Mengapa Setiap Bagian Penting

- **`request.files.get("file")`** – Mengambil file yang diunggah dengan aman; menggunakan `.get` menghindari `KeyError` jika bidang tidak ada.
- **`io.BytesIO`** – Menyimpan semuanya di RAM, sehingga tidak pernah menulis file sementara ke disk. Ini penting untuk skalabilitas.
- **`auto_fit_columns()`** – Tanpa ini, lebar kolom sering terlihat sempit di PDF. Metode ini memperluas setiap kolom agar sesuai dengan sel terpanjang, memberikan tampilan profesional.
- **`workbook.save(..., cells.SaveFormat.PDF)`** – Panggilan tunggal ini melakukan pekerjaan berat mengonversi XLSX ke PDF. Aspose.Cells menangani formula, diagram, dan bahkan sel yang digabung.
- **`flask send_file pdf`** – Mengirim PDF kembali ke klien dengan header yang tepat, memicu unduhan dengan nama `output.pdf`.

## Langkah 4 – Jalankan Server Flask

Tambahkan “run guard” tipikal di bagian bawah `app.py` sehingga skrip dapat dijalankan langsung.

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

Menjalankan `python app.py` akan memulai server pada `http://localhost:5000`. Flag `debug=True` berguna selama pengembangan; ingat untuk mematikannya di produksi.

## Langkah 5 – Uji Endpoint (Manual & Otomatis)

### Uji Manual dengan cURL

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

Jika semuanya berjalan lancar, `result.pdf` akan berisi versi yang diformat dengan baik dari `sample.xlsx`, dengan semua kolom auto‑fitted.

### Uji Otomatis dengan `requests` Python

```python
import requests

with open("sample.xlsx", "rb") as f:
    response = requests.post(
        "http://localhost:5000/convert",
        files={"file": f}
    )
    response.raise_for_status()
    with open("downloaded.pdf", "wb") as out:
        out.write(response.content)

print("PDF saved as downloaded.pdf")
```

Kedua pendekatan menunjukkan alur kerja lengkap **python excel to pdf**—dari unggah ke unduh—tanpa pernah menyentuh sistem file di sisi server.

## Langkah 6 – Kasus Edge & Kesalahan Umum

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Large XLSX files ( > 50 MB ) | Tekanan memori pada server | Alirkan unggahan ke file sementara dan gunakan `Workbook(file_path)` alih-alih `BytesIO`. |
| Password‑protected workbook | `Workbook` melemparkan pengecualian | Berikan password ke konstruktor `Workbook`: `Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`. |
| Missing `auto_fit_columns()` | Kolom PDF terlihat terpotong | Selalu panggil `auto_fit_columns()` **sebelum** `save()`. |
| Client expects a JSON error | Flask mengembalikan halaman error HTML | Kembalikan dict JSON dengan kode status yang tepat seperti yang ditunjukkan di endpoint (baris `return {"error": "No file provided"}, 400`). |

Dengan mengantisipasi skenario ini, API Anda tetap kuat dan ramah pengguna.

## Langkah 7 – Deploy ke Produksi

Saat Anda siap meluncurkan, pertimbangkan penyesuaian tingkat produksi berikut:

- **Gunakan server WSGI** seperti `gunicorn` (`gunicorn -w 4 app:app`) alih-alih server bawaan Flask.
- **Aktifkan HTTPS** melalui reverse proxy (NGINX) untuk melindungi unggahan file.
- **Tetapkan batas ukuran permintaan** (`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`) untuk menghindari serangan denial‑of‑service.
- **Catat error** dengan logger terstruktur (mis., `structlog`) sehingga Anda dapat melacak kegagalan konversi.

Semua langkah ini mempertahankan logika inti **save workbook as pdf** sambil menjadikan layanan siap produksi.

## Output yang Diharapkan

Saat Anda memanggil endpoint `/convert` dengan file XLSX yang valid, respons akan:

1. Memiliki header `Content-Type: application/pdf`.
2. Meminta browser (atau klien) untuk mengunduh file bernama `output.pdf`.
3. Menampilkan spreadsheet dengan kolom yang secara otomatis disesuaikan dengan kontennya, berkat pemanggilan `auto fit excel columns`.

Buka PDF yang diunduh—Anda akan melihat setiap kolom terlihat penuh, formula dievaluasi, dan gambar yang disematkan tetap terjaga.

## Kesimpulan

Anda kini memiliki contoh lengkap yang siap produksi yang **save workbook as pdf** menggunakan Flask, Aspose.Cells, dan Python murni. Tutorial ini mencakup semua hal mulai dari menyiapkan lingkungan, **convert xlsx to pdf**, auto‑fitting kolom, dan akhirnya mengirimkan hasilnya dengan `flask send_file pdf`.

Selanjutnya, Anda dapat mengeksplorasi penambahan **custom styling**, menggabungkan sel, atau bahkan mengonversi beberapa worksheet menjadi satu PDF multi‑halaman. Pola yang sama berlaku untuk tipe file lain—cukup ganti enum `SaveFormat`.

Ada pertanyaan tentang kasus edge atau deployment? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menyimpan Halaman Spesifik dari File Excel sebagai PDF Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Simpan Workbook Excel sebagai PDF dengan Font Kustom menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Konversi Excel ke PDF dengan Fit Columns di Java menggunakan Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}