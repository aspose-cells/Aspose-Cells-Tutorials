---
category: general
date: 2026-06-30
description: Tam bir JavaScript örneğiyle gridjs'i kolayca nasıl oluşturulur, gridjs
  yapılandırması, konteyner kurulumu ve render sürecini kapsayan.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: tr
og_description: Tam bir JavaScript örneğiyle gridjs'i kolayca nasıl oluşturacağınızı,
  gridjs yapılandırması, konteyner kurulumu ve render sürecini kapsayan bir rehber.
og_title: Gridjs Nasıl Oluşturulur – Tam JavaScript Grid Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Gridjs Nasıl Oluşturulur – Tam JavaScript Grid Rehberi
url: /tr/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gridjs Nasıl Oluşturulur – Tam JavaScript Grid Rehberi

Sayfada anında şık bir veri tablosu görmek için **gridjs nasıl oluşturulur** merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici Gridjs'i ilk kez bağlamaya çalıştığında, özellikle yapılandırma nesnesi ve render çağrısı etrafında bir duvara çarpar. İyi haber? Doğru adımları bildiğinizde bu aslında çok kolay.

Bu öğreticide, sıfırdan **gridjs nasıl oluşturulur** gösteren gerçek bir örnek, doğru bir **gridjs yapılandırması** nasıl hazırlanır, grid bir **gridjs konteyneri**'ne nasıl bağlanır ve sonunda **gridjs render** nasıl tetiklenir adımlarını inceleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz tam işlevsel bir grid elde edeceksiniz—gizli bir şey yok, sadece net kod.

## Neler Öğreneceksiniz

- Gridjs için hazır minimal bir HTML sayfası kurun.
- Sütunları, verileri ve seçenekleri tanımlayan bir **gridjs yapılandırması** nesnesi yazın.
- Gridjs örneğini bir **gridjs konteyneri** öğesine bağlayın.
- **gridjs render** metodunu çağırarak tabloyu görüntüleyin.
- Yaygın ayarları (sayfalama, sıralama, stil) ayarlayın ve tipik tuzaklardan kaçının.

Harici derleme araçları gerekmez; her şey tek bir script etiketiyle tarayıcıda çalışır. Hadi başlayalım.

## Önkoşullar

1. Modern bir tarayıcı (Chrome, Edge, Firefox, Safari) – ES6'yı destekleyen herhangi bir tarayıcı.
2. HTML ve JavaScript temel bilgisi – bir çerçeveye ihtiyacınız yok.
3. Gridjs kütüphanesine erişim – onu bir CDN'den çekeceğiz, bu yüzden npm kurulumu gerekmez.

Hepsi bu. Zaten geliştirmek istediğiniz bir sayfanız varsa, kod parçacıklarını doğrudan yapıştırabilirsiniz.

## Adım 1: Gridjs Varlıklarını Sayfanıza Ekleyin

İlk olarak, Gridjs'in CSS ve JavaScript dosyalarını yüklememiz gerekiyor. CDN sürümü hafif ve hızlı demolar için mükemmel.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro ipucu:** Mermaid teması, tabloya ekstra CSS olmadan temiz, modern bir görünüm verir. Farklı bir stil tercih ediyorsanız `classic.min.css` ile değiştirmekten çekinmeyin.

## Adım 2: **gridjs konteyneri** Tanımlayın

**gridjs konteyneri**, render edilen tabloyu barındıracak normal bir `<div>`'dir. Yukarıdaki işaretlemede zaten `<div id="grid"></div>` oluşturduk. `id` özniteliği çok önemlidir çünkü Gridjs örneğini daha sonra bağlamak için bunu kullanacağız.

Aynı sayfada birden fazla grid ihtiyacınız varsa, her konteynera benzersiz bir ID (`grid1`, `grid2`, …) verin ve bağlama mantığını her biri için tekrarlayın.

## Adım 3: Bir **gridjs yapılandırması** Nesnesi Oluşturun

Şimdi **gridjs nasıl oluşturulur** konusunun kalbi – yapılandırma geliyor. Bu sade JavaScript nesnesi Gridjs'e hangi sütunların gösterileceğini, hangi verilerin doldurulacağını ve hangi özelliklerin etkinleştirileceğini söyler.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Bu yapılandırmanın önemi

