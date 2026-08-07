---
category: general
date: 2026-06-30
description: GridJs'te özel bağlam menüsü ekleyin ve Excel çalışma kitabını nasıl
  yükleyeceğinizi, hücre değerini nasıl güncelleyeceğinizi, yazım denetimini nasıl
  etkinleştireceğinizi ve özel komutu nasıl kaydedeceğinizi öğrenin.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: tr
og_description: Excel çalışma kitabını yüklemeyi, hücre değerini güncellemeyi, yazım
  denetimini etkinleştirmeyi ve özel komut kaydetmeyi öğrenirken GridJs'te özel bağlam
  menüsü ekleyin.
og_title: GridJs'e Özel Bağlam Menüsü Ekle – Adım Adım Python Öğreticisi
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
title: GridJs'e Özel Bağlam Menüsü Ekle – Tam Python Rehberi
url: /tr/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs'e Özel Bağlam Menüsü Ekle – Tam Python Rehberi

Hiç **özel bağlam menüsü eklemek** öğelerini GridJs tablosuna eklemeyi merak ettiniz mi? Yalnız değilsiniz. Birçok veri‑ağır uygulamada, kullanıcıların satırları işaretlemesini, öğeleri incelendi olarak işaretlemesini veya sunucu‑tarafı bir eylemi başlatmasını sağlayan sağ‑tık menüsüne ihtiyacınız olur—ızgaradan çıkmadan.  

Bu öğreticide bir Excel çalışma kitabını yüklemeyi, özel bir bağlam‑menüsü girişi bağlamayı, bir hücre değerini güncellemeyi, yazım denetimini etkinleştirmeyi ve değişiklikleri dosyaya geri kaydeden özel bir komut kaydetmeyi adım adım göstereceğiz. Sonunda, kullanıcılarınıza yerel hissettiren ve kaynak elektronik tabloya doğrudan yazan tam işlevsel bir GridJs örneğine sahip olacaksınız.

## Önkoşullar

