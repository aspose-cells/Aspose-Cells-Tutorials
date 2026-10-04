---
category: general
date: 2026-10-04
description: Aspose.Cells を使用して Python で Excel ワークブックを作成します。Excel の条件付き書式（Python）、セルの背景色（Python）、セルの日付書式（Python）をフル例で学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: ja
lastmod: 2026-10-04
og_description: Aspose.Cells を使用して Python で Excel ワークブックを作成します。このチュートリアルでは、Python
  による Excel の条件付き書式、セルの背景色設定、日付のセル書式設定をステップバイステップで紹介します。
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: PythonでExcelブックを作成する – 条件付き書式付き完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Pythonで条件付き書式とセルの背景色を使用したExcelブックを作成
url: /ja/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークブックを Python で作成し、条件付き書式とセルの背景色を設定する

If you need to **create Excel workbook python** quickly, this guide shows you exactly how. You’ll see a complete, runnable example that adds **excel conditional formatting python**, changes the **cell background color python**, and **format cells date python** for a “Yesterday” highlight.  

In many reporting scenarios the visual cue of a colored cell makes the data instantly understandable. This tutorial walks you through every line of code, explains why each step matters, and gives you a ready‑to‑run script you can adapt to your own projects.

## 本記事で達成できること

1. **create Excel workbook python** を Aspose.Cells ライブラリを使用して作成します。  
2. **excel conditional formatting python** を適用し、 “Yesterday” に該当する日付を自動的にハイライトします。  
3. **cell background color python** をピンクに設定します（好きな色に変更可能）。  
4. **format cells date python** を使用して、日付を標準の Excel 日付形式で表示します。  

No prior experience with Aspose.Cells is required—just a working Python 3 environment and pip access.

## 前提条件

- Python 3.8 以上がインストールされていること。  
- `aspose-cells` と `aspose-pydrawing` パッケージを `pip install aspose-cells aspose-pydrawing` でインストール済みであること。  
- Python の構文と Excel の概念（ワークブック、ワークシート、セル）に基本的に慣れていること。  

> **Pro tip:** スクリプトを仮想環境で実行すると、他のプロジェクトとのバージョン競合を回避できます。

## ステップ 1: プロジェクトをセットアップし、必要なクラスをインポートする

The first step when you **create Excel workbook python** is to import the Aspose.Cells classes you’ll need. These classes give you direct access to workbook creation, conditional formatting, and styling.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Why this matters:* 必要なシンボルだけをインポートすることで名前空間が整理され、スクリプトが読みやすくなります。`Workbook` は **create Excel workbook python** のエントリーポイントであり、`FormatConditionType` と `TimePeriodType` は **excel conditional formatting python** に不可欠です。

## ステップ 2: 新しいワークブックを作成し、最初のワークシートを取得する

Now we actually **create Excel workbook python**. The `Workbook()` constructor gives you an empty Excel file with a default worksheet.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explanation:* すべての Excel ファイルは少なくとも 1 つのワークシートから始まります。デフォルトでは Aspose.Cells が “Sheet1” と名付けます。後でシートを追加することも可能ですが、このデモでは単一シートにすることで例をシンプルに保ちます。

## ステップ 3: 条件付き書式の対象範囲を定義する

Conditional formatting works on a rectangular range. Here we choose the range `I19:K20`, which gives us three columns and two rows to play with.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Why we do this:* `get` メソッドは指定した範囲に結び付けられた `ConditionalFormatting` オブジェクトを返します。範囲に書式がまだ設定されていない場合、Aspose.Cells は自動的に新しいコレクションを作成します。

## ステップ 4: TIME_PERIOD 条件を追加し、背景色を設定する

This is the core of **excel conditional formatting python**. We add a `TIME_PERIOD` rule that highlights cells containing dates that fall on “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Deep dive:*  
- `FormatConditionType.TIME_PERIOD` は、Excel に対して日付を現在の日付に対して相対的に評価するよう指示します。  
- `TimePeriodType.YESTERDAY` は組み込みの列挙型で、毎日自動的に更新されるため、ワークブックは常に最新の “Yesterday” をハイライトします。  
- `background_color` を `Color.pink` に、パターンを `SOLID` に設定することで、余分な VBA コードなしで **cell background color python** の効果を実現します。

## ステップ 5: 範囲にサンプル日付を入力し、日付書式を適用する

To see the conditional formatting in action, we need real date values. We also need to **format cells date python** so Excel treats them as dates rather than plain numbers.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Explanation:*  
- `style.number = 30` 行が **format cells date python** のステップです。フォーマットコード 30 は短い日付形式（`m/d/yy`）に対応します。  
- ヘルパー関数を使用することでコードの DRY（Don’t Repeat Yourself）を保ち、後で日付を追加しやすくなります。

## ステップ 6: 説明ラベルを追加する

A small label helps anyone opening the workbook understand why the cells are colored.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## ステップ 7: ワークブックをディスクに保存する

Finally, we **create Excel workbook python** on disk by calling `save`. The `SaveFormat.XLSX` constant ensures the file is in the modern Office Open XML format.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

When you open `TimePeriodDemo.xlsx` in Excel, you’ll see:

- セル `I19` と `K20` に日付が入っています。  
- “Yesterday” に該当するセル（この静的例では `I19`）がピンクでハイライトされます。  
- ラベル “Yesterday” が `I20` に表示されます。  

> **Tip:** スクリプトを別の日に実行しても、条件付き書式は現在のシステム日付のちょうど1日前のセルをハイライトし続けます—コードの変更は不要です。

## 完全スクリプト – コピーしてすぐ実行可能

Below is the complete, self‑contained program that incorporates all the steps above. Copy it into a file named `conditional_format_demo.py`, adjust `YOUR_DIRECTORY`, and execute with `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### 期待される出力

Running the script prints a confirmation line:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Opening the generated file shows the pink background on the cell that matches the “Yesterday” rule, confirming that **excel conditional formatting python** and **cell background color python** are working together.

## 一般的なバリエーションとエッジケース

| 状況 | コードの適応方法 |
|-----------|-----------------------|
| **Different highlight color** | `Color.pink` を他の任意の `Color` 定数（例: `Color.light_green`）に変更します。 |
| **Highlight “Today” instead of “Yesterday”** | `condition.time_period = TimePeriodType.TODAY` に設定します。 |
| **Apply formatting to an entire column** | `"A:A"` のような範囲を使用し、`target_range` 変数をそれに合わせて調整します。 |
| **Use a custom date format** | `style.number = 30` を `style.custom = "dd-mmm-yyyy"` に置き換えて、より読みやすい形式にします。 |
| **Multiple conditions on the same range** |  |

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}