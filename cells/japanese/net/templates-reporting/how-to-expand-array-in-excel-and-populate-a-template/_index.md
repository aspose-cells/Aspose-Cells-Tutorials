---
category: general
date: 2026-09-18
description: EXPAND関数を使用してExcelで配列を拡張する方法、Excelテンプレートにデータを入力する方法、そしてC#で動的範囲のExcelワークシートを作成する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: ja
lastmod: 2026-09-18
og_description: EXPAND関数でExcelの配列を拡張し、Excelテンプレートにデータを入力し、C#コードを使用して動的範囲のExcelソリューションを構築する方法。
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Excelで配列を拡張し、テンプレートに入力する方法
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Excelで配列を拡張し、テンプレートにデータを入力する方法
url: /ja/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excelで配列を拡張しテンプレートにデータを入力する方法

Excelで **how to expand array** を行い、事前にデザインされたテンプレートにデータを埋め込む必要がある場合、本ガイドではエンドツーエンドの完全なソリューションを示します。`EXPAND` 関数と Aspose.Cells の Smart Markers を組み合わせることで、単一セル参照を 5 × 5 の範囲に変換し、`{IsActive}` などのマーカーをリアルタイムデータに自動置換できます。

**populate excel template** の方法、**dynamic range excel** の作成方法、C# プロジェクトでの **use expand function** の正しい使い方を学びます。チュートリアルの最後には、`.xlsx` ファイルを読み込み、配列数式を展開し、Smart Markers を適用して結果を保存する実行可能なプログラムが完成します。

## 前提条件

* .NET 6.0 以降（コードは .NET Core 3.1+ でも動作します）
* Aspose.Cells for .NET（NuGet パッケージ `Aspose.Cells`）
* プレースホルダー数式セル（例: `B2`）と Smart Marker（例: `{IsActive}`）を含む Excel ブック
* C# と Excel 数式の基本的な知識

> **プロのコツ:** `EXPAND` 関数は Microsoft 365 の Excel と Excel 2021 以降でのみ利用可能です。古いバージョンでは `#NAME?` エラーが返されます。

## 手順 1: EXPAND 関数で配列を拡張する方法

最初のステップはブックを読み込み、単一のソースセルを大きな行列に変換する `EXPAND` 数式を書き込むことです。  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

この処理が重要な理由: `EXPAND` を使用すれば、行や列に数式を手動でコピーする必要がなくなります。ソースセル（`A2`）が変更されると、5 × 5 のブロック全体が自動的に更新され、データ変更に応答する **dynamic range excel** が実現します。

## 手順 2: Smart Markers を使って Excel テンプレートにデータを入力する

Smart Markers を利用すると、テンプレート内にプレースホルダーを埋め込み、C# オブジェクトの値で置換できます。これが **populate excel template** をセル単位でコードを書くことなく実現する最も便利な方法です。

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

`SmartMarkersProcessor().Apply` 呼び出しはシート全体を走査し、`{IsActive}` を検出してブール値を注入します。数式は自動的に `"Active"` または `"Inactive"` に評価されます。

## 手順 3: 展開された範囲と入力結果を検証する

`EXPAND` 数式と Smart Markers の両方を適用した後、数セルをプログラムで読み取り、期待通りに動作したかを確認できます。

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

プログラムを実行すると、`A2` の元の値（または配列結果）と、`IsActive` フラグに応じた **Active** または **Inactive** が出力されます。

## 手順 4: ブックを保存 – 最終出力

最後に、変更されたブックをディスクに書き出します。このステップで、読み込み → 拡張 → データ入力 → 永続化までの全フローが示されます。

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

保存された `output.xlsx` には、`EXPAND` 数式で生成された 5 × 5 行列と `{IsActive}` の値を反映したセルが含まれます。Excel でファイルを開くと、動的範囲が実際に機能していることが確認できます。

## エッジケースとベストプラクティス

| Situation                              | Recommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Excel version does not support `EXPAND`| 従来の `=OFFSET` または `=INDEX` 数式にフォールバックするか、Office 365 にアップグレードしてください。 |
| Need to expand to a variable size      | 真の動的化のために `EXPAND` 内で `ROWS(source)` と `COLUMNS(source)` を使用します。   |
| Multiple Smart Markers in the same sheet| 複合データオブジェクトを渡して `SmartMarkersProcessor().Apply` を一度だけ呼び出します。      |
| Large workbooks ( > 10 000 rows)       | 数式を書き込む間は計算を無効化します（`workbook.Settings.CheckFormula = false`）。 |

## 完全動作サンプル

以下は新しいコンソールプロジェクトにコピー＆ペーストできる、完全な自己完結型プログラムです。

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**プログラム実行時の期待出力**（`A2` に数値 `42` が入っていると仮定）:

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

`output.xlsx` を開くと、`A2` から導出された値で埋められた 5 × 5 のブロックと、**Active** と表示されたセルが確認できます。

## 結論

これで **how to expand array** を `EXPAND` 関数で実現し、Smart Markers を使って **populate excel template** を行い、ソースデータに自動で適応する **dynamic range excel** を構築する方法が分かりました。サンプルは実務の C# 自動化シナリオで **use expand function** と **expand array formula** を正しく使用する手順も示しています。

次のステップとして以下を検討してください。

* 固定の `5,5` 次元を `ROWS(A2:A10), COLUMNS(A2:E2)` に置き換えて、真に可変な範囲にする。
* 複数の Smart Markers を組み合わせて、従業員リストや売上表などの完全レポートを生成する。
* Aspose.Cells のスタイリング API を活用し、展開されたブロックを自動で書式設定する。

さまざまなソース配列、マーカー名、ブックレイアウトで実験してみてください。コーディングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に密接に関連するトピックを扱っており、ステップバイステップのコード例と解説が含まれています。これらを活用して、API の追加機能を習得したり、別の実装アプローチを自プロジェクトに取り入れたりしてください。

- [Export Data to Excel: Populate a Template from an Array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [How to create array in Excel with C# – Step-by-Step Guide](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}