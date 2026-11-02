---
category: general
date: 2026-03-25
description: Smart Markers を使用してテンプレートを作成し、行の繰り返し、データのバインド、レポートの生成、テンプレートの簡単作成方法を学ぶ。
draft: false
keywords:
- how to write template
- how to repeat rows
- how to bind data
- how to generate report
- how to create template
language: ja
og_description: Smart Markers を使用したテンプレートの書き方。行の繰り返し、データのバインド、レポートの生成、C# でのテンプレート作成方法をご紹介します。
og_title: スマートマーカーでテンプレートを書く方法 – 完全ガイド
tags:
- Aspose.Cells
- C#
- SmartMarkers
title: スマートマーカーを使用したテンプレートの書き方 – ステップバイステップガイド
url: /ja/net/smart-markers-dynamic-data/how-to-write-template-with-smart-markers-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Smart Markers を使用したテンプレートの書き方 – 完全チュートリアル  

データに基づいて自動的に展開される **テンプレートの書き方** を疑問に思ったことはありませんか？ あなたは一人ではありません—動的な Excel レポートが必要なのに、どの API 機能を使えばよいか分からず壁にぶつかる開発者は多いです。良いニュースは、Aspose.Cells Smart Markers を使えば、単一セルのテンプレートを作成し、階層データをバインドし、ライブラリに行の繰り返しを任せられることです。このガイドでは、**行の繰り返し方法**、**データのバインド方法**、さらには **レポートの生成方法** を、ワークシートを手動でループせずにカバーします。

このチュートリアルの最後までに、マスタ‑詳細シナリオ向けの **テンプレートの作成方法** を示す完全な実行可能サンプルが手に入ります。さらに、エッジケースやパフォーマンスのコツも紹介します。外部ドキュメントは不要です—必要なものはすべてここにあります。

---

## 作成するもの

注文（マスタ）とその明細行（ディテール）を一覧表示する Excel ワークブックを生成します。テンプレートはセル **A1** に配置され、Smart Markers がそれを整ったテーブルに展開します。最終シートは次のようになります：

```
Order1
   A
   B
Order2
   C
```

これは典型的な「レポートの生成方法」シナリオで、コードは .NET 6+ と Aspose.Cells 23.x（以降）で動作します。

---

## 前提条件

- .NET 6 SDK（または最近の .NET バージョン）  
- Visual Studio 2022 または VS Code  
- Aspose.Cells for .NET（NuGet でインストール: `Install-Package Aspose.Cells`）  

これらが揃っていれば、すぐに始められます。

---

## Step 1: プロジェクトのセットアップと Aspose.Cells の追加  

```csharp
// Create a new console app (run this in a terminal)
// dotnet new console -n SmartMarkerDemo
// cd SmartMarkerDemo
// dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook with a single worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
```

*Why this matters*: 新しい `Workbook` から始めることで、クリーンなキャンバスが保証されます。`Worksheet` オブジェクトはテンプレートを配置する場所です。

---

## Step 2: Smart Marker テンプレートの作成  

テンプレートは注文タイトルに `${Master.Name}` を、各明細行を繰り返すために `${Detail:Repeat}` を使用します。

```csharp
            // Step 2: Define a Smart Marker template that repeats detail rows for each master record
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";
            
            // Write the template into cell A1
            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);
```

> **Pro tip**: テンプレートは単一セルに保管してください。Smart Markers が自動的に行に展開します。  

*How this solves the problem*: 繰り返しブロックをセル内に直接埋め込むことで、手動で行を挿入する必要がなくなります—Aspose が処理します。

---

## Step 3: テンプレートに合わせた階層データの構築  

データはテンプレートの構造と一致させる必要があります：`Master` コレクションがあり、各要素が `Detail` 配列を持ちます。

```csharp
            // Step 3: Create hierarchical data matching the template structure
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };
```

*Why we bind data this way*: Smart Markers はリフレクション方式のバインディングを使用するため、プロパティ名はプレースホルダーと完全に一致する必要があります。これが動的レポートの **データのバインド方法** の核心です。

---

## Step 4: テンプレートの処理 – Smart Markers に任せて重い作業を実行  

```csharp
            // Step 4: Process the Smart Markers – the template will be expanded using the data above
            worksheet.SmartMarkerProcessor.Process(orderData);
```

処理後、ワークシートには展開された行が含まれます。ループも手動のセル書き込みも不要です。

---

## Step 5: ワークブックの保存  

