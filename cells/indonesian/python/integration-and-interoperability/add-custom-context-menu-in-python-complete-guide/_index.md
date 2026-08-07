---
category: general
date: 2026-06-30
description: Tambahkan menu konteks khusus ke grid Excel Python dan tulis nilai ke
  sel Excel saat menyimpan file yang diperbarui. Pelajari cara membuat menu klik kanan
  dan memperbarui nilai sel dengan gaya Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: id
og_description: Tambahkan menu konteks khusus di Python untuk menulis nilai ke sel
  Excel dan menyimpan file Excel yang diperbarui. Panduan ini memandu Anda melalui
  pembuatan menu klik kanan dengan GridJs.
og_title: Tambahkan Menu Konteks Kustom di Python – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Menambahkan Menu Konteks Kustom di Python – Panduan Lengkap
url: /id/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Menu Konteks Kustom di Python – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **menambahkan menu konteks kustom** ke dalam grid spreadsheet yang Anda layani dari Python? Mungkin Anda membutuhkan tombol cepat “Mark as Reviewed” yang muncul ketika pengguna mengklik kanan sebuah sel, menulis nilai ke sel Excel, dan kemudian menyimpan workbook yang diperbarui—semua tanpa meninggalkan UI web.  

Dalam tutorial ini kami akan membangun tepat itu: **menu klik kanan kustom** yang didukung oleh GridJs, handler sisi server yang **menulis nilai ke sel excel**, dan langkah akhir yang **menyimpan file excel yang diperbarui** ke disk. Pada akhirnya Anda akan memiliki pola yang dapat digunakan kembali dan dapat dimasukkan ke dalam proyek Flask, FastAPI, atau Django mana pun.

> **Mengapa penting?**  
> Menambahkan menu konteks kustom memperlancar alur kerja peninjauan data, mengurangi penyalinan‑tempel manual, dan memberikan pengguna akhir pengalaman yang terasa native langsung di dalam grid. Selain itu, Anda akan melihat cara **memperbarui nilai sel python**‑style, yang merupakan keterampilan inti untuk tugas otomatisasi Excel apa pun.

## Prasyarat

- Python 3.9+ (kode ini juga berfungsi pada 3.10)  
- `openpyxl` untuk penanganan file Excel  
- `gridjs` pembungkus Python (atau pustaka JS jika Anda lebih suka front‑end)  
- Kerangka web dasar (contoh Flask ditampilkan)  
- File workbook bernama `sample.xlsx` di folder proyek Anda  

Jika Anda belum memiliki salah satu dari ini, jalankan:

```bash
pip install openpyxl flask gridjs
```

Sekarang mari kita mulai.

---

## Langkah 1 – Tambahkan Menu Konteks Kustom: Inisialisasi GridJs dan Kaitkan Worksheet

Hal pertama yang perlu Anda lakukan adalah memulai sebuah instance `GridJs` dan mengarahkannya ke worksheet yang akan Anda kerjakan. Di sinilah frasa **add custom context menu** pertama kali muncul dalam kode kami, dan ini menyiapkan panggung untuk segala hal lainnya.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Apa yang terjadi?**  
`grid.set_worksheet(ws)` memberi tahu GridJs untuk menggunakan data dari `ws` sebagai sumber datanya. Mulai saat ini, setiap modifikasi menu konteks yang kami tambahkan akan secara otomatis menargetkan worksheet yang sama, menjaga UI dan file tetap sinkron.

> **Tip pro:** Buka workbook Anda dalam mode baca/tulis hanya sekali. Membukanya berulang kali di dalam handler permintaan dapat menyebabkan masalah penguncian file di Windows.

---

## Langkah 2 – Tulis Nilai ke Sel Excel: Definisikan Aksi untuk Item Menu

Sekarang grid sudah siap, kita perlu **menulis nilai ke sel excel** ketika pengguna memilih perintah kustom kami. Kami akan menambahkan entri menu bernama “Mark as Reviewed” dan memberi identifier `markReviewed`. Identifier tersebut adalah apa yang akan dikirim kembali ke server oleh JavaScript sisi klien.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Mengapa menggunakan identifier kustom?**  
Identifier memisahkan teks UI dari logika server, memungkinkan Anda mengubah label tanpa menyentuh kode backend. Ini juga membuat operasi **create right‑click menu** menjadi eksplisit dan dapat digunakan kembali.

---