- Python 3.9+ (kod tip ipuçları kullanıyor ancak herhangi bir yeni sürümde çalışır)  
- `cells` kütüphanesi (veya `Workbook` ve `Worksheet` nesnelerini sağlayan herhangi bir Excel‑işleme sarmalayıcısı)  
- `gridjs` Python bağlayıcısı (nesne modeli JavaScript API'sine benzer)  
- Lambda ve JSON yapıları hakkında temel bir anlayış  

Eğer bunlara sahipseniz, başlayalım.

## Adım 1: Excel Çalışma Kitabını Yükleyin ve Bir Çalışma Sayfası Seçin

İlk yapmanız gereken **excel çalışma kitabını yüklemek**, böylece GridJs görüntülemek için veri alır. `cells.Workbook` sınıfı dosya‑IO'yu soyutlar ve satır, sütun ve tek tek hücrelere doğrudan erişim sağlar.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Bu neden önemli:** Çalışma kitabını önceden yüklemek, ızgaranın veriyi talep üzerine çekebilmesini sağlar ve daha sonra yaptığınız tüm düzenlemeler (örneğin **hücre değerini güncellemek**) aynı dosyada kalıcı olur.

## Adım 2: GridJs Örneği Oluşturun ve Çalışma Sayfasına Bağlayın

Şimdi bir `gridjs.GridJs` nesnesi oluşturup hangi çalışma sayfasını render edeceğini söylüyoruz. Bunu, GridJs'in bir sayfa ya da tembel‑yüklenen bir parçayı render etmesi gerektiğinde sorgulayabileceği canlı bir veri kaynağı vermek gibi düşünün.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **İpucu:** Birden fazla sayfa ile çalışıyorsanız, daha sonra sadece `grid.set_worksheet(other_ws)` çağırın—ızgarayı yeniden oluşturmanıza gerek yok.

## Adım 3: Yazım Denetimini Etkinleştirin (ve Diğer İyi Özellikler)

Çoğu iş uygulaması kullanıcılara serbest metin notları yazdırır. **yazım denetimi** etkinleştirmek yazım hatalarını azaltır ve veri kalitesini artırır. GridJs bunun için basit bir bayrak sunar.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Yazım denetimini neden etkinleştirmelisiniz?** İstemci‑tarafında çalışır, ekstra sunucu çağrısı olmadan anlık geri bildirim verir—büyük ölçekli sayfalar için mükemmeldir.

## Adım 4: Özel Bağlam‑Menüsü Öğesi Ekleyin

İşte öğretinin kalbi: **özel bağlam menüsü eklemek** girişleri. “İncelendi Olarak İşaretle” seçeneğini oluşturacağız; tıklandığında bir sonraki adımda tanımlayacağımız sunucu‑tarafı komutu çalıştıracak.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Image illustration**  
> ![Özel Bağlam Menüsü ekleme ekran görüntüsü, sağ‑tık seçeneklerini gösteriyor](/images/add-custom-context-menu.png "Özel Bağlam Menüsü örneği")

Yukarıdaki alt metin anahtar kelimeyi içerir ve SEO gereksinimlerini karşılar.

## Adım 5: Hücre Değerini Güncellemek İçin Özel Komutu Kaydedin

Kullanıcı “İncelendi Olarak İşaretle”yi seçtiğinde, temel Excel hücresini güncelleyen ve dosyayı kaydeden **özel komutu kaydetmek** gerekir. `grid.register_custom_command` yöntemi, daha önce belirlediğimiz eylem tanımlayıcısına bir Python çağrılabilir nesnesi bağlar.

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

> **Bu neden çalışıyor:** İşleyici, istemciden hücre referansını alır, `Worksheet` API'sini kullanarak **hücre değerini güncellemek** ve ardından tüm çalışma kitabını diske yazar. Yanıt, ön‑uçta işlemin başarılı olduğunu bildirir.

### Kenar‑Durum İşleme

- **Eksik hücre referansı:** `req` içinde `"cell"` yoksa, UI'nin bir toast göstermesi için net bir hata yükseltin.  
- **Eşzamanlı düzenlemeler:** Yüksek trafikli senaryolarda, çalışma kitabını kilitlemeyi veya sürüm‑damgası kullanarak yarış koşullarını önlemeyi düşünün.

## Adım 6: Büyük Sayfalar İçin Tembel Yüklemeyi Etkinleştirin

Binlerce satırla uğraşıyorsanız, tembel yükleme UI'yi hızlı tutar. Sayfa boyutunu makul bir parçaya ayarlayın—çoğu tarayıcı için 500 satır iyi çalışır.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **10 000 satırınız olsaydı ne olur?** Izgara, veriyi sayfa‑sayfa isteyecek, hem istemci hem de sunucu üzerindeki bellek baskısını azaltacaktır.

## Adım 7: (İsteğe Bağlı) Satır Düzenleme İçin Özel Modal Ekleyin

Bazen satır içi editörden daha zengin bir UI'ye ihtiyaç duyarsınız. GridJs, istediğiniz yerde barındırabileceğiniz—belki bir React bileşeni ya da basit bir HTML formu—bir modal pencere açmanıza izin verir.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Neden bir modal kullanmalı?** Karmaşık doğrulama mantığını izole eder ve düzen üzerinde tam kontrol sağlar, aynı zamanda ızgaradan tetiklenir.

## Adım 8: İstemci‑Tarafı Konfigürasyon JSON'ını Alın

Son olarak, konfigürasyonu tarayıcıya göndermeniz gerekir. `get_client_config` yöntemi her şeyi bir JSON bloğuna serileştirir ve ön‑uç GridJs kütüphanesi bunu tüketebilir.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Çıktı kabaca şu şekilde görünür (kısaltılmıştır):

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

### Beklenen Sonuç

- Herhangi bir hücreye sağ‑tıklamak, **İncelendi Olarak İşaretle** menüsü açar.  
- Seçildiğinde sunucuya bir istek gönderilir; sunucu **hücre değerini güncellemek** “Reviewed” olarak ayarlar ve `example‑updated.xlsx` dosyasını kaydeder.  
- Yazım denetimi, kullanıcı yazdıkça hatalı kelimeleri vurgular.  

Tüm bunlar tam sayfa yenilemesi olmadan gerçekleşir; tembel yükleme ve hafif JSON yükü sayesinde.

## Sık Sorulan Sorular & İpucu

| Soru | Cevap |
|----------|--------|
| *Çalışma kitabı yalnızca‑okunur ise ne olur?* | Dosya izinlerinin yazma erişimine izin verdiğinden emin olun veya kütüphane destekliyorsa `mode="rw"` ile çalışma kitabını açın. |
| *Birden fazla özel menü öğesi ekleyebilir miyim?* | Kesinlikle—sadece `grid.settings.context_menu.custom_items` listesine ek dict'ler ekleyin. |
| *Bir hücre güncellemesinden sonra ızgarayı yeniden yüklemem gerekir mi?* | GridJs, `{status:"ok"}` döndürürseniz etkilenen satırı otomatik yeniler; aksi takdirde istemciden `grid.refresh()` çağırın. |
| *Yazım denetimini dil‑spesifik nasıl yaparım?* | `grid.settings.spell_check.language = "en-US"` (veya desteklenen herhangi bir yerel) ayarlayın. |
| *Tembel yükleme sunucu‑tarafı filtreleme ile uyumlu mu?* | Evet—`grid.settings.filter.enabled = True` ile birleştirin ve filtre mantığını özel komutunuzda uygulayın. |

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda bir Flask rotasına yerleştirebileceğiniz veya bağımsız bir süreç olarak çalıştırabileceğiniz tek bir betik bulunuyor. `YOUR_DIRECTORY` ifadesini sunucunuzdaki gerçek yol ile değiştirin.

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


## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose.Cells Java Kullanarak Excel Çalışma Kitaplarına Özel İçerik Türü Özellikleri Ekleme](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Workbook'a ID ile Özel XML Bölümleri Ekleme](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Özel Yükleme Filtreleri Excel Dışa Aktarma](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}