- **Columns** – başlık metnini ve isteğe bağlı genişliği tanımlar. Bu olmadan, Gridjs sütun adlarını ilk veri satırından çıkarır, bu genellikle daha az okunaklı olur.
- **Data** – satırların bir dizisi, her satır hücre değerlerinin bir dizisidir. Ayrıca bir API'den veri çeken async bir fonksiyon da sağlayabilirsiniz; kütüphane sözleşmeleri otomatik olarak yönetir.
- **Pagination** – sayfa başına satır sayısını sınırlar, büyük tabloların UI'yı boğmasını önler.
- **Search & Sort** – tek bir boolean ile etkileşimli özellikleri açar, özel işleyiciler yazmaktan sizi kurtarır.
- **Language** – UI metinlerini özelleştirir, yerelleştirme veya markalaşma için mükemmeldir.

Daha sonra statik veri dizisini bir fetch çağrısıyla değiştirmekten çekinmeyin; diğer adımlar tam olarak aynı kalır.

## Adım 4: Gridjs'i Örnekleyin ve **gridjs konteyneri**'ne Bağlayın

Yapılandırma hazır olduğunda, yeni bir `GridJs.Grid` (UMD yapısında sınıf adı `gridjs.Grid`'dir) oluşturur ve onu konteyner öğemize yönlendiririz.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

`document.getElementById('grid')` kullandığımıza dikkat edin—bu, daha önce tanımladığımız **gridjs konteyneri**'dir. Birden fazla konteyneriniz varsa, bu satırı uygun ID ile tekrarlamanız yeterlidir.

## Adım 5: **gridjs render** Çağrısını Tetikleyin

Bulmacanın son parçası **gridjs render** metodudur. Daha önce gönderdiğimiz yapılandırmayı alır ve konteynere tamamen stillendirilmiş bir `<table>` ekler.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

Hepsi bu! Sayfayı bir tarayıcıda açtığınızda, tanımladığımız dört satırla birlikte arama yapılabilir, sayfalı bir tablo göreceksiniz. Arama kutusu otomatik olarak üstte görünür ve sayfalama kontrolleri altta yer alır.

### Beklenen Çıktı

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

Arama kutusuna yazdığınızda veya sütun başlıklarına tıkladığınızda UI uyum sağlar.

## Yaygın Varyasyonlar ve Kenar Durumları

### Veriyi Asenkron Olarak Yükleme

Veriniz bir sunucuda bulunuyorsa, statik `data` dizisini bir Promise döndüren bir fonksiyonla değiştirin:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Gridjs, promise çözülene kadar bir yükleme çubuğu gösterir, ardından tabloyu otomatik olarak render eder.

### Özel Hücre Render'ı

Bazen hücre içinde ikonlar, butonlar veya biçimlendirilmiş tarihleri ihtiyaç duyarsınız. Bir sütunda `formatter` özelliğini kullanın:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

`gridjs.h` yardımcı fonksiyonu, React çekmeden sanal DOM öğeleri oluşturur.

### Tek Sayfada Birden Fazla Grid

Farklı konteyner ID'leriyle adım 2‑5'i tekrarlamanız yeterlidir:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Her grid bağımsız çalışır, böylece sayfalama limitlerini, sütun setlerini ve hatta temaları karıştırabilirsiniz.

## Pro İpuçları ve Kaçınılması Gereken Tuzaklar

- **CSS'i unutmayın** – stil sayfası olmadan tablo sade bir HTML tablo olarak görünür, tüm güzel stil ve sayfalama kontrolleri kaybolur.
- **Yinelenen ID'lerden kaçının** – her **gridjs konteyneri** benzersiz bir ID'ye sahip olmalıdır; aksi takdirde Gridjs ilk örneği üzerine yazar.
- **Veri şekline dikkat edin** – sütun sayısı her satırdaki hücre sayısıyla eşleşmelidir; uyumsuz diziler sessiz yerleşim hatalarına yol açar.
- **Karmaşık hücreler için `gridjs.h` kullanın** – ham HTML string'leri enjekte etmeye çalışmak sanal DOM fark algoritmasını bozabilir.
- **Sürüme dikkat edin** – yukarıdaki CDN bağlantısı en son 5.x sürümüne (Haziran 2026 itibarıyla) işaret eder. Daha eski bir sürüme kilitlerseniz, bazı seçenekler (ör. `language`) eksik olabilir.

## Tam Çalışan Örnek (Kopyala‑Yapıştır)

Aşağıda, `gridjs-demo.html` olarak kaydedip doğrudan bir tarayıcıda açabileceğiniz tam HTML dosyası bulunmaktadır.



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java&#58; Excel Çalışma Kitaplarını Verimli Şekilde Oluşturma ve Biçimlendirme](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Aspose.Cells Java Kullanarak Excel'i HTML'ye Oluşturma ve Dışa Aktarma | Çalışma Kitabı İşlemleri Rehberi](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Aspose.Cells for Java ile Excel Çalışma Kitaplarını Oluşturma ve Birleştirme | Tam Rehber](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}