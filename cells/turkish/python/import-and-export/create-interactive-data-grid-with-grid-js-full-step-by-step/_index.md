---
category: general
date: 2026-06-21
description: Grid.js kullanarak etkileşimli veri ızgarası oluşturun ve sıralama, sayfalama
  ve arama özellikleriyle JSON veri tablosunu nasıl görüntüleyeceğinizi öğrenin. Web
  panoları için mükemmel.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: tr
og_description: Dakikalar içinde etkileşimli veri ızgarası oluşturun. Grid.js'i kullanarak
  sayfalama, sıralama ve arama özelliklerine sahip JSON veri tablosunu nasıl görüntüleyeceğinizi
  öğrenin.
og_title: Grid.js ile Etkileşimli Veri Izgarası Oluşturun – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Grid.js ile Etkileşimli Veri Izgarası Oluşturun – Tam Adım Adım Kılavuz
url: /tr/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grid.js ile Etkileşimli Veri Izgarası Oluşturma – Tam Adım‑Adım Kılavuz

Hiç **etkileşimli veri ızgarası** oluşturup kullanıcıların sıralama, arama ve sayfalama yapabildiği bir tabloyu backend yazmadan hayal ettiniz mi? Yalnız değilsiniz. Birçok gösterge tablosunda en büyük sıkıntı, statik bir JSON dökümünü pürüzsüz, aranabilir bir tabloya dönüştürmek—bir elektronik tablo kadar akıcı ama tamamen tarayıcıda çalışan bir şey—olmaktadır.

Bu öğreticide **Grid.js'i nasıl kullanacağınızı** bir düz HTML sayfasında **JSON veri tablosu** göstermek için adım adım anlatacağız. Sonunda, herhangi bir projeye ekleyebileceğiniz çalışan bir örnek ve araç çubuğunu özelleştirme, büyük veri setleriyle başa çıkma ve yaygın tuzaklardan kaçınma ipuçları elde edeceksiniz.

## Neler Öğreneceksiniz

- Sütunları ve satırları tanımlayan bir JSON dosyasını nasıl alacağınızı.
- **Grid.js**'i sayfalama, sıralama, arama ve özel bir araç çubuğu ile nasıl başlatacağınızı.
- Izgarayı hedef bir konteynıra nasıl render edeceğinizi.
- İsteğe bağlı ayarlamalar: özel hücre biçimlendirme, tema değiştirme ve hata yönetimi.
- Tamamen kopyala‑yapıştır‑hazır bir kod örneği.

### Ön Koşullar

İlerlemeye başlamadan önce şunlara sahip olduğunuzdan emin olun:

1. Modern bir tarayıcı (Chrome, Edge veya Firefox) – Grid.js ES6 özelliklerine dayanır.
2. `grid_data.json` dosyasını içeren yerel veya uzak bir klasör (formatı aşağıda göstereceğiz).
3. HTML ve JavaScript'e temel aşinalık – hiçbir şey karmaşık değil, sadece bir `.html` dosyasını tarayıcıda açabilmek yeterli.

Herhangi bir derleme aracı, npm kurulumu ya da sunucu‑tarafı kodu yok. **Grid.js ile etkileşimli veri ızgarası** oluşturmanın güzelliği burada: CDN üzerinden doğrudan çalışıyor.

---

## Adım 1: Tablonuzu Tanımlayan JSON'ı Hazırlayın

İlk olarak Grid.js'e hangi sütunların mevcut olduğunu ve hangi satırların gösterileceğini söyleyen bir JSON yüküne ihtiyacınız var. Bunu **JSON veri tablosu görüntüleme** için bir plan gibi düşünün. İşte aynı dizinde `grid_data.json` olarak kaydedebileceğiniz minimal bir örnek:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Bu format neden?* Grid.js `columns`'ın dizi halinde (veya gelişmiş yapılandırma için nesne) ve `rows`'un her iç dizinin sütun sırasına uyan dizi dizisi olmasını bekler. Tabii ki daha fazla sütun ya da iç içe nesneler ekleyebilirsiniz – şekiller uyduğu sürece Grid.js bunları render eder.

> **Pro ipucu:** Bir API'den veri çekiyorsanız, statik `fetch('grid_data.json')` ifadesini uç nokta URL'nizle değiştirmeniz yeterli. Kodun geri kalanı aynı kalır.

---

## Adım 2: Grid.js'i Başlatın – **gridjs nasıl kullanılır**'ın Kalbi

