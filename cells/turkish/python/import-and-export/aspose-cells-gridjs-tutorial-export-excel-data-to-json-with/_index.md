---
category: general
date: 2026-07-03
description: Aspose Cells GridJs öğreticisi, Excel verilerini JSON olarak dışa aktarmayı
  ve çalışma sayfasını tembel yükleme kullanarak verimli bir şekilde JSON'a dışa aktarmayı
  gösterir.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: tr
og_description: Aspose Cells GridJs öğreticisi, Excel verilerini JSON olarak dışa
  aktarmayı ve büyük elektronik tablolar için tembel yükleme ile çalışma sayfasını
  JSON’a dışa aktarmayı açıklar.
og_title: Aspose Cells GridJs öğreticisi – Excel verilerini JSON'a aktar
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Aspose Cells GridJs öğreticisi – Excel verilerini tembel yükleme ile JSON'a
  dışa aktar
url: /tr/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells GridJs öğreticisi – Excel verilerini JSON olarak tembel yükleme ile dışa aktar

Büyük bir elektronik tabloyu tarayıcıyı yavaşlatmadan **Excel verilerini JSON** olarak dışa aktarmayı hiç merak ettiniz mi? Bu Aspose Cells GridJs öğreticisinde, **worksheet'i JSON'a dışa aktarma** işlemini tembel yükleme (lazy loading) kullanarak, sadece ihtiyacınız olan satırların talep üzerine alınmasını sağlayan, tamamen çalışır bir çözümü adım adım inceleyeceğiz.

Eğer dev `.xlsx` dosyalarıyla uğraşıyorsanız ve istemci tarafı donuyorsa yalnız değilsiniz. İyi haber? Burada ele aldığımız yaklaşım hem hafif hem de ölçeklenebilir; Aspose.Cells kütüphanesini zaten kullanan herhangi bir Python projesine kolayca ekleyebilirsiniz.

## Bu kılavuzda neler ele alınıyor

Önümüzdeki birkaç dakikada şunları öğreneceksiniz:

1. Aspose.Cells ile büyük bir çalışma kitabını yükleme.
2. GridJs tembel yüklemeyi etkinleştirerek sunucunun satırları parçalar halinde akıtmasını sağlama.
3. GridJs yapılandırmasını, ön uçta kullanılabilecek bir JSON dosyasına dışa aktarma.
4. Optimum performans için parça (chunk) boyutunu ayarlama.
5. Çıktıyı doğrulama ve basit bir HTML sayfasına entegre etme.

Harici hizmetler, gizli sihirler yok—sadece saf Python ve Aspose.Cells API'si. Sonunda **worksheet'i JSON'a dışa aktarma** sürecini, panolar, raporlama araçları veya herhangi bir veri‑ızgara bileşeni için uyarlayabileceğiniz bir şekilde elde edeceksiniz.

### Önkoşullar

- Yerel olarak kurulu Python 3.8+.
- `asposecells` paketi ( `pip install aspose-cells` ile kurabilirsiniz).
- Bilinen bir dizinde bulunan büyük bir Excel dosyası (ör. `large-data.xlsx`).
- Python ve web geliştirme kavramlarına temel aşinalık.

Eğer bu maddeler size yabancı geliyorsa panik yapmayın—her adımda kısa bir “neden” açıklaması bulunacak, böylece kodun arkasındaki mantığı anlayacaksınız.

---

## Adım 1: Aspose.Cells'i kurun ve içe aktarın

İlk olarak Aspose.Cells kütüphanesine ihtiyacımız var. Ticari bir ürün, ancak geliştirme için ücretsiz deneme sürümü yeterli.

```bash
pip install aspose-cells
```

Şimdi script'inizde gerekli sınıfları içe aktarın.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Neden önemli:** `Workbook` sınıfını içe aktarmak, Excel dosyalarını doğrudan belleğe okuyarak daha yavaş `openpyxl` yöntemini atlayan yüksek performanslı motoru kullanmanızı sağlar.

## Adım 2: Büyük veri kümesini içeren çalışma kitabını yükleyin

Kütüphane hazır olduğuna göre, Excel dosyanıza işaret edin. Yol mutlak ya da göreli olabilir; dosyanın mevcut olduğundan emin olun.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Pro ipucu:** Çalışma kitabınız birkaç yüz megabayttan büyükse, Python işlem bellek sınırını artırmayı veya `MemoryError` almamak için 64‑bit yorumlayıcı kullanmayı düşünün.

## Adım 3: GridJs tembel yüklemeyi etkinleştirin

GridJs, Aspose'in JavaScript ızgara bileşenidir. Tembel yükleme, sunucunun yalnızca bir satır alt kümesini göndermesini sağlar—dev sayfalar için mükemmeldir.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Neden tembel yükleme?** Tembel yükleme olmadan, tüm worksheet tek seferde JSON'a serileştirilir ve bu, tarayıcı bellek sınırlarını kolayca aşabilir. `LazyLoadingChunkSize` değerini 500 olarak ayarladığınızda, her istek yönetilebilir bir yük taşır.

