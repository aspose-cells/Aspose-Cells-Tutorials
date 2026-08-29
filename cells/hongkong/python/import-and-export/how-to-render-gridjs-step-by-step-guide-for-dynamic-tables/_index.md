---
category: general
date: 2026-07-03
description: 學習如何在幾分鐘內渲染 Gridjs，提供完整的 HTML/JS 範例。內含 Gridjs 函式庫 CDN、懶載入與設定 JSON 小技巧。
draft: false
keywords:
- how to render gridjs
- gridjs configuration JSON
- gridjs lazy loading
- gridjs library CDN
- gridjs render method
language: zh-hant
og_description: 快速渲染 Gridjs：使用 CDN，取得設定 JSON，然後呼叫 render 方法。非常適合動態資料表。
og_title: 如何渲染 Gridjs – 完整實作指南
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  headline: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  type: TechArticle
- description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  name: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  steps:
  - name: Why Use the CDN?
    text: '- **Performance:** Browsers cache the file across sites, so returning visitors
      may already have it. - **Simplicity:** No bundler configuration, just a single
      `<script>` tag. - **Lazy loading:** You can defer the script with `defer` or
      load it only when needed, which ties into our next step.'
  - name: Breaking Down the Code
    text: '| Line | What It Does | Why It Matters | |------|--------------|----------------|
      | `fetch(''YOUR_DIRECTORY/lazygrid.json'')` | Retrieves the configuration JSON
      via HTTP GET. | Keeps the HTML clean and allows you to change the grid layout
      without touching the page code. | | `.then(response => response'
  - name: Sample `lazygrid.json`
    text: Below is a minimal yet functional configuration file. Save it as `lazygrid.json`
      in the same directory as your HTML (or adjust the fetch path accordingly).
  - name: 1. Using Custom Render Functions
    text: 'Sometimes you need to format a cell—say, add a badge for ages over 28.
      Extend the column definition:'
  - name: 2. Server‑Side Pagination
    text: If your dataset is huge, fetching the entire JSON can be slow. Gridjs supports
      server‑side pagination—just set `pagination.server` to `true` and implement
      an API endpoint that returns slices of data based on `page` and `limit` query
      parameters.
  - name: 3. Styling with CSS Variables
    text: 'The Mermaid theme uses CSS variables for colors. Override them in a `<style>`
      block:'
  - name: 4. Accessibility Considerations
    text: Gridjs adds ARIA attributes automatically, but you can enhance keyboard
      navigation by ensuring your placeholder `<div>` is focusable (`tabindex="0"`).
      This helps screen‑reader users interact with the table.
  type: HowTo
tags:
- JavaScript
- Front‑end
- Data Tables
title: 如何渲染 Gridjs – 動態表格的逐步指南
url: /zh-hant/python/import-and-export/how-to-render-gridjs-step-by-step-guide-for-dynamic-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何渲染 Gridjs – 動態表格逐步指南

有沒有想過 **如何在純 HTML 頁面上渲染 Gridjs**，而不必引入龐大的框架？你並不孤單。許多開發者需要一個輕量、可排序的表格，能從 JSON 檔案取得資料，而 Gridjs 正好讓這件事變得輕而易舉。在本教學中，我們會一步步說明所有必須的程式碼，從載入 Gridjs CDN、懶載入設定 JSON，到最終呼叫 render 方法。

我們也會穿插一些最佳實踐小技巧——例如為什麼懶載入 Gridjs 設定可以提升頁面速度，以及如何結構化 JSON 讓 Gridjs render 方法順利運作。完成後，你將擁有一個可直接套用於任何專案的完整功能表格。

## 你將會建立的內容

- 一個從 CDN 取得 Gridjs 的最小 HTML 頁面  
- 一個 `lazygrid.json` 檔案，定義欄位、資料與可選插件  
- 一段 JavaScript，用來抓取 JSON、建立 Gridjs 實例，並渲染至佔位元素  

不需要建置工具、npm，只要純 HTML 加上一點原生 JS。非常適合靜態網站、文件入口或快速原型。

## 前置條件

- 基本的 HTML 與 JavaScript 知識（不需框架）  
- 能提供靜態檔案的 Web 伺服器或本機開發環境（例如 VS Code Live Server）  
- `lazygrid.json` 檔案已放置於瀏覽器可存取的位置  

如果你已符合以上條件，讓我們開始吧。

## 步驟 1：引入 Gridjs Library CDN

在頁面上取得 Gridjs 最快速的方式是從 CDN 引用其 UMD bundle。這樣就不需要 npm 安裝，教學也能保持輕量。

```html
<!-- Step 1: Include the Gridjs library -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
```

> **小技巧：** `theme/mermaid.min.css` 樣式表會提供乾淨、現代的外觀。若想換成其他風格，只要替換成其他主題即可。

### 為什麼使用 CDN？

- **效能：** 瀏覽器會在不同網站間快取此檔案，回訪的使用者可能已經有快取。  
- **簡易性：** 不需要 bundler 設定，只要一個 `<script>` 標籤即可。  
- **懶載入：** 你可以使用 `defer` 延遲載入腳本，或僅在需要時才載入，這也與下一步驟相呼應。

## 步驟 2：為 Grid 添加佔位元素

Gridjs 需要一個 DOM 節點來掛載表格。建立一個具有唯一 ID 的 `<div>`——這就是 Gridjs render 方法會注入表格標記的地方。

```html
<!-- Step 2: Placeholder where Gridjs will appear -->
<div id="grid"></div>
```

如果需要自訂寬度或外距，可以用 CSS 為此容器加上樣式。目前主題的預設樣式已足夠整齊。

## 步驟 3：載入 Gridjs 設定 JSON 並渲染 Grid

魔法就發生在這裡。我們會抓取一個 JSON 檔案（`lazygrid.json`），裡面描述欄位、資料列以及任何插件。接著以該設定建立 Gridjs 實例，最後呼叫 render 方法。

```html
<!-- Step 3: Fetch config and render Gridjs -->
<script>
  // Step 3.1: Pull the JSON config (replace the path as needed)
  fetch('YOUR_DIRECTORY/lazygrid.json')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(config => {
      // Step 3.2: Create a Gridjs instance using the fetched configuration
      const grid = new GridJs(config);
      // Step 3.3: Render the grid inside the placeholder element
      grid.render(document.getElementById('grid'));
    })
    .catch(error => console.error('Error loading Gridjs config:', error));
