---
category: general
date: 2026-02-14
description: SmartMarkerで請求書作成を自動化：ワークシートの繰り返し方法、動的に名前を付ける方法、そして数分で動的ワークシート命名をマスターしましょう。
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: ja
og_description: SmartMarkerで請求書作成を自動化します。このガイドでは、ワークシートを繰り返し使用する方法、動的に名前を付ける方法、そして動的なワークシート命名をマスターする方法を紹介します。
og_title: 請求書生成の自動化 – 動的シート名付けと繰り返し
tags:
- C#
- SmartMarker
- Excel Automation
title: 請求書生成の自動化 – C#での動的ワークシート命名と繰り返し
url: /ja/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 請求書自動生成 – 動的ワークシート命名と繰り返し（C#）

手動でシートをコピーせずに **請求書の自動生成** を行いたいと考えたことはありませんか？同じように、請求書ごとに別々のワークシートが必要で、シート名を注文番号に合わせたいという壁にぶつかる開発者は多いです。このチュートリアルでは、SmartMarker の `SmartMarkerProcessor` を使用してその問題を解決し、**ワークシートを動的に命名** する方法と **レコードごとにワークシートを繰り返す** 方法を紹介します。最後まで読めば、各請求書がそれぞれの名前付きタブに配置されたブックを生成する、実行可能な C# サンプルが手に入ります。

データソースから注文を取得し、`SmartMarkerOptions` で動的ワークシート命名を設定するまでの手順をすべて解説します。外部ドキュメントは不要です。C# の基本知識と Aspose.Cells ライブラリ（または SmartMarker 対応エンジン）への参照があれば始められます。

---

## 作成するもの

- 注文オブジェクトのコレクションを取得する
- SmartMarker を **ワークシートを繰り返す** 設定にする
- `{OrderId}` プレースホルダーを使って **動的ワークシート命名** を適用する
- 各タブが `Invoice_12345`、`Invoice_67890` などと命名された Excel ファイルを生成する
- ワークブックを開いて出力を確認する

---

## 前提条件

- .NET 6.0 以上（コードは .NET 5+ でもコンパイル可能）
- Aspose.Cells for .NET（または SmartMarker を実装する任意のライブラリ）。NuGet でインストール：

```bash
dotnet add package Aspose.Cells
```

- 基本的な `Order` クラス（独自の DTO に置き換えても可）

---

## 手順 1: プロジェクトとモデルの設定

まず、コンソール アプリを新規作成し、注文を表すデータモデルを定義します。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **プロのコツ:** デモ用にはモデルをシンプルに保ちましょう。後から明細行や税情報などを追加できます。

---

## 手順 2: Excel テンプレートの準備

SmartMarker はテンプレート ワークブックに対して動作します。`InvoiceTemplate.xlsx` という名前のファイルを作成し、シート名を `InvoiceTemplate` にします。セル **A1** に次のような SmartMarker プレースホルダーを配置します。

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

セルの書式設定は自由です。太字ヘッダーや通貨書式など、好きなように整えてください。ファイルはプロジェクトのルート フォルダーに保存します。

> **なぜテンプレートが必要か？** デザインとロジックを分離できるため、デザイナーはコードに触れずにレイアウトを調整できます。

---

## 手順 3: SmartMarker オプションの設定 – 繰り返しとシート名

ここで、SmartMarker にテンプレート シートを **各注文ごとに繰り返す** と同時に、コピーしたシートに注文 ID を含む名前を付けるよう指示します。これが **動的ワークシート命名** の核心です。

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### 動作概要

- **`RepeatWorksheet = true`** は、`orders` コレクションの要素数だけ元シートを複製するようエンジンに指示します。これが **ワークシートを繰り返す** 要件を満たします。
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** はテンプレート文字列で、`{OrderId}` が現在処理中の注文 ID に置き換えられます。これが **ワークシートの命名方法** と **動的ワークシート命名** の答えです。
- プロセッサは各注文のフィールド（`{{OrderId}}`、`{{Customer}}` など）を複製シートにマージし、完全な請求書を生成します。

---

## 手順 4: アプリケーションの実行と出力確認

コンソール アプリをビルドして実行します。

```bash
dotnet run
```

コンソールに成功メッセージが表示されるはずです。`GeneratedInvoices.xlsx` を開くと、次の 3 つのタブが確認できます。

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

各シートにはプレースホルダーが注文データで置き換えられています。テンプレートでデザインしたレイアウトがそのまま保持され、**請求書自動生成** がエンドツーエンドで機能していることが分かります。

### 期待されるスクリーンショット（SEO 用代替テキスト）

![automate invoice generation example showing three dynamically named worksheets](/images/invoice-automation.png)

> *画像の alt テキストには主要キーワードを含め、SEO を最適化しています。*

---

## 手順 5: エッジケースと一般的なバリエーション

### OrderId に使用できない文字が含まれる場合は？

Excel のシート名には `\ / ? * [ ] :` を含められません。ID にこれらが含まれる可能性がある場合は、事前にサニタイズしてください。

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

`Order` に計算プロパティを追加します。

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### 元のテンプレートシートを残したい場合は？

`smartMarkerOptions.RemoveTemplate = false;`（デフォルトは `true`）と設定すれば、`InvoiceTemplate` が参照用として残ります。

### 顧客ごとに請求書をグループ化したい場合は？

**繰り返しグループ** を入れ子にできます。まず顧客で繰り返し、次に各顧客シート内で注文を繰り返す、といった形です。構文はやや複雑になりますが、基本は `RepeatWorksheet` と階層を表す命名パターンを組み合わせるだけです。

---

## 完全動作サンプル（すべてのコードを一括掲載）

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

このコードを `Program.cs` に貼り付け、`InvoiceTemplate.xlsx` を同じフォルダーに置けばすぐに実行できます。

---

## FAQ（よくある質問）

**Q: 大量データ（数千件の請求書）でもこの方法は使えますか？**  
A: はい。SmartMarker はデータをストリーム処理するためメモリ効率が高いですが、メモリ使用量は監視してください。限界に達した場合はバッチ処理に分割し、各バッチを別々のブックに書き出すことを検討してください。

**Q: 各請求書にロゴを自動で追加できますか？**  
A: もちろんです。テンプレートシートにロゴ画像を配置しておけば、シートが複製されるたびにロゴも自動的にコピーされます。

**Q: ワークシートを保護したい場合は？**  
A: 処理後に `wb.Worksheets` をループし、`ws.Protect(Password, ProtectionType.All)` を呼び出します。

---

## まとめ

SmartMarker の **繰り返しワークシート機能** と **巧妙な命名パターン** を活用して、**請求書自動生成** を実現しました。本チュートリアルでは **ワークシートの命名方法**、**ワークシートを繰り返す方法**、そして **動的ワークシート命名** を中心に解説し、データ取得からテンプレート設定、`SmartMarkerOptions` の構成、エッジケースの対処まで、実用的なソリューションを提供しました。

次のステップとして、明細テーブルの追加、条件付き書式の適用、あるいは同データを PDF にエクスポートして完全自動化された請求フローを構築してみてください。

さらにレベルアップしたい方は、「Aspose.Cells を使った大量 Excel エクスポート」や「ワークシートの PDF 変換」や「C# から生成した請求書をメール送信」などの関連トピックを探求してみましょう。可能性は無限大です—ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}