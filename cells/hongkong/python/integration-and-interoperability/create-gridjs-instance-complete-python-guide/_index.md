---
category: general
date: 2026-06-30
description: 在 Python 中建立 GridJs 實例，使用自訂模態視窗設定。了解如何綁定工作表、設定模態視窗，以及輸出客戶端 JSON。
draft: false
keywords:
- create gridjs instance
- gridjs custom modal
- gridjs worksheet integration
- gridjs client configuration
- gridjs python api
language: zh-hant
og_description: 在 Python 中建立 GridJs 實例，並自訂模態設定。提供工作表整合與客戶端設定的逐步說明。
og_title: 建立 GridJs 實例 – 完整 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create GridJs instance in Python with custom modal settings. Learn
    how to bind a worksheet, configure the modal, and output client JSON.
  headline: Create GridJs Instance – Complete Python Guide
  type: TechArticle
tags:
- gridjs
- python
- web‑ui
- data‑grid
title: 建立 GridJs 實例 – 完整 Python 指南
url: /zh-hant/python/integration-and-interoperability/create-gridjs-instance-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 GridJs 實例 – 完整 Python 教學

有沒有想過要 **create gridjs instance** 卻怕自己抓狂？你並不孤單。無論是打造管理儀表板、商品目錄，或是快速檢視的試算表，讓 GridJs 正式運作都是第一道關卡。

在本教學中，我們會一步步示範真實案例：綁定工作表、開啟雙擊彈出的自訂 Modal，最後取得前端所需的設定 JSON。完成後，你將擁有一個可直接套用於任何 Flask 或 Django 專案的 GridJs 設定。

## 前置條件

- 本機已安裝 Python 3.8+  
- 具備 Python OOP 基礎  
- 有一個最小化的 `Worksheet` 類別（我們會為示範 mock 一個）  

目前尚無官方的 GridJs Python 套件，因此我們會模擬一個與 JavaScript 函式庫相同的 API。概念可直接對應到真實的 GridJs JavaScript 用法。

## 步驟 1：定義 Mock GridJs 類別（GridJs Python API）

在 **create gridjs instance** 之前，我們需要一個薄薄的包裝器來模擬真實函式庫。這樣可以讓範例可執行，且專注於設定流程。

```python
# gridjs_mock.py
import json

class Settings:
    """Container for all GridJs settings."""
    def __init__(self):
        self.custom_modal = CustomModal()

class CustomModal:
    """Settings for the double‑click custom modal."""
    def __init__(self):
        self.enabled = False
        self.title = ""
        self.width = "400px"
        self.height = "300px"
        self.url = ""

class GridJs:
    """A lightweight Python representation of a GridJs grid."""
    def __init__(self):
        self._worksheet = None
        self.settings = Settings()

    def set_worksheet(self, worksheet):
        """Bind a Worksheet object to the grid."""
        self._worksheet = worksheet

    def get_client_config(self):
        """Serialize the grid configuration for the front‑end."""
        config = {
            "worksheet": getattr(self._worksheet, "name", "undefined"),
            "custom_modal": {
                "enabled": self.settings.custom_modal.enabled,
                "title": self.settings.custom_modal.title,
                "width": self.settings.custom_modal.width,
                "height": self.settings.custom_modal.height,
                "url": self.settings.custom_modal.url,
            },
        }
        return json.dumps(config, indent=2)
```

> **小技巧：** 讓 Python 包裝器保持精簡——只要能產生要交給 JavaScript 端的 JSON 即可。過度設計會增加維護成本。

## 步驟 2：建立簡易 Worksheet 物件（GridJs Worksheet 整合）

我們的 **gridjs worksheet integration** 可以只是一個帶有 `name` 屬性的類別。實際應用中，你會從資料庫或 CSV 檔讀取資料。

```python
# worksheet.py
class Worksheet:
    """Mock worksheet holding tabular data."""
    def __init__(self, name):
        self.name = name
        # Imagine self.rows = [...] here
```

現在你已經有一個佔位物件，可以傳入 GridJs。

## 步驟 3：組裝 Grid – 核心「Create GridJs Instance」邏輯

有了 mock 類別後，我們終於可以 **create gridjs instance** 並一步步設定。

