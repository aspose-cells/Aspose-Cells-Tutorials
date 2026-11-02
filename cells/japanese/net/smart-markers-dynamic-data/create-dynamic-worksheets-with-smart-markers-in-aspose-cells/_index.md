---
category: general
date: 2026-03-25
description: スマートマーカーを使用して動的なワークシートを作成する方法を学びましょう。aspose.cells を使用したステップバイステップのガイドで、完全な
  C# コード、ヒント、エッジケースの処理が含まれています。
draft: false
keywords:
- create dynamic worksheets
- smart markers aspose.cells
language: ja
og_description: スマートマーカー aspose.cells を使用して、動的なワークシートを簡単に作成できます。C# で動的な Excel 生成をマスターするための完全なチュートリアルをご覧ください。
og_title: 動的ワークシートの作成 – スマートマーカー Aspose.Cells ガイド
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cellsでスマートマーカーを使用して動的なワークシートを作成する
url: /ja/net/smart-markers-dynamic-data/create-dynamic-worksheets-with-smart-markers-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells のスマートマーカーで動的ワークシートを作成

データに基づいて自動的に拡張する **動的ワークシートを作成** ことを考えたことがありますか？ 静的な Excel テンプレートを見て「もっと賢い方法があるはずだ」と思ったことがあるかもしれません。 良いニュースは、**smart markers aspose.cells** を活用すれば、瞬時に **動的ワークシートを作成** できることです。  

このチュートリアルでは、データ ソースの準備から SmartMarker プロセッサの設定まで、必要なすべてを順を追って解説します。コードはそのまま実行可能で、説明は明快です。最後まで読むと、数行コードをプロジェクトに追加するだけで、Aspose.Cells がリアルタイムに完璧な形状の詳細シートを生成する様子を確認できます。

## 学習内容

- `DataTable`、`List<T>`、または任意の列挙可能ソースに基づいて増減する **動的ワークシートを作成** する方法。  
- テンプレート駆動の Excel 生成において、**smart markers aspose.cells** が秘密の要素である理由。  
- 一般的な落とし穴（null データ、名前の衝突）とその回避方法。  
- Visual Studio 2022 にコピー＆ペーストしてすぐに実行できる正確な C# コード。  

> **Prerequisite:** Visual Studio 2022（またはそれ以降）と .NET 6+、有効な Aspose.Cells ライセンス（または無料評価版）が必要です。他のサードパーティ ライブラリは不要です。

![Create dynamic worksheets example](image.png "Screenshot showing dynamic worksheets generated with smart markers aspose.cells")

## ステップ 1 – 動的ワークシート用データソースの準備

最初に必要なのは、Aspose.Cells がテンプレートにマージできるデータソースです。`IEnumerable` を実装していれば何でも機能しますが、最も一般的な選択肢は `DataTable` と `List<T>` です。

```csharp
using System;
using System.Data;
using System.Collections.Generic;
using Aspose.Cells;

namespace ExcelDynamicDemo
{
    class Program
    {
        static void Main()
        {
            // Example 1: DataTable
            DataTable table = new DataTable("Orders");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Price", typeof(double));

            table.Rows.Add("Apple", 10, 0.5);
            table.Rows.Add("Banana", 5, 0.3);
            table.Rows.Add("Cherry", 20, 0.2);

            // Example 2: List<T>
            var orders = new List<Order>
            {
                new Order { Product = "Desk", Quantity = 2, Price = 150.0 },
                new Order { Product = "Chair", Quantity = 5, Price = 45.0 }
            };

            // Choose which one to feed into the processor
            object data = table; // or: object data = orders;
```

**Why this matters:**  
`null` 参照を渡すと、プロセッサは例外をスローし、**動的ワークシートを作成** の試みが黙って失敗します。続行する前に必ずソースを検証してください。

## ステップ 2 – スマートマーカーを含むテンプレート ワークシートの読み込み

次に、スマートマーカーを含むブックを取得します。通常は、Excel で作成した既存の `.xlsx` ファイルから開始します。

```csharp
            // Load the template workbook (ensure the file exists)
            string templatePath = @"Templates\DynamicTemplate.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Assume the first worksheet contains the smart markers
            Worksheet ws = workbook.Worksheets[0];
```

**Tip:**  
テンプレートをプロジェクト内の `Templates` フォルダーに置いてください。これにより環境間でパスが安定し、絶対パスをハードコーディングせずに **動的ワークシートを作成** できます。

## ステップ 3 – 細かな制御のために SmartMarkerOptions を設定

`SmartMarkerOptions` を使用すると、Aspose.Cells がマーカーを扱う方法を微調整できます。動的シート作成の場合、詳細シートの命名パターンを制御したいでしょう。

```csharp
            // Create options object
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();

            // Optional: turn on advanced processing if you have nested collections
            smartMarkerOptions.Advanced = true;
```

