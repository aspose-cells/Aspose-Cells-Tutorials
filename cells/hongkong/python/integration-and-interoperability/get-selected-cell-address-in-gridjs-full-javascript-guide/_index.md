---
category: general
date: 2026-06-30
description: 學習如何取得選取的儲存格位址、更新格子值以及使用 JavaScript 透過 GridJs 讀取輸入值。一步一步的程式碼與技巧。
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: zh-hant
og_description: 取得已選取儲存格的位址、更新格子值並使用 JavaScript 讀取輸入值。遵循本完整指南，順利整合 GridJs。
og_title: 取得所選儲存格地址 – 完整 GridJs JavaScript 教學
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
title: 在 GridJs 中取得選取儲存格位址 – 完整 JavaScript 教學
url: /zh-hant/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 取得選取儲存格位址 – 完整 GridJs JavaScript 教學

是否曾需要從 GridJs 表格中 **取得選取儲存格位址**，卻不確定該使用哪個 API 呼叫？你並非唯一遇到此問題的人。在許多管理介面中，使用者點擊儲存格、在彈出視窗中編輯值，並期望表格立即顯示變更。本教學將完整示範如何取得該位址、從輸入欄位讀取新價格，並 **更新表格儲存格值** 而不需重新載入頁面。

我們也會說明 **使用 JavaScript 讀取輸入值** 的正確方式、處理例外情況，並在更新完成後關閉彈出視窗。完成後，你將擁有一段可直接嵌入任何使用 GridJs 的專案的完整程式碼片段。

## 你將建立的內容

- 一個由 GridJs 驅動的簡易 HTML 表格。
- 一個在點擊儲存格時顯示的編輯彈出視窗。
- JavaScript 程式碼，可 **取得選取儲存格位址**、抓取使用者輸入的價格、**更新表格儲存格值**，最後隱藏彈出視窗。

不需要除 GridJs 之外的其他外部函式庫，且程式碼相容於現代瀏覽器（Chrome 102+、Edge、Firefox）。如果頁面上已經有 GridJs 實例，你可以直接複製貼上相關程式碼。

## 前置條件

- 具備 JavaScript 與 DOM 的基本知識。
- 已載入 GridJs 函式庫（透過 CDN 或 npm）。
- 頁面已渲染 GridJs 表格（我們將示範最小範例）。

如果以上任一項你不熟悉，別擔心——每一步都會有簡短說明。

---

## 步驟 1：設定 HTML 骨架

首先，佈局表格容器、隱藏的彈出視窗以及價格輸入欄位。彈出視窗會透過簡單的 CSS 類別切換顯示。

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

> **小技巧：** `#editModal` 使用了最小化的 CSS 小技巧——只要加入 `active` 類別即可顯示。你可以將其替換為 Bootstrap、Tailwind，或任何你已在使用的彈出視窗元件。

---

## 步驟 2：初始化 GridJs 並捕捉儲存格點擊

現在我們將使用範例資料建立表格，並監聽儲存格的選取。當使用者點擊儲存格時，我們會 **取得選取儲存格位址** 並開啟彈出視窗。

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

> **為什麼這樣有效：** `GridJs.getSelectedCell()` 會回傳類似 `"C2"`（第 C 欄，第 2 列）的字串。將其存入 `lastSelectedCell`，讓我們在之後 **更新表格儲存格值** 時能精確定位。

---

## 步驟 3：從輸入欄位讀取新價格

當使用者點擊 **Save** 時，我們需要安全地 **使用 JavaScript 讀取輸入值**。此步驟同時會驗證輸入的價格是否為正數。

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

> **注意：** 使用 `parseFloat` 可接受小數（例如 `1.99`）。`isNaN` 檢查可防止意外的空白提交。

---

## 步驟 4：更新選取的儲存格值

現在我們終於使用先前捕捉的位址 **更新表格儲存格值**。GridJs 的 `updateCell` 方法會回傳 Promise，讓我們可以串接關閉彈出視窗的動作。

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

> **為什麼使用 Promise？** GridJs 可能需要重新渲染表格或與後端同步。等待 Promise 完成即可保證 UI 只在表格顯示新值後才隱藏。

---

## 步驟 5：處理取消與例外情況

穩健的解決方案總會提供使用者退出的方式。**Cancel** 按鈕只會隱藏彈出視窗並清除任何已儲存的位址。

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### 若未選取任何儲存格會怎樣？

如果使用者在未先點擊儲存格的情況下觸發 **Save** 按鈕（可能是程式化開啟彈出視窗），`lastSelectedCell` 會是 `null`。`updateSelectedCell` 中的提前返回可避免執行時錯誤，並在主控台記錄有用的警告。

### 處理大型表格

對於有分頁的表格，`GridJs.getSelectedCell()` 仍會回傳絕對位址（例如 `"B12"`），而非僅顯示的那一列。這表示即使編輯的列位於其他頁面，更新仍會生效。需注意的是，更新後 UI 不會自動切換頁面——若需要，可呼叫 `grid.forceUpdate()` 或手動導向至相應頁面。

---

## 完整可執行範例

以下是完整程式碼，可直接複製貼上至單一 HTML 檔案。於瀏覽器開啟後，點擊任意儲存格、修改價格，即可即時看到表格更新。



## 接下來你可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [取得整個 Excel 範圍的位址、儲存格數量與偏移量](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [取得整個 Excel 範圍的位址、儲存格數量與偏移量](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [取得整個 Excel 範圍的位址、儲存格數量與偏移量](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}