---
category: general
date: 2026-06-21
description: Aktifkan pemeriksaan ejaan saat mengekspor JSON Excel menggunakan GridJs.
  Pelajari cara mengonversi xlsx ke JSON, mengatur lazy loading, dan memuat workbook
  Excel secara efisien.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: id
og_description: Aktifkan pemeriksaan ejaan saat mengekspor Excel JSON dengan GridJs.
  Panduan ini menunjukkan cara mengonversi xlsx ke JSON, mengonfigurasi lazy loading,
  dan memuat workbook Excel.
og_title: Aktifkan Pemeriksaan Ejaan & Ekspor Excel JSON dengan GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Aktifkan Pemeriksaan Ejaan & Ekspor Excel JSON dengan GridJs
url: /id/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktifkan Pemeriksaan Ejaan & Ekspor Excel JSON dengan GridJs

Pernah membutuhkan untuk **mengaktifkan pemeriksaan ejaan** di UI spreadsheet berbasis web dan bertanya-tanya bagaimana cara mengeluarkan data sebagai JSON sekaligus? Anda tidak sendirian. Banyak pengembang mengalami hal yang sama ketika mereka mencoba **mengekspor Excel JSON** dari sebuah workbook sambil mempertahankan fitur lanjutan seperti validasi rumus.

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang dapat dijalankan, yang menunjukkan cara **memuat workbook Excel**, mengubahnya menjadi payload JSON dengan GridJs, **mengonfigurasi lazy loading**, dan tentu saja **mengaktifkan pemeriksaan ejaan**. Pada akhir tutorial Anda akan dapat **mengonversi xlsx ke JSON** hanya dengan beberapa baris kode—tanpa misteri, tanpa bagian yang hilang.

> **Apa yang akan Anda dapatkan**  
> * Skrip Python yang membaca file `.xlsx`, membuat objek server GridJs, dan menulis `grid_data.json`.  
> * Pemahaman mengapa setiap opsi penting (pemeriksaan ejaan, pemeriksaan rumus, lazy loading).  
> * Tips untuk menskalakan solusi ke workbook yang lebih besar.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut di mesin Anda:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.9+ | Diperlukan untuk paket `cells` yang digunakan di bawah. |
| Perpustakaan `cells` (`pip install cells`) | Menyediakan kelas `Workbook` dan `GridJs`. |
| File Excel contoh (`sample.xlsx`) | Ini adalah sumber yang akan **memuat workbook excel**. |
| Izin menulis ke folder output | Diperlukan untuk langkah `grid.save()`. |

Jika ada yang belum familiar, hentikan sejenak dan instal dulu—jika tidak, skrip akan menghasilkan error impor.

---

## Langkah 1: Muat Workbook Excel

Hal pertama yang Anda lakukan ketika ingin **mengonversi xlsx ke json** adalah membuka workbook. Anggap saja ini seperti membuka pintu sebelum Anda dapat menghias ruangan.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Tips pro:** Jika file Anda sangat besar, pertimbangkan menggunakan `cells.Workbook(..., read_only=True)` untuk mengurangi konsumsi memori.

---

## Langkah 2: Buat Objek Server GridJs

Sekarang workbook sudah berada di memori, kita memerlukan objek **GridJs** yang akan menerjemahkan sheet menjadi JSON yang dapat dikonsumsi UI klien.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

Variabel `grid` pada dasarnya adalah wrapper tipis di atas workbook yang tahu cara men-serialize sel, rumus, dan bahkan informasi styling.

---

## Langkah 3: Aktifkan Pemeriksaan Ejaan (dan Pemeriksa Rumus)

Di sinilah kata kunci utama bersinar. Dengan mengaktifkan flag `enableSpellCheck`, Anda memberi pengguna akhir jaring pengaman terhadap typo—sama seperti di Excel desktop.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Mengapa mengaktifkan keduanya? Pemeriksaan ejaan menangkap kesalahan teks, sementara pemeriksa rumus melindungi dari perhitungan yang rusak. Bersama‑sama mereka membuat UI web terasa sehalus pengalaman Excel native.

---

## Langkah 4: Konfigurasi Lazy Loading

Jika Anda berurusan dengan ribuan baris, mengirim seluruh dataset dalam satu payload akan membuat browser terhambat. **Konfigurasikan lazy loading** untuk mengirim data dalam potongan kecil (500 baris per permintaan dalam contoh kami).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Anda dapat menyesuaikan `pageSize` berdasarkan kondisi jaringan Anda. Halaman yang lebih kecil berarti lebih banyak round‑trip tetapi UI lebih halus; halaman yang lebih besar mengurangi panggilan tetapi dapat menyebabkan lag.

