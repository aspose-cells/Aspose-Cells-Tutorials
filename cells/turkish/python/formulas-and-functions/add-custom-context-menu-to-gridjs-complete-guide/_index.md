---
category: general
date: 2026-06-08
description: GridJs'e özel bağlam menüsü ekleyin ve ızgarayı indirme CSV dosyası blob'u
  ile CSV'ye dışa aktarın. Tamamen çalışan bir örnek için bu adım adım öğreticiyi
  izleyin.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: tr
og_description: GridJs'e özel bağlam menüsü ekleyin ve ızgarayı bir CSV dosyası blob'u
  olarak indirme ile CSV'ye dışa aktarın. Tam uygulamayı 10 dakikadan kısa sürede
  öğrenin.
og_title: GridJs'e Özel Bağlam Menüsü Ekleme – Tam Rehber
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
title: GridJs'e Özel Bağlam Menüsü Ekle – Tam Kılavuz
url: /tr/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs'e Özel Bağlam Menüsü Ekle – Tam Kılavuz

Bir GridJs bileşenine **özel bağlam menüsü eklemek** ister misiniz? Bu öğreticide tam olarak bunu nasıl yapacağınızı ve **CSV dosyası blob'u indir** kullanarak **grid'i CSV olarak dışa aktarmak** göstereceğiz. Hızlı bir yönetim paneli ya da tam kapsamlı bir raporlama panosu oluşturuyor olun, kullanıcıların veriyi CSV olarak almasını sağlayan sağ‑tık menüsü gerçek bir verimlilik artışı sağlayabilir.

İhtiyacınız olan her şeyi ele alacağız: Flask ile Python tarafı, Blob oluşturan JavaScript işleyicisi ve GridJs'in ürettiği HTML/JS. Sonunda, herhangi bir projeye ekleyebileceğiniz bağımsız bir örnek elde edeceksiniz.

---

## İhtiyacınız Olanlar

- **Python 3.9+** ve **Flask** yüklü (`pip install flask`).
- **gridjs** Python sarmalayıcısı (veya doğrudan JavaScript kütüphanesi) – bu kılavuz için JavaScript API'sini yansıtan ince bir Python sarmalayıcısı varsayacağız.
- **async JavaScript** (`fetch`, `Promise`) hakkında temel bir anlayış – ama endişelenmeyin, her satırı açıklayacağız.
- Beğendiğiniz bir editör (VS Code, PyCharm veya basit bir metin editörü bile yeterli).

Hepsi bu. Ek front‑end derleme araçları yok, Node npm karmaşası yok. Sadece GridJs'in ürettiği HTML'i sunan sade Flask.

---

## GridJs'e Özel Bağlam Menüsü Ekle

İlk yapmanız gereken, GridJs'e özel bir sağ‑tık menüsü istediğinizi söylemek. Varsayılan olarak GridJs minimal bir set (kopyala, yapıştır vb.) ile gelir, ancak bunu tamamen değiştirebilirsiniz.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Neden Önemli:**  
`CustomContextMenu` ayarlamak, varsayılan listeyi sağladığınız listeyle değiştirir. `"Export CSV"` sadece bir etiket – gerçek iş, kullanıcının üzerine tıkladığında gerçekleşir ve bunu bir sonraki adımda bağlayacağız.

> *İpucu:* Listeyi kısa tutun. Dağınık bir bağlam menüsü, hızlı eylemlerin amacını bozar.

---

## Blob İndirme ile Grid'i CSV Olarak Dışa Aktar

Artık menü öğesi mevcut olduğuna göre, sunucu ile iletişim kuran, CSV'yi çeken, bir **Blob**'a dönüştüren ve indirmeyi zorlayan bir JavaScript işleyicisine ihtiyacımız var. İşte **download CSV file blob** ifadesinin bulunduğu yer.

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

### İşleyiciyi Açıklama

| Satır | Ne İş Yapar |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Flask rotasını (`/export/csv`) çağırır ve sayfa adını sorgu dizesi olarak gönderir. |
| `.then(r => r.blob())` | HTTP yanıtını bir **Blob**'a dönüştürür – temelde CSV verisi için ikili bir kapsayıcıdır. |
| `URL.createObjectURL(b)` | Tarayıcının bir dosya gibi davranabileceği geçici bir URL oluşturur. |
| `a.download = cell.sheetName + ".csv"` | Kullanıcının indirme iletişim kutusunda göreceği dosya adını ayarlar. |
| `a.click()` | Gizli bağlantıya programlı olarak tıklar, tarayıcının Blob'u indirmesini tetikler. |

> **Neden Blob Kullanılır?**  
> Tarayıcılar, `fetch` ile dönen ham metni doğrudan dosya‑gibi bir şeye dönüştürmeden indiremez. Blob‑URL hilesi, sayfayı yenilemeden **download CSV file blob** tetiklemenin en güvenilir, tarayıcılar arası yoludur.

---

## Flask Backend'ini Kurma

Ön‑uç işleyicisi `/export/csv` adresinde bir uç nokta bekler. İşte sayfa adını alıp, çalışma kitabından verileri çekerek bir CSV akışı gönderen minimal bir Flask görünümü.

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

### Önemli Noktalar

- **`io.StringIO`** dosya sistemine dokunmadan CSV'yi bellek içinde oluşturmamızı sağlar.
- **`Content‑Disposition`** tarayıcıya dosyanın bir ek olduğunu ve bir dosya adı önerdiğini söyler. Ön‑uç da `a.download` ayarlasa da, sunucu tarafında olması JS olmayan istemciler için bir yedek sağlar.
- Rota kasıtlı olarak basittir; daha sonra kimlik doğrulama, izin kontrolleri veya büyük veri setleri için akış ekleyebilirsiniz.

---

## Grid'i İstemci Tarafında Render Etme

Bağlam menüsü ve backend hazır olduğunda, son adım GridJs bileşenini render etmek ve HTML/JS'i tarayıcıya göndermektir.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Bir Flask görünümünde genellikle şu şekilde yaparsınız:

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

Sayfa yüklendiğinde, GridJs tabloyu oluşturur, özel bağlam menüsünü ekler ve daha önce tanımladığımız JavaScript işleyicisi çalışmaya hazırdır. Herhangi bir hücreye sağ‑tıklayın, **Export CSV**'yi seçin ve tarayıcının sayfa adıyla aynı adı taşıyan bir dosya indirdiğini izleyin.

---

## Tam Çalışan Örnek (Tüm Dosyalar)

Aşağıda, yeni bir klasöre kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir kod bulunmaktadır. Flask'i kurun (`pip install flask`) ve `python app.py` komutunu çalıştırın.

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


## Sonra Ne Öğrenmelisin?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [CSV Dosyalarını Özel Ayrıştırıcılarla Yükleme Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [CSV Dışa Aktarma Java Kodu](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Excel CSV Boş Satırları Dışa Aktarma Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}