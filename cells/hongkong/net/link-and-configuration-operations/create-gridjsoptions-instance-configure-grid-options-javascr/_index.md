---
category: general
date: 2026-05-30
description: 學習如何建立 GridJsOptions 實例並配置動態表格的 JavaScript 網格選項。一步一步的完整程式碼指南。
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: zh-hant
og_description: 在幾分鐘內建立 GridJsOptions 實例並設定 Grid 選項的 JavaScript。完整範例、說明與最佳實踐技巧。
og_title: 建立 GridJsOptions 實例 – 設定 Grid Options JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: 建立 GridJsOptions 實例 – 設定 Grid Options JavaScript
url: /zh-hant/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 GridJsOptions 實例 – 設定 Grid Options JavaScript

有沒有想過如何 **create GridJsOptions instance** 而不必在零散的文件中搜尋？你並不是唯一有此困惑的人。當你需要在網頁上呈現一個流暢、可排序的表格時，掌握如何 configure grid options JavaScript 是打造精緻使用者介面的第一步。

在本教學中，我們將逐步說明你需要的完整程式碼，解釋每個設定為何重要，並展示一個可直接執行的範例。完成後，你將能輕鬆 create GridJsOptions instance，調整對齊、分頁，甚至自訂儲存格渲染器——全部使用純 JavaScript。

## 你將學會

- 如何從頭 **create GridJsOptions instance**。
- 讓你 **configure grid options JavaScript** 的關鍵屬性（排序、分頁、數字格式化等）。
- 常見陷阱（例如混用字串與數值類型）以及如何避免。
- 一個完整的 HTML 頁面，你可以直接 copy‑paste 到任何專案並即時看到結果。

### 前置條件

- 現代瀏覽器（Chrome、Edge、Firefox）——不需要建置工具。
- 基本的 JavaScript 知識（變數、物件、DOM）。
- Grid.js 函式庫（我們會從 CDN 載入）。

---

## Step 1: Load Grid.js and Prepare the HTML Skeleton

在我們能 **create GridJsOptions instance** 之前，需要先取得函式庫本身。最簡單的方式是使用官方 CDN。以下是一個最小的 HTML 骨架，同時保留了一個 `<div>` 作為 Grid 的渲染位置。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **專業提示：** 請將 CSS 連結放在自訂樣式之前，以確保 Grid 的預設主題正確載入。

### 為什麼這很重要

從 CDN 載入函式庫可確保你始終取得最新的穩定版本，且不需本機安裝。`<div id="grid-wrapper">` 是 Grid.js 建構子在 **configure grid options JavaScript** 後會目標的佔位元素。

## Step 2: Create a New GridJsOptions Instance

現在進入教學的核心：實際 **creates GridJsOptions instance** 的那一行程式碼。在 HTML 中引用的 `grid-config.js` 檔案裡，我們會寫下：

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

這一行程式碼會產生一個乾淨的物件，你可以開始填入設定。把 `gridOptions` 想成是未來所有功能的控制面板。

### 你正在設定的項目

- **NumberFormatAlignment** – 自動對齊數字字串。
- **Pagination** – 控制每頁筆數與導覽。
- **Sorting** – 開關欄位排序功能。
- **Columns** – 定義標題、資料類型與自訂渲染器。

你可以在最終實例化 Grid 之前加入任何這些屬性。

## Step 3: Enable Number Alignment (A Common Requirement)

大多數表格同時包含文字與數字。預設情況下 Grid.js 會把所有內容左對齊，對於金額等數值顯得不自然。要 **configure grid options JavaScript** 以取得正確的對齊方式，只需設定 `NumberFormatAlignment` 旗標：

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

為什麼要開啟這個功能？當旗標為 true 時，Grid.js 會檢查每個儲存格；若看起來像數字（例如 “1234”、 “12.34%”），就會自動右對齊。這個小調整能讓報表的可讀性大幅提升。

## Step 4: Add Pagination and Sorting

實務上，資料表很少能一次顯示在單一畫面。讓我們開啟分頁（每頁 10 筆）並允許使用者對任意欄位排序。

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### 邊緣案例說明

如果之後你提供的自訂資料來源已自行分頁，則應停用 Grid.js 內建的分頁功能，以免出現雙重分頁。只要將 `gridOptions.Pagination.enabled = false;` 即可。

## Step 5: Define Columns and Sample Data

現在我們要為 Grid 注入一些模擬資料，並說明每個欄位代表什麼。這正是 **create gridjsoptions instance** 模式發揮威力的地方——所有設定都集中在同一個物件內。

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

請注意，我們讓欄位的 `id` 值與每筆資料物件的鍵名保持一致。這個慣例讓 Grid.js 能自動對應值，省去為每個欄位寫自訂格式化程式的麻煩。

## Step 6: Instantiate the Grid with Our Options

最後，我們透過將 `gridOptions` 物件傳入 Grid 建構子來 **configure grid options javascript**。Grid 會在先前準備好的 `<div id="grid-wrapper">` 中渲染。

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

就這樣。從 **create gridjsoptions instance** 到渲染的完整流程，只需要不到一分鐘的程式碼撰寫。

### 預期結果

在瀏覽器開啟 HTML 檔案時，你應該會看到：

- 標題列顯示 “ID”、 “Employee”、 “Salary ($)”、 “Dept.”。
- 薪資數字右對齊（感謝 `NumberFormatAlignment`）。
- 底部出現分頁控制（若資料超過十列）。
- 可點擊的欄位標題，可切換升冪/降冪排序。

如果畫面有異常，請開啟瀏覽器主控台（F12）查看錯誤訊息——大多數問題來自欄位 ID 不匹配或缺少函式庫腳本。

## Step 7: Advanced Tweaks (Optional)

以下提供幾個快速的進階想法，等基本 Grid 正常運作後可以自行實驗。

| 功能 | 如何啟用 | 為何有幫助 |
|---------|---------------|--------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | 讓薪資以粗體顯示。 |
| **Search bar** | `gridOptions.Search = true;` | 讓使用者即時過濾列。 |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | 可支援上千筆資料的規模。 |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | 符合深色模式設計。 |

盡情混搭——Grid.js 本身設計得相當彈性。只要記得保留最上方的 **create gridjsoptions instance** 那一行，之後的所有調整都會以同一個物件為基礎。

## Conclusion

我們剛剛完整示範了如何 **create GridJsOptions instance** 以及 **configure grid options JavaScript**，打造一個功能完整、可排序且具分頁的資料表。從純 HTML 頁面開始，我們載入函式庫、建立選項物件、啟用數字對齊、加入分頁、定義欄位，最後渲染 Grid。

接下來你可以：

- 用 AJAX 呼叫取代靜態的 `sampleData`。
- 為日期、貨幣或圖示加入自訂格式化器。
- 將 Grid 整合至 React 或 Vue 等框架（相同的 `gridOptions` 物件同樣適用）。

可能性幾乎無限，而我們採用的模式——將所有設定集中於單一 `GridJsOptions` 實例——讓程式碼保持乾淨且易於維護。

有任何使用情境不確定嗎？留下評論，我們一起探索。祝程式開發愉快，盡情使用 Grid.js 建構動態表格吧！

## What Should You Learn Next?

- [如何使用 Aspose.Cells .NET 建立與設定 Excel 活頁簿：逐步指南](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 建立與樣式化 Excel 表格 | 逐步指南](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [如何使用 Aspose.Cells for Java 建立與格式化 Excel 儲存格：逐步指南](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}