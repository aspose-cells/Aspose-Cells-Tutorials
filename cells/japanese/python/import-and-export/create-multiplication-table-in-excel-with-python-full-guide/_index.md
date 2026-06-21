---
category: general
date: 2026-06-21
description: Pythonを使ってExcelで掛け算表を作成します。lambda の使い方、makearray の使い方、Excel 配列の表示方法、Excel
  の値を Python で読み取る方法をステップバイステップのチュートリアルで学びましょう。
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: ja
og_description: Python を使用して Excel に掛け算表を作成します。このチュートリアルでは、lambda の使い方、makearray の利用方法、Excel
  配列の表示、そして Excel の値を効率的に読み取る方法を示します。
og_title: PythonでExcelに掛け算表を作成する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: PythonでExcelに掛け算表を作成する – 完全ガイド
url: /ja/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでExcelに掛け算表を作成する – 完全ガイド

Excelでセルを手動で入力せずに **create multiplication table** を作成する方法を考えたことはありませんか？ あなただけではありません。多くのレポートシナリオでは、5×5（またはそれ以上）の製品グリッドがすぐに必要ですが、手作業で作るのは時間の無駄です。  

このチュートリアルでは、その表を生成するクリーンな Python 主導の方法を順を追って説明し、`MAKEARRAY` 式で埋め込み、結果をスクリプトに取り込む方法を紹介します。途中で **how to use lambda**、**how to use makearray**、**display excel array**、**read excel values python** の使い方にも答え、すべてを一つの統合例で示します。

最後まで読むと、任意のブックで動作する再利用可能なスニペットが手に入り、このアプローチが高速で将来性がある理由が理解できるようになります。

## 必要なもの

- Python 3.8+（最新の安定版で問題ありません）
- `openpyxl` ライブラリ（または数式をサポートする任意の Excel 対応ライブラリ）
- Python の lambda 式に関する基本的な理解
- 特別な Excel アドインは不要です。ネイティブの `MAKEARRAY` 関数（Excel 365 で利用可能）が主要な処理を行います

これらが揃っていない場合は、`pip install openpyxl` を実行すればすぐに始められます。

## create multiplication table – 概要

基本的な考え方はシンプルです。新しいブックを作成し、5 × 5 の掛け算行列を構築する `MAKEARRAY` 式を書き込み、Excel に計算させ、最終的に結果の値を Python に読み戻します。

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

スクリプトを実行すると次が出力されます：

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

これが、Python だけで完全に生成された Excel の **create multiplication table** です。

### Python のループではなく `MAKEARRAY` を使う理由

- **Performance**: Excel が計算をネイティブに処理するため、大規模な行列ではより高速です。
- **Live updating**: 後で式のサイズを変更すると、シートが自動的に再計算されます。
- **Readability**: 式は意図（“配列を作成”）を直接表現し、Python コードをすっきり保ちます。

## Excel の数式で Python の lambda を使う方法

`MAKEARRAY` 呼び出しの `LAMBDA` 部分は Excel 側の無名関数であり、Python の lambda ではありません。それでも概念は同じで、`r`（行インデックス）と `c`（列インデックス）を受け取り `r*c` を返す小さなインラインロジックを定義します。

Excel の世界で **how to use lambda** に不慣れな場合、式内だけに存在するミニ関数と考えてください。別途関数を宣言する必要はありません。Python では単に文字列として埋め込むだけです：

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

この行は Excel に対し、*「5 × 5 のブロック内の各セルについて、行 × 列を計算する」* と指示しています。

lambda は Excel によって評価されるため、ここでは Python の lambda 構文を気にする必要はなく、Excel の構文だけを考えればよいです。

## makearray を使って配列を生成する方法

`MAKEARRAY` は比較的新しい Excel 関数ライブラリの追加機能で（2022 年以降の Microsoft 365 で利用可能）、`INDEX` と `ROW`/`COLUMN` の組み合わせといった従来のテクニックに取って代わります。シグネチャは次の通りです：

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – 必要な行数。
- **columns** – 必要な列数。
- **lambda** – `(row, column)` を受け取り値を返す Excel の LAMBDA。

例では古典的な掛け算表のために `5,5` を渡しましたが、これらの数値は簡単に変更できます：

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

これにより Python のループを使わずに 10 × 10 の表が得られます。これは **how to use makearray** が、ルックアップテーブル、ヒートマップ、財務スケジュールなど、任意の決定論的グリッドに対して利用できることを示しています。

## excel 配列を表示 – データを Python に取り込む

Excel が式を計算すると、結果の値は手動で入力したセルと同様にシートに格納されます。**display excel array** するために、範囲を反復し各行を出力します：

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

いくつかのヒント：

- `worksheet.cell(row, column).value` を使用すると、辞書形式のインデックスよりも大きな範囲を扱う際にやや高速です。
- より見やすい表にしたい場合は、`tabulate` や `pandas.DataFrame` を使って出力を整形すると良いでしょう。

以下は結果シートのスクリーンショットです（画像の alt テキストには SEO 用の主要キーワードが含まれています）：

![Python を使用して Excel で create multiplication table を作成するスクリーンショット](/images/multiplication-table-excel.png)

## read excel values python – 行列を抽出してさらに処理する

**display excel array** の後の次のステップは、これらの数値をデータ分析パイプラインに渡すことが多いです。ここで **read excel values python** が活躍します。印刷に使用した同じループを再利用して、リストのリスト、NumPy 配列、または Pandas DataFrame を作成できます：

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

出力：

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

これでプロットしたり CSV にエクスポートしたり、機械学習モデルに入力したりできる完全に型付けされた DataFrame が手に入りました。これでワークフローの **read excel values python** 部分が完了です。

## エッジケースと実用的なヒント

- **Formula recalculation**: 初回の `calculate_formula()` 呼び出し後にブックを変更した場合、再度呼び出す必要があります。さもなければキャッシュされた配列が古いまです。
- **Non‑365 Excel**: 古い Excel バージョンは `MAKEARRAY` をサポートしていません。その場合は Python で生成した表にフォールバックし、各セルを個別に書き込みます。
- **Large tables**: 約 100 × 100 を超える行列の場合、シート全体をメモリに読み込むのを避けるためにデータをストリーミングすることを検討してください。
- **Error handling**: 計算と読み取りのステップを `try/except` ブロックでラップし、`InvalidFileException` や `FormulaError` を捕捉します。

## 結論

ここでは、Python を使用して Excel で **create multiplication table** を作成し、**how to use lambda** と **how to use makearray** の力を活用する方法を示しました。**display excel array** の方法、**read excel values python** で値を読み戻す方法、そして結果を下流分析用の Pandas DataFrame に変換する方法をご覧いただきました。

さらに踏み込むには？掛け算ロジックを、距離行列や確率表、動的価格設定グリッドなど、より複雑なものに置き換えてみてください。同じパターンが適用できます：`MAKEARRAY` の一行、簡単な `calculate_formula()`、そしてデータを取り出すための数行の Python ループです。

このガイドが役立ったと思ったら、GitHub でスターを付けたり、チームメンバーと共有したり、あなたのユースケースをコメントで教えてください。コーディングを楽しみ、単一の式で Excel テーブルを生成する簡潔さを体感してください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells .NET で Excel ワークブックを作成・構成する方法：ステップバイステップガイド](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET チュートリアル：Excel ワークブックを簡単に作成・変更する方法](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [Aspose.Cells .NET を使用して Excel の名前付き範囲を作成・スタイル設定する方法 | ステップバイステップガイド](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}