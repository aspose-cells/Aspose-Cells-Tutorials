---
category: general
date: 2026-06-21
description: Metin kutusunun yazı tipini nasıl değiştireceğinizi, yazı tipi rengini
  programlı olarak nasıl ayarlayacağınızı ve bir ızgarada yazı tipi boyutu hücresini
  nasıl ayarlayacağınızı öğrenin. Metin kutularını stilize etmek için bu pratik öğreticiyi
  izleyin.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: tr
og_description: Bir ızgarada metin kutusu yazı tipini hızlıca değiştirin. Bu kılavuz,
  metin kutusunu nasıl stilize edeceğinizi, yazı tipi rengini programlı olarak nasıl
  ayarlayacağınızı ve net kodla hücre boyutunu nasıl ayarlayacağınızı gösterir.
og_title: Izgarada Metin Kutusu Yazı Tipini Değiştir – Tam Programlama Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: Izgara'da Metin Kutusu Yazı Tipini Değiştir – Tam Adım Adım Kılavuz
url: /tr/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bir Grid'de Metin Kutusu Yazı Tipini Değiştirme – Tam Adım‑Adım Kılavuz

Veri ızgarasında **metin kutusu yazı tipini** değiştirmeniz gerektiğinde ama hangi özelliği ayarlamanız gerektiğinden emin olmadığınız oldu mu? Yalnız değilsiniz—çoğu geliştirici, düzenlenebilir tablolar veya panolar oluştururken bu soruna takılır. Bu öğreticide, metin kutusu yazı tipini nasıl değiştireceğinizi, rengini programlı olarak nasıl ayarlayacağınızı ve hatta yazı tipi boyutunu hücre‑hücre nasıl ayarlayacağınızı adım adım göstereceğiz. Ayrıca **metin kutusunu nasıl stilize ederiz** öğeleri hakkında ipuçları ekleyecek, **hücrede yazı tipi boyutunu değiştirme** senaryolarını ele alacak ve **yazı tipi rengini programlı olarak ayarlama** konusunda saçınızı yolmadan nasıl yapacağınızı göstereceğiz. Sonunda, `getCell` API'sini sunan herhangi bir grid bileşeniyle çalışan yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Önkoşullar

- ES6 desteğine sahip modern bir tarayıcı (Chrome, Edge, Firefox, Safari)
- `grid.getCell(row, col)` sağlayan ve bir `textbox` referansı içeren bir hücre nesnesi döndüren bir grid kütüphanesi
- JavaScript nesneleri ve CSS özellikleri hakkında temel bilgi

Ek paket gerektirmez—sadece saf JavaScript ve grid'in kendi API'si.

## Çözümün Genel Bakışı

Temel fikir basit: hedef hücreyi al, içinde gömülü metin kutusunu yakala, ardından aile, boyut ve rengi tanımlayan yeni bir yazı tipi nesnesi ata. Bunu metin kutusuna yeni bir kıyafet vermek gibi düşün. Aşağıda yüksek‑seviye akış yer alıyor:

1. **Hedef hücreye eriş** – istediğiniz satır/sütunu bulun.
2. **Metin kutusunu al** – metni tutan UI öğesi.
3. **Yazı tipi stil nesnesi oluştur** – aile, boyut ve rengi belirt.
4. **Stili uygula** – nesneyi metin kutusunun `font` özelliğine ata.

Bu kadar. Şimdi her adıma dalalım, neden önemli olduğunu açıklayalım ve kodun nasıl çalıştığını görelim.

![Screenshot of a grid cell with a styled textbox – change textbox font](/images/change-textbox-font-example.png)

## Adım 1: Grid'de Hedef Hücreye Erişme

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Neden önemli:**  
> Izgaralar genellikle satır ve sütunları sıfır‑tabanlı indekslerle saklar. `grid.getCell(2, 3)` çağırarak **satır 2, sütun 3**'teki hücreyi alırız. Farklı bir konum için **hücrede yazı tipi boyutunu değiştirme** ihtiyacınız varsa, sadece indeksleri ayarlamanız yeterlidir.

**Pro ipucu:** Grid'iniz adlandırılmış sütunları destekliyorsa, sayısal sütunu bir anahtar ile değiştirebilirsiniz, ör. `grid.getCell(2, "price")`.

## Adım 2: O Hücrenin İçindeki Metin Kutusunu Yakala

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Ne oluyor:**  
> Çoğu grid uygulaması, düzenlenebilir içeriği bir `<input>` veya `<textarea>` öğesi içinde sarar ve bunu `cell.textbox` olarak sunar. Referansı alarak görsel stilini doğrudan manipüle edebiliriz.

Grid farklı bir özellik adı (ör. `cell.editor`) kullanıyorsa, kodu buna göre ayarlamanız yeterlidir—bu, özel bir bileşen için **metin kutusunu nasıl stilize ederiz** sorunda yaygın bir varyasyondur.

## Adım 3: İstenen Yazı Tipi Özelliklerini Tanımla

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Nesneyi Parçalarına Ayırma

