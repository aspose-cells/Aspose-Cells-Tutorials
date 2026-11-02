---
category: general
date: 2026-03-18
description: C#でJSONからExcelを生成し、シート名の重複を許可し、詳細シートを作成し、数分でブックを保存する方法を学びましょう。
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: ja
og_description: C# を使用して JSON から Excel を生成する。このガイドでは、シート名の重複を許可し、詳細シートを作成し、Aspose.Cells
  を使用して C# でブックを保存する方法を示します。
og_title: C#でJSONからExcelを生成する – 完全チュートリアル
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: C#でJSONからExcelを生成する – ステップバイステップガイド
url: /ja/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で JSON から Excel を生成する – ステップバイステップ ガイド

**JSON から Excel を生成**したいけど、どのライブラリが適切か分からないことはありませんか？企業向けアプリでは、JSON 形式のペイロードを受け取り、売上レポートや在庫ダンプ、監査ログなどの整形されたスプレッドシートにデータを流し込む必要があります。朗報です！Aspose.Cells の SmartMarker エンジンを使えば、JSON 文字列を数行のコードで完全な Excel ファイルに変換できます。

このチュートリアルでは、JSON ペイロードの準備、**シート名の重複を許可**する SmartMarker の設定、**詳細シート**の作成、そして **C# スタイルでブックを保存**するまでの全工程を解説します。最後まで読めば、任意の .NET プロジェクトに組み込める再利用可能なコードスニペットが手に入ります。

> **クイックリキャップ:**  
> • 主目的 – JSON から Excel を生成する。  
> • 副目的 – シート名の重複を許可、詳細シートを作成、C# でブックを保存。  

## 前提条件

作業を始める前に以下を用意してください。

- .NET 6.0 SDK（またはそれ以降の .NET バージョン）。  
- Visual Studio 2022 または C# 拡張機能付き VS Code。  
- **Aspose.Cells for .NET** の有効ライセンスまたは無料トライアル（NuGet パッケージは `Aspose.Cells`）。  
- SmartMarker タグ（例: `&=Name`）と詳細テーブル用プレースホルダーが埋め込まれたテンプレート Excel ファイル（`template.xlsx`）。

これらが初めてでも心配はいりません。NuGet パッケージのインストールはワンコマンドで済み、テンプレートはプレースホルダーセルだけが入った普通のブックでも構いません。

## ソリューションの概要

全体の流れは次の通りです。

1. シートに反映したいデータを表す JSON 文字列を定義する。  
2. `SmartMarkerOptions` を設定し、シート名の重複を許可し、**詳細シート**に予測可能な名前を付ける。  
3. SmartMarker タグが入った Excel テンプレートを読み込む。  
4. SmartMarker プロセッサを実行して JSON データをブックにマージする。  
5. `workbook.Save(...)` で最終ファイルを保存する。

各ステップは以下で詳しく解説し、コードスニペットとその意図を併せて示します。

---

## Step 1 – マージする JSON ペイロードを用意する

まずはテンプレート内の SmartMarker タグに対応した JSON ドキュメントを用意します。JSON が真実の情報源となり、キーが Excel のプレースホルダーにマッピングされます。

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**このステップが重要な理由:**  
SmartMarker は JSON の階層構造を読み取り、`Orders` のようなコレクションに対して自動的にテーブルを展開します。JSON の構造がタグと合致していないと、マージ時に空行が生成されるという典型的な落とし穴が発生します。

---

## Step 2 – シート名の重複を許可し、詳細シートの名前を設定する

デフォルトでは Aspose.Cells はシート名の重複を禁止しますが、マスターレコードごとに詳細シートを生成したい場合は障壁になります。`SmartMarkerOptions` クラスを使ってこの制限を緩め、さらに新規作成される詳細シートの命名パターンを指定できます。

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**このステップが重要な理由:**  
複数の顧客をループ処理し、各イテレーションで新しいシートを作成すると、エンジンは例外を投げます。`AllowDuplicateSheetNames` を `true` に設定すれば、Aspose.Cells は自動的に数値サフィックスを付与し、処理をスムーズに続行できます。

---

## Step 3 – SmartMarker タグが入った Excel テンプレートを読み込む

テンプレートは SmartMarker がデータを書き込むキャンバスです。色、数式、チャートなど任意の書式を保持できるため、プログラム側で同じロジックを再現する必要はありません。

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Tip:**  
テンプレートはプロジェクトの出力フォルダーに含める（例: `Content\Templates`）と、相対パスで参照でき、絶対パスをハードコーディングする手間が省けます。