```csharp
            // Save the result to an XLSX file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

生成されたファイルを開くと、先ほど説明したマスタ‑詳細レイアウトがそのまま表示されます。これは、1 行の処理コードだけで **レポートの生成方法** を実現したものです。

---

## ビジュアル概要  

![Smart Markers によって生成された Excel レポート – テンプレートの書き方](/images/smart-marker-report.png "テンプレートの書き方")

*Alt text*: 「テンプレートの書き方」 – 各注文の繰り返し行が表示された最終 Excel ファイルのスクリーンショット。

---

## 深掘り: Smart Markers がゲームチェンジャーである理由  

### ループなしで行を繰り返す方法  

従来の Excel 自動化では、最終行を計算し、新しい行を挿入し、スタイルをコピーする必要があり、すべてがエラーが起きやすい作業です。Smart Markers はこれを宣言的な `${Detail:Repeat}` ブロックで置き換えます。エンジンはブロックを解析し、コレクションの各要素ごとに行を複製し、値を注入します。この手法は **行の繰り返し方法** を効率的に実現します。

### 複雑なオブジェクトのバインディング  

入れ子オブジェクト、コレクション、あるいは DataTable もバインドできます。プロパティ名が一致している限り、プロセッサはオブジェクトグラフをたどります。これが **データのバインド方法** の本質です：プロセッサに普通の CLR オブジェクト（または今回のように匿名型）を渡すだけで、自動的にマッピングされます。

### 異なるフォーマットの生成  

例では XLSX に保存していますが、`SaveFormat.Pdf` や `SaveFormat.Csv` に一行変更するだけで切り替えられます。これにより、テンプレートを触らずに複数フォーマットで **レポートの生成方法** を迅速に実現できます。

### テンプレートの再利用  

他のワークシート用に **テンプレートの作成方法** が必要な場合は、セルの内容を別シートにコピーするか、文字列リソースに保存するだけです。同じプロセッサ呼び出しがどこでも機能し、コードを DRY かつ保守しやすくします。

---

## よくある質問とエッジケース  

| Question | Answer |
|----------|--------|
| *マスタに明細行がない場合はどうなりますか？* | `${Detail:Repeat}` ブロックはスキップされ、マスタ名だけが残ります。空の行は作成されません。 |
| *繰り返し行にスタイルを適用できますか？* | はい。処理前にテンプレート行（フォント、罫線等）に書式設定を適用してください。書式は生成された各行にコピーされます。 |
| *Workbook を破棄する必要がありますか？* | `Workbook` は `IDisposable` を実装しています。実運用コードでは `using` ブロックで囲んでください。ただし短いコンソールデモの場合は省略可能です。 |
| *データはどの程度の規模まで可能ですか？* | Smart Markers はメモリ効率が高いですが、数十万件といった非常に大規模なコレクションではページングやストリーミングが必要になる場合があります。 |
| *オブジェクトの代わりに JSON ファイルを使用できますか？* | もちろんです。JSON をテンプレートに合わせた POCO にデシリアライズし、`Process` に渡してください。 |

---

## 完全動作例（コピー＆ペースト可能）  

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize workbook
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // Define template
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";

            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);

            // Prepare data
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };

            // Process template
            worksheet.SmartMarkerProcessor.Process(orderData);

            // Save file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

プログラムを実行（`dotnet run`）し、*SmartMarkerReport.xlsx* を開くと、マスタ‑詳細行が整然と配置されているのが確認できます。

---

## まとめ  

ここでは Aspose.Cells Smart Markers を使用した **テンプレートの書き方**、**行の繰り返し方法**、階層オブジェクトによる **データのバインド方法**、そして XLSX（または他のサポート形式）で **レポートの生成方法** を示しました。同じパターンで **テンプレートの作成方法** を請求書、在庫表、または想像できるあらゆるマスタ‑詳細レイアウトに適用できます。

---

## 次にやることは？  

- **出力のスタイル設定**: 処理前にテンプレート行にセルスタイルを適用します。  
- **PDF へのエクスポート**: `SaveFormat.Xlsx` を `SaveFormat.Pdf` に変更して印刷可能なレポートを作成します。  
- **動的ヘッダー**: `${Headers}` プレースホルダーを追加して、列タイトルを動的に生成します。  
- **複数シート**: 追加のワークシートで同様の処理を繰り返し、マルチセクションレポートを作成します。  

自由に試してみてください—データソースを入れ替えたり、ネストレベルを増やしたり、数式と組み合わせたりできます。Smart Markers の柔軟性により、ループコーディングに費やす時間が減り、価値提供に時間を使えます。

*コーディングを楽しんでください！ 問題があれば下にコメントを残すか、`aspose-cells` タグで Stack Overflow にメッセージを送ってください。会話を続けましょう。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}