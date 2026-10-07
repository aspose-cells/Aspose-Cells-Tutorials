---
category: general
date: 2026-10-07
description: PythonでExcelブックを作成し、セルの背景色を設定し、列幅を自動調整し、Excelに日付を入力する簡潔なコード例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: ja
lastmod: 2026-10-07
og_description: PythonでExcelブックを作成し、セルの背景色を設定し、列幅を自動調整し、Excelに日付を入力します。このステップバイステップガイドに従って、TimePeriodDemo.xlsx
  ファイルを生成してください。
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: PythonでExcelワークブックを作成 – 背景設定と自動調整
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
title: PythonでExcelワークブックを作成し、セルの背景を設定する
url: /ja/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでExcelブックを作成し、セルの背景色を設定する

PythonでExcelブックを作成し、数行のコードだけで条件付き書式を適用します。このチュートリアルでは、**Excelの作成方法**をプログラムで示し、セルの背景色の設定、Excel列の自動調整、そしてAspose.Cellsライブラリを使用してExcelに日付を入力する方法を示します。

以下を学びます:
* ワークブックを初期化し、最初のワークシートを取得する。  
* 「Yesterday」日付をハイライトする条件付き書式を定義する。  
* 特定のセルにサンプル日付を挿入する。  
* データが見やすいように列を自動調整する。  
* ワークブックを任意のフォルダーに保存する。

唯一の前提条件は、`aspose-cells` と `aspose-pydrawing` パッケージがインストールされた、動作する Python 3 環境です：

```bash
pip install aspose-cells aspose-pydrawing
```

---

## PythonでExcelブックを作成する – ステップバイステップ

以下のセクションでは、プロセスを管理しやすいステップに分解しています。各ステップには必要なコード、**なぜ**重要なのかの説明、そして一般的な落とし穴を回避するためのヒントが含まれています。

### ステップ 1: 必要な名前空間をインポートし、ヘルパー関数を定義する

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Why this matters*: 正しいクラスをインポートすることで、ワークブックの作成、条件付き書式、カラー処理にアクセスできます。  
**Pro tip**: インポートはファイルの先頭にまとめておくと、スクリプトが読みやすくなり、循環インポートエラーを防げます。

### ステップ 2: ワークブックを作成し、最初のワークシートを取得する

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

`Workbook()` コンストラクタは、メモリ上に空の Excel ワークブックを作成します。  
**Why**: 新しいワークブックから開始することで、以前の実行から残っている書式設定がないことが保証されます。

### ステップ 3: 条件付き書式でセルの背景色を設定する

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

*Why*: **time period** 条件を使用すると、昨日の日付が含まれるセルが自動的にハイライトされ、手動での日付チェックが不要になります。  
**Tip**: `Color.pink` は単なる例です。任意の `Color` オブジェクト（`Color.yellow`、`Color.light_green` など）を使用できます。

### ステップ 4: Excelに日付を入力する

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

ここでは、セル `I19` と `K20` に **Excelに日付を入力** しています。最初の日付は条件付き書式をトリガーし、2 番目はトリガーしません。  
**Why this matters**: 一致する値と一致しない値の両方を示すことで、ルールが期待通りに機能することを確認できます。

### ステップ 5: 可視性向上のために Excel 列を自動調整する

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` は、最も長いセルの値に基づいて列幅を調整します。  
**Tip**: すべてのデータを書き込んだ後に呼び出すと、未完成の内容で幅が計算されるのを防げます。

### ステップ 6: ワークブックを保存する

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

ファイルを保存すると、メモリ上のワークブックが最新の XLSX 形式でディスクに書き込まれます。

### 完全スクリプト – すべてをまとめる

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

**期待される出力**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

生成されたファイルを Excel で開くと、セル `I19:K20` のうち「Yesterday」に該当する日付のセルがピンクの背景で表示され、列 L はラベルが切れずに表示できる幅になっています。

## このアプローチが最適な理由

* **シングルパスワークフロー** – すべての操作が同じ `Workbook` インスタンス上で行われ、不要な I/O を回避します。  
* **条件付き書式** – `FormatConditionType.TIME_PERIOD` を使用すると、Excel が日付ロジックを処理し、カスタムの Python 日付チェックを書くよりも信頼性が高くなります。  
* **明示的なスタイリング** – `background_color` と `pattern` を設定することで、Excel のバージョン間で視覚的な結果が保証されます。  
* **データ入力後の自動調整**

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Excelブック作成 Python – 完全ガイド](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Excelブック作成 Python – 完全ステップバイステップガイド](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Excelブック作成 Python – Lambda を使用した完全ガイド](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}