---

## Step 4 – JSON とオプションを使って SmartMarker プロセッサを実行する

いよいよ魔法の瞬間です。`SmartMarkerProcessor` が JSON を読み取り、設定したオプションを尊重しながらブックにデータを埋め込みます。

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**内部で何が起きているか:**  
- プロセッサは全セルを走査し、`&=Name` や `&=Orders.Item` といったマーカーを検出。  
- スカラー値（`Name`、`Date`）は単純マーカーに置換。  
- コレクション（`Orders`）に対しては新しい詳細シート（名前は “Detail”）を作成し、各アイテムの行をテーブルに追加。  
- シート名の重複が許可されているため、テンプレートに既に “Detail” シートが存在すれば “Detail (2)” が生成されます。

---

## Step 5 – マージ済みブックをディスクに保存する

最後に、データが埋め込まれたブックをファイルとして書き出します。Aspose.Cells がサポートする任意の形式（XLSX、CSV、PDF など）で保存可能です。ここでは最新の XLSX 形式を使用します。

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**このステップが重要な理由:**  
ここが **C# スタイルでブックを保存** する箇所です。Web クライアントへストリームで返す場合は `workbook.Save(Stream, SaveFormat.Xlsx)` を利用します。

---

## 完全動作サンプル

すべてを統合した、すぐに実行できるコンソールアプリの例です。コンパイル前に `Aspose.Cells` NuGet パッケージ（`dotnet add package Aspose.Cells`）をインストールしてください。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### 期待される結果

- **Sheet 1**（マスターシート）には `Name` セルに “John”、`Date` セルに “2023‑01‑01” が表示されます。  
- 新規 **Detail** シートが作成され、Laptop の注文と Mouse の注文の 2 行がテーブルとして格納されます。  
- テンプレートに既に “Detail” シートが存在した場合、`AllowDuplicateSheetNames` フラグのおかげで新シートは “Detail (2)” と命名されます。

![Excel 出力例：マスターシートに名前と日付、Detail シートに注文行が表示された画像](excel-output.png "generate excel from json result")

*画像代替テキスト:* **JSON から Excel を生成 – マスターシートと詳細シートを持つサンプルブック**

---

## よくある質問とエッジケース

### JSON に入れ子のコレクションが含まれる場合は？

SmartMarker は入れ子配列も処理できますが、追加の詳細シートを用意するか、階層マーカーを使用する必要があります。例として `&=Orders.SubItems.Product` と記述すれば、3 階層目のシートが自動生成されます。

### 重複シート名の命名パターンをカスタマイズしたい場合は？

固定の `DetailSheetNewName` の代わりに、`smartMarkerOptions.DetailSheetNameGenerator` にコールバックを割り当てれば、タイムスタンプやユニーク ID をシート名に組み込めます。

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### XLSX ではなく CSV を生成したい場合は？

もちろん可能です。最終的な `Save` 呼び出しを次のように置き換えます。

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

それ以外の処理は同一です。

### ASP.NET Core でも動作しますか？

はい。コントローラーアクション内で同じコードを実行できます。ブックをレスポンスにストリームする例は以下です。

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## プロのコツと落とし穴

- **プロのコツ:** SmartMarker タグは別シート（例: “Template”）にまとめておくと、誤って編集されるリスクを減らしつつ、プロセッサは問題なく読み取れます。  
- **注意点:** スペースや特殊文字を含む JSON キーは避けましょう。Aspose.Cells は有効な JavaScript 識別子を期待します。POCO からデシリアライズする場合は `JsonProperty` 属性で名前をマッピングできます。  
- **パフォーマンスのコツ:** 数千行規模の処理では `smartMarkerOptions.EnableCache = true` を設定し、コンパイル済みマーカーを再利用すると高速化します。  
- **バージョン確認:** 本コードは Aspose.Cells 23.9 以降を対象としています。古いバージョンでは `AllowDuplicateSheetNames` が未実装の場合があります。

---

## 結論

これで **C# で JSON から Excel を生成**するためのエンドツーエンドレシピが完成しました。`SmartMarkerOptions` の設定により **シート名の重複を許可**し、**詳細シート**の命名を制御、最終的に **C# スタイルでブックを保存**する方法を実演しました。この手法は外部サービスに依存せず、NuGet パッケージ一つで完結します。

次のステップは、JSON ソースを実際の API に差し替えてみることです。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}