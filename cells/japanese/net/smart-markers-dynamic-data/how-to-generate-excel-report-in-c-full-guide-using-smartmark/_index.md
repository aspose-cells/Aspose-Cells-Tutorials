---
category: general
date: 2026-03-22
description: C#でマスタ‑デティールテンプレートを使用してExcelレポートを生成する方法。SmartMarkerを使って繰り返しシートを作成し、Excelテンプレートへのデータ投入を迅速に学びましょう。
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: ja
og_description: 再利用可能なテンプレートを使用してC#でExcelレポートを生成する方法。ステップバイステップのガイドで、マスターディテールデータを用いてC#のExcelテンプレートにデータを入力する手順を示します。
og_title: C#でExcelレポートを生成する方法 – 完全なSmartMarkerチュートリアル
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: C#でExcelレポートを生成する方法 – SmartMarkerを使用した完全ガイド
url: /ja/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でExcelレポートを生成する方法 – SmartMarkerを使用した完全ガイド

セルごとにコードを書き続けることなく、C#で **Excelレポートを生成する方法** を考えたことはありませんか？ あなただけではありません。多くの開発者は、注文と明細のようなマスタ‑詳細関係を反映した洗練されたマルチシートレポートが必要になると壁にぶつかりますが、毎回車輪の再発明はしたくありません。

朗報です。既成のExcelテンプレートと Aspose.Cells の **SmartMarker** エンジンを使えば、数行のコードで **populate Excel template C#** が可能です。このチュートリアルでは実践的なシナリオを順に解説し、各ステップの重要性を説明し、すぐにコピー＆ペーストできる完全な実行可能サンプルを提供します。

> **得られるもの:** 各注文が独自のワークシートを生成するマスタ‑詳細Excelレポートで、すべてプレーンな C# オブジェクトで駆動します。セルを手動でループする必要も、壊れやすい数式もなく、クリーンで保守しやすいコードです。

---

## 前提条件

- **.NET 6.0**（またはそれ以降）がインストールされていること – コードは .NET 6 を対象としていますが、.NET Framework 4.7+ でも動作します。
- **Aspose.Cells for .NET** NuGet パッケージ (`Install-Package Aspose.Cells`) – これにより `Workbook`、`SmartMarkerProcessor`、その他のクラスが利用可能になります。
- `YOUR_DIRECTORY` に配置された **MasterDetailTemplate.xlsx** という名前の Excel ファイル。最初のシートに `{{Orders.OrderId}}` のような SmartMarker ブロックがあり、明細行には `{{Orders.Items.Prod}}` の入れ子ブロックが含まれている必要があります。
- C# の匿名型に関する基本的な理解 – これを使用して注文と明細をモデル化します。

これらのいずれかが馴染みがない場合でも心配ありません。後ほど代替手段（例：EPPlus の使用）について触れますが、基本的な概念は変わりません。

## 手順 1: SmartMarker ブロックを保持する Excel テンプレートをロードする

最初に行うのはテンプレートファイルを開くことです。テンプレートは骨格と考えてください。SmartMarker が後で実データで肉付けします。

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**この重要性:** レイアウト（テンプレート）とデータ（C# オブジェクト）を分離することで、デザイナーも開発者も満足できます。デザイナーはコードに触れずにフォントや色、数式を調整できます。

## 手順 2: マスタ‑詳細データソースを構築する

次に、テンプレートに入力するデータを作成します。典型的な注文レポートでは、注文のコレクションがあり、各注文はそれぞれの明細コレクションを持ちます。

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **プロのコツ:** 複数のレポートで再利用が必要な場合は、匿名型の代わりに強く型付けされたクラスを使用してください。匿名型は例を簡潔に保つためのアプローチです。

**この重要性:** SmartMarker はプロパティ名（`Orders`、`OrderId`、`Items`、`Prod`、`Qty`）とテンプレート内のプレースホルダーを照合して動作します。階層が正確に一致しないと、エンジンはそのセクションをスキップします。

## 手順 3: SmartMarker にマスターレコードごとに新しいシートを作成させる

デフォルトでは SmartMarker はすべての行を単一シートに書き込みます。ここでは各注文を個別のワークシートにしたいので、後で印刷や注文ごとの PDF メール送信に最適です。

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**この重要性:** `EnableRepeatingSheet` を使用すると、手動でシートをクローンする必要がなくなります。エンジンは元のシートをコピーし、注文データを注入し、シート名を自動的に（通常は最初の列の値を使用して）リネームします。

