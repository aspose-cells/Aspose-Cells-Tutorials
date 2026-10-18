---
category: general
date: 2026-09-05
description: PythonでExcelブックを作成し、昨日のセルをハイライトする条件付き書式を追加します。完全なコードと各ステップが重要な理由を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: ja
lastmod: 2026-09-05
og_description: PythonでExcelブックを作成し、昨日の日付のセルをハイライトする条件付き書式を追加します。完全な解決策を得るには、このステップバイステップガイドに従ってください。
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: PythonでExcelワークブックを作成 – 条件付き書式を追加
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Pythonで条件付き書式付きのExcelブックを作成する
url: /ja/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで条件付き書式付きExcelブックを作成する

If you need to **create Excel workbook python** for a reporting task, this guide shows you how to generate a workbook and apply a conditional formatting rule that highlights yesterday’s dates. You’ll see the exact code, why each line exists, and how to adapt the solution for other date ranges.

Conditional formatting is a powerful way to draw attention to data that meets a specific condition. In this tutorial we use the Aspose.Cells library for Python via .NET, which provides full Excel feature support without requiring Microsoft Office. By the end of the guide you will have a file where cells in the range *I19:K20* turn pink when they contain yesterday’s date.

## 前提条件

* Python 3.9+ がインストールされていること
* `aspose-cells` パッケージ（`pip install aspose-cells` でインストール）
* Python の構文に関する基本的な知識
* ワークブックを保存するディレクトリへの書き込み権限

.NET ランタイムが利用可能であれば、コードは Windows、macOS、Linux で動作します。

## PythonでExcelブックを作成する

最初のステップは `Workbook` オブジェクトをインスタンス化し、デフォルトのワークシートを取得することです。このオブジェクトはメモリ上の Excel ファイル全体を表します。

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Why this matters*（なぜ重要か）: `Workbook()` は単一のワークシートを持つ空のブックを作成します。`worksheets[0]` にアクセスすることで、後でデータやスタイル、書式設定を追加するハンドルが得られます。

## 条件付き書式の範囲を追加する

次に、条件付きルールで評価される領域を定義します。範囲 `I19:K20` は 2 行にわたる 6 つのセルをカバーします。

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Why this matters*（なぜ重要か）: 特定の範囲に条件付き書式コレクションを追加することで、ルールが他のセルに影響しないように分離できます。これにより **add conditional formatting range** の要件が満たされます。

## ルールの定義：日付に基づいてセルをハイライトする

ここでは `TIME_PERIOD` タイプの条件を作成します。これにより、Excel は各セルの値を事前定義された時間ウィンドウと比較します。

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Why this matters*（なぜ重要か）: `TIME_PERIOD` は “Yesterday” や “Today”、 “Last Week” などを直接サポートする唯一の組み込みタイプです。`condition.time_period` を `YESTERDAY` に設定することで、ルールは自動的に各セルの日付値を現在の日付の前日と比較して評価します。

## 条件を満たすセルのスタイル設定

条件付き書式には視覚的なスタイルも必要です。ここでは、該当するセルを目立たせるためにピンクの単色塗りを選択します。

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Why this matters*（なぜ重要か）: スタイルオブジェクトは、条件を満たすセルが Excel でどのように表示されるかを定義します。単色のピンク塗りを使用することで **highlight cells based on date** の要件を満たし、結果の検証が容易になります。

## 評価用のサンプル日付を入力する

ルールの動作を確認するために、昨日の日付に該当するものと該当しないものの 2 つの日付を挿入します。`number` フォーマット `30` は組み込みの日付フォーマット `mm-dd-yy` に対応しています。

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Why this matters*（なぜ重要か）: マッチする日付とマッチしない日付の両方を提供することで、条件付き書式が正しく機能することを検証できます。スクリプト実行時には日付を当月に合わせるか、動的な値に置き換えてください。

## ワークブックを保存する

最後にファイルをディスクに書き込みます。`SaveFormat.XLSX` 定数により、出力が最新の Excel ファイル形式になることが保証されます。

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Why this matters*（なぜ重要か）: ワークブックを永続化することで、Excel、LibreOffice、または XLSX をサポートする任意のビューアで開くことができます。出力されたパスはファイルが書き込まれた場所を示します。

## 完全なスクリプト

すべての要素を組み合わせた、実行可能な完全スクリプトは以下の通りです。

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### 期待される出力

`TimePeriodExample.xlsx` を開くと:

* セル **I19** は、値が昨日に一致するためピンクの背景で表示されます。
* セル **K20** は、日付が期間外のためデフォルトの背景のままです。
* ラベル **“Yesterday”** は明示のためセル I20 に配置されています。

## 一般的なバリエーションとエッジケース

| シチュエーション | 調整 |
|-----------|------------|
| **昨日ではなく今日をハイライト** | `condition.time_period = TimePeriodType.TODAY` に変更します。 |
| **適用範囲を広げる** | `add("I19:K20")` の範囲文字列を `"A1:Z100"` のように更新します。 |
| **別の塗りつぶし色を使用** | `DrawingColor.pink` を他の `DrawingColor`（例：`DrawingColor.light_green`）に置き換えます。 |
| **動的な日付で処理** | 昨日の日付を `datetime.now() - timedelta(days=1)` で計算し、ルール適用前にその値を書き込みます。 |

**Pro tip**（プロのコツ）: 多数のユーザー向けにプログラムでワークブックを生成する場合、条件付き書式の定義をデータ挿入とは別にしておきましょう。これにより、コードを重複させずに複数シートで同じスタイルを再利用できます。

## プログラムで結果を検証する（オプション）

Excel を開かずに書式設定を確認したい場合は、保存後にセルのスタイルを検査できます。



## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Excel Automation&#58; Aspose.Cells for .NET を使用してワークブックを作成し、リストボックスを追加](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Aspose.Cells for Java で Excel ワークブックを作成し、ラベルを追加](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation：ワークブック作成とリストボックス追加（Aspose Cells）](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}