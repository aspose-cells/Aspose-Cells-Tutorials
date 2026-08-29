---
category: general
date: 2026-06-30
description: Python Excel ızgarasına özel bağlam menüsü ekleyin ve güncellenmiş dosyayı
  kaydederken değeri Excel hücresine yazın. Sağ‑tık menüsü oluşturmayı ve hücre değerini
  Python tarzında güncellemeyi öğrenin.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: tr
og_description: Python'da özel bir bağlam menüsü ekleyerek değeri Excel hücresine
  yazın ve güncellenmiş Excel dosyasını kaydedin. Bu rehber, GridJs ile sağ‑tık menüsü
  oluşturmayı adım adım anlatır.
og_title: Python'da Özel Bağlam Menüsü Ekle – Adım Adım Öğretici
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
title: Python'da Özel Bağlam Menüsü Ekle – Tam Rehber
url: /tr/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Özel Bağlam Menüsü Ekle – Tam Kılavuz

Python'dan hizmet verdiğiniz bir elektronik tablo ızgarasına **özel bağlam menüsü** öğeleri eklemeyi hiç merak ettiniz mi? Belki bir kullanıcının bir hücreye sağ‑tıkladığında ortaya çıkan, hücreye bir değer yazan ve ardından güncellenmiş çalışma kitabını kaydeden hızlı bir “Mark as Reviewed” düğmesine ihtiyacınız var—bütün bunlar web UI'dan çıkmadan.

Bu öğreticide tam olarak bunu oluşturacağız: GridJs tarafından desteklenen bir **custom right‑click menu**, **write(s) value to excel cell** yapan bir sunucu‑tarafı işleyici ve diskte **save(s) updated excel file** yapan son adım. Sonunda, herhangi bir Flask, FastAPI veya Django projesine ekleyebileceğiniz yeniden kullanılabilir bir deseniniz olacak.

> **Neden önemseyelim?**  
> Özel bir bağlam menüsü eklemek, veri inceleme iş akışlarını hızlandırır, manuel kopyala‑yapıştırmayı azaltır ve son‑kullanıcılara ızgara içinde doğrudan yerel‑hissettirir bir deneyim sunar. Ayrıca **update cell value python**‑style nasıl yapılacağını göreceksiniz, bu da herhangi bir Excel otomasyon görevi için temel bir beceridir.

## Gereksinimler

