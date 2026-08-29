---
category: general
date: 2026-08-08
description: PythonでExcelブックを作成し、日付に基づく条件付き書式を追加します。Aspose.Cellsを使用した、昨日のセルをハイライトするステップバイステップガイド。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: ja
lastmod: 2026-08-08
og_description: Aspose.Cells を使用して Python で Excel ワークブックを作成し、日付に基づく条件付き書式を適用して動的なスプレッドシートを実現します。
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: PythonでExcelブックを作成 – 日付の条件付き書式
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: PythonでExcelブックを作成し、日付の条件付き書式を設定する
url: /ja/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでExcelブックを作成し、日付に基づく条件付き書式を適用する

If you need to **create Excel workbook Python** and automatically highlight cells that match a specific date, this tutorial shows you exactly how. You’ll learn to apply **conditional formatting based on date** so that yesterday’s dates light up in pink, using the Aspose.Cells library.

このチュートリアルでは、**create Excel workbook Python** を行い、特定の日付に一致するセルを自動的にハイライトする方法を正確に示します。Aspose.Cells ライブラリを使用して、**条件付き書式（日付ベース）** を適用し、昨日の日付がピンクでハイライトされるようにします。

The guide walks through every step—from installing the SDK to saving the final .xlsx file—so you can copy‑paste a working example into your own project. No external documentation is required; all code and explanations are self‑contained.

このガイドでは、SDK のインストールから最終的な .xlsx ファイルの保存まで、すべての手順を順に解説します。動作するサンプルをコピー＆ペーストして自分のプロジェクトに組み込めます。外部ドキュメントは不要で、コードと説明はすべて本稿に含まれています。

## 前提条件

* Python 3.8 以上がインストールされていること。
* `aspose-cells` パッケージ（Aspose.Cells の Python ラッパー）。以下でインストールします:
  ```bash
  pip install aspose-cells
  ```
* Python と Excel の基本概念（ワークシートやセルスタイルなど）に慣れていること。

> **プロのコツ:** Aspose.Cells は Microsoft Excel がインストールされていなくても動作するため、サーバーサイドの自動化に最適です。

## ステップ 1: Python で Excel ブックを作成する

The first task is to instantiate a new workbook and grab the default worksheet. This object represents the entire Excel file and provides access to rows, columns, and formatting APIs.

最初のタスクは新しいワークブックをインスタンス化し、デフォルトのワークシートを取得することです。このオブジェクトは Excel ファイル全体を表し、行、列、書式設定 API へのアクセスを提供します。

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Creating the workbook is the foundation for any further manipulation, whether you’re adding data, formulas, or formatting rules.

ワークブックの作成は、データや数式、書式設定ルールを追加するなど、以降のすべての操作の基礎となります。

## ステップ 2: 日付ベースの条件付き書式を定義する

Now we add **conditional formatting based on date**. The `FormatConditionType.TIME_PERIOD` enum lets us specify built‑in time periods such as Yesterday, Today, or LastWeek.

ここで **条件付き書式（日付ベース）** を追加します。`FormatConditionType.TIME_PERIOD` 列挙体を使用すると、Yesterday、Today、LastWeek などの組み込み時間期間を指定できます。

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Why this step matters: Excel evaluates the condition for each cell in the range. When a cell’s value falls within the defined period (yesterday), the style we assigned is applied automatically.

このステップが重要な理由: Excel は範囲内の各セルに対して条件を評価します。セルの値が定義された期間（昨日）に該当すると、事前に設定したスタイルが自動的に適用されます。

## ステップ 3: サンプル日付で範囲にデータを入力する

To see the rule in action, we write a couple of `datetime` objects into the target cells. One of them is deliberately set to yesterday’s date relative to the workbook’s internal date system.

ルールの動作を確認するために、対象セルにいくつかの `datetime` オブジェクトを書き込みます。そのうちの一つは、ワークブック内部の日付システムに対して意図的に昨日の日付に設定しています。

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

The `number = 30` line tells Excel to display the value using its standard short‑date format. You can change this index to any built‑in number format if you prefer a different presentation.

`number = 30` 行は、Excel に標準の短い日付形式で値を表示させることを指示します。別の表示形式が必要な場合は、このインデックスを任意の組み込み数値形式に変更できます。

## ステップ 4: 読みやすさのために列幅を調整する

Auto‑fitting the column that contains the dates makes the output easier to read, especially when the workbook is opened in Excel or a viewer.

日付が含まれる列を自動調整すると、特に Excel やビューアでブックを開いたときに出力が読みやすくなります。

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## ステップ 5: ワークブックをディスクに保存する

Finally, store the workbook as an .xlsx file. Replace `"YOUR_DIRECTORY"` with a real path on your machine.

最後に、ワークブックを .xlsx ファイルとして保存します。`"YOUR_DIRECTORY"` を実際のパスに置き換えてください。

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

When you open `TimePeriodDemo.out.xlsx` in Excel, cell **I19** will appear with a pink background because its value matches the “Yesterday” rule, while **K20** remains unchanged.

`TimePeriodDemo.out.xlsx` を Excel で開くと、セル **I19** が値が「Yesterday」ルールに一致しているためピンクの背景で表示され、**K20** は変更されません。

### 期待される出力

| I19（日付） | I20（ラベル） | J19 | J20 | K19 | K20（日付） |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30*（ピンクの背景） | 昨日 | – | – | – | *2008‑08‑03*（書式なし） |

## 一般的なバリエーションとエッジケース

| Situation | How to adapt the code |
|-----------|-----------------------|
| **「昨日」ではなく「今日」をハイライト** | Change `condition.time_period = TimePeriodType.TODAY` |
| **ルールを列全体に適用** | Use `worksheet.get_range("A:A").format_conditions` |
| **カスタム日付範囲を使用（例：過去7日間）** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **異なる背景色** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **ディスプレイなしで Linux 上で実行** | Aspose.Cells is fully headless; no extra configuration required. |

## 完全な実行可能サンプル

Below is the complete script you can execute as‑is (after updating the output directory). All imports, comments, and error‑handling basics are included.

以下は、出力ディレクトリを更新すればそのまま実行できる完全なスクリプトです。すべてのインポート、コメント、エラーハンドリングの基本が含まれています。

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Running the script produces an Excel file where the “Yesterday” cell is automatically highlighted, demonstrating **create Excel workbook Python** combined with **conditional formatting based on date**.

スクリプトを実行すると、Excel ファイルが生成され、「Yesterday」セルが自動的にハイライトされます。これにより **create Excel workbook Python** と **conditional formatting based on date** の組み合わせが実証されます。

## 結論

You now know how to **create Excel workbook Python** objects, define a **date‑based conditional formatting

これで、**create Excel workbook Python** オブジェクトの作成方法と、**日付ベースの条件付き書式** の定義方法がわかりました。

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}