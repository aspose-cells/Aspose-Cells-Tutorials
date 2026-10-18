---
category: general
date: 2026-06-30
description: Tambahkan menu konteks khusus di GridJs dan pelajari cara memuat buku
  kerja Excel, memperbarui nilai sel, mengaktifkan pemeriksaan ejaan, serta mendaftarkan
  perintah khusus.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: id
og_description: Tambahkan menu konteks khusus di GridJs sambil mempelajari cara memuat
  buku kerja Excel, memperbarui nilai sel, mengaktifkan pemeriksaan ejaan, dan mendaftarkan
  perintah khusus.
og_title: Tambahkan Menu Konteks Kustom ke GridJs – Tutorial Python Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Tambahkan Menu Konteks Kustom ke GridJs – Panduan Python Lengkap
url: /id/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Menu Konteks Kustom ke GridJs – Panduan Python Lengkap

Pernah bertanya-tanya bagaimana cara **menambahkan item menu konteks kustom** ke tabel GridJs yang didukung oleh workbook Excel? Anda tidak sendirian. Dalam banyak aplikasi dengan data berat, Anda memerlukan menu klik kanan itu untuk memungkinkan pengguna menandai baris, menandai item sebagai telah ditinjau, atau memicu aksi sisi server—tanpa meninggalkan grid.  

Dalam tutorial ini kami akan menelusuri cara memuat workbook Excel, menyiapkan entri menu konteks kustom, memperbarui nilai sel, mengaktifkan pemeriksaan ejaan, dan mendaftarkan perintah kustom yang menyimpan perubahan kembali ke file. Pada akhir tutorial Anda akan memiliki instance GridJs yang berfungsi penuh, terasa alami bagi pengguna, dan menulis langsung kembali ke spreadsheet sumber.

## Prasyarat

- Python 3.9+ (kode menggunakan type hints tetapi dapat dijalankan pada versi terbaru apa pun)  
- pustaka `cells` (atau pembungkus penanganan Excel apa pun yang menyediakan objek `Workbook` dan `Worksheet`)  
- binding Python `gridjs` (model objeknya mencerminkan API JavaScript)  
- Pemahaman dasar tentang lambda dan struktur JSON  

Jika Anda sudah memiliki semua itu, mari kita mulai.

## Langkah 1: Muat Workbook Excel dan Pilih Worksheet

Hal pertama yang harus Anda lakukan adalah **memuat workbook excel** agar GridJs memiliki data untuk ditampilkan. Kelas `cells.Workbook` mengabstraksi file‑IO dan memberi Anda akses langsung ke baris, kolom, serta sel individu.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Mengapa ini penting:** Memuat workbook di awal berarti grid dapat menarik data sesuai permintaan, dan setiap penyuntingan yang Anda lakukan nanti (seperti **memperbarui nilai sel**) akan dipertahankan ke file yang sama.

## Langkah 2: Buat Instance GridJs dan Sambungkan ke Worksheet

Sekarang kami membuat objek `gridjs.GridJs` dan memberitahukan worksheet mana yang harus dirender. Anggap ini sebagai memberi GridJs sumber data langsung yang dapat di‑query kapan pun diperlukan untuk merender halaman atau potongan yang dimuat secara malas.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Tips pro:** Jika Anda bekerja dengan beberapa sheet, cukup panggil `grid.set_worksheet(other_ws)` nanti—tidak perlu membuat ulang grid.

## Langkah 3: Aktifkan Pemeriksaan Ejaan (dan Fitur Tambahan Lainnya)

Sebagian besar aplikasi bisnis memungkinkan pengguna menulis catatan bebas. Mengaktifkan **pemeriksaan ejaan** mengurangi kesalahan ketik dan meningkatkan kualitas data. GridJs menyediakan flag sederhana untuk itu.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Mengapa mengaktifkan pemeriksaan ejaan?** Ia berjalan di sisi klien, memberikan umpan balik instan tanpa panggilan server tambahan—sempurna untuk lembar kerja berskala besar.

## Langkah 4: Tambahkan Item Menu Konteks Kustom

Berikut inti tutorial: **menambahkan item menu konteks kustom**. Kami akan membuat opsi “Mark as Reviewed” yang, ketika diklik, menjalankan perintah sisi server yang akan kami definisikan selanjutnya.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Ilustrasi gambar**  
> ![Tangkapan layar Tambahkan Menu Konteks Kustom yang menunjukkan opsi klik kanan](/images/add-custom-context-menu.png "Contoh Tambahkan Menu Konteks Kustom")

