---
category: general
date: 2026-06-21
description: JSON を Excel にすばやくインポートし、JSON を XLSX に変換する方法、JSON から Excel を生成する方法、JSON
  をスプレッドシートにエクスポートする方法を、簡単な手順で学びましょう。
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: ja
og_description: JSONを簡単にExcelにインポート。このガイドでは、JSONをXLSXに変換し、JSONからExcelを生成し、C#を使用してJSONをスプレッドシートにエクスポートする方法を紹介します。
og_title: Aspose.CellsでJSONをExcelにインポートする完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Aspose.CellsでJSONをExcelにインポート – 完全プログラミングガイド
url: /ja/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSON を Excel にインポート – 完全プログラミングガイド

**JSON を Excel にインポート**する方法をカスタムパーサーを書かずに知りたくありませんか？同じ悩みを抱える開発者は多いです。JSON ペイロードをレポートやデータ分析用の整ったスプレッドシートに変換しなければならないとき、壁にぶつかることがよくあります。朗報です！Aspose.Cells を使えば、数行のコードで **JSON を XLSX に変換**でき、処理は高速かつ型安全です。

このチュートリアルでは、**JSON から Excel を生成**し、結果を `.xlsx` ファイルとして保存するまでの手順をすべて解説します。また、ソースデータを変更したときに自動的に更新されるスプレッドシートへのエクスポートなど、便利なバリエーションも紹介します。最後まで読めば、任意の .NET プロジェクトに組み込める再利用可能なスニペットが手に入ります。

## 前提条件

作業を始める前に以下を用意してください。

- .NET 6.0 以降（コードは .NET Framework でも動作します）
- 有効な Aspose.Cells for .NET ライセンス、または一時的な評価キー
- Visual Studio 2022（またはお好みの C# IDE）
- JSON 構造と C# 文法の基本的な知識

**Aspose.Cells** 以外の NuGet パッケージは不要なので、セットアップは軽量です。

## 手順 1: Aspose.Cells をインストールしプロジェクトを設定

まずは Aspose.Cells ライブラリをプロジェクトに追加します。Package Manager Console を開き、次のコマンドを実行してください。

```powershell
Install-Package Aspose.Cells
```

.NET CLI を使用する場合は以下のコマンドです。

```bash
dotnet add package Aspose.Cells
```

> **プロのコツ:** インストール後、ライセンスファイル（`Aspose.Cells.lic`）をプロジェクトのルートに配置し、起動時に読み込んでおきましょう。

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

これで **JSON を Excel にインポート**する準備が整いました。

## 手順 2: JSON ペイロードを用意

デモ用にシンプルな人物オブジェクトの配列を使用します。実際のシナリオでは、ファイル、API のレスポンス、またはデータベースから文字列を取得することになるでしょう。

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

JSON がフラットな配列であることに注目してください。これは Aspose.Cells のスマートマーカーと相性が抜群です。

## 手順 3: JSON 読み込みオプションを設定

Aspose.Cells では、JSON 配列全体を *単一* のデータソースとして扱うことができます。これにより、ワークシート内の行が自動的に拡張されます。

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

`ArrayAsSingle = true` を設定すると、ライブラリは配列の各要素に対して繰り返し適用されるスマートマーカーを生成します。これが **JSON を XLSX に変換**するワークフローの核心です。

## 手順 4: ワークブックを作成し JSON をインポート

新しい `Workbook` インスタンスを作成し、スマートマーカー名 `"People"` を使って JSON をインポートします。

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

内部では、Aspose.Cells が JSON を解析し、各プロパティ（`Name`、`Age`）を列にマッピングし、後で行に展開されるプレースホルダーを用意します。

## 手順 5: ワークシートにスマートマーカーを配置

スマートマーカーは `{{People}}` のように記述します。ワークブックを保存すると、Aspose.Cells がこのマーカーを JSON 配列の全データを含むテーブルに置き換えます。

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

マーカーは好きな場所に配置可能です。左上隅は、テーブルが下方向・右方向に伸びる余地が確保できるため、一般的な選択肢です。

## 手順 6: ワークブックを XLSX ファイルとして保存

最後にワークブックをディスクに書き出します。ここで **JSON を Excel として保存**し、Excel、Google Sheets、その他のスプレッドシートアプリで開ける本物の `.xlsx` ファイルが生成されます。

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`JsonSingleCell.xlsx` を開くと、次のような内容が表示されます。

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

これが **JSON から Excel を生成**した結果です。

## 完全動作サンプル

すべてをまとめた、すぐに実行できるプログラムは以下の通りです。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### 期待される出力

プログラムを実行すると次がコンソールに表示されます。

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

ファイルを開くと、ヘッダー **Name** と **Age** を持つ 2 行のテーブルが、元の JSON 配列と完全に一致していることが確認できます。

## 応用バリエーション

### 1. 複数の JSON 配列を別シートにインポート

例えば `"Employees"` と `"Departments"` という配列がある場合、各配列を別々のワークシートにインポートできます。

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

これで **JSON をスプレッドシートにエクスポート**し、タブごとに異なるデータセットを持つブックが完成します。

### 2. 生成されたテーブルにスタイルを適用

データが展開された後にスタイルを適用できます。

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

この小さな調整でヘッダー行が目立ち、レポート用ダッシュボードに最適です。

### 3. 文字列ではなく JSON ファイルを使用

JSON がディスク上にある場合は、まずそれを読み込みます。

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

残りの手順は全く同じなので、任意のソースから **JSON を Excel として保存**できます。

## よくある落とし穴と回避策

- **`ArrayAsSingle` を忘れる** – このフラグが無いと各オブジェクトが別々のデータソースとして扱われ、セルが空になります。配列がトップレベルの場合は必ず設定してください。
- **スマートマーカー名の誤り** – マーカー (`{{People}}`) は `DataSourceName` に渡した文字列（`"People"`）と完全に一致する必要があります。タイプミスがあるとプレースホルダーが置き換わりません。
- **ライセンスがロードされていない** – 評価モードでは出力ファイルに透かしが入ります。早めにライセンスをロードして、クリーンなブックを生成しましょう。
- **ファイルパスの権限** – 保護されたフォルダに保存しようとすると例外がスローされます。`Environment.CurrentDirectory` もしくはユーザーが書き込み可能なパスを使用してください。

## プログラムで結果をテストする方法

Excel を開かずにエクスポートが成功したか確認したい場合、最初のセルを読み取ってみましょう。

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

このような簡易コンソールチェックで **JSON を XLSX に変換**が期待通りに動作したことを確認できます。

## まとめ

Aspose.Cells を使った **JSON を Excel にインポート**の全工程を網羅しました。ライブラリのインストール、JSON の準備、スマートマーカーの設定、そして最終的な **JSON を Excel として保存**まで、一連の流れは同じです。**JSON を XLSX に変換**、**JSON から Excel を生成**、あるいは **JSON をスプレッドシートにエクスポート**したい場合でも、スマートマーカーが重い作業を代行してくれます。

スタイリングや複数シート、さらにはランタイムで JSON を再インポートして動的に更新するなど、自由に実験してみてください。次のステップとして、このコードを Web API に組み込み、要求に応じて Excel レポートをストリームで返す実装に挑戦してみましょう（ファイル保存行をストリーム返却に置き換えるだけです）。

ネストした JSON オブジェクトや大規模データセットに関する質問があれば、下のコメント欄で遠慮なくどうぞ。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Efficiently Import JSON to Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Effortlessly Import JSON into Excel using Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}