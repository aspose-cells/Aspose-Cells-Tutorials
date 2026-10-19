---
category: general
date: 2026-08-24
description: Aspose.Cells を使用して Python で条件付き書式ルールを作成し、日付をハイライトし、列の自動調整と背景色の書式設定を行う。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: ja
lastmod: 2026-08-24
og_description: Aspose.Cells を使用して Python で条件付き書式ルールを作成します。数行のコードで日付をハイライトし、背景色を設定し、列を自動調整する方法を学びましょう。
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Pythonで日付に条件付き書式ルールを作成する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Pythonで日付の条件付き書式ルールを作成する方法
url: /ja/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python で日付に基づく条件付き書式ルールを作成する方法

日付に反応する **条件付き書式ルールを作成** したい場合は、Aspose.Cells for Python を使った手順をこのガイドでご紹介します。レポート用ダッシュボードや自動化スプレッドシートを作成する際に、昨日の日付をハイライトし、カスタム背景色を適用し、**列幅を自動調整** して見栄えを整える方法が分かります。

このチュートリアルでは **日付による条件付き書式** を取り上げ、**背景色の条件付き書式** をデモし、最終的にブックを XLSX ファイルとして保存します。最後まで読むと、任意の **日付ベースの条件付き書式** に再利用できるヘルパーが手に入ります。

## 学べること

* Aspose.Cells を使ってブックとワークシートを設定する方法  
* 任意のセル範囲に **日付ベースの条件付き書式** を追加するヘルパー関数の作成方法  
* ルールを評価できるようにサンプル日付をセルに入力する方法  
* **列幅を自動調整** してコンテンツを見やすくする方法  
* ブックを保存し、ハイライトされたセルを確認する手順  

前提条件は、`aspose-cells` パッケージがインストールされた Python 環境が動作していることだけです。

## 前提条件

| 要件 | 詳細 |
|------|------|
| Python | 3.8 以上 |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Excel の基本概念の知識 | ワークシート、セル、書式設定 |
| 任意: IDE (VS Code, PyCharm など) | Python スクリプトを実行できるエディタ |

## 手順 1: ブックを作成し、最初のワークシートを取得する

最初のステップは **条件付き書式ルール** 用のオブジェクト、`Workbook` とデフォルトの `Worksheet` を **作成** することです。これらのオブジェクトが以降のすべての操作のエントリーポイントになります。

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*ポイント:* `Workbook` は Excel ファイル全体を保持し、`Worksheet` はセルやスタイル、**日付による条件付き書式** を適用する場所です。これらがなければ、残りのコードは実行できません。

## 手順 2: TIME_PERIOD 条件付き書式を追加するヘルパーを作成する

各範囲ごとに同じボイラープレートを繰り返すのは非効率です。そこでロジックをヘルパー関数にカプセル化します。この関数は `TimePeriodType`（例: Yesterday、Today、LastWeek）に基づきセルの **背景色の条件付き書式** を設定します。

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*ヘルパーを使う理由:* **日付ベースの条件付き書式** ロジックを分離でき、コードが読みやすく、テストしやすく、複数シートやプロジェクトで再利用しやすくなります。

## 手順 3: 特定の範囲に条件付き書式ルールを適用する

ヘルパーを使って「Yesterday」に該当するセルをハイライトします。これが **条件付き書式ルールを作成** する核心部分です。

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

ブックを開くと、`I19:K20` のうち日付が昨日と一致するセルはピンクで塗りつぶされます（ヘルパーで設定したスタイル）。`bg_color` 引数を使うと、条件付き色の背後にデフォルト背景色をレイヤーできることを示しています。

## 手順 4: サンプル日付で範囲にデータを入力する

条件付きルールは、ワークシートに条件を満たすデータが入って初めて可視化されます。ここでは「昨日」に一致する日付と、期間外の日付の 2 つを挿入します。

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*ポイント:* `datetime` オブジェクトを使用することで、Excel が値を真の日付として認識し、**日付による条件付き書式** が正しく機能します。数値形式 (`30`) を指定すると、セルが認識しやすい日付として表示されます。

## 手順 5: 列幅を自動調整し、ブックを保存する

データと書式が設定されたら、**列幅を自動調整** して日付がすべて見えるようにします。その後、ファイルをディスクに書き出します。

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

`auto_fit_column` 呼び出しは、列 12（Excel の列 **L** に相当）で最も長いコンテンツを調べ、幅を拡張します。この小さな手順により日付が切れずに表示され、**背景色の条件付き書式** がはっきりと見えるようになります。

### 期待される結果

`TimePeriodDemo.out.xlsx` を開くと以下のようになります。

| I19（日付） | I20（ラベル） | K20（日付） |
|------------|--------------|------------|
| 2008年7月30日（ピンクでハイライト） | 昨日 | 2008年8月3日（ハイライトなし） |

* `I19` のセルは、**条件付き書式ルール** が `YESTERDAY` 期間にマッチしたためピンク背景になります。  
* 他のセルはデフォルト背景（または指定した `medium_sea_green`）のままです。  
* 列 **L** は自動的に幅が広げられ、日付がすべて読み取れるようになります。

## よくあるバリエーションとエッジケース

| 状況 | コードの適応方法 |
|------|-------------------|
| **「昨日」ではなく「今日」をハイライトしたい** | `TimePeriodType.YESTERDAY` を `TimePeriodType.TODAY` に置き換える。 |
| **別の背景色を使用したい** | `condition.style.background_color = Color.pink` を任意の `Color`（例: `Color.light_sky_blue`）に変更する。 |
| **非連続範囲にルールを適用したい** | `add_time_period_condition` を複数回呼び出し、異なる `cell_range` 文字列（例: `"A1:A10", "C1:C10"`）を渡す。 |
| **既存のブックで作業したい** | 新規作成の代わりに `Workbook("myfile.xlsx")` でファイルをロードする。 |
| **同一範囲に複数の日付ベース条件を設定したい** | 最初の `add_time_period_condition` 呼び出し後に、`conditions.add_condition(FormatConditionType.TIME_PERIOD)` を使って別の条件を追加し、異なる `time_period` を設定する。 |

## 結論

これで **日付に反応する条件付き書式ルール** を作成し、**背景色の条件付き書式** を適用し、Aspose.Cells for Python で **列幅を自動調整** する方法が分かりました。ヘルパー関数にロジックを抽象化したので、`Yesterday`、`LastWeek`、カスタム期間など、あらゆる **日付による条件付き書式** シナリオで同じパターンを再利用できます。

次に試したいこと:

* 日付ルールに **アイコンセット** や **データバー** を追加する  
* データベースから日付を取得して動的レポートを生成する  
* 同一シートに複数の **日付ベースの条件付き書式** を組み合わせる  

さまざまな色、期間、範囲で実験し、プロジェクトに最適な形にカスタマイズしてください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを探求したりするのに役立ちます。

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}