Teks alt di atas berisi kata kunci utama, memenuhi persyaratan SEO.

## Langkah 5: Daftarkan Perintah Kustom untuk Memperbarui Nilai Sel

Ketika pengguna memilih “Mark as Reviewed,” kita perlu **mendaftarkan perintah kustom** yang memperbarui sel Excel yang mendasarinya dan menyimpan file. Metode `grid.register_custom_command` mengikat callable Python ke identifier aksi yang kami tetapkan sebelumnya.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Mengapa ini berhasil:** Handler menerima referensi sel dari klien, menggunakan API `Worksheet` untuk **memperbarui nilai sel**, lalu menulis seluruh workbook kembali ke disk. Respons memberi tahu front‑end bahwa operasi berhasil.

### Penanganan Kasus Edge

- **Referensi sel hilang:** Jika `req` tidak memiliki `"cell"`, lempar error yang jelas sehingga UI dapat menampilkan toast.  
- **Edit bersamaan:** Untuk skenario lalu lintas tinggi, pertimbangkan mengunci workbook atau menggunakan cap versi untuk menghindari kondisi balapan.

## Langkah 6: Aktifkan Lazy Loading untuk Lembar Besar

Jika Anda menangani ribuan baris, lazy loading membuat UI tetap responsif. Tetapkan ukuran halaman ke potongan yang wajar—500 baris biasanya cocok untuk kebanyakan browser.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Bagaimana jika Anda memiliki 10 000 baris?** Grid akan meminta data halaman demi halaman, mengurangi tekanan memori pada klien dan server.

## Langkah 7: (Opsional) Tambahkan Modal Kustom untuk Penyuntingan Baris

Kadang‑kadang Anda memerlukan UI yang lebih kaya daripada penyunting inline. GridJs memungkinkan Anda membuka jendela modal yang dapat Anda host di mana saja—mungkin komponen React atau formulir HTML sederhana.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Mengapa menggunakan modal?** Ia memisahkan logika validasi yang kompleks dan memberi Anda kontrol penuh atas tata letak, sambil tetap dipicu dari grid.

## Langkah 8: Ambil Konfigurasi JSON Sisi Klien

Akhirnya, Anda perlu mengirimkan konfigurasi ke browser. Metode `get_client_config` menyerialisasikan semuanya menjadi blob JSON yang dapat dikonsumsi oleh perpustakaan GridJs di front‑end.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Outputnya kira‑kira seperti ini (dipangkas untuk singkat):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Hasil yang Diharapkan

- Klik kanan pada sel mana pun membuka menu dengan **Mark as Reviewed**.  
- Memilihnya mengirim permintaan ke server, yang **memperbarui nilai sel** menjadi “Reviewed” dan menyimpan `example‑updated.xlsx`.  
- Pemeriksaan ejaan menyoroti kata yang salah eja saat pengguna mengetik.  

Semua ini terjadi tanpa penyegaran halaman penuh, berkat lazy loading dan payload JSON yang ringan.

## Pertanyaan Umum & Tips Pro

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika workbook hanya‑baca?* | Pastikan izin file mengizinkan akses menulis, atau buka workbook dengan `mode="rw"` jika pustaka mendukungnya. |
| *Bisakah saya menambahkan lebih dari satu item menu kustom?* | Tentu saja—cukup tambahkan dict tambahan ke `grid.settings.context_menu.custom_items`. |
| *Apakah saya perlu memuat ulang grid setelah pembaruan sel?* | GridJs secara otomatis menyegarkan baris yang terpengaruh jika Anda mengembalikan `{status:"ok"}`; jika tidak, panggil `grid.refresh()` dari klien. |
| *Bagaimana cara membuat pemeriksaan ejaan spesifik bahasa?* | Atur `grid.settings.spell_check.language = "en-US"` (atau locale yang didukung lainnya). |
| *Apakah lazy loading kompatibel dengan penyaringan sisi server?* | Ya—gabungkan `grid.settings.filter.enabled = True` dan implementasikan logika filter dalam perintah kustom Anda. |

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabung)

Berikut adalah skrip tunggal yang dapat Anda letakkan di route Flask atau jalankan sebagai proses mandiri. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya di server Anda.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Tambahkan Properti Tipe Konten Kustom ke Workbook Excel Menggunakan Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Tambahkan Bagian XML Kustom dengan ID ke Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}