</script>
```

### 程式碼說明

| 行 | 功能說明 | 為什麼重要 |
|------|--------------|----------------|
| `fetch('YOUR_DIRECTORY/lazygrid.json')` | 以 HTTP GET 取得設定 JSON。 | 讓 HTML 保持乾淨，且可在不修改頁面程式碼的情況下變更表格布局。 |
| `.then(response => response.json())` | 將回應解析為 JavaScript 物件。 | 確保傳遞給 Gridjs 的是正確的物件。 |
| `new GridJs(config)` | 使用提供的設定建立 Gridjs 實例。 | 這是 **gridjs render method** 的入口點；設定決定欄位、資料與插件。 |
| `grid.render(document.getElementById('grid'))` | 把表格插入 `<div id="grid">` 中。 | 最終步驟，實際 **渲染 Gridjs** 到畫面上。 |
| `.catch(...)` | 優雅地處理網路或解析錯誤。 | 防止頁面靜默失效，並提供除錯資訊。 |

### 範例 `lazygrid.json`

以下是一個最小但可運作的設定檔。請將它存為 `lazygrid.json`，放在與 HTML 同一目錄（或依需求調整 fetch 路徑）。

```json
{
  "columns": [
    "Name",
    "Email",
    { "id": "age", "name": "Age", "type": "number" }
  ],
  "data": [
    ["Alice", "alice@example.com", 30],
    ["Bob", "bob@example.com", 25],
    ["Carol", "carol@example.com", 27]
  ],
  "search": true,
  "pagination": {
    "enabled": true,
    "limit": 5
  }
}
```

- **gridjs 設定 JSON**：`columns` 陣列可以是簡單字串，也可以是物件以取得更高控制（例如自訂渲染器）。  
- **gridjs 懶載入**：將此 JSON 分離存放，可在不重新部署 HTML 的情況下更換。  
- **gridjs render method**：`grid.render(...)` 會讀取此設定並動態建立表格。

## 步驟 4：驗證輸出

在瀏覽器開啟 HTML 檔案。你應該會看到一個可搜尋、分頁的表格，內容與 `lazygrid.json` 中的資料相符。預設的 Mermaid 主題會加入細緻的陰影與懸停效果。

**預期輸出：**

| 姓名  | 電子郵件               | 年齡 |
|-------|---------------------|------|
| Alice | alice@example.com   | 30   |
| Bob   | bob@example.com     | 25   |
| Carol | carol@example.com   | 27   |

如果看不到表格：

1. 開啟瀏覽器開發者工具（F12），檢查 console 錯誤。  
2. 確認 `fetch('YOUR_DIRECTORY/lazygrid.json')` 的路徑正確指向檔案位置。  
3. 確認 CDN 腳本已成功載入（檢查 Network 分頁）。  

## 進階技巧與邊緣案例

### 1. 使用自訂渲染函式

有時需要格式化儲存格——例如，年齡大於 28 歲時顯示徽章。可以在欄位定義中擴充：

```json
{
  "id": "age",
  "name": "Age",
  "formatter": (cell) => {
    return cell > 28 ? `<span style="color:red;">${cell}</span>` : cell;
  }
}
```

> **注意：** formatter 必須是 JavaScript 函式，因此若想保留在 JSON 中，需要直接在腳本內嵌入設定，或以模組方式載入。

### 2. 伺服器端分頁

若資料集龐大，一次抓取全部 JSON 會很慢。Gridjs 支援伺服器端分頁——只要將 `pagination.server` 設為 `true`，並實作一個根據 `page` 與 `limit` 參數回傳資料切片的 API。

### 3. 使用 CSS 變數自訂樣式

Mermaid 主題使用 CSS 變數定義顏色。可在 `<style>` 區塊中覆寫：

```html
<style>
  :root {
    --gridjs-header-bg: #2c3e50;
    --gridjs-header-color: #ecf0f1;
  }
