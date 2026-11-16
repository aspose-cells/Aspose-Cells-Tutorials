---
category: general
date: 2026-11-16
description: Python を使用して Excel で条件付き書式を作成します。条件付き書式の範囲を追加し、日付をハイライトし、プログラムでワークブックを構築する方法を学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: ja
lastmod: 2026-11-16
og_description: Python を使って Excel で条件付き書式を作成します。このチュートリアルでは、条件付き書式の範囲を追加し、日付をハイライトし、ワークブックを生成する方法を示します。
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: PythonでExcelの条件付き書式を作成する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: PythonでExcelの条件付き書式を作成する方法
url: /ja/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ExcelでPythonを使用した条件付き書式の作成方法

Pythonで作業しながらExcelファイルに**条件付き書式を作成**する必要がある場合、このガイドではその手順を正確に示します。**create excel workbook python**‑styleでワークブックを作成し、書式設定範囲を定義し、IDEを離れることなく日付をハイライトする方法を学びます。

条件付き書式を使用すると、特定の条件を満たすセルを視覚的にフラグ付けできます—ダッシュボード、レポート、データ検証シートに最適です。このチュートリアルの最後までに、日付が「Yesterday」のセルをピンクに、その他の範囲は緑のままにする完全に機能するワークブックが作成できます。

## 何が達成できるか

* ゼロから新しいワークブックを作成する。  
* 特定のセルブロックに対して条件付き書式コレクションを追加する。  
* 日付をハイライトする **TIME_PERIOD** ルールを適用する（「日付をハイライトする方法」シナリオ）。  
* ファイルをXLSXワークブックとして保存し、下流の処理に備える。

**Prerequisites**  
* Python 3.8以上  
* `aspose-cells` Python パッケージ (`pip install aspose-cells`)  
* Python の `datetime` モジュールに関する基本的な知識  

---

## Pythonで条件付き書式を作成する方法

最初のステップは、書式設定ルールをホストするワークブックとワークシートを設定することです。

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Why this matters** – `Workbook` はすべてのExcel操作のエントリーポイントです。プログラムでワークブックを作成することで、手動の「File → New」手順を置き換え、レポートの自動化パイプラインを可能にします。

---

## 条件付き書式コレクションの準備 – 条件付き書式範囲の追加

次に、ルールを適用するセルブロックを定義します。この例では範囲は **I19:K20** です。

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explanation** – `conditional_formattings.add` はアドレス文字列に紐付いた新しいコレクションを登録します。最初の条件（`conds[0]`）は「デフォルト」スタイルとして機能し、後のルールは条件が満たされたときにそれを上書きします。

---

## TIME_PERIOD 条件の追加 – 日付をハイライトする方法

ここで、“Yesterday” の日付を識別し、ピンクで塗りつぶす実際のロジックを追加します。

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Why use TIME_PERIOD?** – Aspose.Cells は `YESTERDAY`、`TODAY`、`LAST_WEEK` などの組み込み列挙型を提供します。これらはセルの日付値を現在のシステム日付と比較して評価し、カスタム数式の必要性を排除します。

---

## サンプルデータの投入 – ルールのデモ

書式設定の動作を確認するために、ルールに一致する日付と一致しない日付を挿入します。

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Edge case note** – `TIME_PERIOD` ルールは*実際の*日付に対してのみ機能します。セルにテキスト（例: “N/A”）が含まれている場合、ルールは無視され、予期しない色変更を防ぎます。

---

## ワークブックの保存 – add conditional formatting python

最後に、ワークブックをディスクに書き出します。このファイルは任意のスプレッドシートプログラムで開き、色を確認できます。

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Expected result**  

| I19（緑 → ピンク） | J19（緑） | K19（緑） |
|--------------------|------------|------------|
| 2008/7/30（昨日） | – | – |
| **I20**: “Yesterday” ラベル | – | – |
| I21‑K21（緑） | – | – |

セル **I19** は、その日付が “Yesterday” 期間に一致するためピンクの背景で表示され、**K20** は緑のままです。

---

## よくある質問と実用的なヒント

* **組み込み期間の代わりにカスタム日付範囲を使用できますか？**  
  はい。`condition.time_period` を `condition.formula1 = "TODAY()-1"` に置き換え、`condition.type = FormatConditionType.FORMULA` を設定します。

* **ワークブックに既にデータがある場合はどうすればよいですか？**  
  条件付き書式コレクションを追加する前に、`worksheet.cells.import_data` を使用してデータを一括ロードします。

* **大規模シートでのパフォーマンスは？**  
  多数の条件を追加すると描画が遅くなる可能性があります。同じルールを持つセルは単一の範囲（例: “A1:C1000”）にまとめて、条件数を抑えましょう。

* **クロスプラットフォーム互換性は？**  
  生成されたXLSXファイルは Office Open XML 標準に従っているため、Windows、macOS、Linux のスプレッドシートアプリケーションで動作します。

---

## 結論

これで、Python を使用して Excel ワークブックに **条件付き書式を作成** する方法が分かりました。このチュートリアルでは、ワークブックの作成、**add conditional formatting range** の定義、**how to highlight dates** ルールの適用、ファイルの保存について、すべて Aspose.Cells が提供する **add conditional formatting python** アプローチで解説しました。

ここからは以下が可能です：

* 他の `TimePeriodType` 値（例: `TODAY`、`LAST_MONTH`）を使用してルールセットを拡張する。  
* 同一範囲に複数の条件を組み合わせ、よりリッチな視覚的ヒントを提供する。  
* このワークフローを自動レポートパイプラインやウェブサービスに統合する。

コーディングを楽しんでください。また、レポートのニーズに合わせてさまざまな色、範囲、日付ロジックを自由に試してみてください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Excel ワークブック Python 日付条件付き書式の作成](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [Python を使用して Excel で時間期間条件付き書式を適用する方法](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Excel ワークブック Python – スタイリングと条件付き書式の完全ガイド](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}