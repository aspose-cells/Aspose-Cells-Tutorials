---
category: general
date: 2026-11-22
description: Flask kullanarak bir web uygulamasında Excel'i nasıl sunacağınızı öğrenin.
  Bu kılavuz, Excel çalışma kitabını nasıl yükleyeceğinizi ve GridJs ile web üzerinde
  Excel'i nasıl görüntüleyeceğinizi gösterir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: tr
lastmod: 2026-11-22
og_description: Flask ve GridJs kullanarak Excel dosyalarını nasıl sunabilirsiniz.
  Excel çalışma kitabını yüklemek ve webde görüntülemek için bu eksiksiz öğreticiyi
  takip edin.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: Flask ile Excel Nasıl Sunulur – Adım Adım Rehber
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
title: Flask ve GridJs ile Excel dosyalarını nasıl sunarız
url: /tr/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Flask ve GridJs ile Excel Dosyalarını Sunma

If you need to **how to serve excel** in a Python web application, this tutorial shows a complete solution. You’ll learn how to **load excel workbook** with the `cells` library, expose it through a Flask endpoint, and let users **display excel web** using GridJs.

Python web uygulamasında **how to serve excel**'e ihtiyacınız varsa, bu öğretici tam bir çözüm gösterir. `cells` kütüphanesini kullanarak **load excel workbook**'i nasıl yükleyeceğinizi, bir Flask uç noktası aracılığıyla nasıl ortaya çıkaracağınızı ve kullanıcıların GridJs ile **display excel web**'i nasıl görüntüleyeceğini öğreneceksiniz.

We’ll walk through every line of code, explain why each piece matters, and give you a ready‑to‑run example. By the end of the guide you can embed any `.xlsx` file into a responsive, client‑side grid without writing custom JavaScript data parsers.

Kodun her satırını adım adım inceleyecek, her parçanın neden önemli olduğunu açıklayacak ve size çalıştırmaya hazır bir örnek sunacağız. Kılavuzun sonunda, herhangi bir `.xlsx` dosyasını özel JavaScript veri ayrıştırıcıları yazmadan, duyarlı bir istemci‑tarafı ızgaraya gömebilirsiniz.

## Önkoşullar

- Python 3.9+ yüklü  
- `flask` ve `cells` paketleri (`pip install flask cells`)  
- Bilinen bir dizinde örnek bir Excel dosyası (ör. `sample.xlsx`)  

Ek bir ön‑uç çerçevesi gerekmez; GridJs UI'yi otomatik olarak yönetir.

## Çözümün Genel Görünümü

The core idea is simple:

1. **Load** Excel çalışma kitabını sunucuda yükleyin.  
2. **Create** bir `GridJsHandler` oluşturun; bu, çalışma sayfası verilerini GridJs'in beklediği JSON formatına dönüştürür.  
3. **Expose** bir Flask rotası tanımlayın; bu, JSON görünümünü döndürür ve istemciden gelen düzenlemeleri kabul eder.  
4. **Run** Flask sunucusunu çalıştırın, böylece tarayıcı verileri alıp ızgarayı render eder.

Şimdi her adımı uygulayalım.

## Flask ve GridJs ile Excel Nasıl Sunulur

### Adım 1: Excel Çalışma Kitabını Yükleme

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Neden Önemlidir:**  
`cells.Workbook` `.xlsx` dosyasını bellek içi bir temsile ayrıştırır. Çalışma kitabını başlangıçta bir kez yüklemek, sunucunun hızlı kalmasını sağlar; çünkü sonraki istekler aynı nesneyi tekrar tekrar dosya sistemine erişmeden kullanır.

### Adım 2: GridJs Sunucu‑Tarafı İşleyicisi Oluşturma

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Neden Önemlidir:**  
`GridJsHandler`, Excel satır/kolonlarını GridJs'in tükettiği JSON şemasına dönüştürmeyi soyutlar. Ayrıca istemci‑tarafı düzenlemeleri izler, böylece gerektiğinde değişiklikleri daha sonra çalışma kitabına geri kaydedebilirsiniz.

### Adım 3: Opsiyonel Özellikleri Etkinleştirme (lazy loading)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Neden Önemlidir:**  
Bir çalışma sayfası binlerce satır içerdiğinde, tüm veri kümesini bir anda göndermek tarayıcıyı aşırı yükleyebilir. Lazy loading, veriyi sayfa sayfa akış halinde gönderir ve **display excel web** senaryosu için performansı artırır.

### Adım 4: Minimal Bir Flask Uygulaması Kurma

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Neden Önemlidir:**  
Flask, JSON uç noktaları ve statik dosyalar sunabilen hafif bir HTTP sunucusu sağlar. Flask uygulamasını minimal tutmak saldırı yüzeyini azaltır ve örneği uyarlamayı kolaylaştırır.

