---
category: general
date: 2026-06-30
description: 如何輕鬆建立 gridjs，並提供完整的 JavaScript 範例，涵蓋 gridjs 設定、容器設定及渲染流程。
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: zh-hant
og_description: 如何輕鬆使用完整的 JavaScript 範例建立 gridjs，涵蓋 gridjs 設定、容器配置及渲染過程。
og_title: 如何建立 Gridjs – 完整的 JavaScript 網格指南
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
title: 如何建立 Gridjs – 完整的 JavaScript 網格指南
url: /zh-hant/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何建立 Gridjs – 完整的 JavaScript Grid 指南

有沒有想過 **how to create gridjs**，並立即在頁面上看到一個流暢的資料表格？你並不是唯一有此疑問的人。許多開發者在首次嘗試設定 Gridjs 時，尤其是在 configuration 物件和 render 呼叫上卡住了。好消息是？只要掌握正確步驟，這其實非常簡單。

在本教學中，我們將逐步示範一個實務範例，說明如何從頭開始 **how to create gridjs**、如何打造正確的 **gridjs configuration**、如何將 grid 綁定至 **gridjs container**，最後如何觸發 **gridjs render**。完成後，你將擁有一個可直接嵌入任何專案的完整功能 grid——沒有神祕，只剩清晰的程式碼。

## 你將學會

- 設定一個最小化的 HTML 頁面以使用 Gridjs。
- 撰寫一個定義欄位、資料與選項的 **gridjs configuration** 物件。
- 將 Gridjs 實例附加到 **gridjs container** 元素。
- 呼叫 **gridjs render** 以顯示表格。
- 微調常見設定（分頁、排序、樣式），並避免常見陷阱。

不需要任何外部建置工具；所有程式碼皆在瀏覽器中以單一 script 標籤執行。讓我們開始吧。

## 前置條件

在深入之前，請確保你已具備以下條件：

1. 一個現代瀏覽器（Chrome、Edge、Firefox、Safari）— 任何支援 ES6 的瀏覽器。
2. 基本的 HTML 與 JavaScript 知識 — 不需要任何框架。
3. 取得 Gridjs 函式庫 — 我們會從 CDN 載入，無需 npm 安裝。

就這樣。如果你已經有想要增強的頁面，只要直接貼上程式碼片段即可。

## 步驟 1：將 Gridjs 資源加入你的頁面

首先，我們需要載入 Gridjs 的 CSS 與 JavaScript 檔案。CDN 版輕量且非常適合快速示範。

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

> **Pro tip:** Mermaid 主題讓表格呈現乾淨、現代的外觀，且不需額外 CSS。若你偏好其他樣式，可自行換成 `classic.min.css`。

## 步驟 2：定義 **gridjs container**

**gridjs container** 只是一個普通的 `<div>`，用來容納渲染後的表格。在上述標記中，我們已建立 `<div id="grid"></div>`。`id` 屬性相當重要，因為稍後我們會使用它來綁定 Gridjs 實例。

若同一頁面需要多個 grid，請為每個容器指定唯一的 ID（`grid1`、`grid2`，…），並為每個容器重複綁定程式碼。

## 步驟 3：打造 **gridjs configuration** 物件

現在進入 **how to create gridjs** 的核心——configuration。這個純 JavaScript 物件告訴 Gridjs 要顯示哪些欄位、填入什麼資料，以及啟用哪些功能。

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

### 為何此 configuration 重要

- **Columns** – 定義表頭文字與可選的寬度。若不設定，Gridjs 會從第一筆資料列推斷欄位名稱，通常可讀性較差。
- **Data** – 包含多筆列的陣列，每列為儲存格值的陣列。你也可以提供一個非同步函式從 API 抓取資料；函式庫會自動處理 Promise。
- **Pagination** – 限制每頁顯示的列數，避免大型表格淹沒使用者介面。
- **Search & Sort** – 只需一個布林值即可開啟互動功能，省去自行撰寫處理程式。
- **Language** – 自訂 UI 文字，適合本地化或品牌化。

之後若想改用 fetch 呼叫取代靜態資料陣列，其他步驟皆保持不變，請自行替換即可。

## 步驟 4：實例化 Gridjs 並綁定至 **gridjs container**

配置完成後，我們建立一個新的 `GridJs.Grid`（在 UMD 版中類別名稱為 `gridjs.Grid`），並指向我們的容器元素。

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

請注意我們使用了 `document.getElementById('grid')`——這就是先前定義的 **gridjs container**。若有多個容器，只需以相應的 ID 重複此行程式碼。

## 步驟 5：觸發 **gridjs render** 呼叫

最後一步是 **gridjs render** 方法。它會使用先前傳入的 configuration，並在容器內注入一個完整樣式的 `<table>`。

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

就這樣！當你在瀏覽器開啟此頁面時，會看到一個可搜尋、分頁的表格，內含我們定義的四筆資料。搜尋框會自動出現在上方，分頁控制則位於下方。

### 預期輸出

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

當你在搜尋框輸入文字或點擊欄位標題排序時，介面會即時更新。

## 常見變化與邊緣情況

### 非同步載入資料

如果資料位於伺服器上，請將靜態的 `data` 陣列改為回傳 Promise 的函式：

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

Gridjs 會在 Promise 解決前顯示載入中旋轉圖示，之後自動渲染表格。

### 自訂儲存格渲染

有時候需要在儲存格內放置圖示、按鈕或格式化日期。可於欄位上使用 `formatter` 屬性：

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

`gridjs.h` 輔助函式會建立虛擬 DOM 元素，且不需要引入 React。

### 同頁多個 Grid

只要使用不同的容器 ID，重複步驟 2‑5 即可：

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

每個 grid 都是獨立運作，你可以混合不同的分頁限制、欄位組合，甚至主題。

## 專業提示與避免的陷阱

- **Don’t forget the CSS** – 若未載入樣式表，表格將只顯示為普通的 HTML 表格，失去所有美觀樣式與分頁控制。
- **Avoid duplicate IDs** – 每個 **gridjs container** 必須有唯一的 ID；否則 Gridjs 會覆寫第一個實例。
- **Watch the data shape** – 欄位數量必須與每列儲存格數量相符；不匹配的陣列會導致隱蔽的版面錯誤。
- **Use `gridjs.h` for complex cells** – 嘗試直接注入原始 HTML 字串可能會破壞虛擬 DOM 的 diff 演算法。
- **Mind the version** – 上述 CDN 連結指向最新的 5.x 版（截至 2026 年 6 月）。若鎖定較舊版本，某些選項（如 `language`）可能不存在。

## 完整範例（直接複製貼上）

以下是完整的 HTML 檔案，你可以將其儲存為 `gridjs-demo.html`，直接在瀏覽器開啟。



## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎延伸技術。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [Aspose.Cells for Java：高效建立與格式化 Excel 活頁簿](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [使用 Aspose.Cells Java 建立並匯出 Excel 為 HTML | 活頁簿操作指南](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [使用 Aspose.Cells for Java 建立與合併 Excel 活頁簿 | 完整指南](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}