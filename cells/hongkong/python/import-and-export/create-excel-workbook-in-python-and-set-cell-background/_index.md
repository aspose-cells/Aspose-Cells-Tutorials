---
category: general
date: 2026-10-07
description: 在 Python 中建立 Excel 工作簿，設定儲存格背景色、自動調整欄寬，並以簡潔的程式碼範例填入日期。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: zh-hant
lastmod: 2026-10-07
og_description: 在 Python 中建立 Excel 活頁簿，然後設定儲存格背景顏色、自動調整欄寬，並在 Excel 中填入日期。跟隨此一步一步的指引，即可產生
  TimePeriodDemo.xlsx 檔案。
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: 使用 Python 建立 Excel 工作簿 – 設定背景與自動調整
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: 在 Python 中建立 Excel 工作簿並設定儲存格背景
url: /zh-hant/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中建立 Excel 工作簿並設定儲存格背景

在 Python 中建立 Excel 工作簿，僅需幾行程式碼即可套用條件格式化。本教學示範如何以程式方式 **建立 Excel** 檔案、設定儲存格背景顏色、自動調整 Excel 欄寬，並使用 Aspose.Cells 函式庫在 Excel 中填入日期。

您將學會：
* 初始化工作簿並取得第一個工作表。  
* 定義條件格式以突顯「昨天」的日期。  
* 在特定儲存格插入範例日期。  
* 自動調整欄寬，使資料清晰可見。  
* 將工作簿儲存至指定資料夾。

唯一的先決條件是已安裝 `aspose-cells` 與 `aspose-pydrawing` 套件的 Python 3 環境：

```bash
pip install aspose-cells aspose-pydrawing
```

---

## 在 Python 中建立 Excel 工作簿 – 步驟說明

以下章節將整個流程拆解為可管理的步驟。每一步皆提供所需程式碼、說明 **為何** 重要，以及避免常見陷阱的提示。

### Step 1: 匯入必要的命名空間並定義輔助函式

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Why this matters*: 匯入正確的類別讓您能使用工作簿建立、條件格式化與顏色處理功能。  
**Pro tip**: 將匯入語句放在檔案最上方；這樣腳本較易閱讀，也能避免循環匯入錯誤。

### Step 2: 建立工作簿並取得第一個工作表

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

`Workbook()` 建構式會在記憶體中建立一個空的 Excel 工作簿。  
**Why**: 從全新工作簿開始，可避免前一次執行遺留下的格式設定。

### Step 3: 使用條件格式設定儲存格背景顏色

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Why*: 透過 **時間區間** 條件自動突顯包含昨天日期的儲存格，免除手動日期檢查。  
**Tip**: `Color.pink` 只是範例；您可以使用任何 `Color` 物件（如 `Color.yellow`、`Color.light_green` 等）。

### Step 4: 在 Excel 中填入日期

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

此處 **在 Excel** 儲存格 `I19` 與 `K20` 中填入日期。第一個日期會觸發條件格式化，第二個則不會。  
**Why this matters**: 同時示範符合與不符合條件的值，讓您能驗證規則是否如預期運作。

### Step 5: 為了更佳可視性自動調整 Excel 欄寬

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` 會根據最長的儲存格內容調整欄寬。  
**Tip**: 請在寫入所有資料之後再呼叫，否則寬度可能會以不完整的內容計算。

### Step 6: 儲存工作簿

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

儲存檔案會將記憶體中的工作簿寫入磁碟，使用現代的 XLSX 格式。

### Full script – putting it all together

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Expected output**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

在 Excel 中開啟產生的檔案 – 儲存格 `I19:K20` 會對「昨天」的日期顯示粉紅背景，且 L 欄的寬度足以完整顯示標籤而不被裁切。

---

## 為何此方法是最佳選擇

* **Single‑pass workflow** – 所有操作皆在同一個 `Workbook` 實例上完成，避免不必要的 I/O。  
* **Conditional formatting** – 使用 `FormatConditionType.TIME_PERIOD` 讓 Excel 處理日期邏輯，比自行撰寫 Python 日期檢查更可靠。  
* **Explicit styling** – 設定 `background_color` 與 `pattern` 可保證在各 Excel 版本中的視覺結果一致。  
* **Auto‑fit after data** – 在寫入全部資料後再執行自動調整，可確保欄寬正確。

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，進一步深化您對 API 功能的掌握，並探索在實際專案中可採用的其他實作方式。

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}