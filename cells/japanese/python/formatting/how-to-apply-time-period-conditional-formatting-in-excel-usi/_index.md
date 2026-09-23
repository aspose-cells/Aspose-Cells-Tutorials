---
category: general
date: 2026-09-15
description: Aspose.Cells を使用した Python で、時間帯の条件付き書式を適用し、ワークブックを XLSX として保存する方法を学びます。ステップバイステップのコードを含みます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: ja
lastmod: 2026-09-15
og_description: Python を使用して Excel で期間条件付き書式を適用し、ブックを XLSX として保存します。Aspose.Cells の完全ガイドをご覧ください。
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: PythonでExcelに期間別条件付き書式を適用する
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Python を使用して Excel の期間条件付き書式を適用する方法
url: /ja/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python を使用して Excel で期間条件付き書式を適用する方法

Excel ファイルで **期間条件付き書式** が必要な場合、このチュートリアルでは Python での実装手順を詳しく解説します。ワークブックを作成し、昨日の日付をハイライトし、数行のコードだけで **save workbook as XLSX** する完全な実行可能サンプルをご覧いただけます。

条件付き書式は、特定のルールに合致するデータに注目させる強力な手段です。本ガイドでは「Yesterday」期間に焦点を当てますが、Today、LastWeek、NextMonth などの組み込み期間でも同様のパターンが利用できます。チュートリアルの最後までに、 **how to create excel workbook python** スタイルのスクリプトを本番環境で使える形で作成できるようになります。

## 前提条件

- Python 3.8+ がインストール済み  
- `aspose-cells` と `aspose-pydrawing` パッケージ (`pip install aspose-cells aspose-pydrawing`)  
- Python 文法の基本的な知識  

Aspose.Cells が内部でファイル生成を行うため、追加の Office インストールは不要です。

## Python で Aspose.Cells を使用した期間条件付き書式

このセクションでは、主要タスクに必要なコードを一行ずつ解説します。以下のコードブロックがフルスクリプトで、コメントが各ステップの目的を説明しています。

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### 各ステップの重要性

1. **Creating the workbook** は、Excel を開かずに操作できるインメモリの Excel ファイルを作成します。  
2. **Defining the range** (`I19:K20`) は、Aspose.Cells に対してルールが適用される領域を指定し、ロジックを分離します。  
3. **Adding a TIME_PERIOD condition** は、Aspose の組み込み列挙子 `TimePeriodType.YESTERDAY` を使用します。これにより手動で日付計算を行う必要がなく、ファイルを別の日に開いたときでも自動的に更新されます。  
4. **Setting the style** (`background_color` と `pattern`) は、ハイライトされたセルの表示方法を決定します。`Color.pink` を使用するとルールが視認しやすくなります。  
5. **Writing sample dates** で数値書式 30 を設定すると、Excel はシリアル番号ではなく短い日付として表示します。  
6. **Auto‑fitting the column** は、後からファイルを開く人の可読性を向上させます。  
7. **Saving as XLSX** は、Excel、Google Sheets、その他の最新スプレッドシートプログラムで開ける汎用性の高いファイルを生成します。

## Aspose.Cells で Excel ワークブックを Python スタイルで作成する方法

上記スクリプトはすでに **how to create excel workbook python** の最小手順を示しています。実務では次のような拡張が考えられます。

- 複数シートを追加する (`workbook.worksheets.add("Report")`)。  
- ループや pandas DataFrame (`worksheet.cells.import_data_table`) を使って大規模データテーブルを投入する。  
- `cell.get_style()` を利用してフォントや罫線など追加の書式設定を行う。

これらの操作はすべて同じパターンに従います：オブジェクトを取得し、プロパティを変更し、`set_style` または `save` を呼び出すだけです。

## 条件付き書式 Python の追加 – その他の便利パターン

「Yesterday」例に加えて、Aspose.Cells はさまざまな条件付き書式タイプをサポートしています。

| FormatConditionType | 典型的な使用例 |
|---------------------|----------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | カスタム数式 (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | シンプルな比較 (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | グラデーション カラースケール |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | セル内バー ビジュアライゼーション |

数値しきい値に対して **add conditional formatting python** を行うには、`FormatConditionType.TIME_PERIOD` を `FormatConditionType.CELL_VALUE` に置き換え、`condition.operator_type` と `condition.formula1` を設定します。

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Save workbook as XLSX – ベストプラクティス

**save workbook as xlsx** する際のポイント：

- **正しい `SaveFormat`** (`SaveFormat.XLSX`) を指定してレガシーフォーマットを回避する。  
- スクリプトがループで実行される場合は **決定的なファイル名** を使用する (`f"report_{datetime.now():%Y%m%d}.xlsx"`)。  
- 長時間稼働するサービスでは **リソースを解放** (`workbook.dispose()`) してネイティブメモリを確保する。

例ではすでに `SaveFormat.XLSX` を使用しており、すべての条件付き書式ルールを保持したモダンな zip ベースのワークブックが生成されます。

## Excel で昨日の日付をハイライト – 検証手順

スクリプト実行後、`TimePeriodExample.xlsx` を開きます。

1. セル `I19` と `K20` には日付 `30‑07‑2008` と `03‑08‑2008` が入っています。  
2. セル `I20` にはテキスト “Yesterday” が表示されます。  
3. システム日付を **2008 年 7 月 30 日** に変更してファイルを再度開くと、該当日付のセルが自動的にピンクで塗りつぶされます。  
4. システム日付を他の日に変えるとピンク塗りつぶしが解除され、**time period conditional formatting** のロジックが正しく機能していることが確認できます。

## よくある落とし穴と回避策

- **`aspose-pydrawing` が欠如** – `Color` クラスはこのパッケージに含まれます。インストール忘れは `ImportError` を引き起こします。  
- **数値書式が不正** – デフォルトの General 書式ではシリアル番号 (例: 39822) が表示されます。必ず `style.number = 30` を設定して短い日付表示にしてください。  
- **範囲の不一致** – 条件付き書式の範囲にハイライト対象のセルが含まれていないと、ルールは無効になります。

## プロのコツ：書式設定ルーチンを再利用

同じ「Yesterday」ルールを複数のワークブックで使う場合は、ロジックをヘルパー関数にまとめましょう。

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

必要な場所で `apply_yesterday_highlight(worksheet, "A1:A10")` を呼び出すだけです。

## 結論

本ガイドでは、Python を使って Excel に **time period conditional formatting** を実装し、**save workbook as XLSX** し、**highlight yesterday in Excel** する単一の再利用可能スクリプトを作成する方法を解説しました。これで、日次レポートの生成、ダッシュボード構築、データエクスポートなど、あらゆる自動化プロジェクトに **add conditional formatting python** コードを組み込むための確固たる基盤が手に入りました。

**次のステップ**

- `TimePeriodType` の他の値（`TODAY`、`LAST_WEEK` など）を試す。  
- 同一範囲に複数の条件付きルールを組み合わせて、よりリッチな視覚的ヒントを提供する。  
- ワークブック生成を Web サービスやスケジュールジョブに統合する。

コーディングを楽しみながら、条件付き書式がもたらす視覚的明快さを Excel 自動化に活かしてください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基に、さらに関連するトピックを深く掘り下げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能をマスターしたり、代替実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Aspose.Cells .NET を使用した Excel の条件付き書式マスターガイド](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Aspose.Cells .NET で Excel の交互行に条件付き書式を適用する方法](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Aspose.Cells for .NET と C# を使用したカスタムフォントによる条件付き書式のマスター](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}