## 手順 4: データでテンプレートを処理する

ここで全てを結びつけます。`SmartMarkerProcessor` がブック全体を走査し、タグを置換し、指示通りに新しいシートを作成します。

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**この重要性:** この1行で重い処理を行います—テンプレートの解析、コレクションの反復、入れ子テーブルの処理です。手動ループなしで **populate Excel template C#** の核心となります。

## 手順 5: 完成したレポートを保存する

最後に、データが入ったワークブックをディスクに書き出します。Web アプリの場合は、直接 HTTP 応答にストリームすることも可能です。

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**この重要性:** ファイルに保存することで、Excel で開いたり、ステークホルダーと共有したり、PDF 変換などの下流プロセスに渡したりできる具体的な成果物が得られます。

## 完全動作例（コピー＆ペースト可能）

以下は `using` ディレクティブと `Main` メソッドを含む完全なプログラムです。コンソールアプリに貼り付け、ファイルパスを調整して実行してください。

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### 期待される出力

`MasterDetailResult.xlsx` を開くと、以下が確認できます：

- **シート “Order_1”** – 注文 1 のヘッダーと製品 A と B の 2 行が含まれます。
- **シート “Order_2”** – 注文 2 のヘッダーと製品 C の 1 行が含まれます。
- 元のテンプレートのすべての数式、書式設定、チャートが保持されています。

![各注文ごとに別々のシートがあるExcelレポート – 生成されたワークブックの例](/images/excel-report-example.png "マスタ‑詳細データを含む生成されたExcelレポート")

*画像の代替テキスト: 各注文ごとに別々のシートがある生成されたExcelレポート、C# と SmartMarker を使用して Excel レポートを生成する方法を示しています。*

## よくある質問とエッジケース

### 繰り返しシートと併せて静的シート（例：サマリー）が必要な場合は？

`EnableRepeatingSheet = true` をマスターブロックを含むワークシート **のみ** に設定します。他のシートは変更されないため、元のテンプレートにサマリーページを保持できます。

### 匿名オブジェクトの代わりに DataTable を使用できますか？

もちろんです。SmartMarker は `IEnumerable` を実装する任意のオブジェクトで動作します。匿名型を `DataTable` に置き換え、列名がタグと一致していることを確認してください。

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### 生成されたシートの命名規則を変更するには？

`ISmartMarkerSheetNaming` インターフェイスをカスタム実装する（または処理後に `workbook.Worksheets` を操作する）ことで実現できます。多くの開発者はセルの値に基づいてシート名を変更します：

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### テンプレートが別のプレースホルダー構文を使用している場合は？

SmartMarker は `SmartMarkerOptions` を使用してカスタム区切り文字を設定できます。例えば、`{{ }}` の代わりに `<< >>` を使用する場合は次のようにします：

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

## このアプローチをスケールするためのヒント

- **テンプレートをメモリにキャッシュ** してください。リクエストごとに多数のレポートを生成する場合、毎回ディスクから読み込むと遅延が増えます。
- **PDF 変換と組み合わせる**（`workbook.Save("report.pdf", SaveFormat.Pdf)`）ことで、メールフレンドリーな出力が得られます。
- **ファイルパスをパラメータ化** し、設定ファイルや環境変数を使用して、開発・テスト・本番間で移植性を確保します。
- **データ層を個別にユニットテスト** してください。SmartMarker 自体は決定的なので、提供するデータが期待されるスキーマと一致しているかを検証すれば十分です。

## 結論

C# で **Excelレポートを生成する方法** をエンドツーエンドで解説しました。SmartMarker 対応テンプレートのロードから、マスタ‑詳細関係を反映したマルチシートブックの保存まで。数行のコードで **populate Excel template C#** を行うことで、壊れやすいセル単位のロジックを回避し、デザイナーに最終的な外観を自由に設計させることができます。

次に検討できること：

- シートごとに自動更新されるチャートと共に **populate Excel template C#** を使用する。
- **excel smartmarker c#** を ASP.NET Core と統合し、レポートをブラウザへ直接ストリームする。
- API やデータベースからデータを取得する **c# excel automation** パイプラインを自動化する。

ぜひ試してみて、テンプレートを調整し、生データを洗練された Excel レポートに変換できる速さを体感してください。質問や面白いユースケースがあれば、下のコメント欄にどうぞ—ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}