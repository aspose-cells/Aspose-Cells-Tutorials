---
category: general
date: 2026-11-22
description: Aspose.Cells を使用して Excel テンプレートにデータを入力し、複数のシートを生成し、Aspose ワークブックを保存し、C#
  でマスタ‑ディテイル レポートを作成する。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: ja
lastmod: 2026-11-22
og_description: Aspose.CellsでExcelテンプレートにデータを入力し、複数シートを生成、Asposeブックとして保存し、単一のC#プログラムでマスタ‑ディテールレポートを構築する。
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Aspose.CellsでExcelテンプレートにデータを入力し、複数シートを生成
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  headline: How to populate Excel template and generate multiple sheets with Aspose.Cells
  type: TechArticle
- description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  name: How to populate Excel template and generate multiple sheets with Aspose.Cells
  steps:
  - name: What the resulting workbook looks like
    text: '| Sheet name | Content | |------------|----------| | **Master** | Header
      row with order summary (OrderId, Customer) | | **Details_1** | All `OrderLines`
      where `OrderId = 1` (Pen, Notebook) | | **Details_2** | All `OrderLines` where
      `OrderId = 2` (Pencil) |'
  - name: Expected output
    text: 'Open `MasterDetailResult.xlsx` and you will see:'
  - name: Next steps
    text: '* Explore **SmartMarkerOptions** such as `EnableFormulaCalculation` to
      evaluate formulas after data insertion. * Add charts to the master sheet and
      let the processor update series ranges automatically. * Combine this approach
      with **Aspose.Slides** to export the same data to PowerPoint presentations'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells を使用して Excel テンプレートにデータを入力し、複数のシートを生成する方法
url: /ja/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excelテンプレートにデータを入力し、Aspose.Cellsで複数シートを生成する方法

If you need to **populate Excel template** with dynamic data, this guide shows you a complete, ready‑to‑run solution. Using Aspose.Cells’ Smart Marker engine you can **generate multiple sheets**, save the **Aspose workbook**, and produce a full **master‑detail report** without manual copying or VBA macros.

The tutorial walks through every step—from preparing master‑detail collections to saving the final file—so you can copy the code into your own project and see immediate results.

## 前提条件

* .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
* Aspose.Cells for .NET がインストールされていること（`dotnet add package Aspose.Cells`）
* 基本的な C# 開発環境（Visual Studio、VS Code、Rider など）
* Smart Marker タグ（例: `&=Orders.OrderId`）や `&=OrderLines` でマークされた詳細テーブルを含む Excel テンプレート（`MasterDetailTemplate.xlsx`）

> **Pro tip:** テンプレートはプロジェクトと同じフォルダーに置くか、絶対パスを使用して `FileNotFoundException` を回避してください。

## ソリューションの概要

1. **master‑detail データコレクションの準備** – レポートに供給するソースオブジェクト。  
2. **Excel テンプレートの読み込み** – 既に Smart Marker プレースホルダーが含まれています。  
3. **`SmartMarkerProcessor` の作成** – マーカーを解釈します。  
4. **データの適用** と Aspose.Cells による **複数シートの自動生成** を行います。  
5. **Aspose workbook の保存** – ディスクに保存します。

Each step is explained below, with full code and expected output.

