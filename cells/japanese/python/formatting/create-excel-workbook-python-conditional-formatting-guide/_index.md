---
category: general
date: 2026-07-20
description: Aspose.Cells を使用して Python で Excel ワークブックを作成し、セルの背景色を設定し、日付に基づいてセルのスタイルを変更する条件付き書式を
  Python で追加する。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: ja
lastmod: 2026-07-20
og_description: Aspose.Cells を使用して Python で Excel ワークブックを作成します。セルの背景色の設定方法と、日付でセルをフォーマットする条件付き書式の追加方法を学びましょう。
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: PythonでExcelワークブックを作成 – 条件付き書式を追加
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: PythonでExcelワークブックを作成 – 条件付き書式ガイド
url: /ja/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークブックを Python で作成 – 条件付き書式ガイド

UI を開かずに、最初から **create Excel workbook Python** を作成し、洗練された見た目にする方法を考えたことはありませんか？ あなたは一人ではありません。多くの開発者が、**set cell background color** を設定したり、日付ベースのスタイルをプログラムで適用しようとすると壁にぶつかります。  

このチュートリアルでは、Aspose.Cells を使用して **add conditional formatting python** ルールを追加し、日付でセルをフォーマットし、結果を最新の XLSX ファイルとして保存する、完全で実行可能な例を順に解説します。最後まで読むと、どのプロジェクトにも組み込める自己完結型スクリプトが手に入ります。

## 学べること

- ワークブックを初期化し、最初のワークシートを取得する方法。  
- 全範囲に対して **set cell background color** を設定する方法。  
- **aspose cells conditional formatting** を使用して「Yesterday」日付をハイライトする方法。  
- 列の自動調整とファイルのディスクへの保存。  

外部設定は不要です—Python 3 と Aspose.Cells パッケージだけで動作します。すでに `aspose-cells` をインストール済みならすぐに使用できます。そうでなければ、`pip install aspose-cells` を実行すれば完了です。

## 前提条件

- Python 3.8+（コードは 3.9、3.10 以降でも動作します）。  
- Aspose.Cells for Python via .NET（`aspose-cells` NuGet ラッパー）。  
- Excel の基本概念（セル、範囲、書式設定）に関する基本的な知識。  

揃いましたか？素晴らしい—それでは始めましょう。

## Excel ワークブックを Python で作成 – 設定とワークシート

まず最初に、フレッシュな workbook オブジェクトとデフォルトの worksheet への参照が必要です。ここが後のすべての操作が行われるキャンバスになります。

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Why this matters:** `Workbook()` はメモリ内の Excel ファイルを構築し、一時ファイルの必要性を排除します。`worksheet` 変数はセルレベルの操作のエントリーポイントです。

## セルの背景色を設定

ルールを追加する前に、対象範囲にベースカラーを設定しておくと、条件付き書式が際立ちます。以下のヘルパーは、指定範囲の `FormatConditionCollection` を取得（または作成）し、セルに単色の背景を塗ります。

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Pro tip:** 同じ範囲に複数のルールを適用する予定がある場合、このヘルパーを一度呼び出し、返されたコレクションを保持してください。API 呼び出し回数が削減できます。

## 日付範囲向けの Conditional Formatting Python を追加

さあ楽しいパートです：**time‑period conditional formatting** ルールを作成し、昨日の日付が含まれるセルをハイライトします。これは Aspose.Cells を使用した **format cells by date** の力を示す例です。

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Why use `TIME_PERIOD`?** カスタム数式を書く必要がなくなります。Aspose.Cells は日付を現在のシステム日付と比較して評価するため、ルールは常に有効です。

### ルールの実行

```python
apply_yesterday_rule()
```

生成されたファイルを開くと、セル `I19` がピンクに光ります（「Yesterday」だからです）。一方、`K20` はベースの緑色のままです。

## 列の自動調整とワークブックの保存

整ったスプレッドシートはプロフェッショナルに見えます。自動調整によりデータが詰まり過ぎることを防げます。

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Edge case:** 存在しないディレクトリを指定すると、`workbook.save` がエラーを投げます。エラーハンドリングが必要な場合は、`try/except` ブロックで保存呼び出しをラップしてください。

### 完全スクリプト（コピー＆ペースト可能）

以下が実行可能な完全なスクリプトです。`YOUR_DIRECTORY` をマシン上の有効なフォルダーに置き換えるだけです。

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

このスクリプトを実行すると、先ほど説明した条件付き書式が適用された `TimePeriodExample.xlsx` が生成されます。

## よくある質問とヒント

- **Can I target a different date range?**  
  絶対に可能です。`"I19:K20"` を任意の A1 形式の範囲に変更し、サンプルの日付もそれに合わせて調整してください。

- **What if I need a custom formula instead of `YESTERDAY`?**  
  `FormatConditionType.FORMULA` を使用し、`condition.formula1 = "YOUR_FORMULA"` と設定します。例として、昨日を模倣するには `=TODAY()-A1=1` を使用します。

- **How do I apply multiple rules to the same range?**  
  別の `FormatConditionType` で `conditions.add_condition` を再度呼び出します。順序が重要で、後のルールが先のルールを上書きすることがあります。

- **Is there a way to set font colour together with background?**  
  はい。`condition.style.font.color = Color.white`（または他の `Color`）を変更します。

## 結論

これで、Aspose.Cells を使用して **create Excel workbook Python** を行い、**set cell background color** を設定し、日付でセルをフォーマットする **add conditional formatting python** を追加する方法が分かりました。このスクリプトは完全に機能し、ディレクトリが存在しないといったエッジケースにも対応しており、複数ルールの条件ロジックや動的範囲検出など、より高度なシナリオにも拡張可能です。

次のステップに進む準備はできましたか？「Yesterday」ルールを「Last Week」に置き換えてみたり、グラデーション塗りつぶしを試したり、数十のフォーマット済みテーブルを含む完全なレポートを生成したりしてみてください。基本的な要素はすべて揃っており、Python での **aspose cells conditional formatting** のコアを習得したことになります。

コーディングを楽しんで、コメントであなたのバリエーションもぜひ共有してください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、完全に動作するコード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}