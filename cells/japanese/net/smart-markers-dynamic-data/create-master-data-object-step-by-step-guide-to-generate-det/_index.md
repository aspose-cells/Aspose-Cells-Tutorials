---
category: general
date: 2026-02-14
description: C#でマスターデータオブジェクトを作成し、簡単に詳細シートを生成します。実践的なコード例でSmartMarkerのフルワークフローを学びましょう。
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: ja
og_description: C#でマスターデータオブジェクトを作成し、SmartMarkerで詳細シートを生成します。すぐに実行できるソリューションのための詳細なチュートリアルをご覧ください。
og_title: マスターデータオブジェクトの作成 – 完全ガイド
tags:
- C#
- SmartMarker
- Excel Automation
title: マスターデータオブジェクトの作成 – 詳細シート作成のステップバイステップガイド
url: /ja/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# マスターデータオブジェクトの作成 – 完全チュートリアル

Excel ワークシート用に **create master data object** が必要だったことはありませんか？しかし、SmartMarker の詳細シートにどう結びつけるか分からずに困ったことはありませんか。多くのレポートシナリオでは、マスターオブジェクトが動的な詳細シートを駆動し、配線を正しく行うのは絵のないパズルを組み立てるように感じられます。

このガイドでは、マスターデータオブジェクトの構築、SmartMarker オプションで **generate detail sheet** を設定し、最終的にプロセッサを実行するまでの全工程を順に解説します。最後には、GcExcel ライブラリを使用する任意の .NET プロジェクトに貼り付けられる実行可能なコードスニペットが手に入ります。

## 必要な環境

- .NET 6+（または .NET Framework 4.7.2）で `GcExcel.dll` を参照できる環境
- 基本的な C# の知識（変数、匿名型、オブジェクトイニシャライザ）
- `{{OrderId}}` などの SmartMarker タグと、明細行用テーブルが既に配置された Excel ブック
- Visual Studio、Rider、またはお好みのエディタ

以上だけです。GcExcel 本体以外に追加の NuGet パッケージは不要です。

## Step 1: Create the Master Data Object

まず最初に、SmartMarker タグが期待する構造に合わせた **create master data object** を作成します。これはメモリ上の小さなレポートモデルと考えてください。

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

ここで匿名型を使用する理由は何でしょうか？フルクラスを宣言せずに軽量なコンテナを定義できるため、デモや形が変わらないケースに最適です。後で再利用可能なモデルが必要になったら、`var` を正式な POCO に置き換えるだけです。

> **Pro tip:** プロパティ名（`OrderId`, `Product`, `Quantity`）はワークシート上のプレースホルダーと完全に同一にしてください。SmartMarker は大文字小文字を区別せずにマッチします。

## Step 2: Configure SmartMarker Options to Generate a Detail Sheet

次に、行アイテムテーブル用に別シートを作成したい旨を SmartMarker に指示します。ここで **generate detail sheet** キーワードが登場します。

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

`DetailSheetNewName` パターンは波括弧で囲んだプレースホルダーを使用し、実行時に置換されます。今回の例ではシート名は `Order_1` になります。複数の注文をループ処理すると、各注文ごとにタブが作成され、会計担当者が期待する形になります。

## Step 3: Run the SmartMarker Processor

データとオプションの準備が整ったら、対象ワークシートに対してプロセッサを呼び出します。

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

内部では SmartMarker がシート上のタグを走査し、`orderData` の値を注入します。`DetailSheet` が `true` のため、テンプレートが `Order_1` という新しいシートにクローンされます。すべての明細行が詳細領域に展開され、テンプレートで設定した書式がそのまま保持されます。

### 完全動作サンプル

以下はコンソールアプリケーションの自己完結型サンプルです。テンプレートブック（`Template.xlsx`）を開き、上記 3 ステップを実行し、結果を `Result.xlsx` として保存します。このコードを新しいコンソールプロジェクトに貼り付けて **F5** を押すだけで動作します。

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### 期待される出力

- **Result.xlsx** に `Order_1` というシートが作成されます。
- セル `A1`（`{{OrderId}}` を配置した場所）には `1` が表示されます。
- SmartMarker ブロックから始まるテーブルには次の 2 行がリストされます：

  | 商品 | 数量 |
  |------|------|
  | A    | 2    |
  | B    | 5    |

ファイルを開くと、テンプレートで設定した罫線、フォント、条件付き書式などがすべて保持されていることが確認できます。

## Common Questions & Edge Cases

### 複数の注文がある場合は？

マスターオブジェクトをコレクションでラップすれば、SmartMarker が自動的に繰り返し処理します。

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

各注文ごとにシート（`Order_1`, `Order_2`, …）が生成され、プロセッサは外側の配列をマスターコレクションとして扱います。

### シートの挿入位置を制御したい場合は？

`smartMarkerOptions.DetailSheetInsertIndex = 2;` と設定すれば、2 番目のタブの後に新シートが挿入されます。あるいは `DetailSheetInsertAfter = "Summary"` を使用して、名前付きシートの後に挿入できます。

### 特定の実行で詳細シートを無効にしたい場合は？

`DetailSheet = false;` に切り替えるだけです。SmartMarker は明細行をマスタータグがある同一シートに書き込みます。

### 大規模データセットはどう扱う？

SmartMarker はデータを効率的にストリーミングしますが、数十万行を超えると Excel の 1,048,576 行制限に達する可能性があります。その場合はマスター記録を複数に分割するか、CSV へのエクスポートを検討してください。

## Visual Overview

![SmartMarker を使用してマスターデータオブジェクトを作成し、詳細シートを生成するフロー](/images/smartmarker-flow.png)

*この図は C# のマスターオブジェクト → SmartMarker オプション → ワークシート処理 → 新規詳細シート という流れを示しています。*

## Conclusion

これで C# で **create master data object** を作成し、SmartMarker に **generate detail sheet** を自動的に行わせる方法が分かりました。データ → オプション → プロセッサという 3 ステップのパターンは、GcExcel を使ったほとんどの Excel 自動化シナリオを網羅します。

今後は次のようなことに挑戦してみてください：

- 各詳細シートにヘッダー／フッターデータを追加する
- 注文ステータスに応じた条件付き書式を適用する
- `workbook.SaveAsPdf(...)` を使って生成ブックを PDF にエクスポートする

自由に試行錯誤し、壊してからまた組み立て直すことで、ワークシート自動化のスキルが最速で身につきます。コーディングを楽しんでください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}