Veri kaynağı hazır olduğuna göre, Grid.js'i sayfaya eklememiz ve davranışını tanımlamamız gerekiyor. İşte burada sayfalama, sıralama ve kullanışlı bir araç çubuğu düğmesi gibi **etkileşimli veri ızgarası** işlevselliğini gerçekten oluşturuyoruz.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN en yeni stabil sürümü sağlar ve Mermaid teması kutudan çıkar çıkmaz temiz, modern bir görünüm ekler. Daha çok varsayılan stil istiyorsanız `gridjs.min.css` ile değiştirebilirsiniz.

Ardından bir `<script>` etiketi içinde JSON'u alıp ızgarayı başlatın:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Seçeneklerin Açıklaması

| Seçenek | Ne İşe Yarar | Neden Önemlidir |
|--------|--------------|----------------|
| `pagination` | Satırları sayfalara böler (varsayılan 10 satır/sayfa) | Büyük tabloları UI'yı boğmadan kullanılabilir tutar. |
| `sort` | Tıklanabilir sütun başlıkları artan/azalan sırayı değiştirir | Kullanıcılar en yüksek değerli satırları hızlıca bulabilir. |
| `search` | Satırları anlık filtreleyen bir metin girişi ekler | Veri yeniden yüklenmeden anlık sorgulamalar için idealdir. |
| `toolbar` | Izgaranın üstüne özel düğmeler veya açılır menüler ekler | “Yardım”, “Dışa Aktar” veya “Yenile” gibi eylemler için mükemmeldir. |
| `formatter` | Bir hücre için ham HTML döndürmenizi sağlar | Burada e‑posta metinlerini tıklanabilir mailto linklerine dönüştürüyoruz. |

> **Neden bu yaklaşım?** Izgara yapılandırmasını deklaratif tutarak, çekirdek render mantığını dokunmadan davranışı kolayca ayarlayabilirsiniz. Bu, çoğu proje için **Grid.js nasıl kullanılır** konusunda önerilen yoldur.

---

## Adım 3: Izgarayı Sayfanıza Render Edin

Script'in son satırı—`grid.render(document.getElementById('grid-container'))`—tam işlevsel tabloyu HTML gövdenizde bir yere yerleştirdiğiniz `<div>` içine enjekte eder:

```html
<div id="grid-container"></div>
```

Hepsi bu. Sayfa yüklendiğinde tarayıcı JSON'u çeker, Grid.js örneğini oluşturur ve etkileşimli tabloyu ekrana çizer. İlk yüklemeden sonra yenileme ya da sunucu çağrısı olmaz.

---

## İsteğe Bağlı: Stil ve Tema Ayarları

Varsayılan Mermaid teması damak tadınıza uymuyorsa, yerleşik temalardan (`gridjs.min.css`) birini seçebilir ya da kendi CSS'inizi yazabilirsiniz. Örneğin, başlık arka planını yumuşak bir gri yapmak için:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Bu kodu bir `<style>` etiketi içinde ya da harici bir stil sayfasına ekleyin. Grid.js standart CSS seçicilerine saygı gösterir, böylece yazı tipleri, renkler ve boşluklar üzerinde tam kontrol sahibi olursunuz.

---

## Yaygın Tuzaklar & Nasıl Önlenir

| Tuzak | Belirti | Çözüm |
|---------|---------|-----|
| **CORS hataları** başka bir alan adından JSON çekerken | Tarayıcı konsolunda “Blocked by CORS policy” mesajı | JSON'u aynı origin'de barındırın ya da sunucuda CORS'u etkinleştirin. |
| **Büyük veri setleri gecikmeye neden olur** | Kaydırma takılır, sayfalama yavaşlar | `server` sayfalama (`pagination: { server: { url: (prev, page, limit) => … } }`) ya da tembel yükleme kullanın. |
| **Araç çubuğu düğmesi görünmüyor** | `toolbar.enabled: true` olmasına rağmen düğme yok | Grid.js sürümünün 2.0+ olduğundan emin olun; eski sürümlerde farklı bir toolbar API'si vardı. |
| **E‑posta linkleri tıklanamaz** | Formatter düz metin döndürüyor | Örnekte gösterildiği gibi `gridjs.html(...)` döndürün, düz string yerine. |

Bu sorunları erken ele almak, ileride saatler süren hata ayıklamayı önler.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda `index.html` olarak kaydedebileceğiniz tam HTML dosyası yer alıyor. Bir tarayıcıda açın ve **etkileşimli veri ızgarası** demo'sunun **JSON veri tablosu** ile sıralama, arama ve yardım düğmesi özelliklerini gördüğünüzden emin olun.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakın ilişkili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}