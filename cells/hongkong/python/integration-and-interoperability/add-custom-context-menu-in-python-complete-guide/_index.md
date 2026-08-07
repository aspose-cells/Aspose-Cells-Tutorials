---
category: general
date: 2026-06-30
description: 在 Python Excel 網格中加入自訂右鍵功能表，並在儲存更新後的檔案時寫入儲存格值。學習如何建立右鍵選單以及以 Python 方式更新儲存格的值。
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: zh-hant
og_description: 在 Python 中新增自訂功能表，以寫入值至 Excel 儲存格並儲存更新後的 Excel 檔案。本指南將一步步教您使用 GridJs
  建立右鍵功能表。
og_title: 在 Python 中新增自訂右鍵功能表 – 逐步教學
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: 在 Python 中加入自訂右鍵功能表 – 完整指南
url: /zh-hant/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中新增自訂右鍵功能表 – 完整指南

有沒有想過如何在由 Python 提供的試算表格子上 **add custom context menu** 項目？也許你需要一個快速的「Mark as Reviewed」按鈕，當使用者右鍵點擊儲存格時彈出，寫入值到 Excel 儲存格，然後儲存更新後的工作簿——全部在網頁介面內完成。  

在本教學中，我們將打造這個功能：由 GridJs 提供的 **custom right‑click menu**、一個在伺服器端寫入 Excel 儲存格的處理程式 **write(s) value to excel cell**，以及最後一步 **save(s) updated excel file** 到磁碟。完成後，你將擁有一套可重用的模式，能直接套用於任何 Flask、FastAPI 或 Django 專案。

> **Why care?**  
> 新增自訂右鍵功能表可簡化資料審核流程，減少手動複製貼上，並為最終使用者提供在格子內即時的原生體驗。此外，你還會看到如何以 **update cell value python** 方式更新儲存格，這是任何 Excel 自動化任務的核心技能。

## 前置條件

- Python 3.9+（程式碼在 3.10 亦可執行）  
- `openpyxl` 用於 Excel 檔案處理  
- `gridjs` Python 包裝器（或若你偏好前端則使用 JS 函式庫）  
- 基本的 Web 框架（此處示範 Flask）  
- 名為 `sample.xlsx` 的工作簿檔案，放在專案資料夾內  

如果缺少上述任一項，請執行：

```bash
pip install openpyxl flask gridjs
```

現在讓我們開始吧。

---

## 第一步 – 新增自訂右鍵功能表：初始化 GridJs 並綁定工作表

你需要做的第一件事是啟動一個 `GridJs` 實例，並指向你打算操作的工作表。這裡是 **add custom context menu** 在程式碼中首次出現的地方，也為後續所有操作奠定基礎。

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**發生了什麼？**  
`grid.set_worksheet(ws)` 告訴 GridJs 使用 `ws` 的資料作為資料來源。從此之後，我們加入的任何右鍵功能表修改都會自動針對同一工作表，確保 UI 與檔案同步。

> **Pro tip:** 請僅在一次性以讀寫模式開啟工作簿。於請求處理程序中重複開啟會導致 Windows 上的檔案鎖定問題。

## 第二步 – 寫入值到 Excel 儲存格：為功能表項目定義動作

現在格子已就緒，我們需要在使用者選取自訂指令時 **write value to excel cell**。我們會新增一個名為「Mark as Reviewed」的功能表項目，並給予識別碼 `markReviewed`。此識別碼會由客戶端 JavaScript 回傳給伺服器。

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**為什麼使用自訂識別碼？**  
識別碼將 UI 文字與伺服器邏輯解耦，使你可以在不修改後端程式碼的情況下變更標籤。它同時讓 **create right‑click menu** 操作變得明確且可重用。

## 第三步 – 建立右鍵功能表：註冊伺服器端處理程序

有了功能表項目後，我們需要告訴 GridJs 使用者點擊時該執行什麼。這裡就是實作 **create right‑click menu** 功能，實際向 Python 發送請求的地方。

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

需要注意的幾點：

1. **`ws[cell_address] = "Reviewed"`** 是最直接的 **update cell value python** 方法。底層上，`openpyxl` 會將 A1 形式的地址轉換為列/欄索引。  
2. 處理程序回傳一個小型 JSON 負載。GridJs 期待一個狀態指示；如有需要，你可以擴充以包含錯誤訊息。

現在將識別碼綁定至處理程序：

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**如果儲存格是空的或受保護呢？**  
- 空儲存格沒問題——`openpyxl` 會即時建立。  
- 若工作表受保護，需先解除保護 (`ws.protection.sheet = False`) 或捕捉 `PermissionError`。

## 第四步 – 更新儲存格值（Python）：透過儲存工作簿永久保存變更

寫入值只是故事的一半；你必須 **save updated excel file** 才能讓變更在目前會話之外持續存在。這裡完成了從 UI 到磁碟的完整回傳。

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**為什麼要使用獨立資料夾？**  
儲存至 `output/` 目錄可保持原始範本不被修改，對於稽核追蹤很有幫助。請依你的部署環境調整路徑。

> **Watch out:** 若同時服務多位使用者，建議在 `wb.save()` 周圍使用執行緒安全的鎖 (`threading.Lock`) 以避免競爭條件。

## 第五步 – 產生客戶端設定 JSON 並將所有元件串接起來

最後，我們需要產生前端 GridJs 實例會使用的 JSON。此 JSON 包含工作表資料 **以及** 自訂功能表的定義。

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

當你將 `config_json` 嵌入 HTML 頁面時，GridJs 會渲染格子，並在每個儲存格上提供可右鍵點擊的「Mark as Reviewed」項目。

### 完整 Flask 範例

以下是一個最小化的 Flask 應用程式，將所有部件組合起來。執行後，開啟 `http://localhost:5000`，右鍵任意儲存格即可看到自訂功能表的運作。

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**預期結果：**  
- 右鍵任意儲存格 → 出現「Mark as Reviewed」。  
- 點擊它 → 該儲存格內容變為「Reviewed」。  
- 工作簿 `output/sample-updated.xlsx` 現在已包含新值。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *如果需要多個自訂動作怎麼辦？* | 只需在 `grid.settings.context_menu.custom_items` 中加入更多物件，並為每個物件註冊其識別碼。 |
| *我可以傳遞額外資料（例如列 ID）給處理程序嗎？* | 可以。於客戶端的 JSON 負載中加入額外鍵，然後在 `on_custom_command` 中從 `request` 讀取。 |
| *此方法能與非同步框架相容嗎？* | 完全相容——只要將 `on_custom_command` 定義為 async 函式，若改用 `aiofiles` 等套件則使用 `await wb.save(...)`。 |
| *我要如何設定功能表圖示的樣式？* | 提供任意 Material‑Icons 名稱（例如 `"icon": "edit"`）。前端會自動載入圖示字型。 |
| *大型工作簿該怎麼處理？* | 僅載入所需的工作表，並考慮使用 `openpyxl.iter_rows()` 串流讀取列，以降低記憶體使用量。 |

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在此處示範的技術之上。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [保留 Excel 儲存格或範圍的單引號前綴](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [保留 Excel 儲存格或範圍的單引號前綴（德文）](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [保留 Excel 儲存格或範圍的單引號前綴（法文）](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}