---
category: general
date: 2026-06-30
description: Python'da özel modal ayarlarıyla GridJs örneği oluşturun. Bir çalışma
  sayfasını nasıl bağlayacağınızı, modalı nasıl yapılandıracağınızı ve istemci JSON'ını
  nasıl çıktıya alacağınızı öğrenin.
draft: false
keywords:
- create gridjs instance
- gridjs custom modal
- gridjs worksheet integration
- gridjs client configuration
- gridjs python api
language: tr
og_description: Python'da özel modal ayarlarıyla GridJs örneği oluşturun. Çalışma
  sayfası entegrasyonu ve istemci yapılandırması için adım adım talimatlar.
og_title: GridJs Örneği Oluştur – Tam Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create GridJs instance in Python with custom modal settings. Learn
    how to bind a worksheet, configure the modal, and output client JSON.
  headline: Create GridJs Instance – Complete Python Guide
  type: TechArticle
tags:
- gridjs
- python
- web‑ui
- data‑grid
title: GridJs Örneği Oluştur – Tam Python Rehberi
url: /tr/python/integration-and-interoperability/create-gridjs-instance-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs Örneği Oluşturma – Tam Python Rehberi

Python'dan **create gridjs instance** oluşturmayı hiç düşündünüz mü, saçınızı yolmadan? Tek başınıza değilsiniz. İster bir yönetim paneli, ister bir ürün kataloğu, ister hızlı bir elektronik tablo oluşturuyor olun, GridJs'i kurup çalıştırmak ilk engeldir.  

Bu öğreticide gerçek bir örnek üzerinden ilerleyeceğiz: bir çalışma sayfasını bağlamak, çift tıklamada açılan bir özel modalı etkinleştirmek ve sonunda istemci tarafı yapılandırma JSON'ını alarak ön uca besleyebileceksiniz. Sonunda, herhangi bir Flask veya Django projesine ekleyebileceğiniz çalışan bir GridJs kurulumuna sahip olacaksınız.

## Önkoşullar

- Python 3.8+ yerel olarak kurulu  
- Python'da OOP konusunda temel aşinalık  
- Minimum bir `Worksheet` sınıfı (demo için bir taklit oluşturacağız)  

Python için dış bir GridJs paketi bulunmadığından, JavaScript kütüphanesini yansıtan API'yi taklit edeceğiz. Kavramlar doğrudan gerçek GridJs JavaScript kullanımına aktarılabilir.

## Adım 1: Mock GridJs Sınıfını Tanımlama (GridJs Python API)

**create gridjs instance** yapabilmeden önce, gerçek kütüphaneyi taklit eden ince bir sarmalayıcıya ihtiyacımız var. Bu, örneğin çalıştırılabilir olmasını sağlar ve yapılandırma akışına odaklanır.

```python
# gridjs_mock.py
import json

class Settings:
    """Container for all GridJs settings."""
    def __init__(self):
        self.custom_modal = CustomModal()

class CustomModal:
    """Settings for the double‑click custom modal."""
    def __init__(self):
        self.enabled = False
        self.title = ""
        self.width = "400px"
        self.height = "300px"
        self.url = ""

class GridJs:
    """A lightweight Python representation of a GridJs grid."""
    def __init__(self):
        self._worksheet = None
        self.settings = Settings()

    def set_worksheet(self, worksheet):
        """Bind a Worksheet object to the grid."""
        self._worksheet = worksheet

    def get_client_config(self):
        """Serialize the grid configuration for the front‑end."""
        config = {
            "worksheet": getattr(self._worksheet, "name", "undefined"),
            "custom_modal": {
                "enabled": self.settings.custom_modal.enabled,
                "title": self.settings.custom_modal.title,
                "width": self.settings.custom_modal.width,
                "height": self.settings.custom_modal.height,
                "url": self.settings.custom_modal.url,
            },
        }
        return json.dumps(config, indent=2)
```

> **Pro tip:** Python sarmalayıcısını ince tutun—JavaScript tarafına aktaracağınız JSON'ı üretmek için yeterli olsun. Köprüyü aşırı mühendislik yapmak bakım yükünü artırır.

## Adım 2: Basit bir Worksheet Nesnesi Oluşturma (GridJs Worksheet Entegrasyonu)

**gridjs worksheet integration** bir `name` özniteliğine sahip bir sınıf kadar basit olabilir. Gerçek bir uygulamada verileri bir veritabanı ya da CSV dosyasından çekeriniz.

```python
# worksheet.py
class Worksheet:
    """Mock worksheet holding tabular data."""
    def __init__(self, name):
        self.name = name
        # Imagine self.rows = [...] here
```

Artık ızgaraya aktarabileceğiniz bir yer tutucunuz var.

## Adım 3: Izgarayı Oluşturma – Temel “Create GridJs Instance” Mantığı

Mock sınıflar hazır olduğunda, nihayet **create gridjs instance** yapabilir ve adım adım yapılandırabiliriz.