## Adım 4: GridJs yapılandırmasını JSON'a dışa aktarın

Şimdi Aspose'den, ön uç GridJs bileşeninin beklediği JSON'ı üretmesini istiyoruz. Bu, **export excel data json** işleminin çekirdeğidir.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

`ExportGridJsJson` metodu, worksheet'in JSON temsili içeren bir `bytes` nesnesi döndürür; bu nesneyi kaydedebilir ya da akış olarak gönderebilirsiniz.

## Adım 5: JSON'ı bir dosyaya (veya akışa) yazın

Hızlı bir test için JSON'ı diske yazalım. Üretim ortamında bir Flask/Django uç noktasından doğrudan dönebilirsiniz.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Gördükleriniz:** `lazygrid.json` dosyasını açtığınızda `columns`, `rows` ve sayfalama meta verileri içeren bir yapı göreceksiniz. `rows` dizisi başlangıçta boş olur; GridJs sayfa yüklendiğinde ilk parçayı (chunk) isteyecektir.

## Adım 6: JSON'ı basit bir HTML sayfasına bağlayın (isteğe bağlı)

Izgarayı çalışır halde görmek istiyorsanız, CDN üzerinden GridJs'i yükleyen ve oluşturulan JSON'a işaret eden küçük bir HTML dosyası oluşturun.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Neden ekliyoruz?** Bu, tam bir turu gösterir: Python JSON'ı oluşturur, tarayıcı alır ve GridJs veriyi parça parça render eder. Farklı `LazyLoadingChunkSize` değerleriyle ağınız için en uygun ayarı deneyebilirsiniz.

## Adım 7: Doğrulayın ve sorun giderin

Python script'ini çalıştırın:

```bash
python export_lazy_grid.py
```

Başarı mesajını ve bir `lazygrid.json` dosyasını görmelisiniz. HTML dosyasını tarayıcıda açın; ızgara ilk 500 satırı anında gösterecek ve daha fazlasını yüklemek için sayfalama kontrolleri sunacaktır.

Izgara boş görünüyorsa:

- **JSON dosyasının boyutunu kontrol edin** – sıfır baytlık bir dosya genellikle çalışma kitabı yolunun yanlış olduğuna işaret eder.
- **Tembel yüklemenin etkin olduğundan emin olun** – `LazyLoading` bayrağı `True` olmalı.
- **Tarayıcı konsolunu inceleyin** – CORS ya da 404 hataları JSON'ın doğru servis edilmediğini gösterir.

---

## Yaygın varyasyonlar ve kenar durumları

### Belirli bir worksheet'i dışa aktarma

Yukarıdaki örnek her zaman ilk worksheet'i (`Worksheets[0]`) kullanır. Farklı bir sayfayı dışa aktarmak için indeksi değiştirin ya da sayfa adını kullanın:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Büyük dosyalar için parça (chunk) boyutunu değiştirme

Milyonlarca satır içeren dosyalarda 500 satırlık parça hâlâ çok küçük olabilir ve çok sayıda istek oluşturur. Parça boyutunu 2000 ya da daha yüksek bir değere çıkarabilirsiniz; ancak daha büyük parçalar istekte daha fazla bant genişliği tüketir.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Dosya yerine akışa dışa aktarma

API'niz JSON'ı doğrudan döndürüyorsa, diske yazmanıza gerek yoktur:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Formüller ve biçimlendirme işleme

Varsayılan olarak, `ExportGridJsJson` formüllerin hesaplanmış değerlerini içerir. Ham formüllere ihtiyacınız varsa şu ayarı yapın:

```python
grid_options.ExportFormulas = True
```

---

## Sonuç

Bu **Aspose Cells GridJs öğreticisinde** **Excel verilerini JSON** olarak dışa aktarma ve **worksheet'i JSON'a dışa aktarma** işlemlerini tembel yükleme ile nasıl yapacağınızı öğrendiniz. Aspose.Cells'i kurmaktan tembel yüklemeyi etkinleştirmeye, JSON üretmeye ve basit bir HTML sayfasıyla bağlamaya kadar tam bir full‑stack desenine sahip oldunuz; bu desen dev elektronik tablolarla sorunsuz ölçeklenir.

Deneyin—parça boyutunu ayarlayın, farklı worksheet'lere yönlendirin veya uç noktayı bir Flask ya da Django uygulamasına entegre edin. Olanaklar sınırsız, performans artışı ise anında.

Bir sonraki adıma hazır mısınız? Sütun sıralama, özel hücre renderları ya da sunucu‑tarafı filtreleme ekleyerek GridJs ızgaranızı gerçek anlamda etkileşimli hâle getirin. Bir sorunla karşılaşırsanız aşağıya yorum bırakın; mutlu kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımları keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}