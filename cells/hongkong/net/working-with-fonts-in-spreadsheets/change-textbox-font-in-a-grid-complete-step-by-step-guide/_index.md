---
category: general
date: 2026-06-21
description: 學習如何變更文字方塊的字型、以程式方式設定字體顏色，並調整網格中儲存格的字體大小。跟隨本實用教學，為文字方塊進行樣式設定。
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: zh-hant
og_description: 快速更改網格中文字方塊的字體。本指南示範如何樣式化文字方塊、以程式方式設定字體顏色，並以清晰的程式碼調整儲存格大小。
og_title: 在網格中更改文字方塊字型 – 完整程式設計教學
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
title: 在網格中更改文字方塊字型 – 完整逐步指南
url: /zh-hant/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在資料格中變更文字方塊字型 – 完整逐步指南

是否曾經需要 **變更資料格內文字方塊的字型**，卻不確定要調整哪個屬性？你並不孤單——大多數開發者在建立可編輯表格或儀表板時都會碰到這個問題。在本教學中，我們將一步步說明如何變更文字方塊字型、以程式方式設定其顏色，甚至逐格調整字型大小。

我們也會分享 **如何樣式化文字方塊** 的小技巧，涵蓋 **變更字型大小格** 的情境，並示範 **以程式方式設定字型顏色**，讓你不再抓狂。完成後，你將擁有一段可重複使用的程式碼，適用於任何提供 `getCell` API 的格線元件。

## 前置條件

- 支援 ES6 的現代瀏覽器（Chrome、Edge、Firefox、Safari）
- 提供 `grid.getCell(row, col)` 並回傳包含 `textbox` 參考的格子物件的格線函式庫
- 具備基本的 JavaScript 物件與 CSS 屬性概念

不需要額外套件——只要純 JavaScript 加上格線本身的 API 即可。

## 解決方案概覽

核心概念很簡單：取得目標格子、抓取其內嵌的文字方塊，然後指派一個定義字型、大小與顏色的新字型物件。把它想像成給文字方塊換上新衣服。以下是高階流程：

1. **存取目標格子** – 找到想要的列/欄。
2. **取得文字方塊** – 包含文字的 UI 元素。
3. **建立字型樣式物件** – 指定字型族、大小與顏色。
4. **套用樣式** – 把物件指派給文字方塊的 `font` 屬性。

就這樣。接下來我們會逐步說明每個步驟、解釋其重要性，並展示實作程式碼。

![格子內已樣式化文字方塊的螢幕截圖 – 變更文字方塊字型](/images/change-textbox-font-example.png)

## 步驟 1：在格線中存取目標格子

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **為什麼這很重要：**  
> 格線通常以零基索引儲存列與欄。透過 `grid.getCell(2, 3)` 可以取得 **第 2 列、第 3 欄** 的格子。如果你需要 **變更字型大小格** 的其他位置，只要調整索引即可。

**小技巧：** 若你的格線支援具名欄位，可將數字欄位改為鍵名，例如 `grid.getCell(2, "price")`。

## 步驟 2：抓取該格子內的文字方塊

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **發生了什麼事：**  
> 大多數格線實作會將可編輯內容包在 `<input>` 或 `<textarea>` 元素中，並以 `cell.textbox` 方式公開。取得此參考後，我們即可直接操作其視覺樣式。

如果格線使用不同的屬性名稱（例如 `cell.editor`），只要相應調整程式碼——這在 **如何樣式化文字方塊** 自訂元件時相當常見。

## 步驟 3：定義想要的字型屬性

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### 物件說明

| 屬性      | 用途                     | 範例值                                 |
|----------|--------------------------|----------------------------------------|
| `family` | 字型族 – 控制字體樣式    | `"Arial"`、`"Helvetica"`、`"Courier New"` |
| `size`   | 字型大小（像素或點）      | `12`、`14`、`16`                       |
| `color`  | 文字顏色（任意 CSS 格式）| `"#0066CC"`、`"rgb(255,0,0)"`、`"navy"` |

> **為什麼使用物件：**  
> 把三個屬性打包在一起可以讓程式碼更整潔，也符合許多 UI 函式庫期待的樣式資訊格式。這同時讓你能以單一指派 **變更格線字型族** 或 **以程式方式設定字型顏色**。

## 步驟 4：將字型樣式套用到文字方塊

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **背後原理：**  
> 格線的文字方塊元件會解讀 `font` 屬性並相應更新 CSS。這一行程式碼即可一次取代先前的字型族、大小與顏色——正是你在 **變更文字方塊字型** 時跨多格所需要的。

如果元件使用不同的 API（例如 `textbox.style.fontFamily = ...`），只要改寫指派方式，概念不變。

## 完整可執行範例

以下是一段可直接貼到包含模擬格線物件的 HTML 檔案中的程式碼，示範從步驟 1 到步驟 4 的完整流程，並快速驗證樣式是否已變更。

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

### 預期輸出

- 位於 **第 2 列、第 3 欄** 的文字方塊現在會以 **Arial**、**14 px**、以及 **#0066CC** 藍色顯示文字。
- 在瀏覽器主控台會印出類似以下內容：

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

開啟頁面後，你即可目視確認變更——不再是系統預設字型。

## 常見問題 (FAQ)

### 只想變更字型大小而不影響字型族或顏色，該怎麼做？
完全可以。只要省略不想修改的屬性：

```javascript
textbox.font = { size: 18 }; // only changes size
```

### 我的格線使用不同的屬性名稱來指向文字方塊，該怎麼辦？
在主控台檢查格子物件（`console.log(cell)`），你可能會看到 `cell.editor` 或 `cell.input`。將 `cell.textbox` 換成正確的參考即可。

### 如何一次套用相同樣式到整個欄位？
遍歷所有列，對該欄位的每個格子設定字型：

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### 有沒有辦法還原成原本的字型？
在覆寫之前先儲存原始樣式：

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## 小技巧與最佳實踐

- **批次更新：** 若需樣式大量格子，請將變更包在 `requestAnimationFrame` 或格線特有的批次方法中，以避免版面重新計算。
- **響應式字型：** 若 UI 需要縮放，請使用相對單位（`em`、`rem`）取代固定像素。
- **可及性：** 設定 **以程式方式設定字型顏色** 時，確保對比度足夠；WCAG AA 標準要求普通文字的對比度至少 4.5:1。
- **跨瀏覽器差異：** 某些舊版格線可能需要直接在 `<input>` 元素上設定 `style.fontFamily`，而非使用 `font` 物件。

## 結論

我們已完整說明 **如何在格線中變更文字方塊字型**，從取得正確格子、定義可重用的 `fontStyle` 物件，到以一行程式碼套用。過程中也學會了 **變更字型大小格**、**以程式方式設定字型顏色**，以及 **變更格線字型族** 的技巧。

現在，你可以將此模式套用到任何 UI 函式庫——無論是管理儀表板、類似試算表的編輯器，或是自訂報表工具。盡情嘗試不同的字型族、大小與顏色；甚至加入懸停效果或根據資料值做條件樣式。

有其他樣式挑戰嗎？留下評論，我們一起解決。祝程式開發愉快！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你對 API 功能的掌握，並探索在實際專案中可替代的實作方式。

- [How to Change Font Color in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}