- Python 3.9+ (kod 3.10'da da çalışır)  
- `openpyxl` Excel dosyası işleme için  
- `gridjs` Python sarmalayıcısı (veya ön‑uç tercih ediyorsanız JS kütüphanesi)  
- Temel bir web çerçevesi (Flask örneği gösterilmiştir)  
- Proje klasörünüzde `sample.xlsx` adlı bir çalışma kitabı dosyası  

Eğer bunlardan herhangi birine sahip değilseniz, şu komutu çalıştırın:

```bash
pip install openpyxl flask gridjs
```

Şimdi derinlemesine inceleyelim.

---

## Adım 1 – Özel Bağlam Menüsü Ekle: GridJs'i Başlat ve Çalışma Sayfasını Bağla

İlk yapmanız gereken, bir `GridJs` örneği oluşturup çalışmayı planladığınız çalışma sayfasına yönlendirmektir. İşte kodumuzda **add custom context menu** ifadesinin ilk kez göründüğü yer ve bu, diğer her şey için sahneyi hazırlar.

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

**Ne oluyor?**  
`grid.set_worksheet(ws)` GridJs'e `ws`'den gelen verileri veri kaynağı olarak kullanmasını söyler. Bundan sonra eklediğimiz tüm bağlam‑menüsü değişiklikleri otomatik olarak aynı çalışma sayfasını hedefleyecek, UI ve dosyayı senkronize tutacaktır.

> **Pro ipucu:** Çalışma kitabınızı yalnızca bir kez okuma/yazma modunda açık tutun. Bir istek işleyicisi içinde tekrar tekrar açmak, Windows'ta dosya kilitleme sorunlarına yol açabilir.

---

## Adım 2 – Excel Hücresine Değer Yaz: Menü Öğesi İçin Eylemi Tanımla

Izgara hazır olduğuna göre, kullanıcı özel komutumuzu seçtiğinde **write value to excel cell** yapmamız gerekiyor. “Mark as Reviewed” adlı bir menü girişi ekleyecek ve ona `markReviewed` tanımlayıcısını vereceğiz. Bu tanımlayıcı, istemci‑tarafı JavaScript'in sunucuya geri göndereceği şeydir.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Neden özel bir tanımlayıcı kullanmalı?**  
Tanımlayıcı, UI metnini sunucu mantığından ayırır, etiketi backend koduna dokunmadan değiştirmenize olanak tanır. Ayrıca **create right‑click menu** işlemini açık ve yeniden kullanılabilir hâle getirir.

---

## Adım 3 – Sağ‑Tık Menüsü Oluştur: Sunucu‑Tarafı İşleyiciyi Kaydet

Menü öğesi yerinde olduğunda, kullanıcı tıkladığında GridJs'e ne yapması gerektiğini söylememiz gerekir. İşte **create right‑click menu** işlevselliğinin Python'a bir istek gönderdiği yer.

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

Not edilmesi gereken birkaç nokta:

1. **`ws[cell_address] = "Reviewed"`** **update cell value python** yapmanın en basit yoludur. `openpyxl`, A1‑stilindeki adresi satır/sütun indekslerine dönüştürür.
2. İşleyici küçük bir JSON yükü döndürür. GridJs bir durum göstergesi bekler; gerekirse hata mesajlarını ekleyerek genişletebilirsiniz.

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Hücre boş ya da korumalıysa ne olur?**  
- Boş hücreler sorun değil—`openpyxl` onları anında oluşturur.  
- Korunan sayfalar için önce korumayı kaldırmanız gerekir (`ws.protection.sheet = False`) veya bir `PermissionError` yakalayın.

---

## Adım 4 – Hücre Değerini Python ile Güncelle: Çalışma Kitabını Kaydederek Değişikliği Kalıcı Hale Getir

Bir değeri yazmak hikâyenin sadece yarısı; değişikliğin mevcut oturumun ötesinde kalması için **save updated excel file** yapmanız gerekir. İşte UI'dan diske dönüş yolculuğunu tamamladığımız yer.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Neden ayrı bir klasör?**  
`output/` dizinine kaydetmek, orijinal şablonu dokunulmaz tutar; bu denetim izleri için faydalıdır. Yolu, dağıtım ortamınıza göre ayarlayın.

> **Dikkat:** Çok sayıda eşzamanlı kullanıcı hizmeti veriyorsanız, yarış durumlarını önlemek için `wb.save()` etrafında bir thread‑safe kilidi (`threading.Lock`) kullanmayı düşünün.

---

## Adım 5 – İstemci Konfigürasyon JSON'u Oluştur ve Hepsini Birleştir

Son olarak, ön‑uç GridJs örneğinin tüketeceği JSON'u üretmemiz gerekiyor. Bu JSON, çalışma sayfası verisini **ve** özel menü tanımını içerir.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

`config_json`'i HTML sayfanıza gömdüğünüzde, GridJs her hücrede sağ‑tıkla “Mark as Reviewed” girişini gösteren bir ızgara renderlayacaktır.

### Tam Flask Örneği

Aşağıda, tüm parçaları bir araya getiren minimal bir Flask uygulaması bulunmaktadır. Çalıştırın, `http://localhost:5000` adresini açın ve herhangi bir hücreye sağ‑tıklayarak özel menünün çalışmasını görün.

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

**Beklenen sonuç:**  
- Herhangi bir hücreye sağ‑tıkla → “Mark as Reviewed” görünür.  
- Tıkla → hücre içeriği “Reviewed” olarak değişir.  
- `output/sample-updated.xlsx` çalışma kitabı artık yeni değeri içerir.

---

## Yaygın Sorular & Kenar Durumları

| Soru | Cevap |
|------|-------|
| *Birden fazla özel eyleme ihtiyacım olsaydı ne olur?* | `grid.settings.context_menu.custom_items`'a daha fazla nesne ekleyin ve her birini kendi tanımlayıcısı ile kaydedin. |
| *İşleyiciye ek veri (ör. satır ID'si) geçirebilir miyim?* | Evet. İstemci tarafındaki JSON yüküne ek anahtarlar ekleyin, ardından `on_custom_command` içinde `request`'ten okuyun. |
| *Bu yaklaşım async çerçevelerle uyumlu mu?* | Kesinlikle—`on_custom_command`'ı async bir fonksiyon yapın ve `aiofiles` gibi bir şeye geçerseniz `await wb.save(...)` kullanın. |
| *Menü ikonunu nasıl stilize ederim?* | Herhangi bir Material‑Icons adını (`"icon": "edit"`) sağlayın. Ön‑uç otomatik olarak ikon fontunu yükler. |
| *Büyük çalışma kitaplarıyla ne yapılmalı?* | Yalnızca gerekli sayfayı yükleyin ve bellek kullanımını düşük tutmak için `openpyxl.iter_rows()` ile satırları akış olarak almaya bakın. |

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Excel'de Hücre Değeri veya Aralığının Tek Tırnak Önekini Koru](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Excel'de Hücre Değeri veya Aralığının Tek Tırnak Önekini Koru](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Excel'de Hücre Değeri veya Aralığının Tek Tırnak Önekini Koru](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}