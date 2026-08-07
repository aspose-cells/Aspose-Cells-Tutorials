---
category: general
date: 2026-06-08
description: 為 GridJs 新增自訂右鍵功能表，並將表格匯出為 CSV（下載 CSV 檔案 Blob）。請按照此一步一步的教學，獲得完整可運作的範例。
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: zh-hant
og_description: 為 GridJs 新增自訂右鍵選單，並以下載 CSV 檔案 Blob 的方式匯出表格為 CSV。10 分鐘內即可學會完整實作。
og_title: 為 GridJs 添加自訂右鍵功能表 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: 為 GridJs 添加自訂右鍵功能表 – 完整指南
url: /zh-hant/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 為 GridJs 新增自訂右鍵功能表 – 完整指南

想要 **新增自訂右鍵功能表** 到 GridJs 元件嗎？在本教學中，我們會一步步帶你完成，並示範如何使用 **download CSV file blob** 來 **export grid to CSV**。無論你是要快速建立管理介面，或是完整的報告儀表板，一個右鍵功能表讓使用者能將資料匯出為 CSV，都能大幅提升工作效率。

我們會涵蓋所有必備內容：使用 Flask 的 Python 端、產生 Blob 的 JavaScript 處理函式，以及 GridJs 輸出的 HTML/JS。完成後，你將擁有一個可直接嵌入任何專案的完整範例。

---

## 你需要的環境

- **Python 3.9+** 與 **Flask** 已安裝（`pip install flask`）。
- **gridjs** 的 Python 包裝器（或直接使用 JavaScript 函式庫）— 本教學假設有一個薄層的 Python 包裝器，對應 JavaScript API。
- 具備 **async JavaScript** 的基本概念（`fetch`、`Promise`）— 別擔心，我們會逐行說明。
- 你喜愛的編輯器（VS Code、PyCharm，甚至簡單的文字編輯器皆可）。

就這樣。無需額外的前端建置工具，也不需要 Node npm 的繁雜流程。只要使用 Flask 直接提供 GridJs 產生的 HTML 即可。

---

## 為 GridJs 新增自訂右鍵功能表

首先，你需要告訴 GridJs 你想要自訂的右鍵功能表。預設情況下，GridJs 只提供最基本的選項（複製、貼上等），但你可以完整取代它。

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**為什麼重要：**  
設定 `CustomContextMenu` 會以你提供的清單取代預設項目。字串 `"Export CSV"` 只是顯示的標籤——真正的動作會在使用者點擊時觸發，我們會在下一步完成連結。

> *小技巧：* 列表保持簡短。過於雜亂的右鍵功能表會削弱快速操作的意義。

---

## 使用 Blob 下載將 Grid 匯出為 CSV

現在功能表項目已建立，我們需要一段 JavaScript 處理函式與伺服器通訊、取得 CSV、轉換為 **Blob**，並強制下載。這正是 **download CSV file blob** 所在的地方。

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### 逐行解析處理函式

| 行號 | 功能說明 |
|------|----------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | 呼叫 Flask 路由 (`/export/csv`)，並將工作表名稱作為查詢字串傳遞。 |
| `.then(r => r.blob())` | 將 HTTP 回應轉換為 **Blob**——實質上是 CSV 資料的二進位容器。 |
| `URL.createObjectURL(b)` | 產生一個暫時的 URL，讓瀏覽器可將其視為檔案。 |
| `a.download = cell.sheetName + ".csv"` | 設定使用者在下載對話框中看到的檔名。 |
| `a.click()` | 以程式方式點擊隱藏的 <a> 標籤，觸發瀏覽器下載 Blob。 |

> **為什麼使用 Blob？**  
> 瀏覽器無法直接下載 `fetch` 回傳的純文字，除非先將其轉換為類檔案的形式。使用 Blob‑URL 的技巧是最可靠、跨瀏覽器的方式，在不重新整理頁面的情況下觸發 **download CSV file blob**。

---

## 設定 Flask 後端

前端處理函式會呼叫 `/export/csv` 端點。以下是一個最簡化的 Flask 視圖，接收工作表名稱、從活頁本取得資料，並回傳 CSV 串流。

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### 重點說明

- **`io.StringIO`** 讓我們在記憶體中建立 CSV，無需寫入檔案系統。
- **`Content‑Disposition`** 告訴瀏覽器此檔案為附件，並建議檔名。即使前端已設定 `a.download`，在伺服器端也提供了非 JavaScript 用戶端的備援。
- 此路由刻意保持簡潔；之後可加入驗證、權限檢查，或針對大型資料集的串流處理。

---

## 在客戶端渲染 Grid

在自訂右鍵功能表與後端準備好之後，最後一步是渲染 GridJs 元件，並將 HTML/JS 傳送至瀏覽器。

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

在 Flask 視圖中，你通常會這樣寫：

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

當頁面載入時，GridJs 會建立表格、注入自訂右鍵功能表，且先前定義的 JavaScript 處理函式已可使用。右鍵點擊任意儲存格，選取 **Export CSV**，即可看到瀏覽器下載以工作表名稱命名的檔案。

---

## 完整可執行範例（全部檔案）

以下是完整可執行的程式碼，你可以直接複製貼上到新資料夾。先安裝 Flask（`pip install flask`），再執行 `python app.py`。

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [載入 CSV 檔案自訂解析器 – Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [CSV 匯出 Java 程式碼](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [匯出 Excel CSV 空白列 – Aspose Cells .NET](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}