### Adım 5: GridJs Uç Noktasını Tanımlama

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

**Neden Önemlidir:**  

- **GET** – Tarayıcı ilk çalışma sayfası görünümünü alır.  
- **POST** – Bir kullanıcı bir hücreyi düzenlediğinde, GridJs bir JSON yükü gönderir; `apply_changes` bu düzenlemeleri işleyicinin iç durumuna birleştirir.  

`grid_handler.get_view()`'i döndürmek, istemcinin her zaman en son veriyi almasını sağlar; bu, sorunsuz bir **display excel web** deneyimi için kritiktir.

### Adım 6: Flask Sunucusunu Çalıştırma

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Neden Önemlidir:**  
Port 5000'de çalıştırmak Flask'in varsayılanıdır ve yerel olarak test etmeyi kolaylaştırır (`http://localhost:5000/gridjs`). Üretimde Flask'i bir WSGI sunucusunun (ör. Gunicorn) arkasına koyar ve muhtemelen HTTPS etkinleştirirsiniz.

## Beklenen JSON Çıktısı

`http://localhost:5000/gridjs` adresine GET isteğiyle gittiğinizde, yanıt şu şekilde görünür:

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

GridJs bu yükü otomatik olarak tüketir ve tarayıcıda aranabilir, sıralanabilir bir tablo render eder.

## Tam Çalıştırılabilir Örnek

Aşağıda `app.py` dosyasına kopyalayıp çalıştırabileceğiniz tam betik bulunmaktadır:

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

Betik şu şekilde çalıştırılır:

```bash
python app.py
```

Bir tarayıcı açın ve GridJs'i yükleyen basit bir HTML sayfasına yönlendirin (`<script>` etiketi için GridJs belgelerine bakın). Izgara, Excel içeriğini anında gösterecektir.

## Yaygın Varyasyonlar ve Kenar Durumları

| Durum | Nasıl uyarlamalı |
|-----------|--------------|
| **Birden fazla çalışma sayfası** | Her sayfa için ayrı bir `GridJsHandler` oluşturun ve farklı uç noktalar (`/gridjs/sheet1`, `/gridjs/sheet2`) ortaya çıkarın. |
| **Büyük dosyalar (>10 MB)** | Flask'in istek boyutu limitini (`app.config['MAX_CONTENT_LENGTH']`) artırın ve `lazy_load` özelliğini etkin tutun. |
| **Düzenlemeleri dosyaya geri kaydetme** | `apply_changes` işleminden sonra, değişiklikleri diske yazmak için `workbook.save("output.xlsx")` çağırın. |
| **Kimlik Doğrulama** | Veri döndürmeden önce uç noktayı Flask‑Login veya bir API token kontrolü ile sarın. |
| **Harici ön‑uçlar için CORS** | `from flask_cors import CORS; CORS(app)` ekleyerek çapraz kaynak isteklerine izin verin. |

## Profesyonel İpuçları

- **JSON görünümünü önbelleğe alın** eğer çalışma kitabı nadiren değişiyorsa; `grid_handler.get_view()` etrafında `functools.lru_cache` kullanarak serileştirme yükünü azaltın.  
- **Gelen düzenlemeleri doğrulayın** (`request.json`) bozuk verilerin çalışma kitabını bozmasını önlemek için.  
- HTTPS üzerinden hizmet verirken, trafiği şifrelemek için `app.run(ssl_context=('cert.pem', 'key.pem'))` ayarlayın.

## Sonuç

Artık Flask ve GridJs kullanarak **how to serve excel** dosyalarını nasıl sunacağınızı biliyorsunuz; çalışma kitabını yüklemekten tarayıcının render edebileceği bir JSON görünümü döndürmeye kadar. Örnek tam yaşam döngüsünü kapsar: **load excel workbook**, lazy loading'i etkinleştirme, bir REST uç noktası ortaya çıkarma ve üretime hazır bir sunucu çalıştırma.

Sonra, React ön‑uçta **display excel web** gibi ilgili konuları keşfedin veya işleyiciyi bulut depolamadan (ör. AWS S3) **load excel workbook** yapacak şekilde genişletin. GridJs sütunlarını stilize etmeyi, sayfalama eklemeyi veya kullanıcı düzenlemelerini orijinal tabloya geri kaydetmeyi deneyin.

Kodlamaktan keyif alın ve statik Excel dosyalarını etkileşimli web tablolarına dönüştürmenin tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET ile Excel Dosyalarını Yükleme ve Değiştirme: Kapsamlı Rehber](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [Aspose.Cells Java Kullanarak Excel'i HTML'e Oluşturma ve Dışa Aktarma | Workbook Operations Rehberi](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}