---
category: general
date: 2026-05-23
description: C#でExcelブックを作成し、カスタム数値書式の適用方法、プログラムでセルスタイルを設定する方法、セルを指数表記でフォーマットする方法を学び、最後にブックをxlsx形式で保存します。
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: ja
og_description: C#でExcelブックを素早く作成。カスタム数値書式の適用、セルのプログラムによるスタイリング、指数表記のフォーマット方法を学び、xlsxとして保存します。
og_title: C#でExcelワークブックを作成 – カスタム数値書式を適用
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: C#でExcelブックを作成 – カスタム数値形式を適用
url: /ja/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel ワークブックを作成 – カスタム数値書式を適用

C# で Excel ワークブックを作成するのは思ったより簡単です。このガイドでは、カスタム数値書式の適用、セルを指数表記にフォーマット、プログラムからセルのスタイルを設定、そして最終的にワークブックを xlsx ファイルとして保存する手順を順に解説します。

空白のスプレッドシートを見て「データの投入から数値の見た目まで自動化したい」と考えたことがあるなら、このチュートリアルはあなたのためのものです。最後まで読めば、任意のスプレッドシートプログラムで開ける完全に機能する Excel ファイルが手に入り、**なぜ**その手順が重要なのか、**どうやって**コードを書くかだけでなく理解できるようになります。

## 必要なもの

- **.NET 6+**（またはライブラリをサポートする最近の .NET Framework）  
- **Aspose.Cells for .NET**（または `Workbook`、`Cell`、`CellFormat` クラスを提供する別の API）  
- 基本的な C# の経験 – `Console.WriteLine` が書ければ問題ありません。  

余計な設定ファイルや COM 相互運用は不要ですし、Excel の手動インストールも必要ありません。

---

## Excel ワークブックの作成 – Workbook オブジェクトの初期化

最初に空のワークブックを作成します。`Workbook` クラスは、行・列・スタイルを描くための白紙キャンバスと考えてください。

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

これだけです – 1 行でメモリ上に新しい Excel ファイルが作られます。`Workbook` コンストラクタはデフォルトのワークシートコレクションを生成するので、すぐにデータの追加が可能です。

> **プロのコツ:** 複数シートが必要な場合は、セルにデータを書き込む前に `workbook.Worksheets.Add()` を呼び出してください。

![Create excel workbook example](image-placeholder.png "Create excel workbook screenshot")

*Image alt text: create excel workbook example showing a blank Excel sheet in the IDE.*

## セルにカスタム数値書式を適用

ワークブックができたので、セル **A1** に数値を入れ、カスタム書式を設定しましょう。カスタム数値書式を使うと、通貨・パーセンテージ・日付、あるいは今回のように指数表記といった表示形式を自由に制御できます。

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

なぜ最初にスタイルを取得するのか？ `Cell` オブジェクトは **Style** オブジェクトを保持しており、フォント・罫線・配置・数値書式がすべて一箇所にまとめられています。`Custom` プロパティを編集することで、Excel に「この値は小数点以下 2 桁の指数表記で表示してください」と指示しています。

> **よくある質問:** *組み込みの書式を使うことはできませんか？*  
> はい、組み込みの指数書式は `style.Number = 10` で設定できますが、カスタム文字列を使うと小数点以下の桁数を正確に指定できます。

## プログラムからセルスタイルを設定（数値書式以外）

数値書式だけでなく、太字フォントや薄いグレーの背景色を付けてセルを目立たせたいこともあるでしょう。

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

先ほど調整した同じ `style` オブジェクトを再利用しています。これが **プログラムからセルスタイルを設定** の利点で、スタイルを一度取得すれば必要なプロパティだけ変更して書き戻すだけです。オブジェクトを再生成したり、すでに設定した数値書式を失う心配はありません。

## 指数表記でセルをフォーマット（エッジケース対応）

非常に大きな数や非常に小さな数を扱う場合、指数表記は必須です。今回使用したカスタム書式 (`0.00E+00`) は小数点以下 2 桁を保証し、指数部に必ずプラス記号を付けます。簡単な検証例を示します。

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

生成されたファイルを開くと、B2 が `1.23E-05` と表示され、**指数表記のセルフォーマット** が大きな数でも小さな数でも正しく機能していることが確認できます。

## ワークブックを XLSX として保存

楽しい作業は、実際にファイルを書き出すときに終わります。`Save` メソッドが重い処理を担い、メモリ上の表現を正しい `.xlsx` パッケージに変換します。

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

この一行で **XLSX にワークブックを保存** する目的が達成されます。保存先ディレクトリが存在しない場合は `Save` が例外をスローするので、事前にフォルダーを作成するか、try/catch で囲んでください。

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

これで、科学的表記が適用された数値、太字スタイル、薄いグレーの背景が付いた、共有可能な Excel ファイルが完成です。

## 完全な動作サンプル

以下は、すべてのパーツを結合したコピー＆ペースト可能なプログラムです。コンソールアプリとしてコンパイルできますが、任意の C# プロジェクトにロジックを組み込んでも構いません。

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**期待される結果:** `CustomFormatted.xlsx` を開くと次のように表示されます。

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

両セルとも太字で、薄いグレーの塗りつぶしが施され、数値は小数点以下 2 桁の指数表記で表示されます。

---

## まとめ

私たちは **Excel ワークブックを作成** し、**カスタム数値書式を適用**、**指数表記でセルをフォーマット**、**プログラムからセルスタイルを設定**、そして **XLSX に保存** する一連の手順を、数行の C# で実現しました。この手法はスケーラブルです。行をループして `style` オブジェクトをクローンすれば、数秒で完全にスタイルが適用されたレポートが作れます。

### 次にやることは？

- **動的フォーマット:** 値の大きさに応じて書式を切り替える（例: 通貨 vs. パーセンテージ）。  
- **複数シート:** `workbook.Worksheets.Add("Summary")` でダッシュボードを構築。  
- **高度なスタイリング:** 罫線、条件付き書式、データ検証など。

## 関連チュートリアル

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}