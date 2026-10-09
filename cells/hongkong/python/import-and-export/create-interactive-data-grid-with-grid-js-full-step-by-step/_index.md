---
category: general
date: 2026-06-21
description: 使用 Grid.js 建立互動式資料格，學習如何顯示具排序、分頁與搜尋功能的 JSON 資料表。非常適合網頁儀表板。
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: zh-hant
og_description: 在數分鐘內建立互動式資料格。了解如何使用 Grid.js 顯示具備分頁、排序和搜尋功能的 JSON 資料表。
og_title: 使用 Grid.js 創建互動式資料格 – 完整教學
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
title: 使用 Grid.js 建立互動式資料格 – 完整逐步指南
url: /zh-hant/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Grid.js 建立互動式資料格 – 完整步驟指南

有沒有想過如何 **建立互動式資料格**，讓使用者在不寫後端的情況下就能排序、搜尋、分頁瀏覽資料列？你並不孤單。在許多儀表板中，最大的痛點是將靜態的 JSON 轉換成流暢、可搜尋的表格——感覺像試算表卻完全在瀏覽器中執行。

在本教學中，我們將逐步說明 **如何使用 Grid.js** 於純 HTML 頁面上 **顯示 JSON 資料表**。完成後，你將擁有一個可直接套用於任何專案的範例，並提供自訂工具列、處理大量資料以及避免常見陷阱的技巧。

## 你將學到什麼

- 如何取得定義欄位與列的 JSON 檔案。
- 如何以分頁、排序、搜尋以及自訂工具列來初始化 **Grid.js**。
- 如何將資料格渲染到目標容器中。
- 可選的調整：自訂儲存格格式、主題切換與錯誤處理。
- 完整、可直接複製貼上的程式碼範例。

### 前置條件

在開始之前，請確保你已具備：

1. 現代瀏覽器（Chrome、Edge 或 Firefox）— Grid.js 依賴 ES6 功能。
2. 含有 `grid_data.json` 檔案的本機或遠端資料夾（我們會示範格式）。
3. 基本的 HTML 與 JavaScript 知識 — 不需要高階技巧，只要能在瀏覽器開啟 `.html` 檔案。

不需要建置工具、npm 安裝或伺服器端程式碼。這就是使用 **create interactive data grid** 搭配 Grid.js 的好處：直接從 CDN 即可運作。

---

## 步驟 1：準備定義表格的 JSON

你首先需要一個 JSON 資料，告訴 Grid.js 哪些欄位存在以及要顯示哪些列。把它想像成你的 **display JSON data table** 的藍圖。以下是一個最小範例，可儲存為與 HTML 檔同目錄下的 `grid_data.json`：

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

*為什麼使用此格式？* Grid.js 期待 `columns` 為字串陣列（或用於進階設定的物件），`rows` 為陣列的陣列，且每個內部陣列的順序必須與欄位對應。當然，你可以加入更多欄位或巢狀物件——只要結構相符，Grid.js 都會正確渲染。

> **專業提示：** 若從 API 取得資料，只需將靜態的 `fetch('grid_data.json')` 換成你的端點 URL。其餘程式碼保持不變。

---

## 步驟 2：初始化 Grid.js – **how to use gridjs** 的核心

資料來源準備好後，我們需要將 Grid.js 載入頁面並告訴它如何運作。這裡就是實際 **create interactive data grid** 功能的地方，例如分頁、排序與便利的工具列按鈕。

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN 會提供最新的穩定版，且 Meri­maid 主題可直接呈現乾淨、現代的外觀。如果你偏好預設樣式，可改用 `gridjs.min.css`。

接著，在 `<script>` 標籤內，取得 JSON 並初始化資料格：

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

### 解析各項設定

| 選項 | 功能說明 | 重要性 |
|--------|--------------|----------------|
| `pagination` | 將列分割成多頁（預設每頁 10 筆） | 讓大型表格仍易於使用，不會讓介面負荷過重。 |
| `sort` | 可點擊的欄位標題切換升冪/降冪排序 | 使用者能快速找到最高值的列。 |
| `search` | 新增即時過濾列的文字輸入框 | 方便即時查詢，無需重新載入資料。 |
| `toolbar` | 在資料格上方加入自訂按鈕或下拉選單 | 適合「說明」「匯出」或「重新整理」等操作。 |
| `formatter` | 允許為儲存格回傳原始 HTML | 這裡我們將 email 文字轉成可點擊的 mailto 連結。 |

> **為什麼採用此方式？** 透過宣告式的資料格設定，你可以輕鬆調整行為，而不必觸碰核心渲染程式碼。這是大多數專案中 **how to use Grid.js** 的建議做法。

---

## 步驟 3：將資料格渲染到頁面上

腳本最後一行 `grid.render(document.getElementById('grid-container'))` 會將完整功能的表格注入你在 HTML body 任意位置放置的 `<div>` 中：

```html
<div id="grid-container"></div>
```

就這樣。頁面載入時，瀏覽器會取得 JSON，建立 Grid.js 實例，並在螢幕上繪製互動式表格。首次載入後不再需要重新整理或伺服器呼叫。

---

## 可選：樣式與主題微調

如果預設的 Meri­maid 主題不是你的菜，你可以改用任何內建主題（`gridjs.min.css`）或自行撰寫 CSS。例如，將表頭背景設為淡灰色：

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

將上述程式碼放入 `<style>` 標籤或外部樣式表中。Grid.js 會遵循標準 CSS 選擇器，讓你完整掌控字型、顏色與間距。

---

## 常見問題與避免方法

| 問題 | 徵兆 | 解決方法 |
|---------|---------|-----|
| **CORS 錯誤**（從其他網域取得 JSON 時） | 瀏覽器主控台顯示 “Blocked by CORS policy” | 將 JSON 放在相同來源，或在伺服器上啟用 CORS。 |
| **大量資料導致卡頓** | 捲動不順，分頁緩慢 | 使用 `server` 分頁（`pagination: { server: { url: (prev, page, limit) => … } }`）或延遲載入列。 |
| **工具列按鈕未顯示** | 即使 `toolbar.enabled: true` 仍看不到按鈕 | 確認使用 Grid.js 2.0 以上版本；舊版的工具列 API 不同。 |
| **Email 連結無法點擊** | Formatter 回傳純文字 | 如範例所示，回傳 `gridjs.html(...)` 而非純字串。 |

提前處理這些問題，可為你節省大量除錯時間。

---

## 完整範例（可直接複製貼上）

以下是完整的 HTML 檔案，可儲存為 `index.html`。在瀏覽器開啟後，你會看到一個完整功能的 **create interactive data grid** 示範，能 **display JSON data table**，具備排序、搜尋與說明按鈕。

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


## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在本篇示範的技巧之上。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 建立 Excel 資料驗證清單：步驟指南](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中建立核取方塊 | 資料驗證教學](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [使用 Aspose.Cells for Java 建立與匯入 XML 資料至 Excel](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}