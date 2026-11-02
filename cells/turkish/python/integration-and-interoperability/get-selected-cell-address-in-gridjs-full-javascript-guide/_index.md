---
category: general
date: 2026-06-30
description: GridJs kullanarak JavaScript ile seçili hücre adresini nasıl alacağınızı,
  ızgara hücre değerini nasıl güncelleyeceğinizi ve giriş değerini nasıl okuyacağınızı
  öğrenin. Adım adım kod ve ipuçları.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: tr
og_description: Seçili hücre adresini alın, ızgara hücre değerini güncelleyin ve JavaScript
  ile giriş değerini okuyun. Sorunsuz bir GridJs entegrasyonu için bu kapsamlı rehberi
  izleyin.
og_title: Seçili Hücre Adresini Al – Tam GridJs JavaScript Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: GridJs'de Seçili Hücre Adresini Al – Tam JavaScript Rehberi
url: /tr/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Seçili Hücre Adresini Al – Tam GridJs JavaScript Öğreticisi

Hiç GridJs tablosundan **seçili hücre adresini** almanız gerekti ama hangi API çağrısını kullanacağınızdan emin olmadınız mı? Tek başınıza değilsiniz. Birçok yönetim panelinde, kullanıcılar bir hücreye tıklar, bir modalda değeri düzenler ve ızgaranın değişikliği anında yansıtmasını bekler. Bu öğretici, o adresi nasıl alacağınızı, yeni fiyatı bir giriş alanından nasıl okuyacağınızı ve **ızgara hücre değerini** sayfa yenilemesi olmadan nasıl **güncelleyeceğinizi** tam olarak gösterir.

Ayrıca **JavaScript ile giriş değerini okuma** konusunu doğru şekilde ele alacağız, kenar durumlarını yönetecek ve güncelleme tamamlandığında modalı kapatacağız. Sonunda, GridJs kullanan herhangi bir projeye ekleyebileceğiniz bağımsız bir kod parçacığına sahip olacaksınız.

## Oluşturacağınız Şeyler

- GridJs tarafından desteklenen basit bir HTML tablo.
- Bir hücre tıklandığında ortaya çıkan düzenleme modalı.
- **Seçili hücre adresini alan**, kullanıcının girdiği fiyatı yakalayan, **ızgara hücre değerini güncelleyen** ve sonunda modalı gizleyen JavaScript.

Harici bir kütüphane gerekmez; kod modern tarayıcılarda (Chrome 102+, Edge, Firefox) çalışır. Sayfada zaten bir GridJs örneği varsa, ilgili bölümleri doğrudan kopyalayıp yapıştırabilirsiniz.

## Önkoşullar

- JavaScript ve DOM hakkında temel bilgi.
- GridJs kütüphanesinin yüklü olması (CDN veya npm üzerinden).
- Sayfada bir GridJs ızgarasının zaten render edilmiş olması (minimal bir örnek göstereceğiz).

Bu konulardan herhangi biri size yabancı geliyorsa, panik yapmayın—her adımda kısa bir özet bulunuyor.

---

## Adım 1: HTML İskeletini Oluşturun

İlk olarak tablo konteynerini, gizli modalı ve fiyat girişini yerleştirin. Modal, basit CSS sınıflarıyla gösterilip gizlenecek.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro ipucu:** `#editModal` minimal bir CSS hilesi kullanır—görünür kılmak için sadece `active` sınıfını ekleyin. Bunu Bootstrap, Tailwind veya zaten kullandığınız herhangi bir modal bileşeniyle değiştirebilirsiniz.

---

## Adım 2: GridJs’i Başlatın ve Hücre Tıklamalarını Yakalayın

Şimdi örnek verilerle bir ızgara oluşturacağız ve hücre seçimlerini dinleyeceğiz. Kullanıcı bir hücreye tıkladığında **seçili hücre adresini alacağız** ve modalı açacağız.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Neden işe yarıyor:** `GridJs.getSelectedCell()` `"C2"` (sütun C, satır 2) gibi bir dize döndürür. Bu değeri `lastSelectedCell` içinde saklamak, daha sonra **ızgara hücre değerini güncelleme** sırasında tam konuma başvurabilmemizi sağlar.

---

## Adım 3: Giriş Alanından Yeni Fiyatı Okuyun

Kullanıcı **Kaydet** butonuna tıkladığında, **JavaScript ile giriş değerini okuma** işlemini güvenli bir şekilde yapmamız gerekir. Bu adım aynı zamanda girilen fiyatın pozitif bir sayı olduğunun doğrulamasını da içerir.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Not:** `parseFloat` kullanmak ondalık sayıları (ör. `1.99`) kabul etmemizi sağlar. `isNaN` kontrolü, boş gönderimleri engeller.

---

## Adım 4: Seçili Hücre Değerini Güncelleyin

Şimdi, daha önce yakaladığımız adresi kullanarak **ızgara hücre değerini güncelleyeceğiz**. GridJs’in `updateCell` metodu bir promise döndürdüğü için, modal kapatma işlemini zincirleyebiliriz.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Neden bir promise kullanıyoruz?** GridJs tabloyu yeniden render etme veya bir backend ile senkronize olma ihtiyacı duyabilir. Promise’i bekleyerek, UI yalnızca grid yeni değeri yansıtınca gizlenir.

---

## Adım 5: İptal ve Kenar Durumlarını Yönetme

Sağlam bir çözüm her zaman kullanıcıya bir çıkış yolu sunar. **İptal** butonu sadece modalı gizler ve saklanan adresi temizler.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Hiç Hücre Seçilmemişse Ne Olur?

Kullanıcı, hücreye tıklamadan **Kaydet** butonuna (ör. modalı programatik olarak açtıysa) basarsa, `lastSelectedCell` `null` olur. `updateSelectedCell` içindeki erken dönüş, çalışma zamanı hatasını önler ve faydalı bir uyarı kaydeder.

### Büyük Izgaralarla Çalışmak

Sayfalama kullanılan ızgaralarda, `GridJs.getSelectedCell()` hâlâ mutlak adresi (ör. `"B12"`), sadece görünen satırı değil, döndürür. Bu sayede güncelleme, düzenlenen satır başka bir sayfada olsa bile çalışır. Ancak UI otomatik olarak sayfayı değiştirmez—eğer buna ihtiyacınız varsa `grid.forceUpdate()` çağırabilir veya ilgili sayfaya manuel olarak geçebilirsiniz.

---

## Tam Çalışan Örnek

Aşağıda tek bir HTML dosyasına kopyalayıp yapıştırabileceğiniz tam kod bulunuyor. Tarayıcıda açın, herhangi bir hücreye tıklayın, fiyatı değiştirin ve ızgaranın anında güncellendiğini izleyin.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Tam Excel Aralığı için Adres, Hücre Sayısı ve Ofseti Al](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Tam Excel Aralığı için Adres, Hücre Sayısı ve Ofseti Al (Almanca)](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Tam Excel Aralığı için Adres, Hücre Sayısı ve Ofseti Al (Fransızca)](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}