**Explanation:**  
`Advanced = true` を設定すると、ネストされたループなどの複雑なシナリオをプロセッサが処理できるようになり、マスタ‑詳細関係を含む **動的ワークシートを作成** する際に頻繁に必要となります。

## ステップ 4 – 詳細シートの命名パターンを定義

`DetailSheetNewName` プロパティは、新しく生成されたシートの名前付け方法を決定します。Aspose.Cells は自動的にインクリメンタルな番号を付加します。

```csharp
            // Define the base name for each generated detail sheet
            smartMarkerOptions.DetailSheetNewName = "Detail"; // → Detail1, Detail2, …
```

**Pro tip:**  
多数の詳細シートが予想される場合は、`"OrderDetail"` のような説明的なベース名を使用すると、結果のタブが自明になります。

## ステップ 5 – SmartMarker プロセッサを実行して **動的ワークシートを作成**

いよいよマジックが発動します。プロセッサはデータをテンプレートにマージし、必要に応じてシートを生成します。

```csharp
            // Run the processor
            ws.SmartMarkerProcessor.Process(data, smartMarkerOptions);

            // Save the result
            string outputPath = @"Output\DynamicReport.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Dynamic workbook saved to {outputPath}");
        }
    }

    // Simple POCO for List<T> example
    public class Order
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double Price { get; set; }
    }
}
```

**What you’ll see:**  
`data` に 3 行が含まれている場合、Aspose.Cells は `Detail1`、`Detail2`、`Detail3` という名前の 3 つの新しいワークシートを生成します。各シートはテンプレートに配置したスマートマーカー（例：`&=Product`、`&=Quantity`、`&=Price`）で埋められます。これが、ループロジックを書かずに **動的ワークシートを作成** する核心です。

## エッジケースとよくある質問

### データソースが空の場合は？

`data` が空のコレクションの場合、プロセッサは依然として単一の詳細シート（`Detail1` と命名）を作成しますが、テンプレートの静的部分のみが含まれます。不要なシートを防ぐために、`Process` を呼び出す前にコレクションのカウントを確認してください。

```csharp
if ((data as IEnumerable<object>)?.Cast<object>().Any() == true)
{
    ws.SmartMarkerProcessor.Process(data, smartMarkerOptions);
}
else
{
    Console.WriteLine("No data to merge – skipping dynamic sheet creation.");
}
```

### 生成されるシートの順序を制御できますか？

はい。シートはデータが現れる順序で作成されます。カスタムソートが必要な場合は、プロセッサに渡す前に `DataTable` または `List<T>` をソートしてください。

### **smart markers aspose.cells** は単純なセル数式とどう違うのですか？

スマートマーカーは Aspose.Cells エンジンが実行時に置換するプレースホルダーであり、数式は Excel 自体が評価します。スマートマーカーを使用すると、ループ、条件分岐、さらにはサブテンプレートさえもブック内に直接埋め込むことができ、**動的ワークシートの作成** に最適です。

## 完全な動作例のまとめ

以下は、全体のワークフローを示す、コピー＆ペースト可能な完全なプログラムです：

```csharp
using System;
using System.Data;
using System.Collections.Generic;
using Aspose.Cells;

namespace ExcelDynamicDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Prepare data ----------
            DataTable table = new DataTable("Orders");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Price", typeof(double));
            table.Rows.Add("Apple", 10, 0.5);
            table.Rows.Add("Banana", 5, 0.3);
            table.Rows.Add("Cherry", 20, 0.2);
            object data = table; // Or use a List<Order> instead

            // ---------- Step 2: Load template ----------
            string templatePath = @"Templates\DynamicTemplate.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet ws = workbook.Worksheets[0];

            // ---------- Step 3: Set options ----------
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                Advanced = true,
                DetailSheetNewName = "Detail"
            };

            // ---------- Step 4: Process and save ----------
            ws.SmartMarkerProcessor.Process(data, smartMarkerOptions);
            string outputPath = @"Output\DynamicReport.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Dynamic workbook saved to {outputPath}");
        }
    }

    public class Order
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double Price { get; set; }
    }
}
```

このプログラムを実行すると、`Output\DynamicReport.xlsx` ファイルが生成され、ソーステーブルの各行に対して個別の `Detail` シートが作成されます。これは **smart markers aspose.cells** を使用して **動的ワークシートを作成** する方法そのものです。

## 結論

これで、Aspose.Cells のスマートマーカーを使用して **動的ワークシートを作成** するための、確実なエンドツーエンドの手順が手に入りました。データソースの準備、マーカーが豊富なテンプレートの読み込み、`SmartMarkerOptions` の調整、プロセッサの呼び出しにより、ライブラリにすべての重い処理を任せられます。  

ここから

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}