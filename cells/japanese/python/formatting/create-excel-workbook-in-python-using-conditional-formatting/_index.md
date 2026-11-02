---
category: general
date: 2026-09-21
description: PythonでExcelブックを作成し、セルの背景色を設定し、Aspose.Cellsを使用して日付に基づく条件付き書式を適用する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: ja
lastmod: 2026-09-21
og_description: PythonでExcelブックを作成し、セルの背景色を設定し、Aspose.Cellsを使用して日付に基づく条件付き書式を適用します。ステップバイステップのガイドに従ってください。
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Pythonで条件付き書式付きExcelブックを作成
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Pythonで条件付き書式を使用してExcelブックを作成する
url: /ja/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 条件付き書式を使用したPythonでのExcelブック作成

If you need to **create Excel workbook python** scripts that highlight dates automatically, this guide shows you exactly how. You’ll see how to **set cell background color**, add a “Yesterday” rule, and save the file—all with Aspose.Cells for Python.

Working with Excel files programmatically often means repeating the same formatting logic across many sheets. By the end of this tutorial you’ll have a reusable pattern for **excel conditional formatting python** that you can drop into any project.

## 前提条件

- Python 3.8+ がインストールされていること  
- `aspose-cells` パッケージ (`pip install aspose-cells`)  
- Python の関数と datetime モジュールの基本的な知識  

No additional libraries are required; Aspose.Cells handles all Excel operations.

## 手順 1: ワークブックの作成と最初のワークシートへのアクセス

The first step is to **create excel workbook python** objects and grab the default worksheet. This gives you a clean canvas for further styling.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*重要ポイント:* `Workbook()` はメモリ内のExcelファイルを作成します。`worksheets[0]` にアクセスすることでシート名をハードコーディングせず、デフォルト名が変更されても機能します。

## 手順 2: TIME_PERIOD 条件付き書式を追加するヘルパー

To keep the code tidy, we wrap the conditional‑format creation in a helper. It receives a cell range, a background colour, and the desired time‑period rule.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*重要ポイント:* ヘルパーは条件付き書式作成の繰り返しステップを抽象化し、「Today」や「Last Week」などの他の日付ベースのルールでも簡単に再利用できます。

## 手順 3: 範囲に「Yesterday」ルールを適用

Now we use the helper to highlight cells that contain yesterday’s date. The range `I19:K20` will turn **medium sea green** when the condition is met.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*重要ポイント:* `TimePeriodType.YESTERDAY` は Aspose.Cells の組み込み列挙型の一部で、日付を手動で計算する必要がありません。ライブラリはワークブックが開かれるたびにルールを評価します。

## 手順 4: サンプル日付で範囲にデータを入力

To see the rule in action, we write two dates—one that matches “Yesterday” and one that does not. The `number` style `30` corresponds to a built‑in date format.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*重要ポイント:* 具体的な日付を挿入することで、特定の日にファイルを開かなくても条件付き書式が機能するか検証できます。

## 手順 5: 説明ラベルを追加し、列幅を自動調整

A small label clarifies the purpose of the formatted range, and `auto_fit_column` makes the sheet readable.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## 手順 6: ワークブックを保存

Finally, write the workbook to disk. The `os.makedirs` call ensures the target folder exists.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

*TimePeriodDemo.xlsx* を開くと以下が確認できます:

- セル **I19** は値が「Yesterday」ルールに一致するため **medium sea green** に着色されます。  
- セル **K20** は条件を満たさないためデフォルトの背景のままです。  

これは **format cells by date** を Python のワンラインで実現する例です。

## 完全な実行可能例

Putting all pieces together, here’s the complete script you can copy‑paste and run:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Run the script, open the resulting file, and you’ll see the conditional formatting in action.

## 一般的なバリエーションとエッジケース

| バリエーション | 実装方法 | 使用タイミング |
|-----------|------------------|-------------|
| **“Today” をハイライト** | `TimePeriodType.YESTERDAY` を `TimePeriodType.TODAY` に置き換える | リアルタイム ダッシュボード |
| **複数範囲** | 各範囲に対して `add_time_period` を呼び出し、異なる色を渡す | 複雑なレポート |
| **動的日付範囲** | `TimePeriodType.LAST_7_DAYS` または `TimePeriodType.NEXT_MONTH` を使用 | ローリングレポート |
| **カスタムカラー** | `Color.from_argb(255, r, g, b)` を使用して任意の色合いを作成 | ブランド一貫のスタイリング |

**プロのヒント:** ソリッド塗りつぶしが必要な場合は常に `condition.style.pattern = BackgroundType.SOLID` を設定してください。設定しないと、Excel がバージョン間で一貫性のないグラデーションを表示することがあります。

## 結論

You now know how to **create Excel workbook python** scripts that **set cell background color**, apply **excel conditional formatting python**, and **format cells by date** using Aspose.Cells. The example covers a **date based conditional formatting** scenario, but the same pattern works for any time‑period rule.

Next, you might explore:

- データバーやアイコンセットの追加 (`FormatConditionType.DATA_BAR`)  
- 同一範囲に複数の条件付きルールを組み合わせる  
- レポート用にワークブックを PDF にエクスポート (`SaveFormat.PDF`)  

さまざまな色、範囲、時間期間タイプを試して、特定のレポート要件に合わせてください。コーディングを楽しんでください！

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}