---
category: general
date: 2026-06-08
description: Tambahkan menu konteks kustom ke GridJs dan ekspor grid ke CSV dengan
  blob file CSV yang dapat diunduh. Ikuti tutorial langkah demi langkah ini untuk
  contoh yang berfungsi sepenuhnya.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: id
og_description: Tambahkan menu konteks khusus ke GridJs dan ekspor grid ke CSV dengan
  blob file CSV yang dapat diunduh. Pelajari implementasi lengkapnya dalam kurang
  dari 10 menit.
og_title: Tambahkan Menu Konteks Kustom ke GridJs – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Menambahkan Menu Konteks Kustom ke GridJs – Panduan Lengkap
url: /id/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Menu Konteks Kustom ke GridJs – Panduan Lengkap

Ingin **menambahkan menu konteks kustom** ke komponen GridJs? Dalam tutorial ini kami akan memandu Anda langkah demi langkah, dan menunjukkan cara **mengekspor grid ke CSV** menggunakan **download CSV file blob**. Baik Anda sedang membangun panel admin cepat atau dashboard pelaporan lengkap, menu klik kanan yang memungkinkan pengguna mengekspor data sebagai CSV dapat menjadi peningkatan produktivitas yang nyata.

Kami akan membahas semua yang Anda perlukan: sisi Python dengan Flask, handler JavaScript yang membuat Blob, dan HTML/JS yang dihasilkan GridJs. Pada akhir tutorial Anda akan memiliki contoh mandiri yang dapat Anda masukkan ke proyek mana pun.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- **Python 3.9+** dan **Flask** terpasang (`pip install flask`).
- Wrapper Python **gridjs** (atau perpustakaan JavaScript secara langsung) – untuk panduan ini kami mengasumsikan wrapper Python tipis yang meniru API JavaScript.
- Pemahaman dasar tentang **async JavaScript** (`fetch`, `Promise`) – tetapi jangan khawatir, kami akan menjelaskan setiap baris.
- Editor yang **Anda suka** (VS Code, PyCharm, atau bahkan editor teks sederhana sudah cukup).

Itu saja. Tidak ada alat build front‑end tambahan, tidak ada tarian Node npm. Hanya Flask biasa yang menyajikan HTML yang dihasilkan GridJs.

---

## Menambahkan Menu Konteks Kustom ke GridJs

Hal pertama yang harus Anda lakukan adalah memberi tahu GridJs bahwa Anda menginginkan menu klik kanan kustom. Secara default GridJs menyediakan set minimal (copy, paste, dll.), tetapi Anda dapat menggantinya sepenuhnya.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Mengapa ini penting:**  
Mengatur `CustomContextMenu` menggantikan daftar default dengan daftar yang Anda sediakan. String `"Export CSV"` hanyalah label – pekerjaan sebenarnya terjadi ketika pengguna mengkliknya, yang akan kami hubungkan pada langkah berikutnya.

> *Tip pro:* Jaga daftar tetap singkat. Menu konteks yang berantakan mengalahkan tujuan aksi cepat.

---

## Ekspor Grid ke CSV dengan Unduhan Blob

Sekarang item menu sudah ada, kita memerlukan handler JavaScript yang berkomunikasi dengan server, mengambil CSV, mengubahnya menjadi **Blob**, dan memaksa unduhan. Di sinilah frasa **download CSV file blob** berada.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Menganalisis Handler

| Baris | Apa yang Dilakukan |
|------|--------------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Memanggil route Flask (`/export/csv`) dengan mengirimkan nama sheet sebagai query string. |
| `.then(r => r.blob())` | Mengonversi respons HTTP menjadi **Blob** – pada dasarnya wadah biner untuk data CSV. |
| `URL.createObjectURL(b)` | Membuat URL sementara yang dapat diperlakukan browser seperti file. |
| `a.download = cell.sheetName + ".csv"` | Menetapkan nama file yang akan dilihat pengguna di dialog unduhan. |
| `a.click()` | Secara programatik mengklik anchor tersembunyi, memicu browser mengunduh Blob. |

> **Mengapa menggunakan Blob?**  
> Browser tidak dapat langsung mengunduh teks mentah yang dikembalikan dari `fetch` tanpa mengubahnya menjadi sesuatu yang mirip file. Trik Blob‑URL adalah cara paling dapat diandalkan dan lintas‑browser untuk memicu **download CSV file blob** tanpa menyegarkan halaman.

---

## Menyiapkan Backend Flask

Handler front‑end mengharapkan endpoint di `/export/csv`. Berikut contoh view Flask minimal yang mengambil nama sheet, mengambil data dari workbook, dan mengalirkan CSV kembali.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Poin Penting

- **`io.StringIO`** memungkinkan kami membangun CSV di memori tanpa menyentuh sistem file.
- **`Content‑Disposition`** memberi tahu browser bahwa file adalah lampiran dan menyarankan nama file. Meskipun front‑end juga mengatur `a.download`, menambahkannya di sisi server memberikan cadangan untuk klien non‑JS.
- Route ini sengaja dibuat sederhana; Anda dapat menambahkan otentikasi, pemeriksaan izin, atau streaming untuk dataset besar di kemudian hari.

---

## Merender Grid di Klien

Dengan menu konteks dan backend siap, bagian terakhir adalah merender komponen GridJs dan mengirimkan HTML/JS ke browser.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Di view Flask biasanya Anda akan melakukan:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Saat halaman dimuat, GridJs membangun tabel, menyuntikkan menu konteks kustom, dan handler JavaScript yang kami definisikan sebelumnya siap dijalankan. Klik kanan pada sel mana pun, pilih **Export CSV**, dan lihat browser mengunduh file yang dinamai sesuai sheet.

---

## Contoh Kerja Lengkap (Semua File)

Berikut adalah kode lengkap yang dapat dijalankan yang dapat Anda salin‑tempel ke folder baru. Instal Flask (`pip install flask`) dan jalankan `python app.py`.

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Muat File Csv dengan Parser Kustom Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Kode Ekspor Csv Java](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Ekspor Excel Csv Baris Kosong Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}