</style>
```

### 4. 可及性考量

Gridjs 會自動加入 ARIA 屬性，但你可以透過讓佔位 `<div>` 可聚焦（`tabindex="0"`）來加強鍵盤導覽，讓使用螢幕閱讀器的使用者也能順利操作表格。

## 完整範例

把所有步驟整合起來，以下是一個可直接複製貼上、在本機執行的單一 HTML 檔案。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Render Gridjs Demo</title>
  <!-- Gridjs library CDN -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
  <style>
    /* Optional custom theme tweaks */
    :root {
      --gridjs-header-bg: #34495e;
      --gridjs-header-color: #ecf0f1;
    }
  </style>
</head>
<body>
  <!-- Placeholder for the grid -->
  <div id="grid"></div>

  <!-- Fetch config and render Gridjs -->
  <script>
    fetch('lazygrid.json')
      .then(r => r.ok ? r.json() : Promise.reject('Failed to load'))
      .then(cfg => {
        const grid = new GridJs(cfg);
        grid.render(document.getElementById('grid'));
      })
      .catch(err => console.error(err));
  </script>

  <!-- Optional screenshot for documentation -->
  <img src="gridjs-screenshot.png" alt="Screenshot demonstrating how to render Gridjs grid" style="display:none;">
</body>
</html>
```

將此檔案存為 `index.html`，與 `lazygrid.json` 放在同一資料夾，於瀏覽器開啟，即可即時看到表格呈現。

## 結論

現在你已掌握 **如何渲染 Gridjs**：載入 Gridjs CDN、提供 `gridjs configuration JSON`、懶載入該 JSON、建立 Gridjs 物件，最後呼叫 `gridjs render method`。此方式讓 HTML 保持簡潔、利用懶載入提升效能，且能完整掌控欄位、資料與插件。

接下來可以試試：

- **gridjs 懶載入** 大量資料，搭配伺服器端分頁。  
- 為儲存格自訂渲染器，顯示圖表或進度條。  
- 使用匯出插件，讓使用者下載 CSV 或 Excel 檔案。  

盡情實驗吧！若遇到任何問題，歡迎在下方留言。祝開發愉快！

## 接下來你可以學什麼？

以下教學與本指南緊密相關，能進一步延伸本篇示範的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並探索在專案中使用的其他實作方式。

- [How to Render Excel Sheets as Images Using Aspose.Cells .NET for Seamless Data Visualization](/cells/english/net/import-export/render-excel-sheets-images-aspose-cells-dotnet/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}