---
category: general
date: 2026-07-03
description: Aspose Cells GridJs 教學示範如何使用延遲載入有效率地將 Excel 資料匯出為 JSON 以及將工作表匯出為 JSON。
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: zh-hant
og_description: Aspose Cells GridJs 教學說明如何將 Excel 資料匯出為 JSON，並將工作表匯出為 JSON，針對大型試算表採用懶加載。
og_title: Aspose Cells GridJs 教學 – 將 Excel 數據匯出為 JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Aspose Cells GridJs 教學 – 使用延遲載入將 Excel 資料匯出為 JSON
url: /zh-hant/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells GridJs 教學 – 使用延遲載入匯出 Excel 資料 JSON

有沒有想過要如何在不讓瀏覽器當機的情況下，從龐大的試算表 **export Excel data JSON**？在本篇 Aspose Cells GridJs 教學中，我們將一步步示範完整、可直接執行的解決方案，讓你透過 **export worksheet to JSON** 的延遲載入方式，只在需要時取得所需的列。

如果你一直在與巨大的 `.xlsx` 檔案掙扎，且客戶端總是卡住，你並不孤單。好消息是，我們在此介紹的方法既輕量又具可擴展性，且可以直接套用到已使用 Aspose.Cells 函式庫的任何 Python 專案中。

## 本指南涵蓋內容

在接下來的幾分鐘內，你將學會：

1. 使用 Aspose.Cells 載入大型活頁簿。
2. 開啟 GridJs 延遲載入，讓伺服器分批傳送列資料。
3. 將 GridJs 設定匯出為前端可使用的 JSON 檔案。
4. 調整分塊大小以取得最佳效能。
5. 驗證輸出結果並將其整合到簡易的 HTML 頁面。

不需要外部服務，也沒有隱藏的魔法——只有純粹的 Python 與 Aspose.Cells API。完成後，你將擁有一條 **complete export worksheet to JSON** 流程，能夠套用於儀表板、報表工具或任何資料格元件。

### 前置條件

- 本機已安裝 Python 3.8+。
- 已安裝 `asposecells` 套件（可使用 `pip install aspose-cells`）。
- 準備一個大型 Excel 檔案（例如 `large-data.xlsx`），放置於已知目錄。
- 具備基本的 Python 與 Web 開發概念。

若上述任一項你不熟悉，別慌——每一步都會附上簡短的「為什麼」說明，讓你了解背後的原理。

---

## 步驟 1：安裝並匯入 Aspose.Cells

首先，我們需要 Aspose.Cells 函式庫。它是商業產品，但免費試用版足以開發使用。

```bash
pip install aspose-cells
```

接著在腳本中匯入必要的類別。

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Why this matters:** Importing `Workbook` gives you access to the high‑performance engine that reads Excel files directly into memory, bypassing the slower `openpyxl` approach.

## 步驟 2：載入包含大量資料的活頁簿

函式庫就緒後，指向你的 Excel 檔案。路徑可以是絕對或相對，只要確保檔案確實存在即可。

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Pro tip:** If your workbook is larger than a few hundred megabytes, consider increasing the Python process memory limit or using a 64‑bit interpreter to avoid `MemoryError`.

## 步驟 3：啟用 GridJs 延遲載入

GridJs 是 Aspose 的 JavaScript 資料格元件。啟用延遲載入可讓伺服器只傳送部份列——這對巨量工作表而言是完美解決方案。

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Why lazy loading?** Without it, the entire worksheet would be serialized into JSON in one go, which can easily exceed browser memory limits. By setting `LazyLoadingChunkSize` to 500, each request carries a manageable payload.

## 步驟 4：將 GridJs 設定匯出為 JSON

現在請 Aspose 產生前端 GridJs 元件所需的 JSON，這也是 **export excel data json** 操作的核心。

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

`ExportGridJsJson` 方法會回傳一個 `bytes` 物件，內含工作表的 JSON 表示，可直接儲存或串流。

## 步驟 5：將 JSON 寫入檔案（或直接串流）

為了快速測試，我們先把 JSON 寫到磁碟。若在正式的 API 中，則可直接從 Flask/Django 端點回傳。

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **What you’ll see:** Opening `lazygrid.json` reveals a structure with `columns`, `rows`, and pagination metadata. The `rows` array will initially be empty; GridJs will request the first chunk when the page loads.

## 步驟 6：將 JSON 接入簡易 HTML 頁面（可選）

如果想要實際看到資料格的運作，建立一個小型 HTML 檔，從 CDN 載入 GridJs 並指向剛產生的 JSON。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Why include this?** It demonstrates the full round‑trip: Python creates the JSON, the browser pulls it, and GridJs renders the data chunk‑by‑chunk. You can now experiment with different `LazyLoadingChunkSize` values to find the sweet spot for your network.

## 步驟 7：驗證與除錯

執行 Python 腳本：

```bash
python export_lazy_grid.py
```

你應該會看到成功訊息與 `lazygrid.json` 檔案。於瀏覽器開啟 HTML 檔，資料格應立即顯示前 500 列，並提供分頁控制以載入更多。

如果資料格顯示為空：

- **Check the JSON file size** – a zero‑byte file usually means the workbook path was wrong.
- **Confirm lazy loading is enabled** – the `LazyLoading` flag must be `True`.
- **Inspect browser console** – any CORS or 404 errors indicate the JSON isn’t being served correctly.

---

## 常見變化與邊緣情況

### 匯出特定工作表

上例預設使用第一個工作表 (`Worksheets[0]`)。若要匯出其他工作表，只需更改索引或使用工作表名稱：

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### 調整大型檔案的分塊大小

對於擁有數百萬列的檔案，500 的分塊大小可能仍然太小，會產生過多的往返請求。你可以將其提升至 2000 或更高，但要記住較大的分塊會在每次請求時佔用更多頻寬。

```python
grid_options.LazyLoadingChunkSize = 2000
```

### 匯出至串流而非檔案

如果你的 API 直接回傳 JSON，則不需要寫入磁碟：

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### 處理公式與格式

預設情況下，`ExportGridJsJson` 會包含公式計算後的值。若需要原始公式，請設定：

```python
grid_options.ExportFormulas = True
```

---

## 結論

在本篇 **Aspose Cells GridJs 教學** 中，我們完整說明了如何使用延遲載入 **export Excel data JSON** 以及 **export worksheet to JSON**。從安裝 Aspose.Cells、啟用延遲載入、產生 JSON，到以簡易 HTML 頁面呈現，你現在已掌握一套能隨著巨量試算表平滑擴展的全端模式。

不妨試著調整分塊大小、切換不同工作表，或將端點整合至 Flask 或 Django 應用。可能性無限，效能提升立竿見影。

準備好進一步探索了嗎？試著加入欄位排序、自訂儲存格渲染，甚至伺服器端過濾，讓你的 GridJs 資料格真正互動。如果遇到問題，歡迎在下方留言，祝開發順利！

## 接下來該學什麼？

以下教學與本篇主題密切相關，能進一步延伸本指南中展示的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，或在專案中探索其他實作方式。

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}