```python
# main.py
from gridjs_mock import GridJs
from worksheet import Worksheet

# 1️⃣ Create a GridJs instance
grid = GridJs()

# 2️⃣ Associate the worksheet you want to display
worksheet = Worksheet(name="Products")
grid.set_worksheet(worksheet)

# 3️⃣ Enable the custom modal that appears on double‑click
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Product"
grid.settings.custom_modal.width = "600px"
grid.settings.custom_modal.height = "400px"

# 4️⃣ Point the modal to an external HTML editor page
grid.settings.custom_modal.url = "/product-editor.html"

# 5️⃣ Retrieve the client‑side configuration JSON and output it
config_json = grid.get_client_config()
print(config_json)
```

### 預期輸出（GridJs 客戶端設定）

執行 `python main.py` 後會得到格式化好的 JSON：

```json
{
  "worksheet": "Products",
  "custom_modal": {
    "enabled": true,
    "title": "Edit Product",
    "width": "600px",
    "height": "400px",
    "url": "/product-editor.html"
  }
}
```

這段 JSON 正是你要傳給前端 GridJs 建構子的內容：

```javascript
new Grid({
  data: [],               // will be filled from the worksheet
  customModal: {/* … */} // values from the JSON above
});
```

## 步驟 4：將 JSON 注入前端頁面（完整整合）

剛才列印出的 **gridjs client configuration** 可以直接寫入 Flask 路由：

```python
# app.py (Flask snippet)
from flask import Flask, render_template_string, jsonify
from main import config_json  # reuse the same grid setup

app = Flask(__name__)

@app.route("/grid-config")
def grid_config():
    return jsonify(json.loads(config_json))

# Simple HTML page loading GridJs from CDN
HTML = """
<!doctype html>
<html>
<head>
  <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
</head>
<body>
  <div id="wrapper"></div>
  <script>
    fetch('/grid-config')
      .then(r => r.json())
      .then(config => {
        new gridjs.Grid({
          columns: ['ID', 'Name', 'Price'],
          data: [], // fetch actual rows based on config.worksheet
          customModal: config.custom_modal
        }).render(document.getElementById('wrapper'));
      });
  </script>
</body>
</html>
"""
@app.route("/")
def index():
    return render_template_string(HTML)

if __name__ == "__main__":
    app.run(debug=True)
```

> **為什麼會這樣運作：** 後端提供的 JSON 負載與你在 Python 中定義的設定完全對應。前端讀取相同的負載，即可確保 **gridjs custom modal** 按你設定的方式運作。

## 常見問題與邊緣案例（GridJs Custom Modal）

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| 雙擊時 Modal 完全不開啟 | `custom_modal.enabled` 仍為 `False` | 確認將 `grid.settings.custom_modal.enabled = True` |
| 手機上 Modal 尺寸怪異 | 使用固定像素值（`600px`）無法自適應 | 改用 CSS 相對單位（`80%`、`vh`）或 media query |
| URL 回傳 404 | 路徑 `/product-editor.html` 未被提供 | 在 Flask/Django 加入 static route，或將檔案放在 CDN |
| JSON 中缺少 Worksheet 名稱 | `Worksheet` 物件未設定 `name` 屬性 | 為 Worksheet 加上有意義的 `name`，或在 mock 中加入其他 metadata |

提前處理這些問題，可為你省下大量除錯時間。

## 延伸範例（後續步驟）

- **載入真實資料**：將 mock `Worksheet` 換成 pandas DataFrame，並將列序列化為 JSON。  
- **保護 Modal**：在提供 `/product-editor.html` 前加入驗證機制。  
- **動態欄位對映**：從 worksheet schema 取得欄位標題，而非硬編碼。  
- **國際化**：將 Modal 標題存於語言檔，並透過 JSON 負載注入。

所有這些擴充都以你剛掌握的 **create gridjs instance** 為基礎。

## 結論

我們已完整說明如何在 Python 中 **create gridjs instance**，從連結 worksheet、開啟自訂 Modal，到最後輸出乾淨的前端設定 JSON。這套模式簡潔、可重用，且能輕鬆嵌入任何現代 Web 框架。

快試試看，調整 Modal 大小、換成真實資料庫查詢，你就能在短時間內完成可投入生產的 GridJs 整合。有任何問題歡迎留言，祝 coding 愉快！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你在專案中使用的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能與替代實作方式。

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create a Custom Size Chart PDF with Aspose.Cells .NET: Step‑by‑Step Guide](/cells/english/net/charts-graphs/create-custom-size-chart-pdf-aspose-cells-net/)
- [How to Create a Custom Static Value Function in Aspose.Cells Java](/cells/english/java/formulas-functions/aspose-cells-java-custom-static-value-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}