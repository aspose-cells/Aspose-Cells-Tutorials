---
category: general
date: 2026-07-03
description: Excelブックを作成し、プログラムでデータを書き込む。プログラムでExcelファイルを生成し、特定のセルに値を入力し、Excelブックをディレクトリに保存する方法を学ぶ。
draft: false
keywords:
- create excel workbook and write data
- generate excel file programmatically
- put value into specific excel cell
- save excel workbook to directory
language: ja
og_description: C#でExcelブックを作成し、データを書き込む。このガイドでは、プログラムでExcelファイルを生成し、特定のセルに値を入力し、Excelブックをディレクトリに保存する方法を示します。
og_title: Excelワークブックを作成してデータを書き込む – 完全C#チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create excel workbook and write data programmatically. Learn how to
    generate excel file programmatically, put value into specific excel cell, and
    save excel workbook to directory.
  headline: Create Excel Workbook and Write Data in C# – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create excel workbook and write data programmatically. Learn how to
    generate excel file programmatically, put value into specific excel cell, and
    save excel workbook to directory.
  name: Create Excel Workbook and Write Data in C# – Full Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| A | B | C | |-------|---|---| | ["A","B","C"] | | |'
  - name: Writing Multiple Cells
    text: 'If you need to write more than one value, simply repeat the `PutValue`
      call with different addresses:'
  - name: Using a Different Sheet
    text: 'You can add a new sheet and target it:'
  - name: Handling Large JSON Payloads
    text: When the JSON string exceeds typical cell limits (32,767 characters), consider
      storing it in a hidden sheet or splitting it across cells. Excel will truncate
      anything longer, so plan accordingly.
  - name: Saving to a Stream (e.g., HTTP Response)
    text: 'Instead of writing to disk, you can stream the workbook directly to the
      client:'
  type: HowTo
tags:
- C#
- Excel Automation
- Aspose.Cells
title: C#でExcelブックを作成しデータを書き込む – 完全ステップバイステップガイド
url: /ja/net/excel-workbook/create-excel-workbook-and-write-data-in-c-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel ワークブックを作成しデータを書き込む – 完全ステップバイステップガイド

Excel を自分で開かずに **Excel ワークブックを作成しデータを書き込む** 方法を考えたことはありませんか？ あなただけではありません—開発者は JSON やログ、計算結果をそのままスプレッドシートにダンプしたいと常に思っています。良いニュースは、数行の C# で Excel ファイルを生成し、JSON 配列を単一セルに入れ、好きな場所に保存できるということです。

このチュートリアルでは、ワークブックの初期化から **特定の Excel セルに値を入れる**、そして最終的に **Excel ワークブックをディレクトリに保存する** までの全プロセスを順に解説します。最後まで読めば、任意の .NET プロジェクトに貼り付けられる再利用可能なスニペットが手に入ります。余計な説明は省き、すぐに実行できる実践的なコードだけをご紹介します。

## 学べること

- Aspose.Cells ライブラリ（または互換 API）を使って **プログラムで Excel ファイルを生成** する方法  
- **特定の Excel セルに値を入れる** 手順—JSON 文字列の取り扱いも含む  
- カスタムファイル名で **Excel ワークブックをディレクトリに保存** する方法  
- オブジェクトの破棄忘れなどの一般的な落とし穴と、コードをクリーンに保つコツ  
- Visual Studio にそのまま貼り付けて実行できる **完全なサンプル**  

> **前提条件**  
> • .NET 6.0 以降（コードは .NET Core と .NET Framework でも動作）  
> • NuGet パッケージ `Aspose.Cells`（無料トライアルあり）  
> • C# の基本構文に慣れていること  

さあ、手を動かしてみましょう。

![Diagram showing the flow to create excel workbook and write data programmatically](excel-workflow.png)

*画像代替テキスト: Excel ワークブックを作成しデータを書き込むフロー図*

## 手順 1: プロジェクトのセットアップと Excel ライブラリの追加

**プログラムで Excel ファイルを生成** するには、Excel のファイル形式を扱えるライブラリが必要です。`Microsoft.Office.Interop.Excel` を使うこともできますが、サーバーに Excel がインストールされている必要があり、ほとんどの Web アプリでは NG です。その代わりに、純粋なマネージド .NET ライブラリである **Aspose.Cells** を使用します。

```csharp
// Install via NuGet Package Manager Console
// PM> Install-Package Aspose.Cells

using Aspose.Cells;   // Namespace that contains Workbook, Worksheet, etc.
using System;        // For basic .NET types
```

> **プロのコツ:** CI/CD パイプラインを利用している場合は、`.csproj` にパッケージ参照を追加しておくと、ビルド時に自動で復元されます。

## 手順 2: **Excel ワークブックを作成しデータを書き込む** – ワークブックの初期化

ライブラリの準備ができたら、いよいよ **Excel ワークブックを作成しデータを書き込む** です。ワークブックはノートブックに例えることができ、最初のページ（ワークシート）は自動的に作成されます。

```csharp
// Step 2: Initialize a new workbook (the notebook)
Workbook workbook = new Workbook();                // Creates an empty .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];      // Grab the first (default) worksheet
```

`Worksheets[0]` を取得するのはなぜか？ Aspose はデフォルトで「Sheet1」というシートを 1 枚作成します。シンプルなタスクならこの 1 枚で十分です。必要に応じて後からシートを追加できます。

## 手順 3: **特定の Excel セルに値を入れる** – JSON 配列を書き込む

JSON 配列 `["A","B","C"]` をセル **A1** に格納したいとします。これが **特定の Excel セルに値を入れる** 典型例です。