| Özellik | Amaç | Örnek Değerler |
|----------|------|----------------|
| `family` | Yazı tipi ailesi – tipografi kontrol eder. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | Yazı tipi boyutu piksel (veya grid'e bağlı olarak puan) cinsinden. | `12`, `14`, `16` |
| `color`  | Metin rengi, herhangi bir CSS‑uyumlu formatta. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Neden bir nesne kullanıyoruz:**  
> Üç özelliği bir arada paketlemek kodu düzenli yapar ve birçok UI kütüphanesinin stil bilgisini bekleme şekline benzer. Ayrıca tek bir atama ile **grid'de yazı tipi ailesini değiştirme** veya **yazı tipi rengini programlı olarak ayarlama** yapmanızı sağlar.

## Adım 4: Yazı Tipi Stilini Metin Kutusuna Uygula

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Arka planda:**  
> Grid'in metin kutusu bileşeni `font` özelliğini yorumlar ve CSS'ini buna göre günceller. Bu tek satır, önceki yazı tipi ailesi, boyutu ve rengini bir anda değiştirir—çoklu hücrelerde **metin kutusu yazı tipini değiştirme** ihtiyacınız olduğunda tam da buna ihtiyacınız var.

**Eğer bileşen farklı bir API (ör. `textbox.style.fontFamily = ...`) kullanıyorsa, atamayı uyarlayın ancak aynı prensibi koruyun.**

## Tam Çalışan Örnek

Aşağıda, bir mock grid nesnesi içeren bir HTML dosyasına yapıştırabileceğiniz bağımsız bir kod parçacığı bulunuyor. Adım 1'den adım 4'e kadar tüm akışı ve stilin değiştiğini hızlı bir şekilde doğrulamayı gösterir.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Beklenen Çıktı

- **satır 2, sütun 3**'teki metin kutusu artık **Arial**, **14 px** ve **#0066CC** mavi tonunda metin gösterir.
- Tarayıcı konsolunu açtığınızda aşağıdaki gibi bir şey yazdırılır:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Sayfayı açarsanız, değişikliği görsel olarak teyit edersiniz—artık varsayılan sistem yazı tipine dönmez.

## Sıkça Sorulan Sorular (SSS)

### Sadece yazı tipi boyutunu, aileyi veya rengi etkilemeden değiştirebilir miyim?

Kesinlikle. Değiştirmek istemediğiniz özellikleri atlayın:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### Grid'im metin kutusu için farklı bir özellik adı kullanıyorsa ne olur?

Konsolda hücre nesnesini inceleyin (`console.log(cell)`). Muhtemelen `cell.editor` veya `cell.input` gibi bir şey göreceksiniz. `cell.textbox` ifadesini doğru referansla değiştirin.

### Aynı stili tüm bir sütuna nasıl uygularım?

Satırları döngüye alıp o sütundaki her hücrenin yazı tipini ayarlayın:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Orijinal yazı tipine geri dönmenin bir yolu var mı?

Üzerine yazmadan önce orijinal stili saklayın:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## İpuçları & En İyi Uygulamalar

- **Batch updates:** Çok sayıda hücreyi stilize etmeniz gerekiyorsa, değişiklikleri `requestAnimationFrame` içinde ya da layout çökmesini önlemek için grid‑özel bir toplu yöntemle sarın.
- **Responsive fonts:** UI'nizin ölçeklenmesi gerekiyorsa sabit piksel yerine göreceli birimler (`em`, `rem`) kullanın.
- **Accessibility:** **yazı tipi rengini programlı olarak ayarlama** yaparken yeterli kontrastı sağlayın—WCAG AA minimumu normal metin için 4.5:1 oranıdır.
- **Cross‑browser quirks:** Bazı eski grid'ler bir `font` nesnesi yerine `<input>` öğesine doğrudan `style.fontFamily` ayarlamayı gerektirebilir.

## Sonuç

Şimdi **grid içinde metin kutusu yazı tipini nasıl değiştiririz** konusunu, doğru hücreyi yakalamaktan yeniden kullanılabilir bir `fontStyle` nesnesi tanımlamaya ve tek satırda uygulamaya kadar ele aldık. Bu süreçte ayrıca **hücrede yazı tipi boyutunu değiştirme**, **yazı tipi rengini programlı olarak ayarlama** ve belirli bir sütun için **grid'de yazı tipi ailesini değiştirme** konularını da öğrendik.

Artık bu deseni alıp herhangi bir UI kütüphanesine uyarlayabilirsiniz—ister bir yönetim paneli, bir elektronik tablo benzeri editör, ister özel bir raporlama aracı geliştirin. Farklı aileler, boyutlar ve renklerle denemeler yapın; belki veri değerlerine göre hover efektleri veya koşullu stiller ekleyin.

Başka bir stil sorununuz mu var? Yorum bırakın, birlikte çözelim. Kodlamanın tadını çıkar!

## Sonra Ne Öğrenmelisin?

Bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Change Font Color in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}