## Langkah 3 – Buat Menu Klik Kanan: Daftarkan Handler Sisi Server

Dengan item menu sudah ada, kita perlu memberi tahu GridJs apa yang harus dilakukan ketika pengguna mengkliknya. Di sinilah kami **create right‑click menu** fungsionalitas yang sebenarnya mengirim permintaan kembali ke Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Beberapa hal yang perlu dicatat:

1. **`ws[cell_address] = "Reviewed"`** adalah cara paling sederhana untuk **update cell value python**. Di balik layar, `openpyxl` menerjemahkan alamat gaya A1 menjadi indeks baris/kolom.  
2. Handler mengembalikan payload JSON kecil. GridJs mengharapkan indikator status; Anda dapat memperluasnya untuk menyertakan pesan error jika diperlukan.

Sekarang kami mengaitkan identifier ke handler:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Bagaimana jika sel kosong atau dilindungi?**  
- Sel kosong tidak masalah—`openpyxl` akan membuatnya secara otomatis.  
- Untuk sheet yang dilindungi, Anda harus membuka proteksi terlebih dahulu (`ws.protection.sheet = False`) atau menangkap `PermissionError`.

---

## Langkah 4 – Perbarui Nilai Sel Python: Simpan Perubahan dengan Menyimpan Workbook

Menulis nilai hanyalah setengah cerita; Anda harus **save updated excel file** agar perubahan tetap ada setelah sesi berakhir. Di sinilah kami menyelesaikan perjalanan bolak‑balik dari UI ke disk.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Mengapa folder terpisah?**  
Menyimpan ke dalam direktori `output/` menjaga template asli tetap tidak tersentuh, yang berguna untuk jejak audit. Sesuaikan path sesuai lingkungan deployment Anda.

> **Waspada:** Jika Anda melayani banyak pengguna secara bersamaan, pertimbangkan menggunakan kunci thread‑safe (`threading.Lock`) di sekitar `wb.save()` untuk menghindari kondisi balapan.

---

## Langkah 5 – Hasilkan JSON Konfigurasi Klien dan Sambungkan Semua

Akhirnya, kami perlu menghasilkan JSON yang akan dikonsumsi oleh instance GridJs di front‑end. JSON ini berisi data worksheet **dan** definisi menu kustom.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Saat Anda menyematkan `config_json` ke dalam halaman HTML Anda, GridJs akan merender grid dengan entri “Mark as Reviewed” yang dapat diklik kanan pada setiap sel.

### Contoh Flask Lengkap

Berikut adalah aplikasi Flask minimal yang menyatukan semua komponen. Jalankan, buka `http://localhost:5000` dan klik kanan pada sel mana pun untuk melihat menu kustom beraksi.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Hasil yang diharapkan:**  
- Klik kanan pada sel mana pun → “Mark as Reviewed” muncul.  
- Klik itu → konten sel berubah menjadi “Reviewed”.  
- Workbook `output/sample-updated.xlsx` kini berisi nilai baru.

---

## Pertanyaan Umum & Kasus Edge

| Question | Answer |
|----------|--------|
| *Bagaimana jika saya membutuhkan beberapa aksi kustom?* | Cukup tambahkan lebih banyak objek ke `grid.settings.context_menu.custom_items` dan daftarkan masing‑masing dengan identifiernya. |
| *Apakah saya dapat mengirim data tambahan (misalnya, ID baris) ke handler?* | Ya. Sertakan kunci tambahan dalam payload JSON di sisi klien, kemudian baca mereka dari `request` di `on_custom_command`. |
| *Apakah pendekatan ini kompatibel dengan kerangka kerja async?* | Tentu—cukup ubah `on_custom_command` menjadi fungsi async dan gunakan `await wb.save(...)` jika Anda beralih ke `aiofiles` atau serupa. |
| *Bagaimana cara menata ikon menu?* | Berikan nama Material‑Icons apa pun (`"icon": "edit"`). Front‑end secara otomatis memuat font ikon. |
| *Bagaimana dengan workbook besar?* | Muat hanya sheet yang diperlukan, dan pertimbangkan streaming baris dengan `openpyxl.iter_rows()` untuk menjaga penggunaan memori. |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Pertahankan Awalan Kutip Tunggal Nilai Sel atau Rentang di Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Pertahankan Awalan Kutip Tunggal Nilai Sel atau Rentang di Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Pertahankan Awalan Kutip Tunggal Nilai Sel atau Rentang di Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}