```csharp
// Step 3: Define the JSON string you want to store
string jsonArray = "[\"A\",\"B\",\"C\"]";

// Step 4: Write the JSON string into cell A1
worksheet.Cells["A1"].PutValue(jsonArray);
```

注意点は次の通りです：

- `PutValue` はデータ型を自動判別します。文字列を渡すとテキストとして保存されます。  
- 数値、日付、数式などを保存したい場合も、対応する .NET 型を渡すだけで `PutValue` が処理してくれます。

## 手順 4: **Excel ワークブックをディレクトリに保存** – ファイルの永続化

最後のピースは **Excel ワークブックをディレクトリに保存** です。アプリが書き込み権限を持っている場所ならどこでも保存可能です—ローカルディスク、ネットワーク共有、あるいはクラウドマウントフォルダでも構いません。

```csharp
// Step 5: Define the output path (adjust as needed)
string outputPath = @"C:\Temp\SmartMarker.xlsx";

// Step 6: Save the workbook to the specified file
workbook.Save(outputPath);
```

`Save` が完了すると、`C:\Temp\SmartMarker.xlsx` に完全なファイルが生成されます。Excel で開くと、JSON 文字列がセル A1 にきれいに配置されているはずです。

### 期待される出力

|   A   | B | C |
|-------|---|---|
| ["A","B","C"] |   |   |

これで完了です—JSON が Excel スプレッドシートの一部となり、下流処理や人間のレビューにすぐ使えます。

## 完全動作サンプル（コピー＆ペースト可能）

以下は **完全に実行可能なプログラム** です。新しいコンソールアプリ プロジェクトに貼り付けて **F5** を押すだけで動作します。

```csharp
using System;
using Aspose.Cells;   // Make sure Aspose.Cells is installed via NuGet

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook and get its first worksheet
            Workbook workbook = new Workbook();                 // create excel workbook and write data
            Worksheet worksheet = workbook.Worksheets[0];       // first (default) sheet

            // 2️⃣ Define the JSON array you want to store
            string jsonArray = "[\"A\",\"B\",\"C\"]";

            // 3️⃣ Write the JSON string into cell A1 (put value into specific excel cell)
            worksheet.Cells["A1"].PutValue(jsonArray);

            // 4️⃣ Save the workbook to a file (save excel workbook to directory)
            string outputPath = @"C:\Temp\SmartMarker.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Excel file successfully saved to: {outputPath}");
        }
    }
}
```

**実行**すると、コンソールにファイルの保存場所が表示されます。ファイルを開き、セル **A1** に JSON 配列が入っていることを確認してください。

## よくあるバリエーションとエッジケース

### 複数セルへの書き込み

複数の値を書き込みたい場合は、アドレスを変えて `PutValue` を繰り返すだけです：

```csharp
worksheet.Cells["B2"].PutValue(123);          // numeric value
worksheet.Cells["C3"].PutValue(DateTime.Now); // date/time
```

### 別シートの利用

新しいシートを追加して対象シートを変更することもできます：

```csharp
int newSheetIndex = workbook.Worksheets.Add();
Worksheet newSheet = workbook.Worksheets[newSheetIndex];
newSheet.Name = "DataExport";
newSheet.Cells["A1"].PutValue(jsonArray);
```

### 大容量 JSON ペイロードの取り扱い

JSON 文字列がセルの上限（32,767 文字）を超える場合は、非表示シートに保存するか、複数セルに分割して格納してください。Excel はそれ以上の長さを切り捨ててしまうため、事前に計画が必要です。

### ストリームへの保存（例: HTTP レスポンス）

ディスクに書き込む代わりに、ワークブックを直接クライアントへストリーム送信できます：

```csharp
using (MemoryStream ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    // Return ms.ToArray() as a file download in ASP.NET Core
}
```

## プロのコツ & 注意点

- 高スループットサービスでは、**ワークブックを必ず破棄** してください。Aspose はメモリ管理が優秀ですが、`using` ブロックで囲むとリークを防げます：

  ```csharp
  using (Workbook workbook = new Workbook())
  {
      // ... work with workbook
  }
  ```

- **ファイル権限** に注意。`Save` が `UnauthorizedAccessException` を投げたら、フォルダの存在とプロセスユーザーの書き込み権限を再確認してください。  
- **バージョン互換性**：Aspose.Cells 23.x は .NET 6、.NET 5、.NET Framework 4.6+ と互換です。セキュリティパッチのため、常に最新の安定版 NuGet を参照しましょう。

## まとめ

**Excel ワークブックを作成しデータを書き込む** に必要なすべてを網羅しました：

1. Aspose.Cells をインストールし参照する。  
2. `Workbook` をインスタンス化して **プログラムで Excel ファイルを生成**。  
3. `Cells["A1"].PutValue` で **特定の Excel セルに値を入れる**。  
4. `workbook.Save` で **Excel ワークブックをディレクトリに保存**。

このシンプルな 4 ステップで、レポート自動化、ログエクスポート、下流分析パイプラインへのデータ供給が、Excel の UI に触れることなく実現できます。

## 次に学ぶべきこと

- **セルの書式設定**（フォント、色、罫線）で出力を見栄え良くする。  
- **テーブルやチャートの追加**で視覚的にリッチなレポートを作成。  
- **既存ワークブックの読み取り**で、毎回新規作成せずにデータを更新。

これらのトピックは、今回の基礎の上に直接構築できるので、ぜひ次に挑戦してみてください。

---

*Happy coding! If you hit any snags or have ideas for extensions, drop a comment below—let’s keep the conversation going.*

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するテーマを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Aspose.Cells for .NET を使用して Excel ワークブックを ODS として作成・保存する方法](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Aspnet Aspose Cells で Excel ワークブックを PDF に保存する](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Aspose Cells Dotnet で Excel ワークブックを作成・保存する](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}