![Excelテンプレートにデータを入力する例](https://example.com/images/populate-excel-template.png "Excelテンプレートにデータを入力する例")

## 手順 1: master‑detail データコレクションの準備

Master‑detail レポートは、2 つの関連コレクション（注文リスト（マスター）と注文行リスト（詳細））に依存します。Smart Marker エンジンは `OrderId` フィールドで行をマッチングします。

```csharp
using System.Collections.Generic;

// Master collection – one record per order
var orders = new List<object>
{
    new { OrderId = 1, Customer = "Alice" },
    new { OrderId = 2, Customer = "Bob" }
};

// Detail collection – multiple rows per order
var orderLines = new List<object>
{
    new { OrderId = 1, Item = "Pen",      Qty = 10 },
    new { OrderId = 1, Item = "Notebook", Qty = 5  },
    new { OrderId = 2, Item = "Pencil",   Qty = 20 }
};
```

**この点が重要な理由:**  
`SmartMarkerProcessor` はテンプレート内の `&=Orders.OrderId` や `&=OrderLines.Item` といったマーカーをスキャンします。2 つの別々のコレクションを提供することで、Aspose.Cells はマスターレコードごとに新しいシートを自動的に作成し、対応する詳細行を埋め込みます。

## 手順 2: Smart Marker を含む Excel テンプレートの読み込み

テンプレートはレイアウト、書式設定、プレースホルダータグを保持しています。ファイル名とパスは正確に保ってください。

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**この点が重要な理由:**  
テンプレートを読み込むことで、プロセッサはデータ挿入位置を既に把握した workbook オブジェクトを取得します。フォント、罫線、数式などのすべての書式がそのまま保持されるため、生成されたレポートは追加のスタイリングコードなしでプロフェッショナルに見えます。

## 手順 3: SmartMarkerProcessor の作成

プロセッサはマーカーを実際の値に置き換えるエンジンです。

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**この点が重要な理由:**  
`SmartMarkerProcessor` は Smart Marker のロジックをワークブックの他の部分から分離し、データ適用後に同じワークブックを他の操作（例: チャート）に再利用できます。

## 手順 4: master‑detail データを適用し、複数シートを生成

ここでは 2 つのコレクションをプロセッサにバインドし、Aspose.Cells に各生成シートの名前付け方法を指示します。

```csharp
using Aspose.Cells.SmartMarkers;

// Combine the collections into an anonymous object matching the marker names
var data = new { Orders = orders, OrderLines = orderLines };

// Options let you control sheet naming and other behaviours
var options = new SmartMarkerOptions
{
    // {0} will be replaced by the master record index (1‑based)
    DetailSheetNewName = "Details_{0}"
};

// Apply the data – this step creates a new sheet for each order
processor.ApplyTemplate(data, options);
```

**この点が重要な理由:**  
`DetailSheetNewName` パターンは `Details_1`、`Details_2` などの名前のシートを作成し、マスターコレクションの各注文に対応させます。この自動シート生成は、ワークブックを手動でループせずに **複数シートを生成** する核心です。

### 生成されたワークブックのイメージ

| シート名 | 内容 |
|------------|----------|
| **Master** | 注文サマリー（OrderId、Customer）を含むヘッダー行 |
| **Details_1** | `OrderId = 1` のすべての `OrderLines`（Pen、Notebook） |
| **Details_2** | `OrderId = 2` のすべての `OrderLines`（Pencil） |

マスターシートは `Orders` を反復する Smart Marker テーブルを追加することでデータを入力できます。詳細シートはプロセッサによって自動的に作成されます。

## 手順 5: Aspose workbook の保存

最後に、入力済みのワークブックを新しいファイルに書き出します。

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**この点が重要な理由:**  
`Save` を呼び出すことで、メモリ上のワークブックが実際の `.xlsx` ファイルに書き込まれ、**Aspose workbook の保存** 手順が完了します。ファイルは Excel、Google Sheets、または OpenXML 形式をサポートする任意のビューアで開くことができます。

### 期待される出力

`MasterDetailResult.xlsx` を開くと、次のようになります：

* **Sheet “Master”** – Order 1（Alice）と Order 2（Bob）を一覧表示するテーブル。  
* **Sheet “Details_1”** – 2 行：Pen（10）と Notebook（5）。  
* **Sheet “Details_2”** – 1 行：Pencil（20）。

元のテンプレートのすべての書式（ヘッダーの色、列幅、数値形式）は保持されます。

## 一般的なエッジケースの処理

| 状況 | 推奨アプローチ |
|-----------|----------------------|
| **テンプレートが見つからない** | `new Workbook(...)` 呼び出しを `try/catch` でラップし、`FileNotFoundException` をログに記録します。 |
| **大規模データセット（10 000 行以上）** | シートあたりの行数が必要な場合は `SmartMarkerOptions.MaxRowsPerSheet` を増やすか、手動でページングします。 |
| **カスタムシート名** | `DetailSheetNewName = "Order_{0}_{1}"` のような書式文字列を使用し、`{1}` にマスターレコードのプロパティ（例: `Customer`）を指定します。 |
| **注文ごとの条件付き書式** | テンプレートにマーカー（例: `&=Orders.Status`）を参照する条件付き書式ルールを追加し、プロセッサに評価させます。 |

## 完全な実行可能プログラム

以下は、すべての要素を組み合わせた完全な C# コンソール アプリケーションです。`YOUR_DIRECTORY` を実際のフォルダー パスに置き換えてください。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class SmartMarkerDetailSheetDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Prepare master‑detail data collections
        // -------------------------------------------------
        var orders = new List<object>
        {
            new { OrderId = 1, Customer = "Alice" },
            new { OrderId = 2, Customer = "Bob" }
        };

        var orderLines = new List<object>
        {
            new { OrderId = 1, Item = "Pen",      Qty = 10 },
            new { OrderId = 1, Item = "Notebook", Qty = 5  },
            new { OrderId = 2, Item = "Pencil",   Qty = 20 }
        };

        // -------------------------------------------------
        // Step 2: Load the template workbook that contains smart markers
        // -------------------------------------------------
        string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor to handle the template
        // -------------------------------------------------
        var processor = new SmartMarkerProcessor(workbook);

        // -------------------------------------------------
        // Step 4: Apply the master‑detail data and generate multiple sheets
        // -------------------------------------------------
        var data = new { Orders = orders, OrderLines = orderLines };
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Details_{0}"
        };

        processor.ApplyTemplate(data, options);

        // -------------------------------------------------
        // Step 5: Save the populated Aspose workbook
        // -------------------------------------------------
        string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
        workbook.Save(resultPath);

        Console.WriteLine($"Report generated successfully: {resultPath}");
    }
}
```

プログラムを実行します（`dotnet run` または Visual Studio の `Ctrl+F5`）。完了したら `MasterDetailResult.xlsx` を開き、**Excelテンプレートにデータを入力** が期待通りの master‑detail レポートと **複数シート** を生成したことを確認してください。

## 結論

これで、Aspose.Cells を使用して **Excelテンプレートにデータを入力**、**複数シートを生成**、**Aspose workbook を保存**、そして数行の C# で堅牢な **master‑detail レポート** を作成する方法が分かりました。Smart Marker エンジンにより手動ループが不要になり、書式が保持され、大規模データセットにも容易にスケールします。

### 次のステップ

* `EnableFormulaCalculation` などの **SmartMarkerOptions** を調査し、データ挿入後に数式を評価します。  
* マスターシートにチャートを追加し、プロセッサにシリーズ範囲を自動更新させます。  
* この手法を **Aspose.Slides** と組み合わせて、同じデータを PowerPoint プレゼンテーションにエクスポートします。

さまざまなテンプレートレイアウト、カスタムシート名パターン、追加の詳細コレクションを自由に試してみてください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [C# でマスターディテイルレポートを作成 – SmartMarker を使用した Excel テンプレートへのデータ入力](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [C# と Aspose.Cells を使用してテンプレートから Excel を生成する方法](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Excel テンプレートへのデータ入力](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}