```python
# main.py
from gridjs_mock import GridJs
from worksheet import Worksheet

# 1️⃣ Create a GridJs instance
grid = GridJs()

# 2️⃣ Associate the worksheet you want to display
worksheet = Worksheet(name="Products")
grid.set_worksheet(worksheet)

# 3️⃣ Enable the custom modal that appears on double‑click
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Product"
grid.settings.custom_modal.width = "600px"
grid.settings.custom_modal.height = "400px"

# 4️⃣ Point the modal to an external HTML editor page
grid.settings.custom_modal.url = "/product-editor.html"

# 5️⃣ Retrieve the client‑side configuration JSON and output it
config_json = grid.get_client_config()
print(config_json)
```

### Beklenen Çıktı (GridJs İstemci Yapılandırması)

`python main.py` çalıştırmak, güzel biçimlendirilmiş bir JSON bloğu üretir:

```json
{
  "worksheet": "Products",
  "custom_modal": {
    "enabled": true,
    "title": "Edit Product",
    "width": "600px",
    "height": "400px",
    "url": "/product-editor.html"
  }
}
```

Bu JSON, ön‑uç GridJs yapıcısına besleyeceğiniz tam o veridir:

```javascript
new Grid({
  data: [],               // will be filled from the worksheet
  customModal: {/* … */} // values from the JSON above
});
```

## Adım 4: JSON'ı Ön‑Uç Sayfasına Bağlamak (Hepsini Bir Araya Getirme)

Az önce yazdırdığınız **gridjs client configuration** bir Flask rotasına gömülebilir:

```python
# app.py (Flask snippet)
from flask import Flask, render_template_string, jsonify
from main import config_json  # reuse the same grid setup

app = Flask(__name__)

@app.route("/grid-config")
def grid_config():
    return jsonify(json.loads(config_json))

# Simple HTML page loading GridJs from CDN
HTML = """
<!doctype html>
<html>
<head>
  <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
</head>
<body>
  <div id="wrapper"></div>
  <script>
    fetch('/grid-config')
      .then(r => r.json())
      .then(config => {
        new gridjs.Grid({
          columns: ['ID', 'Name', 'Price'],
          data: [], // fetch actual rows based on config.worksheet
          customModal: config.custom_modal
        }).render(document.getElementById('wrapper'));
      });
  </script>
</body>
</html>
"""
@app.route("/")
def index():
    return render_template_string(HTML)

if __name__ == "__main__":
    app.run(debug=True)
```

> **Neden çalışıyor:** Arka uç, Python'da tanımladığınız ayarları yansıtan bir JSON yükü sağlar. Ön uç aynı yükü okur ve **gridjs custom modal**'ın tam olarak yapılandırdığınız gibi davranmasını garantiler.

## Yaygın Tuzaklar ve Kenar Durumları (GridJs Custom Modal)

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| Modal çift tıklamada hiç açılmıyor | `custom_modal.enabled` `False` olarak bırakıldı | `grid.settings.custom_modal.enabled = True` olarak ayarladığınızdan emin olun |
| Modal boyutları mobilde garip görünüyor | Sabit piksel değerleri (`600px`) ölçeklenmiyor | CSS‑göreceli birimler (`%80`, `vh`) veya medya sorguları kullanın |
| URL 404 hatası döndürüyor | `/product-editor.html` yolu sunulmuyor | Flask/Django'da bir static route ekleyin ya da dosyayı bir CDN'de barındırın |
| Worksheet adı JSON'da eksik | `Worksheet` nesnesinde `name` özniteliği yok | Anlamlı bir `name` sağlayın ya da mock'ı metadata içerecek şekilde genişletin |

Bunları erken ele almak, ileride saatler süren hata ayıklamayı önler.

## Örneği Genişletme (Sonraki Adımlar)

- **Load real data**: Mock `Worksheet`i bir pandas DataFrame ile değiştirin ve satırları JSON'a serileştirin.  
- **Secure the modal**: `/product-editor.html` sunulmadan önce kimlik doğrulama kontrolleri ekleyin.  
- **Dynamic column mapping**: Sütun başlıklarını sabit kodlamak yerine worksheet şemasından çekin.  
- **Internationalization**: Modal başlıklarını bir dil dosyasında saklayın ve JSON yükü aracılığıyla enjekte edin.  

Tüm bu geliştirmeler, az önce öğrendiğiniz aynı **create gridjs instance** temeli üzerine inşa edilir.

## Sonuç

Python'da **create gridjs instance** yapmak için ihtiyacınız olan her şeyi ele aldık; bir worksheet'i bağlamaktan özel bir modalı etkinleştirmeye ve sonunda temiz bir istemci‑tarafı yapılandırma JSON'ı sunmaya kadar. Bu desen basit, yeniden kullanılabilir ve herhangi bir modern web çerçevesine rahatça uyum sağlar.

Bir deneyin, modal boyutlarını ayarlayın, worksheet'i gerçek bir veritabanı sorgusuyla değiştirin ve kısa sürede üretime hazır bir GridJs entegrasyonuna sahip olacaksınız. Sorularınız mı var? Yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisin?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create a Custom Size Chart PDF with Aspose.Cells .NET: Step‑by‑Step Guide](/cells/english/net/charts-graphs/create-custom-size-chart-pdf-aspose-cells-net/)
- [How to Create a Custom Static Value Function in Aspose.Cells Java](/cells/english/java/formulas-functions/aspose-cells-java-custom-static-value-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}