---

## Langkah 5: Ekspor Excel JSON

Semua kerja keras kini berada di belakang layar. Langkah akhir adalah **mengekspor excel json** ke file yang dapat diminta oleh front‑end Anda.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Ketika metode `save` selesai, Anda akan memiliki `grid_data.json` yang rapi berisi:

* Nama dan ID sheet  
* Data baris (nilai, rumus, dan format)  
* Metadata tentang fitur yang diaktifkan (pemeriksaan ejaan, lazy loading, dll.)

Anda dapat memverifikasi output dengan membuka file di editor teks atau memuatnya di konsol browser:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

Itulah **solusi lengkap dan mandiri** untuk mengubah file Excel menjadi payload JSON sambil mempertahankan pemeriksaan ejaan.

---

## Skrip Lengkap – Gabungkan Semua

Berikut adalah seluruh program yang dapat Anda salin‑tempel, sesuaikan jalurnya, dan jalankan. Tanpa langkah tersembunyi, tanpa skrip eksternal—hanya satu file.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Simpan sebagai `export_gridjs.py` dan jalankan:

```bash
python export_gridjs.py
```

Anda akan melihat serangkaian pesan `[✓]` yang mengonfirmasi setiap langkah berhasil.

---

## Pertanyaan Umum & Kasus Pinggir

**Bagaimana jika workbook saya berisi banyak sheet?**  
GridJs secara otomatis mengiterasi setiap sheet, sehingga JSON yang dihasilkan akan memiliki array `sheets`. Anda dapat memfilter di sisi klien jika hanya membutuhkan subset.

**Bisakah saya menonaktifkan pemeriksaan ejaan untuk sheet tertentu?**  
Dictionary `options` berlaku secara global. Untuk mengubah per‑sheet, Anda harus membuat objek `GridJs` terpisah atau memproses JSON setelahnya.

**File saya lebih besar dari 10 MB—apakah lazy loading tetap membantu?**  
Tentu saja. Lazy loading bekerja di level API; server hanya mengalirkan halaman yang diminta. Namun, pertimbangkan meningkatkan `pageSize` menjadi 1000 jika latensi jaringan Anda rendah.

**Apakah saya perlu khawatir tentang karakter Unicode?**  
`cells` menangani UTF‑8 secara default, sehingga karakter seperti emoji atau skrip non‑Latin tetap utuh selama proses.

---

## Tips Pro untuk Produksi

* **Cache JSON** – Jika workbook jarang berubah, cache `grid_data.json` di CDN untuk pemuatan super cepat.  
* **Keamanan** – Jangan pernah mengekspos file Excel mentah; layani hanya JSON yang dihasilkan.  
* **Versi** – Sertakan nomor versi dalam nama file JSON (misalnya `grid_data_v2.json`) untuk menghindari data usang setelah pembaruan.  
* **Pengujian** – Tulis unit test kecil yang memuat JSON dan memeriksa bahwa `enableSpellCheck` bernilai `true`. Ini menangkap regresi lebih awal.

---

## Kesimpulan

Anda kini memiliki resep end‑to‑end yang solid untuk **mengaktifkan pemeriksaan ejaan** sambil **mengekspor Excel JSON** menggunakan GridJs. Dari **memuat workbook excel** hingga **mengonfigurasi lazy loading** dan akhirnya **mengonversi xlsx ke json**, prosesnya sederhana dan siap produksi.

Langkah selanjutnya? Coba sambungkan `grid_data.json` yang dihasilkan ke halaman HTML sederhana yang menggunakan pustaka klien GridJs, bereksperimen dengan renderer sel kustom, atau tambahkan otentikasi di sekitar endpoint JSON. Langit adalah batasnya ketika Anda menggabungkan pemeriksaan ejaan, lazy loading, dan konversi Excel‑to‑JSON yang mulus.

Ada pertanyaan lebih lanjut atau workbook rumit yang sedang Anda perjuangkan? Tinggalkan komentar di bawah, dan selamat coding!

---

![Aktifkan pemeriksaan ejaan di GridJs](/images/enable-spell-check-gridjs.png "Tangkapan layar menunjukkan pemeriksaan ejaan diaktifkan dalam UI GridJs")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Export Excel to JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}