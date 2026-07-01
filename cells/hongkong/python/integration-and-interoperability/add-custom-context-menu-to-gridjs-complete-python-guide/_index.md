---
category: general
date: 2026-06-30
description: 在 GridJs 中新增自訂右鍵功能表，並了解如何載入 Excel 活頁簿、更新儲存格值、啟用拼寫檢查以及註冊自訂指令。
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: zh-hant
og_description: 在 GridJs 中新增自訂右鍵功能表，同時學習載入 Excel 工作簿、更新儲存格值、啟用拼字檢查，並註冊自訂指令。
og_title: 在 GridJs 中加入自訂右鍵功能表 – Python 步驟教學
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: 為 GridJs 添加自訂右鍵選單 – 完整 Python 指南
url: /zh-hant/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 為 GridJs 新增自訂右鍵功能表 – 完整 Python 教學

有沒有想過要 **為 GridJs 表格**（其資料來源是 Excel 活頁簿）加入自訂右鍵功能表項目？你並不孤單。在許多資料密集的應用程式中，需要透過右鍵選單讓使用者標記列、將項目標記為已審核，或啟動伺服器端動作——而不必離開表格。

在本教學中，我們將示範如何載入 Excel 活頁簿、為右鍵功能表加入自訂項目、更新儲存格值、啟用拼字檢查，並註冊自訂指令以將變更寫回檔案。完成後，你將擁有一個功能完整、使用者感受原生的 GridJs 實例，且能直接寫回來源試算表。

## 前置條件

- Python 3.9+（程式碼使用型別提示，但在任何近期版本皆可執行）  
- `cells` 套件（或任何提供 `Workbook` 與 `Worksheet` 物件的 Excel 包裝器）  
- `gridjs` Python 綁定（其物件模型與 JavaScript API 相同）  
- 具備基本的 lambda 與 JSON 結構概念  

如果你已具備上述條件，讓我們開始吧。

## 步驟 1：載入 Excel 活頁簿並選取工作表

首先必須 **載入 Excel 活頁簿**，讓 GridJs 有資料可顯示。`cells.Workbook` 類別會抽象檔案 I/O，並直接提供列、欄與儲存格的存取。

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **為什麼重要：** 事先載入活頁簿意味著格線可以按需取得資料，之後的任何編輯（例如 **更新儲存格值**）都會持續寫回同一檔案。

## 步驟 2：建立 GridJs 實例並綁定至工作表

接下來建立 `gridjs.GridJs` 物件，並告訴它要渲染哪一個工作表。這相當於給 GridJs 一個即時資料來源，讓它在需要渲染頁面或延遲載入區塊時隨時查詢。

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **小技巧：** 若你同時使用多個工作表，只要稍後呼叫 `grid.set_worksheet(other_ws)` 即可——不必重新建立格線。

## 步驟 3：啟用拼字檢查（以及其他便利功能）

大多數商業應用允許使用者輸入自由文字。啟用 **拼字檢查** 能減少錯別字並提升資料品質。GridJs 為此提供簡單的旗標。

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **為什麼要啟用拼字檢查？** 它在客戶端執行，立即回饋而不需額外的伺服器呼叫——非常適合大規模試算表。

## 步驟 4：新增自訂右鍵功能表項目

以下是本教學的核心：**新增自訂右鍵功能表** 項目。我們會建立一個「標記為已審核」的選項，點擊後會執行稍後定義的伺服器端指令。

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **圖片說明**  
> ![新增自訂右鍵功能表的螢幕截圖，顯示右鍵選項](/images/add-custom-context-menu.png "新增自訂右鍵功能表範例")

上方的 alt 文字包含主要關鍵字，符合 SEO 要求。

## 步驟 5：註冊自訂指令以更新儲存格值

當使用者選取「標記為已審核」時，我們需要 **註冊自訂指令**，將底層 Excel 儲存格更新並儲存檔案。`grid.register_custom_command` 方法會將 Python 可呼叫函式綁定至先前設定的動作識別碼。

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **為什麼會有效：** 處理函式會從客戶端取得儲存格參照，使用 `Worksheet` API **更新儲存格值**，然後將整個活頁簿寫回磁碟。回傳的結果讓前端知道操作已成功。

### 邊緣案例處理

- **缺少儲存格參照：** 若 `req` 中沒有 `"cell"`，拋出明確錯誤，讓 UI 能顯示 toast。  
- **同時編輯衝突：** 在高流量情境下，考慮對活頁簿加鎖或使用版本戳記，以避免競爭條件。

## 步驟 6：為大型試算表啟用延遲載入

若資料列數以千計，延遲載入可保持 UI 的流暢度。將每頁大小設為合理的區塊——500 列在大多數瀏覽器上表現良好。

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **如果有 10 000 列呢？** 格線會逐頁請求資料，減少客戶端與伺服器的記憶體壓力。

## 步驟 7：（可選）加入自訂 Modal 以編輯列

有時候需要比內嵌編輯器更豐富的 UI。GridJs 允許彈出 Modal 視窗，你可以在其中放置任意內容——例如 React 元件或簡易的 HTML 表單。

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **為什麼使用 Modal？** 它能將複雜的驗證邏輯隔離，讓你完整掌控版面配置，同時仍可從格線觸發。

## 步驟 8：取得客戶端設定 JSON

最後，需要將設定傳送至瀏覽器。`get_client_config` 方法會把所有設定序列化成 JSON，供前端 GridJs 程式庫使用。

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

輸出大致如下（為簡潔起見已裁切）：

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### 預期結果

- 右鍵點擊任意儲存格時會出現含 **標記為已審核** 的功能表。  
- 選取後會向伺服器發送請求，伺服器 **將儲存格值** 更新為 “Reviewed” 並儲存為 `example‑updated.xlsx`。  
- 拼字檢查會在使用者輸入時即時標示錯字。  

所有動作皆在不重新載入整頁的情況下完成，得益於延遲載入與輕量級 JSON 負載。

## 常見問題與進階小技巧

| 問題 | 解答 |
|----------|--------|
| *如果活頁簿是唯讀的怎麼辦？* | 確認檔案權限允許寫入，或在套件支援時以 `mode="rw"` 開啟活頁簿。 |
| *可以新增超過一個自訂功能表項目嗎？* | 當然可以——只要把額外的 dict 加入 `grid.settings.context_menu.custom_items` 即可。 |
| *儲存格更新後需要重新載入格線嗎？* | 若回傳 `{status:"ok"}`，GridJs 會自動刷新受影響的列；否則可在客戶端呼叫 `grid.refresh()`。 |
| *如何設定拼字檢查的語言？* | 設定 `grid.settings.spell_check.language = "en-US"`（或任何支援的語系）。 |
| *延遲載入能與伺服器端過濾相容嗎？* | 能——只要將 `grid.settings.filter.enabled = True` 並在自訂指令中實作過濾邏輯。 |

## 完整範例（結合所有步驟）

以下是一個可直接放入 Flask 路由或作為獨立程式執行的單一腳本。請將 `YOUR_DIRECTORY` 替換為伺服器上的實際路徑。

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## 接下來該學什麼？

以下教學與本指南所示技術密切相關，並提供完整的程式碼範例與逐步說明，協助你精通更多 API 功能，或在自己的專案中探索替代實作方式。

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}